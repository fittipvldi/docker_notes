
### Conhecendo a Webapp

O seguinte exemplo é realizado com o webapp da LinuxTips, feito em Flask. O clone pode ser realizado no seguinte repositório:

```
$ admin@jupiter:~$ git clone https://github.com/badtuxx/giropops-senhas.git
```

A aplicação roda em flask e é utilizado o gerenciador de pacotes pip para instalações de dependências:

```
$ admin@jupiter:~$ sudo apt install pip
```

As dependências serão feitas em um ambiente virtual (venv). Após instalarmos o venv, é possível cria-lo no mesmo diretório do projeto

```
$ admin@jupiter:~/giropops-senhas$ sudo apt update && sudo apt install python3-venv python3-full

$ admin@jupiter:~/giropops-senhas$ python3 -m venv .venv

$ admin@jupiter:~/giropops-senhas$ source .venv/bin/activate
```

Dentro do venv, é possível instalarmos as dependências para o projeto:

```
$ (.venv) admin@jupiter:~/giropops-senhas$ pip install -r requirements.txt
```

É necessário verificarmos se o redis está rodando em nosso host:

```
(.venv) admin@jupiter:~/giropops-senhas$ systemctl status redis
● redis-server.service - Advanced key-value store
     Loaded: loaded (/usr/lib/systemd/system/redis-server.service; enabled; preset: enabled)
     Active: active (running) since Wed 2026-02-25 00:25:29 UTC; 25min ago
 Invocation: bfe3540c23c741448eb526d9928cfa11
       Docs: http://redis.io/documentation,
             man:redis-server(1)
   Main PID: 644 (redis-server)
     Status: "Ready to accept connections"
      Tasks: 6 (limit: 1097)
     Memory: 11.6M (peak: 12.1M)
        CPU: 4.619s
     CGroup: /system.slice/redis-server.service
             └─644 "/usr/bin/redis-server 127.0.0.1:6379"

Feb 25 00:25:29 jupiter systemd[1]: Starting redis-server.service - Advanced key-value store...
Feb 25 00:25:29 jupiter systemd[1]: Started redis-server.service - Advanced key-value store.
```

Dentro do venv, precisamos exportar a seguinte variável de ambiente para que o redis possa se comunicar:

```
(.venv) admin@jupiter:~/giropops-senhas$ export REDIS_HOST=localhost
```

Então, podemos rodar o nosso webapp, utilizando o Flask:

```
$ (.venv) admin@jupiter:~/giropops-senhas$ flask run --host=0.0.0.0
 * Debug mode: off
WARNING: This is a development server. Do not use it in a production deployment. Use a production WSGI server instead.
 * Running on all addresses (0.0.0.0)
 * Running on http://127.0.0.1:5000
 * Running on http://172.31.27.185:5000
Press CTRL+C to quit

```

Segue portal:

![](../Pasted%20image%2020260224225006.png)

---

### Containerzando o Webapp

Após entendermos como a aplicação funciona, com o nosso conhecimento em docker, podemos gerar uma imagem compactada e posteriormente rodar um container.

Em resumo, podemos criar o seguinte Dockerfile, seguindo os mesmos comandos que realizamos para rodar o webapp, isso sem a necessidade do venv, pois o ambiente já está isolado:

```
$ admin@jupiter:~/giropops-senhas$ cat Dockerfile
FROM python:3.11

WORKDIR /app
COPY requirements.txt .
COPY app.py .
COPY templates templates/
COPY static static/

RUN pip install --no-cache-dir -r requirements.txt

EXPOSE 5000

CMD ["flask", "run", "--host=0.0.0.0"]
```

Construção da imagem:

```
admin@jupiter:~/giropops-senhas$ docker image build -t giropops-senhas:1.0 .
```

Como o container é compacto, é interessante rodarmos o redis em outro container:

```
$ admin@jupiter:~/giropops-senhas$ docker container run -d --name redis -p 6379:6379 redis
```

Com o redis up, podemos rodar o nosso webapp, utilizando a variavel de ambiente no momento de sua criação, pois não é interessante chumbarmos o IP no dockerfile. Também estamos passando o IP, pois o redis está em um container e o webapp em outro:

```
$ admin@jupiter:~$ docker container run -d --name giropops-senhas -p 5000:5000 --env REDIS_HOST=184.72.138.103 giropops-senha:1.0
```

![](../Pasted%20image%2020260224232555.png)
