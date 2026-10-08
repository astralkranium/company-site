# astralkranium.com

The website for Astral Kranium Ltd, an independent game studio in Glasgow. It is a plain static site (HTML and CSS, no build step, no JavaScript) served by GitHub Pages at https://astralkranium.com.

## Files

```
index.html                  Studio landing: logo, studio line, game tiles (Eternally large, Morrathil small), press, contact
404.html                    Not-found page, studio style (GitHub Pages serves it automatically)
eternally/index.html        Eternally game page and press kit
eternally/privacy.html      Eternally privacy policy
morrathil/index.html        Morrathil: Wrath of the Forest game page and press kit
morrathil/privacy.html      Morrathil privacy policy (linked from Google Play)
assets/css/base.css         Shared base, loaded first by every page
assets/css/studio.css       Studio identity (index.html, 404.html)
assets/css/eternally.css    Eternally identity (eternally/)
assets/css/morrathil.css    Morrathil identity (morrathil/)
assets/brand/               Studio logo (WebP for the page, transparent PNG for press), header mark, favicon, apple-touch-icon, og-studio.jpg
assets/fonts/               Cinzel (SIL OFL, Eternally) and Pixel Operator (CC0, Morrathil), each with its licence file
assets/eternally/           Screenshots (1920x1080 WebP, gallery copies at 960 wide), Shimmer loop, Steam capsule art, og image, favicon, apple-touch-icon
assets/eternally/eternals/  Eternal portraits from the splash art (2:3, 800x1200 WebP plus exact 400x600 copies)
assets/morrathil/           Trailer stills (1920x1080 WebP, gallery copies at 960 wide), sprite, icon, favicon
assets/og-image.jpg         1200x630 Morrathil social share image (Morrathil pages)
CNAME                       Custom domain for GitHub Pages (astralkranium.com)
.nojekyll                   Tells Pages to serve files as-is, without Jekyll
robots.txt, sitemap.xml     Search engine files
```

## Three identities

Eternally and Morrathil have different art styles, so the site has three looks that never mix. Every page loads `base.css` and then exactly one brand stylesheet:

```
<link rel="stylesheet" href="/assets/css/base.css">
<link rel="stylesheet" href="/assets/css/eternally.css">
```

`base.css` holds only what every page shares: the reset, body text size, `.wrap` and `.narrow`, the skip link, the focus ring, `.pixelated`, the footer and reduced motion. It has no colours or fonts of its own. It reads these custom properties, which each brand file sets on `:root`: `--bg`, `--text`, `--muted`, `--line`, `--font-body`, `--focus`, `--focus-ink`.

| Identity | Pages | Stylesheet | Look |
|---|---|---|---|
| Studio | `index.html`, `404.html` | `studio.css` | Near-black navy, the cyan Astral Kranium logo, system sans, cyan accents. Plain and neutral, so both games sit on it. |
| Eternally | `eternally/` | `eternally.css` | Dark fantasy. Deep navy and indigo, antique gold `#F2D38A`, steel blue, ember orange buttons. Cinzel for headings, labels and nav; Georgia (a system serif) for body text. Gold hairline dividers, parchment-dark fact sheet. No Pixel Operator. |
| Morrathil | `morrathil/` | `morrathil.css` | Pixel art. Dark forest green, moss and ember, Pixel Operator headings, system sans body. Unchanged from the original design. |

The class names are shared across brands (`section`, `hero`, `features`, `gallery`, `fact-sheet`, `policy`, `button`, `badge`, `label`), but each brand file styles them its own way. Never load two brand files on one page.

Status lines (release date, platform) are plain text, never outlined boxes, so only real buttons have borders. On Eternally that is `ul.status` with `li.badge` items: gold Cinzel after a short gold rule, joined by a dot on wider screens and stacked on phones. The home tiles use `p.tile-release` the same way.

The studio landing shows each game in its own colours on a tile (`.tile-eternally` uses Cinzel and gold, `.tile-morrathil` uses Pixel Operator and green). Those tile styles live in `studio.css`. A font only downloads when a tile uses it.

### Studio pages

