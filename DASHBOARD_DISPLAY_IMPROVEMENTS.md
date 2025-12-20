# Dashboard & Display Improvements

## Overview

Perbaikan dan peningkatan fitur untuk halaman Dashboard dan Display Antrian dengan statistik real-time yang akurat.

## Changes Made

### 1. Backend API Endpoints

#### New Endpoints Added:

- **GET /api/dashboard/stats** - Statistik lengkap untuk dashboard
- **GET /api/global/stats** - Statistik global untuk display antrian

#### QueueController Methods:

##### `dashboardStats()`

Mengembalikan statistik komprehensif untuk dashboard:

```json
{
    "total_today": 32,
    "done_today": 12,
    "currently_serving": 5,
    "waiting": 15,
    "avg_service_time": 8.5,
    "services": [
        {
            "id": 1,
            "name": "Poli Umum",
            "total_today": 10,
            "done_today": 5,
            "waiting": 3,
            "serving": 2
        }
    ],
    "counters": [
        {
            "id": 1,
            "name": "Loket 1",
            "done_today": 5,
            "serving": 1,
            "service": {
                "id": 1,
                "name": "Poli Umum"
            }
        }
    ]
}
```

**Features:**

- Total antrian hari ini
- Selesai dilayani hari ini (dari semua layanan)
- Sedang dilayani (counter aktif)
- Menunggu (belum dipanggil)
- Waktu pelayanan rata-rata (dalam menit)
- Statistik per layanan dengan breakdown
- Performa per counter dengan service info

**SQL Query Highlights:**

- `withCount()` untuk aggregate data
- `whereDate()` untuk filter hari ini
- `julianday()` untuk menghitung durasi di SQLite
- Relasi dengan eager loading untuk efisiensi

##### `globalStats()`

Mengembalikan statistik global untuk display:

```json
{
    "done_today": 12,
    "currently_serving": 5,
    "waiting": 15
}
```

**Features:**

- Data agregat dari SEMUA layanan
- Real-time count dari database
- Tidak hardcoded lagi!

### 2. Frontend Hooks

#### New Hooks in `useQueue.ts`:

##### `useDashboardStats(pollingInterval)`

Custom hook untuk fetch statistik dashboard dengan auto-refresh:

```typescript
const { stats, loading, error, refetch } = useDashboardStats(30000);
```

**Features:**

- Auto-refresh setiap 30 detik (configurable)
- Loading state management
- Error handling
- Manual refetch capability
- TypeScript typed dengan interface `DashboardStats`

##### `useGlobalStats(pollingInterval)`

Custom hook untuk statistik global display:

```typescript
const { stats, loading, error, refetch } = useGlobalStats(30000);
```

**Features:**

- Auto-refresh setiap 30 detik
- Simple, focused data (3 metrics only)
- TypeScript typed dengan interface `GlobalStats`
- Efficient polling dengan cleanup

#### New TypeScript Interfaces:

```typescript
interface DashboardStats {
    total_today: number;
    done_today: number;
    currently_serving: number;
    waiting: number;
    avg_service_time: number;
    services: Array<ServiceStats>;
    counters: Array<CounterStats>;
}

interface GlobalStats {
    done_today: number;
    currently_serving: number;
    waiting: number;
}
```

### 3. Dashboard Page (`dashboard.tsx`)

#### Complete Redesign:

**Before:** Placeholder patterns dengan mock data
**After:** Comprehensive statistics dashboard dengan real data

#### Features:

1. **Main Statistics Cards (4 cards):**
    - Total Antrian Hari Ini - dengan icon BarChart3
    - Selesai Dilayani - hijau dengan persentase
    - Sedang Dilayani - orange untuk counter aktif
    - Menunggu - biru untuk antrian pending

2. **Average Service Time Card:**
    - Besar, prominent display
    - Dalam satuan menit
    - Calculated from called_at to finished_at

3. **Statistics per Service:**
    - List semua layanan (Poli Umum, Farmasi, dll)
    - Breakdown: selesai, dilayani, menunggu per service
    - Total tickets per service
    - Color-coded badges

4. **Counter Performance:**
    - List semua counter
    - Jumlah selesai per counter
    - Service badge
    - "Sedang Aktif" indicator
    - Sorted by performance

