# 🕵️ Bandit 08

A senha para o próximo nível é armazenada no arquivo data.txt e é a única linha de texto que ocorre apenas uma vez.

## Solução

Listando os arquivos no diretório home:
```
bandit8@bandit:~$ ls
data.txt
```

Ordenando os dados do arquivo data.txt e passando seu output como input para o comando uniq com o parametro -u para buscar por strings não repetidas dentro do arquivo:
```
bandit8@bandit:~$ sort data.txt | uniq -u 
UsvVyFSfZZWbi6wgC7dAFyFuR6jQQUhR
```

Obtemos a flag! 🥷

## Explicação

- Comando sort e ordenação de arquivos
- Comando uniq e classificação de arquivos

## Links úteis

- manual do comando sort `man sort`
- manual do comando uniq `man uniq`

