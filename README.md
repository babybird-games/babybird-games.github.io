# babybird studio website

Static site for the babybird studio, served by GitHub Pages from the `main` branch at
<https://babybird-games.github.io/>. No build step: plain HTML plus one shared stylesheet.

## Layout

```
index.html            Studio home: one card per app
assets/site.css       Shared styles and per-app colour themes (light + dark)
fonts/                Shared web fonts (Lilita One, Fredoka; OFL licences included)
logo.png              Studio logo
app-ads.txt           AdMob publisher record. Must stay at the site root.
privacy.html          DEPRECATED copy of the Bloat Float policy (see below)

bloat-float/          One folder per app
  index.html          App page
  privacy.html        Privacy policy (the URL given to Play Console)
  icon.png            App icon, 512 px or larger
  banner.jpg          Optional wide banner (1024 × 500, the Play feature graphic)
  screens/*.jpg       Optional screenshots, 9:16
hanafuda/
  index.html
  privacy.html
  icon.png
```

## Adding a new app

Use a short, lowercase, hyphenated folder name (`my-game/`). Its URLs become
`/my-game/` and `/my-game/privacy.html`.

1. **Create the folder** and copy `hanafuda/index.html` and `hanafuda/privacy.html` into it
   (or the `bloat-float/` versions if the app has a banner and screenshots).
2. **Add the assets:** `icon.png` (512 × 512) and, optionally, `banner.jpg` and `screens/`.
3. **Add a theme** in `assets/site.css`: copy the `.theme-hanafuda` block and its dark-mode
   `@media` block, rename it `.theme-my-game` and change the colours. Set
   `<body class="theme-my-game">` on both new pages.
4. **Edit the app page:** `<title>`, description and `og:` tags, the hero text, the features,
   and the store button. Until the store listing is public, keep the button as a
   non-link `<span class="play">` with "Coming soon to".
5. **Edit the privacy page** for what the app really does (ads, purchases, network, saves).
   Update the "Last updated" date whenever the text changes.
6. **List it on the home page:** copy one `<article class="card app-card …">` in `index.html`,
   set its theme class, icon, name, status label and the two links.
7. **Check locally** (`python -m http.server` in this folder, then open
   <http://localhost:8000/>), at phone width and in dark mode, then commit and push to `main`.
8. **Give Play Console** `https://babybird-games.github.io/my-game/privacy.html` as the
   privacy policy URL.

All links inside an app folder are relative (`../assets/site.css`, `../logo.png`, `../`), so a
copied page works as soon as its folder exists.

## URLs that must not break

| URL | Why |
|---|---|
| `/app-ads.txt` | AdMob reads it from the root of the developer website. |
| `/privacy.html` | Bloat Float's Play Console entry still points here. It stays online with the full policy and a note pointing to `/bloat-float/privacy.html`. Update the Play Console URL first; only then may this page be retired. Until then, change it together with `bloat-float/privacy.html`. |
| `/banner.jpg`, `/bloat-float-icon.png`, `/screens/*.jpg` | Legacy copies of the Bloat Float images from before the per-app folders, kept so old links keep working. New pages use the files in `bloat-float/`. |
| `/hanafuda/privacy.html` | Hanafuda's privacy policy URL in Play Console. |

`.gdignore` stops the Godot editor from importing this folder when it sits inside a Godot
project; it does nothing on the website.
