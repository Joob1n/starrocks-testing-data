# StarRocks Testing Data

Shared test datasets for StarRocks integration tests.

StarRocks references this repository as a Git submodule pinned to a specific
commit. Test cases, expected SQL results, and execution helpers remain in the
StarRocks repository.

## Directory layout

Datasets are grouped by test domain:

- [catalog/](catalog/README.md): external catalog fixtures, organized by table
  format or data source, including [Paimon](catalog/paimon/README.md).
- `load/`: reserved for ingestion inputs, organized by file format and scenario,
  for example `load/csv/null_values/`. Create it when the first dataset is added.

Preserve each format's native directory structure. Parquet files belonging to a
Paimon table stay with that table under `catalog/paimon/`.
Reuse input files across load methods when their contents are identical.
Add other domain directories only when actual datasets need them.

## Contributing

See [CONTRIBUTING.md](CONTRIBUTING.md) for dataset requirements, branch naming,
commit conventions, and the cross-repository PR workflow.

## Using data in StarRocks

Once StarRocks registers this repository at `test/data`, initialize the recorded
version from the StarRocks repository root:

```bash
git submodule update --init test/data
```

CI should use the recorded commit, without `--remote`, to keep test data reproducible.
