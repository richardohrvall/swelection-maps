# AGENTS.md

## Project purpose

This repository contains reproducible workflows for processing, cleaning,
harmonising, and mapping Swedish election geographies and election results.

The immediate priority is the 2026 election. Later stages will extend the
workflow to earlier elections and develop crosswalks between election districts
over time and to other small-area geographies such as DeSO.

## Main principles

- Use R as the primary language.
- Prefer `sf`, `dplyr`, `purrr`, `stringr`, `here`, and related tidyverse tools.
- Use the native R pipe `|>`.
- Prefer modern dplyr syntax.
- Keep code readable and modular.
- Reusable functions should go in `R/`.
- Exploratory and diagnostic work should go in `analysis/` as Quarto `.qmd` files.
- Generated outputs should go in `output/` or `data/processed/`, not in `data/raw/`.

## Raw data

Treat everything under `data/raw/` as immutable source material.

Never:
- overwrite raw files
- modify raw GIS geometries
- rename source files unnecessarily
- delete raw files
- use manually clipped legacy files as substitutes for originals

Files containing `klippt` in their filename are older manually processed versions
and should not be treated as authoritative source files.

## GIS workflow

- Preserve original CRS information.
- For standardised processing, prefer SWEREF 99 TM (EPSG:3006).
- Prefer GeoPackage for processed GIS data.
- Do not convert or clean GIS files unless the task explicitly asks for it.
- Keep analytical geometries separate from cartographic/map geometries.
- Do not simplify geometries unless explicitly requested.
- When cleaning topology, diagnose problems before applying automated fixes.
- Do not remove small polygons solely based on area without checking whether they
  may represent real islands or other legitimate geography.

## Election geographies

Relevant geography types include:
- election districts (valdistrikt)
- municipal constituencies (kommunvalkretsar)
- regional constituencies (landstings-/regionvalkretsar)
- parliamentary constituencies (riksdagsvalkretsar)

For 2026, the nationwide election-district file should be treated as the primary
source. County-specific files are secondary/reference material.

## Longitudinal work

A later project stage will create crosswalks between election districts over time
and to DeSO or other fixed geographies.

Therefore:
- always preserve original district identifiers
- preserve election year and election type
- retain official comparability information where available
- avoid transformations that would make later spatial crosswalks harder to audit

## Safety

Before moving many files or making structural changes:
1. inspect the current directory structure
2. report the proposed changes
3. preserve uncertain files rather than guessing
4. use an `unclassified/` folder when classification is unclear

Do not include passwords, API keys, credentials, or absolute local paths in
version-controlled files.