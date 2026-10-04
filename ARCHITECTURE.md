# Architecture

## Overview

HINAN NAVI uses an **offline-first** architecture.

The system is designed so that critical local functions can remain available without depending on a continuous remote connection.

## Major layers

### 1. Presentation layer

- map-first user interface
- evacuation / shelter workflows
- hazard controls
- training and replay interfaces
- historical archive search
- mobile / touch-oriented interaction

### 2. Local runtime layer

- locally served application assets
- local map access
- locally available route / shelter data where packaged
- replay and historical-disaster runtime
- fail-closed adapters for optional capabilities

### 3. Map / data layer

Large map and hazard assets are stored outside this GitHub repository.

The deployed system may use packaged vector-map data, hazard layers, shelter data, routing data, and other generated assets.

### 4. Live-information layer

Where network access is available, selected current information may be integrated into the application.

Live dependencies are treated as optional inputs rather than assumptions that must always succeed.

## Historical Disaster Archive architecture

The production archive uses two record classes:

- **BASE_M6** — 821 catalog-derived records
- **SPECIAL** — 4 special historical disaster records

The unified search namespace contains **825 records**.

BASE_M6 records open a read-only detail view.

SPECIAL records use dedicated schematic educational renderers.

The replay namespace and the general historical-search namespace remain logically distinct.

## Failure isolation

The project follows a fail-closed approach:

- optional subsystem failure should not corrupt the base application
- unknown records should not be coerced into a replay type
- missing data should not be silently invented
- unsupported historical geometry should not be inferred as fact

## Deployment model

Canonical production:

`https://wakouzan-kichijoji.com/hinan-navi/`

Current production deployment is hosted separately from this GitHub repository.

See [docs/deployment.md](docs/deployment.md).
