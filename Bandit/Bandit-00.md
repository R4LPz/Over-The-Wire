# 🕵️ Bandit 00

O objetivo deste nível é fazer login no jogo usando SSH.
O host ao qual você precisa se conectar é *bandit.labs.overthewire.org*, na porta 2220. 
O nome de usuário é bandit0 e a senha é bandit0 . Uma vez logado, vá para a página do Nível 1 para descobrir como vencer o Nível 1.

## Solução

Realizando a conexão remota com o servidor
```
ssh -p 2220 bandit.labs.overthewire.org
```

Listando os arquivos no diretório home:
```
bandit0@bandit:~$ ls
readme
```

Verificando o conteúdo do arquivo readme:
```
bandit0@bandit:~$ cat readme
boJ9jbbUNNfktd78OOpsqOltutMc3MY1
```

Obtemos a flag! 🥷

## Conteitos utilizados

- SSH 
- Uso básico do terminal linux

## Links úteis

- https://en.wikipedia.org/wiki/Secure_Shell
- http://wiki.inf.ufpr.br/maziero/doku.php?id=unix:comandos_basicos
