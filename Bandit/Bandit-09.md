# 🕵️ Bandit 09

A senha para o próximo nível é armazenada no arquivo data.txt em uma das poucas strings legíveis, precedida por vários caracteres '='.

## Solução

Listando os arquivos no diretório home:
```
bandit9@bandit:~$ ls
data.txt
```

Buscando por textos legíveis através do comando string e passando seu retorno para o grep em busca de repetições do caractere = :
```
bandit9@bandit:~$ strings data.txt | grep ==
========== the*2i"4
========== password
Z)========== is
&========== truKLdjsbJ5g7yyJ2X2R0o3a5HQJFuLk
```

Obtemos a flag! 🥷

## Conceitos utilizados

- Comando strings
- O que são cadeias de caracteres

## Links úteis

- https://www.howtogeek.com/427805/how-to-use-the-strings-command-on-linux/
- https://pt.wikipedia.org/wiki/Cadeia_de_caracteres

