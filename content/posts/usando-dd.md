+++
title = 'Usando Dd'
date = 2023-09-27T15:58:12-03:00
draft = true
+++

# Usando o comando DD

O comando dd(de direct copy) e um clássico dos ambientes Unix-Like, com ele você pode fazer uma copia exata de um arquivo, ou seja uma copia bit a bit.

Sintaxe básica:
```shell
$dd if=origem of=destino
```

Por exemplo:
```shell
bash-3.1$ ls -la
total 5272
drwxrwxrwx 2 v0rtex users 4096 2010-02-07 18:23 .
drwx--x--x 116 v0rtex users 4096 2010-02-07 18:03 ..
-rwxr-xr-x 1 v0rtex users 5375842 2007-12-25 21:04 05 - Whole Lotta Love.mp3
bash-3.1$ dd if=05\ -\ Whole\ Lotta\ Love.mp3 of=whole_lotta_love.mp3
10499+1 registros de entrada
10499+1 registros de saída
5375842 bytes (5,4 MB) copiados, 0,0682746 s, 78,7 MB/s
bash-3.1$ ls -lh
total 11M
-rwxr-xr-x 1 v0rtex users 5,2M 2007-12-25 21:04 05 - Whole Lotta Love.mp3
-rw-r--r-- 1 v0rtex users 5,2M 2010-02-07 18:23 whole_lotta_love.mp3
```

Foi feita uma copia do arquivo “05\ -\ Whole\ Lotta\ Love.mp3″ com o nome whole_lotta_love.mp3 :) uma copia exata feita bit-a-bit pelo comando dd.

Dicas para uso do comando dd:

Copiando um HD para um arquivo.
```shell
# dd if=/dev/sda of=~/backup_hd.img
```

Com isso será feita uma copia exata do hd dentro do diretório do root(#) com o nome “backup_hd.img”.

Se quiser restaurar o “backp_hd.img” no /dev/sda2(lembre o sda2 deve ter pelo menos o mesmo tamanho do arquivo “backup.hd” se não os resultados poderão ser desastrosos.
```shell
# dd if=backup_hd.img of=/dev/sda2
```

Copiando HD para HD:
```shell
#dd if=/dev/sda1 of=/dev/sda2
```
Com isso será feita copia do /dev/sda1 para o /dev/sda2.

Fazendo uma copia do hd para um arquivo compactado:
```shell
dd if=/dev/sda1 | gzip > backup_hd.img.gz
```
Para descompactar dentro de outro HD use:
```shell
# gzip -d -c backup_hd.img.gz | dd of=/dev/sda2
```

Criar um arquivo .iso:
```shell
#dd if=diretorio of=iso_do_diretorio.iso
```

Para visualizar progresso de cópia de arquivos, vá em outro terminal e execute:
```shell
$ watch df -h
```

Para converter todos as letras maiúsculas de um documento para letras minúsculas:
```shell
$dd if=ficheiro1 of=ficheiro2 conv=lcase
```
se quisermos converter todas as letras do ficheiro2 para maiúsculas:
```shell
$dd if=ficheiro2 of=ficheiro3 conv=ucase
```

Para zerar(formatar) o seu HD:
```shell
# dd if=/dev/zero of=/dev/hda
```

Gerar senhas de forma (pseudo) aleatória:
```shell
$ dd if=/dev/random bs=1 count=8 | base64 - 
```

Se o seu dd estiver atualizado (o pacote *coreutils* for a versão 8.24 ou superior) você pode usar o parametro: *status=progress* por exemplo:
```shell
dd if=/dev/sda of=/dev/sdb bs=1024k status=progress
```
Espero que as informações sobre o dd seja bem uteis, quando tiver novas dicas venho a postar mais.

Att.