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
- `DEFERRED_NO_ANDROID_REAL_DEVICE` — Android real-device verification is intentionally deferred because no physical Android device was available; this is not a product-failure classification.

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
| Family-contact SMS production | V01-NAT-FAMILY-CONTACT-SMS-03 production promotion + Real Edge verification | `PASS_CLOSED` | Production web / PWA application boundary |
| iOS Safari SMS handoff | Human-observed real-device handoff with recipient + body prefill and no auto-send | `PROVEN` | iPhone Safari only |
| iOS PWA SMS handoff | Human-observed real-device handoff from installed home-screen PWA | `PROVEN` | iPhone PWA only |
| Android real-device SMS handoff | No physical Android device available | `DEFERRED_NO_ANDROID_REAL_DEVICE` | Android OS handoff not yet proven |
| Physical Android device | Not executed | `NOT_RUN` | No broader physical Android device evidence |
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
ANDROID_REAL_DEVICE_SMS_HANDOFF=DEFERRED_NO_ANDROID_REAL_DEVICE
```

Until those are executed, the project must not claim complete physical-device / real-world GPS validation.

The project also does not claim:

- guaranteed safe route
- guaranteed safe shelter
- no hazard data means safe
- straight-line connector as an evacuation route

## Family communication / SMS evidence

The production family-contact SMS feature was promoted and verified under:

```text
V01-NAT-FAMILY-CONTACT-SMS-03
SMS03_PRODUCTION_PROMOTION=PASS_CLOSED
V01_NAT_FAMILY_CONTACT_SMS_03=PASS_CLOSED
```

Production byte identities recorded at closure:

```text
index.html
128DCD3560EAEEA2E0BCF8425152D285B7633640975C30EE18A320170A46D315

runtime-emergency/emergency-simple-runtime-v0.1.js
72A225CFF3949B1BA69EB2F8694DFB3D4988A5F8C87CF1EB94C688AD94BBE81C
```

Real Edge production verification passed the defined SMS gates:

- 0 / 1 / 2 / 3 contact flows
- one-contact auto-selection
- explicit re-selection when multiple contacts exist
- 119 / 110 rejection from the family-recipient list
- maximum three contacts
- five exact evacuation-status messages
- recipient-prefilled `sms:` URI generation
- `現在地：未取得` fallback
- no new GPS acquisition by the SMS flow
- persistence across reload
- delete / reselection behavior
- Service Worker controlled / activated
- LIVE-03 runtime regression gate
- Real Edge stability
- application-origin contact-data exfiltration gate

The Edge environment contained Kaspersky endpoint-security injection. Six QA observations containing dummy contact test values were directed to a Kaspersky endpoint and were classified as endpoint-security interception rather than application transport. The blocking application-origin contact leak count was zero.

This means the project may state **no application-origin contact-data exfiltration was observed in the defined QA**. It must not convert that result into an absolute claim that browser extensions, endpoint-security products, or other privileged local software cannot inspect page content.

### iOS real-device handoff

Human real-device verification on iPhone confirmed:

```text
IOS_SAFARI_SMS_HANDOFF=PROVEN
IOS_PWA_SMS_HANDOFF=PROVEN
IOS_REAL_OS_SMS_HANDOFF=PROVEN
IOS_RECIPIENT_PREFILL_REAL_DEVICE=PROVEN
IOS_SMS_BODY_REAL_DEVICE=PROVEN
IOS_NO_AUTO_SEND_REAL_DEVICE=PROVEN
USER_FINAL_SEND_REQUIRED=PROVEN
```

The observed message body included the expected evacuation-start text and the location fallback when UI05 location was unavailable.

### Android real-device handoff

```text
ANDROID_REAL_DEVICE_SMS_HANDOFF=DEFERRED_NO_ANDROID_REAL_DEVICE
```

No Android handoff failure was observed; the Android real-device check simply was not executable because no physical Android device was available.

The iOS closure does not close broader physical Android or real-world GPS field validation.

See [the family-contact SMS release record](../releases/2026-10-08-family-contact-sms.md).

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
