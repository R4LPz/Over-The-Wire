# 🕵️ Bandit 03

## Solução

Listando os arquivos no diretório home:
```
bandit3@bandit:~$ ls
inhere
```

Entrando no diretório inhere e listando seus arquivos:
```
bandit3@bandit:~$ cd inhere/

bandit3@bandit:~/inhere$ ls
```

Listando os arquivos ocultos:
```
bandit3@bandit:~/inhere$ ls -la
total 12
drwxr-xr-x 2 root    root    4096 May  7  2020 .
drwxr-xr-x 3 root    root    4096 May  7  2020 ..
-rw-r----- 1 bandit4 bandit3   33 May  7  2020 .hidden
```

Verificando o conteúdo do arquivo .hidden:
```
bandit3@bandit:~/inhere$ cat .hidden 
pIwrPrtPN36QITSp3EQaw936yaFoFgAB

```

Obtemos a flag! 🥷

## Conceitos utilizados

- Arquivos ocultos
- Comando ls

## Links úteis

- Executar o manual do ls com o comando `ls --help`
- https://phoenixnap.com/kb/show-hidden-files-linux

