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
