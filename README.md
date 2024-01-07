# :cloud: Private cloud

A straight-forward, simple to deploy, Docker swarm cluster with GlusterFS.

## Feature overview

- Ansible scripts to provision servers
- Vagrant script to provision VMs for local testing

Planned features are [listed below](#future-functionality)

## Requirements

### Hardware

- 1 VPS (as proxy)
- 3 (or more) Raspberry Pis (64 bit)
- 3 (or more) micro SD cards
- 3 (or more) PoE+ HATs
- 3 (or more) Ethernet cables
- 1 Network switch

### Software

The software listed below should be available on your development machine.

- Git
- An SSH client
- Ansible
- Docker (if you want to test images locally)
- Ruby
- Vagrant

## Future functionality

- Locked down firewall (only necessary ports open)
- Reverse proxy to hide your home IP address
- Highly available applications
- GlusterFS as shared file system (3 swarm nodes required)
- VPN to access internal services
- Internal services
	- Traefik
	- Portainer
	- Prometheus
	- Grafana
- GitHub Actions pipeline to build images and deploy services