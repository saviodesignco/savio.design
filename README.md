# savio.design — Digital Event Invitations

Private, password-protected event invitations hosted on GitHub Pages at `savio.design/events/[event-name]`.

---

## Project Structure

```
savio.design/
├── index.html                  ← Placeholder homepage
├── README.md                   ← This file
├── events/
│   └── template/
│       ├── index.html          ← Master invitation template
│       └── admin.html          ← Config form + live preview tool
└── assets/
    └── fonts/                  ← Reserved for fallback fonts
```

---

## Step 1 — Initialise the Git Repository

```bash
cd /path/to/savio.design
git init
git add .
git commit -m "Initial commit — savio.design invitation system"
```

---

## Step 2 — Create the GitHub Repository and Push

1. Go to [github.com/new](https://github.com/new)
2. Name the repository exactly: `savio.design`
3. Set it to **Public** (required for free GitHub Pages)
4. Do **not** add a README, .gitignore, or license — the repo should start empty
5. Push your local repository:

```bash
git remote add origin https://github.com/YOUR_USERNAME/savio.design.git
git branch -M main
git push -u origin main
```

---

## Step 3 — Enable GitHub Pages

1. In your GitHub repository, go to **Settings → Pages**
2. Under **Source**, select **Deploy from a branch**
3. Choose branch: `main`, folder: `/ (root)`
4. Click **Save**
5. After 1–2 minutes your site will be live at `https://YOUR_USERNAME.github.io/savio.design/`

---

## Step 4 — Connect savio.design via Squarespace DNS

GitHub Pages requires 4 A records pointing to GitHub's servers and 1 CNAME for the `www` subdomain.

### In Squarespace Domains

1. Log in to [account.squarespace.com](https://account.squarespace.com) → **Domains** → **savio.design** → **DNS Settings**
2. Delete any existing A records for `@` (the root domain)
3. Add the following **4 A records**:

| Type | Host | Value           | TTL  |
|------|------|-----------------|------|
| A    | @    | 185.199.108.153 | 3600 |
| A    | @    | 185.199.109.153 | 3600 |
| A    | @    | 185.199.110.153 | 3600 |
| A    | @    | 185.199.111.153 | 3600 |

4. Add the following **CNAME record**:

| Type  | Host | Value                          | TTL  |
|-------|------|--------------------------------|------|
| CNAME | www  | YOUR_USERNAME.github.io        | 3600 |

### Back in GitHub Pages Settings

1. In **Settings → Pages → Custom domain**, type `savio.design` and click **Save**
2. GitHub will create a `CNAME` file in your repo automatically
3. Check **Enforce HTTPS** once the certificate is issued (can take up to 24 hours)

DNS propagation typically takes 1–48 hours. Once active, `savio.design` will serve your GitHub Pages site.

---

## Weekly Workflow — Creating a New Event

### 1. Duplicate the template folder

```bash
cp -r events/template events/my-event-name
```

Replace `my-event-name` with a short, URL-friendly slug (e.g. `spring-dinner`, `april-rooftop`).

### 2. Configure the event using the admin tool

Open `events/template/admin.html` in a browser (just open the file locally — no server needed):

```bash
open events/template/admin.html
# or on Windows: start events/template/admin.html
```

- Fill in all the fields
- Watch the live preview update as you type
- Click **Copy Config Object** when ready
- Paste the copied code into `events/my-event-name/index.html`, replacing the existing `const EVENT = { ... }` block at the top of the `<script>` tag

### 3. Add a hero image (optional)

- Place your image in `events/my-event-name/` (e.g. `hero.jpg`)
- Set `heroImagePath` in the config to `"hero.jpg"` (relative path)

### 4. Test locally

Open `events/my-event-name/index.html` in a browser to verify everything looks correct.

### 5. Commit and push

```bash
git add events/my-event-name/
git commit -m "Add event: my-event-name"
git push
```

GitHub Pages automatically redeploys within ~60 seconds.

### 6. Share the link

Your invitation is live at:
```
https://savio.design/events/my-event-name/
```

---

## Config Reference

All event data lives in the `const EVENT = { ... }` object at the top of `index.html`:

| Variable        | Description                                      |
|-----------------|--------------------------------------------------|
| `eventType`     | Badge label (e.g. "Dinner Party", "Launch")      |
| `eventTitle`    | Main headline                                    |
| `eventSubtitle` | Italic sub-headline                              |
| `hostName`      | Your name, shown throughout the invitation       |
| `date`          | Full date string (e.g. "Saturday, April 12 2025")|
| `dayOfWeek`     | Day name, used in .ics calendar file             |
| `time`          | Start time (e.g. "7:00 PM")                     |
| `doorsOpen`     | Arrival / doors time (e.g. "6:45 PM")           |
| `duration`      | Duration string (e.g. "3 hours") — used for calendar end time |
| `spotsLeft`     | Available spots (set to 0 for "Waitlist Only")   |
| `spotsTotal`    | Total capacity                                   |
| `venueName`     | Venue display name                               |
| `venueAddress`  | Street address                                   |
| `venueCity`     | City and zip code                                |
| `notes`         | Host note to guests (leave `""` to hide section) |
| `heroImagePath` | Path to hero image (leave `""` for gold gradient)|
| `rsvpEmail`     | Email address that RSVP buttons mailto to        |
| `eventPassword` | Password gate (leave `""` to disable)            |

---

## Notes

- **No build tools required** — all files are plain HTML/CSS/JS
- **Admin tool** (`admin.html`) is only ever opened locally — it is never shared with guests
- **Password gate** uses `sessionStorage` — guests only enter the password once per browser session; refreshing the page does not prompt again
- **Google Fonts** are loaded from a CDN; if unavailable, the page falls back to Georgia / system-ui
