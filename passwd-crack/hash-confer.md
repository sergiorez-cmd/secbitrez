```
#!/usr/bin/python3

print ("Comparar Hash de arquivos para confirmar integridade do arquivo")

print ("Para obter Hash dos arquivos digite no shell:")

print ("$m5sum none-do-arquiv.exe")

print ("$sha1sum none-do-arquiv.exe")

print ("$sha256sum none-do-arquiv.exe")

hash1 = input ("Insira o Hash gerado no Shell :")

hash2 = input ("Insira o Hash obtido no site oficial :")

if hash1 == hash2:
    
    print("Hash Confirmado com Sucesso, Arquivo Seguro")

else:
    
    print("Hash Suspeito ou Inseguro, Delete o Arquivo")
```
