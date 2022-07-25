# 🕵️ Bandit 17

Existem 2 arquivos no diretório inicial: passwords.old e passwords.new . A senha para o próximo nível está em passwords.new e é a única linha que foi alterada entre passwords.old e passwords.new


## Solução

Listando os arquivos no diretório home:
```
bandit17@bandit:~$ ls
passwords.new  passwords.old
```

Utilizando o comando diff, podemos verificar quais linhas são diferentes entre os arquivos:
```
bandit17@bandit:~$ diff passwords.new passwords.old 
42c42
< kfBf3eYk5BPBRzwjqutbbfE887SVc5Yd
---
> w0Yfolrc5bwjS4qw5mq1nnQi6mF03bii

```

A nova entrada foi feita no arquivo passwords.new, dessa forma nossa flag será a primeira string do retorno, onde foi inserido um novo valor. 

Obtemos a flag! 🥷

## Conceitos utilizados

- Comando diff
- Comparação de strings

## Links úteis

- manual do comando diff `man diff`

