# 🕵️ Bandit 26

Bom trabalho pegando uma concha! Agora corra e pegue a senha para bandit27!

## Solução

Não temos muitas descrições para este desafio, e mesmo quando tentamos nos conectar ao desafio, ainda seguimos sendo expulsos sem acesso do comando more.

O que podemos fazer é, novamente através do vim, tentar editar qual shell será executada e buscar por uma solução. Para isso, vamos reduzir o nosso terminal novamente e acessar o vim com o comando v.

Dentro do vi, é possível fazer configurações para o ambiente local com o parâmetro :set, dessa forma, podemos dizer que shell=/bin/bash e então executar o shell através do parâmetro :shell.

Isso fará com que uma interface de pseudo terminal seja aberto no vi, nos permitindo buscar pela flag:
```
:set shell /bin/bash
:shell 

temos um shell
```

Agora que temos acesso ao bash, vamos verificar quais arquivos existem no diretório home:
```
bandit26@bandit:~$ ls
bandit27-do  text.txt
```

Existem dois arquivos, o text.txt que está sendo exibido quando uma conexão é realizada e o bandit27-do. Vamos então ver sobre o que esse arquivo se trata:
```
bandit26@bandit:~$ file bandit27-do 
bandit27-do: setuid ELF 32-bit LSB executable, Intel 80386, version 1 (SYSV), dynamically linked, interpreter /lib/ld-linux.so.2, for GNU/Linux 2.6.32, BuildID[sha1]=8e941f24b8c5cd0af67b22b724c57e1ab92a92a1, not stripped
bandit26@bandit:~$ ./bandit27-do 
Run a command as another user.
  Example: ./bandit27-do id
```

Ao executarmos, notamos que este arquivo permite a execução de comandos como bandit27, logo, basta buscarmos o conteúdo da flag para o próximo nível:
```
bandit26@bandit:~$ ./bandit27-do cat /etc/bandit_pass/bandit27 
3ba3118a22e93127a4ed485be72ef5ea
```

Obtemos a flag! 🥷

## Explicação

- Parâmetros VI
- Variáveis de ambiente VI

## Links úteis

- https://br.ccm.net/faq/9893-tutorial-sobre-vi-vim
