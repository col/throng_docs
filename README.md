# Throng Docs

Documentation site for the Throng platform, built with
[MkDocs](https://www.mkdocs.org/) and the
[Material theme](https://squidfunk.github.io/mkdocs-material/).
Dependencies are managed with [uv](https://docs.astral.sh/uv/).

## Project layout

```
throng_docs/
├── docs/             # Markdown source for every page
│   └── index.md      # Home page
├── mkdocs.yml        # Site config (theme, nav, extensions)
├── pyproject.toml    # Python deps (managed by uv)
├── uv.lock           # Locked dep versions — commit this
└── site/             # Built HTML output (gitignored)
```

## One-time setup

```bash
brew install uv          # if you don't already have it
uv sync                  # creates .venv/ and installs locked deps
```

`uv sync` reads `pyproject.toml` + `uv.lock` and produces a `.venv/` with the
exact versions everyone else is using. Run it after pulling changes that
touch dependencies.

## Day-to-day commands

All commands assume you're in the repo root. `uv run <cmd>` runs `<cmd>`
inside the project's virtualenv without needing to activate it.

| Task                          | Command                                |
| ----------------------------- | -------------------------------------- |
| Live preview at localhost:8000 | `uv run mkdocs serve`                 |
| Preview on a different port    | `uv run mkdocs serve -a 127.0.0.1:8001` |
| Build static site into `site/` | `uv run mkdocs build`                 |
| Build with strict warnings     | `uv run mkdocs build --strict`        |
| Deploy to GitHub Pages         | `uv run mkdocs gh-deploy`             |
| List MkDocs subcommands        | `uv run mkdocs --help`                |

`mkdocs serve` watches `docs/` and `mkdocs.yml` and auto-reloads the browser
on every save — leave it running while you write.

## Adding content

- **New page** → create `docs/some-page.md`. It appears in the sidebar
  automatically. The first `# Heading` becomes the page title.
- **Subsection** → create `docs/guides/intro.md`. The folder becomes a nav
  group; an optional `docs/guides/index.md` becomes that group's landing page.
- **Custom nav order** → uncomment and populate the `nav:` block in
  `mkdocs.yml`. Without it, files are listed alphabetically.
- **Images / assets** → put them in `docs/` (e.g. `docs/img/foo.png`) and
  reference with relative paths: `![alt](img/foo.png)`.

## Managing dependencies (uv)

| Task                              | Command                              |
| --------------------------------- | ------------------------------------ |
| Add a package                     | `uv add <pkg>`                       |
| Add a dev-only package            | `uv add --dev <pkg>`                 |
| Remove a package                  | `uv remove <pkg>`                    |
| Upgrade everything to latest      | `uv lock --upgrade && uv sync`       |
| Re-create venv from scratch       | `rm -rf .venv && uv sync`            |

Commit `pyproject.toml` and `uv.lock` after any of these. Never commit
`.venv/`.

## Deploying to GitHub Pages

1. Push this repo to GitHub.
2. Fill in `site_url`, `repo_url`, and `repo_name` in `mkdocs.yml` (see the
   `TODO` comment at the top of the file).
3. Run `uv run mkdocs gh-deploy` — this builds the site and force-pushes it
   to a `gh-pages` branch on the remote.
4. In the GitHub repo's **Settings → Pages**, set the source to the
   `gh-pages` branch (root). The site will be live at `site_url` within a
   minute or two.

For automated deploys on every push to `main`, add a GitHub Actions workflow
later — ask Claude when you're ready.

## Useful links

- MkDocs: <https://www.mkdocs.org/>
- Material theme reference: <https://squidfunk.github.io/mkdocs-material/reference/>
- Material setup guide: <https://squidfunk.github.io/mkdocs-material/setup/>
- uv docs: <https://docs.astral.sh/uv/>
