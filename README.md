# Crate template

A self-describing repository. Drop files into **`data/`**, and an
[RO-Crate](https://www.researchobject.org/ro-crate/) (`ro-crate-metadata.json`) is kept in sync as
the **single source of truth**. Edit its metadata with the four buttons below — no tools required,
just GitHub.

## ✏️ Edit this crate

[![Configure the dataset](https://img.shields.io/badge/Configure_the_dataset-2563eb?style=for-the-badge)](../../issues/new?template=configure-crate.yml)
&nbsp;
[![Add a reference](https://img.shields.io/badge/Add_a_reference-7c3aed?style=for-the-badge)](../../issues/new?template=add-contextual-entity.yml)
&nbsp;
[![Edit a data entity](https://img.shields.io/badge/Edit_a_data_entity-059669?style=for-the-badge)](../../issues/new?template=edit-data-entity.yml)
&nbsp;
[![Tag website content](https://img.shields.io/badge/Tag_website_content-d97706?style=for-the-badge)](../../issues/new?template=tag-website-content.yml)

- **Configure the dataset** — title, description, license, creators for the **whole dataset** (the root).
- **Add a reference** — a *remote* thing the dataset points to: a person, publication, the software
  you used, a funder, or large data hosted elsewhere — by DOI / ORCID / ROR / URL.
- **Edit a data entity** — describe one *local* file or folder (add files to `data/` first).
- **Tag website content** — mark a file with the role it plays on the page (graphical abstract,
  figure, setup diagram…), so the website knows what to show where.

Each button opens a pre-filled issue form; on submit, a GitHub Action writes your answers into the
crate and comments back the equivalent `crate …` command.

## How it works

- **Add data by just adding files** (start with `data/`). Every push, `crate build` mirrors the
  filesystem into the crate as data entities — automatically.
- **The crate is the source of truth.** There's no seed file; the three forms (and the `crate` CLI,
  or [Crate-O](https://github.com/Language-Research-Technology/crate-o)) edit it in place.
- **Enrich** resolves the DOIs / ORCIDs you reference (names, titles, authors…), best-effort.
- The published page is a **generated projection** of the crate — don't hand-edit the crate's
  derived layer (file manifest / git provenance); it's refreshed on every push.

## Local use (optional)

```bash
conda env create -f environment.yml && conda activate crate-kit
crate seed --name "My dataset" --license CC-BY-4.0 --author 0000-0002-1825-0097
crate build .        # scan repo -> crate
crate enrich .       # resolve ORCIDs / DOIs
crate validate .     # check it (add --strict to gate on catalogue-readiness)
crate render . -o _site
```
