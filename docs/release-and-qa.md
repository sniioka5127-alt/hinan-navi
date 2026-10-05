# Release and QA

This document is the authoritative public evidence summary for HINAN NAVI release verification.

README summarizes the status. SAFETY.md explains the safety meaning of the status. Detailed verification facts belong here so that counts, gates, and unresolved items do not diverge across documents.

## Release philosophy

Passed artifacts are treated as immutable.

A defect discovered after a gate creates a new revision rather than mutating the already-recorded artifact in place.

Verification is separated into:

1. **Core Safety** — map / hazard / shelter / routing / warning integration and the evacuation-support path.
2. **Historical / Training** — replay, archive, search, and educational presentation.

Passing the Historical / Training layer does not close unresolved Core Safety field-validation work.

## Status vocabulary

- `PASS_CLOSED` — the stated gate has passed for the stated environment and scope.
- `PASS_CLOSED_PRODUCTION` — the stated production-facing feature / behavior has passed its defined closure checks.
- `PENDING` — required verification remains outstanding.
- `NOT_RUN` — the stated environment or test was not executed.

A PASS status must always be read together with its environment and scope.

## Core Safety evidence matrix

| Area | Evidence | Status | Boundary |
| --- | --- | --- | --- |
| NAV-01 browser / integration gate | R25-R1 startup-budget-aligned integration gate | `PASS_CLOSED` | Browser / integration scope |
| NAV-01 repeatability | 3 passes, 0 failures | `3 / 3 PASS` | Browser cold-profile repeatability |
| Background map package | national PMTiles pinned; Range delivery verified in QA | `PASS` | Pack / HTTP path |
| Hazard static routes | 82 routes materialized / verified | `82 VERIFIED` | Static hazard data path |
| Routing graph | 2,150 graph tiles verified against manifest bytes / SHA-256 | `2,150 VERIFIED` | Static routing graph integrity |
| Shelter data | 295 occupied shelter cells verified against manifest bytes / SHA-256 | `295 VERIFIED` | Static shelter-data integrity |
| Android Emulator packaging / launch | APKS install + cold start | `PASS_CLOSED` | Android Emulator only |
| Real JMA transport on Android Emulator | Aomori City: 59 selected / 59 scanned / 0 scan errors | `PASS` | Android Emulator + real JMA network |
| Physical Android device | Not executed | `NOT_RUN` | No physical Android device evidence |
| Real GPS field QA | Required by NAV-01 gate, not executed | `PENDING` | No real-world GPS / field closure |

### NAV-01 browser gate

The recorded R25-R1 result is:

```text
R25_CLASSIFICATION=PASS_REPEATABLE_AFTER_STARTUP_BUDGET_ALIGNMENT
R25_PASS_COUNT=3
R25_FAIL_COUNT=0
R25_BROWSER_GATE=PASS_CLOSED
R25_FINAL_STATUS=IMPLEMENTED_PENDING_REAL_GPS_FIELD_QA
```

This closes the browser / integration gate. It does **not** close real GPS field validation.

### Static Core Safety asset closure

The deployment-pack evidence verified:

```text
Hazard static routes     82
Routing graph tiles    2150
Shelter cells           295
```

The routing and shelter sets were checked against their manifests for expected bytes and SHA-256 values. Hazard routes were checked for source / destination identity in the deployment-pack evidence.

These are integrity and availability checks. They are not claims that every route or shelter is safe in a real disaster.

### Android Emulator and JMA integration

Recorded Android Emulator QA includes:

```text
INSTALL_APKS=PASS
COLD_START=PASS
REAL_JMA_CANDIDATE_COUNT=59
REAL_JMA_SELECTED_COUNT=59
REAL_JMA_SCANNED_COUNT=59
REAL_JMA_SCAN_ERROR_COUNT=0
REAL_JMA_TRANSPORT_ANDROID_QA=PASS
JMA_TO_COMMON_ENGINE_ANDROID_QA=PASS
REAL_JMA_LIVE_BINDING_QA=PASS
05F_FINAL=PASS_CLOSED_JMA_LIVE_INTEGRATION_ANDROID_EMULATOR
REAL_DEVICE_QA=NOT_RUN
```

The recorded result is specifically an **Android Emulator** result. It must not be described as physical Android device validation.

## Explicitly unresolved Core Safety verification

The following remain open:

```text
REAL_GPS_FIELD_QA=PENDING
PHYSICAL_ANDROID_DEVICE_QA=NOT_RUN
```

Until those are executed, the project must not claim complete physical-device / real-world GPS validation.

The project also does not claim:

- guaranteed safe route
- guaranteed safe shelter
- no hazard data means safe
- straight-line connector as an evacuation route

## Historical / Training layer

Historical Disaster Archive status is tracked separately from Core Safety.

Current production historical namespace:

```text
BASE_M6                    821
Special Historical           4
Unified Search              825
Historical Archive QA       PASS_CLOSED
Historical Archive I18N     PASS_CLOSED_PRODUCTION
```

### Historical behavior verified

The tested Historical Archive behavior includes:

- BASE_M6 result present
- BASE_M6 opens read-only detail
- BASE_M6 does not dispatch as replay
- Special Historical results render through the dedicated educational path
- four Special Historical records are present
- Special Historical replay controls are suppressed where not applicable
- restoration back to base state
- production search / preset UX
- English / Japanese Historical Archive I18N production verification

Special Historical content remains **schematic educational** and does not claim clock-accurate reconstruction or exact historical disaster geometry.

## Production deployment evidence

Earlier Historical Archive production promotion used local Real Edge QA, human visual review, Hostinger smoke verification, and byte-for-byte verification of the then-current release delta.

That earlier delta record must not be read as a permanent statement that every later production revision is still represented by the same changed-file count. Subsequent repairs and I18N revisions are separate revisions and must be evaluated by their own evidence.

## Evidence authority

When documentation conflicts:

1. the underlying audit artifact / immutable QA evidence takes precedence;
2. this file is the authoritative public summary;
3. README is a concise project-level summary;
4. SAFETY.md defines safety interpretation and prohibited claims.

This structure is intended to keep verified facts, unresolved work, and user-facing safety language aligned.
