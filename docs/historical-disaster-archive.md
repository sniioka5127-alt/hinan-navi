# Historical Disaster Archive

## Production status

**PASS_CLOSED**

Public application:

https://wakouzan-kichijoji.com/hinan-navi/

## Search namespace

The current production namespace contains:

| Class | Records |
| --- | ---: |
| BASE_M6 | 821 |
| Special Historical | 4 |
| **Total** | **825** |

## BASE_M6

BASE_M6 records are catalog-derived earthquake records.

Selection behavior:

- open read-only historical detail
- do not dispatch to replay
- do not infer synthetic historical geometry

Typical displayed fields may include:

- origin time
- magnitude / magnitude type
- depth
- epicenter catalog name
- maximum intensity
- latitude / longitude
- catalog identifier

## Special Historical

Current special cases:

1. `jp-0864-fujisan-jogan-eruption`
2. `jp-0887-ninna-earthquake`
3. `jp-1707-hoei-earthquake`
4. `jp-1707-fujisan-hoei-eruption`

These use dedicated renderers.

## Evidence boundary

Special Historical output is:

`SCHEMATIC_EDUCATIONAL`

It is not:

- clock-accurate replay
- exact historical geometry
- automatic georeferenced disaster reconstruction

## Production verification

The production release passed:

- search namespace verification: 825
- BASE_M6 detail verification
- BASE_M6 no-replay verification
- Special search dispatch
- Special 4-of-4 renderer verification
- base restore verification
- visual QA
- query-backdoor negative QA
- remote deployment SHA verification
