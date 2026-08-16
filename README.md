> Note: this document will change overtime as I implement new services, etc. It is a "living document"
> 
> Project Status: ONLINE
> 
> Next Step: None

# homelab

This is just a repo where I can put info about my homelab - not really a project-project, but still a cool thing people can look at and know I do.

The bulk of this is just me yapping in this readme about specs, services, reasoning, etc. A friend suggested I put compose files here too (without the actual info duh) so that I can just copy my setup on another machine if I ever get to that point - won't do that yet since I'm not too familiar with what I should/shouldn't make public. 

---

## INSPIRATION

The reason why I started a homelab (ie setup my own server) is mainly because: 

a) I was already in the process of "de-googling". I haven't gotten to google photos yet, but I'll get to it soon, so setting up something like immich and getting used to it before I do would make the transition smoother.

b) friend pushed me to do it - I was gonna do it either way but I did it sooner thanks to them.

(also [its just not appropriate as a grown man to backup your data on the cloud](https://www.tiktok.com/@sandboxsessions/video/7611533386473114893))

---

## ARCHITECTURE / NETWORK

### HOST SPECS
- **Computer:** Desktop
- **OS:** Debian GNU/Linux 13 (Trixie)
- **CPU:** Intel Core i7-3770 @ 3.40 GHz
- **RAM:** 16 GB DDR3 (2 × 8 GB, 1333 MT/s)
- **Storage:** 1 TB (WDC WD1002FAEX-00Y9A0)
- **GPU:** NVIDIA GeForce GTX 1050


### other stuff

// this is the section people actually check for security understanding
// answer directly:
//   - is anything exposed to the public internet, or is it Tailscale-only?
//   - how do you personally connect to it remotely?
//   - one diagram or bullet list of: internet -> router -> server -> containers

recommendation: a simple diagram (even ASCII) showing Tailscale as the only ingress point,
no forwarded ports, no public DNS record pointing at it.

---

## ACCESS

Most apps I just

For accessing the server itself, I use SSH. If I'm not in my network I rely on tailscale, where I've setup a tailnet for my devices so that I can access the server.

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
