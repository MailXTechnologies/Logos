# Logos

Shared artwork for **ISTE KJSSE** email signatures. Used by every council
member's signature, so please don't rename or delete files here — doing so
breaks the signature in every email already sent.

## Files

| File | Size | Purpose |
|---|---|---|
| `iste-emblem.png` | 230×230 | ISTE crest |
| `instagram-dm.png` · `mail-dm.png` · `linkedin-dm.png` · `website-dm.png` | 88×88 | `#3C67C9` set — dual-mode, works on light *and* dark |
| `instagram-2563eb.png` · `linkedin-2563eb.png` · `website-2563eb.png` | 88×88 | `#2563EB` set — matches the `#2563EB` signature palette, light mode |
| `instagram-dark.png` · `linkedin-dark.png` · `website-dark.png` | 88×88 | `#93B4FA` set — **dark mode only**, too pale for white (2.07:1) |

### Which set do I use?

- **One set for both modes** → the `-dm` (`#3C67C9`) files. Simplest; works
  everywhere including Gmail, which deletes style blocks.
- **Different colour per mode** → pair a light set (`-dm` or `-2563eb`) with
  the matching `-dark` file and swap them with a media query. See
  "Swapping icons per colour mode" below.

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

## Swapping icons per colour mode

CSS cannot recolour a PNG, so showing a different colour in dark mode needs
two `<img>` tags with only one visible at a time:

```html
<img class="ico-lt" src=".../instagram-2563eb.png" alt="Instagram"
     width="18" height="18" border="0" style="display:block;">
<!--[if !mso]><!--><img class="ico-dk" src=".../instagram-dark.png"
     alt="Instagram" width="18" height="18" border="0"
     style="display:none;"><!--<![endif]-->
```

```css
@media (prefers-color-scheme: dark) {
  .ico-lt { display: none !important; }
  .ico-dk { display: block !important; }
}
```

Three details make this safe:

1. **The dark image is hidden inline** (`style="display:none;"`). Gmail's
   signature editor deletes style blocks, so the media query disappears and
   the inline rule survives — you get the light icon only, never both.
2. **The `<!--[if !mso]>` wrapper** hides the dark image from Outlook's Word
   engine, which ignores `display:none` and would otherwise show all six.
3. **Both images keep real `alt` text.** Only one is ever visible, so there
   is no duplication when a client blocks images.
