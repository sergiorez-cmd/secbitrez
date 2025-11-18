## Kali Tools Sub Domains

https://www.kali.org/tools/subfinder
```
sudo apt install -y subfinder
```
$ subfinder -ls

$ subfinder -d example.com --silent

$ subfinder -d example.com -o sub-domains.txt

$ subfinder -d example.com -cs
```
sudo apt install -y httprobe httpx-toolkit
```
```
cat sub-domains.txt | httprobe | tee sub-online.txt
```
```
httpx-toolkit -l sub-domains.txt
```
