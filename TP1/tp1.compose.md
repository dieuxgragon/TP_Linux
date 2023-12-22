## Docker compose

### Créez un fichier docker-compose.yml

```
[enzo@localhost] cd /home/enzo 
[enzo@localhost] mkdir compose_test
[enzo@localhost] cd compose_test
[enzo@localhost compose_test] touch docker-compose.yml

[enzo@localhost compose_test]$ docker compose up -d
[+] Running 3/3
 ✔ conteneur_flopesque 1 layers [⣿]      0B/0B      Pulled                                                                                             2.8s
   ✔ bc0734b949dc Already exists                                                                                                                       0.0s
 ✔ conteneur_nul Pulled                                                                                                                                3.0s
[+] Running 3/3
 ✔ Network compose_test_default                  Created                                                                                               1.8s
 ✔ Container compose_test-conteneur_flopesque-1  Started                                                                                               0.2s
 ✔ Container compose_test-conteneur_nul-1        Started


[baptiste@localhost compose_test]$ docker compose ps
NAME                                 IMAGE     COMMAND        SERVICE               CREATED          STATUS          PORTS
compose_test-conteneur_flopesque-1   debian    "sleep 9999"   conteneur_flopesque   14 seconds ago   Up 12 seconds
compose_test-conteneur_nul-1         debian    "sleep 9999"   conteneur_nul         14 seconds ago   Up 12 seconds
```

## ouvrir un bash 

```bash
[baptiste@localhost compose_test]$ docker exec -it compose_test-conteneur_nul-1 bash
root@162c854f0b9e:/#

root@162c854f0b9e:/# apt install iputils-ping

PING conteneur_flopesque (172.18.0.2) 56(84) bytes of data.
64 bytes from compose_test-conteneur_flopesque-1.compose_test_default (172.18.0.2): icmp_seq=1 ttl=64 time=0.232 ms
64 bytes from compose_test-conteneur_flopesque-1.compose_test_default (172.18.0.2): icmp_seq=2 ttl=64 time=0.148 ms
```