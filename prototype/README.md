# נשמה · Interactive Prototype

A self-contained, mobile-first, RTL clickable prototype of the Neshama app in the new
blue-white-gold design language. One file, no build step.

**Flow:** splash → onboarding (gender · goals · age · name · nusach · reading level) →
building → personalized value → paywall → app shell with 5 tabs (Today · Tehillim · Siddur ·
Tanakh · Chat). Prayer cards and readers are tappable, verses open a selection toolbar
(explain / highlight / copy / font-size), the chat responds to a few prompts, and Settings is
reachable from the gear.

## Open it on your phone

### Option A — instant, no setup (recommended for a quick look)
Scan **`qr.png`**. It is pinned to the **exact current commit** so it always shows the
freshest build (a branch URL gets cached by githack and can serve a stale copy). Regenerate
the QR after each change to point at the new commit — e.g.:

```
# QR target = the current commit, immutable & un-cached:
https://raw.githack.com/DudiMaman/jewapp/<commit-sha>/prototype/index.html
```

Works because the repo is public; no configuration needed. (githack is a third-party
convenience CDN — fine for demos. The un-pinned branch URL —
`.../DudiMaman/jewapp/claude/jewish-prayer-app-spec-2qmx9y/prototype/index.html` — is
convenient but may lag a few minutes behind the latest push.)

### Option B — permanent first-party URL via GitHub Pages (~1 min, one-time)
1. GitHub → repo **DudiMaman/jewapp** → **Settings → Pages**.
2. **Source: “Deploy from a branch.”**
3. Branch **`claude/jewish-prayer-app-spec-2qmx9y`** (or `main` after merge), folder
   **`/ (root)`** → **Save**.
4. After ~1 minute: `https://dudimaman.github.io/jewapp/prototype/`.

> If you change the hosting URL, regenerate the QR for the new address.

## Run locally
Open `index.html` in any browser, or:
```
python3 -m http.server -d prototype 8080   # then visit http://localhost:8080/
```
