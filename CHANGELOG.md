# Changelog

## 2026-10-08 — Family contact SMS production + iOS real-device handoff

Status: **PASS_CLOSED**

### Added / verified

- family-contact storage for 1–3 recipients
- explicit recipient selection when multiple contacts exist
- 119 / 110 separation from family contacts
- five fixed evacuation-status SMS messages
- existing UI05 location reuse with `現在地：未取得` fallback
- recipient-prefilled OS SMS handoff
- no automatic SMS send; final send remains a user action
- production Real Edge verification
- iOS Safari real-device handoff
- iOS home-screen PWA real-device handoff
- application-origin contact-data exfiltration gate

### Production evidence

```text
V01-NAT-FAMILY-CONTACT-SMS-03=PASS_CLOSED
IOS_SAFARI_SMS_HANDOFF=PROVEN
IOS_PWA_SMS_HANDOFF=PROVEN
ANDROID_REAL_DEVICE_SMS_HANDOFF=DEFERRED_NO_ANDROID_REAL_DEVICE
```

Kaspersky endpoint-security injection was observed during Edge QA and classified separately from application transport. The blocking application-origin contact leak count remained zero.

See [releases/2026-10-08-family-contact-sms.md](releases/2026-10-08-family-contact-sms.md).

## v1.0.0 — Production historical-disaster archive release

Status: **PASS_CLOSED**

### Added

- unified historical-disaster search namespace
- BASE_M6 read-only catalog detail
- four Special Historical records
- schematic educational renderer
- production activation path without QA-query activation
- production deployment verification

### Historical archive counts

- BASE_M6: 821
- Special Historical: 4
- Unified Search: 825

### Verification

- Local Real Edge QA: PASS_CLOSED
- Human Visual QA: PASS_CLOSED
- Hostinger Remote Smoke: PASS_CLOSED
- Remote deployment identity: 19 / 19 SHA-256 match

See [releases/v1.0.0.md](releases/v1.0.0.md).
