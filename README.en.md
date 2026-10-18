# log-hazmat-transport-checker

[![License: MIT](https://img.shields.io/badge/Code%20License-MIT-yellow.svg)](LICENSE)
[![Content: ARR](https://img.shields.io/badge/Content%20License-ARR%20%7C%20citable-blue.svg)](LICENSE-CONTENT)

> **Status: RESERVED (placeholder · open for claim)** — this repository already ships the four-file industry-access skeleton per the platform protocol, and waits for an operator with domain credentials to claim it and fill in real rules.

This is the SynomosAI **domain profile** for road transport of dangerous goods (hazmat) — carrier qualification and carriage conditions. It decomposes "may this cargo be carried, and who is qualified to carry it" into verifiable attributes, so that AI only provides prerequisite guidance — never a carriage dispatch clearance.

## What this domain governs

Road dangerous-goods transport qualification and carriage-condition verification.

Dangerous goods carry category-specific packaging, vehicle, personnel and emergency-response requirements; undeclared/mis-declared cargo is the leading accident cause. AI can lay out qualifications vs. conditions; carriage clearance belongs to the enterprise safety officer and the transport authority.

## Domain identity

| Field | Value |
|---|---|
| Domain ID | `log` (globally unique, never reused) |
| Domain name | Logistics · road dangerous-goods transport qualification |
| Profile version | `domain/1.0` |
| Status | `RESERVED` |
| Reserved at | 2026-09-12 |

## Attributes

| Key | Type | Meaning |
|---|---|---|
| `log.cargo_class` | enum | Hazmat class per JT/T 617; hazmat status follows the classification conclusion · explosives/gases/flammable_liquid/flammable_solid/oxidizing/toxic/radioactive/corrosive/miscellaneous/not_hazmat/undetermined |
| `log.transport_permit` | enum | Road dangerous-goods operating permit (incl. scope) · valid/expired/none/not_required |
| `log.vehicle_qualification` | enum | Vehicle/tank safety condition fitting the carried class · qualified/unqualified/unknown/not_required |
| `log.personnel_cert` | enum | Driver/escort practitioner certificates & current validity · valid/expired/none/unknown |
| `log.emergency_plan` | enum | Emergency plan filing & drill records · filed/missing/not_required |

## Red lines (machine-readable, non-negotiable)

1. Never output "may carry / may dispatch" — the transport authority's permit is the sole basis.
2. Never state that transport may proceed when personnel certs are lapsed, vehicles unqualified, or the class unknown.
3. Never suggest undeclared/mis-declared cargo, mixing with general cargo, or split declarations to evade hazmat control.

Each red line has a matching blocking rule in `gate-map.json`; the platform validator fails if coverage is missing.

## Quick Start / 快速开始

This repo is a declarative skeleton — no runtime, no install.

```bash
git clone https://github.com/SynomosAI/log-hazmat-transport-checker.git
cd log-hazmat-transport-checker
python -m json.tool domain.manifest.json    # validate the manifest
cat checker.io.json                         # read the MCP tool contract
```

The checker MCP tool returns only four states — `shown / missing / expired / unverifiable` — and is forbidden from outputting "may-carry / compliant" conclusions (see `_forbidden_outputs` in `checker.io.json`).

## Repository layout

```text
domain.manifest.json   # declaration: attributes / issuer requirements / red lines / validity
gate-map.json          # friction levels per action class (gate/1.0)
privacy.json           # privacy notice (privacy/1.0) — an admission condition
checker.io.json        # MCP checker I/O contract (show & verify, never judge)
LICENSE                # code & config: MIT
LICENSE-CONTENT        # prose content: All Rights Reserved (citable with attribution)
```

## References

- Regulations on Safety Management of Hazardous Chemicals (危险化学品安全管理条例)
- Road Transport Regulation of the PRC (道路运输条例)
- Provisions on the Administration of Road Dangerous Goods Transport (道路危险货物运输管理规定)
- JT/T 617 Rules for Road Transport of Dangerous Goods (危险货物道路运输规则)
- Work Safety Law of the PRC (安全生产法)

The above references only explain the origin of the domain's attributes; they are not legal advice.

## Claiming this domain

The domain is open to qualified institutions. To claim:

1. Fork this repo and fill in `operator` and `checker_endpoint`.
2. Calibrate attribute values and red lines per current rules.
3. Run the platform validator self-test (all five criteria must pass).
4. Open a PR with credential proof and rule citations.

## License

Code and configuration are MIT-licensed. Prose content is copyrighted by SynomosAI.

© 2026 SynomosAI. All rights reserved.

Full terms: [LICENSE](LICENSE) (MIT) · [LICENSE-CONTENT](LICENSE-CONTENT) (ARR). Report security issues privately via [SECURITY.md](SECURITY.md).
