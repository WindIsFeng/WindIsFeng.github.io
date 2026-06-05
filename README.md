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
