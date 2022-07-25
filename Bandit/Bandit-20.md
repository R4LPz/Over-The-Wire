# 🕵️ Bandit 20

Existe um binário setuid no diretório home que faz o seguinte: ele faz uma conexão com localhost na porta que você especifica como um argumento de linha de comando. Em seguida, ele lê uma linha de texto da conexão e a compara com a senha do nível anterior (bandit20). Se a senha estiver correta, transmitirá a senha para o próximo nível (bandit21).

## Solução

Listando os arquivos no diretório home:
```
bandit20@bandit:~$ ls
suconnect
```

Verificando o formato do arquivo listado:
```
bandit20@bandit:~$ file suconnect 
suconnect: setuid ELF 32-bit LSB executable, Intel 80386, version 1 (SYSV), dynamically linked, interpreter /lib/ld-linux.so.2, for GNU/Linux 2.6.32, BuildID[sha1]=74c0f6dc184e0412b6dc52e542782f43807268e1, not stripped
```

Como dito no enunciado, o arquivo fará uma conexão com localhost em uma determinada porta e recebe um valor da conexão, se este valor for a chave do nível atual, obteremos a flag. 

Dessa forma, vamos fazer com que uma de nossas portas fique ouvindo por novas conexões. Quando uma conexões for realizada, envie o valor da flag.

Fazemos isso por meio do link com os comandos echo e netcat, ambos ja citados anteriormente.

Por fim, como isso fará com que o netcat fique ouvindo a conexão, podemos utilizar o operador & para que esse processo seja executado em segundo plano e ainda tenhamos acesso ao shell enquanto ele é executado:
```
bandit20@bandit:~$ echo GbKksEFF4yrVs6il55v6gwY5aVje5f0j | nc -lp 6666 &
[1] 15074
```

De volta ao shell, podemos agora executar o comando, especificando a porta que abrimos no netcat:
```
bandit20@bandit:~$ ./suconnect 6666
Read: GbKksEFF4yrVs6il55v6gwY5aVje5f0j
Password matches, sending next password
gE269g2h3mw3pwgrj0Ha9Uoqen1c9DGr
[1]+  Done                    echo GbKksEFF4yrVs6il55v6gwY5aVje5f0j | nc -lp 6666

```

Após o código ser executado, ele recebe a chave de leitura e nos retorna a flag! Além de encerrar nosso processo em segundo plano, graças ao encerramento da conexão.

Obtemos a flag! 🥷

## Conceitos utilizados

- Processos em segundo plano
- Arquitetura cliente e servidor com Netcat
- Difereça de ctrl+z e &

## Links úteis

- https://www.todoespacoonline.com/w/2015/08/primeiro-e-segundo-plano-no-shell-do-linux-jobs-fg-e-bg/
- https://www.varonis.com/pt-br/blog/netcat-commands

