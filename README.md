# Omega Manifesto — Interactive Site

An elegant, static site for **"Manifesto of an Omega-Type Civilization"** with client UI, plus a tiny **secure proxy server** for Gemini text, image, and TTS requests. Ready for GitHub Pages (static) + any Node host for the API (Render, Railway, Fly, your VPS).

## ✨ Features
- Beautiful, responsive Tailwind UI (your original design preserved)
- Text generation, image generation, and TTS via Gemini (proxied securely)
- Zero client-side secrets (API key stays on the server)
- GitHub Pages workflow included
- Conventional Commits, basic CI

---

## 🧭 Repo Structure
```
.
├─ site/                     # Static site (GitHub Pages)
│  └─ index.html             # Adapted to use server proxy endpoints
├─ server/                   # Minimal Node/Express API proxy
│  ├─ index.js
│  ├─ package.json
│  ├─ .env.example
│  └─ Dockerfile
├─ .github/workflows/
│  ├─ ci.yml                 # Basic CI
│  └─ pages.yml              # Deploy /site to GitHub Pages
├─ .gitignore
├─ LICENSE
├─ CONTRIBUTING.md
├─ CODE_OF_CONDUCT.md
├─ SECURITY.md
└─ CHANGELOG.md
```

> **Why proxy?** GitHub Pages is static and public. If you call Google APIs directly from the browser you must ship an API key — unsafe. The small server keeps your key secret and can be hosted anywhere.

---

## 🚀 Quick Start

### 1) Local dev (server + site)
```bash
# 1. Clone your repo
git clone git@github.com:<your-username>/<your-repo>.git
cd <your-repo>

# 2. Run the server
cd server
cp .env.example .env     # add your GOOGLE_API_KEY to .env
npm install
npm run dev              # http://localhost:8787

# 3. Open the site
# The server serves /site as static. Visit:
#   http://localhost:8787
```

### 2) Deploy static site to GitHub Pages
- Push to GitHub and enable **Pages** (Settings → Pages → "Build and deploy: GitHub Actions").
- The provided workflow `.github/workflows/pages.yml` will deploy `site/` automatically on each push to `main`.

### 3) Deploy the server (pick one)
- **Render** / **Railway** / **Fly.io** / **VPS** / **Docker** — all work.
- Set env var `GOOGLE_API_KEY` on the platform.
- Expose port **8787** (or your chosen port).

Now set the site to call your server in production. Add to `site/index.html` before closing `</head>` or right after `<body>`:
```html
<script>
  window.OMEGA_API_BASE = "https://your-server-domain.example.com";
</script>
```
In local dev, you can leave it empty — it defaults to same origin.

---

## 🔐 Secrets & Security
- Never commit `.env` or API keys.
- The server reads `GOOGLE_API_KEY` from env and proxies requests.
- CORS is locked down by default to your Pages domain (edit as needed).

---

## 🧪 CI
- `ci.yml` checks Node version and that the server starts.
- Extend it with tests as you grow.

---

## 📝 Conventional Commits
Use prefixes like `feat:`, `fix:`, `docs:`, `refactor:` etc.

---

## 📄 License
MIT. See [LICENSE](LICENSE).

---

## 🤝 Contributing
See [CONTRIBUTING.md](CONTRIBUTING.md).
