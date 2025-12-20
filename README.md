# ZeroDrama.ai Website

AI-powered organizational change management consulting website with integrated chat tool.

---

## Files to Upload to GitHub

1. **index.html** — Complete website
2. **background.mp4** — Your video file (rename to this)
3. **CNAME** — Custom domain configuration
4. **README.md** — This file

---

## Setup Instructions

### Step 1: Create GitHub Repository

1. Go to [github.com](https://github.com) (use same account as jeremysatre.com)
2. Click **+** → **New repository**
3. Name it: `zerodrama.ai`
4. Set to **Public**
5. Leave all checkboxes unchecked
6. Click **Create repository**

### Step 2: Upload Files

1. Click **Add file** → **Upload files**
2. Drag and drop:
   - `index.html`
   - `background.mp4` (your video, renamed)
   - `CNAME`
3. Click **Commit changes**

### Step 3: Enable GitHub Pages

1. Go to **Settings** → **Pages**
2. Under **Source**: Select **Deploy from a branch**
3. Under **Branch**: Select **main** and **/ (root)**
4. Click **Save**
5. Wait a moment, then add custom domain: `zerodrama.ai`
6. Click **Save**
7. Once DNS propagates, check **Enforce HTTPS**

### Step 4: Configure GoDaddy DNS

Go to GoDaddy → DNS Management for zerodrama.ai

**Delete existing records**, then add:

**A Records (4 total):**
| Type | Name | Value |
|------|------|-------|
| A | @ | 185.199.108.153 |
| A | @ | 185.199.109.153 |
| A | @ | 185.199.110.153 |
| A | @ | 185.199.111.153 |

**CNAME Record:**
| Type | Name | Value |
|------|------|-------|
| CNAME | www | yourusername.github.io |

(Replace `yourusername` with your GitHub username)

---

## Claude API Setup

The chat tool uses Claude Haiku (cheapest model) for responses.

### Get Your API Key

1. Go to [console.anthropic.com](https://console.anthropic.com)
2. Sign up / Log in
3. Go to **API Keys** → **Create Key**
4. Copy your key (starts with `sk-ant-...`)

### Add Credits

1. In Anthropic Console, go to **Billing**
2. Add $10-20 to start (this will last a while with Haiku)

### Set Spending Limit

1. Go to **Settings** → **Limits**
2. Set monthly limit (e.g., $20)
3. API stops when limit reached (no surprise bills)

### How Users Enter the API Key

Currently, when a user first tries to chat, they'll be prompted to enter an API key. This is a temporary setup for testing.

**For production**, you have two options:

**Option A: Your API key (you pay)**
- Hardcode your key in the JavaScript (line ~470)
- You pay for all usage
- Users get seamless experience

**Option B: Proxy server (recommended for production)**
- Set up a simple backend that holds your API key
- Frontend calls your server, server calls Claude
- Keeps your key secure

---

## Email Capture

Emails are currently stored in the browser's localStorage. 

**To collect emails properly**, integrate with one of these free services:

| Service | Free Tier | Integration |
|---------|-----------|-------------|
| **Formspree** | 50 submissions/month | Add form action |
| **EmailOctopus** | 2,500 subscribers | API integration |
| **Mailchimp** | 500 subscribers | Embed form |

### Quick Formspree Setup

1. Go to [formspree.io](https://formspree.io)
2. Create free account
3. Create new form
4. Get your form endpoint (e.g., `https://formspree.io/f/xxxxx`)
5. Update the email form in `index.html` to submit to Formspree

---

## Cost Summary

| Item | Cost |
|------|------|
| GitHub Pages hosting | **Free** |
| Domain (already owned) | Your existing GoDaddy cost |
| Claude API (Haiku) | **~$10-20/month** depending on usage |
| Email capture (Formspree) | **Free** (50/month) |
| **Total** | **~$10-20/month** |

---

## Haiku vs Sonnet Pricing

| Model | Input (per 1M tokens) | Output (per 1M tokens) |
|-------|----------------------|------------------------|
| **Claude Haiku** | $0.25 | $1.25 |
| Claude Sonnet | $3.00 | $15.00 |

Haiku is **12x cheaper** and still excellent for change management Q&A.

---

## Customization

### Change Colors

Edit the CSS variables at the top of `index.html`:

```css
:root {
    --navy: #1a2b4a;
    --steel-blue: #5889A8;
    --lime: #B8D84F;
    --coral: #FF9A6C;
}
```

### Change Contact Email

Search for `jeremy@zerodrama.ai` and replace with your preferred email.

### Edit Content

All content is in the HTML - just edit the text directly.

---

## Troubleshooting

**Video not playing?**
- Ensure file is named exactly `background.mp4`
- Check file is under 100MB
- Try re-encoding with HandBrake (Web preset)

**Chat not working?**
- Check browser console for errors (F12 → Console)
- Verify API key is correct
- Ensure you have credits in Anthropic account

**Site not loading?**
- DNS can take up to 48 hours
- Verify GitHub Pages is enabled
- Check CNAME file contains `zerodrama.ai`

---

## Support

Questions? Email jeremy@zerodrama.ai
