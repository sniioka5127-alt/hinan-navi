# Release and QA

## Release philosophy

Passed artifacts are treated as immutable.

A defect discovered after a gate creates a new revision rather than mutating the already-recorded artifact in place.

## Current production release

Historical Disaster Archive release status:

```text
Local Real Edge QA              PASS_CLOSED
Human Visual QA                 PASS_CLOSED
Canonical Production Promotion PASS
Hostinger Remote Smoke          PASS_CLOSED
Remote File Identity            19 / 19 SHA256 MATCH
Release                         PASS_CLOSED
```

## Browser QA coverage

The final local production QA verified, among other things:

- production activation ready
- unified search count = 825
- BASE_M6 result present
- BASE_M6 read-only detail
- BASE_M6 not dispatched to replay
- Special search result rendering
- four Special Historical records
- renderer image loading
- replay-control suppression for Special views
- restoration back to base state
- zero blocking failures in the tested path

## Production activation safety

The production release uses an explicit production feature flag.

The QA query activation route used during staging was removed from production activation.

Remote semantic verification confirmed:

- explicit production flag present
- QA query absent from production index activation
- QA query absent from activation runtime
- activation runtime does not use URLSearchParams for this feature
- activation uses the explicit global feature flag path

## Remote verification

After Hostinger deployment, all 19 changed / added release files were fetched from the public URL and matched the expected local SHA-256 values.

This verified byte identity between the approved local release delta and the deployed files.
