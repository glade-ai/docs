# Supported Courts

## Overview

Glade files automatically only in the bankruptcy courts listed on this page. Some courts are limited to a specific chapter or filing type.

## Key Behaviors

Glade currently supports automated filing in the following bankruptcy courts:

- Alabama Northern (ALNB) — Chapter 7 (individual filings only; joint petitions are not yet supported)
- Florida Middle (FLMB)
- Florida Northern (FLNB)
- Florida Southern (FLSB)
- Idaho (IDB)
- Kentucky Western (KYWB) — Chapter 7
- Louisiana Eastern (LAEB) — Chapter 7
- Maryland (MDB) — Chapter 7
- South Carolina (SCB)
- Virginia Eastern (VAEB) — Chapter 7
- Washington Eastern (WAEB) — Chapter 7
- Washington Western (WAWB) — Chapter 7 and Chapter 13

Districts that list a chapter (for example, Kentucky Western — Chapter 7) only support filings of the listed chapter. Districts without a chapter qualifier support all chapters Glade files (Chapter 7 and Chapter 13). Courts not in this list are not available for automated filing.

## Configuration

| Setting | Description |
|---------|-------------|
| Court district | Selected per filing from the case's eFiling modal |

## Edge Cases & Limitations

- Only bankruptcy cases (Chapters 7 and 13) are supported. Other case types (civil, criminal, appellate) are not available.
- Courts outside the supported list cannot be filed to through Glade.

## Related Features

- [PACER Integration](./README.md)
- [District rules checked before filing](../efiling/pre-filing-review/district-rules.md)
- [South Carolina DeBN elections](./south-carolina-debn.md)
