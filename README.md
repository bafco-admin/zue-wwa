<div align="center">

<img src="https://img.shields.io/badge/Payzue-Payment%20Infrastructure-7c3aed?style=for-the-badge&logoColor=white" alt="Payzue" />

# Payzue - Public Website

**Modern, responsive marketing site for Payzue - India's payment infrastructure platform.**

[![HTML5](https://img.shields.io/badge/HTML5-E34F26?style=flat-square&logo=html5&logoColor=white)](https://developer.mozilla.org/en-US/docs/Web/HTML)
[![CSS3](https://img.shields.io/badge/CSS3-1572B6?style=flat-square&logo=css3&logoColor=white)](https://developer.mozilla.org/en-US/docs/Web/CSS)
[![JavaScript](https://img.shields.io/badge/JavaScript-F7DF1E?style=flat-square&logo=javascript&logoColor=black)](https://developer.mozilla.org/en-US/docs/Web/JavaScript)
[![Cloudflare](https://img.shields.io/badge/Cloudflare-F38020?style=flat-square&logo=cloudflare&logoColor=white)](https://cloudflare.com)
[![License](https://img.shields.io/badge/License-Proprietary-red?style=flat-square)](LICENSE)

[Live Site](https://thepayzue.com) · [Get Started](mailto:support@payzue.com) · [Report Bug](mailto:support@payzue.com)

</div>

---

## Overview

This repository contains the public-facing marketing website for **Payzue** - a secure, scalable payment infrastructure platform built for businesses across India. The site is a zero-dependency, single-file HTML/CSS/JS implementation optimised for performance, accessibility, and SEO.

Payzue handles UPI and wallets so product teams can focus on building - not managing payment plumbing.

> **This repo is the website only.** The broader Payzue platform also includes:

| Service             | Description                                                 |
| ------------------- | ----------------------------------------------------------- |
| **Payzue Gateway** | Core payment processing engine (Spring Boot, UPI / wallets) |
| **CipherBank**      | Bank statement reconciliation and settlement automation     |
| **Payzue Relay**   | Android SMS gateway for real-time transaction notifications |

---

## Page Sections

| Section          | Selector          | Content                                                                                                    |
| ---------------- | ----------------- | ---------------------------------------------------------------------------------------------------------- |
| Header / Nav     | `header`          | Sticky glassmorphism navbar with theme toggle and mobile drawer                                            |
| Hero             | `.hero`           | Headline, CTA, animated UPI Scan & Pay phone visual, live badge                                            |
| Stats            | `.stats`          | 50+ payment options · 97%+ success rate · 1M+ monthly transactions · 24/7 support                          |
| Partners Marquee | `.partners-strip` | Auto-scrolling strip: X (Twitter), LinkedIn, HDFC, Yes Bank, Axis, ICICI, REST APIs, Shopify, WooCommerce  |
| Features         | `#features`       | 6-card grid covering payment methods, performance, payouts, security, DX, monitoring                       |
| How It Works     | `.how-it-works`   | 3-step onboarding: create credentials → first API call → go live                                           |
| Developers       | `#developers`     | Multi-tab live API code block (cURL, Node.js, Python, Java, Go) with copy button, Payzue watermark         |
| Security         | `#security`       | Enterprise-grade pillars: TLS 1.3, HMAC-SHA256 signing, rate limiting, audit logs, PCI-DSS, RBI compliance |
| Pricing          | `#pricing`        | Growth and Enterprise tiers                                                                                |
| FAQ              | `.faq-section`    | Accordion-style common questions                                                                           |
| CTA              | `.cta-section`    | Full-width call-to-action with urgency copy                                                                |
| Footer           | `footer`          | Links, address, newsletter strip, copyright                                                                |

---

## Features

- **Light / Dark mode** - system preference detection with animated circular reveal transition, persisted via `localStorage`
- **Scroll-driven card animations** - `IntersectionObserver`-based reveal with per-card stagger delays
- **Animated UPI Scan & Pay visual** - CSS `perspective` + `transform-style: preserve-3d` phone mockup with hover tilt, a looping scan → processing → success sequence, and floating settlement toasts
- **Responsive layout** - mobile-first grid, slide-in hamburger nav, fluid typography with `clamp()`
- **Animated background** - layered radial gradients and moving grid/dot patterns that adapt to theme
- **Animated stat counters** - numbers count up from 0 on first viewport entry
- **Multi-language code tabs** - cURL, Node.js, Python, Java, Go with one-click clipboard copy
- **Integration partners marquee** - infinite auto-scroll strip with `animation-play-state` pause on hover
- **Scroll progress indicator** - gradient bar fixed below the navbar
- **Back-to-top button** - appears after 400px scroll, smooth scroll on click
- **Mobile nav auto-close** - clicking a nav link collapses the hamburger menu
- **Custom error pages** - branded `404` (Not Found) and `502` (Bad Gateway) pages

---

## Tech Stack

| Layer     | Technology                                                                                  |
| --------- | ------------------------------------------------------------------------------------------- |
| Markup    | Semantic HTML5 (`<header>`, `<nav>`, `<section>`, `<footer>`, `<article>`)                  |
| Styling   | Vanilla CSS3 - custom properties, grid, flexbox, `clamp()`, `@keyframes`, `backdrop-filter` |
| Scripting | Vanilla ES6+ JavaScript - no frameworks, no build step                                      |
| Fonts     | Google Fonts: `Inter` (body) · `Montserrat` (display) · `JetBrains Mono` (code)             |
| CDN / DNS | Cloudflare - edge caching, DDoS protection                                                  |
| Hosting   | Nginx reverse proxy via aaPanel (GCP / DigitalOcean)                                        |
| CI/CD     | GitHub Actions → `release` branch → SSH deploy with Telegram notifications                  |

---

## Project Structure

```
.
├── index.html       # Main landing page (self-contained - HTML + CSS + JS)
├── 404.html         # Custom 404 Not Found error page
├── 502.html         # Custom 502 Bad Gateway error page
└── README.md
```

> All styles and scripts are inlined. There are no build steps, package managers, or external runtime dependencies.

---

## Getting Started

No build toolchain required. Clone and open directly.

```bash
git clone https://github.com/The-Payzue/Payzue-Public-Website.git
cd Payzue-Public-Website
```

**Open in browser (no server needed):**

```bash
# macOS
open index.html

# Linux
xdg-open index.html

# Windows
start index.html
```

**Or serve locally with a dev server for accurate `file://` behaviour:**

```bash
# Python (built-in)
python3 -m http.server 3000

# Node.js
npx http-server . -p 3000
```

Then visit `http://localhost:3000`.

---

## Deployment

The site is served statically behind Nginx. Minimal config:

```nginx
server {
    listen 443 ssl http2;
    server_name thepayzue.com www.thepayzue.com;

    root /var/www/payzue-web;
    index index.html;

    error_page 404 /404.html;
    error_page 502 503 504 /502.html;

    location / {
        try_files $uri $uri/ =404;
    }

    # Cache static assets aggressively
    location ~* \.(html|css|js|svg|woff2)$ {
        expires 7d;
        add_header Cache-Control "public, immutable";
    }
}
```

**CI/CD pipeline:** pushes to the `release` branch trigger a GitHub Actions workflow that SSHs into the production server, copies files, and sends a Telegram notification on success or failure.

---

## Performance Targets

| Metric                   | Target                                    |
| ------------------------ | ----------------------------------------- |
| First Contentful Paint   | < 1.2s                                    |
| Largest Contentful Paint | < 2.5s                                    |
| Total Blocking Time      | < 100ms                                   |
| Cumulative Layout Shift  | < 0.1                                     |
| Page Weight              | < 200 KB (all inline, no external JS/CSS) |

---

## Browser Support

| Browser                | Support                                              |
| ---------------------- | ---------------------------------------------------- |
| Chrome / Edge 90+      | ✅ Full                                              |
| Firefox 88+            | ✅ Full                                              |
| Safari 15+             | ✅ Full (View Transitions fallback for older Safari) |
| Mobile (iOS / Android) | ✅ Full                                              |
| Internet Explorer      | ❌ Not supported                                     |

---

## Branch Strategy

| Branch      | Purpose                                         |
| ----------- | ----------------------------------------------- |
| `main`      | Stable development branch                       |
| `release`   | Production - merging here triggers deployment   |
| `feature/*` | Feature branches (e.g. `feature/faq-accordion`) |
| `fix/*`     | Bug fix branches (e.g. `fix/mobile-nav`)        |

---

## Related Repositories

| Repo                         | Description                                            |
| ---------------------------- | ------------------------------------------------------ |
| `The-Payzue/PaymentGateway` | Core payment processing service (Spring Boot, Java 17) |
| `The-Payzue/CipherBank`     | Bank reconciliation and statement processing engine    |
| `The-Payzue/Relay`          | Android SMS gateway app for transaction notifications  |

---

## Contributing

This is a proprietary internal repository. External contributions are not accepted. For internal team members:

1. Branch off `main` using `feature/<description>` or `fix/<description>`
2. Open a pull request targeting `main`
3. Once reviewed, merge to `release` to trigger production deployment

---

## Contact

**Payzue Technologies Pvt. Ltd.**

📧 [support@payzue.com](mailto:support@payzue.com)  
🌐 [thepayzue.com](https://thepayzue.com)

---

<div align="center">

© 2026 Payzue Technologies Pvt. Ltd. · Built in India · All rights reserved.

</div>
