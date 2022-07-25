# 🕵️ Bandit 06

A senha para o próximo nível está armazenada em algum lugar no servidor e possui todas as seguintes propriedades:

- usuário bandit7
- grupo bandit6
- 33 bytes de tamanho

## Solução

Buscando por arquivos no diretório home:
```
bandit6@bandit:~$ ls

bandit6@bandit:~$ ls -la
total 20
drwxr-xr-x  2 root root 4096 May  7  2020 .
drwxr-xr-x 41 root root 4096 May  7  2020 ..
-rw-r--r--  1 root root  220 May 15  2017 .bash_logout
-rw-r--r--  1 root root 3526 May 15  2017 .bashrc
-rw-r--r--  1 root root  675 May 15  2017 .profile
```

Como não obtemos só arquivos nativos da máquina, vou buscar a flag a partir do diretório raiz. 

Com o comando find, vamos buscar no diretório / (raíz), por arquivos que tenham 33 bytes de tamanho, que o usuário bandit6 e o grupo bandit7 tenham acesso:
```
bandit6@bandit:~$ find / -size 33c -user bandit6 -group bandit7
...
```

A grande maioria dos retornos tem permissão negada para leitura, porém existe um que não teve o acesso negado. Vamos verificar seu conteúdo:
```
bandit6@bandit:~$ cat /var/lib/dpkg/info/bandit7.password
HKBPTKQnIay4Fw76bEy8PVxKEDQRKTzs
```

Obtemos a flag! 🥷

## Conceitos utilizados

- Diretório raíz em sistemas linux
- Acesso de arquivos por grupos
- Como funcionam permissões de arquivos no linux

## Links úteis

- https://www.ubuntudicas.com.br/2012/04/estrutura-de-diretorios-no-linux/
- https://ricardo-reis.medium.com/gerenciamento-de-usu%C3%A1rios-e-grupos-no-linux-ef0c6cb95880

