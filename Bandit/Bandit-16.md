# 🕵️ Bandit 16

As credenciais para o próximo nível podem ser recuperadas enviando a senha do nível atual para uma porta no localhost no intervalo de 31000 a 32000 . Primeiro descubra qual dessas portas tem um servidor escutando nelas. Em seguida, descubra quais deles falam SSL e quais não. Há apenas 1 servidor que fornecerá as próximas credenciais, os outros simplesmente enviarão de volta para você o que você enviar para ele.

## Solução

Precisamos enumerar as portas abertas no servidor, para isso podemos utilizar a ferramenta nmap e fazer uma varredura da porta 31000 até a 32000:

**Obs**: O parâmetro sV tentará identificar através de scripts, qual serviço está sendo executado em cada porta.

```
bandit16@bandit:~$ nmap -v -sV 127.0.0.1 -p 31000-32000
...
PORT      STATE    SERVICE     VERSION
31046/tcp open     echo
31518/tcp filtered unknown
31691/tcp open     echo
31790/tcp open     ssl/unknown
31960/tcp open     echo
1 service unrecognized despite returning data. If you know the service/version, please submit the following fingerprint at https://nmap.org/cgi-bin/submit.cgi?new-service :
SF-Port31790-TCP:V=7.40%T=SSL%I=7%D=7/23%Time=62DC48D9%P=x86_64-pc-linux-g
SF:nu%r(GenericLines,31,"Wrong!\x20Please\x20enter\x20the\x20correct\x20cu
SF:rrent\x20password\n")%r(GetRequest,31,"Wrong!\x20Please\x20enter\x20the
SF:\x20correct\x20current\x20password\n")%r(HTTPOptions,31,"Wrong!\x20Plea
SF:se\x20enter\x20the\x20correct\x20current\x20password\n")%r(RTSPRequest,
SF:31,"Wrong!\x20Please\x20enter\x20the\x20correct\x20current\x20password\
SF:n")%r(Help,31,"Wrong!\x20Please\x20enter\x20the\x20correct\x20current\x
SF:20password\n")%r(SSLSessionReq,31,"Wrong!\x20Please\x20enter\x20the\x20
SF:correct\x20current\x20password\n")%r(TLSSessionReq,31,"Wrong!\x20Please
SF:\x20enter\x20the\x20correct\x20current\x20password\n")%r(Kerberos,31,"W
SF:rong!\x20Please\x20enter\x20the\x20correct\x20current\x20password\n")%r
SF:(FourOhFourRequest,31,"Wrong!\x20Please\x20enter\x20the\x20correct\x20c
SF:urrent\x20password\n")%r(LPDString,31,"Wrong!\x20Please\x20enter\x20the
SF:\x20correct\x20current\x20password\n")%r(LDAPSearchReq,31,"Wrong!\x20Pl
SF:ease\x20enter\x20the\x20correct\x20current\x20password\n")%r(SIPOptions
SF:,31,"Wrong!\x20Please\x20enter\x20the\x20correct\x20current\x20password
SF:\n");
...
```

O retorno mostra que na porta 31790, ao realizar a conexão, o nmap retornou algumas vezes uma mensagem informando que o password estava incorreto. Dessa forma, nossas suspeitas sobre essa porta aumentam. 

