# :cloud: Self hosted swarm

A straight-forward, simple to deploy, Docker swarm with GlusterFS.

## Feature overview

- Ansible scripts to provision servers
- Vagrant script to provision VMs for local testing
- GlusterFS as shared file system (1 or 3+ nodes required)
- Reverse proxy to hide your home IP address
- Locked down firewall

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

## Getting started

The easiest way to get started with this project, is to start the virtual machines using Vagrant. After that, run the ansible playbook "up" to provision the right software to the right machines. This will bring up a proxy, a swarm manager and a swarm worker.

```sh
vagrant up
cp playbooks/config.example.yml playbooks/config.yml
ansible-playbook -i hosts-vagrant playbooks/up.yml
```

## Future functionality

- Highly available applications
- Private network between nodes
- VPN to access internal services
- Internal services
	- Traefik
	- Portainer
	- Prometheus
	- Grafana
- GitHub Actions pipeline to build images and deploy services
