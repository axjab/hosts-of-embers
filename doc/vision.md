# Vision and boundaries

## Why it exists

A bare OS is not yet a usable, trusted member of an infrastructure. Establishing connectivity, identity, peer discovery, configuration, credentials, and verification by hand is repetitive and easy to get wrong.

The predecessor project, [`kindling`](https://github.com/axjab/kindling), identified the essential failure mode: a homegrown configuration language and orchestrator merely produce another system to maintain. Hosts of Embers carries forward the lesson **use existing mature tools; implement only our own business rules**.

## Objective

Turn a freshly installed, supported Linux machine into a known, identity-bearing Host of Embers, then keep its **declared managed state** aligned with the authoritative control plane.

- **Provision** once with `kindle.sh`.
- **Inspect and synchronize** explicitly with `embers`.
- **Observe and reconcile** continuously with Fire Keeper.
- **Define and audit** inventory and policy centrally at `hosts.alj.cx`.

## Non-goals

This is not a new package manager, remote shell, generic backup tool, secrets vault, monitoring suite, Ansible replacement, `systemctl` frontend, or general-purpose distributed scheduler. Ordinary system health tools remain ordinary system health tools.

## Initial scope

- Initial target: **Debian 13 (Trixie)**. Ubuntu Server is a planned additional target, with the exact compatibility matrix to be decided.
- A minimal, authenticated host registry and desired-state interface.
- Go CLI with `host`, `sync`, and a read-only diagnostic command; agent runs from the same executable.
- A single realistic host onboarding and reconciliation scenario before adding many integrations.

## What success means

From a disposable minimal Debian install, an operator can bring up networking, establish a unique identity, enroll, discover authorized peers, apply one owned resource, run diagnostics, and see a trustworthy current-or-stale report in the control plane. Repeating safe operations produces no unwanted changes.
