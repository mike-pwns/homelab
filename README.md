> Note: this document will change overtime as I implement new services, etc. It is a "living document"
> 
> Project Status: ONLINE
> 
> Next Step: finish this doc --> setup vikanja

# homelab

This is just a repo where I can put info about my homelab - not really a project-project, but still a cool thing I can share on here.

The bulk of this is just me yapping in this readme about specs, services, reasoning, etc. A friend suggested I put compose files here too (without the actual info duh) so that I can just copy my setup on another machine if I ever get to that point - won't do that yet since I'm not too familiar with what I should/shouldn't make public. 

---

## INSPIRATION

The reason why I started a homelab (ie setup my own server) is mainly because: 

a) I was already in the process of "de-googling". I haven't gotten to google photos yet, but I'll get to it soon, so setting up something like immich and getting used to it before I do would make the transition smoother.

b) friend pushed me to do it - I was gonna do it either way but I did it sooner thanks to them.

(also [its just not appropriate as a grown man to backup your data on the cloud](https://www.tiktok.com/@sandboxsessions/video/7611533386473114893))

https://www.instagram.com/reel/DWWaTlZEdoG/

---

## ARCHITECTURE / NETWORK

### HOST SPECS
- **Computer:** Desktop
- **OS:** Debian GNU/Linux 13 (Trixie)
- **CPU:** Intel Core i7-3770 @ 3.40 GHz
- **RAM:** 16 GB DDR3 (2 × 8 GB, 1333 MT/s)
- **Storage:** 1 TB (WDC WD1002FAEX-00Y9A0)
- **GPU:** NVIDIA GeForce GTX 1050

### FILE STRUCTURE

```
└── services
│   └── each service has its own directory with its docker compose, etc
└── storage
    └── services like immich, jellyfin, tandoor have on-server databases, so postgres, media directories - thats here.
```

### CONNECTION SCHEME

So.. how do I actually connect to this server?

Simple! If I'm on the right network, just SSH to the local ip that I know. 

Device (laptop, phone) <---------------> Router (home) <---------------> Server

Otherwise, I SSH via my tailnet (which uses wireguard protocol for e2e which is cool!):

Device (laptop, phone) <----> Router <----> Tailscale servers <----> Router (home) <----> Server

The reasoning for tailscale instead of something like setting up port forwarding is because if its setup by a noob (ahem), it can cause security vulnerabilities for a home network.

^^^ Real-world case: my friend has an mc server port-forwarded. Within days random people started joining...

Using tailscale, the server's access to the internet (my other devices) is very tightly controlled and in a way that even I could easily manage it through an app or a single command, `sudo tailscale up/down`. There are benefits to port forwarding, sure, but for my case where I'm just running my own services for myself, this is the simplest method. And as a dear mentor of mine says:
> "Simplicity scales, complexity fails!"

This solution just requires me to connect to the tailnet and that's it - getting in between that, or heck even getting access points is pretty much impossible (as far as I know, but I frankly have a lot to learn) - the only way to access the server as a hacker ("bad actor" for the snotty nerds out there) is to find my tailnet account and get into it, which I guess they can have fun with. Honestly, even if they get the tailnet ip, they'd still need to get the credentials for the server itself :/

---

## SERVICES

Here's a small list of services and some details on why I use it.

| Service | Purpose | Why |
|---|---|---|
| Jellyfin | media streaming | For streaming.. legally acquired.. stuff. In reality, using streaming services are usually my go to - I only really keep movies or shows that I adore/connected with deeply. Just feels more right for things I love - being able to access it whenever - to actually HAVE the stuff rather than just request it from another server. Shoutout Cyberpunk, Ghibli movies, Брат / Брат 2, The Matrix series. |
| Immich | photo backup/library | Replacement for google photos. |
| Tandoor | Recipe manager | Supper cool service that allows me to save recipes and share them and know what to get etc etc, seeing as ive been putting off learning how to look for a while, this is straight gold! Eventually I hope to get some other people on my instance and have them share recipes there too! Amazing for meal prep and stuff too!!! Hella excited to use this |
| Vikunja | Todo list | Unfortunately I gotta say goodbye to Todoist - i really liked it.. but for more security I gotta opt for the self hosted option.. I chose this cuz I needed a todo list that syncs accross mobile and desktop - thats just convenient for me. Todoist did it well, but yknow.. paid model.. sign in.. thats just an ick in 2026. Note to self: maybe help out with their mobile app; its still pretty early in development. |
| Minecraft server | game server for friends | This was the first thing I did. We don't use it anymore, we set it up on another server, but regardless it was a decent experience. 6/10. |
| Portainer | container management/monitoring | Just a cool webUI for managing containers I heard of and wanted to try. |
| Tailscale | VPN | Alternative to port forwarding - no exposed ports. Like my own personal internet on the internet! Cool tech honestly. |

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

- theres only 1 drive, no backups yet
- tailscale isnt as hardened as it can be
- there were more but i forgot them

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
