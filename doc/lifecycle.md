# Host lifecycle

## Cold → kindled

The intended **`kindle.sh`** lifecycle is:

1. Establish Internet connectivity (for example, using NetworkManager/`nmcli` where needed).
2. Install script prerequisites and the `embers` executable.
3. Establish and protect the host's SSH/GPG and other required identity material.
4. Enroll in the authorized Tailscale network and Hosts of Embers control plane.
5. Discover authorized peers; manage owned sections of `/etc/hosts` and SSH client configuration.
6. Retrieve initial approved configuration, credentials, and selected application data.
7. Apply the initial managed configuration through existing tools.
8. Start required services, including Fire Keeper.
9. Verify readiness and report the result.

A host becomes **kindled** after successful verification. Failed and partially completed stages must be diagnosable and safely repeatable where practical. Bootstrap enrollment is not routine daily reconciliation.

## Kindled → tended

During ongoing operation:

- `embers host list/show` queries the fleet's authorized records.
- `embers sync` performs explicit managed synchronization, not blanket updates.
- `embers doctor` (working name) checks host identity, compliance, service dependencies, and relevant system facts without changing anything.
- `embers agent daemon` (Fire Keeper) heartbeats, checks approved state, and reports or applies permitted corrections.

## Loss of connectivity

An offline machine retains its last **validated** applied configuration. The agent does not erase peers or credentials merely because the hub is unreachable; it retries with backoff and the hub records the observation as stale. New revisions must be authenticated before application.

## Recovery and replacement

Identity compromise, re-enrollment, host replacement, revocation, and configuration rollback require an explicit policy before implementation. No default operation should silently reset identities or destroy user data.
