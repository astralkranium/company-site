# astralkranium.com

The website for Astral Kranium Ltd, an independent game studio in Glasgow. It is a plain static site (HTML and one CSS file, no build step, no JavaScript) served by GitHub Pages at https://astralkranium.com.

## Files

```
index.html               Home: Eternally hero, studio line, games (Eternally featured, Morrathil secondary), press, contact
morrathil/index.html     Morrathil: Wrath of the Forest game page and press kit
morrathil/privacy.html   Morrathil privacy policy (linked from Google Play)
eternally/index.html     Eternally game page and press kit
eternally/privacy.html   Eternally privacy policy
404.html                 Not-found page (GitHub Pages serves it automatically)
assets/css/site.css      The only stylesheet, shared by every page
assets/fonts/            Pixel Operator (CC0, the game's UI font) with its licence
assets/morrathil/        Trailer stills (1920x1080 WebP, gallery copies at 960 wide), sprite and icon
assets/eternally/        Screenshots (1920x1080 WebP, gallery copies at 960 wide), Shimmer loop, Steam capsule art, og image
assets/og-image.jpg      1200x630 Morrathil social share image (Morrathil pages)
favicon.png              32x32 favicon
CNAME                    Custom domain for GitHub Pages (astralkranium.com)
.nojekyll                Tells Pages to serve files as-is, without Jekyll
robots.txt, sitemap.xml  Search engine files
```

## Home page structure

Eternally is the studio's main game and leads the home page. Morrathil is a side project: present, but secondary.

1. **Hero** (`section.hero.hero-home`): a darkened Eternally screenshot as background (`vexaroth-army.webp`, decorative, `alt=""`), the Eternally key art (`eternally-capsule.jpg`) beside the text on wide screens and above it on phones, then title, subtitle, tagline, a one-sentence pitch, the release line (`p.release`) and two buttons: "Wishlist on Steam" and "See the game".
2. **Studio line** (`section.studio-line`): one sentence about the studio.
3. **Games**: the featured Eternally card (`article.game-card.game-card-featured#eternally`, gameplay art, Steam badge, buttons and the Follow Eternally row) and below it the compact Morrathil card (`article.game-card.game-card-side#morrathil`, labelled "Also in the works").
4. **Press** and **Contact**.

The home `<title>`, meta description and og/twitter tags preview Eternally and use `assets/eternally/og-eternally.jpg`. The Morrathil pages keep `assets/og-image.jpg`. The 404 page points to Eternally.

## Who owns what

- **Studio pages** (`index.html`, `404.html`, shared `assets/`) and **Morrathil** (`morrathil/`, `assets/morrathil/`) belong to the main site work.
- **Eternally** (`eternally/`, `assets/eternally/`) belongs to the Eternally thread. On the home page the Eternally content is the hero and the featured card; keep them in step with `eternally/index.html` (date, buttons, pitch).
- New pages should copy the head and header from `morrathil/index.html`. In the footer, replace the credit line and point the privacy link at your game's own `privacy.html`. Use the existing classes in `site.css` (`section`, `wrap`, `hero`, `game-card`, `features`, `gallery`, `fact-sheet`, `policy`, `follow`). Add new styles to `site.css` rather than a second stylesheet. Add any new public page to `sitemap.xml`.

## Conventions

- Footer: every page ends with the contact email, `&copy; 2026 Astral Kranium Ltd. Glasgow, United Kingdom.` and the company disclosure line `Astral Kranium Ltd is registered in Scotland, company number SC868626. Registered office: 3/1 25 Camphill Avenue, Glasgow, G41 3AU.` Game pages add their own credit line and their own privacy link above that. The home footer lists each game's privacy policy, Eternally first. Adam approved publishing the company number and registered office on 8 October 2026 (they are public on Companies House). Both privacy policies carry the same details in their Contact section.
- Social links are plain text links (no icon fonts, no remote images), in a `p.follow` row with a `span.follow-label`. Eternally: YouTube @EternallyGame, TikTok @eternallygame, Instagram @eternally.game, Discord.
- Card art (`.card-art`) can be a pixel sprite with the `pixelated` class, shown at 96x144 (64x96 in the compact side card), or a full-width image with `card-art-wide`.
- Gallery images use `srcset` with a 960-wide copy (`name-960.webp`, an exact 2x downscale) and the full 1920 file. The full file stays the press-kit download.
- Pixel Operator sizes are multiples of 16px only (1rem, 2rem, 3rem, 4rem, 6rem). Other sizes blur the glyphs.
- Paths are root-relative (`/assets/...`), which works because the site lives at the domain root.
- Pixel Operator is for headings and labels; body text uses the system sans stack.
- Small pixel art (sprites, icons) gets the `pixelated` class so it scales without blur.
- Images below the fold use `loading="lazy"` and always have `width`, `height` and `alt` (empty `alt` only for decorative backgrounds).
- No JavaScript and no external requests: fonts and images are all local. Outbound links are fine.

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
- On launch day, 14 October 2026 (Eternally thread): change "Wishlist on Steam" to "Buy on Steam" in the hero of `eternally/index.html` and the home hero; change the "Out 14 October 2026" badge on `eternally/index.html`, the home release line ("Out 14 October 2026 on Steam") and the featured card badge to "Out now"; update the home `<title>` and og/twitter titles, which say "out 14 October 2026 on Steam".
