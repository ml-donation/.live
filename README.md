# ML Donation — JSONBin-only GitHub Pages package

This is a static GitHub Pages site. Shared member, donation, proof, message, and website-setting data is stored in one JSONBin record.

## Deploy
1. Extract this folder's contents into the root of the GitHub Pages repository.
2. Keep `member.html`, `admin/`, `jsonbin-config.js`, `manifest.webmanifest`, `pwa-install.js`, `service-worker.js`, and `icons/` at these exact paths.
3. In GitHub repository Settings → Pages, publish from the `main` branch and repository root.
4. Open the public homepage. Member access is at `/member.html`; the admin dashboard is at `/admin/`.

For the repository URL `https://ml-donation.github.io/.org/`, the member page should resolve to `https://ml-donation.github.io/.org/member.html` and the admin page to `https://ml-donation.github.io/.org/admin/`.

## JSONBin
`jsonbin-config.js` contains the Bin ID and browser access key. The Bin must already contain the structure in `jsonbin-seed.json`. If it does not, import that seed into the existing Bin; do not create a second Bin if you want to preserve existing records.

The member page, homepage settings loader, and admin dashboard all use this same JSONBin record directly. No other database or server component is used.

## Important limitations
Because GitHub Pages is static, the JSONBin access key and client-side admin password are visible to visitors. This is a demonstration-grade setup, not secure authentication. Anyone who obtains the access key can potentially read or alter the entire shared record. Do not store real passwords, bank credentials, gift-card redemption codes, identity documents, or sensitive personal information. Rotate any key that has been publicly exposed.

JSONBin is a single shared JSON document. Simultaneous writes from different browsers can still conflict or overwrite one another; a static site cannot provide server-side transactions or reliable locking. Large profile/proof images also increase the Bin size quickly.

## PWA
The site includes an installable web-app manifest, icons, and a service worker. JSONBin operations require an internet connection. The service-worker cache version has been incremented so deployed browsers fetch the updated app shell.


## Troubleshooting the current build
The public homepage no longer carries a duplicate embedded copy of the member page. The member signup preloader is short, and JSONBin requests fail with a visible timeout message instead of waiting indefinitely. After deployment, close the old browser tab and reopen the site; if it was installed as a PWA, refresh it once so the v5 service worker can replace the older cache.
