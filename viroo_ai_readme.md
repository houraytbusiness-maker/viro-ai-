<div align="center">

# Viroo AI

**Open-Source AI Creative Studio & Multi-Platform Ad Launcher — All in One Place.**

[![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg)](https://opensource.org/licenses/MIT)
[![PRs Welcome](https://img.shields.io/badge/PRs-welcome-brightgreen.svg)](CONTRIBUTING.md)
[![Self-Hostable](https://img.shields.io/badge/Self--Hostable-Docker-2496ED.svg)](#getting-started)
[![Status](https://img.shields.io/badge/Status-Active%20Development-orange.svg)](#roadmap)

</div>

---

## Overview

**Viroo AI** is an open-source, self-hostable platform that unifies **multi-model AI ad creative generation** (video, image, and voiceover) with **streamlined multi-platform ad campaign launching** (Meta, TikTok, Snapchat, and more).

### The Problem We Solve
Indie developers, e-commerce founders, and lean marketing teams currently face a fragmented and expensive workflow:
1. Paying for multiple separate SaaS subscriptions to generate ad videos, static creatives, and AI voiceovers.
2. Manually downloading, organizing, and re-uploading assets across multiple disconnected ad managers.
3. Dealing with vendor lock-in and high per-seat or usage markups.

**Viroo AI** bridges this gap by bringing the entire creative-to-launch pipeline into a single, developer-friendly, **Bring-Your-Own-Key (BYOK)** open-source codebase.

---

## Key Features

### 1. Multi-Model AI Creative Studio
- **AI Video Generation:** Plug-and-play adapters for leading video generation models to create high-converting short-form ad creatives.
- **AI Image Generation:** Generate, upscale, and resize product shots and ad banners for all aspect ratios (`9:16`, `1:1`, `16:9`).
- **AI Voiceovers & Audio:** Multi-language, natural-sounding voice synthesis for UGC-style and direct-response video ads.
- **Unified Asset Library:** Organize generated creatives, scripts, and variations in one searchable workspace.

### 2. Multi-Platform Ad Launcher
- **One-Click Publishing:** Push creatives directly from the studio to connected ad accounts without manual re-uploading.
- **Unified Campaign Templates:** Standardize campaign structures, budgets, and targeting presets across platforms.
- **Marketing API Integrations:** Modular connectors designed for Meta Marketing API, TikTok Marketing API, Snapchat Ads API, and Google Ads.
- **OAuth & Token Management:** Secure, encrypted handling of ad account tokens and refresh lifecycles.

### 3. Developer-First & Self-Hostable
- **Bring Your Own Keys (BYOK):** Connect your own AI provider API keys with zero platform markup.
- **Async Media Pipeline:** Background job processing for heavy video rendering, transcoding, and API uploads.
- **Full Data Ownership:** Deploy on your own VPS, Docker setup, or cloud infrastructure.

---

## Architecture Overview

```text
+-------------------------------------------------------------------+
|                         Viroo AI Web App                          |
|        (Creative Studio | Asset Library | Ad Launcher UI)         |
+---------------------------------+---------------------------------+
                                  |
                                  v
+-------------------------------------------------------------------+
|                      Core API & Orchestrator                      |
|      (Auth/OAuth | Campaign Builder | Rate Limiting | Webhooks)   |
+----------------+----------------------------------+---------------+
                 |                                  |
                 v                                  v
+---------------------------------+  +------------------------------+
|     Async Media Job Queue       |  |    Ad Platform Connectors    |
|  (Video / Image / Voice Models) |  | (Meta | TikTok | Snap | ...) |
+----------------+----------------+  +--------------+---------------+
                 |                                  |
                 v                                  v
+---------------------------------+  +------------------------------+
|   Object Storage (S3 / R2)      |  |    External Marketing APIs   |
+---------------------------------+  +------------------------------+
```

---

## Tech Stack

- **Frontend & Full-Stack Framework:** Next.js (App Router), React, TypeScript, Tailwind CSS
- **Database & ORM:** PostgreSQL, Prisma / Drizzle ORM
- **Background Jobs & Queues:** Redis / BullMQ (for asynchronous AI generation & ad publishing pipelines)
- **Media Storage:** S3-compatible storage (AWS S3, Cloudflare R2, or MinIO)
- **Deployment:** Docker & Docker Compose

---

## Getting Started

### Prerequisites
- Node.js `>= 20.x`
- PostgreSQL & Redis (or Docker)
- API keys for your preferred AI providers and Ad Platform Developer Apps

### 1. Clone the Repository
```bash
git clone https://github.com/<your-username>/viroo-ai.git
cd viroo-ai
```

### 2. Install Dependencies
```bash
npm install
```

### 3. Configure Environment Variables
Copy the example environment file and fill in your credentials:
```bash
cp .env.example .env
```

```env
# Database & Queue
DATABASE_URL="postgresql://user:password@localhost:5432/viroo_ai"
REDIS_URL="redis://localhost:6379"

# Storage (S3 / Cloudflare R2)
S3_BUCKET="viroo-assets"
S3_ENDPOINT=""
S3_ACCESS_KEY_ID=""
S3_SECRET_ACCESS_KEY=""

# AI Provider Keys (BYOK)
AI_VIDEO_API_KEY=""
AI_IMAGE_API_KEY=""
AI_VOICE_API_KEY=""

# Ad Platform OAuth Apps
META_APP_ID=""
META_APP_SECRET=""
TIKTOK_APP_ID=""
TIKTOK_APP_SECRET=""
```

### 4. Run Database Migrations & Start Dev Server
```bash
npx prisma migrate dev
npm run dev
```

Open `http://localhost:3000` in your browser to access Viroo AI.

---

## Roadmap

- [x] Core architecture & modular provider interface
- [x] Unified Creative Studio UI (Image & Voice generation workflows)
- [x] Multi-model AI Video generation pipeline
- [ ] Meta Marketing API full campaign launcher & ad set templates
- [ ] TikTok & Snapchat Marketing API connectors
- [ ] Automated A/B creative testing & cross-platform ROAS dashboard
- [ ] One-command Docker Compose production deployment
- [ ] Comprehensive unit & integration test suite for all API wrappers

---

## Contributing

We welcome contributions from the open-source community! Whether it's adding a new AI model adapter, improving an ad platform connector, fixing bugs, or enhancing documentation, your help is appreciated.

1. Fork the repository.
2. Create a feature branch (`git checkout -b feat/new-ai-provider`).
3. Commit your changes (`git commit -m "feat: add new AI video provider adapter"`).
4. Push to the branch (`git push origin feat/new-ai-provider`).
5. Open a Pull Request.

Please open an issue first for major architectural changes so we can discuss the best approach.

---

## License

This project is open-source and licensed under the **MIT License**. See the [LICENSE](LICENSE) file for full details.