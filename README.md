# astralkranium.com

The website for Astral Kranium Ltd, an independent game studio in Glasgow. It is a plain static site (HTML and one CSS file, no build step, no JavaScript) served by GitHub Pages at https://astralkranium.com.

## Files

```
index.html               Studio home: intro, game cards, press, contact
morrathil/index.html     Morrathil: Wrath of the Forest game page and press kit
morrathil/privacy.html   Morrathil privacy policy (linked from Google Play)
404.html                 Not-found page (GitHub Pages serves it automatically)
assets/css/site.css      The only stylesheet, shared by every page
assets/fonts/            Pixel Operator (CC0, the game's UI font) with its licence
assets/morrathil/        Trailer stills (1920x1080 WebP, gallery copies at 960 wide), sprite and icon
assets/og-image.jpg      1200x630 social share image
favicon.png              32x32 favicon
CNAME                    Custom domain for GitHub Pages (astralkranium.com)
.nojekyll                Tells Pages to serve files as-is, without Jekyll
robots.txt, sitemap.xml  Search engine files
```

## Who owns what

- **Studio pages and Morrathil** (`index.html`, `morrathil/`, `404.html`, `assets/`) belong to the main site work.
- **Eternally** belongs to the Eternally thread. On the home page it is the `<article id="eternally">` card inside the Games list. That card is self-contained, so it can be replaced as one block. Eternally's own page and privacy policy go in a new `eternally/` folder (`eternally/index.html`, `eternally/privacy.html`), with screenshots in `assets/eternally/`.
- New pages should copy the head and header from `morrathil/index.html`. In the footer, replace the credit line and point the privacy link at your game's own `privacy.html`. Use the existing classes in `site.css` (`section`, `wrap`, `game-card`, `features`, `gallery`, `fact-sheet`, `policy`). Add new styles to `site.css` rather than a second stylesheet. Add any new public page to `sitemap.xml`.

## Conventions

- Footer: every page ends with the contact email and `&copy; 2026 Astral Kranium Ltd. Glasgow, United Kingdom.` Game pages add their own credit line and their own privacy link above that. The home footer lists each game's privacy policy; add an "Eternally privacy policy" link next to the Morrathil one once `eternally/privacy.html` exists.
- Card art (`.card-art`) can be a pixel sprite with the `pixelated` class, shown at 96x144, or a full-width image such as a Steam capsule.
- Gallery images use `srcset` with a 960-wide copy (`name-960.webp`, an exact 2x downscale) and the full 1920 file. The full file stays the press-kit download.
- Pixel Operator sizes are multiples of 16px only (1rem, 2rem, 3rem, 4rem, 6rem). Other sizes blur the glyphs.
- Paths are root-relative (`/assets/...`), which works because the site lives at the domain root.
- Pixel Operator is for headings and labels; body text uses the system sans stack.
- Small pixel art (sprites, icons) gets the `pixelated` class so it scales without blur.
- Images below the fold use `loading="lazy"` and always have `width` and `height`.
- No external requests: fonts and images are all local.

## Preview locally

Root-relative paths need a local web server; opening the files directly won't load the CSS. From the repo root:

```
python -m http.server 8000
```

Then open http://localhost:8000.

## GitHub Pages and DNS

1. Repo **Settings > Pages**: Source "Deploy from a branch", branch `main`, folder `/ (root)`.
2. Custom domain: `astralkranium.com` (the `CNAME` file sets this too).
3. DNS at the domain registrar:
   - Apex `astralkranium.com`, four `A` records:
     `185.199.108.153`, `185.199.109.153`, `185.199.110.153`, `185.199.111.153`
   - `www` as a `CNAME` to `astralkranium.github.io`
   - Leave the MX and other email records exactly as they are, so contact@astralkranium.com keeps working.
4. Once the certificate is issued, tick **Enforce HTTPS** in the Pages settings.

## Open items

- Add the real Google Play link and pre-registration to the Morrathil page and home card when the listing goes live.
- Replace the trailer stills and screenshots with new captures that show the new animations.
- Eternally content: the home card, `eternally/` page and its privacy policy (Eternally thread).
- When `eternally/index.html` exists (Eternally thread): change the home Press line back to "Each game page has its own fact sheet and screenshots you are free to use in coverage." and add an "Eternally press kit" link next to the Morrathil one.
- Adam to supply the company number, registered office address and place of registration (for example, Registered in Scotland) for the footer and the privacy policy Contact section. UK trading-disclosure rules require them. Never fill them in without Adam.
