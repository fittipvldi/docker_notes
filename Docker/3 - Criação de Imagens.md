### Primeiro Dockerfile

O dockerfile é um arquivo de instruções para criação de uma imagem de container.

Para melhor organização, na pasta home do meu usuário criei o diretório Dockerfiles. Posteriormente criei o meu primeiro Dockerfile:

```
$ admin@jupiter:~/Dockerfiles/primeiros_dockerfiles$ cat Dockerfile
FROM ubuntu:18.04
RUN apt-get update && apt-get install nginx -y
EXPOSE 80
CMD ["nginx","-g","daemon off;"]
```

Segue definições para criação do nosso primeiro Dockerfile:

`FROM` imagem base para criação do container.
`RUN` no processo de criação, estou atualizando a árvore de repositórios e instalando o webserver nginx.
`EXPOSE` expondo a porta 80.
`CMD` após o comando estar pronto, executa o comando.

`docker image build -t webserver:1.0 .` criação da imagem webserver:1.0, a partir do diretório atual.

---

### COPY | WORKDIR | ENV

No próximo exemplo, temos as seguintes definições:

```
$ admin@jupiter:~/Dockerfiles/primeiros_dockerfiles$ cat Dockerfile
FROM ubuntu:18.04
RUN apt-get update && apt-get install nginx -y && rm -rf /var/lib/apt/lists
EXPOSE 80
COPY index.html /var/www/html/
CMD ["nginx","-g","daemon off;"]
WORKDIR /var/www/html
ENV APP_VERSION 1.0.0
```
`COPY` cópia do arquivo local para o container.
`WOKDIR` diretório de início.
`ENV` criação de variáveis de ambiente.

---

### LABEL | ENTRYPOINT

```
$ admin@jupiter:~/Dockerfiles/primeiros_dockerfiles$ cat terceiro-dockerfile
FROM ubuntu:18.04
LABEL maintainer="henrique.fitipaldi"
RUN apt-get update && apt-get install nginx -y && rm -rf /var/lib/apt/lists
EXPOSE 80
COPY index.html /var/www/html/
WORKDIR /var/www/html
ENV APP_VERSION=1.0.0
ENTRYPOINT ["nginx"]
CMD ["-g","daemon off;"]
```

`LABEL` etiqueta para identificação.
`ENTRYPOINT` comando principal para execução do container. Depois que o entrypoint é definido, o `CMD` serve apenas como parâmetros para o `ENTRYPOINT`.

---

### ADD | HEALTHCHECK

`ADD` está trazendo um pacote comprimido do host e descompactando dentro do container:

```
$ admin@jupiter:~/Dockerfiles/primeiros_dockerfiles$ ls -lha
total 10M
drwxrwxr-x 2 admin admin 4.0K Feb 22 23:20 .
drwxrwxr-x 6 admin admin 4.0K Feb 22 22:13 ..
-rw-rw-r-- 1 admin admin  391 Feb 22 23:20 Dockerfile
-rw-rw-r-- 1 admin admin   22 Feb 20 05:12 index.html
-rw-rw-r-- 1 admin admin 9.9M May 27  2023 node_exporter-1.6.0.linux-amd64.tar.gz
-rw-rw-r-- 1 admin admin  108 Feb 20 05:04 primeiro-dockerfile
-rw-rw-r-- 1 admin admin  391 Feb 21 05:16 quarto-dockerfile
-rw-rw-r-- 1 admin admin  213 Feb 21 02:13 segundo-dockerfile
-rw-rw-r-- 1 admin admin  263 Feb 21 02:42 terceiro-dockerfile
$ admin@jupiter:~/Dockerfiles/primeiros_dockerfiles$ cat Dockerfile
FROM ubuntu:18.04
LABEL maintainer="henrique.fitipaldi"
RUN apt-get update && apt-get install nginx curl -y && rm -rf /var/lib/apt/lists/*
EXPOSE 80
ADD node_exporter-1.6.0.linux-amd64.tar.gz /root/node-exporter
COPY index.html /var/www/html/
WORKDIR /var/www/html
ENV APP_VERSION=1.0.0
ENTRYPOINT ["nginx"]
CMD ["-g","daemon off;"]
HEALTHCHECK --timeout=2s CMD curl -f localhost || exit 1
```

