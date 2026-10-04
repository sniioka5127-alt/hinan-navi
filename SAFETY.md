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

### Historical presentation boundaries

Historical-disaster material may contain schematic educational representations.

Unless explicitly supported by evidence, the application does not claim:

- clock-accurate reconstruction
- exact historical disaster geometry
- exact historical jurisdictional boundaries
- automatically inferred disaster extent

### BASE_M6 records

BASE_M6 catalog records are read-only historical records.

They must not be silently promoted into executable replay scenarios.

### Fail closed

When a dependency or optional subsystem cannot be validated, the preferred behavior is to disable or isolate that function rather than create a false impression of certainty.

## Software limitations

No navigation system can guarantee a safe route.

Road closures, fire, flooding, tsunami, landslide, structural damage, weather, human congestion, and rapidly changing local conditions can invalidate a route.

Users must compare application output with actual conditions and official instructions.

## Responsible reporting

Security or safety issues should be reported privately to the repository maintainer rather than disclosed in a way that could create avoidable risk before a fix is available.