#### UI/UX Improvements:

- Loading state dengan spinner
- Empty state handling
- Responsive grid layout (md:grid-cols-2, lg:grid-cols-4)
- Consistent icon usage (Lucide React)
- Color coding: green=done, orange=serving, blue=waiting
- Auto-refresh tanpa page reload

### 4. Display Page (`display.tsx`)

#### Bug Fix:

**Problem:** "Selesai Hari Ini" hardcoded ke 0
**Solution:** Menggunakan `useGlobalStats()` hook

#### Changes:

1. Import `useGlobalStats` dan icon `CheckCircle`
2. Hook initialization:
    ```typescript
    const { stats: globalStats } = useGlobalStats(30000);
    ```
3. Updated statistics cards:

    ```typescript
    // Before
    <div className="text-2xl font-bold">0</div>

    // After
    <div className="text-2xl font-bold">{globalStats?.done_today ?? 0}</div>
    ```

4. Updated "Total Menunggu":
    ```typescript
    {
        globalStats?.waiting ?? 0;
    }
    ```
5. Updated "Sedang Dilayani":
    ```typescript
    {
        globalStats?.currently_serving ?? 0;
    }
    ```

#### Result:

- ✅ "Selesai Hari Ini" now shows REAL count
- ✅ Updates automatically setiap 30 detik
- ✅ Counts ALL services (not per-service)
- ✅ Accurate from database, not calculated in JS

## Testing Instructions

### 1. Test Dashboard:

```bash
# Akses dashboard
http://localhost:8000/dashboard
```

**Verify:**

1. ✅ Total Antrian Hari Ini = 32 (sesuai dummy data)
2. ✅ Selesai Dilayani = 3 (ada 3 tickets dengan status 'done')
3. ✅ Sedang Dilayani = 4 (ada 4 tickets dengan status 'called')
4. ✅ Menunggu = 25 (ada 25 tickets dengan status 'waiting')
5. ✅ Waktu rata-rata muncul (dihitung dari called_at ke finished_at)
6. ✅ List layanan menampilkan 5 services (Poli Umum, Poli Gigi, Farmasi, KIA, Lab)
7. ✅ List counter menampilkan 7 counters dengan service badge
8. ✅ Auto-refresh setiap 30 detik (cek Network tab)

### 2. Test Display:

```bash
http://localhost:8000/queue/display
```

**Verify:**

1. ✅ "Selesai Hari Ini" = 3 (TIDAK LAGI 0!)
2. ✅ "Sedang Dilayani" = 4
3. ✅ "Total Menunggu" = 25
4. ✅ Angka update otomatis setiap 30 detik

### 3. Test Integration:

**Scenario:** Selesaikan antrian dari management panel

1. Buka http://localhost:8000/queue/management
2. Pilih counter (misal: Loket Farmasi 1)
3. Panggil antrian (C-003)
4. Klik "SELESAIKAN PELAYANAN"
5. Buka tab lain dengan Dashboard
6. **Verify:** "Selesai Dilayani" bertambah dari 3 → 4
7. **Verify:** Counter "Loket Farmasi 1" bertambah dari 1 → 2
8. Buka tab Display
9. **Verify:** "Selesai Hari Ini" bertambah dari 3 → 4
10. **Verify:** "Menunggu" berkurang dari 25 → 24

### 4. Test API Directly:

```bash
# Test dashboard stats
curl http://localhost:8000/api/dashboard/stats

# Test global stats
curl http://localhost:8000/api/global/stats

# Test counter stats
curl http://localhost:8000/api/counter/1/stats
```

## Database Queries Explained

### Dashboard Stats Query:

```php
// Count with relation filter
Service::withCount([
    'tickets as total_today' => fn($q) => $q->whereDate('created_at', $today),
    'tickets as done_today' => fn($q) => $q->where('status', 'done')->whereDate('finished_at', $today),
    'tickets as waiting' => fn($q) => $q->where('status', 'waiting'),
    'tickets as serving' => fn($q) => $q->where('status', 'called'),
])->where('is_active', true)->get();
```

**Why this approach?**

