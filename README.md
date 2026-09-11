# Tadhkiratu Al-Akhirah Academy Website

A fully self-contained website — `index.html` includes all HTML, CSS, JavaScript,
videos, images, and PDFs embedded directly in the file (as base64 data). No
separate asset files to manage or lose.

## What's inside

```
index.html          → the entire site — structure, styling, behaviour, AND all
                       media (videos, book covers, PDFs, icons) embedded inline
manifest.json        → PWA config (lets phones "Add to Home Screen")
assets/social-preview.jpg → the ONE file that must stay external (see note below)
```

## Why one file is still separate

Open Graph / Twitter Card preview images (the thumbnail that shows up when you
share the link on WhatsApp, Facebook, etc.) **must** be a real fetchable URL —
social media crawlers cannot read embedded base64 images. This is a platform
limitation, not a choice — so `social-preview.jpg` has to stay as its own file
for link previews to work once this is hosted online.

## Running it locally

No install or build step needed.

- Double-click `index.html` to open it directly in a browser, or
- Serve it locally:
  ```bash
  python3 -m http.server 8000
  ```
  then visit `http://localhost:8000`

## Deploying with GitHub Pages

1. Push this repository to GitHub.
2. Go to **Settings → Pages**.
3. Under "Build and deployment", set **Source** to `Deploy from a branch`.
4. Choose the `main` branch and `/ (root)` folder, then save.
5. GitHub will give you a live URL within a minute or two.

## A few things worth knowing

- **File size**: `index.html` is around 26MB because the videos are embedded
  directly. This is fine for GitHub (well under its 100MB hard limit) and for
  hosting, but it does mean:
  - The page downloads everything up front on first visit — no lazy-loading
    or browser caching of videos separately from the page itself.
  - Some code editors are slow to open very large single files. If you need
    to edit the code often, consider asking for the "separate assets folder"
    version instead, which is much lighter to work with (~700KB HTML +
    ~19MB assets folder, loaded on demand).
- **Forms** (Registration, Attendance, Complaints) submit via
  [FormSubmit](https://formsubmit.co) to `tadhkiratualakhirahacademy@gmail.com`.
  The **first** submission to a new address triggers a one-time confirmation
  email — someone needs to click it, or submissions won't arrive after that.
- **Attendance** routes a WhatsApp confirmation to a different number
  depending on which Halqoh/Class is selected (see the `data-wa` attributes
  on the `<select id="attendanceHalqoh">` options in `index.html`).
- **Registration** opens a pre-filled WhatsApp message to the Director's
  number after a successful submission.
- **Complaints** goes to Gmail only — no WhatsApp step.
- The **Student Portal** login checks names against a hardcoded roster inside
  `index.html`. Anyone who views the page source can see that roster — there's
  no real authentication.
- Editing content means editing the relevant section of `index.html` directly
  — search for the section's HTML comment
  (e.g. `<!-- ================= FACULTY MEMBERS ================= -->`).

## Tech

Plain HTML/CSS/JS. Bilingual (English/Arabic with RTL support). No
dependencies, no npm, no build process.
