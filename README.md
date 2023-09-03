# murphywants-ansible-role-application-pihole

Purpose:

```
Image: 'pihole'
src: 'registry.hub.docker.com/pihole/pihole'
tag: latest # unless otherwise specificed in the variables
```

This role will:
- Setup pihole docker container and start it

## Requirements/Dependencies
Uses the following modules:
- community.general
  - community.general.zfs
  - community.general.ufw
- community.docker.docker_compose:

Uses the following roles:
n/a

## Tags
Ansible role template with the following actions & tags:

Tag | Description
--- | ---
Setup/Baseline | Setup the application and apply the configuration baseline
Start | Start required services
Stop | Stop required services
Backup | Run the backup for the component or application or OS
Update | Update the component applications
Remove | Remove configurations and applications
Purge | Remove all configurations and applications relating to the app/component

## Variables
Variable | Default Value | Description
---|---|---
PIHOLE_HTTP_PORT | 8083 | PiHole Admin Page HTTP Port Map
PIHOLE_PATH | '/mnt/pihole' | The location of the container persistent data. A parition will be created and mounted here if the folder doens't exist. 
PIHOLE_STORAGE_ZFS_POOL | 'apps_pool' | The Linux host's ZFS pool name, where the partition will be created from
PIHOLE_STORAGE_ZFS_FS | 'pihole' | The name fo the filesystem that ZFS is creating
PIHOLE_SERVICE_ACCOUNT | 'srv_pihole' | Placeholder service account, todo later
PIHOLE_CONTAINER_VERSION | 'latest' | Can be used to specify specific branch of the container to pull and use
PIHOLE_FQDN | 'pihole.domain.com' | Change this to your fully qualified domain name
PIHOLE_TIMEZONE | "America/New_York" | Timezone of the container


## Example Playbook

playbook.yml
```
- hosts: all 
  gather_facts: yes
  become: yes
  roles:
  - role: murphywants-ansible-role-application-pihole
```

## Example Inventory

static.ini
```
[all]
hostname

[all:vars]
PIHOLE_FQDN="pihole.domain.example.com"
```

# TODO List
- Implement Backups
  - ZFS snapshots
  - Borg
- Implement DNS entries, so I can create a DNS zone from env vars
- Nginx Proxy PiHole Admin Page
