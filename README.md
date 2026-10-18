# EVEL LumaGlass Studio

An Arabic RTL media-processing workspace with a liquid-glass visual interface. It combines a static frontend with a FastAPI backend, FFmpeg/Pillow processing, a Redis/RQ queue, and optional S3-compatible result storage.

## Available tools

- Compress video with quality and resolution controls.
- Convert common video/audio formats.
- Extract audio, export a frame, or trim a clip.
- Convert images and constrain their maximum width.
- Conventional scaling and sharpening for images/videos (not AI restoration).
- Queue/progress/history UI and temporary-file cleanup.
- Optional direct media-file URL import with HTTPS and hostname allowlisting. Social-media post URLs are intentionally not supported.

## Deploy

- **Demo:** use `render.yaml` via Render Blueprint. See [`RENDER_DEPLOYMENT.md`](RENDER_DEPLOYMENT.md). This profile is deliberately a single Docker service and uses ephemeral storage; queued jobs/results can be lost on restart or idle spin-down.
- **More robust hosting:** use [`media-studio/Dockerfile`](media-studio/Dockerfile) and [`media-studio/docker-compose.yml`](media-studio/docker-compose.yml) on a Docker server with persistent storage. See [`media-studio/DEPLOYMENT.md`](media-studio/DEPLOYMENT.md).

This is a full-stack media app, not a static-only Vercel website. The service needs Python dependencies, FFmpeg, Redis/RQ, and writable temporary storage. Keep `REQUIRE_API_KEY=true`, set an unpredictable `API_ACCESS_TOKEN`, and serve public traffic over HTTPS with rate limiting.

## Repository setup

Put this package in its **own repository**. Do not overwrite the unrelated `buildlab-egypt` website or the Telegram bot repository. The `.github/workflows/lumaglass-checks.yml` workflow checks Python syntax, frontend JavaScript syntax, media operations, and both Docker build profiles.

## Local checks

```bash
cd media-studio
python -m pip install -r requirements.txt pytest
python -m py_compile app/main.py app/jobs.py
python -m pytest -q tests
```

See [`media-studio/README.md`](media-studio/README.md) for configuration, optional R2 setup, import constraints, and production notes.

© 2026 EVEL. See [`media-studio/COPYRIGHT.md`](media-studio/COPYRIGHT.md) for third-party license notices.
