# Natality source-access alpha, 2000–2024

Led by Dr. Atalay Demiray. Independent project.

This release adds 14 annual Parquets for 2000–2013 to the unchanged 2014–2024 release. The composite `data-manifest.json` pins all 25 files and their release URLs. Native dictionaries and validation bundles distinguish original-code preservation from clinical review. Read `DATA_USE.md` and `KNOWN_ISSUES.md` before analysis.

The installable **natality 0.5.0.9007** R source package supports automatic downloads for 2000–2024. It is an alpha, not a CRAN release or independently reviewed harmonization. The 2025 archive is discoverable but has not been processed because annual layout authority is pending. Clinical graph holds for 2000–2010 remain.

## Download files

- [2000–2013 data and the R package](https://github.com/atalaydemiray/natality-data/releases/tag/source-v1-historical-alpha)
- [2014–2024 data](https://github.com/atalaydemiray/natality-data/releases/tag/source-v1-alpha)

Together these releases contain 98,919,648 occurrence records in 25 annual Parquet files (5.25 GB in total). The new release contains a composite manifest for all 25 years. The 2014–2024 files retain their original identities and URLs.

## Install and read

```r
install.packages(c("digest", "jsonlite", "arrow"))
install.packages(
  "https://github.com/atalaydemiray/natality-data/releases/download/source-v1-historical-alpha/natality_0.5.0.9007.tar.gz",
  repos = NULL, type = "source"
)
library(natality)
natality_years(details = TRUE)
natality_codebook("DMAGE", years = 2000)
births <- read_natality(
  2000, vars = c("DMAGE", "BIRMON"), population = "us_residents"
)
# Reuse the verified download offline.
births <- read_natality(
  2000, vars = c("DMAGE", "BIRMON"),
  population = "us_residents", download = FALSE
)
```

Use the annual dictionary before changing fields or pooling years; `DMAGE` is the native 2000 age field. The first read downloads the complete annual Parquet, then reads only selected columns. `natality_cache_clear(2000)` removes its local cache copy when space is needed; subsequent reads must download it again. Keep original cloud backups outside a disposable cache.

Direct Arrow, SQL and Python reads can use the same Parquets. Verify the SHA-256 in `SHA256SUMS.txt`. Each historical dictionary includes native field names, byte positions, manual references, known issues and pending review status. Original records represent births, not unique mothers. `RESTATUS` codes 1–3 select U.S.-resident births. Unknown, nonreporting and out-of-range values are not interchangeable.

## Limits and reporting issues

Historical gestation measures remain distinct. Do not fill gaps by substituting computed/LMP gestation for modern obstetric estimate. The original 2005 file retains its Vermont undercoverage warning. The 2009/2010 supplemental mappings remain unapproved, and the 2010 clinical comparison discrepancy remains unresolved. The literal 2000 `DRINK` value `"9 "` is preserved with a warning; its meaning is not inferred.

Report reproducible problems through the [project issue tracker](https://github.com/atalaydemiray/natality-data/issues), identifying the year, field, release and aggregate evidence. Do not attach individual records or credentials. Cite CDC/NCHS annual data and the exact software version separately. No DOI or independent scientific approval is claimed.

## Validation, citation and preservation

The release check downloaded all 25 annual files without GitHub authentication and verified their hashes, occurrence and resident counts, all recorded maternal-age and birth-month counts, and offline reuse through natality 0.5.0.9007. Annual dictionaries and validation bundles document the scope of each check. Source preservation does not establish clinical comparability. The Atlas website remains in private development; this repository provides public data and the installable R package.

Follow [DATA_USE.md](DATA_USE.md) and the [NCHS Data User Agreement](https://www.cdc.gov/nchs/policy/data-user-agreement.html). Cite the NCHS source years and the exact release and software version used; `natality_cite(2000:2024)` supplies separate source and software entries.

Corrections require a new release with a changelog. The historical release and its assets are immutable. GitHub is the configured public host; verified cached files remain usable during an outage, while new downloads require GitHub access. Private project backups are archived separately in iCloud. Zenodo and a separate backup disk remain deferred.
