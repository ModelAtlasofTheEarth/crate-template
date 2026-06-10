# `mate/` — website assets (a convenience, not a rule)

A conventional home for the images, animations, and thumbnails that appear on your
model's website page. Dropping files here keeps a repo tidy and makes it obvious to
contributors *where website material goes*.

**It is only a convention.** What actually puts a file on the page is **tagging it
with a role** (open the *Tag website content* issue, or `crate role <file> --as …`) —
the build reads the role from the crate, never the folder path. So assets can live
anywhere; this folder is just the easy default.

Suggested layout:

```
mate/
├── figures/       # stills: graphical abstract, setup diagram, result figures
└── animations/    # simulation movies (.mp4 / .webm / …)
```
