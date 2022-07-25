# 🕵️ Bandit 32

Depois de todo esse git, é hora de outra fuga. Boa sorte!

## Solução

Quando realizamos a conexão, somos apresentados ao que o servidor chamou de uppercase shell. Isso faz com que todos os comando executados sejam convertidos para caixa alta antes de serem executados.

O problema disso é que o shell não entende estes comandos em caixa alta, nos 'travandos a executas os comando usuais:
```
WELCOME TO THE UPPERCASE SHELL
>> 

>> ls
sh: 1: LS: not found
>> pwd
sh: 1: PWD: not found
>> 
```

Para tentar contornar isso, podemos utilizar uma variável de ambiente que não terá letras e portanto não será convertida em caixa alta.

As variáveis posicionais são uma espécie de comando específico para o linux onde temos valores predefinidos. 

Por exemplo, o valor $0 retornará o nome do arquivo que está sendo executado ou o shell padrão que está sendo executado. 

Dessa forma se enviarmos este comando, como os comandos provavelmente são executados em uma chamada de shell dentro do sistema, teremos como valor de entrada o shell padrão no sistema. Vejamos:

```
>> $0
$
```

Como visto, agora saimos do código e estamos em um shell a parte, vamos começar qual usuário está executando o código:
```
$ whoami
bandit33
```

Como o usuário é bandit33, o programa escalou privilégios e nos deu permissões do bandit33. Vamos listar os arquivos no diretório home para ver os possíveis acessos do uppershell:
```
$ ls -la
total 28
drwxr-xr-x  2 root     root     4096 May  7  2020 .
drwxr-xr-x 41 root     root     4096 May  7  2020 ..
-rw-r--r--  1 root     root      220 May 15  2017 .bash_logout
-rw-r--r--  1 root     root     3526 May 15  2017 .bashrc
-rw-r--r--  1 root     root      675 May 15  2017 .profile
-rwsr-x---  1 bandit33 bandit32 7556 May  7  2020 uppershell
```

Como já temos o acesso do bandit33, vamos chamar o bash para facilitar nossa visualização e buscar o conteúdo da flag:
```
$ /bin/bash
bandit33@bandit:~$ cat /etc/bandit_pass/bandit33 
c9c3199ddf4121b10cf581a98d51caee
```

Obtemos a flag!

Ao realizar o push obtemos a flag através da mensagem de retorno! 🥷

##  Conceitos utilizados

- Variáveis posicionais
- Tipos de shell
- Escalação de privilégios

## Links úteis

- https://www.vivaolinux.com.br/artigo/Variaveis-padrao-para-usar-em-seus-scripts-em-shell
- https://br.ccm.net/contents/320-linux-o-shell
