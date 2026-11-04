# NUU Studios site

Video portfolio for NUU Studios (Malvin's creative studio, North Carolina). Modeled on ghettotexasamerica.com: the hero is a slowly spinning, draggable cloud of image tiles in the shape of North Carolina, one tile per piece of work, repeated to fill the state.

## Files

- `index.html`: the page (HTML, CSS and JS inline). No build step.
- `videos.json`: the site details and video list the page loads.
- `images/`: tile images, `<video id>-sm.jpg` (640px, for the cloud and folders) and `<video id>-md.jpg` (1400px, for the grid and lightbox).
- `_headers`: Cloudflare Pages caching rules.
- `_blob/` (git-ignored): raw assets downloaded from the claude.ai artifact.

## Where it lives

- Public site: Cloudflare Pages, deployed from the GitHub repo `malvinvu/NUU-Studios-Portfolio` on every push to `main`, on Malvin's domain (already on Cloudflare).
- Editing copy: the claude.ai artifact https://claude.ai/artifact/E6EwzXFtnC1HAWhV6ysHKy still has the "+ add video" form, which uploads to the artifact's asset store and saves the page. That form only works on claude.ai; on the public site it stays hidden.
- To bring work added on claude.ai to the public site: read the artifact's `<script id="data">`, download each new video's `sm`/`md` assets, save them as `images/<id>-sm.jpg` / `-md.jpg`, add the entry to `videos.json` with those paths (and `cover` set to the `md` path), then commit and push.
- The artifact still runs the older single-file setup (inline data, `/_blob/` ids). Don't publish this `index.html` to it as-is: it loads `videos.json`, which the artifact doesn't serve.

## How the page is built

- Data: `videos.json` holds `{name, handle, tagline, email, videos:[...]}`.
  Each video: `id, title, who, cat (lowercase category), year, kind ("file" | "link"), desc`, plus
  `sm`/`md` (image paths), `cover` (same as `md` for link entries), `link`, `w`/`h` (aspect).
  Categories are fixed in `CATS` in `index.html`.
- Hero: `initThree()` draws the tile cloud on a 2D canvas (no libraries). Tiles drift gently, the cloud "breathes", tiles part slightly around the cursor, and hovering a tile lifts it with a white glow. Tiles show still images only, each with its own random crop for a collage look.
- Categories: buttons in the top bar (`#topcats`) and macOS-style folders above the grid (`#folders`). Picking one pops that category's tiles forward and dims the rest, and filters the grid.
- Lightbox: tapping a tile opens the video (uploaded clip plays; links open YouTube/Vimeo/Instagram in a new tab).

## Design

- Background: solid royal blue `#1a24d2`, sampled from a reference hoodie, with fine grain and a faint uneven-dye texture.
- Text white on blue. Fonts: Archivo (display) and IBM Plex Mono (labels), from Google Fonts.
- Name "nuu studios" sits large and faint behind the cloud.

## Preferences from Malvin

- The NC shape must be made of separate, spaced tiles of his work, not a solid object.
- Gentle drifting; no fading in/out; subtle-but-visible parting around the cursor.
- Tiles should show images (collage feel), not playing video.
