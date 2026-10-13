# Hosts of Embers

> A host, once cold. A flame, divided. Across forgotten lands, the embers still answer one another. None recall who struck the first spark.

**Hosts of Embers** is a planned, self-hosted system for bringing Linux machines into a trusted fleet and keeping their managed state understandable and consistent.

A freshly installed machine begins **cold**. `kindle.sh` establishes the prerequisites for joining the fleet. The Go CLI, **`embers`**, inspects host records, diagnoses management problems, and coordinates synchronization through existing tools. A resident **Fire Keeper** agent (a mode of `embers`, not a separate program) reports to a small control plane at **[hosts.alj.cx](https://hosts.alj.cx)**.

**Status: design phase. This repository contains documentation only.** No bootstrap script, CLI, agent, or web service is implemented here yet; the commands below describe intended behavior.

## The pieces

| Component | Role | Planned implementation |
| --- | --- | --- |
| `kindle.sh` | Bring a cold Debian/Ubuntu host to a provisioned, enrolled, verified state | Bash bootstrapper |
| `embers` | Query the fleet, synchronize managed resources, diagnose host compliance | Go CLI |
| Fire Keeper | Report host state and apply authorized managed changes continuously | `embers agent daemon`, managed by systemd |
| `hosts.alj.cx` | Authoritative host inventory, desired state, policies, and agent reports | Minimal web control plane; Python backend or Angular frontend approach still undecided |

Names such as `firelink` and `majula` belong to individual hosts, not executable programs.

## Intended interface

```console
embers host list
embers host show firelink
embers sync --dry-run
embers sync
embers doctor              # diagnostic name still provisional
embers agent daemon
```

`embers sync` orchestrates **declared** synchronization operations, delegating actual work to tools such as Git, Gopass, Unison, and rsync. It is not an unconditional `git pull` or an arbitrary filesystem mirror: resource ownership, direction, conflict behavior, and safety rules must be explicit.

`embers doctor` is intended to be a read-only diagnostic report: show relevant system facts, verify enrollment and managed resources, distinguish warnings from failures, and provide useful exit codes. The `doctor` name is still open to review.

## Design principles

- **Do not reinvent the wheel.** Use existing tools for package management, services, networking, storage, and file transfer.
- **Business rules first.** Custom code must implement Hosts of Embers-specific identity, policy, inventory, reconciliation, or reporting.
- **One repository, separate deployables.** Bootstrap, host CLI/agent, and the minimal control plane share contracts without needing to run as one process.
- **Safe repetition.** Bootstrap and reconciliation should be recoverable and idempotent wherever possible.
- **Explicit ownership and trust.** The hub defines authorized desired state; hosts only apply changes they can authenticate and are permitted to make.
- **Public code, private secrets.** No private keys, credentials, or live secret-store contents belong in this repository.

## Documentation

- [Vision and boundaries](doc/vision.md)
- [Architecture and planned layout](doc/architecture.md)
- [Host lifecycle](doc/lifecycle.md)
- [Security principles](doc/security.md)
- [Roadmap](doc/roadmap.md)
- [Decisions and open questions](doc/decisions.md)

The [GitHub issues](https://github.com/axjab/hosts-of-embers/issues) are the implementation backlog. Earlier explorations remain in the [deprecated `kindling` repository](https://github.com/axjab/kindling); they are historical context, not the new architecture's source of truth.
