# Adding or updating a project

## How the sync works

Nothing in this repo generates content. Each project repo:

1. Keeps its Mintlify pages under `docs/<slug>/` in its own repo — already
   scoped to that path, so what's on disk there is exactly the folder that
   ends up here.
2. Runs a `sync-docs.yml` workflow on every push to its default branch that
   touches `docs/<slug>/**`. The workflow checks out this repo, replaces
   `<slug>/` wholesale with the current `docs/<slug>/`, and pushes straight
   to `main` if anything changed.

This repo doesn't care how a project versions itself — changesets, a
hand-rolled release script, or a changelog someone edits by hand all produce
the same thing from this repo's side: a folder to copy. Nothing here parses
version numbers or changelog formats.

## Adding a new project

1. Pick a slug (a short, URL-safe name — `bmux`, `glua`, whatever the next
   one is called).
2. In the project's own repo, put its Mintlify content under `docs/<slug>/`
   — an `index.mdx` at minimum. Root-relative links inside those pages need
   the `/<slug>` prefix (e.g. `/glua/installation`, not `/installation`),
   since that's where the page will actually live once it's synced here.
3. Copy `.github/workflows/sync-docs.yml` from `bmux` or `glua-lsp` into the
   new repo, and change `SLUG` (and the branch name, if its default branch
   isn't `main`/`master`).
4. Create a fine-grained GitHub PAT scoped to **this** repo
   (`Bluejutzu/docs`) with **Contents: Read and write**, and add it to the
   new project's repo as the `DOCS_SYNC_TOKEN` secret.
5. Open a PR against this repo adding a `"product"` entry to `docs.json`
   under `navigation.products`, with pages under `<slug>/...`. This step
   stays manual — the nav structure (tabs vs. flat groups, ordering) is a
   judgment call, not something worth generating.
6. Merge once the first sync has run and the `<slug>/` folder exists.

## Renaming or removing pages

Rename/delete inside the source repo's `docs/<slug>/` as normal — the next
sync overwrites the whole folder, so stale pages don't linger. Update the
matching entries in this repo's `docs.json` in the same PR that changes the
navigation-relevant structure (adding/removing/renaming a page), since the
sync workflow never touches `docs.json` itself.
