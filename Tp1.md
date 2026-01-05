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
