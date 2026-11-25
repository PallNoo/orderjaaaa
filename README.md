# OrderJaa — Sistem Tempahan Makanan Layan Diri

Sistem skrin tempahan makanan layan diri (Kiosk) dan panel admin CMS menggunakan **Cloudflare Workers**, **Cloudflare D1**, dan **HTML/CSS/JavaScript tulen**.

## Ciri Utama
- **Skrin Kiosk (`/`)**: Paparan kategori aktif & kad menu (dengan fallback emoji), troli pesanan, pilihan **Makan Sini** / **Bungkus**, serta nombor giliran berjujukan & status pesanan secara langsung.
- **Panel Admin CMS (`/admin.html`)**: Log masuk `ADMIN_PASSWORD` (pulangkan `503` jika belum diset), pengurusan pesanan dapur, tambah/edit/salin/padam menu, upload gambar termampat (`< 95 KB`), tukar harga cepat, aktif/nyahaktif item & kategori (sekat padam kategori dengan `409` jika masih ada item), serta tetapan kedai.
- **Auto-setup D1**: Jadual & 15 menu contoh dicipta automatik sekali sahaja dalam `ensureDb()` (di-cache dengan flag `dbReady`).

## Persediaan & Auto-Deploy GitHub ke Cloudflare Dashboard

1. **Tetapkan Secret `ADMIN_PASSWORD`** di Cloudflare Dashboard:
   - Pergi ke **Workers & Pages** → pilih projek `orderjaa` → **Settings** → **Variables and Secrets** → tambah Secret bernama `ADMIN_PASSWORD`.
   - Untuk pembangunan tempatan, cipta fail `.dev.vars`:
     ```env
     ADMIN_PASSWORD=kata_laluan_anda
     ```

2. **Pembangunan Tempatan**:
   ```bash
   npm install
   npx wrangler dev
   ```

3. **Deploy Manual / Auto-Deploy GitHub**:
   - Sambungkan repositori GitHub di Cloudflare Dashboard (**Workers & Pages** → **Create** → **Import a repository**).
   - Build command: *(kosongkan atau `npm install`)*
   - Deploy command: `npx wrangler deploy`
   - Binding D1 (`DB` → `orderjaa-db`) sudah dikonfigurasi di dalam `wrangler.toml`.
