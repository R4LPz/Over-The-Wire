# 🕵️ Bandit 14

A senha para o próximo nível pode ser recuperada enviando a senha do nível atual para a porta 30000 no localhost .

## Solução

Para realizarmos a conexão com uma porta local, utilizamos o endereço ip 127.0.0.1 (ou localhost) e nos conectamos a porta 30000 por meio do netcat:
```
bandit14@bandit:~$ echo 4wcYUJFw0k0XLShlDzztnTBHiqxU3b3e | nc 127.0.0.1 30000
Correct!
BfMYroe26WYalil77FoDi9qh59eK5xNr
```

Obtemos a flag! 🥷

## Conceitos utilizados

- O que são portas (sockets)
- Conexões locais (localhost)
- Comando echo
- Ferramenta netcat

## Links úteis

- https://blog.pantuza.com/artigos/o-que-sao-e-como-funcionam-os-sockets
- https://pt.wikipedia.org/wiki/Netcat

