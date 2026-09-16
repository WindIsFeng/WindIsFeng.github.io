# Feng Hu Personal Homepage

This repository hosts the source code for Feng Hu's personal academic website:

https://windisfeng.github.io/

Feng Hu is a PhD student at City University of Hong Kong. His research focuses on tropical cyclone wind hazard modeling and risk analysis, using AI models, probabilistic models, and physics-based models.

## Site Content

- About and biography
- Research interests
- Selected publications
- Full publication list
- News
- CV

## Development

Install Node.js 22 (including npm) on your computer; keep its runtime and installers outside this project.

Install dependencies:

```bash
npm ci
```

Run the local development server:

```bash
npm run dev
```

Build the static site:

```bash
npm run build
```

The production site is deployed automatically to GitHub Pages through GitHub Actions whenever changes are pushed to the `main` branch.

## Main Content Files

See the **[Chinese content maintenance guide](docs/content-editing-guide.md)** for editing instructions, field explanations, examples, and publishing checks.

- `content/config.toml`: English site metadata, navigation, and social links
- `content/about.toml`: English homepage section layout
- `content/bio.md`: English biography
- `content/publications.bib`: Publication metadata
- `content/news.toml`: English news items
- `content_zh/`: Chinese localized content
- `public/profile.jpg`: Profile photo
- `public/papers/`: Publication preview images

## Acknowledgement

This site is customized from the open-source PRISM academic homepage template.

## Local files and disk space

`node_modules/` contains local dependencies needed for development and builds; restore it with `npm ci`. `.next/` is build cache and `out/` is generated static output. After stopping the development server, these generated directories can be removed and recreated with `npm run build`. Git already ignores them; cloud-sync exclusions must be configured separately. Keep `package.json` and `package-lock.json` for reproducible installation. npm uses a user-level cache by default, so a project-local `.npm-cache/` is unnecessary.

