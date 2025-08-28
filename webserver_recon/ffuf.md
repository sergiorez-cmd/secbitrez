# ffuf 

sudo apt install seclists -y

## Basic

$ ffuf -u http://10.0.0.123/FUZZ -w /usr/share/wordlists/seclists/Discovery/Web-Content/big.txt

## Find pages and directories

$ ffuf -u http://10.0.0.123/indexFUZZ -w /usr/share/wordlists/seclists/Discovery/Web-Content/web-extensions.txt

$ ffuf -u http://10.0.0.123/FUZZ -w /usr/share/wordlists/seclists/Discovery/Web-Content/raft-medium-words-lowercase.txt -e .php,.txt

$ ffuf -u http://10.0.0.123/FUZZ -w /usr/share/wordlists/seclists/Discovery/Web-Content/raft-medium-directories-lowercase.txt

## Filters

https://en.wikipedia.org/wiki/List_of_HTTP_status_codes

$ ffuf -u http://10.0.0.123/FUZZ -w /usr/share/wordlists/seclists/Discovery/Web-Content/raft-medium-files-lowercase.txt -fc 403

$ ffuf -u http://10.0.0.123/FUZZ -w /usr/share/wordlists/seclists/Discovery/Web-Content/raft-medium-files-lowercase.txt -mc 200

$ ffuf -u http://10.0.0.123/FUZZ -w /usr/share/wordlists/seclists/Discovery/Web-Content/raft-medium-files-lowercase.txt -fr '/\..*'

## Fuzzing parameters

$ ffuf -u 'http://10.0.0.123/sqli-labs/Less-1/?FUZZ=1' -c -w /usr/share/wordlists/seclists/Discovery/Web-Content/burp-parameter-names.txt -fw 39

$ ffuf -u 'http://10.0.0.123/sqli-labs/Less-1/?FUZZ=1' -c -w /usr/share/wordlists/seclists/Discovery/Web-Content/raft-medium-words-lowercase.txt -fw 39

$ ruby -e '(0..255).each{|i| puts i}' | ffuf -u 'http://10.0.0.123/sqli-labs/Less-1/?id=FUZZ' -c -w - -fw 33

$ ruby -e 'puts (0..255).to_a' | ffuf -u 'http://10.0.0.123/sqli-labs/Less-1/?id=FUZZ' -c -w - -fw 33

$ for i in {0..255}; do echo $i; done | ffuf -u 'http://10.0.0.123/sqli-labs/Less-1/?id=FUZZ' -c -w - -fw 33

$ seq 0 255 | ffuf -u 'http://10.0.0.123/sqli-labs/Less-1/?id=FUZZ' -c -w - -fw 33

$ cook '[0-255]' | ffuf -u 'http://10.0.0.123/sqli-labs/Less-1/?id=FUZZ' -c -w - -fw 33

## Brute force

$ ffuf -u http://10.0.0.123/sqli-labs/Less-11/ -c -w /usr/share/wordlists/seclists/Passwords/Leaked-Databases/hak5.txt -X POST -d 'uname=Dummy&passwd=FUZZ&submit=Submit' -fs 1435 -H 'Content-Type: application/x-www-form-urlencoded' 

## Finding vhosts and subdomains

$ ffuf -u http://FUZZ.mydomain.com -c -w /usr/share/wordlists/seclists/Discovery/DNS/subdomains-top1million-5000.txt

$ ffuf -u http://FUZZ.mydomain.com -c -w /usr/share/wordlists/seclists/Discovery/DNS/subdomains-top1million-5000.txt -fs 0

$ ffuf -u http://mydomain.com -c -w /usr/share/wordlists/seclists/Discovery/DNS/subdomains-top1million-5000.txt -H 'Host: FUZZ.mydomain.com' -fs 0

## Proxifying ffuf traffic

Proxy URL (SOCKS5 or HTTP). For example: http://127.0.0.1:8080 or socks5://127.0.0.1:8080

$ ffuf -u http://10.0.0.123/FUZZ -c -w /usr/share/wordlists/seclists/Discovery/Web-Content/common.txt -x http://127.0.0.1:8080

$ ffuf -u http://10.0.0.123/FUZZ -c -w /usr/share/wordlists/seclists/Discovery/Web-Content/common.txt -replay-proxy http://127.0.0.1:8080
