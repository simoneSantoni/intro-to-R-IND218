# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## What this is

Course materials for an MSc "Introduction to R" module for analytics students. Everything user-facing lives in `website/`, a Quarto website that renders `.qmd` files with executable R chunks and deploys to GitHub Pages. There is no application code, test suite, or linter; "building" means rendering the site.

## Commands

Run from the repository root. Quarto 1.10.x is installed under `~/opt/quarto-<version>` and symlinked to `~/.local/bin/quarto`. R, `knitr`, `rmarkdown`, and `tidyverse` are installed system-wide.

```bash
quarto preview website          # live-reload dev server
quarto render website           # full build to website/_site/ (tracked, see below)
quarto render website/modules/module-5/joining-data.qmd   # render one page
```

Other R packages loaded by content pages: `lubridate`, `here`, `stringr`, `forcats`, `vroom`, `readxl`, `jsonlite`, `dtplyr`, `data.table`, `magrittr`. Chunks that need something not installed are usually marked `#| eval: false`; check before installing anything.

## How rendering works (non-obvious)

- **Engine is knitr, not Jupyter.** `_quarto.yml` declares a `jupyter: kernelspec` block, but every page uses `{r}` chunks with no `engine:` key, so Quarto selects knitr. The `_freeze/**/html.json` files confirm `"engine": "knitr"`. The kernelspec block is inert; do not add Jupyter-specific config expecting it to take effect.
- **Both `_freeze/` and `_site/` are committed.** `execute: freeze: auto` plus tracked `website/_freeze/` means a page only re-executes when its source changes. The rendered `website/_site/` is also tracked and is what gets deployed, so after editing a `.qmd`, re-render and commit the updated `_freeze` entry and `_site` HTML alongside the source, otherwise the published site lags. Rendering also touches `website/.gitignore` (Quarto appends its own ignore patterns); that change is harmless.
- **Rendering writes files into the source tree.** `website/modules/module-2/working-with-files.qmd` calls `write.csv`, `saveRDS`, `writeLines`, `dir.create`, etc. with relative paths, and knitr's working directory is the page's own folder. The CSVs, `.rds`, `.RData`, `output/`, `scripts/`, and `my_analysis_project/` under `module-2/` are render by-products that have been committed. Treat them as generated: do not hand-edit them, and expect them to change when that page re-executes.
- **Chunk conventions.** Chunks use YAML-style `#|` options. `#| eval: false` is used widely for illustrative code that should not run (installers, absolute paths, slow or destructive examples); `#| error: true` for deliberate error demos; a `#| label: setup` chunk with `#| message: false` loads packages at the top of each page. Site-wide defaults are `echo: true`, `warning: false`, `message: false`.

## Site structure

- `website/_quarto.yml` is the single source of truth for navigation. Adding a page means creating the `.qmd` **and** adding an entry to the matching `sidebar.contents` section; nothing is auto-discovered in the nav (`render: "**/*.qmd"` renders everything, but unlisted pages are orphaned).
- `website/index.qmd` is the homepage; `website/course/` holds syllabus, schedule, support, and team pages; `website/modules/module-N/` holds one folder per module, each with an `index.qmd` overview (Module 1 has none) followed by topic pages.
- Six modules progress from setup, through base-R fundamentals, into the tidyverse (readr/dplyr/tidyr intro, stringr/forcats/lubridate, dplyr wrangling, tidyr reshaping). Content favors tidyverse idioms over base R where a choice exists, and uses invented business-style datasets built inline rather than bundled data files.
- Theming: Cosmo bootstrap with `theme.scss` (light) and `theme-dark.scss` (dark), Atkinson Hyperlegible as `mainfont`. `styles.css` and `theme-switcher.js` exist in `website/` but are not referenced from `_quarto.yml`, so editing them has no effect unless they are wired in.

## Course code

The module code is **IND218** (changed from IND215 in September 2026; a few pages had also said IND216). The GitHub repo, the GitHub Pages URL (`https://simonesantoni.github.io/intro-to-R-IND218`), `_quarto.yml`, page `author:` fields, and all prose use IND218. Keep new content on this code and keep URLs consistent with whatever GitHub Pages actually serves.
