# Talim Tech and Design – Complete Build & Business Guide
## AI Marketing SaaS for Kenyan Small Businesses

---

## 1. APP IDEA

**Name:** Talim Tech and Design  
**Tagline:** "AI Marketing Tools for Kenyan Businesses"  
**Domain:** talimtech.co.ke

---

## 2. PROBLEM SOLVED

Small businesses in Kenya (mitumba sellers, electronics shops, barbershops, cyber cafés, online sellers) struggle to create professional marketing content. Hiring a social media manager costs KES 15,000–30,000/month. Talim Tech and Design gives them AI-powered marketing tools for KES 400/month.

---

## 3. FEATURES LIST

| Feature | Free | Pro |
|---|---|---|
| AI Ad & Caption Writer | 5/day | Unlimited |
| Poster Generator | 1 template | 10 templates |
| Kenyan Hashtag Generator | 10 tags | 50+ tags |
| WhatsApp Bulk Formatter | ✅ | ✅ (100 msgs) |
| Analytics Dashboard | Basic | Full |
| Priority WhatsApp Support | ❌ | ✅ |

---

## 4. TECH STACK

```
Frontend:  Pure HTML + CSS + Vanilla JS (no framework needed)
AI:        Anthropic Claude API (claude-sonnet-4-20250514)
Database:  localStorage (MVP) → Firebase (scale)
Auth:      Custom email/password → Firebase Auth (scale)
Payments:  M-Pesa Daraja API (Safaricom)
Hosting:   Netlify (free tier) or Vercel
```

---

## 5. FOLDER STRUCTURE

```
nairobiads/
├── index.html          ← Main app (single-file MVP)
├── README.md           ← This file
├── GUIDE.md            ← Business plan
├── assets/
│   ├── logo.png
│   └── og-image.png    ← For social sharing
├── api/                ← If using serverless functions
│   ├── generate.js     ← Proxy Claude API calls (hides key)
│   └── mpesa.js        ← M-Pesa Daraja integration
└── netlify.toml        ← Netlify config
```

---

## 6. DEPLOYMENT STEPS

### Option A: Netlify (Recommended – Free)

```bash
# 1. Create account at netlify.com
# 2. Drag & drop the Talim Tech and Design/ folder onto Netlify dashboard
# 3. Set environment variables:
#    ANTHROPIC_API_KEY = your_key_here
# 4. Get free SSL and custom domain setup
# 5. Connect talimtech.co.ke domain (KES ~700/year at Afriregister)
```

### Option B: Vercel

```bash
npm install -g vercel
cd nairobiads/
vercel deploy
# Follow prompts – free tier is enough for MVP
```

### Option C: GitHub Pages (Zero cost)

```bash
git init
git add .
git commit -m "Talim Tech and Design MVP launch"
git remote add origin https://github.com/yourusername/nairobiads
git push -u origin main
# Enable GitHub Pages in Settings → Pages → main branch
```

### Important: Hiding your API Key (Production)

Create a simple serverless function on Netlify:

```javascript
// netlify/functions/generate.js
const Anthropic = require('@anthropic-ai/sdk');

exports.handler = async (event) => {
  const { prompt, model } = JSON.parse(event.body);
  const client = new Anthropic({ apiKey: process.env.ANTHROPIC_API_KEY });
  
  const msg = await client.messages.create({
    model: 'claude-sonnet-4-20250514',
    max_tokens: 1000,
    messages: [{ role: 'user', content: prompt }]
  });
  
  return {
    statusCode: 200,
    body: JSON.stringify({ content: msg.content })
  };
};
```

Then call `/netlify/functions/generate` from your frontend instead of the Anthropic API directly.

---

## 7. M-PESA DARAJA INTEGRATION

```javascript
// api/mpesa.js – Safaricom Daraja API
// 1. Register at developer.safaricom.co.ke
// 2. Create app, get Consumer Key & Secret
// 3. Use STK Push for seamless payment

const mpesaSTKPush = async (phone, amount, accountRef) => {
  // Get OAuth token
  const tokenRes = await fetch(
    'https://sandbox.safaricom.co.ke/oauth/v1/generate?grant_type=client_credentials',
    {
      headers: {
        Authorization: 'Basic ' + btoa(`${CONSUMER_KEY}:${CONSUMER_SECRET}`)
      }
    }
  );
  const { access_token } = await tokenRes.json();

  // Initiate STK Push
  const timestamp = new Date().toISOString().replace(/[-:T.Z]/g,'').slice(0,14);
  const password  = btoa(`${BUSINESS_SHORT_CODE}${PASSKEY}${timestamp}`);

  const stkRes = await fetch(
    'https://sandbox.safaricom.co.ke/mpesa/stkpush/v1/processrequest',
    {
      method: 'POST',
      headers: {
        Authorization: `Bearer ${access_token}`,
        'Content-Type': 'application/json'
      },
      body: JSON.stringify({
        BusinessShortCode: BUSINESS_SHORT_CODE,
        Password: password,
        Timestamp: timestamp,
        TransactionType: 'CustomerPayBillOnline',
        Amount: amount,
        PartyA: phone,       // Customer phone e.g. 254712345678
        PartyB: BUSINESS_SHORT_CODE,
        PhoneNumber: phone,
        CallBackURL: 'https://talimtech.co.ke/api/mpesa-callback',
        AccountReference: accountRef,
        TransactionDesc: 'Talim Tech and Design Pro Subscription'
      })
    }
  );
  return stkRes.json();
};
```

