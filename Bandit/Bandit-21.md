# 🕵️ Bandit 21

Um programa está sendo executado automaticamente em intervalos regulares a partir do cron , o agendador de tarefas baseado em tempo. Procure em /etc/cron.d/ a configuração e veja qual comando está sendo executado.


## Solução

Como precisamos de um processo do cron, vamos entrar em cron.d e listar seus arquivos:
```
bandit21@bandit:~$ cd /etc/cron.d

bandit21@bandit:/etc/cron.d$ ls
cronjob_bandit15_root  cronjob_bandit22  cronjob_bandit24
cronjob_bandit17_root  cronjob_bandit23  cronjob_bandit25_root
```

Agora que vemos que existe um job com nome de bandit22, vamos verificar o que ele está executando:
```
bandit21@bandit:/etc/cron.d$ cat cronjob_bandit22 
@reboot bandit22 /usr/bin/cronjob_bandit22.sh &> /dev/null
* * * * * bandit22 /usr/bin/cronjob_bandit22.sh &> /dev/null
```

O script sendo executado se encontra em /usr/bin, vamos então ver qual seu conteúdo:
```
bandit21@bandit:/etc/cron.d$ cat /usr/bin/cronjob_bandit22.sh 
#!/bin/bash
chmod 644 /tmp/t7O6lds9S0RqQh9aMcz6ShpAoZKF7fgv
cat /etc/bandit_pass/bandit22 > /tmp/t7O6lds9S0RqQh9aMcz6ShpAoZKF7fgv
```

O script tem como finalidade, através do bash, dar permissões de leitura e escrita para um arquivo em /tmp e inserir nele o valor da flag.

Vamos então buscar o conteúdo desse arquivo, que contém nossa flag:
```
bandit21@bandit:/etc/cron.d$ cat /tmp/t7O6lds9S0RqQh9aMcz6ShpAoZKF7fgv
Yk7owGAcWjwMVRwrTesJEwB7WVOiILLI
```

Obtemos a flag! 🥷

## Conceitos utilizados

- Cron - agendador de eventos
- Scripts shell no bash
- Permissão de escrita 

## Links úteis

- https://medium.com/totvsdevelopers/entendendo-o-crontab-607bc9f00ed3
- https://www.devmedia.com.br/introducao-ao-shell-script-no-linux/25778