- Header: `a.brand` (the skull mark plus "Astral Kranium" in spaced caps) and nav to Games, Press, Contact.
- CSS star specks sit only behind `.studio-hero` and `.not-found` (a masked `::before`), kept to the top band and the side margins so none land on text. Every other studio section is flat `--bg`.
- Home order: `section.studio-hero` (the logo is the `h1`, with `alt="Astral Kranium"`, then one line about the studio), Games (`.tiles`, Eternally first and larger, Morrathil second), Press (`.press-links` to each game's press section and the logo PNG), Contact.
- The home share tags use `assets/brand/og-studio.jpg`. Favicon and apple-touch-icon come from the skull icon (`assets/brand/`).

### Eternally pages

- Header: `div.brand` with the "Eternally" wordmark (links to `/eternally/`) and a small "by Astral Kranium" link home, then nav to The game, Eternals, Screenshots, Press.
- Favicon is the gold E from the Eternally logo (`assets/eternally/favicon-32.png`). Preload `Cinzel-Variable.woff2` in the head.
- `.wrap.narrow` columns and `.press-notes` are centred in the container on this brand (Morrathil keeps them left).
- Cinzel is a variable font (weights 400 to 900), so any `font-weight` in that range works.

### Morrathil pages

- Keep the look as it is. The header is the pixel "Astral Kranium" wordmark with the studio nav.
- Pixel Operator sizes are multiples of 16px only (1rem, 2rem, 3rem, 4rem, 6rem). Other sizes blur the glyphs. This applies to the Morrathil tile on the home page too.

## Adding a page

1. Pick the identity. A new game gets its own brand file: set the `:root` custom properties that `base.css` needs, then add the game's own styles. Do not stretch another game's file to fit.
2. Copy the head, header and footer from a page of the same identity (`index.html`, `eternally/index.html` or `morrathil/index.html`). Keep `base.css` first.
3. Set the canonical URL, description, og/twitter tags, favicon and theme colour for that page.
4. Footer: keep the shared pattern (see Conventions). Game pages point the privacy link at their own `privacy.html`.
5. Add any public page to `sitemap.xml`, and add a tile on the home page for a new game.

## Who owns what

- **Studio pages** (`index.html`, `404.html`, `studio.css`, `assets/brand/`) and **Morrathil** (`morrathil/`, `morrathil.css`, `assets/morrathil/`) belong to the main site work.
- **Eternally** (`eternally/`, `eternally.css`, `assets/eternally/`) belongs to the Eternally thread. The home Eternally tile repeats its date, tagline and Steam button; keep them in step with `eternally/index.html`.

## Conventions

- Footer, one pattern on every page: game pages start with `A game by Adam Pantak-Ripoll at <a href="/">Astral Kranium</a>.`, then a line with the privacy link and contact@astralkranium.com, then `&copy; 2026 Astral Kranium Ltd. Glasgow, United Kingdom.` and the company disclosure line `Astral Kranium Ltd is registered in Scotland, company number SC868626.` Studio pages skip the credit line and list each game's privacy policy, Eternally first. Adam approved publishing the company number on 8 October 2026. The registered office is his home address, so it is deliberately NOT shown (8 October 2026); add it back only if he moves to a registered office service. Both privacy policies carry the same details in their Contact section.
- Social links are plain text links (no icon fonts, no remote images), in a `p.follow` row with a `span.follow-label`. Eternally: YouTube @EternallyGame, TikTok @eternallygame, Instagram @eternally.game, Discord.
- Gallery images use `srcset` with a 960-wide copy (`name-960.webp`, an exact 2x downscale) and the full 1920 file. The full file stays the press-kit download.
- Paths are root-relative (`/assets/...`), which works because the site lives at the domain root.
- Small pixel art (sprites, icons) gets the `pixelated` class so it scales without blur.
- Images below the fold use `loading="lazy"` and always have `width`, `height` and `alt` (empty `alt` only for decorative images).
- No JavaScript and no external requests: fonts and images are all local. Outbound links are fine. A new font needs an open licence, with its licence file in `assets/fonts/`.

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

- Add the real Google Play link and pre-registration to the Morrathil page and home tile when the listing goes live.
- Replace the trailer stills and screenshots with new captures that show the new animations.
- On launch day, 14 October 2026 (Eternally thread): change "Wishlist on Steam" to "Buy on Steam" in the hero of `eternally/index.html` and on the home Eternally tile; change the "Out 14 October 2026" status line on `eternally/index.html` and the home tile release line ("Out 14 October 2026 on Steam") to "Out now"; update the home meta description and og/twitter descriptions, which say Eternally is out on 14 October 2026.
