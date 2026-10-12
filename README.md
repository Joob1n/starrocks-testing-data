# StarRocks Testing Data

Shared datasets for StarRocks tests. Test cases and SQL expectations remain in
the StarRocks repository.

## Layout

- [catalog/](catalog/README.md): external catalog fixtures, including
  [Paimon](catalog/paimon/README.md).
- `load/<format>/<scenario>/`: ingestion inputs; create directories as needed.

Keep datasets small and preserve native table structures. Include data sources,
generation instructions, and expected results when adding fixtures. Reuse
identical files and do not include credentials or sensitive data.

## Use in StarRocks

From the StarRocks repository root, fetch the pinned data version:

```bash
git submodule update --init test/data
```

After a data PR is squash-merged, update the StarRocks submodule pointer to the
merged commit.
