# Dataset crate (template)

A self-describing dataset repository. Its metadata lives in **`ro-crate-metadata.json`** — an
[RO-Crate](https://www.researchobject.org/ro-crate/) built *dynamically from whatever is in
this repo*. That crate is the **single source of truth**; this README and the published page
are **generated projections** of it.

This template is domain-free: it produces a generic [schema.org](https://schema.org) `Dataset`
crate. A discipline (e.g. geoscience) is opted into by dropping a `.mate/profile.yml` in the
repo — the engine (`mate` toolkit) is identical either way.

## How it works

- **Seed it once.** Fill `.mate/metadata.yml` (or open a *New dataset* issue). On push, an
  action writes those values into the crate's root entity.
- **Add data by just adding files.** `mate build` scans the filesystem and mirrors every file
  and folder into the crate as data entities — automatically, on every push.
- **Enrich.** Best-effort resolution of any DOIs / ORCIDs you provided.
- **Describe specifics.** Per-file/-folder detail (a different author, a description, a type)
  is an editing act: `mate describe <path>` locally, or Crate-O — *not* the issue.

## Local use

```bash
conda env create -f environment.yml      # installs the mate toolkit + quarto
conda activate mate
mate build .        # scan repo -> crate (preserves authored content, refreshes the derived layer)
mate enrich .       # resolve ORCIDs / DOIs (best-effort)
mate validate .     # check the crate
mate render . -o _site
```

> Do not hand-edit `ro-crate-metadata.json`'s derived layer or the generated page — they are
> regenerated on every push.
