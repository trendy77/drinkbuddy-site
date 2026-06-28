# Drink Buddy Landing Page — Setup Guide

## Files
- `index.html` — the landing page
- `assetlinks.json` — Android App Links verification file (for Google App Indexing)
- `og-image.png` — **you need to add this** (1200×630px social share image)

---

## Step 1: Domain ✅

Using **drinkbuddy.trendypublishing.com** as a subdomain of trendypublishing.com (purchased on Namecheap).

In Namecheap DNS, add a CNAME record: `drinkbuddy` → `yourusername.github.io`
Then in your GitHub repo: Settings → Pages → Custom domain → `drinkbuddy.trendypublishing.com`

---

## Step 2: Host on GitHub Pages

1. Create a new GitHub repo, e.g. `drinkbuddy-site`
2. Push `index.html` and `assetlinks.json` to the `main` branch
3. Go to **Settings → Pages → Source: main branch / root**
4. GitHub gives you `https://yourusername.github.io/drinkbuddy-site/`
5. Add your custom domain in Settings → Pages → Custom domain

---

## Step 3: Set up the assetlinks.json (for App Indexing)

This file tells Google that your website and Android app are linked.

It must be served at exactly: `https://drinkbuddy.trendypublishing.com/.well-known/assetlinks.json`

### Get your SHA-256 fingerprint

Run this in terminal (requires Java/keytool):

```bash
keytool -list -v -keystore your-release-key.jks -alias your-key-alias
```

Or via Android Studio: **Build → Generate Signed Bundle / APK** and note the SHA-256 shown.

Replace `REPLACE_WITH_YOUR_SHA256_FINGERPRINT` in `assetlinks.json` with the actual value.

### Deploy the file

On GitHub Pages, create a folder `.well-known/` in your repo root and add `assetlinks.json` inside it:

```
repo/
  index.html
  .well-known/
    assetlinks.json
```

### Verify it works

Use Google's Digital Asset Links testing tool:
https://developers.google.com/digital-asset-links/tools/generator

---

## Step 4: Add og-image.png

Create a 1200×630px image (e.g. in Canva) showing the app name and a screenshot.
Save as `og-image.png` in the repo root.

---

## Step 5: Submit to Google Search Console

1. Go to https://search.google.com/search-console
2. Add property → URL prefix → `https://drinkbuddy.trendypublishing.com/`
3. Verify ownership (GitHub Pages supports HTML file verification)
4. Submit your sitemap: `https://drinkbuddy.trendypublishing.com/sitemap.xml` (optional but recommended)
5. Use the **URL Inspection** tool to request indexing of your homepage

---

## Keywords this page targets

- drink tracker app android
- BAC calculator app
- alcohol tracker android
- blood alcohol calculator app
- unit tracker app
- drink counter app
- alcohol monitor app

---

## What the App Indexing does

The combination of:
1. `<meta name="google-play-app" content="app-id=com.drinkbuddy.tracker" />` in the HTML
2. `<link rel="alternate" href="android-app://..." />` in the HTML
3. `/.well-known/assetlinks.json` served on your domain

...tells Google that this website and your Android app are the same product. Google can then:
- Show "Open in app" banners in Chrome on Android
- Surface your app in Google Search results alongside the web page
- Index in-app content if you implement App Actions later
