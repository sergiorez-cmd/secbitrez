## Kali Tools Sub Domains

https://www.kali.org/tools/subfinder
```
sudo apt install -y subfinder
```
$ subfinder -ls

$ subfinder -d example.com -cs -o sub-domains.txt
```
sudo apt install -y httprobe httpx-toolkit
```
```
cat sub-domains.txt | httpprobe
```
```
httpx-toolkit -l sub-domains.txt
```
