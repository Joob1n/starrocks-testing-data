# External catalog test data

Organize fixtures by table format or data source. Each directory contains its
native data layout, generation tools where available, and dataset documentation.

- [paimon/](paimon/README.md): Paimon filesystem catalog fixtures.

Keep a table's data and metadata together. The `catalog/` directory groups assets
in this repository; it does not prescribe their runtime object-storage paths.
Test cases and environment setup remain in the StarRocks repository.
