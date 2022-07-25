# 🕵️ Bandit 01

A senha para o próximo nível é armazenada em um arquivo chamado "-" localizado no diretório inicial.

## Solução

Listando os arquivos no diretório home:
```
bandit1@bandit:~$ ls
-
```

Obtendo o conteúdo do arquivo através do path relativo:
```
bandit1@bandit:~$ cat ./- 
CV1DtqXWVFXTvM2F0k09SHz0YwRINYA9
```

Obtemos a flag! 🥷

## Conceitos utilizados

- Caminhos de arquivos
- Path relativo e absoluto

## Links úteis

- comando `cat --help` para exibir as opções da ferramenta
- https://stackoverflow.com/questions/42187323/how-to-open-a-dashed-filename-using-terminal
- https://mange.ifrn.edu.br/site/doc-ubuntu-fr2pt_br/caminhos.html

