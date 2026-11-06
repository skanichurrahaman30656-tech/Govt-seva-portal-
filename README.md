# Govt Seva Portal

> **Independent information website. Not affiliated with any government department.**
> It only links to official Indian government websites. It never collects Aadhaar or PAN numbers, OTPs, passwords or identity documents.

A static, mobile-friendly portal where people can find official links for documents, certificates, schemes and state services.

## Features
- Instant search, plus filters by category, state and department, with A–Z / Z–A sorting
- Service cards with Apply, Correction, Download, Status and Official Website buttons (a button shows only when an official link exists, otherwise "Official Link Not Available Yet")
- Government schemes and West Bengal services, plus a selector for all 28 states and 8 Union Territories
- 14 languages: English, Hindi, Bengali, Assamese, Gujarati, Kannada, Malayalam, Marathi, Nepali, Odia, Punjabi, Tamil, Telugu, Urdu (Urdu is right-to-left)
- Light and dark mode
- Pages: About, Privacy Policy, Terms & Conditions, Disclaimer, Cookie Policy, Contact
- Cookie consent banner; Google AdSense loads only after the visitor accepts and only if you add your IDs

## Project structure
```
govt-seva-portal/
├─ public/              # the website (this folder is deployed)
│  ├─ index.html        # whole site: HTML, CSS, JavaScript and service data
│  ├─ robots.txt
│  ├─ sitemap.xml
│  └─ ads.txt           # AdSense template
├─ scripts/check.js     # pre-deploy checks
├─ vercel.json          # Vercel settings and security headers
├─ package.json
├─ .gitignore
└─ README.md
```
There is **no build step**. It is plain HTML, CSS and JavaScript, so it cannot have build errors.

## Run and check locally
```bash
npm run check   # checks JS syntax, anchors, https links, secrets
npm run dev     # opens the site locally using "serve"
```

## Deploy
1. **GitHub:** create a new repository, then
   ```bash
   git init && git add . && git commit -m "Initial commit"
   git branch -M main
   git remote add origin https://github.com/YOUR-USER/YOUR-REPO.git
   git push -u origin main
   ```
2. **Vercel:** open vercel.com, choose *Add New → Project*, import the repository and click *Deploy*. Leave the build settings alone; `vercel.json` already sets the output folder to `public`.
3. **Custom domain (optional):** add it under Project → Settings → Domains.

## Before you go live (required)
- [ ] Replace `[add your contact email here before launch]` in the Contact and Privacy pages (search `index.html` for "add your contact email").
- [ ] Replace `YOUR-DOMAIN` in `public/robots.txt` and `public/sitemap.xml` with your real domain.
- [ ] **Open every service link and confirm it works.** Links were added from known official domains but were not verified live. After checking, set `verified` dates in the data if you want to show them.
- [ ] Have the policy pages reviewed for your situation and have a native speaker check each translation.

## Add or edit a service
Open `public/index.html` and find `const D=[`. Each row is:
```
["id","Name","Category","State","Department","Description",{apply:"",correct:"",download:"",status:""},"official-site-url"]
```
Use only official links (`.gov.in`, `.nic.in` and similar). Leave a link out and its button will not appear. Never use fake or placeholder URLs. Run `npm run check` after editing.

## Google AdSense
1. Deploy on your own domain and get the site approved by AdSense.
2. In `index.html`, set `const ADS={client:"ca-pub-XXXXXXXXXXXXXXXX",slot:"YOUR-SLOT-ID"}` using your own IDs.
3. Put the line AdSense gives you in `public/ads.txt`.

## Security and secrets
- No API keys, passwords or secrets are in this repository, and none are needed. `.gitignore` blocks `.env` files and key files.
- Your AdSense publisher ID is public by design (it appears in the page source). Keep your AdSense login and any Vercel or GitHub tokens out of the repository.

## Not included
- No admin dashboard or login. A secure admin needs a backend with server-side authentication and a database; the service list is edited in `index.html` for now.
- Not a React/TypeScript/Tailwind project.
