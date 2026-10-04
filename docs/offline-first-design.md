# Offline-First Design

## Goal

The application should retain meaningful disaster-support capability when internet access is unavailable or unreliable.

## Design priorities

1. local availability of critical application assets
2. local map access where packaged
3. local shelter / route support where packaged
4. graceful isolation of live-network features
5. clear UI state when data is unavailable

## Why this matters

Disasters often create exactly the conditions that make cloud-only applications least reliable:

- congestion
- infrastructure damage
- power loss
- mobile-network degradation
- temporary isolation

Offline-first design is therefore treated as a safety property rather than merely a performance optimization.

## Fail-closed behavior

Optional online or historical subsystems should not break core offline behavior.

If a dependency fails, the application should preserve the base experience whenever possible.
