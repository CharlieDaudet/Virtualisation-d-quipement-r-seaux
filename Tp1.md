# TP1 : On r'voit les basics 

## Part 1 : Most simplest LAN
### 3. Know your MAC
🌞 Déterminer l'adresse MAC de vos deux machines

```bash 
VPCS> show

NAME   IP/MASK              GATEWAY           MAC                LPORT  RHOST:PORT
VPCS1  10.1.1.1/24          0.0.0.0           00:50:79:66:68:01  10004  127.0.0.1:10005
       fe80::250:79ff:fe66:6801/64

``` 
```bash
VPCS> show

NAME   IP/MASK              GATEWAY           MAC                LPORT  RHOST:PORT
VPCS1  10.1.1.2/24          0.0.0.0           00:50:79:66:68:00  10002  127.0.0.1:10003
       fe80::250:79ff:fe66:6800/64
```

### 4. IP Setup

🌞 Définir une IP statique sur les deux machines

```bash 

VPCS> ip 10.1.1.1/24
Checking for duplicate address...
PC1 : 10.1.1.1 255.255.255.0


VPCS> ip 10.1.1.2/24
Checking for duplicate address...
PC1 : 10.1.1.2 255.255.255.0

```

🌞 Effectuer un ping d'une machine à l'autre
```bash
VPCS> ping 10.1.1.2
84 bytes from 10.1.1.2 icmp_seq=1 ttl=64 time=0.815 ms
84 bytes from 10.1.1.2 icmp_seq=2 ttl=64 time=1.038 ms
84 bytes from 10.1.1.2 icmp_seq=3 ttl=64 time=0.816 ms
84 bytes from 10.1.1.2 icmp_seq=4 ttl=64 time=1.084 ms
84 bytes from 10.1.1.2 icmp_seq=5 ttl=64 time=0.801 ms

```

```bash
VPCS> ping 10.1.1.1
84 bytes from 10.1.1.1 icmp_seq=1 ttl=64 time=0.818 ms
84 bytes from 10.1.1.1 icmp_seq=2 ttl=64 time=0.944 ms
84 bytes from 10.1.1.1 icmp_seq=3 ttl=64 time=0.805 ms
```

### 5. Analyze

🌞 Protocolz ?

```
ARP
```
📁 [p1_ping.pcap fdghjkl](p1_ping.pcapng)

## Part 2 : Bring that switch in
### 3. Même chose en fast

🌞 Déterminer l'adresse MAC de vos trois machines

```bash 

VPCS> show

NAME   IP/MASK              GATEWAY           MAC                LPORT  RHOST:PORT
VPCS1  10.1.1.1/24          0.0.0.0           00:50:79:66:68:01  10004  127.0.0.1:10005
       fe80::250:79ff:fe66:6801/64
```

```bash 
VPCS> show

NAME   IP/MASK              GATEWAY           MAC                LPORT  RHOST:PORT
VPCS1  10.1.1.2/24          0.0.0.0           00:50:79:66:68:00  10002  127.0.0.1:10003
       fe80::250:79ff:fe66:6800/64

```

```bash 

VPCS> show

NAME   IP/MASK              GATEWAY           MAC                LPORT  RHOST:PORT
VPCS1  10.1.1.3/24          0.0.0.0           00:50:79:66:68:02  10007  127.0.0.1:10008
       fe80::250:79ff:fe66:6802/64
```
🌞 Définir une IP statique sur les trois machines

```bash
VPCS> ip 10.1.1.1/24
Checking for duplicate address...
PC1 : 10.1.1.1 255.255.255.0
```
```bash 
VPCS> ip 10.1.1.2/24
Checking for duplicate address...
PC1 : 10.1.1.2 255.255.255.0
```
```bash 

VPCS> ip 10.1.1.3/24
Checking for duplicate address...
PC1 : 10.1.1.3 255.255.255.0
```
🌞 Effectuer des ping d'une machine à l'autre
```bash 
De node1 
VPCS> ping 10.1.1.2
84 bytes from 10.1.1.2 icmp_seq=1 ttl=64 time=2.064 ms
84 bytes from 10.1.1.2 icmp_seq=2 ttl=64 time=3.564 ms
84 bytes from 10.1.1.2 icmp_seq=3 ttl=64 time=3.005 ms

VPCS> ping 10.1.1.3
84 bytes from 10.1.1.3 icmp_seq=1 ttl=64 time=2.088 ms
84 bytes from 10.1.1.3 icmp_seq=2 ttl=64 time=3.755 ms

De node2 

VPCS> ping 10.1.1.3
84 bytes from 10.1.1.3 icmp_seq=1 ttl=64 time=1.557 ms
84 bytes from 10.1.1.3 icmp_seq=2 ttl=64 time=3.002 ms

```
### 4. ARP old friend

🌞 Afficher la table ARP de node1

