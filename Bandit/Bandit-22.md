# 🕵️ Bandit 22

Um programa está sendo executado automaticamente em intervalos regulares a partir do cron , o agendador de tarefas baseado em tempo. Procure em /etc/cron.d/ a configuração e veja qual comando está sendo executado.


## Solução

Primeiramente vamos verificar qual job o cron está executando relativo ao bandit23:
```
bandit22@bandit:~$ cd /etc/cron.d

bandit22@bandit:/etc/cron.d$ ls
cronjob_bandit15_root  cronjob_bandit22  cronjob_bandit24
cronjob_bandit17_root  cronjob_bandit23  cronjob_bandit25_root
```

Verificando qual script está sendo executado:
```
bandit22@bandit:/etc/cron.d$ cat cronjob_bandit23 
@reboot bandit23 /usr/bin/cronjob_bandit23.sh  &> /dev/null
* * * * * bandit23 /usr/bin/cronjob_bandit23.sh  &> /dev/null
```

Sabendo qual arquivo está sendo executado, vejamos seu conteúdo e vamos analisar o que acontece neste código:
```
bandit22@bandit:/etc/cron.d$ cat /usr/bin/cronjob_bandit23.sh
#!/bin/bash

myname=$(whoami)
mytarget=$(echo I am user $myname | md5sum | cut -d ' ' -f 1)

echo "Copying passwordfile /etc/bandit_pass/$myname to /tmp/$mytarget"

cat /etc/bandit_pass/$myname > /tmp/$mytarget
```

Primeiramente, o script buscará qual usuário o executou através do comando whoami, seu retorno será uma string, que será armazenada na variável myname. 

Em seguida, encripta via md5sum a string "I am user 'nome do usuário'", removendo através do comando cut o espaço final na string de retorno.

Dessa forma, a variável mytarget terá um hash gerado pela frase acima. 

Por fim, o código pega o valor da flag para o usuário informado e a coloca em um arquivo em /tmp com o nome do hash gerado.
Sabendo disso, é fácil notar a relação entre o usuário whoami e a obtenção da flag, isso pois, o arquivo da flag tem o mesmo nome do usuário.

Porém, precisamos contornar de alguma forma, nos passando pelo bandit23. Vamos então definir a variável myname como bandit23 e descobrir o valor do hash para isso:
```
bandit22@bandit:~$ myname=bandit23

bandit22@bandit:~$ echo I am user $myname | md5sum | cut -d ' ' -f 1
8ca319486bfbbc3663ea0fbe81326349
```

Agora que sabemos o valor do hash para o bandit23, basta buscarmos este arquivo no diretório /tmp:
```
bandit22@bandit:/tmp/bdt22$ cat /tmp/8ca319486bfbbc3663ea0fbe81326349
jc1udXuA1tiHqjIsL8yaapX5XIAI6i0n
```

Obtemos a flag! 🥷

## Conceitos utilizados

- Criptografia md5
- Comando cut
- Análise de shell script

## Links úteis

- https://pt.wikipedia.org/wiki/MD5
- Manual do comando cut `man cut`

