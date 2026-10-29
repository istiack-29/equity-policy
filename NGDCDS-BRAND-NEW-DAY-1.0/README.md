# NGDCDS Brand New Day 1.0 — Forms

## Repository layout

```text
/
├── B1.ttf
├── E1.ttf
├── E2.ttf
└── NGDCDS-BRAND-NEW-DAY-1.0/
    ├── index.html
    ├── clash/index.html
    ├── equity/index.html
    ├── club.png
    ├── ev.png
    ├── style.css
    ├── form.js
    └── cl/index.html
```

Put the three font files in the repository root exactly as named. The `B1.ttf`, `E1.ttf`, and `E2.ttf` font files are not bundled; add your licensed/original font files yourself.

## Deploy the static website

Upload the contents while preserving the directory structure to the GitHub repository / static host. The public URLs will be:
- `/NGDCDS-BRAND-NEW-DAY-1.0/`
- `/NGDCDS-BRAND-NEW-DAY-1.0/clash/`
- `/NGDCDS-BRAND-NEW-DAY-1.0/equity/`
- `/NGDCDS-BRAND-NEW-DAY-1.0/cl/`

`ev.png` is configured as the favicon and Open Graph image. `club.png` is used as the club logo.

## Cloudflare Worker

1. In `worker/wrangler.toml`, replace `REPLACE_WITH_YOUR_KV_NAMESPACE_ID` with the ID from `wrangler kv namespace create FORM_STATE`.
2. In `worker/index.js`, set `DISCORD_WEBHOOK_URL` to your private Discord webhook URL.
3. Run `wrangler secret put ADMIN_PASSWORD` and enter a strong password.
4. Run `wrangler deploy` from the `worker` directory.
5. Copy the deployed Worker URL into `form.js` and `cl/index.html` in place of the placeholder URL.
6. Deploy the updated static files.

The Worker is responsible for checking whether each form is open before accepting submissions and for password-protecting open/close actions. Keep the Discord channel for equity reports private to authorized equity-team members only.

## Important

- Verify the deployed Worker URL in both frontend files.
- Configure CORS to allow only your website origin before production use.
- Evidence uploads must be supported by the chosen storage service if you want actual file attachments retained; a text-only webhook payload cannot store uploaded files by itself.
