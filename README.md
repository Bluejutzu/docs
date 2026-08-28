# bluejutzu docs

The Mintlify site behind [docs.bluejutzu.dev](https://docs.bluejutzu.dev). One
Mintlify project, one theme, one search index — every project gets its own
folder and its own entry in the product switcher.

This repo does not author content. Each project keeps writing and reviewing
its own docs in its own repo; a workflow there copies the result in here on
every push. This repo only holds the synced copies plus the top-level
`docs.json` that wires them into one site. See [CONTRIBUTING.md](./CONTRIBUTING.md)
for how that sync works and how to add a new project.

| Project | Source | Path here |
| --- | --- | --- |
| bmux | [Bluejutzu/bmux](https://github.com/Bluejutzu/bmux) `docs/bmux/` | `/bmux` |
| GLua | [Bluejutzu/glua-lsp](https://github.com/Bluejutzu/glua-lsp) `docs/glua/` | `/glua` |

`glua.bluejutzu.dev` still exists as a path-preserving redirect to
`docs.bluejutzu.dev/glua/*`, since the old URLs are baked into already-shipped
config file schemas and extension versions.
