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

## Combining with highlight-author

chronobib pairs well with [highlight-author](https://github.com/michaelaye/highlight-author). Put highlight-author first since it invokes citeproc; chronobib will detect the existing bibliography and skip the redundant citeproc call:

```yaml
citeproc: false
filters:
  - michaelaye/highlight-author
  - michaelaye/chronobib

highlight-author: "Aye"
```

## License

MIT
