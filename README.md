# Mindsurf

Stratospheric internet for Germany via HAPS (High Altitude Platform Systems) — solar-powered gliders at 20 km altitude delivering 5G connectivity.

## Repository Contents

| File | Description |
|------|-------------|
| `index.html` | Landing page — waitlist, plans, coverage check |
| `mindsurf.py` | 5G digital twin simulation (signal power validation) |
| `config.js` | Firebase configuration |
| `firebase.json` | Firebase Hosting configuration |
| `requirements.txt` | Python dependencies for the simulation |

---

## Hosting the Landing Page

### Option A — GitHub Pages (simplest)

1. Push this repo to GitHub.
2. Go to **Settings → Pages**.
3. Set source to **Deploy from a branch**, branch `main`, root `/`.
4. GitHub will publish the site at `https://<your-username>.github.io/<repo-name>/`.

To use a custom domain, add a `CNAME` file at the repo root containing your domain (e.g. `mindsurf.io`) and configure your DNS accordingly.

---

### Option B — Firebase Hosting

Requires the [Firebase CLI](https://firebase.google.com/docs/cli).

```bash
npm install -g firebase-tools
firebase login
firebase deploy --only hosting
```

The site will be live at `https://mindsurf.web.app` (or your custom domain configured in the Firebase console).

**Custom domain**: Firebase Console → Hosting → Add custom domain.

---

### Option C — Any Static Host (Netlify, Vercel, Cloudflare Pages)

The landing page is a single `index.html` with no build step. Drop the repo into any static hosting service:

- **Netlify**: Connect the GitHub repo, set publish directory to `.` (root), deploy.
- **Vercel**: `vercel --prod` from the repo root.
- **Cloudflare Pages**: Connect repo, framework preset = None, build output = `/`.

---

## Running the 5G Simulation

`mindsurf.py` simulates a complete 5G signal chain through an urban CDL-C fading channel using [Sionna](https://nvlabs.github.io/sionna/) (NVIDIA's link-level simulator).

**System**: 3.5 GHz · 256-QAM · 2×2 MIMO · 50 MHz BW → ~150 Mbit/s

**Install dependencies** (GPU recommended, Google Colab works well):

```bash
pip install -r requirements.txt
```

**Run**:

```bash
python mindsurf.py
```

**Output**: Three constellation diagrams showing transmitted → faded → equalized signal recovery, plus BER validation confirming LDPC achieves zero errors.

---

## Project Status

Waitlist open — infrastructure launch pending HAPS operator deployment readiness (Airbus Zephyr / HAPSMobile / Aalto HAPS).
