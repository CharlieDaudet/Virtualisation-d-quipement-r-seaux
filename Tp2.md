# TP2 Part1 : Network Setup

## 7. Proof or lie
🌞 Tout le monde doit pouvoir se ping
```bash 
node 1: 

VPCS> ping 10.2.1.12
84 bytes from 10.2.1.12 icmp_seq=1 ttl=64 time=2.017 ms
84 bytes from 10.2.1.12 icmp_seq=2 ttl=64 time=2.022 ms
84 bytes from 10.2.1.12 icmp_seq=3 ttl=64 time=1.522 ms


VPCS> ping 10.2.2.11
84 bytes from 10.2.2.11 icmp_seq=1 ttl=63 time=32.087 ms
84 bytes from 10.2.2.11 icmp_seq=2 ttl=63 time=15.479 ms

``` 
```bash
node3
VPCS> ping 10.2.2.12
84 bytes from 10.2.2.12 icmp_seq=1 ttl=64 time=2.378 ms
84 bytes from 10.2.2.12 icmp_seq=2 ttl=64 time=2.258 ms
84 bytes from 10.2.2.12 icmp_seq=3 ttl=64 time=1.635 ms
```

```bash
node4 

VPCS> ping 10.2.1.12
84 bytes from 10.2.1.12 icmp_seq=1 ttl=63 time=39.825 ms
84 bytes from 10.2.1.12 icmp_seq=2 ttl=63 time=21.696 ms
```

📁 [p1_routed_ping.pcap](p1_routed_ping.pcapng)

# TP2 Part2 : C'est mieux avec internet
### 1. Accès internet routeur

🌞 Prouver que...
```bash 

r1tp2efrei#ping 1.1.1.1

Type escape sequence to abort.
Sending 5, 100-byte ICMP Echos to 1.1.1.1, timeout is 2 seconds:
!!!!!
Success rate is 100 percent (5/5), round-trip min/avg/max = 24/32/48 ms

```
```bash 

VPCS> ping 1.1.1.1
1.1.1.1 icmp_seq=1 timeout
1.1.1.1 icmp_seq=2 timeout
1.1.1.1 icmp_seq=3 timeout
```

📁 [p1_no_nat.pcap](p1_no_nat.pcapng)

### 2. Accès internet clients
🌞 Proooooooooof or lie

```bash 
VPCS> ping 1.1.1.1
84 bytes from 1.1.1.1 icmp_seq=1 ttl=253 time=50.673 ms
84 bytes from 1.1.1.1 icmp_seq=2 ttl=253 time=43.696 ms
84 bytes from 1.1.1.1 icmp_seq=3 ttl=253 time=34.872 ms
```
📁 [p1_nat.pcap](p1_nat.pcapng)

📁 [r1_running_config.txt](r1_running_config.txt)
