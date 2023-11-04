## COMPTE RENDU

### ☀️ Sur node1.lan1.tp2

    afficher ses cartes réseau :

    [raph@node1 ~]$ ip a

    [...]

    2: enp0s3: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc fq_codel state UP group default qlen 1000
    link/ether 08:00:27:88:c0:1d brd ff:ff:ff:ff:ff:ff
    inet 10.1.1.11/24 brd 10.1.1.255 scope global noprefixroute enp0s3
       valid_lft forever preferred_lft forever
    inet6 fe80::a00:27ff:fe88:c01d/64 scope link
       valid_lft forever preferred_lft forever

    afficher sa table de routage :

    [raph@node1 ~]$ ip route
    10.1.1.0/24 dev enp0s3 proto kernel scope link src 10.1.1.11 metric 100

    prouvez qu'il peut joindre node2.lan2.tp2 :

    [root@node1 raph]# ping 10.1.2.12
    PING 10.1.2.12 (10.1.2.12) 56(84) bytes of data.
    64 bytes from 10.1.2.12: icmp_seq=1 ttl=63 time=0.547 ms
    64 bytes from 10.1.2.12: icmp_seq=2 ttl=63 time=1.13 ms
    64 bytes from 10.1.2.12: icmp_seq=3 ttl=63 time=1.38 ms
    64 bytes from 10.1.2.12: icmp_seq=4 ttl=63 time=1.94 ms
    64 bytes from 10.1.2.12: icmp_seq=5 ttl=63 time=0.885 ms
    64 bytes from 10.1.2.12: icmp_seq=6 ttl=63 time=1.42 ms
    64 bytes from 10.1.2.12: icmp_seq=7 ttl=63 time=1.70 ms
    64 bytes from 10.1.2.12: icmp_seq=8 ttl=63 time=1.34 ms
    64 bytes from 10.1.2.12: icmp_seq=9 ttl=63 time=0.922 ms
    ^C
    --- 10.1.2.12 ping statistics ---
    9 packets transmitted, 9 received, 0% packet loss, time 8094ms
    rtt min/avg/max/mdev = 0.547/1.250/1.938/0.405 ms

    prouvez avec un traceroute que le paquet passe bien par router.tp2 :

    [root@node1 raph]# traceroute 10.1.1.254
    traceroute to 10.1.1.254 (10.1.1.254), 30 hops max, 60 byte packets
    1  10.1.1.254 (10.1.1.254)  0.336 ms !X  0.299 ms !X  0.290 ms !X


## II. Interlude accès internet

