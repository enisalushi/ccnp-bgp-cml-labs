# BGP Packet Captures

This folder contains Wireshark packet captures from the Cisco CML BGP lab.

The captures were taken on the eBGP link between:

- R2 — AS65002 — 10.23.23.1
- R3 — AS65003 — 10.23.23.2

## Captures

### 01-bgp-session-establishment.pcap

Demonstrates the complete BGP session establishment process:

- TCP SYN / SYN-ACK / ACK
- TCP port 179
- TCP MD5 authentication
- BGP OPEN messages
- BGP KEEPALIVE messages
- BGP UPDATE messages

The BGP OPEN message shows:

- BGP Version 4
- AS65002
- Hold Time 30 seconds
- BGP Router ID 2.2.2.2

---

### 02-bgp-prefix-advertise-withdraw.pcap

Demonstrates the advertisement and withdrawal of:

`172.16.70.0/24`

During the advertisement, the BGP UPDATE contains:

- ORIGIN: IGP
- AS_PATH: 65003
- NEXT_HOP: 10.23.23.2
- NLRI: 172.16.70.0/24

During the withdrawal, the same prefix appears under:

`Withdrawn Routes`

with no path attributes required.

## Useful Wireshark Filters

```text
bgp
tcp.port == 179
bgp.type == 1
bgp.type == 2
ip.addr == 10.23.23.1 && ip.addr == 10.23.23.2
