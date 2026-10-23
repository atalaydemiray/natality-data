# Natality source-access alpha, 2000–2024

Led by Dr. Atalay Demiray. Independent project.

This release adds 14 annual Parquets for 2000–2013 to the unchanged 2014–2024 release. The composite `data-manifest.json` pins all 25 files and their release URLs. Native dictionaries and validation bundles distinguish original-code preservation from clinical review. Read `DATA_USE.md` and `KNOWN_ISSUES.md` before analysis.

The installable **natality 0.7.0** R source package supports automatic downloads for 2000–2024. It is an alpha, not a CRAN release or independently reviewed harmonization. The 2025 archive is discoverable but has not been processed because annual layout authority is pending. Historical record-based clinical holds for 2000–2010 remain. The Atlas separately identifies published historical reference series.

The [0.6.0 software update](https://github.com/atalaydemiray/natality-data/releases/tag/natality-r-0.6.0-alpha) adds opt-in `standardize_natality()` for eight core concepts, with original columns and rows preserved, explicit missing-value statuses, and interval bounds for grouped ages. It retains all 4,143 classified historical comparisons and 132 unresolved decisions. The dictionary covers 714 artifact-column identities and 6,218 annual entries. The known v1 `F_MM_` naming exception remains disclosed. This is a research alpha, not fully validated harmonization; no generic gestation transformation is supplied. Existing annual artifacts are unchanged.

The [0.6.1 update](https://github.com/atalaydemiray/natality-data/releases/tag/natality-r-0.6.1-alpha) adds `natality_concepts()` and the explicit `gestational_diabetes` transformation. The native field is `RF_GEST` in 2004–2013 and `RF_GDIAB` in 2014–2024; the reporting flag retains its name. Annual reporting and historical certificate eligibility are required. Generic combined diabetes is never substituted. Prepregnancy diabetes has family discovery, not a new transformation. Reporting coverage changes across years, so this does not establish nationally comparable prevalence.

The [0.7.0 update](https://github.com/atalaydemiray/natality-data/releases/tag/natality-r-0.7.0-alpha) extends concept discovery to all 6,218 annual source fields: 519 families, 24 chronological boundaries and 6,518 comparisons. Use `natality_crosswalk()` and `natality_transitions()` to inspect annual fields, rules and source evidence. `align_natality()` preserves literal annual codes under a common concept identifier; it does not authorize common clinical values, population filters or pooling. It keeps multiple source variants explicit and separates reused names such as the historical TOBUSE reporting flag versus the later tobacco-use item. The catalog retains 1,485 reporting associations with their scope, 134 unresolved source comparisons and 80 unresolved annual reporting references. The latter two counts are different measures, not a unique-issue total.

## Download files

- [2000–2013 data and the original R package](https://github.com/atalaydemiray/natality-data/releases/tag/source-v1-historical-alpha)
- [2014–2024 data](https://github.com/atalaydemiray/natality-data/releases/tag/source-v1-alpha)

Together these releases contain 98,919,648 occurrence records in 25 annual Parquet files (5.25 GB in total). The new release contains a composite manifest for all 25 years. The 2014–2024 files retain their original identities and URLs.

## Install and read

```r
install.packages(c("digest", "jsonlite", "arrow"))
install.packages(
  "https://github.com/atalaydemiray/natality-data/releases/download/natality-r-0.7.0-alpha/natality_0.7.0.tar.gz",
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

## Optional core standardization

```r
x <- read_natality(2024, vars = c("DBWT", "MAGER"), population = "us_residents")
z <- standardize_natality(x, 2024,
  concepts = c("birthweight", "low_birthweight", "maternal_age"))
table(z$nat_birthweight_status, useNA = "ifany")
```

Source columns and provenance remain intact. New `nat_*` columns carry explicit status fields. Grouped age endpoints remain intervals; undocumented historical codes are not assigned an invented meaning. See `?standardize_natality` for the annual scope and limitations.

## Limits and reporting issues

Historical gestation measures remain distinct. Do not fill gaps by substituting computed/LMP gestation for modern obstetric estimate. The original 2005 file retains its Vermont undercoverage warning. The 2009/2010 supplemental mappings remain unapproved, and the 2010 clinical comparison discrepancy remains unresolved. The literal 2000 `DRINK` value `"9 "` is preserved with a warning; its meaning is not inferred.

Report reproducible problems through the [project issue tracker](https://github.com/atalaydemiray/natality-data/issues), identifying the year, field, release and aggregate evidence. Do not attach individual records or credentials. Cite CDC/NCHS annual data and the exact software version separately. No DOI or independent scientific approval is claimed.

## Validation, citation and preservation

The release check downloaded all 25 annual files without GitHub authentication and verified their hashes, occurrence and resident counts, all recorded maternal-age and birth-month counts, and offline reuse through natality 0.5.0.9007. Annual dictionaries and validation bundles document the scope of each check. Source preservation does not establish clinical comparability. The [Natality Atlas](https://atalaydemiray.com/natality-atlas/) is public; its source repository remains private. This repository provides public data and the installable R package.

The exact publicly downloaded 0.6.0 package also passed isolated installation and a 2024 resident-data check: original fields/provenance and all monthly counts matched, with 308,966 low-birthweight births among 3,625,941 records with known birthweight. Local R CMD check returned Status: OK with 987 passing expectations. These internal checks do not replace external scientific reproduction.

The 0.6.1 package passed R CMD check with 1,524 expectations. All five release assets were anonymously verified. Actual-data checks covered 2004, 2013, 2014 and 2024 using the same R/catalog payload as the final tarball, matching every derived value to a separate raw-code calculation while preserving original columns. See its release evidence for exact artifact identities and scope. External scientific review remains pending.

The exact 0.7.0 source package passed local R CMD check and 2,059 assertions. Its installed API passed synthetic checks for all 519 families and 6,218 annual native variants, including explicit reporting-reference warnings. All five release assets were anonymously downloaded and verified. Annual data files are unchanged; these software checks do not replace external scientific reproduction.

Follow [DATA_USE.md](DATA_USE.md) and the [NCHS Data User Agreement](https://www.cdc.gov/nchs/policy/data-user-agreement.html). Cite the NCHS source years and the exact release and software version used; `natality_cite(2000:2024)` supplies separate source and software entries.

Corrections require a new release with a changelog. The historical release and its assets are immutable. GitHub is the configured public host; verified cached files remain usable during an outage, while new downloads require GitHub access. Private project backups are archived separately in iCloud. Zenodo and a separate backup disk remain deferred.