- Single query dengan subqueries (efficient!)
- Laravel eloquent relationship counting
- Automatic grouping per service/counter
- Type-safe dengan Eloquent models

### Average Service Time (SQLite):

```php
Ticket::where('status', 'done')
    ->whereDate('finished_at', $today)
    ->whereNotNull('called_at')
    ->whereNotNull('finished_at')
    ->selectRaw('AVG((julianday(finished_at) - julianday(called_at)) * 24 * 60) as avg_time')
    ->value('avg_time');
```

**Why julianday?**

- SQLite tidak support `TIMESTAMPDIFF()`
- `julianday()` menghitung perbedaan dalam days
- `* 24 * 60` convert ke menit
- Result: float (e.g., 8.5 menit)

## Performance Considerations

### Polling Intervals:

- Dashboard: 30 seconds (data tidak perlu super real-time)
- Display: 30 seconds (bisa dikurangi ke 10s jika perlu)
- Management: 10 seconds (queue status), 30 seconds (stats)

### Query Optimization:

- Using `withCount()` instead of separate queries
- Index on: `counter_id`, `service_id`, `status`, `finished_at`
- `whereDate()` optimal dengan index on date columns
- Eager loading untuk relasi (`with('service')`)

### Caching Opportunities (Future):

```php
// Cache dashboard stats for 1 minute
Cache::remember('dashboard_stats', 60, function() {
    return QueueController::dashboardStats();
});
```

## Troubleshooting

### Issue: Stats tidak update

**Solution:**

1. Check browser console untuk API errors
2. Verify Network tab menunjukkan requests setiap 30s
3. Check Laravel logs: `storage/logs/laravel.log`
4. Test API manual dengan curl

### Issue: Average time = 0

**Cause:** Belum ada tickets dengan status 'done' yang memiliki both `called_at` dan `finished_at`
**Solution:** Normal jika baru setup. Akan terisi setelah ada tickets yang selesai.

### Issue: Service/Counter tidak muncul

**Cause:** Data `is_active = false`
**Solution:** Check database atau run seeder:

```bash
php artisan db:seed
```

## Code Quality

### TypeScript Type Safety:

✅ All hooks fully typed
✅ Interface definitions for all data structures
✅ Null-coalescing operators (`??`) untuk safety
✅ No `any` types used

### Error Handling:

✅ Try-catch dalam semua fetch operations
✅ Loading states untuk better UX
✅ Graceful degradation (show 0 if API fails)
✅ Error state exposed in hooks

### Code Reusability:

✅ Custom hooks dapat digunakan di halaman lain
✅ Consistent pattern dengan existing hooks
✅ Configurable polling intervals
✅ Manual refetch capability

## Future Enhancements

### Dashboard:

1. **Charts & Graphs:**
    - Line chart untuk trend per jam
    - Bar chart untuk perbandingan service
    - Pie chart untuk distribusi status

2. **Date Range Selector:**
    - View statistik kemarin, minggu ini, bulan ini
    - Export data ke CSV/Excel

3. **Real-time Updates:**
    - WebSocket untuk instant updates (no polling delay)
    - Push notifications untuk milestones

### Display:

1. **Fullscreen Mode:**
    - Hide sidebar/header untuk TV display
    - Bigger fonts untuk visibility
    - Auto-rotate through services

2. **Animations:**
    - Smooth transitions untuk number changes
    - Highlight new ticket calls
    - Confetti effect saat milestones

## Conclusion

**Before:**

- ❌ Dashboard kosong (placeholder)
- ❌ Display "Selesai Hari Ini" hardcoded 0
- ❌ Tidak ada statistik komprehensif
- ❌ Tidak ada performa tracking

**After:**

- ✅ Dashboard lengkap dengan 10+ metrics
- ✅ Display menampilkan data REAL dari database
- ✅ Auto-refresh setiap 30 detik
- ✅ Per-service dan per-counter breakdown
- ✅ Average service time calculation
- ✅ TypeScript typed hooks
- ✅ Production-ready dengan error handling

**Impact:**

- Admin dapat monitor performa sistem real-time
- Operator dapat melihat pencapaian mereka
- Management dapat analisis bottleneck
- Visitor dapat melihat status antrian akurat
