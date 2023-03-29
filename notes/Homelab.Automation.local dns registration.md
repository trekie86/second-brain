---
id: l4sl76z0apcozxcmp6ttocg
title: localdns registration
desc: ''
updated: 1676592097791
created: 1676591418047
---

When new nodes are added to my proxmox cluster, I want to be able to automate, or at least have a single run script that will synchronize my nodes with my local DNS.

My local DNS is provided via [pihole](https://pi-hole.net/).

Example action to remove from the local DNS:
```bash
docker -H "ssh://pi@192.168.4.94" exec -it pihole pihole -a removecustomdns 192.168.4.118 swarm-02
```

Example to add to the local DNS:
```bash
docker -H "ssh://pi@192.168.4.94" exec -it pihole pihole -a addcustomdns 192.168.4.118 swarm-02
```