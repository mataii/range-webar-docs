# Range WebAR Exporter — Documentation

Documentation site for the Range WebAR Exporter Blender addon.  
Built with [MkDocs Material](https://squidfunk.github.io/mkdocs-material/).

## Local preview

```bash
pip install mkdocs-material
mkdocs serve
```

Open `http://localhost:8000` in your browser.

## Deploy to GitHub Pages

1. Push this repo to GitHub
2. Go to **Settings → Pages → Source** and select **GitHub Actions**
3. Push a commit to `main` — the workflow in `.github/workflows/deploy.yml` builds and deploys automatically

Remember to update `site_url` in `mkdocs.yml` to match your GitHub Pages URL:
```
https://your-username.github.io/your-repo-name/
```

## License

GPL v3 — same as the addon.
