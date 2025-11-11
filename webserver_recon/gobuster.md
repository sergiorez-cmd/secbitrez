$ gobuster dir -u http://example.com -w /usr/share/dirb/wordlists/common.txt -o dir-report.txt

$ gobuster dir -u http://example.com -w /usr/share/dirb/wordlists/big.txt -t 4 --delay 3s -a "Mozilla/5.0"

$ gobuster dir -u http://example.com -w /usr/share/dirb/wordlists/big.txt -x php,html,js,txt,zip --random-agent -t 4 -o dir-report.txt

$ gobuster dns --domain example.com -w wordlist-dns.txt --no-error -t 2

$ gobuster dns -q -r 8.8.8.8 -d https://example.com -w /usr/share/wordlists/seclists/Discovery/DNS/subdomains-top1million-5000.txt

$ gobuster vhost -u https://example.com -w /usr/share/wordlists/seclists/Discovery/DNS/bitquark-subdomains-top100000.txt -o subdom.report.txt

$ gobuster dir -u https://wdsapp.corpnetwork.com.br/wdsapp/ -w /usr/share/seclists/Discovery/Web-Content/common-and-portuguese.txt --random-agent -x php -o wdsapp-dir.txt
