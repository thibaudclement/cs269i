# Stanford CS269I Course Notes (Spring 2025)

These course notes for **Stanford CS269I: Incentives in Computer Science** are based on the content of Aviad Rubinstein's lectures in the Spring 2025 quarter. This site is inspired by Eric Gao's course notes from the Winter 2023 quarter, and developed by Thibaud Clement.

## Stack

The site is built with [MkDocs](https://www.mkdocs.org/) and styled using the [Material theme](https://github.com/squidfunk/mkdocs-material).

## Hosting

The site is hosted via [GitHub Pages](https://pages.github.com/) and is available [here](https://thibaudclement.github.io/cs269i/).

## Navigation

To update the site's structure, edit the `nav:` in the `mkdocs.yml` configuration file.

## Formatting

Custom CSS rules are defined in `docs/stylesheets/extra.css` to visually distinguish different types of content. Use the following HTML snippets in Markdown files:

- Definitions: `<div class="definition" markdown="1"> ... </div>`
- Theorems: `<div class="theorem" markdown="1"> ... </div>`
- Proofs: `<div class="proof" markdown="1"> ... </div>`
- Examples: `<div class="example" markdown="1"> ... </div>`
- Call-outs: `<div class="remark" markdown="1"> ... </div>`
- Recaps: `<div class="summary" markdown="1"> ... </div>`

## Deploy

After making changes, you can deploy the site using the following commands:

```
  git add .
  git commit -m "Commit message goes here."
  git push origin main
  mkdocs gh-deploy
```