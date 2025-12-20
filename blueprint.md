# Puskesmas Queue — Laravel 12 + Filament 4 (Admin) + React (Display)

Sederhana, rapi, dan cukup “wow” untuk tugas kuliah. Admin kelola antrian via Filament; layar display React menayangkan nomor yang dipanggil + suara otomatis (“Antrian A-001 ke loket 1”).

---

## 1) Fitur Utama

**Admin (Filament 4)**

- Buat/tutup **Layanan** (Poli Umum, Gigi, KIA, Farmasi, dll.)
- Kelola **Loket/Counter** dan assign layanan.
- **Generate tiket** (ambil nomor), cetak opsional.
- **Panggil tiket** (berikutnya/ulang), pilih loket tujuan.
- Status: Menunggu, Dipanggil, Selesai, Batal.
- **Reset harian** (nomor ulang dari 001 per layanan) — via command + scheduler.
- Laporan ringkas harian.

**Layar Display (React)**

- Tampilkan **tiket berjalan** (current called) + **antrian berikutnya**.
- **Suara otomatis** saat ada panggilan baru.
- Multi-layanan: filter per layanan atau layar gabungan (ticker).
- **Realtime** via Laravel Echo + Reverb (WebSocket) dengan fallback polling.

**API & Realtime**

- REST API sederhana + Broadcast event `TicketCalled`.
- Otentikasi Sanctum untuk endpoint admin (Filament handle), publik-only untuk display.

---

## 2) ERD Ringkas

**services** (id, code, name, prefix, is_active)

**counters** (id, name, service_id, is_active)

**tickets** (id, service_id, number_int, number_str, status [waiting|called|done|cancelled], called_at, counter_id, finished_at)

**calls** (id, ticket_id, counter_id, user_id, type [call|recall], created_at)

**users** (role: administrator|admin|user)

Relasi: service hasMany tickets & counters; counter belongsTo service; ticket belongsTo service + counter; call belongsTo ticket & counter & user.

---

## 3) Migrations (cuplikan penting)

```php
// 2025_10_04_000001_create_services_table.php
Schema::create('services', function (Blueprint $t) {
  $t->id();
  $t->string('code')->unique(); // e.g. POLI-01
  $t->string('name');           // "Poli Umum"
  $t->string('prefix')->default('A'); // tiket: A-001
  $t->boolean('is_active')->default(true);
  $t->timestamps();
});

// 2025_10_04_000002_create_counters_table.php
Schema::create('counters', function (Blueprint $t) {
  $t->id();
  $t->string('name'); // "Loket 1"
  $t->foreignId('service_id')->constrained()->cascadeOnDelete();
  $t->boolean('is_active')->default(true);
  $t->timestamps();
});

// 2025_10_04_000003_create_tickets_table.php
Schema::create('tickets', function (Blueprint $t) {
  $t->id();
  $t->foreignId('service_id')->constrained()->cascadeOnDelete();
  $t->unsignedInteger('number_int'); // 1..999
  $t->string('number_str'); // A-001
  $t->enum('status',["waiting","called","done","cancelled"]) ->default('waiting');
  $t->timestamp('called_at')->nullable();
  $t->foreignId('counter_id')->nullable()->constrained()->nullOnDelete();
  $t->timestamp('finished_at')->nullable();
  $t->timestamps();
  $t->unique(['service_id','number_int']);
});

// 2025_10_04_000004_create_calls_table.php
Schema::create('calls', function (Blueprint $t) {
  $t->id();
  $t->foreignId('ticket_id')->constrained()->cascadeOnDelete();
  $t->foreignId('counter_id')->constrained()->cascadeOnDelete();
  $t->foreignId('user_id')->constrained()->cascadeOnDelete();
  $t->enum('type',["call","recall"])->default('call');
  $t->timestamps();
});
```

---

## 4) Model ringkas

