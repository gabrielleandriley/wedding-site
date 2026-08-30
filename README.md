# gabrielleandriley.com

Our wedding website. Built with [Quarto](https://quarto.org), same as Gabrielle's
academic site.

**June 19, 2027 · Fontainebleau Inn · Alpine, New York**

## Editing

Each page is a `.qmd` file. The content is plain HTML inside a ` ```{=html} ` block,
so you can edit the text directly without touching any layout.

| File | Page |
|---|---|
| `index.qmd` | Home — hero, date, weekend details, countdown, photo |
| `travel.qmd` | Travel & Stay — hotels, shuttle, B&Bs |
| `things-to-do.qmd` | Things to Do — wineries, hiking, food, shops, kids |
| `registry.qmd` | Registry — Zola |
| `styles.scss` | All colors, fonts, and layout |
| `_quarto.yml` | Site title, nav bar, footer |

Colors and fonts live at the top of `styles.scss` as variables — change `$green-deep`
or `$sage` there and it updates everywhere.

To preview locally with live reload:

```sh
quarto preview
```

## Publishing

The site deploys to GitHub Pages. To push an update:

```sh
quarto publish gh-pages
```

That rebuilds the site and pushes the output to the `gh-pages` branch. Commit your
source changes separately with `git commit` / `git push`.

### One-time setup

1. Create an empty repo on the joint GitHub account (e.g. `wedding`).
2. Point this folder at it:
   ```sh
   git remote add origin https://github.com/<account>/<repo>.git
   git push -u origin main
   ```
3. Run `quarto publish gh-pages` once — it creates the `gh-pages` branch.
4. On GitHub: **Settings → Pages** → set Source to the `gh-pages` branch.
5. Under **Custom domain**, enter `gabrielleandriley.com` and tick
   *Enforce HTTPS* once the certificate finishes provisioning.

### DNS at Wix

The domain is registered through Wix, so the DNS records get changed there
(**Domains → gabrielleandriley.com → Manage DNS**). Point it at GitHub Pages:

| Type | Host | Value |
|---|---|---|
| A | `@` | `185.199.108.153` |
| A | `@` | `185.199.109.153` |
| A | `@` | `185.199.110.153` |
| A | `@` | `185.199.111.153` |
| CNAME | `www` | `<account>.github.io` |

Remove any existing A or CNAME records on `@` and `www` that point at Wix's own
servers first, or they will conflict. DNS changes can take a few hours to
propagate.

The `CNAME` file in this folder is what tells GitHub Pages which domain to serve —
it gets copied into the build output automatically. Don't delete it.

## Images

Source photos live in `../Photos` and `../Backgrounds`. The web-ready versions in
`images/` were derived from them:

- `hero-venue.jpg` — `Backgrounds/FB high.png`, cropped to the inn and the lake
- `maine.jpg` — `Photos/maine_hike.JPEG`, rotated upright (the original is
  EXIF-flipped 180°)
- `greenshells.jpg` — `Backgrounds/greenshells.jpg`, resized for tiling

Engagement photos slot into `index.qmd` where the Maine photo is now.
