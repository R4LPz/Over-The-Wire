# 🕵️ Bandit 29

Existe um repositório git em ssh://bandit31-git@localhost/home/bandit31-git/repo. A senha do usuário bandit31-git é a mesma do usuário bandit31.

Clone o repositório e encontre a senha para o próximo nível.

## Solução

Clonando o repositório:
```
bandit31@bandit:~$ mkdir /tmp/bdt31
bandit31@bandit:~$ cd /tmp/bdt31
bandit31@bandit:/tmp/bdt31$ git clone ssh://bandit31-git@localhost/home/bandit31-git/repo
```

Verificando o conteúdo do arquivo README.md :
```
bandit31@bandit:/tmp/bdt31/repo$ cat README.md 
This time your task is to push a file to the remote repository.

Details:
    File name: key.txt
    Content: 'May I come in?'
    Branch: master
```

O arquivo nos informa para seguirmos para o próximo nível precisamos fazer um push na branch master. 

Vamos então começar criando o arquivo solicitado:
```
bandit31@bandit:/tmp/bdt31/repo$ nano key.txt
May I come in?
```

Vamos adicionar o arquivo em stagging para ser commitado:
```
bandit31@bandit:/tmp/bdt31/repo$ git add key.txt 
The following paths are ignored by one of your .gitignore files:
key.txt
Use -f if you really want to add them.
```

Ao tentarmos adicionar o arquivo, somos informados que o arquivo .gitignore, ignora esse tipo de arquivo. 

Este arquivo, quando presente em um repositório git, define arquivos que devem ser ignorados pelo git no momento do envio dos arquivos.

Para contornar este problema, vamos resolver a restrição de arquivos .txt do gitignore:
```
bandit31@bandit:/tmp/bdt31/repo$ nano .gitignore 
```

Tentando adicionar o arquivo novamente, devemos ter exito. Em seguida vamos fazer o commit, passando uma mensagem de identificação para ele e realizar o push na branch master:
```
bandit31@bandit:/tmp/bdt31/repo$ git add key.txt 

bandit31@bandit:/tmp/bdt31/repo$ git commit -m 'give me the flag'
[master f23ad99] give me the flag
 1 file changed, 1 insertion(+)
 create mode 100644 key.txt
bandit31@bandit:/tmp/bdt31/repo$ git push origin master
...
remote: ### Attempting to validate files... ####
remote: 
remote: .oOo.oOo.oOo.oOo.oOo.oOo.oOo.oOo.oOo.oOo.
remote: 
remote: Well done! Here is the password for the next level:
remote: 56a9bf19c63d650ce78e6ec0354ee45e
remote: 
remote: .oOo.oOo.oOo.oOo.oOo.oOo.oOo.oOo.oOo.oOo.
remote: 
...
```

Ao realizar o push obtemos a flag através da mensagem de retorno! 🥷

##  Conceitos utilizados

- Gitignore
- Git push
- Git add
- Fluxo de commits


## Links úteis

- https://git-scm.com/doc (documentação extensa, porém completa de como utilizar o git)

