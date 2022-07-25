# 🕵️ Bandit 11

A senha para o próximo nível é armazenada no arquivo data.txt , onde todas as letras minúsculas (az) e maiúsculas (AZ) foram giradas em 13 posições

## Solução

Listando os arquivos no diretório home:
```
bandit11@bandit:~$ ls
data.txt
```

Verificando o conteúdo do arquivo data.txt:
```
bandit11@bandit:~$ cat data.txt 
Gur cnffjbeq vf 5Gr8L4qetPEsPk8htqjhRK8XSP6x2RHh
```

Utilizando o comando tr para alterar as letras de retorno do arquivo data.txt. Basicamente "construímos" um algorítmo rot13 para que as letras de "a" até "m" sejam trocadas em 13 posições (metade do alfabeto):
```
bandit11@bandit:~$ cat data.txt | tr 'A-Za-z' 'N-ZA-Mn-za-m'
The password is 5Te8Y4drgCRfCx8ugdwuEX8KFC6k2EUu
```

Obtemos a flag! 🥷

## Explicação

- Algorítmo de rotação de caracteres (cifra de César)
- Rot 13
- Comando tr para mudança de caracteres

## Links úteis

- https://ironlinux.com.br/o-comando-tr-no-linux/
- https://pt.wikipedia.org/wiki/Cifra_de_C%C3%A9sar

