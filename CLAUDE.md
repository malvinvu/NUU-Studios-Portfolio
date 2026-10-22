# NUU Studios site

Video portfolio for NUU Studios (Malvin's creative studio, North Carolina). Modeled on ghettotexasamerica.com: the hero is a slowly spinning, draggable cloud of image tiles in the shape of North Carolina, one tile per piece of work, repeated to fill the state.

## Files

- `index.html`: the whole site in one file (HTML, CSS and JS inline). No build step.

## Where it lives right now

Published as a Claude artifact (private until shared): https://claude.ai/artifact/E6EwzXFtnC1HAWhV6ysHKy

The live page saves itself: the "+ add video" form uploads files to the artifact's asset store and republishes the page with the new video list. That only works on claude.ai. Opening `index.html` locally shows the design, but the upload form and uploaded images won't work there.

The live page is the source of truth for the video list. Before republishing to the artifact, read the live version first and keep its `<script id="data">` contents, or videos added from the page will be lost.

Plan: move to self-hosting (Netlify, own domain such as nuustudios.com), with full videos on YouTube/Vimeo embedded in the page, YouTube thumbnails as tile images, and the video list in a plain data file or a published Google Sheet instead of the upload form.

## How the page is built

- Data: `<script id="data" type="application/json">` holds `{name, handle, tagline, videos:[...]}`.
  Each video: `id, title, who, cat (lowercase category), year, kind ("file" | "link")`, plus
  `asset` (uploaded clip id), `poster` (auto frame grab id), `full` (link to the full video, for uploaded previews),
  `link` and `cover` (for link entries), `w`/`h` (aspect).
- Hero: `initThree()` draws the tile cloud on a 2D canvas (no libraries). Tiles drift gently, the cloud "breathes", tiles part slightly around the cursor, and hovering a tile lifts it with a white glow. Tiles show still images only, each with its own random crop for a collage look.
- Categories: buttons in the top bar (`#topcats`) and above the grid (`#chips`). Picking one pops that category's tiles forward and dims the rest, and filters the grid.
- Lightbox: tapping a tile opens the video (uploaded clip plays; links open YouTube/Vimeo/Instagram in a new tab).

## Design

- Background: solid royal blue `#1a24d2`, sampled from a reference hoodie, with fine grain and a faint uneven-dye texture.
- Text white on blue. Fonts: Archivo (display) and IBM Plex Mono (labels), from Google Fonts.
- Name "nuu studios" sits large and faint behind the cloud.

## Preferences from Malvin

- The NC shape must be made of separate, spaced tiles of his work, not a solid object.
- Gentle drifting; no fading in/out; subtle-but-visible parting around the cursor.
- Tiles should show images (collage feel), not playing video.
