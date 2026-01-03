# ZeroDrama.ai - Complete Setup Guide

## 📦 What's Included

| File | Purpose |
|------|---------|
| `tool.html` | AI Diagnostic Tool - The core product with 3 entry modes and 10+ intake questions |
| `early-access.html` | Early Access signup page with Google Sheets integration |
| `index.html` | Homepage (already updated with Early Access buttons) |
| `cloudflare-worker.js` | Updated Cloudflare Worker code |

---

## 🚀 Step 1: Upload Files to GitHub

### Option A: Via GitHub Web Interface (Easiest)

1. Go to: `github.com/YOUR-USERNAME/zerodrama.ai`
2. For each file:
   - Click **"Add file"** → **"Create new file"**
   - Name it (e.g., `tool.html`)
   - Paste the content
   - Click **"Commit new file"**

### Option B: Replace Existing Files

For `index.html` (if you want the updated version with Early Access buttons):
1. Click on `index.html` in your repo
2. Click the **pencil icon** (Edit)
3. Select all → Delete → Paste new content
4. Click **"Commit changes"**

---

## 🔧 Step 2: Set Up Google Sheets Email Capture

### A. Create Your Spreadsheet

1. Go to [sheets.google.com](https://sheets.google.com)
2. Create new spreadsheet: **"ZeroDrama Signups"**
3. Add these headers in Row 1:

| A | B | C | D | E | F |
|---|---|---|---|---|---|
| Timestamp | First Name | Email | Role | Challenge | Source |

### B. Add the Apps Script

1. In your spreadsheet, click **Extensions → Apps Script**
2. Delete any existing code
3. Paste this code:

```javascript
function doPost(e) {
  var sheet = SpreadsheetApp.getActiveSheet();
  var data = JSON.parse(e.postData.contents);
  
  sheet.appendRow([
    data.timestamp,
    data.firstName,
    data.email,
    data.role,
    data.challenge || '',
    data.source
  ]);
  
  return ContentService.createTextOutput(JSON.stringify({success: true}))
    .setMimeType(ContentService.MimeType.JSON);
}
```

4. Click **Save** (Ctrl+S)
5. Name the project: "ZeroDrama Form Handler"

### C. Deploy the Script

1. Click **Deploy → New deployment**
2. Click the gear icon → Select **"Web app"**
3. Configure:
   - Description: "Email signup handler"
   - Execute as: **Me**
   - Who has access: **Anyone**
4. Click **Deploy**
5. Click **Authorize access** → Choose your Google account → Allow
6. **COPY THE URL** (looks like: `https://script.google.com/macros/s/ABC123.../exec`)

### D. Update Your Early Access Page

1. Go to your GitHub repo
2. Open `early-access.html`
3. Find this line (around line 270):
```javascript
const GOOGLE_SCRIPT_URL = 'YOUR_GOOGLE_SCRIPT_URL';
```
4. Replace `YOUR_GOOGLE_SCRIPT_URL` with your copied URL
5. Commit changes

**That's it!** Signups will now save to your Google Sheet automatically.

---

## ⚡ Step 3: Verify Cloudflare Worker

Your Cloudflare Worker at `zerodrama-api.jeremysatre.workers.dev` should already be working. If you need to update it:

1. Go to [dash.cloudflare.com](https://dash.cloudflare.com)
2. Left sidebar → **Workers & Pages**
3. Click on **zerodrama-api**
4. Click **"Edit Code"** or **"Quick Edit"**
5. Verify the code matches `cloudflare-worker.js`
6. Make sure your Claude API key is set correctly
7. Click **Deploy**

---

## ✅ Step 4: Test Everything

### Test 1: Homepage
- Visit `zerodrama.ai`
- Verify Early Access buttons appear in nav and hero
- Test the chat tool works

### Test 2: Early Access Page
- Visit `zerodrama.ai/early-access.html`
- Fill out the form
- Check your Google Sheet for the new entry

### Test 3: Diagnostic Tool
- Visit `zerodrama.ai/tool.html`
- Select an entry mode
- Complete the intake questions
- Verify you get an action plan

---

## 🔗 Final URL Structure

| URL | Description |
|-----|-------------|
| `zerodrama.ai` | Homepage with chat tool |
| `zerodrama.ai/early-access.html` | Waitlist signup |
| `zerodrama.ai/tool.html` | Full diagnostic tool (the product) |

---

## 💡 What's Different About the Diagnostic Tool

The `tool.html` page is the **actual product** - here's what makes it special:

### Three Entry Modes (Not a Blank Chat Box)
Users choose their situation:
1. 🎯 **A Critical Conversation is Coming** - Prep for difficult talks
2. 🔍 **This Initiative is Stalling** - Diagnose and unblock projects
3. ⚖️ **I'm Caught in the Middle** - Navigate between leadership and team

### 10 Diagnostic Questions per Mode
Based on your OCM expertise:
- Power dynamics and authority
- Type of resistance (not all resistance is the same)
- User's internal state (separating their friction from others')
- Timing and stakes
- Desired outcomes

### Structured Output (Every Time)
The AI produces these sections:
1. 🔍 **What's Really Happening** - Diagnosis
2. 🎯 **How to Frame This** - Strategic approach
3. 💬 **Language to Use** - Actual scripts and phrases
4. ➡️ **Your Next 3 Steps** - Concrete actions
5. ⚠️ **Watch Out For** - Red flags and common mistakes

### Chat Refinement
After the initial output, users can ask follow-up questions to go deeper.

---

## 📊 Tracking Success

### Google Analytics Events
The pages automatically track:
- `early_access_signup` - When someone joins waitlist
- Page views on all pages

### Google Sheets
Captures for each signup:
- Timestamp
- Name and email
- Role
- Current challenge
- Source page

### Validation Metrics to Watch
- **Week 1-2:** 50+ email signups
- **Week 3-4:** 100+ total signups
- **Survey responses:** 30%+ would pay $10-50/month

---

## 🆘 Troubleshooting

### "Early Access form isn't saving emails"
1. Check browser console (F12) for errors
2. Verify Google Script URL is correct
3. Make sure script is deployed as "Anyone can access"
4. Test the script URL directly in a new tab

### "Diagnostic tool shows error"
1. Check browser console for specific error
2. Verify Cloudflare Worker is running
3. Check Claude API key is valid and has credits
4. Test the Worker URL directly

### "Page shows 404"
1. Verify file was committed to GitHub
2. Check filename is exact (case-sensitive)
3. Wait 2-3 minutes for GitHub Pages to rebuild

---

## 🎯 Next Steps After Setup

1. **Post on LinkedIn** to drive traffic to `/early-access.html`
2. **Monitor Google Sheet** for signups
3. **Send survey** to signups after 50+ join
4. **Conduct interviews** with interested leads
5. **Iterate** based on feedback

---

Good luck with the launch! 🚀
