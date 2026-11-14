# Data Analytics and Databases

Car-sharing demand analysis and SQLite database coursework from my MSc Computer Science at Keele University in **2023/24**. This repository preserves the assessed notebooks, the resulting database and a privacy-reviewed technical report extract, alongside later tools for inspecting the database safely.

| Academic record | Detail |
| --- | --- |
| Module | Data Analytics and Databases, CSC-40054 |
| Level and credit | Level 7, 15 CATS |
| Verified module mark | **89%** |
| Project year | **2024** |

The overall module mark was verified against my private official transcript. It is not a notebook test score or a fresh model benchmark. [Keele's archived 2023/24 specification](https://www.keele.ac.uk/catalogue/2023-24/csc-40054.htm) describes the database, statistical-analysis and machine-learning context.

## What is here

The coursework uses an hourly car-sharing demand dataset with calendar and weather variables. The database work imports records, creates backup and derived tables, categorises temperature and weather, and produces demand summaries. The analytics notebook explores preprocessing, statistical relationships, time-series forecasting, random-forest and neural-network regression, and clustering.

| Material | Purpose |
| --- | --- |
| [DatabaseManagement.ipynb](DatabaseManagement.ipynb) | Original database creation, transformation and SQL analysis |
| [DataAnalytics.ipynb](DataAnalytics.ipynb) | Original preprocessing, statistics and modelling experiments |
| [CarSharing.db](CarSharing.db) | Historical database snapshot, including 8,708 source records in `CarSharingBackup` |
| [Student report extract](docs/original/student-report-technical-text.md) | Historical technical explanation and source-code appendix with identifiers and screenshots excluded |
| [Assessment evidence](docs/original/README.md) | Official coursework/exam briefs and document provenance |
| [Coursework guide](docs/COURSEWORK.md) | Skills mapped to actual files and task boundaries |
| [Engineering notes](docs/ENGINEERING.md) | Reproduction limits, data contracts and safe maintenance |

## Inspect the supplied database

The maintained inspection command uses only the Python standard library and opens the database read-only. Download or clone the complete repository, then run from its root with Python 3.12:

```bash
python scripts/inspect_database.py
python -m unittest discover -s tests -v
```

To export a bounded copy of the original backup table to a **new** CSV file:

```bash
python scripts/inspect_database.py --table CarSharingBackup --output CarSharing-extract.csv --limit 10000
```

The committed backup has 8,708 rows, so this limit includes all of them. Exports cannot overwrite existing files. This is a convenient way to inspect the historical data; it is not proof that the exported CSV is byte-identical to the original KLE source.

## Explore the notebooks

Create a separate working copy before executing `DatabaseManagement.ipynb`: it drops and recreates tables in `CarSharing.db`. Both notebooks retain a historical absolute path to `CarSharing.csv`. The original course input was supplied through Keele's KLE and is not newly redistributed here because its external licence is unverified. You can use the backup export above as a clearly labelled reconstruction by changing the notebook input path to `CarSharing-extract.csv` in your working copy.

Use Jupyter in a virtual environment. Database exploration imports pandas; the complete analytics notebook also imports NumPy, scikit-learn, statsmodels, seaborn, matplotlib, pmdarima and TensorFlow. [The runbook](docs/ENGINEERING.md) explains sequencing, compatibility and why the saved model outputs are historical evidence rather than a freshly reproduced result.

The existing `web/` directory is a **2026 synthetic demonstration**, using small illustrative records. It does not query `CarSharing.db`, execute the notebooks or reproduce the assessed model results.

## Validation and provenance

The database inspector's two regression tests passed locally on 14 November 2026 after fixing a Windows test-fixture connection leak. They check read-only access, byte preservation, quoted table names, bounded export, refusal to overwrite output and missing-file behaviour. The actual supplied database was inspected successfully and contains 14 tables. Full notebook execution and model retraining were not performed in this review.

`original-work/DADB` and `original-work/Data-Analytics` preserve earlier repository snapshots with their import manifests; the migration archive is not native merged Git ancestry. The conference-booking analysis import is related historical learning material, not assessed car-sharing coursework. Current naming and documentation are dated 2026; academic work is from 2024. University briefs and third-party dataset rights remain with their owners.
