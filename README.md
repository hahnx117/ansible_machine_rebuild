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

## David Desktop
+ Slack
+ Zoom
+ VS Code

### Directories
```
/mnt/backup
/mnt/common_backup
```

### Windows Restoration Steps
1. Boot Windows USB
2. Get to Command Prompt
3. launch `diskpart`
4. select windows disk
5. Either get the disk drive letter or assign one
6. `bcdboot <drive_letter>:\Windows`


### `os-prober` Steps
```
sudo os-prober
sudo grub2-mkconfig -o /etc/grub2-efi.cfg
```

### Packages
```
gstreamer1-plugin-openh264
mozilla-openh264
```

#### Slack
https://slack.com/downloads/linux

#### VS Code
```
sudo rpm --import https://packages.microsoft.com/keys/microsoft.asc

sudo sh -c 'echo -e "[code]\nname=Visual Studio Code\nbaseurl=https://packages.microsoft.com/yumrepos/vscode\nenabled=1\ngpgcheck=1\ngpgkey=https://packages.microsoft.com/keys/microsoft.asc" > /etc/yum.repos.d/vscode.repo'
```

#### Zoom
https://zoom.us/client/5.16.10.668/zoom_x86_64.rpm (11/28/2023)

#### Firefox Videos
```
sudo dnf install gstreamer1-plugin-openh264 mozilla-openh264
```

#### Proton VPN
https://protonvpn.com/support/official-linux-vpn-fedora/

```
wget https://repo.protonvpn.com/fedora-39-stable/protonvpn-stable-release/protonvpn-stable-release-1.0.1-2.noarch.rpm

sudo dnf install ./protonvpn-stable-release-1.0.1-2.noarch.rpm
```

## Kubernetes head node setup

### Kubernetes Repo

```
wget -O- https://packages.cloud.google.com/apt/doc/apt-key.gpg |
    gpg --dearmor |
    sudo tee /etc/apt/keyrings/kubernetes-archive-keyring.gpg > /dev/null
    sudo chmod 644 /etc/apt/keyrings/kubernetes-archive-keyring.gpg
```
`/etc/apt/sources.list.d/kubernetes.list`:
```
deb [signed-by=/etc/apt/keyrings/kubernetes-archive-keyring.gpg] https://apt.kubernetes.io/ kubernetes-xenial main

```


You should now deploy a pod network to the cluster.
Run "kubectl apply -f [podnetwork].yaml" with one of the options listed at:
  https://kubernetes.io/docs/concepts/cluster-administration/addons/

Then you can join any number of worker nodes by running the following on each as root:

kubeadm join 192.168.0.79:6443 --token 4c2rai.gmlrpwtccmuhuwbm \
	--discovery-token-ca-cert-hash sha256:d4a7e82d998032ec08a77404f6fe56b96a71a30fc430013bb23d066d28dccd2a 
