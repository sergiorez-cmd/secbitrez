## Instalar Nuclei
```
sudo apt update
```
``` 
sudo apt install -y golang-go
``` 
```
go install -v github.com/projectdiscovery/nuclei/v3/cmd/nuclei@latest
```
## Inserir variável de ambiente 

$ nano ~/.zshrc

export PATH="$PATH:/home/kali/go/bin"

$ reset

$ nuclei --help

$ nuclei -update-templates

$ nuclei -u https://scanme.sh -o scan-report.txt

$ nuclei -u https://scanme.sh -t dns

$ nuclei -u https://scanme.sh -t cves

$ nuclei -u https://scanme.sh -severity critical

$ nuclei -u https://scanme.sh -tags tech,xss
