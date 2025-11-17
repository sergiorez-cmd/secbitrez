## Instalar Nuclei

$ sudo apt update

$ sudo apt install -y golang-go

$ go install -v github.com/projectdiscovery/nuclei/v3/cmd/nuclei@latest

## Inserir variável de ambiente 

$ subl ~/.zshrc

export PATH="$PATH:/home/kali/go/bin"

$ reset

$ nuclei --help

$ nuclei -u https://scanme.sh
