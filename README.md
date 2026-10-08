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

## Core Safety verification

Core Safety is the highest-priority verification layer. Historical / training features are tracked separately and do not substitute for evacuation-path verification.

Current evidence status:

```text
NAV-01 browser / integration gate        PASS_CLOSED
NAV-01 repeatability                     3 / 3 PASS
Android Emulator integration             PASS_CLOSED
Android Emulator cold start              PASS
Real JMA scan (Aomori City)              59 / 59, errors 0
Hazard static routes                     82 verified
Routing graph tiles                      2,150 verified
Shelter static cells                     295 verified
Family-contact SMS production            PASS_CLOSED
iOS Safari SMS handoff                   PROVEN
iOS PWA SMS handoff                      PROVEN

Not yet verified
Real GPS field QA                        PENDING
Physical Android device QA               NOT_RUN
Android real-device SMS handoff          DEFERRED_NO_ANDROID_REAL_DEVICE
```

These results mean that the browser / emulator integration path and packaged Core Safety assets have passed the recorded gates. They do **not** mean that a physical Android device or real-world GPS field behavior has been validated.

The project therefore does not claim that any generated route or shelter is guaranteed safe.

The detailed evidence matrix and status definitions are maintained in [docs/release-and-qa.md](docs/release-and-qa.md), which is the authoritative release-evidence record.

---

## Family communication / SMS

Production family-contact SMS support is now verified for the web / PWA path.

Current recorded status:

```text
V01-NAT-FAMILY-CONTACT-SMS-03             PASS_CLOSED
iOS Safari real-device SMS handoff        PROVEN
iOS PWA real-device SMS handoff           PROVEN
Android real-device SMS handoff           DEFERRED_NO_ANDROID_REAL_DEVICE
```

The implemented safety contract is:

- 1–3 family contacts
- contact name and phone number stored by the application in browser-local storage
- 119 / 110 are kept separate from family contacts
- one contact may be selected automatically; multiple contacts require explicit recipient selection
- five fixed evacuation-status messages
- existing UI05 location is reused; the SMS flow does not start a new GPS acquisition
- if no UI05 location is available, the message uses `現在地：未取得`
- the application creates the message and opens the OS SMS composer
- the application does **not** send SMS automatically; final send remains a user action

Real-device iPhone testing verified the handoff in both Safari and the installed home-screen PWA, including recipient prefill, message body transfer, and the no-auto-send boundary.

During Windows / Edge QA, Kaspersky endpoint-security injection was observed inspecting form content. This was classified separately from application transport: blocking application-origin contact-data exfiltration remained zero. Accordingly, “local-only” is an **application-boundary** claim and is not a claim that browser extensions or endpoint-security software cannot inspect page content.

This iOS evidence does not close the still-unrun physical Android or real-world GPS field-validation work.

See [the family-contact SMS release record](releases/2026-10-08-family-contact-sms.md) and [docs/release-and-qa.md](docs/release-and-qa.md) for the evidence boundary.

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

Historical Archive / training verification is tracked as a separate upper-layer release concern. It does not close the remaining real-device / real-GPS Core Safety gaps.

---

## Release verification

Current high-level state:

```text
Core Safety
NAV-01 Browser Gate                    PASS_CLOSED
Android Emulator Integration           PASS_CLOSED
Real GPS Field QA                      PENDING
Physical Android Device QA             NOT_RUN

Historical / Training Layer
BASE_M6                                821
Special Historical                      4
Unified Search                         825
Historical Archive QA                  PASS_CLOSED
Historical Archive I18N                PASS_CLOSED_PRODUCTION

Family Communication Layer
Family-contact SMS production          PASS_CLOSED
iOS Safari SMS handoff                 PROVEN
iOS PWA SMS handoff                    PROVEN
Android real-device SMS handoff        DEFERRED_NO_ANDROID_REAL_DEVICE
```

Earlier Historical Archive deployment evidence included local Real Edge QA, human visual QA, Hostinger smoke verification, and byte-identity checks for the release delta. Later production repairs and I18N revisions are tracked as subsequent revisions rather than being collapsed into that earlier delta statement.

See [docs/release-and-qa.md](docs/release-and-qa.md) for the authoritative evidence matrix and [releases/v1.0.0.md](releases/v1.0.0.md) for the Historical Disaster Archive release record.

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
