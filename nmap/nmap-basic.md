# NMAP Cheat Sheet

## Port Status

- Open: This indicates that an application is listening for connections on this port.
- Closed: This indicates that the probes were received but there is no application listening on this port.
- Filtered: This indicates that the probes were not received and the state could not be established. It also indicates that the probes are being dropped by some kind of filtering.
- Unfiltered: This indicates that the probes were received but a state could not be established.
- Open/Filtered: This indicates that the port was filtered or open but Nmap couldn’t establish the state.
- Closed/Filtered: This indicates that the port was filtered or closed but Nmap couldn’t establish the state.

## Base nmap Syntax:

```
nmap [ScanType] [Options] {targets}
```
If no port range is specified, Nmap scans the 1,000 most popular ports.

- `nmap -p <port1>-<port2> [IP_Alvo]`: Scans a port range
- `nmap -p <port1>,<port2>,<port#> [IP_Alvo]`: Scans a port list
- `nmap -pU:53,U:110,T20-445 [IP_Alvo]`: Mix TCP and UDP
- `nmap -r [IP_Alvo]`: Scans linearly (does not randomize ports)
- `nmap --top-ports [IP_Alvo]`: Scan n most popular ports
- `nmap -p-65535 [IP_Alvo]`: Leaving off the initial port in range makes Nmap scan start at port 1
- `nmap -p- [IP_Alvo]`: Leaving off the end port in range makes Nmap scan all ports
- `nmap -F [IP_Alvo]`: (Fast (limited port) scan)

## Scan Types

- `nmap -sn [IP_Alvo]`: Probe only (host discovery, not port scan)
- `nmap -sS [IP_Alvo]`: SYN Scan
- `nmap -sT [IP_Alvo]`: TCP Connect Scan
- `nmap -sU [IP_Alvo]`: UDP Scan
- `nmap -sV [IP_Alvo]`: Version Scan
- `nmap -O [IP_Alvo]`: Used for OS Detection/fingerprinting
- `nmap --scanflags [IP_Alvo]`: Sets custom list of TCP using `URG ACK PSH RST SYN FIN` in any order

## Probing Options

- `-Pn`: Don't probe (assume all hosts are up)
- `-PB`: Default probe (TCP 80, 445 & ICMP)
- `-PS<portlist>` : Checks if ssytems are online by probing TCP ports
- `-PE`: Using ICMP Echo Request
- `-PP`: Using ICMP Timestamp Request
- `-PM`: Using ICMP Netmask Request

## Timing Options
- `-T0` (Paranoid): Very slow, used for IDS evasion
- `-T1` (Sneaky): Quite slow, used for IDS evasion
- `-T2` (Polite): Slows down to consume less bandwidth, runs ~10 times slower than default
- `-T3` (Normal): Default, a dynamic timing model based on target responsiveness
- `-T4` (Aggressive): Assumes a fast and reliable network and may overwhelm targets
- `-T5` (Insane): Very aggressive; will likely overwhelm targets or miss open ports

## Output Options

- `-oN`: Standard Nmap output
- `-oG`: Greppable format
- `-oX`: XML format
- `-oA`: <basename> Generate Nmap, Greppable, and XML output files using basename for files
  
 ## Additional Options
 
- `-n`: Disables reverse IP address lookups
- `-6`: Uses IPv6 only
- `-A`: Uses several features, including OS Detection, Version Detection, Script Scanning (default), and traceroute
- `--reason`: Displays the reason Nmap thinks that the port is open, closed, or filtered
