# Data layout

Data are grouped first by provider and then, where relevant, by election year.
Source filenames and file contents are preserved, while directory structure may 
be organised for clarity, so that later processing and longitudinal crosswalks 
remain auditable.

### Data providers and roles

The project uses geodata from three main providers with different roles:

- **Valmyndigheten** is the authoritative source for election-specific
  geographies, including election districts and constituencies. These files
  define the electoral units used in the analyses.
- **Lantmäteriet** provides reference geodata used for geometric validation and
  cartographic processing. In particular, Topografi 50 is used for consistent
  coastlines, lakes, and larger watercourses, while Kommun, län och rike may be
  used as a reference for administrative boundaries.
- **Statistics Sweden (SCB)** provides generalised municipal and county
  geometries suitable for thematic maps of aggregated election results.

Reference data from Lantmäteriet or SCB must not be used to redefine
Valmyndigheten's election districts. Where cartographic versions of election
geographies are created, they should be stored separately from the source or
analytical geometries.

## Raw data

Everything below `data/raw/` is immutable source material. Do not overwrite,
rename, clean, simplify, or otherwise modify files in place. Write derived data
to `data/processed/` and analytical or diagnostic outputs to `output/`.

Valmyndigheten material is stored under `data/raw/valmyndigheten/` using these
categories inside each year:

- `geodata/<geography>/`: election geography source files, retaining the
  provider's original file or directory name.
- `geodata/valdistrikt/nationwide/`: nationwide election-district sources.
- `geodata/valdistrikt/county/`: county-specific election-district sources.
- `comparability/`: official or historical district-change and mapping tables.
- `reference-tables/`: non-spatial tables that describe the geography.
- `supplementary/`: related official material, such as polling-place data.
- `legacy-cartography/`: older clipped geometries and map-project artifacts.
  These files are preserved for provenance but are not authoritative sources.
- `unclassified/`: files whose provenance or processing status is uncertain.
  Preserve them, but do not use them as authoritative inputs without first
  establishing their provenance.

Provider-wide documentation that is not specific to one election year is under
`data/raw/valmyndigheten/documentation/`.

## 2026 priority sources

The primary nationwide 2026 election-district source is:

`data/raw/valmyndigheten/2026/geodata/valdistrikt/nationwide/valdistrikt-riket-2026.zip`

The county ZIP files under the adjacent `county/` directory are secondary
reference material. The nationwide district table is under `reference-tables/`,
and the preliminary 2022--2026 comparison is under `comparability/`.

## Legacy and uncertain files

Files with `klippt` in their names are manually processed legacy versions and
must not substitute for the original geometries. R histories, scripts, R
objects, and loose derived geometry sets found alongside the 2022 and 2024
downloads have been retained under `unclassified/local-working-files/` rather
than treated as Valmyndigheten source data.