### ☀️ Sur router.tp2

      prouvez que vous avez un accès internet (ping d'une IP publique) :

      [root@routeur raph]# ping 8.8.8.8
      PING 8.8.8.8 (8.8.8.8) 56(84) bytes of data.
      64 bytes from 8.8.8.8: icmp_seq=1 ttl=114 time=15.4 ms
      64 bytes from 8.8.8.8: icmp_seq=2 ttl=114 time=16.0 ms
      64 bytes from 8.8.8.8: icmp_seq=3 ttl=114 time=15.7 ms
      64 bytes from 8.8.8.8: icmp_seq=4 ttl=114 time=15.6 ms
      64 bytes from 8.8.8.8: icmp_seq=5 ttl=114 time=15.6 ms
      64 bytes from 8.8.8.8: icmp_seq=6 ttl=114 time=15.4 ms
      64 bytes from 8.8.8.8: icmp_seq=7 ttl=114 time=16.1 ms
      64 bytes from 8.8.8.8: icmp_seq=8 ttl=114 time=16.3 ms
      64 bytes from 8.8.8.8: icmp_seq=9 ttl=114 time=16.2 ms
      ^C
      --- 8.8.8.8 ping statistics ---
      9 packets transmitted, 9 received, 0% packet loss, time 8016ms
      rtt min/avg/max/mdev = 15.380/15.814/16.263/0.311 ms

      prouvez que vous pouvez résoudre des noms publics (ping d'un nom de domaine public) :

      [root@routeur raph]# ping google.com
      PING google.com (142.250.179.110) 56(84) bytes of data.
      64 bytes from par21s20-in-f14.1e100.net (142.250.179.110): icmp_seq=1 ttl=115 time=15.2 ms
      64 bytes from par21s20-in-f14.1e100.net (142.250.179.110): icmp_seq=2 ttl=115 time=15.9 ms
      64 bytes from par21s20-in-f14.1e100.net (142.250.179.110): icmp_seq=3 ttl=115 time=16.7 ms
      64 bytes from par21s20-in-f14.1e100.net (142.250.179.110): icmp_seq=4 ttl=115 time=15.8 ms
      64 bytes from par21s20-in-f14.1e100.net (142.250.179.110): icmp_seq=5 ttl=115 time=15.9 ms
      64 bytes from par21s20-in-f14.1e100.net (142.250.179.110): icmp_seq=6 ttl=115 time=16.5 ms
      ^C
      --- google.com ping statistics ---
      6 packets transmitted, 6 received, 0% packet loss, time 5010ms
      rtt min/avg/max/mdev = 15.204/15.980/16.671/0.486 ms


   ### ☀️ Accès internet LAN1 et LAN2

      dans le compte-rendu, mettez-moi que la conf des points précédents sur node2.lan1.tp2 :

      [root@node2 raph]# cat /etc/sysconfig/network-scripts/ifcfg-enp0s3
      DEVICE=enp0s3

      BOOTPROTO=static
      ONBOOT=yes

      IPADDR=10.1.1.12
      NETMASK=255.255.255.0

      GATEWAY=10.1.2.254
      DNS1=1.1.1.1

      prouvez que node2.lan1.tp2 a un accès internet :

      il peut ping une IP publique :

      [root@node2 raph]# ping 8.8.8.8
      PING 8.8.8.8 (8.8.8.8) 56(84) bytes of data.
      64 bytes from 8.8.8.8: icmp_seq=1 ttl=113 time=17.2 ms
      64 bytes from 8.8.8.8: icmp_seq=2 ttl=113 time=17.0 ms
      64 bytes from 8.8.8.8: icmp_seq=3 ttl=113 time=16.4 ms
      64 bytes from 8.8.8.8: icmp_seq=4 ttl=113 time=17.2 ms
      64 bytes from 8.8.8.8: icmp_seq=5 ttl=113 time=20.6 ms
      64 bytes from 8.8.8.8: icmp_seq=6 ttl=113 time=17.1 ms
      64 bytes from 8.8.8.8: icmp_seq=7 ttl=113 time=16.8 ms
      64 bytes from 8.8.8.8: icmp_seq=8 ttl=113 time=17.0 ms
      64 bytes from 8.8.8.8: icmp_seq=9 ttl=113 time=17.9 ms
      64 bytes from 8.8.8.8: icmp_seq=10 ttl=113 time=17.1 ms
      ^C
      --- 8.8.8.8 ping statistics ---
      10 packets transmitted, 10 received, 0% packet loss, time 9019ms
      rtt min/avg/max/mdev = 16.416/17.433/20.624/1.118 ms


      il peut ping un nom de domaine public :

      [root@node2 raph]# ping www.ynov.com
      PING www.ynov.com (104.26.11.233) 56(84) bytes of data.
      64 bytes from 104.26.11.233 (104.26.11.233): icmp_seq=1 ttl=55 time=21.2 ms
      64 bytes from 104.26.11.233 (104.26.11.233): icmp_seq=2 ttl=55 time=12.8 ms
      64 bytes from 104.26.11.233 (104.26.11.233): icmp_seq=3 ttl=55 time=11.9 ms
      ^C
      --- www.ynov.com ping statistics ---
       3 packets transmitted, 3 received, 0% packet loss, time 2001ms
      rtt min/avg/max/mdev = 11.852/15.279/21.213/4.212 ms

      

   ### ☀️ Sur dhcp.lan1.tp2

      setup du serveur DHCP

      commande d'installation du paquet:

      [root@node2 raph]# dnf -y install dhcp-server
      
      fichier de conf:

      [root@node2 raph]# cat /etc/dhcp/dhcpd.conf


       DHCP Server Configuration file.
       see /usr/share/doc/dhcp-server/dhcpd.conf.example
       see dhcpd.conf(5) man page


       option domain-name    "srv.world";


       option domain-name-servers   dlp.srv.world;


       default-lease-time 600;

       max-lease-time 700;

       authoritative;

      subnet 10.1.1.0 netmask 255.255.255.0 {

        range dynamic-bootp 10.0.0.100 10.0.0.200;

        option broadcast-address 10.1.1.255;

        option routers 10.1.1.254;

        option domain-name-servers 1.1.1.1;
      }
      service actif:

      
