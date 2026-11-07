# Dokumentasi Milestone 3 - NusanCode

Selamat datang di pusat dokumentasi teknis proyek **NusanCode** untuk Milestone 3. Berikut adalah daftar dokumen pendukung dan hasil audit infrastruktur VPS:

## Daftar Dokumen Utama
- **[Requirements](./requirements.md)**: Problem statement, target pengguna, fitur fungsional (FR/NFR), serta batasan ruang lingkup (*scope*).
- **[Architecture](./architecture.md)**: Penjelasan arsitektur sistem (Flask, Gunicorn, Caddy) dan batasan sumber daya VPS.
- **[Deployment Guide](./deployment.md)**: Panduan langkah demi langkah untuk *manual deployment*, pembaruan (*update*), hingga *rollback*.
- **[Changelog](./changelog.md)**: Catatan riwayat perubahan versi aplikasi.
- **[Architecture Decision Record (ADR)](./adr/0001-initial-architecture.md)**: Catatan keputusan desain arsitektur awal.

## Bukti Pengujian & Audit VPS (Evidence M03)
Seluruh hasil audit sistem, keamanan, dan kesehatan aplikasi dapat dilihat di dalam folder **[Evidence M03](./evidence/m03/)**:
- `os.txt`: Versi sistem operasi VPS.
- `resources.txt`: Kapasitas CPU, RAM, dan penyimpanan disk.
- `ufw.txt`: Status aturan keamanan firewall.
- `ports.txt`: Audit port jaringan yang terbuka.
- `service.txt`: Status layanan *systemd* untuk aplikasi Gunicorn.
- `health-internal.txt`: Hasil pengujian kesehatan server secara internal.
- `health-public.txt`: Hasil pengujian akses publik server.
- `notes.md`: Catatan tambahan pengujian M03.Dokumentasi Milestone 3 NusanCode