```bash 
VPCS> show arp

00:50:79:66:68:00  10.1.1.2 expires in 92 seconds
00:50:79:66:68:02  10.1.1.3 expires in 114 seconds
```

📁 [p2_arp_node2.pcap ejf](./p2_arp_node2.pcapng)

📁 [p2_arp_node3.pcap djqgf](./p2_arp_node3.pcapng)

## Part 3 : DHCP is a nice guy
### 3. Setuuuup
🌞 Installer un serveur DHCP

```bash 
[root@efrei-xmg4agau1 ~]# dnf -y install dnsmasq

[root@dhcp ~]# sudo vim /etc/dnsmasq.conf

[root@efrei-xmg4agau1 ~]# systemctl enable --now dnsmasq

[root@efrei-xmg4agau1 ~]# firewall-cmd --add-service=dns
success

[root@efrei-xmg4agau1 ~]# firewall-cmd --runtime-to-permanent
success

[root@efrei-xmg4agau1 ~]# systemctl restart dnsmasq
[root@efrei-xmg4agau1 ~]# systemctl status dnsmasq
● dnsmasq.service - DNS caching server.
     Loaded: loaded (/usr/lib/systemd/system/dnsmasq.service; enabled; preset: disabled)
     Active: active (running) since Tue 2026-01-06 14:26:30 CET; 3s ago
 Invocation: 046bffd36e4e4c0f879f8915f6cfc72f
    Process: 2054 ExecStart=/usr/sbin/dnsmasq (code=exited, status=0/SUCCESS)
   Main PID: 2056 (dnsmasq)
      Tasks: 1 (limit: 10643)
     Memory: 608K (peak: 1.2M)
        CPU: 14ms
     CGroup: /system.slice/dnsmasq.service
             └─2056 /usr/sbin/dnsmasq

janv. 06 14:26:30 efrei-xmg4agau1.etudiants.campus.villejuif systemd[1]: Starting dnsmasq.service - DNS caching server.>
janv. 06 14:26:30 efrei-xmg4agau1.etudiants.campus.villejuif dnsmasq[2056]: started, version 2.90 cachesize 150
janv. 06 14:26:30 efrei-xmg4agau1.etudiants.campus.villejuif dnsmasq[2056]: DNS service limited to localhost
janv. 06 14:26:30 efrei-xmg4agau1.etudiants.campus.villejuif dnsmasq[2056]: compile time options: IPv6 GNU-getopt DBus >
janv. 06 14:26:30 efrei-xmg4agau1.etudiants.campus.villejuif dnsmasq-dhcp[2056]: DHCP, IP range 10.1.1.10 -- 10.1.1.50,>
janv. 06 14:26:30 efrei-xmg4agau1.etudiants.campus.villejuif dnsmasq[2056]: reading /etc/resolv.conf
janv. 06 14:26:30 efrei-xmg4agau1.etudiants.campus.villejuif dnsmasq[2056]: using nameserver 172.26.129.138#53
janv. 06 14:26:30 efrei-xmg4agau1.etudiants.campus.villejuif dnsmasq[2056]: using nameserver 172.26.129.139#53
janv. 06 14:26:30 efrei-xmg4agau1.etudiants.campus.villejuif dnsmasq[2056]: read /etc/hosts - 8 names
janv. 06 14:26:30 efrei-xmg4agau1.etudiants.campus.villejuif systemd[1]: Started dnsmasq.service - DNS caching server..
```
### 4. Proof or you're lying
🌞 Récupérer une IP automatiquement depuis les 3 nodes
```bash

VPCS> ip dhcp
DDORA IP 10.1.1.48/24 GW 10.1.1.253

VPCS> show

NAME   IP/MASK              GATEWAY           MAC                LPORT  RHOST:PORT
VPCS1  10.1.1.48/24         10.1.1.253        00:50:79:66:68:03  10004  127.0.0.1:10005
       fe80::250:79ff:fe66:6803/64
```
```bash

VPCS> ip dhcp
DDORA IP 10.1.1.47/24 GW 10.1.1.253

VPCS> show

NAME   IP/MASK              GATEWAY           MAC                LPORT  RHOST:PORT
VPCS1  10.1.1.47/24         10.1.1.253        00:50:79:66:68:02  10006  127.0.0.1:10007
       fe80::250:79ff:fe66:6802/64

```

```bash
VPCS> ip dhcp
DDORA IP 10.1.1.46/24 GW 10.1.1.253

VPCS> show

NAME   IP/MASK              GATEWAY           MAC                LPORT  RHOST:PORT
VPCS1  10.1.1.46/24         10.1.1.253        00:50:79:66:68:01  10008  127.0.0.1:10009
       fe80::250:79ff:fe66:6801/64

```

📁 [p3_dhcp.pcap djvfe](p3_dhcp.pcapng)

