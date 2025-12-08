# Perthia

<p align="center">
  <img src="branding/Perthia.svg" alt="Perthia logo" width="220" />
</p>

Perthia is a small web presence and branding space for a Perth-based gaming community. The site is a static landing page with simple assets and a containerized Nginx setup for easy hosting.

## Project Structure

- `branding/` — brand assets and notes.
- `web/` — website and container files.
  - `docs/` — static site content served by Nginx (`index.html`, `style.css`, images).
  - `docker/` — Dockerfile and Nginx configuration for hosting.

## Getting Started

You can serve the static site locally or via Docker.

### Option 1: Quick local preview

Use a simple HTTP server to preview `web/docs`:

```bash
cd web/docs
python3 -m http.server 8080
# Open http://localhost:8080
```

### Option 2: Run with Docker

Build and run the Nginx container that serves the `web/docs` directory.

```bash
cd web
docker build -t perthia-site -f docker/Dockerfile .
docker run --rm -p 8080:80 perthia-site
# Open http://localhost:8080
```

## Website

- Entry point: `web/docs/index.html`
- Styles: `web/docs/style.css`
- Favicon and SVG assets should be placed in `web/docs/`

The page is intentionally minimal, mobile-friendly, and optimized with basic metadata (Open Graph and Twitter cards).

## Deployment

Any static host or container platform works. For Nginx-based hosting:

- Container: build with the provided `Dockerfile`.
- Config: `web/docker/nginx.conf` maps `/` to the `docs` content.

On a Linux server with Docker installed:

```bash
git clone https://github.com/axodouble/perthia.git
cd perthia/web
docker build -t perthia-site -f docker/Dockerfile .
docker run -d --name perthia -p 80:80 perthia-site
```

## Contributing

- Keep the site minimal and fast.
- Maintain consistency with the existing color palette and typography.
- Optimize images/SVGs for web (minify where reasonable).

Open a PR on `master` with a brief summary of changes. Please avoid adding unnecessary dependencies.

## Notes

- The `index.html` references `style.css` with a cache-busting query string (`?d=05122025`). Update as needed when you change styles.
- If you add new assets (e.g., `favicon.png`, `outline.svg`), place them in `web/docs/` and reference them with relative paths.
