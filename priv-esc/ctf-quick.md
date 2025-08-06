# 1° Scan Nmap 

$sudo nmap -A [Target_IP]

$sudo nmap -Pn -sV -O [Target_IP] -oN report-nmap.txt

$sudo nmap -Pn --script vuln [Target_IP]

$sudo nmap -Pn -p 80 --script http-enum [Target_IP]

$sudo nmap -Pn --script http-robots.txt [Target_IP]

$sudo nmap -Pn -p 21 --script ftp-anon [Target_IP]

# 2° Scan Dirb/Gobuster

$dirb http://example.com -o dirb-report.txt

$gobuster -u http://example.com -w /usr/share/dirb/wordlists/big.txt dir

