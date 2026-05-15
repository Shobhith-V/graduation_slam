# 🎓 Shobhith's Graduation Slam Book

A beautiful online slam book where friends and family can leave messages, memories, and photos — automatically delivered to Shobhith's inbox **two years later**.

> Built with plain HTML/CSS/JS + Google Apps Script. No frameworks, no paid services, completely free.

---

## How it works

1. Friends open the link and fill in their name, email, a message, and optionally attach photos/videos
2. On submit, the entry is sent to a Google Apps Script web app
3. The script saves any files to Google Drive and queues the email
4. A daily trigger checks the queue and delivers each message to Shobhith exactly **2 years** after it was submitted
5. Shobhith receives a beautiful HTML email in 2027 🕊️

---

## Project structure

```
graduation-slam-book/
├── index.html          # The slam book page (deployed via GitHub Pages)
└── README.md           # This file
```

> `slambook_script.js` lives in Google Apps Script only — not in this repo since it contains private config (email, Drive folder ID).

---

## Setup

### 1. Fork or clone this repo
```bash
git clone https://github.com/YOUR_USERNAME/graduation-slam-book.git
```

### 2. Create a Google Drive folder
- Go to [drive.google.com](https://drive.google.com) → New → Folder → name it **"Slam Book Media"**
- Right-click → Share → **Anyone with the link can view**
- Copy the folder ID from the URL (the string after `/folders/`)

### 3. Set up Google Apps Script
- Go to [script.google.com](https://script.google.com) → New project
- Paste the contents of `slambook_script.js` (kept separately, not in this repo)
- Replace `REPLACE_WITH_YOUR_DRIVE_FOLDER_ID` with your folder ID
- Deploy → New deployment → **Web app**
  - Execute as: Me
  - Who has access: Anyone
- Copy the Web App URL

### 4. Update index.html
Replace `REPLACE_WITH_YOUR_APPS_SCRIPT_URL` with your Web App URL from step 3

### 5. Set up the daily email trigger
- In Apps Script → Triggers (clock icon) → Add trigger
- Function: `checkAndSendDue`
- Event: Time-driven → Day timer → 8am–9am
- Save and authorize

### 6. Enable GitHub Pages
- Repo → Settings → Pages
- Source: Deploy from branch → `main` → `/ (root)`
- Your site goes live at `https://YOUR_USERNAME.github.io/graduation-slam-book`

### 7. Test it
- In Apps Script → run `testSubmission()`
- Wait 2 minutes → run `checkAndSendDue()`
- Check your inbox ✦

---

## Customization

| What | Where |
|------|-------|
| Your name on the page | `index.html` — search for "Shobhith" |
| Unlock date (default: 2 years) | `index.html` — change `setFullYear(+2)` |
| Your email address | `slambook_script.js` — `MY_EMAIL` constant |
| Writing prompts | `index.html` — the `.chip` buttons |
| Colors & fonts | `index.html` — CSS variables in `:root` |

---

## Stack

- **Frontend** — HTML, CSS, vanilla JS (no dependencies)
- **Backend** — Google Apps Script (free, runs on Google's servers)
- **Storage** — Google Script Properties (email queue) + Google Drive (media files)
- **Hosting** — GitHub Pages (free, permanent)
- **Email** — GmailApp (Google Apps Script built-in)

---

## Privacy

- Submissions are stored in Google Script Properties — not in any database you can casually browse
- Media files go into a private Google Drive folder only you have access to
- Emails are queued and sent automatically — there is no UI to read them early

---

*Made with love for graduation 2025 · Messages unlock in 2027 ✦*