# TP1 : Maîtrise réseau du poste

## I. Basics

### ☀️ Carte réseau WiFi

    l'adresse MAC de votre carte WIFI :

    C:\Users\Raphael>ipconfig /all
    
    Adresse physique . . . . . . . . . . . : 14-85-7F-7B-A8-31

     l'adresse IP de votre carte WIFI :

     C:\Users\Raphael>ipconfig /all

    Adresse IPv4. . . . . . . . . . . . . .: 172.20.10.3(préféré)

    le masque de sous-réseau du réseau LAN auquel vous êtes connectés en WiFi :

    C:\Users\Raphael>ipconfig /all

    Masque de sous-réseau. . . . . . . . . : 255.255.255.240
    CIDR : /28



### ☀️ Déso pas déso

    l'adresse de réseau du LAN auquel vous êtes connectés en WiFi :
    
    172.20.10.0

    l'adresse de broadcast : 

     172.20.10.3.255    

     le nombre d'adresses IP disponibles dans ce réseau :

     14

    
### ☀️ Hostname

    déterminer le hostname de votre PC :

    C:\Users\Raphael>ipconfig /all

    Configuration IP de Windows

    Nom de l’hôte . . . . . . . . . . : tototototototototototototototototo


### ☀️ Passerelle du réseau


    l'adresse IP de la passerelle du réseau :

     Passerelle par défaut. . . . . . . . . : 172.20.10.1

    l'adresse MAC de la passerelle du réseau :

    C:\Users\Raphael>ping 172.20.10.1

    C:\Users\Raphael>arp -a

      Adresse Internet      Adresse physique      Type
      172.20.10.1           32-82-16-33-c4-64     dynamique


### ☀️ Serveur DHCP et DNS


    l'adresse IP du serveur DHCP qui vous a filé une IP :

     C:\Users\Raphael>ipconfig /all

     Serveur DHCP . . . . . . . . . . . . . : 172.20.10.1

    l'adresse IP du serveur DNS que vous utilisez quand vous allez sur internet :

    C:\Users\Raphael>ipconfig /all

     Serveurs DNS. . .  . . . . . . . . . . : fe80::3082:16ff:fe33:c464%16
                                       1.0.0.1
                                       1.1.1.1
                                       192.168.1.1



### ☀️ Table de routage


    dans votre table de routage, laquelle est la route par défaut :

    PS C:\Users\Raphael> netstat -r

    IPv4 Table de routage
    ===========================================================================
    Itinéraires actifs :
    Destination réseau  Masque réseau  Adr. passerelle   Adr. interface Métrique
          0.0.0.0          0.0.0.0     10.33.79.254      10.33.76.210      30



# II. Go further


### ☀️ Hosts ?

    faites en sorte que pour votre PC, le nom b2.hello.vous corresponde à l'IP 1.1.1.1 :

    # Copyright (c) 1993-2009 Microsoft Corp.

    This is a sample HOSTS file used by Microsoft TCP/IP for Windows.

    [...]

	1.1.1.1		b2.hello.vous

    [...]

    prouvez avec un ping b2.hello.vous que ça ping bien 1.1.1.1 : 

    PS C:\Users\Raphael> ping b2.hello.vous

    Envoi d’une requête 'ping' sur b2.hello.vous [1.1.1.1] avec 32 octets de données :
    Réponse de 1.1.1.1 : octets=32 temps=10 ms TTL=57
    Réponse de 1.1.1.1 : octets=32 temps=11 ms TTL=57
    Réponse de 1.1.1.1 : octets=32 temps=13 ms TTL=57
    Réponse de 1.1.1.1 : octets=32 temps=15 ms TTL=57

    Statistiques Ping pour 1.1.1.1:
    Paquets : envoyés = 4, reçus = 4, perdus = 0 (perte 0%),
    Durée approximative des boucles en millisecondes :
    Minimum = 10ms, Maximum = 15ms, Moyenne = 12ms


### ☀️ Requêtes DNS

    à quelle adresse IP correspond le nom de domaine www.ynov.com :

     PS C:\Users\Raphael> ping ynov.com

    Envoi d’une requête 'ping' sur ynov.com [172.67.74.226] avec 32 octets de données :
    Réponse de 172.67.74.226 : octets=32 temps=10 ms TTL=57

    à quel nom de domaine correspond l'IP 174.43.238.89 :

    PS C:\Users\Raphael> nslookup 174.43.238.89

    Serveur :   one.one.one.one
    Address:  1.0.0.1

    Nom :    89.sub-174-43-238.myvzw.com
    Address:  174.43.238.89


### ☀️ Go mater une vidéo youtube et déterminer, pendant qu'elle tourne...

 Capture Wireshark [youtube](youtube.pcapng)
    
    l'adresse IP du serveur auquel vous êtes connectés pour regarder la vidéo :

    je suis connecté a l'adresse suivante : 91.68.245.143

    le port du serveur auquel vous êtes connectés :

    le port : 443

    le port que votre PC a ouvert en local pour se connecter au port du serveur distant :

    le port : 50591

### ☀️ Hop hop hop

    par combien de machines vos paquets passent quand vous essayez de joindre www.ynov.com :

    PS C:\Users\Raphael> tracert ynov.com

    Détermination de l’itinéraire vers ynov.com [104.26.10.233]
    avec un maximum de 30 sauts :

      1     6 ms     1 ms     1 ms  10.33.79.254
      2     2 ms     2 ms     3 ms  145.117.7.195.rev.sfr.net [195.7.117.145]
      3     2 ms     2 ms     1 ms  237.195.79.86.rev.sfr.net [86.79.195.237]
      4     3 ms     3 ms     3 ms  196.224.65.86.rev.sfr.net [86.65.224.196]
      5    10 ms    10 ms    11 ms  12.148.6.194.rev.sfr.net [194.6.148.12]
      6    11 ms    11 ms    10 ms  12.148.6.194.rev.sfr.net [194.6.148.12]
      7    11 ms    10 ms    10 ms  141.101.67.48
      8    11 ms    11 ms    10 ms  141.101.67.54
      9    13 ms    10 ms    18 ms  104.26.10.233

    Itinéraire déterminé.

    il passe donc par 9 machines.


### ☀️ IP publique


    l'adresse IP publique de la passerelle du réseau (le routeur d'YNOV donc si vous êtes dans les locaux d'YNOV quand vous faites le TP) :

    PS C:\Users\Raphael> nslookup myip.opendns.com resolver1.opendns.com
    Serveur :   dns.opendns.com
    Address:  208.67.222.222

    Réponse ne faisant pas autorité :
    Nom :    myip.opendns.com
    Address:  195.7.117.146

### ☀️ Scan réseau


    combien il y a de machines dans le LAN auquel vous êtes connectés :


# III. Le requin

### ☀️ Capture ARP


## capture ARP

la capture ARP en question [regarde elle est la](arp.pcapng)

filtré en ecrivant arp 



### ☀️ Capture DNS


## capture DNS

la capture DNS en question [regarde elle est la aussi](dns.pcapng)

filtré en ecrivant dns

### ☀️ Capture TCP


## capture TCP

la capture TCP en question [pour finir elle est la aussi](tcp.pcapng)

filtré en ecrivant TCP





    