```php
class Service extends Model { use HasFactory; protected $fillable=['code','name','prefix','is_active'];
  public function tickets(){ return $this->hasMany(Ticket::class); }
  public function counters(){ return $this->hasMany(Counter::class); }
}

class Counter extends Model { use HasFactory; protected $fillable=['name','service_id','is_active'];
  public function service(){ return $this->belongsTo(Service::class); }
}

class Ticket extends Model { use HasFactory; protected $fillable=['service_id','number_int','number_str','status','counter_id','called_at','finished_at'];
  protected $casts = ['called_at'=>'datetime','finished_at'=>'datetime'];
  public function service(){ return $this->belongsTo(Service::class); }
  public function counter(){ return $this->belongsTo(Counter::class); }
}

class Call extends Model { use HasFactory; protected $fillable=['ticket_id','counter_id','user_id','type']; }
```

---

## 5) Seeder contoh

```php
Service::factory()->createMany([
  ['code'=>'POLI-UMUM','name'=>'Poli Umum','prefix'=>'A'],
  ['code'=>'POLI-GIGI','name'=>'Poli Gigi','prefix'=>'B'],
  ['code'=>'FARMASI','name'=>'Farmasi','prefix'=>'C'],
]);

Counter::factory()->createMany([
  ['name'=>'Loket 1','service_id'=>1],
  ['name'=>'Loket 2','service_id'=>1],
  ['name'=>'Loket Gigi','service_id'=>2],
  ['name'=>'Farmasi','service_id'=>3],
]);
```

---

## 6) Alur ambil nomor & format tiket

- Saat **Ambil Nomor** (Admin klik tombol di Filament atau endpoint umum, mis. loket resepsionis), cari `max(number_int)` **hari ini** untuk service terkait → +1.
- Bentuk `number_str = prefix . '-' . str_pad(number_int,3,'0',STR_PAD_LEFT)`.

> Opsional: batasi 1..999 per hari; jika habis → layanan ditutup.

---

## 7) Broadcast Event (Realtime)

```php
// app/Events/TicketCalled.php
class TicketCalled implements ShouldBroadcast {
  use Dispatchable, InteractsWithSockets, SerializesModels;
  public function __construct(public Ticket $ticket) {}
  public function broadcastOn(){ return new Channel('queue'); }
  public function broadcastAs(){ return 'ticket.called'; }
  public function broadcastWith(){
    return [
      'id'=>$this->ticket->id,
      'service'=>$this->ticket->service->name,
      'prefix'=>$this->ticket->service->prefix,
      'number_int'=>$this->ticket->number_int,
      'number_str'=>$this->ticket->number_str,
      'counter'=>$this->ticket->counter?->name,
      'called_at'=>optional($this->ticket->called_at)->toIso8601String(),
    ];
  }
}
```

**Konfigurasi Broadcasting (Reverb / Pusher compatible)**

`.env` cuplikan:

```
BROADCAST_CONNECTION=reverb
REVERB_APP_ID=local
REVERB_APP_KEY=local
REVERB_APP_SECRET=local
REVERB_HOST=127.0.0.1
REVERB_PORT=8080
REVERB_SCHEME=http
```

Jalankan: `php artisan reverb:start` (pakai Laravel 12). Alternatif: laravel-websockets/soketi.

---

## 8) Controller/API (publik untuk display)

```php
// routes/api.php
Route::get('/status', [QueueController::class,'status']); // ringkas untuk layar
Route::get('/status/{service}', [QueueController::class,'statusByService']);

// Admin/Resepsionis
Route::post('/tickets', [QueueController::class,'createTicket']);
Route::post('/call/next', [QueueController::class,'callNext']);
Route::post('/call/{ticket}/recall', [QueueController::class,'recall']);
```

