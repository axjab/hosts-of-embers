# Roadmap

Issues in [the GitHub backlog](https://github.com/axjab/hosts-of-embers/issues) are the active plan. This document defines **sequencing**, not a promise of delivery dates.

## Phase 0 — Contracts and choices

- Specify host identity, enrollment, authorization, and inventory records.
- Define managed-resource ownership, synchronization policies, and observable results.
- Confirm control-plane MVP and backend/frontend technology.
- Specify the narrowest working Debian 13 acceptance scenario.

## Phase 1 — Bring up one host

- Adapt the old `kindling` concepts into `bin/kindle.sh`; do not copy the retired architecture unchanged.
- Build the smallest usable Go executable in `src/embers/`.
- Provide `embers doctor` (or its final name) as a read-only diagnostic surface.

## Phase 2 — Connect and reconcile

- Introduce minimal `hosts.alj.cx` enrollment, inventory, and desired-state endpoints.
- Implement one safe, dry-runnable managed sync resource, then selected Git/Gopass/Unison/rsync adapters where justified.
- Run Fire Keeper as `embers agent daemon` with authenticated heartbeats and bounded reconciliation.

## Phase 3 — Prove it

On a disposable Debian 13 host, demonstrate cold → kindled → reporting → desired state changed → successful sync → compliant diagnostics. Repeat the safe operations; verify no unintended changes. Test network outages and partial failures.

## Deferred

Expanded platform support, complex fleet jobs, multi-host orchestration, rich dashboards, generic backup, and extensive performance telemetry. These require concrete use cases before being added.
