# Deployment Guide - Milestone 3

## 1. Prerequisites
- VPS running Linux (Ubuntu/Debian)
- Python 3 and pip installed
- Gunicorn web server configured as a systemd service

## 2. Manual Deployment Steps
1. Clone the repository to `/srv/cc-m03`
2. Create and activate a virtual environment:
   ```bash
   python3 -m venv .venv
   source .venv/bin/activate
