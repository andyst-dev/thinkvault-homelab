# Security policy

This repository contains deployment definitions only. Runtime state is
intentionally excluded because it can contain authentication material and
personal data.

## Never commit

- `.env` files
- Plex, Jellyfin or qBittorrent configuration directories
- databases, logs, cookies, certificates or private keys
- torrent metadata or `.fastresume` files
- media libraries, downloads or backups
- public IP addresses, private DNS records or router configuration

If any secret reaches Git history, removing the current file is not sufficient.
Revoke or rotate the credential, then clean the repository history before
publishing it again.

## Network exposure

Jellyfin, the qBittorrent Web UI and Dashdot bind to `127.0.0.1` by default. If
`BIND_ADDRESS` is changed to `0.0.0.0`, restrict access with a host firewall and
never forward administrative web interfaces directly from the internet.

Plex uses host networking in this stack. Review its documented ports and
remote-access settings before enabling router port forwarding.

The qBittorrent peer port `6881/TCP+UDP` is intentionally published on all host
interfaces. Restrict or change it according to the network's threat model.

Dashdot runs privileged to match the source deployment. Treat that container as
trusted, keep it updated, and do not expose it outside the trusted LAN.
