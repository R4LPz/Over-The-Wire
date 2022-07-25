# 🕵️ Bandit 19

Para obter acesso ao próximo nível, você deve usar o binário setuid no diretório inicial. Execute-o sem argumentos para descobrir como usá-lo. A senha para este nível pode ser encontrada no local usual (/etc/bandit_pass), após você ter usado o binário setuid.

## Solução

Listando os arquivos no diretório home:
```
bandit19@bandit:~$ ls
bandit20-do
```

Verificando o formato do arquivo bandit20-do:
```
bandit19@bandit:~$ file bandit20-do
bandit20-do: setuid ELF 32-bit LSB executable, Intel 80386, version 1 (SYSV), dynamically linked, interpreter /lib/ld-linux.so.2, for GNU/Linux 2.6.32, BuildID[sha1]=8e941f24b8c5cd0af67b22b724c57e1ab92a92a1, not stripped
```

Como o arquivo se trata de um ELF, significa que temos um arquivo executável. Vamos então entender como ele funciona:
```
bandit19@bandit:~$ ./bandit20-do 
Run a command as another user.
  Example: ./bandit20-do id
```

Ao executarmos, podemos notar que se trata de um código que executa um comando com permissões de outro usuário. 

Dessa forma, podemos tentar acessar a flag do próximo nível com ele:
```
bandit19@bandit:~$ ./bandit20-do cat /etc/bandit_pass/bandit20
GbKksEFF4yrVs6il55v6gwY5aVje5f0j
```

Obtemos a flag! 🥷

## Conceitos utilizados

- Arquivos ELF
- Execução de arquivos no linux

## Links úteis

- https://pt.wikipedia.org/wiki/Executable_and_Linkable_Format

