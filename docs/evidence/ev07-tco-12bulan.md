# EV-07 — Estimasi Total Cost of Ownership (TCO) 12 Bulan

**Proyek:** NusanCode  
**Provider:** Microsoft Azure  
**Region:** Australia East  
**Tanggal penyusunan:** 2026-11-09  
**Status:** Estimasi awal; perlu verifikasi akhir melalui Azure Pricing Calculator dan tagihan aktual.

## 1. Tujuan dan asumsi

TCO digunakan untuk memperkirakan biaya infrastruktur dan operasional NusanCode selama 12 bulan. Perhitungan awal menggunakan spesifikasi VPS yang tercatat pada EV-01:

- VM Linux Standard B2ats v2, 2 vCPU dan 1 GiB RAM.
- Region Australia East.
- Disk OS Premium SSD yang tercatat berkapasitas 30 GB. Harga pembanding disk menggunakan tier terdekat 32 GiB (P4); tagihan aktual harus diperiksa di Azure.
- Perkiraan VM menggunakan harga pay-as-you-go publik pembanding sebesar USD 10,32/bulan. Harga dapat berbeda dari harga kontrak, kredit, pajak, dan konfigurasi aktual.
- Perhitungan bulanan menggunakan 730 jam.

## 2. Estimasi biaya dasar

| Komponen | Dasar perhitungan | Estimasi/bulan (USD) | Estimasi 12 bulan (USD) | Catatan |
|---|---|---:|---:|---|
| Azure VM Standard B2ats v2 | 730 jam × harga pembanding | 10.32 | 123.84 | Harga publik pembanding Australia East |
| Managed Disk Premium SSD P4 | 730 jam × USD 0.0072/jam | 5.26 | 63.07 | Tier 32 GiB sebagai pendekatan untuk disk 30 GB |
| Domain | Belum dipilih/dibeli | Belum ditentukan | Belum ditentukan | Isi setelah registrar dan ekstensi domain ditetapkan |
| Backup offsite | Belum ditentukan | Belum ditentukan | Belum ditentukan | Bergantung kapasitas, redundansi, dan transaksi |
| Transfer data keluar | Belum diukur | Belum ditentukan | Belum ditentukan | Bergantung pemakaian jaringan |
| IP publik dan biaya lain | Perlu cek konfigurasi/tagihan Azure | Belum ditentukan | Belum ditentukan | Verifikasi pada Cost Management |
| Pajak dan kurs | Mengikuti tagihan aktual | Belum ditentukan | Belum ditentukan | Belum dimasukkan |

**Subtotal komponen yang memiliki angka:** USD 15.58/bulan atau sekitar USD 186.91/12 bulan.

Subtotal tersebut bukan TCO final karena domain, backup offsite, transfer data, IP publik (jika dikenakan biaya), pajak, dan kurs belum dimasukkan.

## 3. Rumus perhitungan

- Biaya VM 12 bulan = biaya VM bulanan × 12.
- Biaya disk 12 bulan = biaya disk bulanan × 12.
- TCO 12 bulan = seluruh biaya infrastruktur dan operasional selama 12 bulan.
- Total final baru dapat dihitung setelah seluruh komponen yang belum diketahui diverifikasi.

## 4. Kredit Azure

Kredit Azure atau benefit akun harus dicatat terpisah dari harga normal. Kredit dapat mengurangi tagihan yang dibayar selama masa berlaku, tetapi tidak mengubah biaya dasar layanan.

| Informasi kredit | Nilai |
|---|---|
| Kredit yang tercatat pada catatan proyek sebelumnya | USD 79 |
| Tanggal pengecekan catatan | 2026-11-07 |
| Masa berlaku dan saldo terbaru | Perlu diverifikasi pada portal Azure |
| Estimasi biaya setelah kredit | Belum dihitung; bergantung saldo dan layanan yang memenuhi syarat |

Jangan menganggap kredit USD 79 otomatis menutup biaya selama 12 bulan. Periksa saldo, masa berlaku, dan transaksi yang memenuhi syarat di portal Azure.

## 5. Sumber dan cara verifikasi

1. Azure Pricing Calculator — https://azure.microsoft.com/pricing/calculator/  
   Gunakan region Australia East, Linux, Standard B2ats v2, jam pemakaian 730 jam/bulan, dan jenis/ukuran disk aktual.
2. Microsoft Learn, *Estimate costs with the Azure pricing calculator* — https://learn.microsoft.com/en-us/azure/cost-management-billing/costs/pricing-calculator/
3. Harga VM pembanding Australia East, diperiksa 2026-11-08 — https://vmprices.com/azure/australiaeast/
4. Harga Managed Disk pembanding Australia East, diperiksa 2026-11-09 — https://instances.usage.ai/azure/disks/region/australiaeast

Harga pembanding dari situs pihak ketiga hanya untuk estimasi awal. Angka final harus mengikuti Azure Pricing Calculator dan Cost Management untuk subscription serta konfigurasi yang digunakan.

## 6. Data yang perlu dilengkapi

| Data | Nilai aktual | Sumber bukti |
|---|---|---|
| SKU VM dan region | Standard B2ats v2, Australia East (tercatat EV-01) | EV-01 |
| Jenis dan ukuran disk | Premium SSD, 30 GB (tercatat EV-01) | Azure VM > Disks |
| Harga VM aktual | Belum diverifikasi | Azure Pricing Calculator / Cost Management |
| Harga disk aktual | Belum diverifikasi | Azure Pricing Calculator / Cost Management |
| Domain dan biaya tahunan | Belum ditentukan | Invoice registrar |
| Backup offsite | Belum ditentukan | Kalkulator penyedia storage |
| Transfer data | Belum diukur | Azure Cost Management |
| Kredit dan sisa saldo | Perlu diperbarui | Azure Cost Management |

## 7. Kesimpulan sementara

Berdasarkan harga pembanding yang tersedia, biaya dasar VM dan disk diperkirakan sekitar USD 15.58 per bulan atau USD 186.91 untuk 12 bulan. Angka tersebut belum mencakup seluruh komponen sehingga belum boleh disebut sebagai TCO final. Estimasi perlu diperbarui menggunakan Azure Pricing Calculator dan data tagihan aktual sebelum dipakai sebagai dasar keputusan biaya proyek.
