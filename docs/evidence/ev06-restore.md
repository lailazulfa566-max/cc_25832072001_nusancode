# EV-06 — Pengujian Restore Database

**Proyek:** NusanCode  
**Lingkungan:** Azure VM, Ubuntu Server 24.04 LTS  
**Status:** Rencana pengujian disiapkan; restore belum dilaksanakan.  
**Tanggal penyusunan:** 2026-11-09

## 1. Tujuan

Memastikan file backup NusanCode dapat dipulihkan menjadi database SQLite yang valid, serta mencatat waktu pemulihan dan kehilangan data yang mungkin terjadi.

## 2. Kondisi dan batasan

Database SQLite masih tercatat sebagai rencana pada dokumentasi M03. Oleh karena itu, pengujian restore belum dapat dinyatakan selesai sebelum database dan file backup nyata tersedia.

Pengujian pertama harus dilakukan pada salinan/lokasi uji, bukan dengan menimpa database aktif. Jangan memasukkan database, data pengguna, password, token, atau secret ke GitHub.

## 3. Target pemulihan

| Parameter | Target | Hasil aktual |
|---|---|---|
| RPO (Recovery Point Objective) | Maksimal 24 jam | Belum diuji |
| RTO (Recovery Time Objective) | Kurang dari 60 menit | Belum diuji |
| Integritas database hasil restore | `PRAGMA integrity_check` menghasilkan `ok` | Belum diuji |
| Aplikasi dapat membaca database uji | Pemeriksaan aplikasi berhasil | Belum diuji |

Target di atas merupakan sasaran proyek, bukan hasil pengujian.

## 4. Prosedur uji restore

Lakukan setelah EV-05 menghasilkan file backup yang valid. Gunakan direktori uji terpisah dan sesuaikan path dengan lokasi aktual.

```bash
# 1. Siapkan direktori pengujian
mkdir -p ~/restore-test
chmod 700 ~/restore-test

# 2. Salin file backup ke direktori pengujian
cp /path/backup/nusancode-backup.db ~/restore-test/restored-test.db
chmod 600 ~/restore-test/restored-test.db

# 3. Periksa integritas database hasil pemulihan
sqlite3 ~/restore-test/restored-test.db "PRAGMA integrity_check;"

# 4. Periksa struktur tabel
sqlite3 ~/restore-test/restored-test.db ".tables"

# 5. Catat waktu selesai dan ukuran file
date -Is
stat ~/restore-test/restored-test.db
```

Perintah di atas hanya menguji salinan di direktori uji. Jangan mengganti database aplikasi aktif dengan file hasil uji sebelum ada prosedur pemeliharaan dan verifikasi terpisah.

## 5. Skenario pengujian

| No. | Skenario | Hasil yang diharapkan | Hasil aktual | Status |
|---|---|---|---|---|
| 1 | File backup tersedia | File dapat dibaca | Belum diuji | Pending |
| 2 | Pemeriksaan integritas | Hasil `ok` | Belum diuji | Pending |
| 3 | Pemeriksaan tabel | Struktur tabel dapat ditampilkan | Belum diuji | Pending |
| 4 | Aplikasi uji membaca database hasil restore | Pemeriksaan aplikasi berhasil | Belum diuji | Pending |
| 5 | Pengukuran durasi restore | Durasi tercatat | Belum diukur | Pending |

## 6. Formulir pencatatan hasil

| Informasi | Hasil |
|---|---|
| Tanggal/waktu mulai | Belum diisi |
| Tanggal/waktu selesai | Belum diisi |
| Sumber file backup | Belum diisi |
| Ukuran file backup | Belum diisi |
| Hasil integrity check | Belum diuji |
| Tabel ditemukan | Belum diuji |
| Aplikasi uji berhasil membaca database | Belum diuji |
| Durasi restore | Belum diukur |
| RPO aktual | Belum dihitung |
| RTO aktual | Belum dihitung |
| Pelaksana | Belum diisi |
| Bukti pendukung | Belum tersedia |

## 7. Bukti yang harus disimpan

Simpan bukti yang telah disanitasi pada `docs/evidence/m05/`:

- `restore-integrity.txt` — hasil pemeriksaan integritas.
- `restore-tables.txt` — daftar tabel, tanpa isi data pribadi.
- `restore-timing.txt` — waktu mulai, selesai, dan durasi.
- `restore-test-result.md` — ringkasan skenario dan hasil.

## 8. Kriteria keberhasilan

Restore dinyatakan berhasil jika file backup dapat dipulihkan ke lingkungan uji, pemeriksaan integritas menghasilkan `ok`, struktur database tersedia, dan aplikasi uji dapat membaca database. RTO dan RPO hanya boleh diisi setelah waktu dan titik backup aktual dicatat.

**Kesimpulan sementara:** EV-06 masih berupa rencana pengujian. Belum ada hasil restore nyata, sehingga RTO dan RPO aktual belum dapat dinyatakan tercapai.
