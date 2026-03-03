# Changelog

All notable changes to this project will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.1.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## [0.2.0] - 2026-03-03

### Added

- `split-keyword` configuration option to split bibliography entries into two groups based on a BibTeX keyword (e.g. `refereed` / `non-refereed`).
- Support for filling user-defined placeholder divs (`#refs-{keyword}`, `#refs-non{keyword}`) for use with Quarto's native `panel-tabset`.
- Extracted reusable `group_by_year()` helper function for year-based grouping.

### Changed

- Year headings inside split tabs use `heading-level + 1` to nest properly under tab headers.
- Year div IDs include a suffix (`-refereed`, `-nonrefereed`) to prevent duplicate HTML IDs when using split mode.

## [0.1.0] - 2026-03-02

### Added

- Initial release.
- Groups bibliography entries by year with reverse-chronological section headings.
- Configurable heading level (`heading-level`, default: 2).
- Configurable sort order (`sort`: `ascending` or `descending`, default: `descending`).
- Automatic citeproc detection — skips redundant citeproc call if another filter (e.g. `highlight-author`) already ran it.
- Year headings placed outside refs divs so they appear in the table of contents.

[0.2.0]: https://github.com/michaelaye/chronobib/compare/v0.1.0...v0.2.0
[0.1.0]: https://github.com/michaelaye/chronobib/releases/tag/v0.1.0
