# 🕵️ Bandit 04

A senha para o próximo nível é armazenada no único arquivo legível no diretório interno . 

*Dica*: se o seu terminal estiver bagunçado, tente o comando “reset”.

## Solução

Listando os arquivos no diretório home
```
bandit4@bandit:~$ ls
inhere
```

Entrando no diretório inhere e listando seus arquivos
```
bandit4@bandit:~$ cd inhere/

bandit4@bandit:~/inhere$ ls
-file00  -file02  -file04  -file06  -file08
-file01  -file03  -file05  -file07  -file09
```

Verificando qual tipo de dado de cada arquivo
```
bandit4@bandit:~/inhere$ file ./-file0*
./-file00: data
./-file01: data
./-file02: data
./-file03: data
./-file04: data
./-file05: data
./-file06: data
./-file07: ASCII text
./-file08: data
./-file09: data
```

Verificando o conteúdo do arquivo ASCII
```
bandit4@bandit:~/inhere$ cat ./-file07 
koReBOKuIDDepwhWk7jZC0RTdopnAYKh
```

Obtemos a flag !

## Conceitos utilizados

- Comando file
- ASCII
- Uso do caractere * para seleção geral


## Links úteis

- https://www.certificacaolinux.com.br/comando-linux-file/
- https://pt.wikipedia.org/wiki/ASCII
- https://linuxize.com/post/linux-file-command/


