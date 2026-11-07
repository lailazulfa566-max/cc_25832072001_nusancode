# EV-01 — Spesifikasi dan Inventaris VPS

Tanggal/waktu pengamatan: 2026-11-07 [JAM] WIB
Pelaksana: Lailatul Zulfa (25832072001)

## Identitas sumber daya
| Item | Nilai |
|---|---|
| Provider / region | Microsoft Azure / [Australia East] |
| SKU | Standard B2ats v2 |
| Alamat IPv4 publik | 20.211.31.222 |
| Akun admin | cloudstudent (non-root) |

## Bukti teknis (output asli)
| Pemeriksaan | Berkas |
|---|---|
| OS dan kernel | docs/evidence/m03/os.txt |
| CPU, RAM, disk | docs/evidence/m03/resources.txt |
| Firewall UFW | docs/evidence/m03/ufw.txt |
| Port yang listen | docs/evidence/m03/ports.txt |
| Service aplikasi | docs/evidence/m03/service.txt, cc-m03.service.txt |
| Caddy dan Caddyfile | docs/evidence/m03/caddy.txt, Caddyfile.txt |
| Pengaturan SSH | docs/evidence/m03/ssh.txt |
| Health check | docs/evidence/m03/health-internal.txt, health-public.txt |
| Akses dari luar | docs/evidence/m03/public-access.png |

## Hasil
- Gunicorn listen di 127.0.0.1:8000 (loopback), Caddy di port 80.
- UFW aktif (22 dan 80). Login root dan password SSH dinonaktifkan.
- Service cc-m03 dan caddy aktif otomatis setelah reboot.

Status: LULUS
Isu tersisa: HTTPS/FQDN belum (dijadwalkan M04). Backup dan restore belum (M05).
