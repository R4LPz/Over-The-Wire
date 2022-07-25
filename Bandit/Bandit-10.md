# 🕵️ Bandit 10

A senha para o próximo nível é armazenada no arquivo data.txt , que contém dados codificados em base64.

## Solução

Listando os arquivos do diretório home:
```
bandit10@bandit:~$ ls
data.txt
```

Verificando o conteúdo do arquivo, obtemos um hash em base64 (verificável pleo padrão da quantidade de caracteres e final com ==) :
```
bandit10@bandit:~$ cat data.txt 
VGhlIHBhc3N3b3JkIGlzIElGdWt3S0dzRlc4TU9xM0lSRnFyeEUxaHhUTkViVVBSCg==
```
Decodificando o arquivo através do comando base64:
```
bandit10@bandit:~$ cat data.txt | base64 -d
The password is IFukwKGsFW8MOq3IRFqrxE1hxTNEbUPR
```

Obtemos a flag! 🥷

## Conceitos utilizados

- O que é criptografia
- O que é um hash
- Algorítmo de hash base64

## Links úteis

- https://pt.wikipedia.org/wiki/Criptografia
- https://pt.wikipedia.org/wiki/Fun%C3%A7%C3%A3o_hash
- https://pt.wikipedia.org/wiki/Base64

