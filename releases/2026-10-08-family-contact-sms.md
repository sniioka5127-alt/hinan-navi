# HINAN NAVI — Family Contact SMS Production / iOS Real-Device Record

Date: **2026-10-08**

## Status

```text
V01-NAT-FAMILY-CONTACT-SMS-03=PASS_CLOSED
V01_NAT_FAMILY_CONTACT_SMS_03=PASS_CLOSED

V01_NAT_FAMILY_CONTACT_SMS_04_IOS=PASS_CLOSED
IOS_SAFARI_SMS_HANDOFF=PROVEN
IOS_PWA_SMS_HANDOFF=PROVEN

ANDROID_REAL_DEVICE_SMS_HANDOFF=DEFERRED_NO_ANDROID_REAL_DEVICE
```

## Production scope

The production promotion changed exactly two files:

```text
index.html
runtime-emergency/emergency-simple-runtime-v0.1.js
```

Recorded production identities:

```text
index.html
128DCD3560EAEEA2E0BCF8425152D285B7633640975C30EE18A320170A46D315

runtime-emergency/emergency-simple-runtime-v0.1.js
72A225CFF3949B1BA69EB2F8694DFB3D4988A5F8C87CF1EB94C688AD94BBE81C
```

The promotion did not modify `app.js`, `sw.js`, LIVE alert runtime, hazard runtime, or training runtime.

## Behavior closed in production

- family contacts: 1–3
- name + phone stored by the application in browser-local storage
- one contact: auto-selected
- multiple contacts: explicit recipient selection required
- 119 / 110 excluded from family contacts
- five evacuation-status messages
- existing UI05 location reused
- no new GPS acquisition by the SMS flow
- `現在地：未取得` fallback
- OS SMS composer handoff
- no automatic send
- final send remains a user action

## Real Edge production QA

The production Real Edge gate passed all defined family-SMS runtime gates, including Service Worker control, LIVE-03 regression coverage, persistence / delete flows, and application-origin contact-data exfiltration checks.

## Endpoint-security boundary

Kaspersky endpoint-security injection was observed during Edge QA.

```text
CONTACT_LEAK_NETWORK_HIT_COUNT=6
ENDPOINT_SECURITY_INTERCEPTION_HIT_COUNT=6
BLOCKING_CONTACT_LEAK_HIT_COUNT=0
ENDPOINT_SECURITY_CLASSIFICATION=KASPERSKY_ENDPOINT_SECURITY_INJECTION
ABSOLUTE_DEVICE_LOCALITY_ASSERTED=False
```

This evidence supports the narrower statement that **no application-origin contact-data exfiltration was observed in the defined QA**.

It does not support an absolute claim that browser extensions, endpoint-security software, or other privileged local software cannot inspect page content.

## iOS real-device QA

Human-observed iPhone testing verified both Safari and the installed home-screen PWA.

Observed behavior:

- iOS message composer opened
- selected recipient was prefilled
- message body was transferred
- evacuation-start text was correct
- `現在地：未取得` was preserved when UI05 position was unavailable
- the message was not sent automatically
- final send remained a user action
- the app remained usable after returning from the composer

Result:

```text
IOS_REAL_OS_SMS_HANDOFF=PROVEN
IOS_SAFARI_SMS_HANDOFF=PROVEN
IOS_PWA_SMS_HANDOFF=PROVEN
FAMILY_CONTACT_SMS_IOS_E2E=PASS_CLOSED
```

## Android boundary

No physical Android device was available for the corresponding handoff check.

```text
ANDROID_REAL_DEVICE_SMS_HANDOFF=DEFERRED_NO_ANDROID_REAL_DEVICE
```

This is a deferred verification item, not a product-failure result.

## Remaining broader safety gaps

```text
REAL_GPS_FIELD_QA=PENDING
PHYSICAL_ANDROID_DEVICE_QA=NOT_RUN
```

The iOS SMS result must not be generalized to broader Android or real-world GPS behavior.
