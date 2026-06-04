# Dataset crate (template)

A self-describing dataset repository. Its metadata lives in **`ro-crate-metadata.json`** — an
[RO-Crate](https://www.researchobject.org/ro-crate/) built *dynamically from whatever is in
this repo*. That crate is the **single source of truth**; this README and the published page
are **generated projections** of it.

This template is domain-free: it produces a generic [schema.org](https://schema.org) `Dataset`
crate. A discipline (e.g. geoscience) is opted into by dropping a `.mate/profile.yml` in the
repo — the engine (`mate` toolkit) is identical either way.

## How it works

There is **no seed file** — the crate (`ro-crate-metadata.json`, shipped here empty) *is* the
thing you author. Three surfaces edit it; all write the crate, none keep a parallel document:

- **Author the root.** `mate seed --name "…" --description "…" --license CC-BY-4.0 --author <ORCID>`
  — or open the **"Add / edit metadata"** issue (it defaults to the dataset root).
- **Add data by just adding files.** `mate build` scans the filesystem and mirrors every file
  and folder into the crate as data entities — automatically, on every push.
- **Describe a specific folder/file.** `mate describe <path> --description "…" --type … --author …`
  locally, or pick that path in the same issue form, or use Crate-O. Per-entity edits survive
  rebuilds.
- **Enrich.** Best-effort resolution of any DOIs / ORCIDs you provided.

The published page and any README projection are **generated** from the crate — don't hand-edit
the crate's derived layer (the file manifest / git provenance); it's refreshed on every push.

## Local use

```bash
conda env create -f environment.yml      # installs the mate toolkit + quarto
conda activate mate
mate seed --name "My dataset" --license CC-BY-4.0 --author 0000-0002-1825-0097
mate build .        # scan repo -> crate (preserves authored content, refreshes the derived layer)
mate enrich .       # resolve ORCIDs / DOIs (best-effort)
mate validate .     # check the crate (add --strict to gate on catalogue-readiness)
mate render . -o _site
```
