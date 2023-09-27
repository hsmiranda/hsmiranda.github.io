+++
title = 'Utilizando o scanner de rede nmap'
date = 2023-09-27T15:59:57-03:00
draft = false
+++

# Utilizando o scanner de rede nmap

O Nmap (“Network Mapper”) é uma ferramenta de código aberto para exploração de 
rede e auditoria de segurança. Ela foi desenhada para escanear rapidamente redes
amplas, embora também funcione muito bem contra hosts individuais.

O Nmap utiliza pacotes IP em estado bruto (raw) de maneira inovadora para 
determinar quais hosts estão disponíveis na rede, quais serviços 
(nome da aplicação e versão) os hosts oferecem, quais sistemas operacionais (e 
versões de SO) eles estão executando, que tipos de filtro de pacotes/firewalls 
estão em uso, e dezenas de outras características.

Embora o Nmap seja normalmente utilizado para auditorias de segurança, muitos 
administradores de sistemas e rede consideram-no útil para tarefas rotineiras 
tais como inventário de rede, gerenciamento de serviços de atualização 
agendados, e monitoramento de host ou disponibilidade de serviço.

Além disso, como já citado em post anterior, essa ferramenta pode ser utilizada 
para validar o funcionamento do firewall e IPS.

Neste texto são apresentadas diversas dicas para o uso do scanner nmap.

Usando nmap para descoberta de host.
```shell
# nmap -sL 128.230.18.30-35
Host npropane.syr.edu (128.230.18.30) not scanned
Host helpeiam1.syr.edu (128.230.18.31) not scanned
Host tracker5-18.syr.edu (128.230.18.32) not scanned
Host mirage2.syr.edu (128.230.18.33) not scanned
Host backup01-18.syr.edu (128.230.18.34) not scanned
Host cwis01.syr.edu (128.230.18.35) not scanned
Nmap done: 6 IP addresses (0 hosts up) scanned in 6.628 seconds
```

Utilizando como banner scan, escaneado uma faixa de ips, procurando pela porta 25 rodando um e-mail.
```shell
# nmap -sV 12.150.145.135-139 -p25 | grep IMail -B 3
Interesting ports on 138.145.static.conninc.com (12.150.145.138):
PORT STATE SERVICE VERSION
25/tcp open smtp IMail NT-ESMTP 6.06 28262-4
--
Interesting ports on 139.145.static.conninc.com (12.150.145.139):
PORT STATE SERVICE VERSION
25/tcp open smtp IMail NT-ESMTP 6.06 28263-5
```
Usando como banner scan, escaneado uma faixa de ips,procurando pela porta 25 rodando um e-mail,e salvando a saída em um arquivo
```shell
# nmap -sV 12.150.145.137-139 -p25 | grep IMail -B 3 >> nmap.txt
# cat nmap.txt
Interesting ports on 138.145.static.conninc.com (12.150.145.138):
PORT STATE SERVICE VERSION
25/tcp open smtp IMail NT-ESMTP 6.06 29384-6
Interesting ports on 139.145.static.conninc.com (12.150.145.139):
PORT STATE SERVICE VERSION
25/tcp open smtp IMail NT-ESMTP 6.06 29385-7
```

Usando a mais intensiva opção de checagem de versão.
```shell
# nmap -sV --version-all 128.230.18.35 -p 80
Starting Nmap 4.50 ( http://insecure.org ) at 2008-01-17 22:37 EST
Interesting ports on cwis01.syr.edu (128.230.18.35):
PORT STATE SERVICE VERSION
80/tcp open http Apache httpd
```
Usando nmap como scanner de banners, escaneando uma faixa aleatória de IPs procurando pela porta 21 aberta, rodando o ProFTP.
```shell
# nmap -sV -iR 1500 -p21 | grep ProFTPD -B 3
Starting Nmap 4.50 ( http://insecure.org ) at 2008-01-17 17:41 EST
Interesting ports on www.buford-thompson.net (161.58.19.143):
PORT STATE SERVICE VERSION
21/tcp open ftp ProFTPD
```
Usando o nmap para descobrir o sistema operacional do host
```shell
# nmap -PN -O --osscan-limit 38.117.198.214 | grep Running
Running (JUST GUESSING) : ZyXEL ZyNOS (96%)
```
Usando nmap como tracerouter verificando a porta aberta é contando os hops
```shell
# nmap --traceroute 128.230.18.35
Starting Nmap 4.50 ( http://insecure.org ) at 2008-01-17 22:27 EST
Interesting ports on cwis01.syr.edu (128.230.18.35):
Not shown: 1656 closed ports, 49 filtered ports
PORT STATE SERVICE
80/tcp open http
TRACEROUTE (using port 80/tcp)
HOP RTT ADDRESS
1 2.89 192.168.1.1
2 12.18 10.114.0.1
3 9.52 172.22.5.13
4 12.33 172.22.5.69
5 10.86 172.22.33.73
6 12.48 172.22.32.106
7 15.21 12.86.87.29
8 41.73 tbr2.attga.ip.att.net (12.122.96.74)
9 41.78 tbr1.dlstx.ip.att.net (12.122.2.89)
10 73.50 ggr3.dlstx.ip.att.net (12.123.16.201)
11 42.87 br2-a3120s2.attga.ip.att.net (192.205.33.206)
12 66.36 66.192.240.226
13 74.74 64-132-176-170.static.twtelecom.net (64.132.176.170)
14 77.85 128.230.61.1
15 74.08 c6509r-srv.syr.edu (128.230.61.58)
16 73.36 cwis01.syr.edu (128.230.18.35)
Nmap done: 1 IP address (1 host up) scanned in 111.295 seconds
```
Usando nmap para testar o estado de uma porta.
```shell
# nmap --reason 128.230.18.35 -p 21
Starting Nmap 4.50 ( http://insecure.org ) at 2008-01-17 22:31 EST
Interesting ports on cwis01.syr.edu (128.230.18.35):
PORT STATE SERVICE REASON
21/tcp filtered ftp no-response

Nmap done: 1 IP address (1 host up) scanned in 1.247 seconds
```
Usando nmap para MAC address spoofing.
```shell
# nmap –spoof-mac 08:00:69:02:01:FC -iR 3
Starting Nmap 4.50 ( http://insecure.org ) at 2008-01-17 22:51 EST
Spoofing MAC address 08:00:69:02:01:FC (Silicon Graphics)
Nmap done: 3 IP addresses (0 hosts up) scanned in 3.387 seconds
```

Fazendo uma varredura com IPs forjado,com uma escolha aleatória de alvos.
```shell
# nmap -D 198.162.1.100,198.162.1.101 -iR 3
Starting Nmap 4.50 ( http://insecure.org ) at 2008-01-17 23:22 EST
Nmap done: 3 IP addresses (0 hosts up) scanned in 3.082 seconds
```
Bom com isso tivemos alguns exemplo do uso do NMAP e constantamos que ele é uma
ferramenta essencial para todos os sysadmin.