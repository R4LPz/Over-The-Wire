# 🕵️ Bandit 27

Existe um repositório git em ssh://bandit27-git@localhost/home/bandit27-git/repo. A senha do usuário bandit27-gité a mesma do usuário bandit27.

## Solução

Git é um sistema de versionamento de código que nos permite manusear um repositório de forma que suas alterações façam parte de um "linha do tempo". Sabendo disso, para clonarmos este repositório, precisaremos de premissão de escrita em uma pasta.

Vamos então criar uma pasta em /tmp/ onde tenhamos estas permissões:
```
bandit27@bandit:~$ mkdir /tmp/bdt27
bandit27@bandit:~$ cd /tmp/bdt27
```

Já na pasta, podemos realizar o comando git clone para que o repositório seja extraído e montado no diretório atual:
```
bandit27@bandit:/tmp/bdt27$ git clone ssh://bandit27-git@localhost/home/bandit27-git/repo
Cloning into 'repo'...

bandit27-git@localhost's password: 
remote: Counting objects: 3, done.
remote: Compressing objects: 100% (2/2), done.
remote: Total 3 (delta 0), reused 0 (delta 0)
Receiving objects: 100% (3/3), done.
```

Vamos agora verificar o conteúdo que nos foi gerado:
```
bandit27@bandit:/tmp/bdt27$ cd repo/
bandit27@bandit:/tmp/bdt27/repo$ ls
README
```

Temos apenas um arquivo README, vejamos seu conteúdo:
```
bandit27@bandit:/tmp/bdt27/repo$ cat README 
The password to the next level is: 0ef186ac70e04ea33b4c1853d2526fa2
```

Obtemos a flag! 🥷

## Conceitos utilizados

- git
- versionamento de código

## Links úteis

- https://git-scm.com/doc (documentação extensa, porém completa de como utilizar o git)

