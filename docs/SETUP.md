You can implement this setup on any hardware capable of running an Ubuntu server reliably.

My hardware consists of:

```
1. A spare laptop that is plugged in 24/7.
2. An ethernet cable connected to the laptop and my router. (recommended over using Wi-Fi)
3. A personal computer to manage the AdGuard dashboard.
```

Operating System, files, and software used:

```
1. Ubuntu server (with encryption enabled) https://ubuntu.com/download/server
2. Docker (sudo apt install -y docker.io docker-compose-v2) or https://www.docker.com/products/docker-desktop/
3. Netplan (pre installed with Ubuntu server)
4. Systemd (pre installed with Ubuntu server)
5. Vlock (sudo apt install -y vlock)
```

QoL configurations:

Since I am using a laptop, I disabled lid-switch actions using ```sudo nano /etc/systemd/logind.conf``` and setting ```HandleLidSwitch=ignore``` before uncommenting it. Afterwards I used ```sudo systemctl mask sleep.target suspend.target hibernate.target hybrid-sleep.target``` to prevent Ubuntu from entering power-saving modes completely, and restarted the power service by using ```sudo systemctl restart systemd-logind```

Docker:

I installed docker using ```sudo apt update && sudo apt install -y docker.io docker-compose-v2``` and created a directory to work within ```mkdir -p ~/homelab/adguard && cd ~/homelab/adguard```, afterwards I configured ```docker-compose.yml``` and launched it using ```docker compose up -d```. You can find the configuration I used under the docker directory in this repository.

Netplan:

I used Netplan to always give my laptop the same IP address upon boot (optional step). This can also be done using your router's DHCP IP Reservation settings. You can find my configuration for ```/etc/netplan/50-cloud-init.yaml``` under the netplan directory. Then I fixed the file permissions using ```sudo chmod 600 /etc/netplan/*.yaml``` and ```sudo chown root:root /etc/netplan/*.yaml``` and applied everything using ```sudo netplan apply```

Physical security:

First, I disabled ctrl+alt+delete interrupts using ```sudo systemctl mask ctrl-alt-del.target``` and ```sudo systemctl daemon-reload``` afterwards. And I also installed vlock to lock my terminal screen using ```sudo apt install -y vlock```.

AdGuard dashboard:

After following through the 5 step setup guide given to you by AdGuard, I went to DNS Settings and implemented these 3 upstream DNS servers.

```
https://dns.cloudflare-dns.com/dns-query
https://dns.quad9.net/dns-query
tls://dns.adguard-dns.com
```

Afterwards, I went to filters and added specific blocklists to my DNS blocklists using the existing list AdGuard offers.

Router settings:

After the initial set up, I went to my router's settings and put my laptop's IPv4 and IPv6 as my DNS server.