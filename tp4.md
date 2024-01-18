# I. Simple bs program

https://github.com/Raphh1/B2_reseau_tp4_python

## 🌞 Commandes...

### je veux dans le compte-rendu toutes les commandes réalisées sur le client et le serveur pour que ça fonctionne :


    [root@localhost raph]# dnf install git

    [root@localhost raph]# git clone https://github.com/Raphh1/B2_reseau_tp4_python.git

    [root@localhost raph]# cd B2_reseau_tp4_python

    [root@localhost B2_reseau_tp4_python]# python bs_client_I1.py
    Le serveur a répondu b'Hi mate !'


### oh et je veux un ss sur le serveur

    [root@localhost B2_reseau_tp4_python]# ss -lapute | grep 13337
    tcp   LISTEN 0      1                   0.0.0.0:13337        0.0.0.0:*      users:(("python",pid=1341,fd=3)) ino:22225 sk:30 cgroup:/user.slice/user-1000.slice/session-6.scope <->

    