# chronobib

A [Quarto](https://quarto.org) extension that groups bibliography entries by year with section headings, newest first.

## Use cases

- **Academic homepages** — show your publication timeline at a glance
- **CVs and resumes** — organize references chronologically
- **Lab group pages** — display collective output by year
- **Research reports** — structure literature reviews by period

Works with any Quarto output format: HTML, PDF, Word, and more.

## Installation

```bash
quarto add michaelaye/chronobib
```

## Usage

Add to your document's YAML front matter:

```yaml
bibliography: references.bib
citeproc: false
filters:
  - michaelaye/chronobib

nocite: |
  @*
```

**Important:** `citeproc: false` is required because this filter runs citeproc internally to process the bibliography before grouping entries.

This produces a bibliography with year headings:

> ## 2024
>
> Brown, Sierra, et al. 2024. "PDR: The Planetary Data Reader." ...
>
> Walter, S. H. G., et al. 2024. "Mars Reconnaissance Orbiter ..." ...
>
> ## 2023
>
> Mc Keown, L. E., et al. 2023. "Martian Araneiforms: A Review." ...

### Configuration options

**Defaults** (no configuration needed — newest first, H2 headings):

```yaml
filters:
  - michaelaye/chronobib
```

**Custom heading level and sort order:**

```yaml
chronobib:
  heading-level: 3     # use H3 instead of H2 (default: 2)
  sort: ascending       # oldest first (default: descending)
```

## Splitting by keyword (e.g. refereed / non-refereed)

You can split the bibliography into groups using a BibTeX keyword and display them in Quarto's native tabset panels. This is useful for separating refereed journal articles from conference proceedings.

Add `split-keyword` to your chronobib config and create placeholder divs inside a tabset in the document body:

```yaml
---
bibliography: references.bib
citeproc: false
filters:
  - michaelaye/chronobib
chronobib:
  split-keyword: refereed
---

::: {.panel-tabset}
## Refereed

::: {#refs-refereed}
:::

## Non-Refereed

::: {#refs-nonrefereed}
:::
:::
```

The filter splits entries based on whether the keyword (here `refereed`) appears in the BibTeX `keywords` field, then fills each placeholder div with year-grouped entries. Quarto handles the tab rendering natively.

**Requirements:**

- Each BibTeX entry must have the keyword (e.g. `refereed`) in its `keywords` field. Entries without the keyword go to the "non" group.
- The placeholder div IDs must follow the pattern `refs-{keyword}` and `refs-non{keyword}`.
- When `split-keyword` is not set, the filter produces the standard flat year-grouped output (fully backward-compatible).

## Related tools

- [highlight-author](https://github.com/michaelaye/highlight-author) — Quarto extension that highlights a specific author's name in bibliography entries. Put highlight-author first since it invokes citeproc; chronobib will detect the existing bibliography and skip the redundant citeproc call:

```yaml
citeproc: false
filters:
  - michaelaye/highlight-author
  - michaelaye/chronobib

highlight-author: "Aye"
```

- [ads-bib-tools](https://github.com/michaelaye/ads-bib-tools) — Fetch your complete publication list from NASA ADS by ORCID, with cleanup and refereed/non-refereed tagging. The tagged `.bib` file works directly with chronobib's `split-keyword` feature.

## License

MIT
