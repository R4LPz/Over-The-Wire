# 🕵️ Bandit 25

Entrar no bandit26 a partir do bandit25 deve ser bem fácil... O shell para o usuário bandit26 não é /bin/bash , mas outra coisa. Descubra o que é, como funciona e como sair disso.

## Solução

Quando tentamos realizar a conexão, ela sempre será encerrada pelo host: 
```
bandit25@bandit:~$ ssh -i bandit26.sshkey bandit26@localhost
...
Connection to localhost closed.
```

Para tentar entender o que acontece, podemos verificar o que existe no arquivo passwd para entender qual o shell está sendo utilizado, visto que o desafio nos informa que não é o bash:
```
bandit25@bandit:~$ cat /etc/passwd | grep bandit26
bandit26:x:11026:11026:bandit level 26:/home/bandit26:/usr/bin/showtext
```

Ao verificarmos o arquivo, notamos que o shell é um executável contido em /usr/bin, podemos então analisar seu conteúdo:
```
bandit25@bandit:~$ cat /usr/bin/showtext 
#!/bin/sh

export TERM=linux

more ~/text.txt
exit 0
```

A execução deste arquivo é simples, ele define a variável TERM como linux, isso faz com que o emulador de terminal executado seja o linux e não o xterm (que geralmente é o padrão).

Em seguida, chama o comando more para exibir o conteúdo do arquivo text.txt e em seguida encerra com saída 0.

O problema é que o comando more tem como papel fazer paginação de arquivos, como o arquivo text.txt é pequeno, a paginação não é feita, portanto apenas exibe seu conteúdo e encerra a conexão.

Para burlarmos isso, precisaremos reduzir o tamanho do terminal para algo menor que o arquivo text.txt, assim a paginação acontecerá e poderemos acessar o vim através do shell.

Vamos reduzir o tamanho do terminal para algo menor que 6 linhas e realizar novamente a conexão. Quando ela ocorrer, o arquivo deverá ser paginado

Agora com a paginação feita, podemos apertar a tecla v, ela abrirá a interface do vim para editarmos o arquivo que está sendo exibido. 

O segredo é que através do vim podemos abrir um novo arquivo na conexão realizada ou até mesmo um shell para executar comandos. Então passando o comando :e e o cominho do arquivo que desejamos, podemos verificar o conteúdo da flag.
```
v

:e /etc/bandit_pass/bandit26

5czgV9L3Xx8JPOyRbXh6lQbmIOWvPT6Z 
```

Obtemos a flag! 🥷

## Conceitos utilizados

- /etc/passwd
- Comando more através do manual `man more`
- Editor vi/vim
- Escalação de privilégios


## Links úteis

- https://ubunlog.com/pt/etc-passwd/
- https://guialinux.uniriotec.br/more/
- https://br.ccm.net/faq/9893-tutorial-sobre-vi-vim