`HEALTHCHECK` retorna o status do container, combinado com o que você definiu como healthcheck. No exemplo, definimos que o curl para o localhost deve retornar em até dois segundos, senão ele encerra o container.

É possível identificar o status como "healthy":

```
$ admin@jupiter:~/Dockerfiles/primeiros_dockerfiles$ docker container ls
CONTAINER ID   IMAGE           COMMAND                  CREATED        STATUS                            PORTS                                     NAMES
b5ef34d11a2d   webserver:4.0   "nginx -g 'daemon of…"   42 hours ago   Up 4 seconds (health: starting)   0.0.0.0:8882->80/tcp, [::]:8882->80/tcp   webserver4
```

---

### Multistage

O MultiStage é um recurso no Dockerfile para que possamos utilizar duas imagens base, com o objetivo do nosso container ser ainda menor.

No exemplo abaixo realizamos uma construção de container para rodar o binário `hello` em go:

```
$ admin@jupiter:~/Dockerfiles/go_teste$ ls -lha
total 16K
drwxrwxr-x 2 admin admin 4.0K Feb 22 22:01 .
drwxrwxr-x 6 admin admin 4.0K Feb 22 22:13 ..
-rw-rw-r-- 1 admin admin  108 Feb 22 21:31 Dockerfile
-rw-rw-r-- 1 admin admin   77 Feb 22 21:32 hello.go
$ admin@jupiter:~/Dockerfiles/go_teste$ cat Dockerfile
FROM golang:1.18
WORKDIR /app
COPY . ./
RUN go mod init hello
RUN go build -o /app/hello
CMD ["/app/hello"]
```

Com o MultiStage, podemos utilizar o `FROM` pela segunda vez. Nesse exemplo utilizamos uma imagem do Alpine, que é referência em imagens compactas:

```
$ admin@jupiter:~/Dockerfiles/go_teste2$ ls -lha
total 16K
drwxrwxr-x 2 admin admin 4.0K Feb 22 21:54 .
drwxrwxr-x 6 admin admin 4.0K Feb 22 22:13 ..
-rw-rw-r-- 1 admin admin  185 Feb 22 21:54 Dockerfile
-rw-rw-r-- 1 admin admin   77 Feb 22 21:51 hello.go
$ admin@jupiter:~/Dockerfiles/go_teste2$ cat Dockerfile
FROM golang:1.18 AS buildando
WORKDIR /app
COPY . ./
RUN go mod init hello
RUN go build -o /app/hello

FROM alpine:3.15.9
COPY --from=buildando /app/hello /app/hello
CMD ["/app/hello"]
```

`FROM golang:1.18 AS buildando` aqui estamos referenciando um apelido pra nossa primeira imagem.
`COPY --from=buildando /app/hello /app/hello` cópia do diretório da nossa primeira imagem para a segunda imagem.

Os container tem o a mesma execução, que é o processo de rodar o binário `hello`. Porém, ao compararmos o tamanho das imagens, é possível identificar uma nítida diferença entre a go-teste:1.0 e a go-teste:2.0:

```
$ admin@jupiter:~/Dockerfiles/go_teste2$ docker image ls
                                                    i Info →   U  In Use
IMAGE                ID             DISK USAGE   CONTENT SIZE   EXTRA
go-teste:1.0         56fdcad2bf7d       1.41GB          355MB    U
go-teste:2.0         377f50ec16c7       11.9MB         3.88MB    U
```

---

### ENV | ARG

`ENV` é para criarmos uma variável de ambiente dentro do container:

