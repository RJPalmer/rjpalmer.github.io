# rjpalmer.github.io

A small, static personal portfolio page that dynamically lists the owner's GitHub repositories grouped by programming language. The site is a single-page application (vanilla HTML/CSS/JavaScript) that fetches public repositories from the GitHub REST API and renders them as an accordion UI so visitors can browse projects by language.

## What this project does
- Fetches public repositories for the GitHub user `RJPalmer` and groups them by `language`.
- Renders an accessible-ish accordion UI with per-repo cards containing the repo name, description, star count, and last-updated date.
- Provides controls to Expand All / Collapse All and a theme toggle (light/dark) persisted in `localStorage`.

## Stack
- Languages: HTML, CSS, JavaScript (vanilla)
- No build step or server required — this is a static site intended for GitHub Pages or any static host.

## Files of interest
- `index.html` — Single-page application. Contains the fetch to `https://api.github.com/users/RJPalmer/repos?per_page=100` and all client-side logic that groups and renders repositories.
- `css/styles.css` — Styling and theme variables.

## How it works (brief)
When the page loads the client-side JS calls the GitHub REST API to retrieve repositories for `RJPalmer`. Repositories are grouped by the `language` property returned by the API and displayed in accordion sections sorted by last-updated date. The theme toggle stores the user's choice in `localStorage` and the page updates the `data-theme` attribute on the root element to switch themes.

## Running locally
There is no build step. To view the page after cloning, serve the folder with a simple static server (recommended to avoid filesystem fetch restrictions):

```bash
# from repo root
python3 -m http.server 8000
# open http://localhost:8000
```

Or use a Node static server:

```bash
npx http-server -p 8000
# open http://localhost:8000
```

You can also publish the repository to GitHub Pages (main branch) and access the site at `https://rjpalmer.github.io/`.

## Notes and considerations
- GitHub API rate limits: the page uses unauthenticated requests, which are limited to 60 requests per hour per IP. If you expect higher traffic or want to avoid rate limits during development, consider:
  - Hosting on GitHub Pages so requests come from users' browsers (still subject to rate limits per IP), or
  - Pre-fetching repository data server-side (GitHub Action) and committing a static JSON file the page reads instead of calling the API from the browser.
- Accessibility: the accordion is functional but could be improved (keyboard handling, ARIA roles, focus management).

## Contributing
This repo is a personal site, but patches and suggestions are welcome. Typical changes you might make:
- Improve accessibility and keyboard interactions in `index.html`.
- Add caching or a prefetch Action to avoid API rate limits.
- Enhance the UI with per-repo language badges or filtering controls in `index.html` and `css/styles.css`.

## License
This repository does not include a license file. Add a `LICENSE` if you want to grant reuse rights.
