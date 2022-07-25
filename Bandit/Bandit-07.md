# 🕵️ Bandit 07

A senha para o próximo nível é armazenada no arquivo data.txt ao lado da palavra millionth

## Solução

Listando os arquivos no diretório home:
```
bandit7@bandit:~$ ls
data.txt
```

Verificando o conteúdo do arquivo data.txt:
```
bandit7@bandit:~$ file data.txt 
data.txt: UTF-8 Unicode text
```

Buscando os dados do arquivo data.txt e utilizando seu output como entrada para o comando grep, que por sua vez buscará pela palavra millionth:
```
bandit7@bandit:~$ cat data.txt | grep "millionth"
millionth	cvX2JJa4CFALtqS87jk27qwqGhBM9plV
```

Obtemos a flag! 🥷

## Conceitos utilizados

- Comando grep
- Ligação de comandos no linux
- Operador Pipe |

## Links úteis

- manual do comando grep `man grep`
- https://www.tutorialspoint.com/unix/unix-io-redirections.htm
- https://unix.stackexchange.com/questions/159513/what-are-the-shells-control-and-redirection-operators

