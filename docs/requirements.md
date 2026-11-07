# Requirements NusanCode

## Problem Statement
Guru TIK SMA menyusun soal dan merekap nilai secara manual, dan materi belum dikaitkan dengan kearifan lokal. NusanCode menyediakan e-modul bertema kearifan lokal, pengumpulan tugas, rekap nilai, dan generator kuis pilihan ganda otomatis.

## Target Users dan Peran
- **Guru:** Mengelola kelas, modul, kuis, nilai, serta meninjau hasil generator kuis AI sebelum dipublikasikan.
- **Siswa:** Mengakses modul, mengerjakan kuis, dan mengumpulkan tugas.

## Definisi Istilah
"Deep Learning" pada judul proyek berarti **pendekatan pembelajaran mendalam (pedagogis)**, bukan model kecerdasan buatan. Komponen AI hanya berupa fitur generator kuis yang memanggil OpenAI API (`gpt-4o-mini`).

## Functional Requirements (FR)
- **FR-01:** Autentikasi dan pembagian hak akses pengguna berdasarkan peran (guru dan siswa).
- **FR-02:** Pengelolaan modul pembelajaran berbasis kearifan lokal.
- **FR-03:** Pengumpulan tugas dan penyimpanan rekap nilai menggunakan basis data SQLite.
- **FR-04:** Generator kuis otomatis via OpenAI API dengan opsi peninjauan oleh guru.
- **FR-05:** Sistem menyediakan endpoint `GET /health` untuk pemeriksaan kesehatan layanan peladen.

## Non-Functional Requirements (NFR)
- **NFR-01:** Backend Gunicorn hanya *listen* pada antarmuka *loopback* (`127.0.0.1:8000`).
- **NFR-02:** Aplikasi dikelola secara otomatis oleh *systemd service*.
- **NFR-03:** Seluruh akses publik masuk melalui Caddy *reverse proxy*.
- **NFR-04:** Tidak ada *secret* atau kunci privat yang disimpan di dalam repositori Git (menggunakan `.env` di luar Git).
- **NFR-05:** Arsitektur dioptimalkan untuk batas sumber daya VPS 2 vCPU dan RAM 1 GB (Azure Standard B2ats v2).

## Batasan Ruang Lingkup M03
- Infrastruktur menggunakan satu instance VM (potensi *single point of failure*).
- Belum menggunakan domain atau HTTPS definitif (dijadwalkan pada M04).
- Target RPO dan RTO masih berupa rancangan awal sebelum diuji secara empiris.

## Constraints
- Azure Standard B2ats v2: 2 vCPU (burstable), 1 GB RAM, 30 GB Premium SSD
- Ubuntu Server 24.04 LTS, satu IPv4 publik

## Cakupan M03
- **Termasuk:** repository, requirements, arsitektur v0.1, ADR-0001, aplikasi dasar dengan `/health`,
  hardening SSH, UFW, Gunicorn, systemd, Caddy, deployment HTTP
- **Tidak termasuk:** database produksi, container, IaC, CI/CD, domain dan HTTPS (M04),
  backup dan restore (M05)

## Kriteria penerimaan M03
- [x] `/health` mengembalikan HTTP 200
- [x] Gunicorn listen di `127.0.0.1:8000`
- [x] Service tetap hidup setelah reboot
- [x] Evidence tersimpan di `docs/evidence/m03/`
- [x] Halaman utama dapat dibuka dari internet (HTTP), dites dari HP
