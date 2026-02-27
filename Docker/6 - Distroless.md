### O que é?

O nome vem de algo "sem distribuição", sem imagem base. É a criação de uma imagem de container com apenas uma camada.

O conceito foi criado por conta de vulnerabilidades. Muitos recursos que não utilizamos em nossa aplicação podem estar instalados em nossa imagem base, o distroless veio para mitigar isso.

Se compararmos algumas imagens de containers que já criamos, é possível identificar diversas camadas criadas, inclusive a da nossa imagem base:

```
$ admin@jupiter:~/giropops-senhas$ docker history giropops-senha:2.0
IMAGE          CREATED         CREATED BY                                      SIZE      COMMENT
5de8bd530ac8   8 minutes ago   CMD ["flask" "run" "--host=0.0.0.0"]            0B        buildkit.dockerfile.v0
<missing>      8 minutes ago   EXPOSE [5000/tcp]                               0B        buildkit.dockerfile.v0
<missing>      8 minutes ago   RUN /bin/sh -c pip install --no-cache-dir -r…   21.6MB    buildkit.dockerfile.v0
<missing>      8 minutes ago   COPY static static/ # buildkit                  131kB     buildkit.dockerfile.v0
<missing>      8 minutes ago   COPY templates templates/ # buildkit            24.6kB    buildkit.dockerfile.v0
<missing>      8 minutes ago   COPY app.py . # buildkit                        12.3kB    buildkit.dockerfile.v0
<missing>      8 minutes ago   COPY requirements.txt . # buildkit              12.3kB    buildkit.dockerfile.v0
<missing>      8 minutes ago   WORKDIR /app                                    8.19kB    buildkit.dockerfile.v0
<missing>      32 hours ago    CMD ["python3"]                                 0B        buildkit.dockerfile.v0
<missing>      32 hours ago    RUN /bin/sh -c set -eux;  for src in idle3 p…   16.4kB    buildkit.dockerfile.v0
<missing>      32 hours ago    RUN /bin/sh -c set -eux;   savedAptMark="$(a…   48.4MB    buildkit.dockerfile.v0
<missing>      33 hours ago    ENV PYTHON_SHA256=8d3ed8ec5c88c1c95f5e558612…   0B        buildkit.dockerfile.v0
<missing>      33 hours ago    ENV PYTHON_VERSION=3.11.14                      0B        buildkit.dockerfile.v0
<missing>      33 hours ago    ENV GPG_KEY=A035C8C19219BA821ECEA86B64E628F8…   0B        buildkit.dockerfile.v0
<missing>      33 hours ago    RUN /bin/sh -c set -eux;  apt-get update;  a…   4.94MB    buildkit.dockerfile.v0
<missing>      33 hours ago    ENV LANG=C.UTF-8                                0B        buildkit.dockerfile.v0
<missing>      33 hours ago    ENV PATH=/usr/local/bin:/usr/local/sbin:/usr…   0B        buildkit.dockerfile.v0
<missing>      3 days ago      # debian.sh --arch 'amd64' out/ 'trixie' '@1…   87.4MB    debuerreotype 0.17
```

### Criação de uma imagem distroless

No endereço https://www.chainguard.dev/, existem diversas imagens distroless para download.

Após consultar o catálogo, iremos apontar para uma imagem ditroless em nosso dockerfile e criar a imagem do container:

```
$ admin@jupiter:~/giropops-senhas$ cat Dockerfile
FROM cgr.dev/chainguard/python:latest-dev

WORKDIR /app
COPY requirements.txt .
RUN pip install --user --no-cache-dir -r requirements.txt
COPY app.py .
COPY templates templates/
COPY static static/

ENTRYPOINT ["flask", "run", "--host=0.0.0.0"]
```

Ao executarmos o history, visualizamos apenas nossas camadas, sendo a da distroless apenas uma:

```
$ admin@jupiter:~/giropops-senhas$ docker history giropops-senha:3.0
IMAGE          CREATED          CREATED BY                                      SIZE      COMMENT
bd216fad2488   16 seconds ago   ENTRYPOINT ["flask" "run" "--host=0.0.0.0"]     0B        buildkit.dockerfile.v0
<missing>      16 seconds ago   COPY static static/ # buildkit                  131kB     buildkit.dockerfile.v0
<missing>      16 seconds ago   COPY templates templates/ # buildkit            24.6kB    buildkit.dockerfile.v0
<missing>      16 seconds ago   COPY app.py . # buildkit                        12.3kB    buildkit.dockerfile.v0
<missing>      16 seconds ago   RUN /bin/sh -c pip install --user --no-cache…   9.38MB    buildkit.dockerfile.v0
<missing>      19 seconds ago   COPY requirements.txt . # buildkit              12.3kB    buildkit.dockerfile.v0
<missing>      19 seconds ago   WORKDIR /app                                    8.19kB    buildkit.dockerfile.v0
<missing>      8 hours ago      apko                                            3.33MB    python by Chainguard

```




