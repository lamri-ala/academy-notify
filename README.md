# Academy Notify — Windows Desktop App

A fully local Windows desktop application for private academies to manage students, courses, schedules, revision sessions, and send notifications via Telegram and WhatsApp.

---

## Requirements

- **Node.js** v18 or higher — https://nodejs.org
- **Windows 10 / 11** (64-bit)
- Internet connection only needed for sending messages

---

## Quick Start (Run in Development)

```bash
# 1. Open a terminal in this folder

# 2. Install dependencies
npm install

# 3. Run the app
npm start
```

The app will open as a desktop window. Demo data is pre-loaded automatically.

---

## Build a Windows Installer (.exe)

```bash
# Build a full installer + portable .exe
npm run build
```

Output will be in the `dist/` folder:
- `Academy Notify Setup.exe` — installer for Windows
- `Academy Notify Portable.exe` — no install required, just run it

---

## Project Structure

```
academy-notify/
├── main.js          ← Electron main process (SQLite, API calls, IPC)
├── preload.js       ← Secure bridge between main and renderer
├── package.json     ← Dependencies and build config
├── src/
│   ├── index.html   ← App shell (sidebar, topbar, content area)
│   ├── css/
│   │   └── app.css  ← All styles
│   └── js/
│       ├── db.js    ← In-memory data cache + helpers
│       ├── ui.js    ← Toast, modal, nav, shared utilities
│       ├── app.js   ← App bootstrap and page router
│       └── pages/
│           ├── dashboard.js  ← Dashboard page
│           ├── students.js   ← Student management
│           ├── teachers.js   ← Teachers, Courses, Schedule, Revision (combined)
│           ├── send.js       ← Send message page
│           └── logs.js       ← Message logs + Settings
└── assets/
    └── icon.ico     ← App icon (replace with your own)
```

---

## Where Data is Stored

All data lives **locally** on the admin's PC:

```
C:\Users\<Admin>\AppData\Roaming\academy-notify\
  ├── academy.db      ← SQLite database (all students, courses, logs...)
  └── config.json     ← Bot tokens and academy settings
```

No cloud. No server. No subscription.

---

## Setting Up Telegram Bot

1. Open Telegram, search for **@BotFather**
2. Send `/newbot` and follow instructions
3. Copy the **token** (looks like `7812345678:AAHdqTcvCHi...`)
4. Open **Settings** in the app and paste it under "Telegram Bot Token"
5. Click **Test Connection** to verify

> **Note:** Students must press `/start` on your bot before you can message them.
> Share the bot link: `https://t.me/YourBotName`

---

## Setting Up WhatsApp Business API

1. Go to **https://developers.facebook.com**
2. Create a Meta Business App
3. Add the **WhatsApp** product
4. Get your **Phone Number ID** and **Temporary/Permanent Token**
5. Open **Settings** in the app and fill in both fields
6. Click **Test Connection**

> Free tier: 1,000 conversations/month. Paid tiers available for more.

---

## Self-Registration (Telegram)

Students can register themselves via Telegram:

1. Share your bot link with students: `https://t.me/YourBotName`
2. Student opens Telegram and presses **START**
3. In the app, go to **Settings → Check New Registrations**
4. New students appear and can be added with one click

---

## Features

| Feature | Description |
|---|---|
| Students | Add/edit/delete with parent contact and course enrollment |
| Teachers | Manage teachers and their subjects |
| Courses | Group and private (1-on-1) courses |
| Schedule | Visual weekly timetable |
| Revision Sessions | One pre-exam session per course with auto-notifications |
| Send Message | Broadcast to all / by course / one student |
| Templates | Built-in message templates with `{{name}}`, `{{course}}` variables |
| Message Logs | Full delivery history |
| Dual Channel | Telegram + WhatsApp simultaneously |
| Local Storage | SQLite — no internet required except for sending |

---

## Troubleshooting

**App won't start:**
- Make sure Node.js is installed: run `node --version` in terminal
- Run `npm install` again

**"better-sqlite3" build error:**
- Run: `npm install --build-from-source`
- Or: `npm rebuild better-sqlite3`

**Messages not sending:**
- Check your tokens in Settings
- Use the "Test Connection" buttons
- Ensure you have internet access

---

## License
MIT — Free to use and modify.
