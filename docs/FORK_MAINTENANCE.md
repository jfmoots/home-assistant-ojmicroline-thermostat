# Maintaining this fork

The `local-control` branch is the maintained installation source. The
`feature/wg4-local-control` branch is the unbranded upstream contribution.
The original repository remains the `upstream` Git remote. Keep local support
in version control and install tagged releases through this fork's HACS entry.
Do not enable automatic branch synchronization that resets `local-control` to
upstream `main`.

For an upstream update, create a review branch from `local-control`, merge
`upstream/main`, resolve conflicts, and review the changes to lifecycle,
coordinator, options, entity identity, dependency versions, and local protocol.
Run `uv sync`, `uv run prek run --all-files`, and the full test suite with
coverage before merging. Test the packaged release on the real thermostat,
including HA restart, reconnection, temperature/manual/schedule controls, and
preserved entities. Keep a known-working zip and HA backup for rollback.

Source manifests stay at `0.0.0`. Publish an incremented tagged GitHub release;
`.github/workflows/release.yaml` puts the tag version into the manifest and
attaches `ojmicroline_thermostat.zip`, which HACS downloads. Confirm that the zip
has component files at its root and contains no private profile, keys, caches,
or packet captures. Only offer reviewed, tested releases for installation.
A release number on this fork does not imply the same release upstream.

If upstream accepts local support, compare its final implementation before
switching repository sources. Do not assume an upstream update contains the
experimental gateway merely because its version number is higher.

The gateway is part of HA Core's integration process. Preserve the HA address,
thermostat DNS override, port 9533 reachability, and private `.storage`/gateway
folder in backups. No separate relay service needs to be updated or restarted.
