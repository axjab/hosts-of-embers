# Public repository and host security

## Public-repository rule

Only public documentation, source code, safe examples, templates, and non-sensitive test fixtures belong here. Never commit real SSH/GPG private keys, Tailscale auth keys, access tokens, gopass contents, recovery material, host-specific passwords, or actual secret-bearing rendered configuration.

Hostnames such as `firelink` and `majula` are part of the documented naming scheme; inventory examples must not inadvertently disclose private network addresses or credentials.

## Security requirements to design

- **Identity:** Uniqueness, enrollment proof, rotation/revocation, and recovery of machine credentials.
- **Authority:** The hub determines which host is authorized to receive which data.
- **Delivery:** Authenticate desired-state revisions and bind them to the intended host.
- **Ownership:** Change only explicitly managed resources; never seize arbitrary paths or services.
- **Secrets:** Delegate storage to an established secret manager, minimize exposure in process arguments/logs, and control permissions.
- **Reconciliation:** Idempotent changes, dry-run where possible, explicit conflict/destructive policy, and auditable results.
- **Privilege:** Keep Fire Keeper's privileges restricted to the resources it genuinely manages.
- **Reporting:** Separate observation timestamps from current health; an offline host is *unknown/stale*, not healthy.

These are requirements, not claims that the current documentation-only repository already implements protections.
