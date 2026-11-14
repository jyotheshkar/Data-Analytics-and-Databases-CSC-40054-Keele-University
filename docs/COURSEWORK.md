# Coursework evidence and source walkthrough

## Assessment context

Data Analytics and Databases was a 15-CATS Level 7 module in the 2023/24 MSc Computer Science programme. My verified overall module mark is 89%. The private official transcript establishes the mark; the coursework report alone does not. [Keele's 2023/24 module specification](https://www.keele.ac.uk/catalogue/2023-24/csc-40054.htm) describes a 50% written assignment and a 50% open-book examination. The stored briefs are requirements, not marked student submissions.

The coursework brief divides the assignment between database management and data analytics. It describes hourly demand with calendar and weather data, supplied as `CarSharing` through KLE. It requires SQL/sqlite3 for database tasks, with other tools allowed for analytics, importing and exporting. These are course constraints; the repository is an archive of my submitted approach and does not imply that every historical implementation choice was ideal.

## Evidence map

| Area | Code or document | What it demonstrates |
| --- | --- | --- |
| SQLite storage | `DatabaseManagement.ipynb` | Table creation, data import, backup, `ALTER TABLE`, `CASE` categorisation and relational decomposition |
| SQL querying | Same notebook and `CarSharing.db` | Aggregation, date extraction, weekday filtering, weather summaries and highest-demand queries |
| Preprocessing | `DataAnalytics.ipynb`, task 1 | Duplicate removal, mean/mode imputation and MinMax scaling |
| Statistical analysis | Tasks 2-3 | ANOVA, ordinary least squares, seasonal decomposition and autocorrelation |
| Forecasting | Tasks 4 and 6 | Weekly aggregation, stationarity testing, ARIMA selection and train/test comparison |
| Machine learning | Task 5 | Random-forest regression and a small TensorFlow dense neural network |
| Clustering | Task 7 | K-means and hierarchical clustering of temperature observations |
| Reporting | `docs/original/student-report-technical-text.md` | Historical technical narrative and code appendix, with redaction/format limitations documented |
| Later maintenance | `scripts/inspect_database.py` | Read-only schema inspection and bounded CSV export, separate from the assessed notebook |

## Database snapshot

The verified committed database is 5,124,096 bytes with SHA-256 `fb135952ce82f36ab51f414f815d226e8129a8feab594ffef4abc0fc565b2401`. Its schema inspection on 14 November 2026 found 14 tables. `CarSharingBackup` has 8,708 rows and 11 columns: `id`, `timestamp`, `season`, `holiday`, `workingday`, `weather`, `temp`, `temp_feel`, `humidity`, `windspeed`, `demand`. This is the retained pre-transformation backup within the coursework database.

`CarSharing` also has 8,708 rows but reflects later transformations. `temperature` contains the extracted temperature fields; `weather` is a weather-code lookup. Other tables store highest-demand, hourly, monthly, windspeed and humidity summaries. The backup enables a readable CSV reconstruction without rerunning mutating notebook cells, but it does not establish the original CSV's exact formatting or external data licence.

## Scientific interpretation and known limits

The analytics notebook fits imputation and scaling before later train/test splits. That can leak information from the test period. In particular, demand is scaled too, so an error reported after preprocessing is not automatically in original demand units. Its random split for regressors does not establish future-time forecasting performance. A decomposition period must match observation frequency; a fixed period of 365 on hourly rows is not an annual cycle.

Some printed findings are explicitly labelled hypothetical in the source notebook. Do not quote them as measured conclusions. Saved plots and scores belong to the historical run and were not regenerated in this maintenance review. A future experiment should use chronological holdouts, fit transformations only on training data, inverse-transform demand for interpretation and compare a seasonal or naive baseline.

## Authorship and later changes

This is my individual coursework report and notebooks. Imported `original-work/Data-Analytics` content concerns a separate conference-booking project, which had team contributions; it is retained as migration history rather than relabelled as this assignment.

The 2026 documentation update connects actual source to skills, adds a redacted report extract and records checked hashes. It also closes a SQLite fixture connection explicitly in the existing tests so Windows can remove its temporary database. No new model results, marks or original assignment code are invented. The `web/` illustration is a later teaching aid and is excluded from assessed-work claims.
