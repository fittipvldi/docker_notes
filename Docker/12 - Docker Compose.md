
### O que é?

Basicamente o Docker Compose é o processo de subir containers com o arquivo yaml, definindo suas propriedades, conforme documentação: https://docs.docker.com/compose/

Verificando a instalação:

```
$ admin@jupiter:~$ docker compose version
Docker Compose version v5.0.2
```

### Primeiro Yaml

Nosso primeiro arquivo de configuração do docker compose, será um webservice rodando na porta 8080 do nosso host:

```
$ admin@jupiter:~/compose$ cat docker-compose.yaml
version: '3'
services:
  nginx:
    image: nginx
    ports:
      - "8080:80"

```

Então, podemos subir nossa configuração:

```
$ admin@jupiter:~/compose$ docker compose up
[+] up 2/2
 ✔ Network compose_default   Created                                                                0.0s
 ✔ Container compose-nginx-1 Created                                                                0.2s
Attaching to nginx-1
nginx-1  | /docker-entrypoint.sh: /docker-entrypoint.d/ is not empty, will attempt to perform configuration
nginx-1  | /docker-entrypoint.sh: Looking for shell scripts in /docker-entrypoint.d/
nginx-1  | /docker-entrypoint.sh: Launching /docker-entrypoint.d/10-listen-on-ipv6-by-default.sh
nginx-1  | 10-listen-on-ipv6-by-default.sh: info: Getting the checksum of /etc/nginx/conf.d/default.conf
nginx-1  | 10-listen-on-ipv6-by-default.sh: info: Enabled listen on IPv6 in /etc/nginx/conf.d/default.conf
nginx-1  | /docker-entrypoint.sh: Sourcing /docker-entrypoint.d/15-local-resolvers.envsh
nginx-1  | /docker-entrypoint.sh: Launching /docker-entrypoint.d/20-envsubst-on-templates.sh
nginx-1  | /docker-entrypoint.sh: Launching /docker-entrypoint.d/30-tune-worker-processes.sh
nginx-1  | /docker-entrypoint.sh: Configuration complete; ready for start up
nginx-1  | 2026/04/28 00:21:12 [notice] 1#1: using the "epoll" event method
nginx-1  | 2026/04/28 00:21:12 [notice] 1#1: nginx/1.29.5
nginx-1  | 2026/04/28 00:21:12 [notice] 1#1: built by gcc 14.2.0 (Debian 14.2.0-19)
nginx-1  | 2026/04/28 00:21:12 [notice] 1#1: OS: Linux 6.12.73+deb13-cloud-amd64
nginx-1  | 2026/04/28 00:21:12 [notice] 1#1: getrlimit(RLIMIT_NOFILE): 524288:524288
nginx-1  | 2026/04/28 00:21:12 [notice] 1#1: start worker processes
nginx-1  | 2026/04/28 00:21:12 [notice] 1#1: start worker process 29
nginx-1  | 2026/04/28 00:21:12 [notice] 1#1: start worker process 30
```

Então, se acessarmos a porta do 8080 do host, temos acesso a página do nginx:

![](../images/12%20-%20Docker%20Compose/nginx.png)

### Comandos Básicos

Finalizar o docker compose com o `docker compose down`

```
$ admin@jupiter:~/compose$ docker compose down
[+] down 2/2
 ✔ Container compose-nginx-1 Removed                                                                0.3s
 ✔ Network compose_default   Removed                                                                0.1s
```

Visualizar quais composes estão rodando localmente com o `docker compose ls`:

```
$ admin@jupiter:~/compose$ docker compose ls
NAME                STATUS              CONFIG FILES
compose             running(1)          /home/admin/compose/docker-compose.yaml
```

Executar o monitor de processados com o `docker compose top`:

```
$ admin@jupiter:~/compose$ docker compose top
SERVICE  #   UID    PID   PPID  C   STIME  TTY  TIME      CMD
nginx    1   root   9924  9899  0   00:23  ?    00:00:00  nginx: master process nginx -g daemon off;
nginx    1   uuidd  9994  9924  0   00:23  ?    00:00:00  nginx: worker process
nginx    1   uuidd  9995  9924  0   00:23  ?    00:00:00  nginx: worker process
```

Pausar e despausar o docker compose:

```
$ admin@jupiter:~/compose$ docker compose pause
[+] pause 1/1
 ✔ Container compose-nginx-1 Paused                                                                 0.0s
$ admin@jupiter:~/compose$ docker compose unpause
[+] unpause 1/1
 ✔ Container compose-nginx-1 Unpaused 
```

### Segundo Exemplo de Yaml

No exemplo abaixo, subimos a aplicação giropops-senhas, utilizada previamente em outros exemplos:

```
$ admin@jupiter:~/compose$ cat docker-compose.yaml
version: '3'
services:
  giropops-senhas:
    image: linuxtips/giropops-senhas:1.0
    ports:
      - "5000:5000"
    networks:
      - giropops
    environment:
      REDIS_HOST: redis
  redis:
    image: redis
    ports:
      - "6379:6379"
    networks:
      - giropops

networks:
  giropops:
    driver: bridge
```

Segue a aplicação rodando:

![](../images/12%20-%20Docker%20Compose/giropops-senhas.png)

### Terceiro Exemplo de Yaml

Nesse terceiro exemplo, podemos adicionar um pouco mais de complexidade ao nosso compose. 

```
$ admin@jupiter:~/compose$ cat docker-compose.yaml
version: '3'
services:
  giropops-senhas:
    image: linuxtips/giropops-senhas:1.0
    ports:
      - "5000:5000"
    networks:
      - giropops
    environment:
      REDIS_HOST: redis
    volumes:
      - strigus:/strigus
    depends_on:
      - redis
    deploy:
      resources:
        reservations:
          cpus: '0.25'
          memory: 128M
        limits:
          cpus: '0.5'
          memory: 256M
  redis:
    image: redis
    networks:
      - giropops


networks:
  giropops:
    driver: bridge
volumes:
  strigus:
```