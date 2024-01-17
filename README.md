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

The following software is only required when deploying locally

- Ruby
- Vagrant
- dnsmasq
- Brew (only when you need mkcert)
- [mkcert](https://github.com/FiloSottile/mkcert) (only when deploying in Vagrant)

## Getting started

The easiest way to get started with this project, is to start the virtual machines using Vagrant. After that, run the ansible playbook "up" to provision the right software to the right machines. This will bring up a proxy, a swarm manager and two swarm workers. We need the second worker to have consensus in Gluster.

```sh
vagrant up
cp playbooks/config.example.yml playbooks/config.yml
ansible-playbook -i hosts-vagrant playbooks/up.yml
```

If you deploy this project locally, it means that TLS certificates from Let's Encrypt are not available and you need to supply your own certificates. Luckily, this is pretty easy to do with [mkcert](https://github.com/FiloSottile/mkcert). Install mkcert, generate a root certificate authority and generate a TLS certificate that supports your local domain.

```sh
brew install mkcert
mkcert -install
mkcert -cert-file playbooks/roles/stacks/files/traefik/local-certificates/global.crt \
	-key-file  playbooks/roles/stacks/files/traefik/local-certificates/global.key \
	"*.domain.test" domain.test 10.10.10.10
	
```

Use dnsmasq to point `domain.test` to your local host:

```sh
sudo su -c 'echo "address=/.test/10.10.10.10" >> /etc/dnsmasq.conf'
```

## Future functionality

- Better documentation
- Highly available applications
- Private network between nodes
- VPN to access internal services
- Internal services
	- Traefik
	- Portainer
	- Prometheus
	- Grafana
- GitHub Actions pipeline to build images and deploy services