```php
// app/Http/Controllers/QueueController.php
class QueueController extends Controller {
  public function status(){
    // Ambil last called per service + next 5 waiting
    $services = Service::with(['tickets'=>fn($q)=>$q->latest('called_at')])->get();
    $payload = [];
    foreach ($services as $s) {
      $current = Ticket::where('service_id',$s->id)->where('status','called')->latest('called_at')->first();
      $next = Ticket::where('service_id',$s->id)->where('status','waiting')->orderBy('number_int')->take(5)->get(['number_str']);
      $payload[] = [
        'service'=>$s->name,
        'current'=>$current?->number_str,
        'counter'=>$current?->counter?->name,
        'next'=>$next->pluck('number_str'),
      ];
    }
    return response()->json($payload);
  }

  public function statusByService(Service $service){
    $current = Ticket::where('service_id',$service->id)->where('status','called')->latest('called_at')->first();
    $next = Ticket::where('service_id',$service->id)->where('status','waiting')->orderBy('number_int')->take(5)->get(['number_str']);
    return [
      'service'=>$service->name,
      'current'=>$current?->number_str,
      'counter'=>$current?->counter?->name,
      'next'=>$next->pluck('number_str'),
    ];
  }

  public function createTicket(Request $r){
    $service = Service::findOrFail($r->service_id);
    $today = now()->startOfDay();
    $last = Ticket::where('service_id',$service->id)->whereDate('created_at',$today)->max('number_int');
    $num = ($last ?? 0) + 1; if($num>999) abort(422,'Kuota habis');
    $ticket = Ticket::create([
      'service_id'=>$service->id,
      'number_int'=>$num,
      'number_str'=>$service->prefix.'-'.str_pad($num,3,'0',STR_PAD_LEFT),
    ]);
    return $ticket;
  }

  public function callNext(Request $r){
    $counter = Counter::findOrFail($r->counter_id);
    $ticket = Ticket::where('service_id',$counter->service_id)->where('status','waiting')->orderBy('number_int')->first();
    if(!$ticket) abort(404,'Tidak ada antrian');
    $ticket->update(['status'=>'called','called_at'=>now(),'counter_id'=>$counter->id]);
    event(new TicketCalled($ticket));
    Call::create(['ticket_id'=>$ticket->id,'counter_id'=>$counter->id,'user_id'=>auth()->id(),'type'=>'call']);
    return $ticket;
  }

  public function recall(Ticket $ticket){
    if($ticket->status!=='called') abort(422,'Ticket belum dipanggil');
    event(new TicketCalled($ticket));
    Call::create(['ticket_id'=>$ticket->id,'counter_id'=>$ticket->counter_id,'user_id'=>auth()->id(),'type'=>'recall']);
    return $ticket->refresh();
  }
}
```

---

## 9) Filament 4 Resource (ringkas)

Buat Resource: `ServiceResource`, `CounterResource`, `TicketResource` + **Custom Page** "Panggil Antrian" dengan tombol **Next** & **Recall**.

```php
// app/Filament/Resources/TicketResource/Pages/CallQueue.php
class CallQueue extends Page {
  protected static string $resource = TicketResource::class;
  protected static string $view = 'filament.pages.call-queue';
}
```

`resources/views/filament/pages/call-queue.blade.php` (pseudo):

```blade
<x-filament::page>
  <div class="grid md:grid-cols-3 gap-4">
    <x-filament::section heading="Pilih Loket">
      <x-filament::select wire:model="counterId" :options="$counters" />
    </x-filament::section>
    <x-filament::section heading="Kontrol">
      <x-filament::button wire:click="callNext">Panggil Berikutnya</x-filament::button>
      <x-filament::button wire:click="recall" color="warning">Ulangi Panggilan</x-filament::button>
    </x-filament::section>
  </div>
</x-filament::page>
```

Gunakan Livewire v3 untuk aksi `callNext()` → panggil endpoint atau langsung service kelas.

---

## 10) Daily Reset Command + Scheduler

```php
// app/Console/Commands/QueueDailyReset.php
class QueueDailyReset extends Command {
  protected $signature = 'queue:daily-reset';
  protected $description = 'Reset status tiket kemarin dan mulai hitungan baru';
  public function handle(){
    // Tutup tiket waiting kemarin → cancelled
    Ticket::where('status','waiting')->whereDate('created_at','<',today())->update(['status'=>'cancelled']);
    $this->info('Reset done');
  }
}
```

