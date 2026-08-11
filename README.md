# homelab

// one or two sentences: what this is, why you made it, host hardware

---

## OVERVIEW

// what the server physically is (Pi? mini PC? old laptop?), what OS, why you started this
// note this was a friend-driven project if that's true — that's a fine reason, just be accurate

---

## ARCHITECTURE / NETWORK

// this is the section people actually check for security understanding
// answer directly:
//   - is anything exposed to the public internet, or is it Tailscale-only?
//   - how do you personally connect to it remotely?
//   - one diagram or bullet list of: internet -> router -> server -> containers

recommendation: a simple diagram (even ASCII) showing Tailscale as the only ingress point,
no forwarded ports, no public DNS record pointing at it.

---

## SERVICES

// table: Service | Purpose | Why this one

| Service | Purpose | Why |
|---|---|---|
| Jellyfin | media streaming | // your reason |
| Immich | photo backup/library | // your reason |
| Minecraft server | game server for friends | // your reason |
| Portainer | container management/monitoring | // your reason |
| Tailscale | private mesh VPN, no exposed ports | // your reason |

---

## DEPLOYMENT

// sanitized docker-compose.yml lives in this repo, .env.example shows variable names only
// briefly note how you deploy/update (docker compose up -d, Portainer stacks, etc)
// do NOT include real ports/IPs/tokens here — link to docker-compose.yml instead

---

## CONTAINER ISOLATION

// are services on separate docker networks, or all on the default bridge?
// do any containers run as root unnecessarily?
// if you haven't segmented anything yet, say so — that's a legitimate current-state note,
// not something to hide

---

## BACKUPS

// does Immich (actual irreplaceable data — photos) get backed up anywhere?
// if no backup exists yet, write that explicitly as a known risk, not silence

---

## SECURITY NOTES

// SSH: key-only auth? password auth disabled? non-standard port? fail2ban?
// firewall: ufw/iptables rules, or relying entirely on Tailscale's network isolation?
// update strategy: are images pinned to specific versions or floating on `latest`?
// this section is what turns "homelab" into "homelab with a security mindset" —
// don't skip it even if the honest answer to most of these is "not yet configured"

---

## KNOWN GAPS / ROADMAP

// bullet list, plain and honest:
//   - no automated backups for Immich
//   - all containers on default bridge network, no segmentation
//   - no monitoring/alerting beyond Portainer dashboard
//   - image versions not pinned
//   - (add your real ones)

recommendation: this list is more valuable to a reviewer than a clean feature list —
it shows you can audit your own setup honestly

---

## CREDITS / NOTES

// optional — anything you built following a specific guide, friend's help, etc
// keep it honest, same way you did in your other repo
