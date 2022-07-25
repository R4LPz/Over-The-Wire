# 🕵️ Bandit 18

A senha para o próximo nível é armazenada em um arquivo leia -me no diretório inicial. Infelizmente, alguém modificou o .bashrc para desconectá-lo quando você fizer login com SSH.

## Solução

Ao tentarmos realizar a conexão com o servidor, recebemos apenas uma mensagem e a conexão é encerrada:
```
...
Byebye !
Connection to bandit.labs.overthewire.org closed.
```

Para tentarmos contornar isso, podemos tentar invocar um pseudo terminal através do parâmetro '-t', se funcionar, podemos executar códigos arbitrários no servidor antes que a conexão seja encerrada.

Para testar, vamos executar um comando ls no servidor:
```
ssh -p 2220 bandit18@bandit.labs.overthewire.org -t 'ls -la'
This is a OverTheWire game server. More information on http://www.overthewire.org/wargames

bandit18@bandit.labs.overthewire.org's password: 
total 24
drwxr-xr-x  2 root     root     4096 May  7  2020 .
drwxr-xr-x 41 root     root     4096 May  7  2020 ..
-rw-r--r--  1 root     root      220 May 15  2017 .bash_logout
-rw-r-----  1 bandit19 bandit18 3549 May  7  2020 .bashrc
-rw-r--r--  1 root     root      675 May 15  2017 .profile
-rw-r-----  1 bandit19 bandit18   33 May  7  2020 readme
Connection to bandit.labs.overthewire.org closed.
```

Como visto, antes da conexão ser encerrada, recebemos os arquivos presentes no diretório home do servidor. Entre estes arquivos, existe um chamado readme, que possivelmente conterá a flag. 

Podemos verificar, novamente com o parâmetro -t, porém, realizando um cat no arquivo:
```
ssh -p 2220 bandit18@bandit.labs.overthewire.org -t 'cat readme'
This is a OverTheWire game server. More information on http://www.overthewire.org/wargames

bandit18@bandit.labs.overthewire.org's password: 
IueksS7Ubh8G3DCwVzrTd8rAVOwq3M5x
Connection to bandit.labs.overthewire.org closed.
```

E está lá, conseguimos a flag sem nos mantermos conectados ao servidor! 🥷

## Conceitos utilizados

- Interface de pseudo terminal
- Comando ssh
- Execução arbitrária de código

## Links úteis

- https://en.wikipedia.org/wiki/Pseudoterminal
- https://pt.wikipedia.org/wiki/C%C3%B3digo_arbitr%C3%A1rio

