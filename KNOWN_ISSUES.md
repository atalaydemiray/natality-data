# Known source and interpretation issues

This alpha preserves source values. Independent scientific review and clinical harmonization remain pending.

- **IMP_PLUR, 2016 → 2017:** printed meanings of blank and 1 reverse. Whether this is a documentation correction or a processing change is unresolved. Do not automatically invert the flag or pool across this boundary.
- **MRACE6, 2014–2022:** the manual prints length 2 at position 107, while MRACE15 begins at 108. The conversion preserves byte 107 and records both the printed length and actual slice width. This is a layout discrepancy, not evidence of changed race categories.
- **2015 race codes:** 2,923 occurrence records (2,911 U.S. residents and 12 foreign residents) contain MRACE31=99, MRACE6=9, MRACE15=99 together. These combinations are not listed in the corresponding manual entries. Values remain literal; their meaning is not assigned or converted to NA. The validation reports distinguish this exception from a passing documented-domain check.
- **FILLER_F, 2015–2016:** byte 165 is labeled a father-education reporting flag despite its printed name. It is preserved as FILLER_F; genuine blank filler is excluded.
- **Reserved bytes, 2014–2015:** positions 328 and 338 contain values despite printed filler descriptions. The auxiliary natality_source_record column preserves each complete 1,345-byte source record. These positions have no inferred analytic meanings. The corrected annual dictionary distinguishes physical width from a printed field length.
- **Certificate and reporting changes:** 2014–2015 contain revised and unrevised certificate contexts. Matching column names does not establish comparability. Reporting flags, unknowns, applicability and annual quality guidance require study-specific decisions.

Consult the annual dictionaries, linked original manuals and validation reports. Literal blanks and sentinels remain source values. Unknown gestation has no determined term/preterm status. Data files contain occurrence records; population restrictions must be explicit.
