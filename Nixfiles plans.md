# Deployment long-term

* Make colmena, but not shit?
	* Handle flakes properly
	* Handle tags/nodegroups properly
	* Handle remote building

Core ideas:
* stateless
* decentralized


* it should be easy to choose where each host builds, whether local, distributed/remote, ...?
* it should be easy to deploy every host, or a single host, or a group of hosts
* it should be easy to make these decisions at build time with configuration, or at deploy time with switches to override

Wants:
* despite statelessness, record time of last deploy; provide a CI job that notifies warnings about duration since last upload
# Redo caching / CI
* Node cache
* Shell cache?
* Profile cache?
* Program specific cache?
* CUDA support builds?

## To-do
* figure out why CI jobs do not work anymore
* set cachix back up
# Services

* crab-hole
* Anubis
* freshrss 
* Forgejo
	* Proper sync from GItHub account
* Suwayomi-Server
* pict-rs maybe?
* Prosody
* Akkoma?
* Authentik?
	* https://github.com/nix-community/authentik-nix

# Other plans

Start using NixOS containers
Look into microvm.nix / https://github.com/microvm-nix/microvm.nix/tree/main
Make use of daiyousei and the two small AMD boxes?
Make syncthing actually work?
Check out if the backups saved to the storagebox actually work
Make a jumpbox
Make a GUI VM - Proxmox, somewhere?
Start using disko where I can

Start using lanzaboote on koishi and goliath

# Pinkie 

>>> i've been thinking about.... a reasonably operator-friendly(ymmv?) "distributed" runtime(?) for use as a  post-closure-deployment agent (with potential for being given knowledge of the actual configuration / closure / ...) over the last few days and staring at elixir and its distributed tasks ...

Two sides:
* Presentation (Server)
* Agents (Client)

## Identity

* Figure out how to integrate with Authentik natively

## An exploration

If one were to write nix modules to create JSON output from your flake for Pinkie to intake, one could trivially give dashy data about all of your services, their domains, ... ahead of time, to set up monitoring in config.

## Host list

Profiles the host:
* for NixOS and nix-darwin hosts, check closure build dates, how old packages are?
* OS
* kernel string
* IP, GeoIP, IPv6
* uptime
* cpu
* gpu
* swap
* memory status
* locales
* timezone
* displays
* installed programs
	* terminal
	* graphical / .desktop files
* current X11/wayland state,
* run directories,
* network information

This information is provided to the server.
## Central container(s) and MicroVM(s) panel

* Associated per host?
* Health?
* IP addresses within their local network(?)
* Domains?
* Disk usage?
* Memory usage?
* Bound paths?
* Network usage?

## Network circumstances

* VPN status(?)
* Location / GeoIP
* IP, IPv6
## PostgreSQL

* Database size viewing
* Database size alerting

## Systemd Services
## Filesystem

Central place for managing other disk related modules

* Alerting about filesystem paths getting increasingly large
	* Associate them with services, potentially?
### ZFS, BTRFS

* Alerting about degraded filesystem(s)
### RAID

* Alerting about degraded RAID.
### SMART

* Alerting about drive health.

## Per-host, container and MicroVM terminal option

# Architecture

## To-dos
* Write your own dashboard? You could use grafana for service monitoring but like...
* Sunshine ?
* Rethink notification source(s)
* Successful login notifications for servers
* Rethink email
* fail2ban
	* SSH
* Notifications for disk usage of
	* databases
	* services
* Have a proper monitoring / a consistent dashboard for things? Collect data.
	* Syslog server?
	* Prometheus capture???
	* Alerting
* DB MicroVM
	* Set up TLS?
	* Password per user as secret per service?
* DNS MicroVM
	* What will our upstream be? Not cloudflare?
	* Caching?
## Host: Daiyousei

### DB MicroVM (cloud-hypervisor)

Contains:
* postgres
### DNS MicroVM (cloud-hypervisor)

Contains:
* crab-hole
### Auth MicroVM (cloud-hypervisor)

Contains:
* Authentik via authentik-nix

### Monitoring(?) MicroVM (cloud-hypervisor)

Contains:
* ?
### Anubis Container (nixos)

Prevent AI scraping.

Contains:
* Anubis
### Forgejo Container (nixos)

Provide an alternative to GitHub.

Contains:
* forgejo instance

### Prosody Container (nixos)

XMPP

Contains:
* prosody instance
### FreshRSS Container (nixos)

RSS :3

Reddit?
hacker news
lobsters
...

Contains:
* FreshRSS instance

## Host: Mei

VPN + Jumpbox?

## Host: Mai
