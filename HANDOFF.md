# EasyPak QR code — handoff (2026-10-21)

## What this is
A permanent QR code printed on EasyPak packages and business cards.
It encodes **https://qr.easypaksa.com/** and opens a small branded page with four buttons:

| Button | Link |
|---|---|
| Website | https://easypaksa.com/ |
| Instagram | https://www.instagram.com/easypak_sa/ |
| Facebook | https://www.facebook.com/people/Easypak/61561414935207/ |
| TikTok | https://www.tiktok.com/@easypaksa |

Footer: +966 50 842 8883 · info@easypaksa.com

## Why it survives WordPress deletion / host migration
The page is **not** on the WordPress site or the cPanel host. It lives in the public GitHub repo
`digitaldotdeveloper/easypak-qr`, served by GitHub Pages on the subdomain `qr.easypaksa.com`.
The only dependency is the domain itself: keep easypaksa.com on auto-renew and keep the `qr` DNS record.

**Never change the printed URL.** To change where the QR leads, edit `index.html` and push.

## Files
| Path | Purpose |
|---|---|
| `index.html` | the landing page (links + styles inline) |
| `logo.png` | EasyPak wordmark (from easypaksa.com) |
| `CNAME` | tells GitHub Pages the custom domain (`qr.easypaksa.com`) |
| `print/easypak-qr-black-2048.png` | **give this to the printer** |
| `print/easypak-qr-black.svg`, `print/easypak-qr.pdf` | vector versions, any size |
| `print/easypak-qr-blue-*.{png,svg}` | EasyPak blue (#48586A) variant |
| `print/easypak-qr-transparent-2048.png` | no background, for coloured packaging |

QR spec: version 4 (41×41 modules), error-correction level **H** (30%) — survives scuffs and a small
centre logo. Print at least **2 cm wide** with a white quiet zone around it.

## DNS — the one manual step (status: PENDING)
easypaksa.com DNS is at GoDaddy (ns55/ns56.domaincontrol.com). It cannot be edited via cPanel
(GoDaddy locks the cPanel zone to MX records only) and no GoDaddy login/API key is stored locally.
Add in the GoDaddy DNS panel:

```
Type: CNAME   Name: qr   Value: digitaldotdeveloper.github.io   TTL: 1 hour
```

Then in GitHub → repo Settings → Pages → tick **Enforce HTTPS** (becomes available once the record resolves).
Until then the page is reachable at https://digitaldotdeveloper.github.io/easypak-qr/

## Regenerating the QR (only if the URL must change — it shouldn't)
```
py -m pip install segno
py -c "import segno; segno.make('https://qr.easypaksa.com/', error='h').save('qr.png', scale=60, border=4)"
```

## Local clone
`C:\Users\Firass\Desktop\easypak-qr` — push with `git push origin main` (gh CLI is logged in as digitaldotdeveloper).
