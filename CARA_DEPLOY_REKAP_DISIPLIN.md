# Rekap Kehadiran Guru & Staf untuk Kepala Sekolah

Kepala Sekolah melihat per guru/staf: **Tidak Hadir (Alpa), Terlambat, Pulang Lebih Awal, Ijin, Sakit, Dinas Luar (jumlah hari/kali), dan Predikat**, plus baris jumlah. Jam scan dan jumlah menit TIDAK dikirim ke browser.
Sumbernya rekap yang disimpan admin di Rekap Absen (tombol "Simpan rekap").

1. Project pdp -> deploy Edge Function baru: `supabase functions deploy rekap-disiplin`
   (atau Dashboard -> Edge Functions -> buat `rekap-disiplin`, isi dengan `supabase/functions/rekap-disiplin/index.ts`).
   Secrets `REKAP_SUPABASE_URL` dan `REKAP_SERVICE_KEY` sudah ada, tidak perlu diisi lagi.
2. **Deploy ulang** `rekap-disiplin` (ada kolom jumlah baru): `supabase functions deploy rekap-disiplin`.
3. Upload `disiplin.html`, `portal.html`, `bottomnav.js` dan semua halaman yang memuat `bottomnav.js?v=9`.
4. Tidak perlu SQL. Rekap yang tampil = rekap tersimpan; pilih rekap lain lewat dropdown di halaman.

Akses: Kepala Sekolah (dan admin). Guru/staf yang membuka disiplin.html dikembalikan ke Menu Utama,
dan server menolak permintaannya.

## Catatan nama kolom
Edge Function mencocokkan nama kolom jumlah di rekap tersimpan secara toleran (mis. `tidakHadir`/`alpa`, `terlambat`, `pulangCepat`, `izin`/`ijin`, `sakit`, `dinasLuar`). Kolom berisi "menit" diabaikan.
Jika ada kolom yang tidak ditemukan, halaman menampilkan peringatan kuning dan sel berisi “–”. Rekap lama biasanya perlu **Simpan rekap** ulang di Rekap Absen.
