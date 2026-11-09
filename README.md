# Incredible Hindistan — interactive scroll presentation

A website-style, animated version of the 44-slide deck **“Incredible Hindistan”**
(Minnath Mohamed Kuttakaren · İstanbul Üniversitesi · Uluslararası İlahiyat).
Every slide is a full-screen section; scrolling (or a presentation clicker) moves
through the five chapters: **Coğrafya · Tarih · Din · Kültür · İslam**.

Built with React 19, Vite, Tailwind CSS 4, Motion (Framer Motion), Lucide icons and hand-made SVG.

---

## Presenting

Open the site full-screen on the projector and use the keyboard or a clicker:

| Key | Action |
| --- | --- |
| `↓` `→` `PageDown` `Space` `J` | next (reveals steps first, e.g. the warm-up quiz cards) |
| `↑` `←` `PageUp` `Shift+Space` `K` | previous |
| `Home` / `End` | first / last slide |
| `F` | toggle fullscreen |
| `H` | hide / show the progress bar, chapter rail and slide counter |

- **Warm-up (slide 2):** each `↓` flips the next “True or false?” card; after the third, the answer banner appears. Cards can also be clicked.
- **Hero pills** (Tarih, Kültür, Din, Coğrafya) and the **chapter rail** on the right jump straight to a chapter.
- **Anthem card:** press play to run the 52-second “everyone stands” timer.
- Maps are interactive — hover a state to see its name.
- Everything is sized from the viewport, so text stays readable from the back of the room
  (tested at 1920×1080, 1366×768 and on phones). Animations respect “reduce motion”.

## Run it locally

```bash
npm install
npm run dev        # http://localhost:5173
npm run build      # production build in dist/
npm run preview    # serve the production build
```

Requires Node 20 or newer.

## Publish on GitHub Pages

**Option A — automatic (recommended)**

1. Create a new GitHub repository and push this folder to its `main` branch.
2. In the repository: **Settings → Pages → Build and deployment → Source: GitHub Actions**.
3. Every push to `main` now builds and deploys via `.github/workflows/deploy.yml`.
   The site appears at `https://<your-user>.github.io/<repo-name>/`.

**Option B — manual**

Run `npm run build` and upload the contents of `dist/` to any static host
(or to a `gh-pages` branch). All asset paths are relative (`base: './'`), so it works
under any sub-folder without changing the config.

## Project structure

```
src/
  App.jsx                 slide order (one component per original slide)
  lib/presenter.jsx       keyboard / clicker navigation, steps, active slide tracking
  lib/chapters.js         chapter names & colours (progress rail)
  components/             Section, Heading, motion helpers (Reveal, SplitText, Counter…),
                          ChapterCover, IndiaMap, TiltCard, backdrops, presenter UI
  sections/<chapter>/     the 44 slide sections
  components/Photo.jsx    photo frame with a slow Ken Burns drift
  photos/                 real photos from Wikimedia Commons (WebP) + credits.json
  data/geo/               pre-computed SVG paths for the maps
  assets/img/             photos taken from the original slides (WebP)
```

To edit text, open the section file for that slide — the content sits at the top of each file.

## Content & credits

- All facts, figures and wording come from the original slides (spelling lightly corrected,
  a few overlapping labels fixed). Statistics marked “Census of India 2011” follow the deck.
- Hero, festival, food and Islam-chapter photos are the ones used in the original deck, cropped
  and compressed.
- All other photos come from Wikimedia Commons under free licences (CC0, public domain,
  CC BY, CC BY-SA). Every photo, its author and licence is listed in [CREDITS.md](CREDITS.md)
  and in the **Photo credits** button on the last slide.
- India state boundaries: `covid19india/covid19india-react` (`public/maps/india.json`, official
  boundaries). World map: Natural Earth via `world-atlas`. Paths were pre-projected with
  `d3-geo` at build time; no map libraries ship to the browser.
- Fonts: Anton, Playball, Nunito and Noto Sans/Naskh families for Devanagari, Arabic,
  Malayalam, Tamil, Bengali and Gurmukhi (self-hosted via Fontsource, so it also works offline
  once loaded).
