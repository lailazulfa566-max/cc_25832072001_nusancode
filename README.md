# NusanCode — Web E-Learning TIK Berbasis Kearifan Lokal

Proyek Individu Cloud Computing (PTI 2802), Institut Pendidikan Indonesia
Semester Ganjil 2026/2027
Dosen: Muhaemin Sidiq, S.Pd., M.Pd.

**Mahasiswa:** Lailatul Zulfa
**NIM:** 25832072001
**Kelas:** PTI 2A

**Judul lengkap:** Pengembangan Web E-Learning Interaktif Berbasis Kearifan Lokal dengan Pendekatan Deep Learning pada Mata Pelajaran TIK di SMA

## 1. Tentang NusanCode

NusanCode merupakan platform e-learning TIK berbasis kearifan lokal yang dirancang untuk mendukung proses pembelajaran secara digital. Platform ini mengadopsi konsep Learning Management System (LMS) seperti Edlink agar guru dan siswa dapat melakukan kegiatan pembelajaran melalui satu platform.

NusanCode direncanakan memiliki fitur pengelolaan kelas, penyampaian materi, pengumpulan tugas, pelaksanaan kuis, dan rekap nilai. Materi pembelajaran dikaitkan dengan budaya dan kearifan lokal Indonesia agar pembelajaran TIK lebih kontekstual.

Selain itu, NusanCode direncanakan memiliki fitur AI berbasis OpenAI API untuk membantu guru membuat kuis berdasarkan materi atau topik pembelajaran.

## 2. Definisi Istilah

"Deep Learning" pada judul proyek berarti pendekatan pembelajaran mendalam (pedagogis), bukan teknologi AI. Fitur AI NusanCode direncanakan menggunakan OpenAI API untuk membantu guru membuat berbagai jenis kuis. Model yang direncanakan adalah `gpt-4o-mini`.

## 3. Target Pengguna

- **Guru:** Mengelola kelas, mengunggah materi, memberikan tugas, membuat kuis dengan bantuan AI, serta mengelola nilai.
- **Siswa:** Bergabung ke kelas, mengakses materi, mengerjakan kuis, mengumpulkan tugas, dan melihat nilai.

## 4. Status Fitur

Tidak seluruh fitur NusanCode sudah diterapkan pada M03.

| Fitur | Status |
|---|---|
| Halaman utama dan endpoint `GET /health` | Tersedia (M03) |
| Autentikasi guru dan siswa | Rencana |
| Pengelolaan kelas dan materi | Rencana |
| Pengumpulan tugas dan rekap nilai | Rencana |
| Database SQLite | Rencana (M05) |
| Generator kuis AI | Rencana |

## 5. Infrastruktur

Bukti spesifikasi VPS tersedia di `docs/evidence/ev01-vps-spec.md`.

| Komponen | Keterangan |
|---|---|
| Provider | Microsoft Azure |
| Region | Australia East |
| VM | Standard B2ats v2 |
| CPU | 2 vCPU (burstable) |
| RAM | 1 GB |
| Penyimpanan | 30 GB Premium SSD |
| Sistem Operasi | Ubuntu Server 24.04 LTS |
| Alamat Website | http://20.211.31.222 |
| Teknologi | Flask, Gunicorn, systemd, Caddy, UFW |

Akses website saat ini masih menggunakan HTTP. Domain dan HTTPS direncanakan pada M04.

## 6. Arsitektur Sistem

Garis penuh menunjukkan komponen yang sudah berjalan pada M03. Garis putus-putus menunjukkan komponen yang masih direncanakan.

```mermaid
flowchart TB
    U[Guru dan Siswa] -->|HTTP :80| C[Caddy]
    C -->|127.0.0.1:8000| G[Gunicorn]
    G --> F[Flask Application]
    F -.->|Rencana M05| D[(SQLite)]
    F -.->|Rencana| O[OpenAI API]
cat >> README.md <<'EOF'
## 5. Infrastruktur

Bukti spesifikasi VPS tersedia di `docs/evidence/ev01-vps-spec.md`.

| Komponen | Keterangan |
|---|---|
| Provider | Microsoft Azure |
| Region | Australia East |
| VM | Standard B2ats v2 |
| CPU | 2 vCPU (burstable) |
| RAM | 1 GB |
| Penyimpanan | 30 GB Premium SSD |
| Sistem Operasi | Ubuntu Server 24.04 LTS |
| Alamat Website | http://20.211.31.222 |
| Teknologi | Flask, Gunicorn, systemd, Caddy, UFW |

Akses website saat ini masih menggunakan HTTP. Domain dan HTTPS direncanakan pada M04.

## 6. Arsitektur Sistem

Garis penuh menunjukkan komponen yang sudah berjalan pada M03. Garis putus-putus menunjukkan komponen yang masih direncanakan.

```mermaid
flowchart TB
    U[Guru dan Siswa] -->|HTTP :80| C[Caddy]
    C -->|127.0.0.1:8000| G[Gunicorn]
    G --> F[Flask Application]
    F -.->|Rencana M05| D[(SQLite)]
    F -.->|Rencana| O[OpenAI API]