---

## 8. MONETIZATION PLAN

### Pricing Model
| Tier | Price | Target |
|---|---|---|
| Free | KES 0 | Lead magnet – convert to paid |
| Pro | KES 400/month | Main revenue |
| Pro Annual | KES 3,600/year (25% off) | Retention |

### Revenue Projections

| Customers | Daily Revenue |
|---|---|
| 5 Pro users | KES 2,000 → ~$15/day |
| 15 Pro users | KES 6,000 → ~$45/day |
| 50 Pro users | KES 20,000 → ~$150/day |

### Path to $15/Day (5 Pro customers)

**Week 1–2:**
- Post daily in 5 Facebook groups (Nairobi Buy & Sell, Kenya Online Business, etc.)
- Share in 3 WhatsApp groups of entrepreneurs
- Create 1 TikTok showing the tool saving time

**Week 3–4:**
- Offer 7-day free trial of Pro to first 20 signups
- Ask satisfied users for testimonials
- Convert 5 trial users to paid = **$15/day achieved**

---

## 9. GROWTH STRATEGY FOR KENYA

### Facebook Groups (Post daily)
- Nairobi Business Network
- Kenya Online Business Community  
- Mitumba Traders Kenya
- Nairobi Buy & Sell
- Kenya Entrepreneurs Hub

### WhatsApp Marketing Script
```
Mambo! 👋 Nimepata tool ya AI inayoandika ads na captions kwa biashara yako 
kwa sekunde 30 tu. Inafanya kazi vizuri kwa mitumba, electronics, salon na zaidi.
Free trial ipo. Angalia hapa: https://talimtech.co.ke
```

### TikTok Content Ideas
1. "Watch me generate a Facebook ad in 10 seconds for my mitumba shop 🤯"
2. "Stop paying KES 15,000 for a social media manager – use this instead"
3. "I grew my Instagram from 200 to 2000 followers using AI captions"

### Referral Program
- Give users a referral link
- Each referral who upgrades = 1 free month for referrer
- Works automatically with localStorage + simple backend

---

## 10. DEBUGGING CHECKLIST

### Common Issues & Fixes

| Bug | Cause | Fix |
|---|---|---|
| "API key invalid" | Key not set | Set ANTHROPIC_API_KEY env var |
| "Failed to fetch" | CORS issue | Use serverless function proxy |
| Content not saving | localStorage blocked | Check browser privacy settings |
| M-Pesa STK not sending | Wrong phone format | Use 254XXXXXXXXX format |
| App blank on mobile | CSS overflow issue | Check `overflow-x: hidden` on body |
| Poster not downloading | html2canvas not loaded | Add html2canvas CDN script |

### Debug Mode (add to URL)
```javascript
// Add ?debug=1 to URL to see all state
if (window.location.search.includes('debug=1')) {
  console.log('STATE:', JSON.stringify(STATE, null, 2));
}
```

### Error Boundaries
All API calls are wrapped in try/catch with fallback demo content, so users always see something even if the API fails.

---

## 11. SCALABILITY IMPROVEMENTS

### Phase 1 (MVP – 0 to 50 users): Current file
- Single HTML file
- localStorage
- Direct API calls

### Phase 2 (50–500 users)
- Firebase Auth + Firestore
- Netlify serverless functions (hide API key)
- Stripe + M-Pesa Daraja for payments
- Email with Resend.com (free 3000 emails/month)

### Phase 3 (500+ users)
- Next.js frontend
- Supabase backend
- Redis for rate limiting
- CDN for poster assets

---

## 12. SECURITY BASICS

```
✅ Never expose ANTHROPIC_API_KEY in frontend code
✅ Use serverless functions as API proxy
✅ Rate limit: 5 generations/day on free tier (in STATE)
✅ Validate all inputs before sending to API
✅ HTTPS enforced (Netlify provides free SSL)
✅ M-Pesa callbacks verified with Safaricom signature
⚠️ In production: add proper JWT auth (Firebase Auth recommended)
⚠️ In production: store user data in Firestore, not just localStorage
```

---

## 13. REALISTIC 30-DAY ACTION PLAN

```
Day 1-3:   Deploy to Netlify, get domain talimtech.co.ke
Day 4-7:   Post in 10 Facebook groups daily, 50 signups target
Day 8-14:  First 5 paid users, collect testimonials
Day 15-21: TikTok launch, WhatsApp group sharing
Day 22-30: Referral program live, target 15 paid users = $45/day
```

---

*Built for Kenya 🇰🇪 – Made with ❤️ using Claude AI*
