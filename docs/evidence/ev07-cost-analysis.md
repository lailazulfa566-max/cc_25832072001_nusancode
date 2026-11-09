# EV-07 — Bukti Cost Analysis dan Proyeksi Biaya Azure

**Proyek:** NusanCode — Cloud Computing PTI 2802  
**Subscription:** Azure for Students  
**Lokasi resource:** Australia East  
**Tanggal pemeriksaan:** 9 November 2026  
**Sumber bukti:** PDF tangkapan layar Azure Cost Management yang diperiksa pada 9 November 2026.

## 1. Tujuan

Dokumen ini mencatat hasil pemeriksaan biaya pada Azure Cost Management sebagai bukti pendukung EV-07. Data Cost Analysis digunakan untuk memverifikasi pemakaian aktual dan melihat forecast pada periode yang ditampilkan. Angka forecast bulanan tidak dianggap sebagai proyeksi biaya 12 bulan.

## 2. Ringkasan hasil yang terlihat pada portal

| Tampilan portal | Periode/cakupan yang terlihat | Nilai | Keterangan |
|---|---|---:|---|
| Cost Analysis | 1–30 November 2026 | US$4,73 actual cost | Akumulasi biaya pada tampilan November |
| Cost Analysis | Forecast pada tampilan November | US$17,60 | Perkiraan sampai akhir periode yang ditampilkan, bukan forecast 12 bulan |
| Cost Analysis | 11 Oktober–9 November 2026 | US$16,97 actual cost | Nilai aktual untuk rentang tanggal pada tampilan kedua |
| Cost Analysis | Forecast pada tampilan kedua | US$17,60 | Forecast sesuai tampilan portal |
| Ringkasan akun penagihan | Tagihan bulan November | US$5,31 | Nilai yang ditampilkan pada ringkasan Azure for Students |
| Azure for Students | Kredit tersedia | US$78 dari US$100 | Sisa kredit yang terlihat saat tangkapan layar dibuat |
| Azure for Students | Masa berlaku kredit | 315 hari tersisa | Portal menampilkan tanggal kedaluwarsa 19 September 2027 |

**Catatan interpretasi:** Nilai US$4,73, US$16,97, US$17,60, dan US$5,31 berasal dari tampilan atau cakupan yang berbeda. Nilai-nilai tersebut tidak boleh dijumlahkan atau diperlakukan sebagai angka yang saling menggantikan. Sebelum pelaporan akhir, rentang tanggal dan filter pada Cost Analysis harus dicantumkan bersama setiap angka.

## 3. Komponen biaya yang terlihat

Pada tampilan Cost Analysis November, rincian layanan yang terlihat adalah:

| Layanan | Biaya yang terlihat |
|---|---:|
| Storage | US$2,76 |
| Virtual Network | US$1,88 |
| Ubuntu Pro – VM 2 vCPU | US$0,10 |
| Bandwidth | US$0,00 |
| Virtual Machines | US$0,00 |

Jumlah rincian yang terlihat tersebut adalah US$4,74 karena pembulatan tampilan; portal menampilkan total actual cost US$4,73. Gunakan total portal sebagai angka ringkasan, dan jangan mengoreksi total berdasarkan penjumlahan angka yang telah dibulatkan.

## 4. Kondisi resource saat pemeriksaan

Tangkapan layar halaman Virtual Machine menunjukkan:

- Nama VM: LailaZulfa.
- Ukuran: Standard B2ats v2 (2 vCPU, 1 GiB RAM).
- Sistem operasi: Linux / Ubuntu.
- Region: Australia East.
- Status pada saat tangkapan layar: dihentikan (dialokasikan kembali / deallocated).
- Public IP yang ditampilkan: 20.211.31.222.

Status VM yang deallocated tidak berarti seluruh resource pendukung otomatis berhenti menimbulkan biaya. Disk terkelola dan alamat IP perlu diperiksa secara terpisah pada Cost Analysis.

## 5. Hubungan dengan TCO dan proyeksi 12 bulan

Dokumen studi kelayakan menggunakan asumsi biaya VPS Rp289.648 per bulan atau Rp3.475.776 untuk 12 bulan. Angka tersebut merupakan estimasi yang perlu diverifikasi terhadap konfigurasi, periode pemakaian, dan tarif aktual Azure.

Hasil Cost Analysis di atas merupakan bukti biaya aktual/forecast pada rentang waktu yang terlihat, bukan bukti biaya 12 bulan penuh. Untuk menyelesaikan proyeksi 12 bulan, lakukan langkah berikut:

1. Verifikasi harga VM Standard B2ats v2 Linux di region Australia East melalui Azure Pricing Calculator atau Azure Retail Prices.
2. Periksa biaya disk Premium SSD P4 dan Public IP Standard IPv4 secara terpisah.
3. Tentukan asumsi jam operasi VM per bulan (24/7 atau hanya saat praktikum).
4. Susun skenario penggunaan kredit Azure for Students dan skenario biaya setelah kredit habis.
5. Perbarui total TCO hanya setelah seluruh komponen dan asumsi biaya terdokumentasi.

## 6. Batasan dan status verifikasi

- Data pada PDF adalah tangkapan layar portal, bukan invoice final.
- Forecast US$17,60 hanya mengikuti cakupan tanggal yang tampak pada Cost Analysis; tidak boleh dikalikan 12 sebagai proyeksi tahunan tanpa dasar asumsi.
- Angka saldo kredit US$78 merupakan saldo yang terlihat pada tanggal tangkapan layar dan dapat berubah.
- Data pemakaian melalui Azure CLI sebelumnya menampilkan nilai PretaxCost sebagai None; karena itu output tersebut tidak digunakan sebagai sumber nominal biaya.
- Biaya backup off-site, domain (jika tidak disediakan dosen), dan layanan eksternal tetap perlu dinyatakan sesuai kondisi aktual. Jangan menyatakan biaya tersebut nol tanpa bukti.

**Kesimpulan:** PDF Cost Analysis memberikan bukti bahwa subscription Azure for Students memiliki pemakaian biaya dan forecast pada periode yang diperiksa, serta menampilkan sisa kredit US$78 dari US$100. Bukti ini mendukung EV-07, tetapi belum cukup untuk menyatakan biaya operasional final atau total biaya 12 bulan. Estimasi 12 bulan tetap harus disusun dari tarif dan asumsi penggunaan setiap resource.

## 7. Referensi bukti

- PDF tangkapan layar Azure Cost Management yang diperiksa pada 9 November 2026 (sumber yang digunakan untuk menyusun catatan EV-07).
- Dokumen *Perencanaan Studi Kelayakan Proyek Cloud Computing PTI 2802*, bagian 10.1 Register Biaya TCO dan 10.2 Proyeksi Biaya–Manfaat 12 Bulan.
