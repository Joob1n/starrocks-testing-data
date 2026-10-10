# StarRocks Testing Data

Shared test datasets for StarRocks integration tests.

StarRocks references this repository as a Git submodule pinned to a specific
commit. Test cases, expected SQL results, and execution helpers remain in the
StarRocks repository.

## Directory layout

Datasets are grouped by format:

- [paimon/](paimon/README.md): Paimon tables, generation tools, and documentation.

Add other format directories when datasets are introduced. Preserve each format's
native directory structure. Parquet files belonging to a Paimon table stay with
that table; standalone Parquet datasets belong in a separate `parquet/` directory.

## Adding or updating data

- Keep datasets small and focused on the behavior being tested.
- Include generation instructions and tool versions where available.
- Document expected logical results and required physical layouts.
- Keep generation tools alongside their datasets.
- Prefer a new table or dataset when a change would invalidate existing tests.
- Do not include credentials, private endpoints, or sensitive data.

## Using data in StarRocks

Once StarRocks registers this repository at `test/data`, initialize the recorded
version from the StarRocks repository root:

```bash
git submodule update --init test/data
```

CI should use the recorded commit, without `--remote`, to keep test data reproducible.

## Coordinating changes

1. Open a data PR here and a linked StarRocks PR.
2. After the data PR is squash-merged, update the StarRocks submodule pointer to
   the merged commit.
3. Validate and merge the StarRocks PR.

Tests using existing datasets only require a StarRocks PR.
