# נשמה · Interactive Prototype

A self-contained, mobile-first, RTL clickable prototype of the Neshama app in the new
blue-white-gold design language. One file, no build step.

**Flow:** splash → onboarding (gender · goals · age · name · nusach · reading level) →
building → personalized value → paywall → app shell with 5 tabs (Today · Tehillim · Siddur ·
Tanakh · Chat). Prayer cards and readers are tappable, verses open a selection toolbar
(explain / highlight / copy / font-size), the chat responds to a few prompts, and Settings is
reachable from the gear.

## Open it on your phone (QR)

Scan **`qr.png`** once GitHub Pages is live. Target URL:

```
https://dudimaman.github.io/jewapp/prototype/
```

### Enable GitHub Pages (one-time, ~1 min)
1. GitHub → repo **DudiMaman/jewapp** → **Settings → Pages**.
2. **Build and deployment → Source: “Deploy from a branch.”**
3. Choose branch **`claude/jewish-prayer-app-spec-2qmx9y`** (or `main` after you merge) and
   folder **`/ (root)`**, then **Save**.
4. Wait ~1 minute, then open `https://dudimaman.github.io/jewapp/prototype/` or scan the QR.

> The repo must be **public** for the Pages URL to be reachable without login (private-repo
> Pages requires a paid GitHub plan). If you regenerate the URL, recreate the QR for the new
> address.

## Run locally
Just open `index.html` in any browser, or serve the folder:
```
python3 -m http.server -d prototype 8080   # then visit http://localhost:8080/
```
