# Rumah Kita – Jadwal Rumah Tangga

Aplikasi web (PWA) untuk suami dan istri: tugas bersama, jadwal, waktu sholat, dan keuangan. Stack: Supabase + GitHub + Vercel.

## Isi folder
| File | Fungsi |
|---|---|
| `index.html` | Seluruh aplikasi (tampilan, login, logika) |
| `supabase.sql` | Database dan aturan keamanan, dijalankan sekali di Supabase |
| `manifest.json` | Agar bisa di-install di HP dan PC |
| `sw.js` | Mode offline dan notifikasi di HP |
| `icon-192.png`, `icon-512.png`, `icon-maskable-512.png` | Ikon aplikasi |
| `vercel.json` | Pengaturan kecil untuk Vercel |

## 1. Supabase
1. Buat proyek di supabase.com.
2. Buka **SQL Editor**, tempel seluruh isi `supabase.sql`, klik **Run**.
3. Buka **Project Settings > API**, salin **Project URL** dan **anon public key**.
4. Buka `index.html`, isi bagian paling atas script:
   ```js
   const SB={url:'https://xxxx.supabase.co',key:'eyJ...'};
   ```
   (Ubah juga `LOK` jika kotamu bukan Semarang.)
5. **Authentication > URL Configuration**: isi **Site URL** dengan alamat Vercel-mu (setelah langkah 3 di bawah).
6. Opsional: **Authentication > Providers > Email**, matikan **Confirm email** agar daftar langsung masuk.

## 2. GitHub
Buat repository baru, lalu unggah semua file di folder ini (tombol *Add file > Upload files*).

## 3. Vercel
1. vercel.com > **Add New > Project** > pilih repository tadi.
2. Framework Preset: **Other**. Kosongkan Build Command dan Output Directory.
3. Klik **Deploy**. Salin alamatnya (misalnya `https://rumah-kita.vercel.app`) ke Site URL Supabase (langkah 1.5).

## 4. Dipakai berdua
- Pemilik pertama: tab **Daftar** > pilih peran > **Buat keluarga baru**. Kode keluarga muncul di Beranda.
- Pasangan: tab **Daftar** > pilih peran lainnya > **Gabung dengan kode** > isi kode tadi.

## 5. Pasang di HP dan PC
- **PC / HP (Chrome atau Edge):** buka alamat Vercel lalu klik **Install** di bilah alamat atau menu. Aktifkan notifikasi lewat ikon lonceng di aplikasi.
- **APK / EXE:** buka pwabuilder.com, tempel alamat Vercel, lalu unduh paket Android (apk) atau Windows (exe).

## Catatan
- Setiap kali `index.html` diubah, naikkan nomor `V` di `sw.js` (misalnya `rumahkita-v2`).
- Notifikasi muncul saat aplikasi terbuka atau berjalan di latar belakang. Notifikasi saat aplikasi benar-benar tertutup butuh layanan push tambahan.
