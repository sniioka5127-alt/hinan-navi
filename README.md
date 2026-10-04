# HINAN NAVI — Offline Disaster Preparedness & Evacuation Navigation for Japan

**HINAN NAVI（避難ナビ）** is an offline-first disaster preparedness and evacuation-support project for Japan.

Its purpose is simple:

> Help people make safer decisions when networks are congested, unavailable, or unreliable.

Public application:  
https://wakouzan-kichijoji.com/hinan-navi/

---

## Mission

Disaster-support software should remain useful when the conditions are worst.

HINAN NAVI is designed around that principle:

- offline-first operation
- local map availability
- evacuation-support workflows
- hazard-context display
- historical disaster learning
- fail-closed behavior when a dependency is unavailable
- clear separation between verified data and illustrative / educational presentation

This project is intended to support preparedness and evacuation decisions. It is **not an official government service** and does not replace instructions from public authorities, emergency services, municipalities, the Japan Meteorological Agency, or other official sources.

---

## Current capability areas

The project includes work across:

- offline vector maps
- evacuation shelter navigation
- offline walking-route support
- GPS / rerouting integration
- hazard-layer integration
- live warning integration
- training / replay workflows
- historical disaster archive and search
- family communication support
- Android packaging / WebView delivery
- web / PWA deployment

Large map and hazard datasets are intentionally kept outside this GitHub repository.

---

## Historical Disaster Archive

The current production release includes a unified historical-disaster search namespace:

- **BASE_M6 catalog records:** 821
- **Special historical records:** 4
- **Unified search namespace:** 825

### BASE_M6

BASE_M6 records are catalog-derived historical earthquake records.

They are displayed as **read-only catalog detail** and are **not dispatched as replay scenarios**.

### Special historical records

The current special historical set contains:

1. **864–866 — Fuji / Jōgan eruption**
2. **887 — Ninna earthquake**
3. **1707 — Hōei earthquake**
4. **1707 — Fuji / Hōei eruption**

These records use a **schematic educational renderer**.

Important boundaries:

- not clock-accurate replay
- no claim of exact historical geometry
- no automatic georeferenced disaster-extent inference
- modern administrative codes, where used, are search / reference aids rather than claims about historical jurisdiction

---

## Release verification

The current production release was closed only after:

- static integration QA
- real Microsoft Edge browser QA
- human visual review
- BASE_M6 read-only / no-replay verification
- Special Historical 4-of-4 rendering verification
- base restore verification
- production activation / query-backdoor negative QA
- local canonical-production verification
- Hostinger remote smoke verification
- byte-for-byte remote SHA-256 verification of the 19-file production delta

Current release state:

```text
Historical Disaster Archive
BASE_M6                         821
Special Historical               4
Unified Search                  825

Local Real Edge QA              PASS_CLOSED
Human Visual QA                 PASS_CLOSED
Hostinger Remote Smoke          PASS_CLOSED
Remote deployment file identity 19 / 19 SHA256 MATCH
Release                         PASS_CLOSED
```

See [docs/release-and-qa.md](docs/release-and-qa.md) and [releases/v1.0.0.md](releases/v1.0.0.md).

---

## Repository role

This repository is a **public project record and technical documentation repository**.

It is intended to make the project's:

- goals
- architecture
- safety boundaries
- data provenance
- release evidence
- implementation decisions

understandable to researchers, developers, public-sector reviewers, disaster-preparedness practitioners, and interested users.

It is **not** the canonical storage location for multi-gigabyte map, hazard, audit, or build artifacts.

---

## Storage / deployment model

### Production

Public production application:

https://wakouzan-kichijoji.com/hinan-navi/

### Large canonical artifacts

Large data packs, generated maps, audit evidence, and release artifacts are maintained separately from GitHub.

This separation is deliberate:

- GitHub → source-facing documentation, architecture, public history
- production host → deployed web application
- archival storage → large generated datasets, evidence, release packages

---

## Documentation

- [Project identity](PROJECT_IDENTITY.md)
- [Architecture](ARCHITECTURE.md)
- [Safety model](SAFETY.md)
- [Data provenance](DATA_PROVENANCE.md)
- [Historical Disaster Archive](docs/historical-disaster-archive.md)
- [Offline-first design](docs/offline-first-design.md)
- [Hazard architecture](docs/hazard-architecture.md)
- [Evacuation routing](docs/evacuation-routing.md)
- [Replay engine](docs/replay-engine.md)
- [Release and QA](docs/release-and-qa.md)
- [Deployment](docs/deployment.md)
- [Changelog](CHANGELOG.md)

---

## Project principles

1. **Human life comes before feature count.**
2. **Offline capability is a safety requirement, not a convenience.**
3. **Unknown or unverified information must not be presented as fact.**
4. **Historical reconstruction must clearly distinguish evidence from illustration.**
5. **A failed dependency should fail closed rather than fabricate certainty.**
6. **Passed release artifacts are immutable; fixes create new revisions.**
7. **Deployment should be reproducible and auditable.**

---

## Maintainer

**Niioka Shoshin / 新岡 昌心 / SHOSHIN**

GitHub:  
https://github.com/sniioka5127-alt

Related public work:

- ZEN LAMP PROJECT — https://zen-lamp.com/
- HIRAKU — https://zen-lamp.com/hiraku/
- Wakouzan Kichijoji / Yasuragi Kannondo — https://wakouzan-kichijoji.com/

---

## License

No repository-wide license has been declared yet.

This is intentional while the project separates:

- original application code
- third-party libraries
- public-sector / official source data
- generated or transformed map / hazard assets

Do not assume that every dataset or asset referenced by this project has the same reuse conditions.
