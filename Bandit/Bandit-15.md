# 🕵️ Bandit 15

A senha para o próximo nível pode ser recuperada enviando a senha do nível atual para a porta 30001 no localhost usando criptografia SSL.

## Solução

Entendendo como o openssl funciona:
```
bandit15@bandit:~$ man openssl
```

Vamos realizar uma conexão  ssl com o servidor, passando os parametros 's_client' para dizermos que somos um client e '-connect' para explicitar o host e a porta na qual queremos nos conectar.

Ao realizarmos a conexão, podemos enviar a flag atual para obter a nova flag:
```
bandit15@bandit:~$ openssl s_client -connect 127.0.0.1:30001
BfMYroe26WYalil77FoDi9qh59eK5xNr
Correct!

cluFn7wTiGryunymYOu4RcffSxQluehd
closed
```

Obtemos a flag! 🥷

## Conceitos utilizados

- SSL
- Comando openssl

## Links úteis

- https://pt.wikipedia.org/wiki/Transport_Layer_Security
- https://www.openssl.org/

