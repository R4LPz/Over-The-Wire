# 🕵️ Bandit 28

Existe um repositório git em ssh://bandit28-git@localhost/home/bandit28-git/repo. A senha do usuário bandit28-gité a mesma do usuário bandit28.

## Solução

Vamos começar clonando o repositório como nos desafios anteriores:
```
bandit28@bandit:~$ mkdir /tmp/bdt28 && cd /tmp/bdt28
bandit28@bandit:/tmp/bdt28$ git clone ssh://bandit28-git@localhost/home/bandit28-git/repo
```

Verificando o conteúdo do repositório clonado:
```
bandit28@bandit:/tmp/bdt28/$ cd repo/
bandit28@bandit:/tmp/bdt28/repo$ ls
README.md
```

Verificando o conteúdo do arquivo README.md:
```
bandit28@bandit:/tmp/bdt28/repo$ cat README.md 
# Bandit Notes
Some notes for level29 of bandit.

## credentials

- username: bandit29
- password: xxxxxxxxxx
```

Notamos que a senha desta vez não está presente no arquivo.

O git é um versionador de códigos, então o que podemos ver se esta é a unica versão que temos deste código através do comando git log. Esse comando irá listar todos os commits e suas mensagens de commit:
```
bandit28@bandit:/tmp/bdt28/repo$ git log 
...

commit c086d11a00c0648d095d04c089786efef5e01264
Author: Morla Porla <morla@overthewire.org>
Date:   Thu May 7 20:14:49 2020 +0200

    add missing data

...
```

Analisando a saída, veremos que existe um commit no qual a mensagem de commit é 'add missing data', essa é provavelmente a alteração que estamos buscando.

Para mudar nosso código para esta versão, vamos utilizar o comando git checkout com o código do commit. Isso fará a mudança para um 'outro estado' do código:
```
bandit28@bandit:/tmp/bdt28/repo$ git checkout c086d11a00c0648d095d04c089786efef5e01264
```

Verificando novamente o conteúdo de README.md: 
```
bandit28@bandit:/tmp/bdt28/repo$ cat README.md 
# Bandit Notes
Some notes for level29 of bandit.

## credentials

- username: bandit29
- password: bbc96594b4e001778eee9975372716b2
```

Obtemos a flag ! 🥷

## Conceitos utilizados

- Git log
- Git commit
- Git checkout

## Links úteis

- https://git-scm.com/doc (documentação extensa, porém completa de como utilizar o git)

