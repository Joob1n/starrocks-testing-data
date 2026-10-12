# Paimon test data

`warehouse/` preserves Paimon's filesystem catalog layout. The `paimon_test.db/`
directory contains these tables:

| Table | Purpose |
| --- | --- |
| `scalar_types` | Scalar values, nulls, and reader mode comparisons |
| `variant_basic` | VARIANT reads |
| `image_blob` | BLOB reads |
| `image_blob_desc` | Additional BLOB read coverage |
| `image_blob_view` | BLOB view read coverage |
| `pk_merge_v1` | Primary-key updates and deletes across overlapping L0 files |

The first five tables were copied byte-for-byte from StarRocks PR #79856
(commit `bed6f25ced9f5fd3fa3a74f85021de6ec1ce0469`). Their original generator
versions were not recorded. The SQL expectations remain in StarRocks under
`test/sql/test_paimon_catalog/`.

Only `pk_merge_v1` has a generator in this repository. See
[datagen/README.md](datagen/README.md) for the Paimon 2.0.0 generation commands,
expected rows, and physical layout checks.

Keep existing fixtures unchanged where possible. Add new tables for new scenarios.
StarRocks stages selected tables to a per-case OSS warehouse before reading them;
this repository itself does not require OSS credentials.
