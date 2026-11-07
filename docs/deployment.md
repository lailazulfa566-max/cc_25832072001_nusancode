# Deployment Guide — Milestone 3

## Ringkasan
- VM: Azure Standard B2ats v2 (2 vCPU, 1 GB RAM, 30 GB), Ubuntu Server 24.04 LTS
- Akun administrasi: `cloudstudent` (non-root, sudo)
- Lokasi aplikasi: `/home/cloudstudent/cc_25832072001_nusancode`
- Virtual environment: `venv/`
- Service: `cc-m03.service` (Gunicorn 1 worker, 2 thread, bind `127.0.0.1:8000`)
- Reverse proxy: Caddy `:80` meneruskan ke `127.0.0.1:8000`
- Firewall: UFW (22 dan 80) dan NSG Azure

## Deployment manual
1. Clone repository dan masuk ke foldernya:
   ```bash
   git clone https://github.com/lailazulfa566-max/cc_25832072001_nusancode
   cd cc_25832072001_nusancode
   ```
2. Buat virtual environment dan pasang dependensi:
   ```bash
   python3 -m venv venv
   source venv/bin/activate
   python -m pip install -r requirements.txt
   ```
3. Uji manual:
   ```bash
   venv/bin/gunicorn --workers 1 --threads 2 --bind 127.0.0.1:8000 app:app
   curl -i http://127.0.0.1:8000/health
   ```
4. Pasang service di `/etc/systemd/system/cc-m03.service` (isi lengkap ada di
   `docs/evidence/m03/cc-m03.service.txt`), lalu:
   ```bash
   sudo systemctl daemon-reload
   sudo systemctl enable --now cc-m03
   ```
5. Konfigurasi Caddy di `/etc/caddy/Caddyfile`:
   ```
   :80 {
       encode zstd gzip
       reverse_proxy 127.0.0.1:8000
   }
   ```
   ```bash
   sudo caddy validate --config /etc/caddy/Caddyfile
   sudo systemctl enable --now caddy
   ```
6. Verifikasi:
   ```bash
   sudo ss -ltnp                      # gunicorn di 127.0.0.1:8000, caddy di :80
   curl -i http://127.0.0.1/health    # 200 OK
   ```

Pada M03 belum ada secret. Untuk fitur berikutnya, simpan secret di `.env` di luar repository.

## Prosedur update
```bash
cd ~/cc_25832072001_nusancode
git pull
source venv/bin/activate
python -m pip install -r requirements.txt
sudo systemctl restart cc-m03
curl -fsS http://127.0.0.1/health
```

## Rollback dasar
```bash
git log --oneline --decorate -10
git checkout m03
sudo systemctl restart cc-m03
curl -fsS http://127.0.0.1/health
git switch main
```

## Troubleshooting
| Gejala | Cek |
|---|---|
| 502 Bad Gateway | `sudo journalctl -u cc-m03 -n 100 --no-pager` |
| Tidak bisa diakses dari luar | `sudo ufw status`, aturan NSG Azure, `sudo ss -ltnp` |
| Caddy gagal start | `sudo caddy validate --config /etc/caddy/Caddyfile` |
| Port 80 bentrok | `sudo ss -ltnp \| grep :80` (harus hanya Caddy) |
