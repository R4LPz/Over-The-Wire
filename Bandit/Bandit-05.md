# 🕵️ Bandit 00

A senha para o próximo nível é armazenada em um arquivo em algum lugar no diretório inhere e possui todas as seguintes propriedades:

- legível por humanos
- 1033 bytes de tamanho
- não executável

## Solução

Listando todos os arquivos no diretório home:
```
bandit5@bandit:~$ ls
inhere
```

Verificando os arquivos dentro do diretório inhere:
```
bandit5@bandit:~$ cd inhere/

bandit5@bandit:~/inhere$ ls
maybehere00  maybehere04  maybehere08  maybehere12  maybehere16
maybehere01  maybehere05  maybehere09  maybehere13  maybehere17
maybehere02  maybehere06  maybehere10  maybehere14  maybehere18
maybehere03  maybehere07  maybehere11  maybehere15  maybehere19
```

Buscando por um arquivo do tipo file, com 1033 bytes de tamanho e que não seja executável através do comando find:
```
bandit5@bandit:~/inhere$ find ./ -type f -size 1033c ! -executable
./maybehere07/.file2
```

Verificando o conteúdo do arquivo retornado na consulta anterior:
```
bandit5@bandit:~/inhere$ cat ./maybehere07/.file2 
DXjZPULLxYr17uwoI01bNLQbtFemEgo7
```

Obtemos a flag! 🥷

## Comandos utilizados 

- Comando find
- Como os arquivos tem seu tamanho medido?
- Operador de negação !


## Links úteis

- manual do comando find através de `find --help` ou `man find`
- https://guialinux.uniriotec.br/find/

