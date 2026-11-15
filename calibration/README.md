# Measured registry text headroom

The initial corpus was collected on 2026-11-02 from the real rooted LG development TV
(app source `9266c34e7`) and the Linux/Ubuntu 24.04 simulator built by app CI run
[41461558740](https://github.com/GLinnik21/plx-native/actions/runs/41461558740)
(source `60410e182b1474cf10c48dac89310fdfd0ac0c7e`). The TV session used the repository TV lock,
a synthetic guest/mock, a muted TV and its panel on. Deployment verified all 47 files.
The native diagnostic reported `hud-text-metrics: wrote 12276 samples`.

The TV's `/usr/lib/libSDL2_ttf-2.0.so.0` SHA-256 was
`ab1dd4bd1648055f028459a573384a381e5a8ce276f22493910543fc756f3c42`.
Font identities are recorded in both reports and match exactly. No account, server address,
credential or device serial is part of the stored measurement reports.

`tv-metrics.json` is the native report. `60410e182.host.json` is the Linux CI report;
`60410e182.json` records their hashes, complete corpus coverage and worst positive differences.
There are 12,276 rows: all eleven shipped languages, every supported rung and both weights,
using the lint's actual label/command/chapter/episode-prefix candidates and clock-width envelopes.
A clock envelope can choose different widest digits on each renderer; its maximum width is compared.

| Rung | Registry margin, px |
|---|---:|
| MICRO | 7 |
| CAPTION | 6 |
| LABEL | 4 |
| BODY | 4 |
| HEADLINE | 7 |
| TITLE | 6 |
| DISPLAY | 6 |
| HUD_TITLE | 8 |
| HERO | 9 |

Each margin is the ceiling of the maximum positive `TV width - Linux width` at that rung.
Registry lint receives it explicitly with `--text-skew`; normal TV admission adds zero and uses
its own native widths. These measurements describe this renderer/font corpus; installed HUDs
continue to compile locally on each TV.

Every accepted simulator pin has a profile naming its exact host source and font bytes. The
release job compares an unchanged corpus directly with this TV evidence. When translations or
languages change, it carries the empirical per-rung margins only while the font hashes, native
text-renderer library hashes and type scale match a measured baseline. The profile records both
the original measurement and its current host binding; it does not claim the new strings were
measured on the TV. Changed fonts, renderer libraries or type sizes with a changed corpus require
fresh native evidence. Local compilation on each TV remains authoritative.
The `60410e182`, `f1436ba` and `1c9a75db` profiles retain earlier iteration evidence. The preceding
`1c9a75db` bundle was published by app CI run
[41487654770](https://github.com/GLinnik21/plx-native/actions/runs/41487654770), with profile `3f9a62fc…`.
The preceding developer SDK was source `3bc30f4edd3b392724968f9945dbef002cd646f2`, published by app CI run
[41515162200](https://github.com/GLinnik21/plx-native/actions/runs/41515162200). Its manifest-hash-
named profile and host report (`4f88bbe2…`) compare all 12,276 rows directly with the native report,
without carrying a changed corpus, and produce the same margins above. Only the source binding
differs from the preceding host report; its metric rows and font hashes are identical. The pinned
bundle includes both actual PMS chapter `tag` values in the long-title fixture and the shared
UTF-8 buffer truncation fix.

The active bundle SDK is source `017ff3ad29443e5ecf47e7c3d3b93f4625cf5c2c`, published by app CI run
[41664064627](https://github.com/GLinnik21/plx-native/actions/runs/41664064627). Its manifest-hash-named
profile and exact host report are `913f7662…`. The existing `release_profile` helper compares all
12,276 new Linux rows directly with `tv-metrics.json` and reproduces the margins above.
The profile records host source `017ff3a`, TV source `9266c34e7`, both report hashes, identical font
identities and the current SDK renderer/type-scale identities. The original TV report is retained.
Registry-native lint and captures are recorded separately in `IMPLEMENTATION.md` as they complete.

## v0.10.0 remeasurement (2026-11-16)

The published `v0.10.0` simulator (source `015868116287136757e456797754fd9a846d42b4`, manifest
`4911fce1…`) grew the corpus from 12,276 to 13,608 rows: Catalan (`ca`, 1,134 rows) joined the
shipped languages, and the new `watch.intro` label added 18 rows in each of the other eleven.
No existing row's text or type size changed, and the font bytes are identical. Its caption renderer
`pkg/libass-plx-host.so.0` changed (`789639d6…` to `bd5eee75…`), so no measured baseline matched
for carrying margins, and `release_profile` correctly refused the release until fresh TV evidence
existed.

`tv-metrics.json` is now the native report from that exact source: the app CI debug package
`com.beb.plxnative.debug_0.10.0_arm.ipk` (artifact `plxnative-0158681…` of
[CI run 43245350897](https://github.com/plxnative/plx-native/actions/runs/43245350897)), installed
on the same rooted LG development TV under the repository TV lock, its binary MD5 verified on the set,
and booted with no injected token and only the `hud-text-metrics` trigger armed. The measurement
runs before the frame loop; no account, server or mock is involved. The diagnostic reported
`hud-text-metrics: wrote 13608 samples`. The TV's `libSDL2_ttf-2.0.so.0` SHA-256 is still
`ab1dd4bd…3c42`. Debug builds report the next development version (`0.11.0-dev`); the report's
`source_sha` is `0158681`.

All 12,276 rows measured on source `9266c34e7` reproduce identical widths. Against the v0.10.0
Linux report, `calibrate` covers all 13,608 rows in twelve languages and both weights and yields
the same per-rung margins as the table above. The previous native report is retained as
`9266c34e7.tv.json` (SHA-256 `dc2e1f38…`), which earlier profiles name as their `tv` evidence.
