# Contributing to StarRocks Testing Data

This repository stores shared datasets for StarRocks tests.
Test cases, expected SQL results, and execution helpers belong in
the StarRocks repository.

## Branches and commits

Use descriptive branch names with these prefixes:

- `feature/`: add datasets or generation tools.
- `bugfix/`: correct existing data or tools.
- `docs/`: update documentation.

Example: `feature/paimon-fixtures`.

Write commit messages in English and describe the change clearly.
Sign off every commit with `git commit -s`.

## Dataset layout

Group datasets by test domain at the top level:

- `catalog/<format-or-source>/`: external catalog fixtures, such as Paimon or Iceberg.
- `load/<file-format>/<scenario>/`: ingestion inputs, such as CSV null-value cases.

Create directories only when adding actual datasets. Each domain may use the
internal layout its data requires. Preserve native table structures and keep
data files and metadata belonging to the same table together.

Reuse identical input files across load methods instead of duplicating them.
Introduce a shared directory only when concrete cross-domain reuse requires one.

Keep generation tools and instructions alongside their datasets.
See [catalog/paimon/](catalog/paimon/README.md) for an example.

## Dataset requirements

- Keep datasets small and focused on specific test scenarios.
- Document their source, purpose, and expected logical results.
- Record generator versions and reproduction commands when available.
  For imported fixtures, explicitly note any unknown source information
  or tool versions.
- Document required physical properties, such as overlapping files
  or delete records.
- Do not include credentials, private endpoints, personal information,
  or data without appropriate redistribution rights.
- Prefer adding a new table or dataset when changing existing files
  would invalidate tests that use them.

Reproduction should preserve the required logical results and physical
properties. Generated filenames and timestamps do not need to match.

## Pull requests

Write PR titles and descriptions in English. Use the
[PR template](.github/PULL_REQUEST_TEMPLATE.md) to describe:

- Why the data is needed and what changed.
- The related StarRocks PR, when applicable.
- The test domain, format, approximate data size, and generation instructions.
- How the data was validated.
- Any changes to existing datasets and their impact on tests.

When moving existing fixtures, verify that their contents are unchanged.

## Coordinating with StarRocks

StarRocks pins this repository to a specific submodule commit.

For changes that require both data and test code:

1. Open a data PR and a related StarRocks PR, linking them together.
2. Develop and review both PRs in parallel where practical.
3. Merge the data PR first.
4. Update the StarRocks submodule pointer to the resulting squash commit.
5. Validate and merge the StarRocks PR.

CI must use the commit recorded by StarRocks rather than automatically
tracking the latest data branch.

Tests that reuse existing datasets only require a StarRocks PR.