`app/Console/Kernel.php`:

```php
$schedule->command('queue:daily-reset')->dailyAt('06:00');
```

---

## 11) React Display App (Vite)

**Struktur minimal**

```
react-display/
  src/App.jsx
  src/api.js
  index.html
```

**index.html** (ringkas)

```html
<!doctype html>
<html>
    <head>
        <meta charset="utf-8" />
        <meta name="viewport" content="width=device-width, initial-scale=1" />
        <title>Display Antrian Puskesmas</title>
        <style>
            body {
                font-family:
                    system-ui,
                    Segoe UI,
                    Roboto,
                    Inter,
                    Arial;
                background: #0b1220;
                color: #eef;
            }
            .wrap {
                max-width: 1200px;
                margin: auto;
                padding: 24px;
            }
            .grid {
                display: grid;
                grid-template-columns: 1fr 1fr;
                gap: 24px;
            }
            .card {
                background: #111a2b;
                border-radius: 16px;
                padding: 20px;
                box-shadow: 0 10px 30px rgba(0, 0, 0, 0.25);
            }
            .current {
                font-size: 96px;
                font-weight: 800;
                letter-spacing: 0.06em;
            }
            .service {
                font-size: 20px;
                opacity: 0.8;
            }
            .counter {
                font-size: 28px;
                margin-top: 8px;
            }
            .next li {
                font-size: 24px;
                list-style: none;
                padding: 6px 0;
                border-bottom: 1px dashed #223;
            }
            .ticker {
                overflow: hidden;
                white-space: nowrap;
            }
            .ticker span {
                display: inline-block;
                padding-right: 40px;
            }
        </style>
    </head>
    <body>
        <div id="root"></div>
        <script type="module" src="/src/App.jsx"></script>
    </body>
</html>
```

**src/api.js**

```js
export const API_BASE = 'http://localhost:8000/api';
export async function getStatus() {
    const res = await fetch(`${API_BASE}/status`);
    return res.json();
}
```

**src/App.jsx** (Echo + TTS; fallback polling)

```jsx
import { useEffect, useRef, useState } from 'react';
import Echo from 'laravel-echo';

window.Pusher = undefined; // required by Echo if not using pusher pkg

export default function App() {
    const [rows, setRows] = useState([]);
    const lastAnnounceRef = useRef('');

    async function load() {
        const res = await fetch('http://localhost:8000/api/status');
        const data = await res.json();
        setRows(data);
    }

    // TTS Indonesia
    function speak(text) {
        if (!('speechSynthesis' in window)) return;
        const utt = new SpeechSynthesisUtterance(text);
        utt.lang = 'id-ID';
        window.speechSynthesis.cancel();
        window.speechSynthesis.speak(utt);
    }

    // WebSocket realtime
    useEffect(() => {
        load();
        const echo = new Echo({
            broadcaster: 'reverb',
            key: 'local',
            wsHost: '127.0.0.1',
            wsPort: 8080,
            forceTLS: false,
            enabledTransports: ['ws'],
        });
        const channel = echo.channel('queue');
        channel.listen('.ticket.called', (e) => {
            // Update UI cepat
            setRows((prev) => {
                const copy = [...prev];
                const idx = copy.findIndex((r) => r.service === e.service);
                const item = { service: e.service, current: e.number_str, counter: e.counter, next: copy[idx]?.next || [] };
                if (idx > -1) copy[idx] = item;
                else copy.unshift(item);
                return copy;
            });
            const phrase = `Nomor antrian ${e.prefix} ${String(e.number_int).padStart(3, '0')} silakan ke ${e.counter}`;
            if (lastAnnounceRef.current !== e.id) {
                speak(phrase);
                lastAnnounceRef.current = e.id;
            }
        });

        // Fallback polling tiap 10 detik
        const id = setInterval(load, 10000);
        return () => {
            clearInterval(id);
            echo.disconnect();
        };
    }, []);

    return (
        <div className="wrap">
            <h1>Display Antrian Puskesmas</h1>
            <div className="grid">
                {rows.map((r, i) => (
                    <div key={i} className="card">
                        <div className="service">{r.service}</div>
                        <div className="current">{r.current ?? '--'}</div>
                        <div className="counter">{r.counter ? `Ke ${r.counter}` : 'Menunggu panggilan'}</div>
                        <h3>Berikutnya</h3>
                        <ul className="next">
                            {(r.next || []).map((n, idx) => (
                                <li key={idx}>{n}</li>
                            ))}
                        </ul>
                    </div>
                ))}
            </div>

            {/* Ticker gabungan */}
            <div className="card" style={{ marginTop: 24 }}>
                <div className="ticker">
                    <span>{rows.map((r) => `${r.service}: ${r.current ?? '--'} → `).join('')}</span>
                </div>
            </div>
        </div>
    );
}
```