```
$ admin@jupiter:~/Dockerfiles/go_teste3$ cat Dockerfile
FROM golang:1.18 AS buildando
WORKDIR /app
COPY . ./
RUN go mod init hello
RUN go build -o /app/hello

FROM alpine:3.15.9
COPY --from=buildando /app/hello /app/hello
ENV APP="hello_world"
CMD ["/app/hello"]
```

Após criarmos a imagem e rodarmos o container, é possível identificar a variável de ambiente com o comando `inspect`

```
$ admin@jupiter:~/Dockerfiles/go_teste3$ docker container inspect epic_visvesvaraya

...
"Mounts": [],
        "Config": {
            "Hostname": "1446b33f25a9",
            "Domainname": "",
            "User": "",
            "AttachStdin": true,
            "AttachStdout": true,
            "AttachStderr": true,
            "Tty": true,
            "OpenStdin": true,
            "StdinOnce": true,
            "Env": [
                "PATH=/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin",
                "app=hello_world"
            ],
...
```

`ARG` vai criar uma variável de ambiente no container, no momento de sua execução:

```
$ admin@jupiter:~/Dockerfiles/go_teste3$ cat Dockerfile
FROM golang:1.18 AS buildando
WORKDIR /app
COPY . ./
RUN go mod init hello
RUN go build -o /app/hello

FROM alpine:3.15.9
COPY --from=buildando /app/hello /app/hello
ENV APP="hello_world"
ARG TESTE="testando"
RUN echo "minha variavel é: $TESTE"
CMD ["/app/hello"]
```

No momento da criação, é possível identificarmos nossa variável:

```
$ admin@jupiter:~/Dockerfiles/go_teste3$ docker build -t go-teste:4.0 .
...
 => CACHED [buildando 2/5] WORKDIR /app                                                                 0.0s
 => [buildando 3/5] COPY . ./                                                                           0.0s
 => [buildando 4/5] RUN go mod init hello                                                               0.3s
 => [buildando 5/5] RUN go build -o /app/hello                                                          1.0s
 => CACHED [stage-1 2/3] COPY --from=buildando /app/hello /app/hello                                    0.0s
 => [stage-1 3/3] RUN echo "minha variavel é: testando"                          
 ...
```

---

### Volumes

É possível adicionar um ponto de montagem a partir do seu Dockerfile, compartilhando a informação dentro do seu container com o seu host:

```
$ admin@jupiter:~/Dockerfiles/go_teste3$ cat Dockerfile
FROM golang:1.18 AS buildando
WORKDIR /app
COPY . ./
RUN go mod init hello
RUN go build -o /app/hello

FROM alpine:3.15.9
COPY --from=buildando /app/hello /app/hello
ENV APP="hello_world"
ARG TESTE="testando"
RUN echo "minha variavel é: $TESTE"
VOLUME /app/dados
CMD ["/app/hello"]
```

Após buildar a imagem, com o comando `inspect` é possível identificar a montagem no container quanto no host:

```
$ admin@jupiter:~/Dockerfiles/go_teste3$ docker container run -ti go-teste:5.0 sh

$ admin@jupiter:~/Dockerfiles/go_teste3$ docker container inspect wonderful_cerf

...

                "PATH=/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin",
                "APP=hello_world"
            ],
            "Cmd": [
                "sh"
            ],
            "Image": "go-teste:5.0",
            "Volumes": {
                "/app/dados": {}
                
...

"Mounts": [
            {
                "Type": "volume",
                "Name": "36c103a74105b239bab9006f8945a8d1c4064d640d1864b327a10a33764f215c",
                "Source": "/home/admin/.local/share/docker/volumes/36c103a74105b239bab9006f8945a8d1c4064d640d1864b327a10a33764f215c/_data",
                "Destination": "/app/dados",
                "Driver": "local",
                "Mode": "",
                "RW": true,
                "Propagation": ""

```
