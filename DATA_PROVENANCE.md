# Data Provenance

## Purpose

This document records the project's data-handling policy.

It is not yet an exhaustive per-file source manifest.

## Data classes

HINAN NAVI works with several classes of information:

- map data
- administrative boundaries / identifiers
- shelter information
- hazard information
- warning / alert information
- routing data
- historical disaster records
- generated educational renderings

Each source class may have different attribution, redistribution, transformation, and update requirements.

## Historical Disaster Archive

### BASE_M6

The current BASE_M6 collection contains **821 catalog-derived earthquake records**.

The project preserves catalog-style fields and presents these records as read-only historical detail.

### Special Historical

The current special set contains four historical cases:

- 864–866 Fuji / Jōgan eruption
- 887 Ninna earthquake
- 1707 Hōei earthquake
- 1707 Fuji / Hōei eruption

Their visual output is explicitly classified as **schematic educational**.

## Live / current information

Where the application integrates live warning information, the source and retrieval path should be recorded in the relevant build / deployment evidence.

The project has used Japan Meteorological Agency data in live-warning integration work.

## Transformation policy

Transforming public data for offline use does not change the original source's authority or licensing conditions.

Derived artifacts should retain enough provenance to answer:

- where the source came from
- when it was obtained
- how it was transformed
- which version / hash entered the release
- what claims the transformed artifact is allowed to support

## Large artifacts

Large generated map packs, hazard packs, routing graphs, and audit evidence are maintained outside this GitHub repository.

GitHub documents the architecture and release state; archival storage holds the large canonical artifacts.
