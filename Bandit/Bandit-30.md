# 🕵️ Bandit 29

Existe um repositório git em ssh://bandit30-git@localhost/home/bandit30-git/repo. A senha do usuário bandit30-git é a mesma do usuário bandit30.

Clone o repositório e encontre a senha para o próximo nível.

## Solução

Clonando o repositório:
```
bandit30@bandit:/tmp/bdt$ mkdir /tmp/bdt30
bandit30@bandit:/tmp/bdt$ cd  /tmp/bdt30
bandit30@bandit:/tmp/bdt30$ git clone ssh://bandit30-git@localhost/home/bandit30-git/repo
```

Verificando o conteúdo do README.md: 
```
bandit30@bandit:/tmp/bdt30/repo$ cat README.md 
just an epmty file... muahaha
```

Listando o conteúdo remoto com ls-remote:
```
bandit30@bandit:/tmp/bdt30/repo$ git ls-remote
Could not create directory '/home/bandit30/.ssh'.
The authenticity of host 'localhost (127.0.0.1)' can't be established.
ECDSA key fingerprint is SHA256:98UL0ZWr85496EtCRkKlo20X3OPnyPSB5tB5RPbhczc.
Are you sure you want to continue connecting (yes/no)? yes
Failed to add the host to the list of known hosts (/home/bandit30/.ssh/known_hosts).
This is a OverTheWire game server. More information on http://www.overthewire.org/wargames

bandit30-git@localhost's password: 
From ssh://bandit30-git@localhost/home/bandit30-git/repo
3aefa229469b7ba1cc08203e5d8fa299354c496b	HEAD
3aefa229469b7ba1cc08203e5d8fa299354c496b	refs/heads/master
f17132340e8ee6c159e0a4a6bc6f80e1da3b1aea	refs/tags/secret
```

Podemos ver que existe uma tag chamada secret. Tags são utilizadas para marcar ações e pontos específicos do código. 

Vamos verificar as tags existentes no repositório com o comando git tag passando o parâmetro -l para listar todas:
```
bandit30@bandit:/tmp/bdt30/repo$ git tag -l
secret
```

Como só existe essa tag, vamos verificar seu conteúdo:
```
bandit30@bandit:/tmp/bdt30/repo$ git show secret
47e603bb428404d265f59c42920d81e5
```

Obtemos a flag! 🥷

##  Explicação

- Listagem de tags
- git Tags 
- Conteúdo remoto


## Links úteis

- https://git-scm.com/doc (documentação extensa, porém completa de como utilizar o git)