> **Catatan suara**: Web Speech TTS tidak perlu file audio. Jika butuh suara berbasis audio file, siapkan `audio/A-001.mp3` dst dan panggil `audio.play()` ketika event masuk.

---

## 12) UX Filament: tombol cepat

- Di `TicketResource` tambahkan **Action**: "Panggil Berikutnya" (memilih loket), "Recall", "Selesaikan".
- Di `CounterResource` tampilkan jumlah waiting.
- Dashboard ringkas: Kartu per layanan: Waiting | Called (sedang) | Selesai.

---

## 13) Peran & Akses

- **administrator**: semua resource
- **admin**: kelola tickets/calls, read-only services/counters
- **user**: hanya akses display (tidak perlu login; halaman React publik)

Sederhana: gunakan policy/`Gate::before` atau paket Filament Shield jika mau cepat (opsional).

---

## 14) Instalasi Cepat (Laragon)

```bash
# Backend
composer create-project laravel/laravel puskesmas-queue
cd puskesmas-queue
composer require filament/filament:^4 guzzlehttp/guzzle laravel/sanctum
php artisan vendor:publish --provider="Laravel\Sanctum\SanctumServiceProvider"
php artisan migrate --seed

# Reverb (jika belum ada)
composer require laravel/reverb
php artisan reverb:install
php artisan reverb:start
php artisan serve # http://localhost:8000

# Filament user
php artisan make:filament-user # buat akun admin

# Frontend display
npm create vite@latest react-display -- --template react
cd react-display
npm i laravel-echo
npm run dev # http://localhost:5173
```

Pastikan CORS di Laravel mengizinkan asal dari `http://localhost:5173`.

`config/cors.php` → tambahkan origin dev.

---

## 15) CORS dev (cuplikan)

```php
// config/cors.php
'paths' => ['api/*','broadcasting/*'],
'allowed_origins' => ['http://localhost:5173'],
'allowed_methods' => ['*'],
'allowed_headers' => ['*'],
'supports_credentials' => false,
```

---

## 16) Bonus Sederhana (nilai plus)

- **QR Ticket** di halaman cetak (libs: endroid/qr-code) berisi `number_str` + tanggal.
- **Auto-done**: tiket yang sudah dipanggil > X menit tanpa recall → tandai selesai.
- **Tema TV**: tombol full-screen di React display.
- **Marquee pengumuman**: teks berjalan (jadwal dokter/libur).

---

## 17) Ringkasan Alur Demo

1. Admin login Filament → buat Layanan & Loket → ambil beberapa tiket untuk tiap layanan.
2. Buka **React display** di TV/laptop → terlihat daftar waiting (current `--`).
3. Admin klik **Panggil Berikutnya** (pilih loket) → nomor tampil besar di layar + suara otomatis.
4. Admin bisa **Recall** jika pasien tidak datang.
5. Selesai → ubah status tiket ke `done`.

Selesai. Sederhana, rapi, dan punya realtime + suara. Siap jadi tugas kuliah. 🚀
