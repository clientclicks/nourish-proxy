# Nourish — Vercel Proxy Setup

## What this does
This is a tiny serverless function that sits between your Nourish app
and the Anthropic API. It keeps your API key secure on the server side
so the mobile app sandbox can't block it.

---

## Deploy in 5 steps

### 1. Create a free Vercel account
Go to https://vercel.com and sign up (free, no credit card needed).

### 2. Install Vercel CLI (requires Node.js)
```bash
npm install -g vercel
```

### 3. Deploy this folder
From inside the `vercel-proxy` folder, run:
```bash
vercel deploy --prod
```
Follow the prompts. When asked about settings, accept all defaults.

At the end you'll get a URL like:
  https://nourish-proxy-abc123.vercel.app

### 4. Add your Anthropic API key
In the Vercel dashboard (vercel.com/dashboard):
- Open your project → Settings → Environment Variables
- Add: ANTHROPIC_API_KEY = your key from https://console.anthropic.com
- Click Save, then redeploy (Deployments → Redeploy)

### 5. Update the Nourish app
In the nourish-app.jsx artifact, replace this line near the top:

  const PROXY_URL = "YOUR_VERCEL_URL_HERE";

with your actual URL:

  const PROXY_URL = "https://nourish-proxy-abc123.vercel.app";

---

## Test it
Visit: https://your-vercel-url.vercel.app/api/chat
You should see a 405 Method Not Allowed — that means it's working!
(It only accepts POST requests from the app.)

---

## Your API key
Get one free at: https://console.anthropic.com/keys
