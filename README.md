# KhataAI — Waitlist Page

A single-page waitlist landing site for **KhataAI**, the WhatsApp-based AI bookkeeper for Pakistani social media sellers. Built by Squad Chenab for Comebck Pakistan, Cohort 1.

Collects email + WhatsApp number from interested sellers and writes each signup straight into a Google Sheet — no backend, no database, no server required.

## What's inside

```
khataai-waitlist.html   # the entire site — HTML, CSS, and JS in one file
```

## How it works

- Static HTML/CSS/JS. No build step, no dependencies to install.
- The waitlist form submits directly to a **Google Form**, which is linked to a **Google Sheet**. Every submission shows up as a new row automatically.
- Fonts are loaded from Google Fonts via CDN (Fraunces, Inter, IBM Plex Mono).

## One-time setup: connect the Google Sheet

The form is already wired up to a Google Form in this repo, but if you need to point it at a **new** Form/Sheet, do this:

1. Create a Google Form with two short-answer questions: **Email** and **WhatsApp number**.
2. In the Form, go to **Responses → click the green Sheets icon** to link a new Google Sheet — every submission will land there automatically.
3. In the Form's `⋮` menu, click **"Get pre-filled link."**
4. Fill the Email field with `EMAILTEST` and the WhatsApp field with `WHATSAPPTEST`, then click **Get link**.
5. The generated link looks like this:
   ```
   https://docs.google.com/forms/d/e/FORM_ID/viewform?usp=pp_url&entry.847343028=EMAILTEST&entry.577851895=WHATSAPPTEST
   ```
6. Copy the three values into `khataai-waitlist.html`:
   ```js
   const GOOGLE_FORM_ID = "FORM_ID";              // between /d/e/ and /viewform
   const EMAIL_ENTRY_ID = "847343028";             // entry.XXXXXXXXX next to EMAILTEST
   const WHATSAPP_ENTRY_ID = "577851895";          // entry.XXXXXXXXX next to WHATSAPPTEST
   ```
7. Save the file. New submissions will now appear as rows in the linked Google Sheet.

## Running locally

Just open `khataai-waitlist.html` in a browser — no server needed.

For a local dev server (optional, avoids some browser file:// quirks):
```bash
python3 -m http.server 8000
```
Then visit `http://localhost:8000/khataai-waitlist.html`.

## Deploying

Since this is a static file, it can be deployed anywhere that serves static sites:

- **Netlify / Vercel** — drag-and-drop the HTML file, or connect this repo for auto-deploys.
- **GitHub Pages** — enable Pages on this repo, set the root, and rename the file to `index.html`.
- **Railway** — deploy as a static site, or serve it via a minimal FastAPI/Flask static route if you want it alongside the KhataAI backend.

## Notes

- No PII is stored anywhere except the linked Google Sheet — treat that Sheet as sensitive data (contains real emails and phone numbers).
- The animated ledger preview on the page is illustrative sample data, not connected to any live KhataAI account or real user data.
