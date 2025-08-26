## Active vs. Passive transformations (Informatica)

### Active transformation
- **What it means**: Can change the number of rows or the transaction boundary/order.
- **Typical effects**: filters/splits rows, aggregates, joins, ranks, unions, changes row type (DD_INSERT/UPDATE/DELETE).
- **Common examples**: Source Qualifier, Filter, Router, Aggregator, Joiner, Rank, Sorter, Union, Normalizer, Update Strategy, Transaction Control.
- **Notes**: Many are blocking/semi‑blocking (e.g., Aggregator, Sorter), which can affect memory and performance.

### Passive transformation
- **What it means**: Does not change the number of rows; each input row produces at most one output row and doesn’t alter transaction boundaries.
- **Typical effects**: cleans/enriches data, generates sequence keys, looks up reference data.
- **Common examples**: Expression, Sequence Generator, Lookup (single‑row), Stored Procedure (passive), Data Masking.
- **Notes / special cases**: Lookup becomes active if configured to return multiple matches (“Use All Values”) or with certain dynamic cache behaviors; Java/SQL transformations can be active or passive depending on mode.


