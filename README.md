# Talim Tech and Design
### Creativity meets Performance

> AI-powered marketing tools built for Kenyan small businesses.

## 🚀 Live Demo
[Visit the App](https://talim-tech-design.netlify.app) *(deploy to update this link)*

## ✨ Features
- **AI Ad & Caption Writer** – Facebook ads, Instagram captions, TikTok hooks in English, Swahili & Sheng
- **Poster Generator** – Instant promo posters with 5 color themes
- **Kenyan Hashtag Generator** – Trending tags for Instagram, TikTok & Twitter/X
- **WhatsApp Bulk Formatter** – Personalized messages for your customers
- **Analytics Dashboard** – Track your content creation activity

## 💰 Pricing
| Plan | Price | Limit |
|------|-------|-------|
| Free | KES 0 | 5 AI generations/day |
| Pro  | KES 400/month | Unlimited everything |

## 🛠️ Tech Stack
- **Frontend:** HTML, CSS, Vanilla JavaScript (single-file, zero dependencies)
- **AI:** Anthropic Claude API (`claude-sonnet-4-20250514`)
- **Storage:** localStorage (MVP) → Firebase (scale)
- **Payments:** M-Pesa Daraja API simulation
- **Deploy:** Netlify / Vercel / GitHub Pages

## 📁 Project Structure
```
talim-tech-design/
├── index.html    ← Full app (landing page + dashboard)
├── GUIDE.md      ← Business plan & monetization strategy
└── README.md     ← This file
```

## ⚡ Quick Deploy

### Netlify (Recommended)
1. Fork this repository
2. Go to [netlify.com](https://netlify.com) → **Add new site** → **Import from Git**
3. Select this repo
4. Set environment variable: `ANTHROPIC_API_KEY = your_key`
5. Deploy!

### GitHub Pages
1. Go to **Settings → Pages**
2. Source: **Deploy from a branch → main → / (root)**
3. Save – live in ~60 seconds

### Vercel
```bash
npm install -g vercel
vercel deploy
```

## 🔑 Environment Variables
| Variable | Description |
|----------|-------------|
| `ANTHROPIC_API_KEY` | Your Claude API key from [console.anthropic.com](https://console.anthropic.com) |

## 📲 M-Pesa Integration
See `GUIDE.md` for full Daraja API setup instructions.

## 🎯 Target Market
Mitumba sellers, electronics shops, barbershops, cyber cafés, online sellers — all across Kenya 🇰🇪

## 📄 License
MIT License – free to use and modify.

---
*Built with ❤️ using Claude AI · Talim Tech and Design © 2026*
