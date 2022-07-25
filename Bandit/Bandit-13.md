# 🕵️ Bandit 13

A senha para o próximo nível é armazenada em /etc/bandit_pass/bandit14 e só pode ser lida pelo usuário bandit14 . Para este nível, você não obtém a próxima senha, mas obtém uma chave SSH privada que pode ser usada para fazer login no próximo nível. Nota: localhost é um nome de host que se refere à máquina em que você está trabalhando

## Solução

Listando os arquivos no diretório home:
```
bandit13@bandit:~$ ls
sshkey.private
```

Como temos uma chave privada, podemos realizar a conexão ssh com o próximo nível através dela (parâmetro -i):
```
bandit13@bandit:~$ ssh bandit14@localhost -i sshkey.private
```

Conectados como bandit14, temos acesso de leitura ao arquivo da flag:
```
bandit14@bandit:~$ cat /etc/bandit_pass/bandit14 
4wcYUJFw0k0XLShlDzztnTBHiqxU3b3e
```

Obtemos a flag! 🥷

## Conceitos utilizados

- Chaves públicas e privadas.
- Como o SSH funciona (assinatura por chaves)

## Links úteis

- https://pt.wikipedia.org/wiki/Criptografia_de_chave_p%C3%BAblica
- https://pt.wikipedia.org/wiki/Secure_Shell

