# Replay Engine

## Purpose

Replay is used for training-oriented disaster scenarios.

It is intentionally separated from general historical catalog browsing.

## Namespace separation

The general Historical Disaster Archive and replay scenarios are not the same thing.

BASE_M6 catalog records are **not replay scenarios**.

Special Historical records can use the special historical presentation path, but their historical renderer remains schematic and is not a claim of clock-accurate reconstruction.

## Control behavior

When a Special Historical view is active, replay controls that would imply clock-accurate simulation are suppressed / disabled.

Returning to a base replay scenario restores the normal control state.

## Design principle

The application should never make a historical catalog row “look replayable” merely because the UI has a replay engine elsewhere.
