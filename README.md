# ansible_machine_rebuild
A repo for Ansible playbooks to rebuild machines

## Machines and Categories

### Mac Mini
+ ~mac-mini~
    + ~tranmission~
        + ~settings.json~
    + ~/etc/fstab~

### Dells
+ haho-services
    + docker_compose
    + /etc/fstab
+ haho-backup
    + /etc/fstab

### Raspberry Pi
+ pi4-4gb-dev
+ garage_pi
+ weather_pi
+ adsb_pi


## Ansible Galaxy Roles

```
ansible-galaxy collection install community.docker
```


## Usage
### `raspi-cam.yaml`

Can comment out various Docker repos. Uses `local_docker_pi` role that installs Docker and allows the an insecure registry on a single IP for local testing.

```
ansible-playbook -i <hostname_or_ip>, raspi-cam.yaml -K --ask-vault-pass
```

