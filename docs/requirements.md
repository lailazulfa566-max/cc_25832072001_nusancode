# Requirements NusanCode

## Problem Statement

NusanCode merupakan platform e-learning TIK berbasis kearifan lokal yang dirancang untuk mendukung proses pembelajaran secara digital. Platform ini mengadopsi konsep Learning Management System (LMS) seperti Edlink, sehingga guru dan siswa dapat melakukan kegiatan pembelajaran melalui satu platform.

NusanCode menyediakan fitur pengelolaan kelas, penyampaian materi, pengumpulan tugas, pelaksanaan kuis, dan rekap nilai. Selain itu, NusanCode dilengkapi fitur AI berbasis OpenAI API yang membantu guru membuat kuis secara otomatis berdasarkan materi atau topik pembelajaran dengan bentuk soal yang fleksibel. Materi pembelajaran juga diarahkan untuk menghubungkan pengetahuan TIK dengan budaya dan kearifan lokal Indonesia.

## Target Users dan Peran

- **Guru:** Mengelola kelas, mengunggah materi pembelajaran, memberikan tugas, membuat kuis dengan bantuan AI, mengelola nilai, serta meninjau dan mengedit kuis sebelum dipublikasikan.
- **Siswa:** Bergabung ke kelas, mengakses materi pembelajaran, mengerjakan kuis, mengumpulkan tugas, dan melihat hasil atau nilai pembelajaran.

## Definisi Istilah

"Deep Learning" pada judul proyek berarti **pendekatan pembelajaran mendalam (pedagogis)**, bukan model kecerdasan buatan. Komponen AI pada NusanCode direncanakan menggunakan OpenAI API untuk membantu guru menghasilkan kuis berdasarkan materi atau topik pembelajaran.

## Functional Requirements (FR)

Daftar berikut merupakan kebutuhan fungsional yang direncanakan untuk pengembangan NusanCode. Tidak seluruh fitur sudah diimplementasikan pada M03.

- **FR-01:** Sistem menyediakan autentikasi dan pembagian hak akses pengguna berdasarkan peran, yaitu guru dan siswa.
- **FR-02:** Sistem menyediakan fitur pengelolaan kelas dan modul pembelajaran berbasis kearifan lokal.
- **FR-03:** Sistem menyediakan fitur pengumpulan tugas dan penyimpanan rekap nilai menggunakan basis data SQLite yang direncanakan untuk diterapkan pada M05.
- **FR-04:** Sistem menyediakan fitur generator kuis berbasis OpenAI API yang membantu guru membuat berbagai jenis soal secara otomatis berdasarkan materi atau topik pembelajaran. Guru dapat meninjau dan mengedit soal sebelum dipublikasikan kepada siswa.
- **FR-05:** Sistem menyediakan endpoint `GET /health` untuk pemeriksaan kesehatan layanan peladen.

## Non-Functional Requirements (NFR)

- **NFR-01:** Backend Gunicorn hanya *listen* pada antarmuka *loopback* (`127.0.0.1:8000`).
- **NFR-02:** Aplikasi dikelola secara otomatis menggunakan *systemd service*.
- **NFR-03:** Seluruh akses publik masuk melalui Caddy sebagai *reverse proxy*.
- **NFR-04:** Tidak ada *secret* atau kunci privat yang disimpan di dalam repositori Git. Konfigurasi rahasia yang diperlukan untuk fitur tertentu nantinya disimpan di luar repositori, misalnya menggunakan file `.env`.
- **NFR-05:** Arsitektur dioptimalkan untuk batas sumber daya VPS 2 vCPU dan RAM 1 GB (Azure Standard B2ats v2).

## Batasan Ruang Lingkup M03

- Infrastruktur menggunakan satu instance VM sehingga masih memiliki potensi *single point of failure*.
- Belum menggunakan domain atau HTTPS definitif karena dijadwalkan pada M04.
- Database produksi, backup, dan restore belum diterapkan karena direncanakan pada M05.
- Fitur pengelolaan kelas, materi, tugas, kuis AI, dan rekap nilai masih merupakan kebutuhan pengembangan dan belum seluruhnya tersedia pada M03.
- Target RPO dan RTO masih berupa rancangan awal sebelum diuji secara empiris.

## Constraints

- Azure Standard B2ats v2: 2 vCPU (*burstable*), 1 GB RAM, dan 30 GB Premium SSD.
- Ubuntu Server 24.04 LTS.
- Menggunakan satu IPv4 publik.
- Pengembangan dan deployment menyesuaikan keterbatasan sumber daya VPS.

## Cakupan M03

- **Termasuk:** repository, requirements, arsitektur v0.1, ADR-0001, aplikasi dasar dengan endpoint `/health`, hardening SSH, UFW, Gunicorn, systemd, Caddy, dan deployment melalui HTTP.
- **Tidak termasuk:** database produksi, fitur AI generator kuis, container, Infrastructure as Code (IaC), CI/CD, domain dan HTTPS (M04), serta backup dan restore (M05).

## Kriteria Penerimaan M03

- [x] Endpoint `/health` mengembalikan HTTP 200.
- [x] Gunicorn *listen* pada `127.0.0.1:8000`.
- [x] Service tetap berjalan setelah VPS mengalami reboot.
- [x] Evidence tersimpan di `docs/evidence/m03/`.
- [x] Halaman utama dapat diakses melalui internet menggunakan HTTP dan telah diuji melalui HP.
