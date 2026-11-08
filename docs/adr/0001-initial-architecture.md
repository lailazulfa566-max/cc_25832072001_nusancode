# ADR-0001: Arsitektur Deployment Awal (Single VM Azure)

## Status
Accepted

## Context
Azure Standard B2ats v2 (2 vCPU burstable, 1 GB RAM, 30 GB Premium SSD),
Ubuntu Server 24.04, kredit Azure for Students terbatas.

## Decision
Flask + Gunicorn (1 worker, 2 thread, bind 127.0.0.1:8000)
+ systemd + Caddy + UFW.

SQLite direncanakan untuk penyimpanan data pada M05 dan belum diterapkan pada M03.

## Alternatives
1. Django: ditolak, memori idle lebih berat untuk 1 GB RAM.
2. Docker: ditunda ke M06 agar stabilitas systemd dibuktikan dulu.
3. Managed database: ditolak, biaya di luar kredit dan tidak perlu untuk skala uji coba.

## Consequences
Positif: ringan, cepat dideploy, mudah dijelaskan.
Negatif: single point of failure; HTTP saja pada M03.

## Review Trigger
Ditinjau ulang pada M05 (data/backup) dan M06 (container) atau bila beban melampaui kapasitas.
