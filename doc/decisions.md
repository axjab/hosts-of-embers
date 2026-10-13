# Decisions and open questions

## Accepted

| Decision | Rationale |
| --- | --- |
| Repository: `axjab/hosts-of-embers` | One ecosystem, one public monorepo |
| Root organization: `doc/`, `bin/`, `src/` | Keep the repository root uncluttered |
| CLI: `embers` written in Go | Clear, memorable interface (`embers host list`) |
| Bootstrap: `kindle.sh` | Initial provisioning, distinct from ongoing management |
| Agent: Fire Keeper | Background mode of `embers`, not a second host executable |
| Hub: `hosts.alj.cx` | Authoritative inventory, policies, desired and reported state |
| `embers sync` | Coordinate managed synchronization through established tools |
| Read-only diagnostics | DMS-style report; inspection must not modify the host |
| Public docs first | Establish contracts before shipping code |

## Provisional

- **Diagnostic verb:** `doctor` is the working name; `check` and `inspect` were considered.
- **Hub technology:** Python backend, Angular frontend for learning, or a minimal combination; no decision on framework or storage yet.
- **Supported OS:** Debian 13 first; define Ubuntu target and compatibility specifics before claiming support.
- **Scope of auto-reconciliation:** Which resources Fire Keeper may modify without interactive approval.
- **Resource contracts:** Per-tool sync direction, conflicts, safety, secret delivery, retry behavior, and rollback.
- **Enrollment recovery:** Rotation, revocation, repair, and replacement rules.

## Historical reference

[`axjab/kindling`](https://github.com/axjab/kindling) remains useful for its motivation and earlier research. It is deprecated. Its prior Ansible-centered architecture, `kindling` executable naming, and legacy script paths are **not** decisions of this project.