Vamos tentar realizar a conexão ssl e passar o valor da chave:
```
bandit16@bandit:~$ openssl s_client --connect localhost:31790

cluFn7wTiGryunymYOu4RcffSxQluehd
Correct!
-----BEGIN RSA PRIVATE KEY-----
MIIEogIBAAKCAQEAvmOkuifmMg6HL2YPIOjon6iWfbp7c3jx34YkYWqUH57SUdyJ
imZzeyGC0gtZPGujUSxiJSWI/oTqexh+cAMTSMlOJf7+BrJObArnxd9Y7YT2bRPQ
Ja6Lzb558YW3FZl87ORiO+rW4LCDCNd2lUvLE/GL2GWyuKN0K5iCd5TbtJzEkQTu
DSt2mcNn4rhAL+JFr56o4T6z8WWAW18BR6yGrMq7Q/kALHYW3OekePQAzL0VUYbW
JGTi65CxbCnzc/w4+mqQyvmzpWtMAzJTzAzQxNbkR2MBGySxDLrjg0LWN6sK7wNX
x0YVztz/zbIkPjfkU1jHS+9EbVNj+D1XFOJuaQIDAQABAoIBABagpxpM1aoLWfvD
KHcj10nqcoBc4oE11aFYQwik7xfW+24pRNuDE6SFthOar69jp5RlLwD1NhPx3iBl
J9nOM8OJ0VToum43UOS8YxF8WwhXriYGnc1sskbwpXOUDc9uX4+UESzH22P29ovd
d8WErY0gPxun8pbJLmxkAtWNhpMvfe0050vk9TL5wqbu9AlbssgTcCXkMQnPw9nC
YNN6DDP2lbcBrvgT9YCNL6C+ZKufD52yOQ9qOkwFTEQpjtF4uNtJom+asvlpmS8A
vLY9r60wYSvmZhNqBUrj7lyCtXMIu1kkd4w7F77k+DjHoAXyxcUp1DGL51sOmama
+TOWWgECgYEA8JtPxP0GRJ+IQkX262jM3dEIkza8ky5moIwUqYdsx0NxHgRRhORT
8c8hAuRBb2G82so8vUHk/fur85OEfc9TncnCY2crpoqsghifKLxrLgtT+qDpfZnx
SatLdt8GfQ85yA7hnWWJ2MxF3NaeSDm75Lsm+tBbAiyc9P2jGRNtMSkCgYEAypHd
HCctNi/FwjulhttFx/rHYKhLidZDFYeiE/v45bN4yFm8x7R/b0iE7KaszX+Exdvt
SghaTdcG0Knyw1bpJVyusavPzpaJMjdJ6tcFhVAbAjm7enCIvGCSx+X3l5SiWg0A
R57hJglezIiVjv3aGwHwvlZvtszK6zV6oXFAu0ECgYAbjo46T4hyP5tJi93V5HDi
Ttiek7xRVxUl+iU7rWkGAXFpMLFteQEsRr7PJ/lemmEY5eTDAFMLy9FL2m9oQWCg
R8VdwSk8r9FGLS+9aKcV5PI/WEKlwgXinB3OhYimtiG2Cg5JCqIZFHxD6MjEGOiu
L8ktHMPvodBwNsSBULpG0QKBgBAplTfC1HOnWiMGOU3KPwYWt0O6CdTkmJOmL8Ni
blh9elyZ9FsGxsgtRBXRsqXuz7wtsQAgLHxbdLq/ZJQ7YfzOKU4ZxEnabvXnvWkU
YOdjHdSOoKvDQNWu6ucyLRAWFuISeXw9a/9p7ftpxm0TSgyvmfLF2MIAEwyzRqaM
77pBAoGAMmjmIJdjp+Ez8duyn3ieo36yrttF5NSsJLAbxFpdlc1gvtGCWW+9Cq0b
dxviW8+TFVEBl1O4f7HVm6EpTscdDxU+bCXWkfjuRb7Dy9GOtt9JPsX8MBTakzh3
vBgsyi/sN3RqRBcGU40fOoZyfAMT8s1m/uYv52O6IgeuZ/ujbjY=
-----END RSA PRIVATE KEY-----

closed
```

Conseguimos a chave privada para o próximo nível, vamos criar um arquivo e armazena-la para que possamos realizar a conexão ssh:
```
bandit16@bandit:~$ mkdir /tmp/bdt16

bandit16@bandit:~$ cd /tmp/bdt16

bandit16@bandit:/tmp/bdt16$ nano bandit17.key
# Inserir a chave recebida no arquivo
```

Precisamos dar permissão de leitura do arquivo para o usuário atual. Para isso vamos utilizar o valor 400 para o comando chmod:
```
bandit16@bandit:/tmp/bdt16$ chmod 400 bandit17.key 
```

Com tudo feito, podemos realizar a conexão ssh e buscar pela chave através do bandit 17:
```
bandit16@bandit:/tmp/bdt16$ ssh -i bandit17.key  bandit17@localhost

bandit17@bandit:~$ cat /etc/bandit_pass/bandit17 
xLYVMN9WE5zQ5vHacb0sZEVqbrp7nBTn
```

Obtemos a flag! 🥷

## Conceitos utilizados

- Port Scanners
- Ferramenta Nmap
- Chaves privadas e públicas
- Permissões de arquivos no linux
- Comando chmod

## Links úteis

- https://nmap.org/man/pt_BR/index.html
- https://guialinux.uniriotec.br/chmod/

