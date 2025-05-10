# Ansible with Proxmox

I use a dynamic Proxmox inventory in combination with Ansible to perform various tasks, such as updating all my LXC containers or pulling and running `docker-compose.yml` files from a repository.

To create groups I tag my Proxmox hosts with different tags for example 'Script, Docker, Network'.

For testing purposes all playbooks run on `host: all` so remember to provide a `-l TAG` to limit the range of the playbook

---

## Setup

1. Edit `ansible.cfg` according to your environment.
2. Provide your Proxmox URL and token in `/inventory/hosts.proxmox.yml/`.
3. Provide your `/vault/env/.env` files and `/inventory/group_vars/.yml` files.
4. Optional: Modify `example.vault_pass.txt` and provide your vault password.
5. Optional: Use `ansible-vault encrypt /path/to/file.yml --vault-password-file /path/to/vault_password.txt` to encrypt sensitive data.

---

## Usage

Run a playbook:

`ansible-playbook -i /path/to/hosts.proxmox.yml path/to/playbook.yml/`

Run a playbook on a single tag for example 'Docker':

`ansible-playbook -i /path/to/hosts.proxmox.yml path/to/playbook.yml/` -l Docker

List all of your inventory:
` ansible-inventory /path/to/hosts.proxmox.yml --list` 

Filter your inventory for a single host:
` ansible-inventory /path/to/hosts.proxmox.yml --host NAME`
 