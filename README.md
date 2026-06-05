# Dataset crate (template)

A self-describing dataset repository. Its metadata lives in **`ro-crate-metadata.json`** — an
[RO-Crate](https://www.researchobject.org/ro-crate/) built *dynamically from whatever is in
this repo*. That crate is the **single source of truth**; this README and the published page
are **generated projections** of it.

This template is domain-free: it produces a generic [schema.org](https://schema.org) `Dataset`
crate. A discipline (e.g. geoscience) is opted into by dropping a `.mate/profile.yml` in the
repo — the engine (`crate-kit`) is identical either way.

## How it works

There is **no seed file** — the crate (`ro-crate-metadata.json`, shipped here empty) *is* the
thing you author. Three surfaces edit it; all write the crate, none keep a parallel document:

- **Configure the dataset (root).** `crate seed --name "…" --description "…" --license CC-BY-4.0
  --author <ORCID>` — or open the **"Configure dataset (root)"** issue.
- **Add data by just adding files.** `crate build` scans the filesystem and mirrors every file
  and folder into the crate as data entities — automatically, on every push.
- **Describe a specific folder/file** (a *data entity = local*). `crate describe <path> --description
  "…" --type … --author …` locally, or open the **"Edit a data entity"** issue (pick the folder
  from the dropdown), or use Crate-O. Per-entity edits survive rebuilds.
- **Add a remote reference** (a *contextual entity = remote*): a person, publication, the software
  you used, a funder, or large data hosted elsewhere. `crate add publication 10.1038/…` (or
  `creator`/`software`/`funder`/`remote_data`), or open the **"Add a contextual entity"** issue.
- **Enrich.** Best-effort resolution of the DOIs / ORCIDs you referenced (names, titles, authors…).

The published page and any README projection are **generated** from the crate — don't hand-edit
the crate's derived layer (the file manifest / git provenance); it's refreshed on every push.

## Local use

```bash
conda env create -f environment.yml      # installs the crate-kit + quarto
conda activate crate-kit
crate seed --name "My dataset" --license CC-BY-4.0 --author 0000-0002-1825-0097
crate build .        # scan repo -> crate (preserves authored content, refreshes the derived layer)
crate enrich .       # resolve ORCIDs / DOIs (best-effort)
crate validate .     # check the crate (add --strict to gate on catalogue-readiness)
crate render . -o _site
```
