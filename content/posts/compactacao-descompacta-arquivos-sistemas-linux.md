+++
title = 'Compactacao Descompacta Arquivos Sistemas Linux'
date = 2023-09-27T15:59:25-03:00
draft = false
+++
---

Compactação e descompactação de arquivos em sistemas Linux 

Estive um bom tempo sem cabeça para escrever mais voltando ativa segue abaixo um artigo sobre compactação e descompactação de arquivo em ambientes Linux.

## Gzip
O gzip é a abreviação de GNU zip, um Software Livre de compressão sem perda de 
dados, criado por Jean-loup Gailly e Mark Adler. O programa é baseado no 
algoritmo DEFLATE. A extensão gerada pelo gzip é o .gz, e seu formato contém 
apenas um arquivo comprimido. 

Em sistemas UNIX é comum gerar um arquivo contendo diversos outros arquivos com
o programa tar, e depois comprimi-lo com o gzip, gerando um arquivo .tar.gz.
Não confundir com o formato ZIP, que é mais portável e comporta diversos 
arquivos sem precisar recorrer a um outro programa externo para isso.

### Uso pratico do gzip:

Compactando:
```shell
$ gzip nome_do_arquivo
```

O resultado sera um arquivo nome_do_arquivo.gz, para ter mais eficiência em compactar o arquivo usa-se o parâmetro -9:
```shell
$gzip -9 nome_do_arquivo
```

Descompactando:
```shell
$gunzip nome_do_arquivo.gz
```
Isso ira descompactar o arquivo no diretório atual.

## Bzip2

O bzip2 é um algoritmo e um software Compactador de arquivos. Sua licença é 
livre e de código aberto (open source), podendo ser melhor desenvolvido para 
fins próprios. Seu desenvolvedor é Julian Seward, tendo começado seu trabalho 
com este projeto em 1996, porém vindo somente a ficar popular no ano 2000. 

A principal vantagem em favor de bzip2 é o tamanho do arquivo compactado. bzip2
quase sempre irá comprimir melhor que gzip. Em alguns casos, isto pode resultar
em arquivos dramaticamente menores. Isto pode ser uma grande vantagem para 
pessoas com conexões lentas. A desvantagem de bzip2 é que ele utiliza mais 
recursos de processamento do que o gzip. Isto significa que descomprimir um 
arquivo com bzip2 geralmente será mais demorado e utilizar mais o processador 
do que o gzip o faria. 

Na escolha de um programa de compressão a se usado, você precisa considerar o 
tempo de compressão e o tamanho do arquivo compactado e determinar o que é 
mais importante.

Uso pratico do bzip2

Compactando:
```shell
$bzip2 nome_do_arquivo
```

Será gerado um arquivo .bz2, para obter melhor eficiência usa-se o parâmetro -9:
```shell
$bzip2 -9 nome_do_arquivo
```

Descompactando:
```shell
$gunzip2 nome_do_arquivo.bz2
```
Irá descompactar o arquivo no diretório atual.

## Tar

O TAR ou tar (abreviatura de Tape ARchive), é um formato de arquivamento de 
arquivos. Apesar do nome “tar” ser derivado de “tape archive”, o seu uso não 
se restringe a fitas magnéticas. Ele se tornou largamente usado para armazenar
vários arquivos em um único, preservando informações como datas e permissões. 
Normalmente é produzido pelo comando “tar”. É suportado pelo programa Winrar. 

O tartambém é o nome de um programa de arquivamento desenvolvido para armazenar 
e extrair arquivos de um arquivo tar (que contém os demais) conhecido como 
tarfile ou tarball. 

O primeiro argumento para tar deve ser uma das seguintes opções: Acdrtux, 
seguido por uma das seguintes funções adicionais. Os argumento finais do tar 
são os nomes dos arquivos ou diretórios nos quais eles podem ser arquivados. 

O uso de um nome de diretório, implica sempre que os subdiretórios sob ele, 
serão incluídosno arquivo. Uso pratico:

Descompactando tar.gz :
```shell
$ tar -zxvf arquivo.tar.gz
```
Descompactando tar.bz2:
```shell 
$tar -jxvf arquivo.tar.bz

Isso ira descompactar o arquivo no diretório atual. 

Para criar um arquivo.tar use:
```shell
$ tar -cvf arq.tar diretorio
```

Para compactar em tar.gz:
```shell
$ tar -zcvf arquivos.tar.gz arquivos
```
Para compactar em tar.bz2:
```shell
$ tar -jcvf arquivos.tar.bz2 arquivos
```

Lista de parâmetros:
```
-c –cria um novo arquivo tar;
-M –cria, lista ou extrai um arquivo multivolume;
-p –mantém as permissões originais do(s) arquivo(s);
-r –acrescenta arquivos a um arquivo tar;
-t –exibe o conteúdo de um arquivo tar;
-v –exibe detalhes da operação;
-w –pede confirmação antes de cada ação;
-x –extrai arquivos de um arquivo tar;
-z –comprime ou extrai arquivos tar resultante com o gzip;
-j –comprime ou extrai arquivos tar resultante com o bz2;
-f –especifica o arquivo tar a ser usado;
-C –especifica o diretório dos arquivos a serem armazenados.
```

## Zip

Arquivo de compressão é denominado zip, e o de descompressão é denominado unzip.
```shell
$ zip teste 
```

*Isto criará o arquivo teste.zip, que irá conter todos os arquivos do diretório 
atual. 

O zip adicionará a extensão .zip automaticamente, de forma que não há 
necessidade de incluí-la no nome do arquivo. Você também pode recursivamente 
comprimir os subdiretórios existentes:
```shell
$ zip -r teste *
```

Bem como, descomprimir arquivos também é fácil.
```shell
$ unzip teste.zip
```

Isto irá extrair todos os arquivos e diretórios no arquivo teste.zip. 
Os utilitários zip têm várias opções avançadas para criar pacotes que podem 
se extrair automaticamente, excluir arquivos, controlar o tamanho do arquivo 
compactado, mostrar o que acontecerá e muito mais. Veja as páginas de manual 
dos comandos zip e unzip para descobrir como usar essas opções.