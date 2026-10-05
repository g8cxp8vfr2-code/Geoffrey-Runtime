# Current status — October 5, 2026

## Radio V2 in preparation

Radio V2 is being prepared and verified. The main Radio installer is temporarily unavailable, and no earlier installer is offered on the [official Radio page](https://geoffreyruntime.com/radio/install).

Radio remains free and local-first. No Jackson-West account is required. The published setup path uses Global Lock and does not require Global Key. Station and Speaker Button catalogs remain available for $0; consult their permanent pages for current setup and terms.

Geoffrey Runtime downloads do not automatically grant access to Jackson-West's separate private services.

The [Black Line Express browser preview](https://geoffreyruntime.com/black-line-express/demo/) is a separate concept with simulated vehicle controls and an external WVLG player link. It is not a Radio V2 release or an active vehicle connection.

## Archived status — September 30, 2026

The dated record below describes the frozen V1 architecture and deployment work at that time. Its installation/publication table is historical; use the official Radio page for current availability.

## Geoffrey Runtime Radio V1

**Architecture/readiness review complete. Architecture frozen.** The [official architecture](docs/radio-v1.md) is the source of truth. This status records the owner's freeze decision; it does not claim that this documentation task executed or tested an installed Shortcut.

Radio is local-first. Global Lock / Jackson-West access defaults false/off. Free Radio executes without Jackson-West governance; optional enabled communication follows the local action as a receipt/state report, never a second execution. Play, Stop, Back, and Next are the only V1 actions; volume, pause, and resume are excluded. Customer-owned Shortcuts and registries stay editable; Jackson-West is the independently enforced server security boundary.

Initialization requires at least one local run to create `radio.json` using the public bootstrap registry on the interactive path. Server-originated/structured cold-start execution is unsupported. Distributable Jackson-West Core and Text Jackson-West customer values are intentionally blank until optional onboarding. Mac media labels are development-device artifacts requiring customer-device verification.

## Installation and deployment

Radio controller → required Radio Stations → required Speakers/outputs → Global Lock → optional Jackson-West service. Stations/Speakers have separate packaging, verification, and publication. Their unpublished helper links are not engine defects.

| Area | Status / next step |
| --- | --- |
| Frozen engine architecture and schema | Documentation aligned; no runtime or schema-field changes |
| iPhone/customer-device verification | Remaining deployment verification |
| Radio/controller Apple download | Publication link still to be supplied |
| Stations | Package/publish helpers and supply exact names and installation links |
| Speakers/outputs | Package/publish helpers and supply compatible setup details and links |
| Website | Three permanent install pages published; download links/catalog content still need completion |
| Global Lock | Existing separate $0 installer available |
| Final customer-install tests | Verify complete install, first local run, and initialized structured/server execution |

Permanent pages: [Radio](https://geoffreyruntime.com/radio/install), [Stations](https://geoffreyruntime.com/radio/install/stations), [Speakers](https://geoffreyruntime.com/radio/install/speakers), [Global Lock](https://geoffreyruntime.com/global-lock/install). Page publication alone does not establish completed Apple downloads or customer-install verification. No V2 behavior or local tamper-resistance work is required by the freeze.

