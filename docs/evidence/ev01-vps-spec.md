# EV-01 — Spesifikasi dan Inventaris VPS

Tanggal/waktu pengamatan: 2026-11-07, sekitar 22.16–22.25 WIB
Pelaksana: Lailatul Zulfa (25832072001)

## Identitas sumber daya
| Item | Nilai |
|---|---|
| Provider / region | Microsoft Azure / Australia East |
| Resource group / nama VM | vm_cc_zulfa / LailaZulfa |
| SKU | Standard B2ats v2 (2 vCPU, 1 GiB RAM) |
| OS | Ubuntu Server 24.04 LTS |
| Disk | 30 GB Premium SSD (disk OS, tanpa disk data) |
| Alamat IPv4 publik | 20.211.31.222 |
| Akun admin | cloudstudent (non-root, sudo) |

Subscription ID sengaja tidak dicantumkan (tersanitasi).

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
| Baseline keamanan | docs/evidence/m03/security-baseline.txt |
| Health check | docs/evidence/m03/health-internal.txt, health-public.txt |
| Akses dari luar | docs/evidence/m03/public-access.png |

## Hasil
- Gunicorn listen di 127.0.0.1:8000 (loopback), Caddy di port 80.
- UFW aktif (22 dan 80). Login root dan password SSH dinonaktifkan; `AllowUsers cloudstudent`.
- Setelah reboot (boot terakhir 2026-11-07 22:22:39 WIB), service cc-m03 dan caddy aktif otomatis
  dan `/health` menjawab 200 OK.

Status: LULUS

## Isu tersisa
- SSH memakai kunci RSA bawaan Azure; kunci Ed25519 sesuai modul belum diterapkan.
- HTTPS/FQDN belum (dijadwalkan M04). Backup dan restore belum (M05).
