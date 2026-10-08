# Safety Model

HINAN NAVI is safety-oriented software, but it is **not an official emergency service**.

## Core safety boundaries

### Official instructions take precedence

Users should follow instructions from:

- emergency services
- national and local government
- municipalities
- the Japan Meteorological Agency
- other competent public authorities

### No fabricated certainty

The application should not present uncertain, unavailable, or unverified information as confirmed fact.

### Fail closed

When a dependency or optional subsystem cannot be validated, the preferred behavior is to disable or isolate that function rather than create a false impression of certainty.

## Verification boundary

The project separates **verified browser / emulator behavior** from **unverified physical-device / field behavior**.

Recorded Core Safety evidence currently includes:

- NAV-01 browser / integration gate: `PASS_CLOSED`
- NAV-01 repeatability: `3 / 3 PASS`
- Android Emulator integration: `PASS_CLOSED`
- Android Emulator cold start: `PASS`
- Aomori City real-JMA scan: `59 / 59`, scan errors `0`
- hazard static routes: `82 verified`
- routing graph tiles: `2,150 verified`
- shelter static cells: `295 verified`

The following remain explicitly unverified:

- real GPS field QA: `PENDING`
- physical Android device QA: `NOT_RUN`

Browser and emulator evidence must not be described as equivalent to real-device field validation.

The authoritative detailed evidence matrix is [docs/release-and-qa.md](docs/release-and-qa.md).

## Routing and shelter claims

No navigation system can guarantee a safe route.

Road closures, fire, flooding, tsunami, landslide, structural damage, weather, human congestion, and rapidly changing local conditions can invalidate a route.

Accordingly, HINAN NAVI does **not** claim:

- that a generated route is guaranteed safe
- that a displayed shelter is guaranteed safe or usable
- that absence of hazard data means an area is safe
- that a straight-line connector is an evacuation route
- that browser or emulator success proves real-world GPS / physical-device behavior

Users must compare application output with actual conditions and official instructions.

## Historical presentation boundaries

Historical-disaster material may contain schematic educational representations.

Unless explicitly supported by evidence, the application does not claim:

- clock-accurate reconstruction
- exact historical disaster geometry
- exact historical jurisdictional boundaries
- automatically inferred disaster extent

### BASE_M6 records

BASE_M6 catalog records are read-only historical records.

They must not be silently promoted into executable replay scenarios.

Historical / training feature closure is separate from Core Safety field validation.

## Family communication / SMS boundaries

The family-contact SMS feature is designed as an explicit user-controlled handoff, not as an automatic emergency-message sender.

Recorded production behavior includes:

- 1–3 family contacts
- 119 / 110 kept outside the family-recipient list
- explicit recipient selection when multiple contacts exist
- five fixed evacuation-status messages
- reuse of the existing UI05 location state rather than a new GPS acquisition
- `現在地：未取得` when no UI05 position is available
- OS SMS-composer handoff
- no automatic send; the user must perform the final send action

The application stores family-contact name / phone data in browser-local storage and does not intentionally submit those values to an application backend.

This “local-only” statement is an **application-boundary** statement. Browser extensions, endpoint-security products, accessibility software, operating-system services, or other software with page-inspection capability may still inspect content. During Edge QA, Kaspersky endpoint-security injection was observed and classified separately from application-origin transport; blocking application-origin contact-data leakage remained zero.

Real-device handoff evidence currently includes:

- iOS Safari: `PROVEN`
- iOS home-screen PWA: `PROVEN`
- Android real device: `DEFERRED_NO_ANDROID_REAL_DEVICE`

The iOS result does not imply Android real-device equivalence and does not close real-GPS field validation.

## Responsible reporting

Security or safety issues should be reported privately to the repository maintainer rather than disclosed in a way that could create avoidable risk before a fix is available.
