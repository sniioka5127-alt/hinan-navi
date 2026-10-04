# Evacuation Routing

## Purpose

Routing supports movement toward evacuation destinations when route data is available locally.

## Design goals

- offline route calculation
- walking-oriented evacuation use
- GPS integration
- rerouting support
- route rendering independent from continuous cloud connectivity

## Safety boundary

A mathematically valid route is not necessarily a safe route.

The routing engine cannot guarantee knowledge of:

- debris
- fire
- collapsed structures
- closed roads
- active flooding
- tsunami arrival
- landslide activity
- crowd conditions

Routing output must therefore be interpreted alongside hazard information, official instructions, and direct observation.

## Fail-closed principle

If routing data is missing or invalid, the system should not fabricate a route.