### 5. DHCP lease

🌞 Bail DHCP

```bash
[root@dhcp ~]# cd ..
[root@dhcp /]# cd var/lib/dnsmasq
[root@dhcp dnsmasq]# ls
dnsmasq.leases
[root@dhcp dnsmasq]# vim dnsmasq.leases

1767752432 00:50:79:66:68:01 10.1.1.46 * 01:00:50:79:66:68:01
1767752419 00:50:79:66:68:02 10.1.1.47 * 01:00:50:79:66:68:02
1767752661 00:50:79:66:68:03 10.1.1.48 VPCS1 01:00:50:79:66:68:03
~
~
``` 
🌞 Use grep

```bash
[root@dhcp /]# cat var/lib/dnsmasq/dnsmasq.leases | grep VPCS1
1767752661 00:50:79:66:68:03 10.1.1.48 VPCS1 01:00:50:79:66:68:03
```

## Part 4 : real haxor
### 1. DHCP spoofing

🌞 Installez et configurez un serveur DHCP sur votre machine attaquante
```bash 
[root@rogue ~]# sudo dnf install -y vim

[root@rogue ~]# sudo vim /etc/dnsmasq.conf

[root@rogue ~]# systemctl enable --now dnsmasq

[root@rogue ~]# sudo firewall-cmd --add-service=dhcp
success
[root@rogue ~]# sudo firewall-cmd --add-service=dhcp --permanent
success

[root@rogue ~]# systemctl restart dnsmasq
[root@rogue ~]# systemctl status dnsmasq
● dnsmasq.service - DNS caching server.
     Loaded: loaded (/usr/lib/systemd/system/dnsmasq.service; enabled; preset: disabled)
     Active: active (running) since Tue 2026-01-06 17:11:00 CET; 10s ago
 Invocation: 456632f958be40ee8d0b24cc848f14d9
    Process: 2079 ExecStart=/usr/sbin/dnsmasq (code=exited, status=0/SUCCESS)
   Main PID: 2081 (dnsmasq)
      Tasks: 1 (limit: 10643)
     Memory: 612K (peak: 1.2M)
        CPU: 55ms
     CGroup: /system.slice/dnsmasq.service
             └─2081 /usr/sbin/dnsmasq

janv. 06 17:11:00 rogue.tp1.efrei systemd[1]: Starting dnsmasq.service - DNS caching server....
janv. 06 17:11:00 rogue.tp1.efrei dnsmasq[2081]: started, version 2.90 cachesize 150
janv. 06 17:11:00 rogue.tp1.efrei dnsmasq[2081]: compile time options: IPv6 GNU-getopt DBus no-UBus i18n IDN2 DHCP DHCPv6 no-Lua TFTP conntrack ipset no-nf>
janv. 06 17:11:00 rogue.tp1.efrei dnsmasq-dhcp[2081]: DHCP, IP range 10.1.1.210 -- 10.1.1.250, lease time 12h
janv. 06 17:11:00 rogue.tp1.efrei dnsmasq[2081]: reading /etc/resolv.conf
janv. 06 17:11:00 rogue.tp1.efrei dnsmasq[2081]: using nameserver 172.26.129.138#53
janv. 06 17:11:00 rogue.tp1.efrei dnsmasq[2081]: using nameserver 172.26.129.139#53
janv. 06 17:11:00 rogue.tp1.efrei dnsmasq[2081]: read /etc/hosts - 8 names
janv. 06 17:11:00 rogue.tp1.efrei systemd[1]: Started dnsmasq.service - DNS caching server..
lines 1-21/21 (END)
```

🌞 Test !  

```bash 

VPCS> ip dhcp
DDORA IP 10.1.1.247/24 GW 10.1.1.33
```
#### B. Race!

📁 [p4_dhcp_race.pcap](p4_dhcp_race.pcapng)

### 3. ARP poisoning

#### A. Simple poisoning

🌞 Proof !

```bash 
VPCS> arp

arp table is empty

``` 
```bash 

[root@rogue ~]# sudo arping -c 1 -U -s 10.1.1.34 -I enp0s8 10.1.1.248
arping: bind: Ne peut attribuer l'adresse demandée

[root@rogue ~]# sudo sysctl net.ipv4.ip_nonlocal_bind=1
net.ipv4.ip_nonlocal_bind = 1
[root@rogue ~]# sudo arping -c 1 -U -s 10.1.1.34 -I enp0s8 10.1.1.248
ARPING 10.1.1.248 de 10.1.1.34 enp0s8
1 sondes envoyées (1 diffusion(s))
0 réponse(s) reçue(s)
```

```bash 
VPCS> arp

08:00:27:77:c4:e6  10.1.1.34 expires in 111 seconds

```
📁 [p4_poisoning.pcap](p4_poisoning.pcapng)

#### B. MITM