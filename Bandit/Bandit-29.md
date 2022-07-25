# 🕵️ Bandit 29

Existe um repositório git em ssh://bandit29-git@localhost/home/bandit29-git/repo. A senha do usuário bandit29-git é a mesma do usuário bandit29.

Clone o repositório e encontre a senha para o próximo nível.

## Solução

Clonando o repositório:
```
bandit29@bandit:~$ mkdir /tmp/bdt30 && cd /tmp/bdt30
bandit29@bandit:/tmp/bdt30$ git clone ssh://bandit29-git@localhost/home/bandit29-git/repo
```

Verificando seu conteúdo:
```
bandit29@bandit:/tmp/bdt30$ cd repo/

bandit29@bandit:/tmp/bdt30/repo$ ls
README.md

bandit29@bandit:/tmp/bdt/repo$ cat README.md 
# Bandit Notes
Some notes for bandit30 of bandit.

## credentials

- username: bandit30
- password: <no passwords in production!>
```

Ao verificar o conteúdo do arquivo, notamos que existe uma informação de que não existem passwords em produção. Logo, podemos verificar se existem branchs para dev e homologação através do comando git ls-remote, que listará todas as branchs remotas no repositório:
```
bandit29@bandit:/tmp/bdt30/repo$ git ls-remote

bandit29-git@localhost's password: 
From ssh://bandit29-git@localhost/home/bandit29-git/repo
208f463b5b3992906eabf23c562eda3277fea912	HEAD
bc833286fca18a3948aec989f7025e23ffc16c07	refs/heads/dev
208f463b5b3992906eabf23c562eda3277fea912	refs/heads/master
786d5bea2bd2dcbed2c8896a310c3c5306bc713c	refs/heads/sploits-dev
```

Agora que sabemos que existe uma branch de dev, vamos fazer o checkout para ela:
```
bandit29@bandit:/tmp/bdt30/repo$ git checkout bc833286fca18a3948aec989f7025e23ffc16c07
```

E por fim, verificar se o conteúdo do arquivo foi alterado:
```
bandit29@bandit:/tmp/bdt30/repo$ cat README.md 
# Bandit Notes
Some notes for bandit30 of bandit.

## credentials

- username: bandit30
- password: 5b90576bedb2cc04c86a9e924ce42faf
```

Obtemos a flag! 🥷

##  Conceitos utilizados

- Branchs
- Branchs remotas
- Ambientes de desenvolvimento

## Links úteis

- https://social.msdn.microsoft.com/Forums/pt-BR/c2f65545-08a2-47d6-a273-400d9f09ac22/qual-a-diferena-de-ambientes-de-desenvolvimento-homologao-e-produo?forum=sharepointpt
- https://git-scm.com/doc (documentação extensa, porém completa de como utilizar o git)

