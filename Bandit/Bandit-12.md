# 🕵️ Bandit 00

A senha para o próximo nível é armazenada no arquivo data.txt , que é um hexdump de um arquivo que foi compactado repetidamente. Para este nível pode ser útil criar um diretório em /tmp no qual você possa trabalhar usando mkdir. 

*Por exemplo*: mkdir /tmp/myname123. Em seguida, copie o arquivo de dados usando cp e renomeie-o usando mv (leia as páginas de manual!)

## Solução

**Essa é a primeira fuga, portanto, não se assuste com o tamanho da solução, apesar de extensa, a lógica não é complexa!**

Listando os arquivos no diretório home:
```
bandit12@bandit:~$ ls
data.txt
```

Como precisaremos manusear este arquivo, e só temos permissão de criação no diretório '/tmp', vamos criar uma pasta e copiar o arquivo para ela:
```
bandit12@bandit:~$ mkdir /tmp/bdt12

bandit12@bandit:~$ cp data.txt /tmp/bdt12

bandit12@bandit:~$ cd /tmp/bdt12
```

Verificando o conteúdo do arquivo, vemos que se trata de um hexdump como informado:
```
bandit12@bandit:/tmp/bdt12$ cat data.txt 
00000000: 1f8b 0808 0650 b45e 0203 6461 7461 322e  .....P.^..data2.
00000010: 6269 6e00 013d 02c2 fd42 5a68 3931 4159  bin..=...BZh91AY
00000020: 2653 598e 4f1c c800 001e 7fff fbf9 7fda  &SY.O...........
00000030: 9e7f 4f76 9fcf fe7d 3fff f67d abde 5e9f  ..Ov...}?..}..^.
00000040: f3fe 9fbf f6f1 feee bfdf a3ff b001 3b1b  ..............;.
...
```

Utilizamos o comando xxd para realizar o "dump reverso", ou seja, transformar o arquivo hexdump em um binário:
```
bandit12@bandit:/tmp/bdt12$ cat data.txt | xxd -r > data
```

Verificando o formato do arquivo gerado, vemos que é um arquivo compactado em gzip.
Vamos alterar sua extensão para não nos confundirmos e realizar a descompressão.
```
bandit12@bandit:/tmp/bdt12$ file data
data: gzip compressed data, was "data2.bin", last modified: Thu May  7 18:14:30 2020, max compression, from Unix

bandit12@bandit:/tmp/bdt12$ mv data data.gz

bandit12@bandit:/tmp/bdt12$ gzip -d data.gz 
```

Verificando o formato do arquivo gerado, vemos que é um arquivo compactado em bzip2.
Vamos alterar sua extensão para não nos confundirmos e realizar a descompressão.
```
bandit12@bandit:/tmp/bdt12$ file data
data: bzip2 compressed data, block size = 900k

bandit12@bandit:/tmp/bdt12$ mv data data.bz

bandit12@bandit:/tmp/bdt12$ bzip2 -d data.bz
```

Verificando o formato do arquivo gerado, vemos que é um arquivo compactado em gzip.
Vamos alterar sua extensão para não nos confundirmos e realizar a descompressão.
```
bandit12@bandit:/tmp/bdt12$ file data
data: gzip compressed data, was "data4.bin", last modified: Thu May  7 18:14:30 2020, max compression, from Unix

bandit12@bandit:/tmp/bdt12$ mv data data.gz

bandit12@bandit:/tmp/bdt12$ gzip -d data.gz 
```

Verificando o formato do arquivo gerado, vemos que é um arquivo compactado em tar.
Vamos alterar sua extensão para não nos confundirmos e realizar a descompressão.
```
bandit12@bandit:/tmp/bdt12$ file data
data: POSIX tar archive (GNU)

bandit12@bandit:/tmp/bdt12$ mv data data.tar

bandit12@bandit:/tmp/bdt12$ tar -xvf data.tar 
data5.bin
```

Verificando o formato do arquivo gerado, vemos que é um arquivo compactado em tar.
Vamos alterar sua extensão para não nos confundirmos e realizar a descompressão.
```
bandit12@bandit:/tmp/bdt12$ file data5.bin 
data5.bin: POSIX tar archive (GNU)

bandit12@bandit:/tmp/bdt12$ mv data5.bin data.tar 

bandit12@bandit:/tmp/bdt12$ tar -xvf data.tar 
data6.bin
```

Verificando o formato do arquivo gerado, vemos que é um arquivo compactado em bzip2.
Vamos alterar sua extensão para não nos confundirmos e realizar a descompressão.
```
bandit12@bandit:/tmp/bdt12$ file data6.bin 
data6.bin: bzip2 compressed data, block size = 900k

bandit12@bandit:/tmp/bdt12$ mv data6.bin data.bz

bandit12@bandit:/tmp/bdt12$ bzip2 -d data.bz
```

Verificando o formato do arquivo gerado, vemos que é um arquivo compactado em tar.
Vamos alterar sua extensão para não nos confundirmos e realizar a descompressão.
```
bandit12@bandit:/tmp/bdt12$ file data
data: POSIX tar archive (GNU)

bandit12@bandit:/tmp/bdt12$ mv data data.tar

bandit12@bandit:/tmp/bdt12$ tar -xvf data.tar 
data8.bin
```

Verificando o formato do arquivo gerado, vemos que é um arquivo compactado em gzip e que esta é a compressão maxima que conseguimos alcançar no Unix.
Vamos alterar sua extensão para não nos confundirmos e realizar a descompressão.
```
bandit12@bandit:/tmp/bdt12$ file data8.bin 
data8.bin: gzip compressed data, was "data9.bin", last modified: Thu May  7 18:14:30 2020, max compression, from Unix

bandit12@bandit:/tmp/bdt12$ mv data8.bin data.gz

bandit12@bandit:/tmp/bdt12$ gzip -d data.gz 
```

Verificando o formato do arquivo gerado, vemos que é um arquivo ASCII de texto aberto.
Vamos verificar o conteúdo do arquivo
```
bandit12@bandit:/tmp/bdt12$ file data
data: ASCII text

bandit12@bandit:/tmp/bdt12$ cat data
The password is 8ZjyCRiBWFYkneahHwxCv3wb2a1ORpYL
```

Obtemos a flag! 🥷

## Conceitos utilizados

- O que são hexdumps
- Conversão de arquivos hexadecimais em binários
- Comando xxd
- Compressão de arquivos Unix
- comando gzip
- comando bzip2
- comando tar

## Links úteis

- https://pt.wikipedia.org/wiki/Hex_dump
- https://howtosanta.com/portuguese/guia-do-iniciante-do-linux-xxd-command-com-exemplos/
- https://www.linuxdescomplicado.com.br/2016/11/8-ferramentas-para-compressao-de-arquivos-no-linux.html

