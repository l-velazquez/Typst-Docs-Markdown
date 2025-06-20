# Version 0.13.1 (March 7, 2025)

## Command Line Interface

- Fixed high CPU usage for `typst watch` on Linux. Depending on the
  project size, CPU usage would spike for varying amounts of time. This
  bug appeared with 0.13.0 due to a behavioral change in the inotify
  file watching backend.

## HTML export

- Fixed export of tables with
  [gutters](/reference/model/table/#parameters-gutter)
- Fixed usage of `<html>` and `<body>` element within
  [context](/reference/context/ "context")
- Fixed querying of
  [metadata](/reference/introspection/metadata/ "metadata") next to
  `<html>` and `<body>` element

## Visualization

- Fixed [curves](/reference/visualize/curve/) with multiple non-closed
  components

## Introspection

- Fixed a regression where labelled
  [symbols](/reference/foundations/symbol/) could not be
  [queried](/reference/introspection/query/) by label

## Deprecations

- Fixed false positives in deprecation warnings for type/str comparisons

## Contributors
