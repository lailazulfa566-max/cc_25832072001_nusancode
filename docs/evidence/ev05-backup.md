# EV-05 — Prosedur Backup Database

**Proyek:** NusanCode  
**Lingkungan:** Azure VM, Ubuntu Server 24.04 LTS  
**Status:** Prosedur disiapkan; pelaksanaan backup belum dibuktikan.  
**Tanggal penyusunan:** 2026-11-09

## 1. Tujuan

Dokumen ini menjelaskan prosedur pencadangan database NusanCode agar data dapat dipulihkan apabila terjadi kerusakan atau kehilangan data.

## 2. Kondisi saat ini

Berdasarkan README dan arsitektur M03, SQLite masih direncanakan untuk milestone berikutnya. Karena database aplikasi belum dibuktikan aktif, belum ada file backup produksi yang dapat dijadikan bukti. Prosedur berikut digunakan setelah database SQLite diterapkan.

## 3. Rencana kebijakan backup

| Parameter | Rencana |
|---|---|
| Jenis database | SQLite |
| Frekuensi | Harian, setelah database digunakan |
| Retensi | 7 salinan harian dan 4 salinan mingguan (perlu disesuaikan kapasitas) |
| Lokasi sementara | Direktori backup privat di VPS |
| Lokasi salinan kedua | Storage privat terpisah dari VPS |
| Perlindungan | Hak akses terbatas; enkripsi sebelum pemindahan ke storage offsite |
| Target RPO | 24 jam (target, belum diuji) |

**Penting:** File database, file backup, kredensial, token, dan data pengguna tidak boleh diunggah ke repository GitHub. Repository hanya menyimpan dokumentasi dan bukti yang sudah disanitasi.

## 4. Prosedur backup SQLite

Jalankan setelah lokasi database aktual diketahui. Ganti `/path/aktual/nusancode.db` sesuai konfigurasi aplikasi.

```bash
# 1. Buat direktori backup privat
sudo install -d -m 700 -o cloudstudent -g cloudstudent /var/backups/nusancode

# 2. Buat nama file berdasarkan waktu
BACKUP="/var/backups/nusancode/nusancode-$(date +%Y%m%d-%H%M%S).db"

# 3. Buat backup konsisten menggunakan SQLite
sqlite3 /path/aktual/nusancode.db ".backup '$BACKUP'"

# 4. Batasi akses file backup
chmod 600 "$BACKUP"

# 5. Periksa integritas file backup
sqlite3 "$BACKUP" "PRAGMA integrity_check;"

# 6. Catat checksum untuk pemeriksaan integritas
sha256sum "$BACKUP"
```

Hasil pemeriksaan integritas yang diharapkan adalah `ok`. Jika perintah gagal atau hasil berbeda, backup tidak boleh dinyatakan valid.

## 5. Bukti yang harus disimpan

Simpan bukti yang sudah disanitasi pada folder lokal proyek, kemudian unggah hanya bukti nonrahasia ke:

`docs/evidence/m05/`

| ID | Bukti | Nama berkas yang disarankan | Status |
|---|---|---|---|
| B-01 | Waktu dan perintah backup (tanpa data sensitif) | `backup-command.txt` | Belum |
| B-02 | Daftar file backup, ukuran, dan permission | `backup-list.txt` | Belum |
| B-03 | Hasil `PRAGMA integrity_check` | `backup-integrity.txt` | Belum |
| B-04 | Checksum SHA-256 | `backup-sha256.txt` | Belum |
| B-05 | Bukti salinan offsite, tanpa kredensial | `backup-offsite.txt` | Belum |

## 6. Catatan pelaksanaan

| Tanggal/waktu | Nama backup | Ukuran | Integrity check | Checksum dicatat | Lokasi salinan kedua | Pelaksana |
|---|---|---|---|---|---|---|
| Belum dilaksanakan | — | — | — | — | — | — |

## 7. Kriteria keberhasilan

Backup dapat dinyatakan berhasil setelah file dibuat, permission dibatasi, pemeriksaan integritas menghasilkan `ok`, checksum tercatat, dan salinan kedua tersimpan di lokasi privat terpisah.

**Kesimpulan sementara:** EV-05 baru memiliki prosedur tertulis. Bukti pelaksanaan belum tersedia sehingga statusnya belum dapat dinyatakan lulus.
