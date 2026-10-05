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

## Responsible reporting

Security or safety issues should be reported privately to the repository maintainer rather than disclosed in a way that could create avoidable risk before a fix is available.
