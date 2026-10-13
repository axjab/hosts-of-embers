# Architecture

## Responsibilities

| Owner | Responsibility | Does not replace |
| --- | --- | --- |
| `kindle.sh` | Initial network readiness, prerequisites, host identity, enrollment, initial configuration and verification | Package and network utilities |
| `embers` (Go) | Human/scriptable inventory queries, diagnostics, and policy-driven sync | Git, Gopass, Unison, rsync, SSH, systemctl |
| Fire Keeper | Background heartbeat, desired-revision retrieval, managed-state observation, permitted reconciliation, result reporting | General telemetry/monitoring suites |
| Control plane (`hosts.alj.cx`) | Authoritative inventory, trust policy, per-host desired state, observed state and staleness | Operating-system configuration managers |

The Fire Keeper daemon is **`embers agent daemon`**, not an independent binary. A minimal control-plane server may be a separate deployable; that does not require another repository.

## Planned source layout (not created during the documentation phase)

```text
hosts-of-embers/
├── README.md
├── doc/                      # Design and operational documentation
├── bin/
│   └── kindle.sh             # Initial bootstrap
└── src/
    ├── embers/               # Go CLI + embedded Fire Keeper agent
    └── hub/                  # Minimal hosts.alj.cx backend/frontend
```

Only `README.md` and `doc/` exist in the first commit. `bin/` and `src/` will be created **when implementation begins**.

## Logical flow

1. The bootstrapper creates or confirms a host identity and enrolls it.
2. The hub records its authorized inventory membership and publishes host-specific desired state.
3. The Go CLI can query inventory, check local compliance, and request managed synchronization.
4. Fire Keeper periodically authenticates to the hub, reports observed state, compares revisions, and performs only approved changes.
5. The hub records freshness and results; it does not infer that a silent host is healthy.

## Synchronization contract

Every registered resource eventually needs a declared owner, source, destination, sync direction, selected underlying tool, authentication requirements, dependencies, conflict policy, dry-run capability, and failure behavior. Tools may differ; Hosts of Embers provides one coherent policy and status model. `git pull` is not an acceptable default for every working tree; bidirectional Unison and destructive rsync options must be treated distinctly.

## Language choice

- **Host executable:** Go (decided).
- **Bootstrap:** Bash (decided).
- **Control plane:** Python and/or an Angular frontend (undecided). Angular is a frontend framework, so it may need a minimal API backend. The first implementation should remain deliberately small.

## Operational boundary

A local inspection must not modify state. Reconciliation should stage/validate changes, avoid unknown resources, never accept arbitrary remote shell scripts as jobs, and report partial failures. Fleet coordination belongs to the hub, not to ad hoc SSH fan-out by the host CLI.
