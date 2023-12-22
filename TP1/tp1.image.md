## Récupérez des images

```
[enzo@localhost ~]$ docker pull python:3.11
[enzo@localhost ~]$ docker pull mysql
[enzo@localhost ~]$ docker pull wordpress
[enzo@localhost ~]$ docker pull linuxserver/wikijs


[enzo@localhost ~]$ docker images
REPOSITORY           TAG       IMAGE ID       CREATED        SIZE
mysql                latest    73246731c4b0   3 days ago     619MB
linuxserver/wikijs   latest    869729f6d3c5   7 days ago     441MB
python               latest    fc7a60e86bae   2 weeks ago    1.02GB
wordpress            latest    fd2f5a0c6fba   2 weeks ago    739MB
nginx                latest    d453dd892d93   8 weeks ago    187MB
hello-world          latest    d2c94e258dcb   7 months ago   13.3kB

```

## Lancez un conteneur à partir de l'image Python

```
[enzo@localhost ]$ touch dockerfile
[enzo@localhost ]$ touch app.py

app.py
-----------------------------------------------------
import emoji

print(emoji.emojize("Cet exemple d'application est vraiment naze :thumbs_down:"))"
-----------------------------------------------------

dockerfile
------------------------------------------------
FROM debian:latest

RUN apt update -y && apt install -y python3 && apt install -y python3-pip && apt install python3-emoji

COPY app.py /app.py

ENTRYPOINT ["python3", "/app.py"]
-----------------------------------------------

[enzo@localhost ]$ docker build -t python_emoji_app .

[enzo@localhost ]$ sudo docker run python_emoji_app
```