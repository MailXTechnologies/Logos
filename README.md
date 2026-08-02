# Logos

Shared artwork for **ISTE KJSSE** email signatures. Used by every council
member's signature, so please don't rename or delete files here — doing so
breaks the signature in every email already sent.

## Files

| File | Size | Purpose |
|---|---|---|
| `iste-emblem.png` | 230×230 | ISTE crest shown at 115×115 in the signature |
| `instagram-dm.png` | 88×88 | Instagram icon |
| `mail-dm.png` | 88×88 | Email icon |
| `linkedin-dm.png` | 88×88 | LinkedIn icon |
| `website-dm.png` | 88×88 | Website icon (optional, off by default) |

## Use them via jsDelivr, not raw GitHub

```
https://cdn.jsdelivr.net/gh/MailXTechnologies/Logos@main/<file>.png
```

`raw.githubusercontent.com` sends `Content-Type: text/plain` and is rate
limited, so many email clients refuse to render it. jsDelivr serves proper
image headers and is built for hotlinking.

## Do not re-host these on a free image host

The signature previously pointed at imgbb. imgbb blocks hotlinking from
email and returns **an advertisement image in its place** — every recipient
saw "upgrade to a Pro account" instead of the icons. The failure is silent:
it returns HTTP 403 but still sends a valid PNG body, so the client renders
it happily. If you need a new icon, add it to this repo.

## Icon specification

The `-dm` suffix means **dual-mode**: these work on light *and* dark email
backgrounds.

- **Colour:** `#3C67C9` — ISTE navy hue (222°), lightened only as far as
  needed to stay legible on dark. Contrast: 5.28:1 on white, 3.29:1 on
  `#1A1A1A`, 3.05:1 on Gmail's `#202124`, 3.98:1 on black.
- **Background:** fully transparent, real alpha. No white plate, no baked-in
  checkerboard.
- **Canvas:** square, so all icons align at 22×22 in the signature.

A darker navy would match the crest more closely but drops below 3:1 on
Gmail's dark background and becomes unreadable. `#072464` measures 1.20:1 on
dark — effectively invisible. Images are never recoloured by a mail client's
dark mode, so the file itself has to work on both.

If you add an icon, match that spec or it will look wrong next to the others.
