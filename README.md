# Natality Atlas data

Led by Dr. Atalay Demiray · Independent project.

Versioned, source-preserving Parquet copies of CDC/NCHS public-use U.S. natality data for 2014–2024. Free access for statistical research.

**Source-access alpha. Independent scientific review and clinical harmonization remain pending.** These files preserve original source values, including unresolved documentation discrepancies. They do not supply automatically harmonized analytic variables.

## Download

Open the [source-v1-alpha release](https://github.com/atalaydemiray/natality-data/releases/tag/source-v1-alpha). Download the annual Parquet file and its matching dictionary. Each year also has a validation report and R-to-Atlas reconciliation report. The release manifest records exact source URLs, versions, sizes and checksums.

The eleven files contain 41,576,190 occurrence records and occupy approximately 1.60 GiB in total. Each annual file is approximately 109–315 MiB. Source codes remain character strings, including blanks, leading zeros and unknown codes. Births to foreign residents are included in the occurrence population; use RESTATUS 1–3 for the U.S.-resident population.

## Read directly in R

```r
# Install arrow separately if needed: install.packages("arrow")
base <- "https://github.com/atalaydemiray/natality-data/releases/download/source-v1-alpha/"
file <- "natality_2024_source_v1.parquet"
options(timeout = max(600, getOption("timeout")))
download.file(paste0(base, file), file, mode = "wb")
# Compare the downloaded SHA-256 with SHA256SUMS.txt before use.
births <- arrow::read_parquet(file, col_select = c("MAGER", "OEGest_Comb", "DBWT", "RESTATUS"))
```

The developing `natality` R package adds verified caching, codebook discovery and guarded reads. Its source repository and Atlas website remain in private development; this repository distributes the public data assets. CRAN distribution is a later step.

## Scientific scope

Local tests cover complete source-field preservation, record framing, selected official population controls and 1,661 R-to-Atlas checks. They do not establish exhaustive code-domain validity, measurement comparability, or independent scientific approval. Read KNOWN_ISSUES.md and the annual dictionary and reports before analysis. In particular, the IMP_PLUR 2016/2017 printed reversal is unresolved; the 2015 source contains unlisted race-code combinations; 2014–2015 preserve unexplained reserved bytes in an auxiliary full-record column. Modern public-use records have no state or county identifiers.

## Source, use and citation

Source: CDC, National Center for Health Statistics, National Vital Statistics System. [Original natality files](https://ftp.cdc.gov/pub/Health_Statistics/NCHS/Datasets/DVS/natality/) are also available from NCHS without charge. These independent conversions are not endorsed by CDC, HHS or the U.S. Government.

Follow the [NCHS Data User Agreement](https://www.cdc.gov/nchs/policy/data-user-agreement.html) and [DATA_USE.md](DATA_USE.md). Cite NCHS for each source year, plus: Demiray A. Natality Atlas data: U.S. natality source-preserving Parquet files, 2014–2024. source-v1-alpha (2026). https://github.com/atalaydemiray/natality-data/releases/tag/source-v1-alpha. No DOI has been assigned.

## Corrections and preservation

Report reproducible issues through this repository's Issues tab without posting individual records. Include year, variable, release and an aggregate description. Existing data assets will not be silently replaced: corrections require a new version with a changelog. Source preservation and scientific review statuses are reported separately.

GitHub is the only configured public host. Zenodo and an independent backup disk are deferred. Existing verified local copies continue working during a GitHub outage; new downloads require GitHub to be available. Original ZIPs and manuals are retained locally by the project and are not included in this release.
