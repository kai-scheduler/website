# KAI Scheduler Website

Source for the [KAI Scheduler](https://github.com/kai-scheduler/KAI-Scheduler) website at **https://kai-scheduler.dev/**.

The site is built with [Hugo](https://gohugo.io/) (extended) and the [Docsy](https://www.docsy.dev/) theme, pulled in as a Hugo module.

---

## Prerequisites

You'll need:

| Tool   | Version            | Why                                                |
| ------ | ------------------ | -------------------------------------------------- |
| Hugo   | extended, ≥ 0.128  | SCSS compilation requires the extended build       |
| Go     | ≥ 1.21             | Used by Hugo to resolve the Docsy theme module     |
| Node   | ≥ 18               | PostCSS + autoprefixer run as part of CSS pipeline |
| npm    | bundled with Node  | Installs the PostCSS toolchain                     |

### macOS

```bash
brew install hugo go node
```

### Linux

```bash
# Hugo: grab the latest "extended" .deb from https://github.com/gohugoio/hugo/releases
# then:
sudo dpkg -i hugo_extended_*.deb

# Go and Node from your distro's package manager, or:
# https://go.dev/doc/install
# https://nodejs.org/
```

Verify:

```bash
hugo version            # must say "extended"
go version
node -v && npm -v
```

---

## Local development

```bash
git clone https://github.com/kai-scheduler/website.git
cd website

# Install the PostCSS toolchain Hugo invokes during builds
npm install

# Start the dev server (hot reload)
hugo server
```

Open <http://localhost:1313/> in your browser. Edits to `content/`, `layouts/`, `assets/`, or `static/` reload automatically.

### Production build

```bash
hugo --minify
```

The static site is written to `public/`. That directory is what gets deployed.

---

## Repository layout

```
.
├── hugo.yaml                  # Site config (title, baseURL, top nav, params)
├── go.mod / go.sum            # Hugo module — pulls in google/docsy
├── package.json               # PostCSS + autoprefixer
├── content/en/                # Page content (Markdown + front matter)
│   └── _index.md              #   Homepage front matter
├── layouts/
│   ├── index.html             # Homepage template
│   └── partials/              # Reusable sections (hero terminal, arch diagram, talks, blogs, …)
├── assets/
│   ├── scss/                  # Brand variables + component styles
│   └── icons/                 # Inline SVG icons
└── static/                    # Pass-through assets
    ├── favicons/
    ├── images/logos/          # Logo SVGs the site itself renders
    └── brand/                 # Full press kit (SVG + PNG, all variants) + logo reference PDF
```

### Customisation entry points

| File                                       | What it controls                                    |
| ------------------------------------------ | --------------------------------------------------- |
| `hugo.yaml`                                | Top nav, site title, baseURL, social/GitHub links   |
| `assets/scss/_variables_project.scss`      | Brand colours, fonts (Docsy/Bootstrap overrides)    |
| `assets/scss/_styles_project.scss`         | Docsy chrome overrides (navbar, footer, typography) |
| `assets/scss/_alt-d.scss`                  | Homepage-specific styles (scoped under `.alt-d`)    |
| `layouts/partials/kai-*.html`              | Homepage section partials — edit copy/markup here   |
| `layouts/partials/navbar.html`             | Top-nav override                                    |

Hugo resolves project files before theme files at the same path, so anything in `layouts/` or `assets/` here wins over the corresponding file in the Docsy theme.

### Brand kit

Colours, type, and the full set of logo SVGs are vendored in this repo.

**Colours**

- **KAI Magenta** `#F30099`
- **Space Blue** `#00203E`

**Typography**

- **Headlines:** Albert Sans 800
- **Body:** Albert Sans 500
- **Code:** JetBrains Mono

Both web fonts are loaded from Google Fonts in `assets/scss/_styles_project.scss`.

**Quick reference** — the logo variants the site itself uses, under [`static/images/logos/`](static/images/logos/):

| File                                          | Format     | Use on                                |
| --------------------------------------------- | ---------- | ------------------------------------- |
| `horizontal-color-positive-transparent.svg`   | Horizontal | Light surfaces (transparent)          |
| `horizontal-white.svg`                        | Horizontal | Any surface (solid Space Blue tile)   |
| `horizontal-white-transparent.svg`            | Horizontal | Dark or coloured surfaces (transparent) |
| `stacked-color.svg`                           | Stacked    | Any surface (solid white tile)        |
| `stacked-color-transparent.svg`               | Stacked    | Light surfaces (transparent)          |
| `stacked-color-negative.svg`                  | Stacked    | Any surface (solid Space Blue tile)   |
| `stacked-color-negative-transparent.svg`      | Stacked    | Dark or coloured surfaces (transparent) |

**Full brand kit** — every logo variant in SVG + PNG, plus the official logo reference PDF, lives under [`static/brand/`](static/brand/):

```
static/brand/
├── logo-reference.pdf         ← brand guidelines (clear space, do/don't, sizing)
├── horizontal/                ← wide format, wordmark + icon side-by-side
├── stacked/                   ← square format, icon above wordmark
└── icon/                      ← icon mark only
```

Each format has six variants — `color-positive`, `color-negative`, `color`, `black`, `white`, `space-blue` — provided in both `.svg` (vector, infinitely scalable) and `.png` (raster, for tools that need it). Pick the one that suits your background.

---

## Contributing

1. Fork this repo and create a feature branch.
2. Make your changes — run `hugo server` locally and confirm the page renders as expected.
3. Open a pull request describing what changed and why.

For larger changes (new sections, restructured navigation, design shifts), it's worth opening an issue first so we can align on direction.

---

## License

The website content and code in this repository are released under the [Apache License 2.0](LICENSE).
