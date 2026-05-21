# School Retention Risk Analyser
## Deployment Guide

---

## STEP 1 — Install Git (if not already installed)

Open Command Prompt and type:
```
git --version
```
If you see "not recognized", download Git from https://git-scm.com and install it.
Restart Command Prompt after installing.

---

## STEP 2 — Create a GitHub repository

1. Go to https://github.com
2. Click the "+" icon (top right) → New repository
3. Name it: retention-risk-tool
4. Set to Public
5. Do NOT add README or .gitignore
6. Click Create repository
7. Copy the repository URL shown (looks like: https://github.com/YOUR_USERNAME/retention-risk-tool.git)

---

## STEP 3 — Push the code to GitHub

Open Command Prompt in your Downloads folder:
```
cd C:\Users\ANKIT\Downloads\retention-risk-tool
git init
git add .
git commit -m "Initial commit — School Retention Risk Analyser"
git branch -M main
git remote add origin https://github.com/YOUR_USERNAME/retention-risk-tool.git
git push -u origin main
```
Replace YOUR_USERNAME with your actual GitHub username.

---

## STEP 4 — Deploy to Vercel

1. Go to https://vercel.com and log in
2. Click "Add New Project"
3. Click "Import" next to retention-risk-tool
4. Leave all settings as default
5. Click "Deploy"

Wait 60 seconds. Vercel gives you a live URL like:
https://retention-risk-tool.vercel.app

---

## STEP 5 — Add your Anthropic API key to Vercel

This is the critical step — keeps your key secure on the server.

1. In Vercel dashboard, open your project
2. Go to Settings → Environment Variables
3. Click Add New
4. Name: ANTHROPIC_API_KEY
5. Value: your API key (starts with sk-ant-)
6. Click Save
7. Go to Deployments → click the three dots → Redeploy

Your live tool now works with the API key stored securely — never exposed in the code.

---

## STEP 6 — Add to your website (solvestories.in)

In Wix, add an Embed HTML element to any page and paste:
```html
<iframe
  src="https://retention-risk-tool.vercel.app"
  width="100%"
  height="800px"
  frameborder="0"
  style="border-radius:8px">
</iframe>
```

Or simply link to the Vercel URL directly from your website.

---

## Project Structure

```
retention-risk-tool/
├── vercel.json          → Routing config
├── api/
│   └── claude.js        → Serverless function (holds API key)
└── public/
    └── index.html       → The full tool (frontend)
```

---

## How the API key security works

Local (your computer):  Browser → proxy.js (Node) → Anthropic
Deployed (Vercel):      Browser → /api/claude (Vercel function) → Anthropic

In both cases, the API key is never in the HTML file.
The frontend auto-detects which environment it is in and calls the right endpoint.
