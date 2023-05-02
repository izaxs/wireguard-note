# WireGuard Note
_Setup your own VPN elegantly_

## The Old Manual Way: WireGuard Guide
To learn how to manually setup, check [WIREGUARD.md](WIREGUARD.md)

## The Tailscale Way: 2023 Update
It's significantly easier to setup a VPN exit node server with Tailscale

### Tailscale Signup
Follow [Tailscale's official guide](https://tailscale.com/kb/1017/install/#step-1-sign-up-for-an-account) to signup

### Setup SSH on Server
Suggestion: Before working on WireGuard, setup SSH on client with alias, so you can easily manage the server later

[SSH server guide](HOWTOSSH.md)

Following commands assume the server OS is Debian Bullseye

### Setup APT Repo
```
curl -fsSL https://pkgs.tailscale.com/stable/debian/bullseye.noarmor.gpg | sudo tee /usr/share/keyrings/tailscale-archive-keyring.gpg >/dev/null
curl -fsSL https://pkgs.tailscale.com/stable/debian/bullseye.tailscale-keyring.list | sudo tee /etc/apt/sources.list.d/tailscale.list
```

### Install Tailscale
```
sudo apt-get update
sudo apt-get install tailscale
```

### Setup Linux Packet Forwarding Rule
```
echo 'net.ipv4.ip_forward = 1' | sudo tee -a /etc/sysctl.d/99-tailscale.conf
echo 'net.ipv6.conf.all.forwarding = 1' | sudo tee -a /etc/sysctl.d/99-tailscale.conf
sudo sysctl -p /etc/sysctl.d/99-tailscale.conf
```

### Run Tailscale
```
sudo tailscale up --advertise-exit-node
```
An auth link will show up after this command, paste it into your browser to finish the authentication

### Manage Joined Device

Use [Tailscale Admin Console](https://login.tailscale.com/admin/machines) to manage your network

### Reference:

[Setting up Tailscale on Linux](https://tailscale.com/kb/1031/install-linux/)

[Exit Nodes](https://tailscale.com/kb/1103/exit-nodes/)
