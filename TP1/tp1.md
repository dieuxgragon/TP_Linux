## 3. sudo c pa bo

```bash

[enzo@localhost ~]$ sudo usermod -aG docker enzo

restart ssh 

[enzo@localhost ~]$ docker ps
CONTAINER ID   IMAGE     COMMAND   CREATED   STATUS    PORTS     NAMES
```

## 4. Un premier conteneur en vif

```bash

[enzo@localhost ~]$ docker run -d -p 9999:80 nginx

```
## Visitons

```bash
[enzo@localhost ~]$ docker ps
CONTAINER ID   IMAGE     COMMAND                  CREATED          STATUS          PORTS
   NAMES
be9c74574355   nginx     "/docker-entrypoint.…"   27 seconds ago   Up 25 seconds   0.0.0.0:9999->80/tcp, :::9999->80/tcp   jolly_diffie
------------------------------------------------------
[enzo@localhost ~]$ docker logs be
------------------------------------------------------
[enzo@localhost ~]$ docker inspect be
------------------------------------------------------
[enzo@localhost ~]$ sudo ss -lnpt
[sudo] password for enzo:
State    Recv-Q    Send-Q       Local Address:Port       Peer Address:Port   Process
LISTEN   0         4096               0.0.0.0:9999            0.0.0.0:*       users:(("docker-proxy",pid=14056,fd=4))
LISTEN   0         128                0.0.0.0:22              0.0.0.0:*       users:(("sshd",pid=681,fd=3))
LISTEN   0         4096                  [::]:9999               [::]:*       users:(("docker-proxy",pid=14061,fd=4))
LISTEN   0         128                   [::]:22                 [::]:*       users:(("sshd",pid=681,fd=4))
------------------------------------------------------
[enzo@localhost ~]$ sudo firewall-cmd --add-port=9999/tcp --permanent
success
[enzo@localhost ~]$ sudo firewall-cmd --reload
success
----------------------------------------------------
http://10.1.2.10:9999
```

## On va ajouter un site Web au conteneur NGINX

```bash
[enzo@localhost ~]$ cd /home/enzo/
[enzo@localhost ~]$ mkdir ngninx

[enzo@localhost ~]$ cd ngninx/
[enzo@localhost ngninx]$ touch index.html site_nul.conf

le port 9999 ecoute toujours go le fermer
[enzo@localhost ngninx]$ docker stop be

[enzo@localhost ngninx]$ docker run -d -p 9999:8080 -v /home/enzo/nginx/index.html:/var/www/html/index.html -v /
home/enzo/nginx/site_nul.conf:/etc/nginx/conf.d/site_nul.conf nginx

[enzo@localhost nginx]$ docker ps
CONTAINER ID   IMAGE     COMMAND                  CREATED         STATUS         PORTS
             NAMES
bed473b278c8   nginx     "/docker-entrypoint.…"   3 seconds ago   Up 2 seconds   80/tcp, 0.0.0.0:9999->8080/tcp, :::9999->8080/tcp   unruffled_gould

http://10.1.2.10:9999
```
## 5. Un deuxième conteneur en vif

```bash
[enzo@localhost nginx]$ docker run -it python bash

```
## Installe des libs Python
```python
root@3b12347eeb72:/# pip install aiohttp

root@3b12347eeb72:/# pip install aioconsole

python 
>>> import aiohttp  

root@3b12347eeb72:/# ls
bin  boot  dev  etc  home  lib  lib32  lib64  libx32  media  mnt  opt  proc  root  run  sbin  srv  sys  tmp  usr  var
```


