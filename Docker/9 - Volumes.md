
Esse tema está relacionado a persistência de dados utilizando containers. É possível verificar todas as informações na documentação oficial https://docs.docker.com/engine/storage/. Abaixo segue os tipos de volumes:
### Bind

Os volumes de tipo Bind basicamente são diretórios da sua máquina host que você está referenciando para o seu container utilizar, como se fosse um ponto de montagem.

Abaixo estamos criando um container, referenciando o diretório `/home/admin/volumes` do nosso Host. Dentro do container todos os arquivos que estão nesse diretório, irão para o `/teste` dentro do container. Segue exemplo utilizando o parâmetro --mount:

```
$ admin@jupiter:~$ docker run -ti --name teste-volumes --mount type=bind,source=/home/admin/volumes,target=/teste debian
Unable to find image 'debian:latest' locally
latest: Pulling from library/debian
866771c43bf5: Pull complete
e6a3c865571e: Download complete
Digest: sha256:3615a749858a1cba49b408fb49c37093db813321355a9ab7c1f9f4836341e9db
Status: Downloaded newer image for debian:latest
$ root@84d90477b5bb:/# ls
bin   dev  home  lib64	mnt  proc  run	 srv  teste  usr
boot  etc  lib	 media	opt  root  sbin  sys  tmp    var
```

Com o inspect, é possível identificar o volume mapeado:

```
$ admin@jupiter:~$ docker inspect teste-volumes
[
    {
        "Id": "84d90477b5bbf9de192df699c3d45e0f42bdc88fcf44604907c912ee8a91627d",
        "Created": "2026-03-02T00:26:15.691043958Z",
        "Path": "bash",
        "Args": [],
        "State": {
            "Status": "running",
...
"Mounts": [
            {
                "Type": "bind",
                "Source": "/home/admin",
                "Destination": "/teste",
                "Mode": "",
                "RW": true,
                "Propagation": "rslave"
            }
...
```

Lembrando que, podemos utilizar a possibilidade de restringirmos permissão do container para escrita, utilizando o `readonly`:

```
$ admin@jupiter:~$ docker run -ti --name teste-volumes2 --mount type=bind,source=/home/admin,target=/teste,readonly debian
$ root@b6648ee76c1e:/# touch /teste/criando-arquivo
touch: cannot touch '/teste/criando-arquivo': Read-only file system
```

Outra alternativa de utilizar os volumes é com o parametro `-v`. Teremos o mesmo resultado de uma forma mais fácil:

```
$ admin@jupiter:~$ docker run -ti --name teste-volumes2 -v teste-volume debian
$ root@5b45156907cb:/# ls
bin   dev  home  lib64	mnt  proc  run	 srv  teste-volume  usr
boot  etc  lib	 media	opt  root  sbin  sys  tmp	    var
```
---
### Volume

Os volumes do tipo Volume são gerenciados pelo próprio Docker. Eles seguem a mesma forma do bind, com a diferença de ser criado por padrão na estrutura `/var/lib/docker/volumes/`

A criação pode ser realizada dessa forma:

```
$ admin@jupiter:~$ docker volume create teste-volume
teste-volume
$ admin@jupiter:~$ docker volume inspect teste-volume
[
    {
        "CreatedAt": "2026-03-02T00:50:25Z",
        "Driver": "local",
        "Labels": null,
        "Mountpoint": "/home/admin/.local/share/docker/volumes/teste-volume/_data",
        "Name": "teste-volume",
        "Options": null,
        "Scope": "local"
    }
]
```

No exemplo acima, a criação default está sendo em: `/home/admin/.local/share/docker/volumes/teste-volume/_data`

Criação do container utilizando o tipo volume:

```
$ admin@jupiter:~$ docker run -ti --name teste-volumes1 --mount type=volume,source=teste-volume,target=/teste debian
$ root@4ee7488dd6a6:/# ls
bin   dev  home  lib64	mnt  proc  run	 srv  teste  usr
boot  etc  lib	 media	opt  root  sbin  sys  tmp    var
$ root@4ee7488dd6a6:/# cd teste/
$ root@4ee7488dd6a6:/teste# ls
arquivo-teste
```

Outra forma de realizar a criação do volume é utilizar o parametro `-v`:

```
$ admin@jupiter:~$ docker run -ti --name teste-volumes2 -v teste-volume:/teste debian
root@c206ab7ebbd8:/# ls /teste/
arquivo-teste  outro-arquivo
```

---
### tmpfs

Não são utilizados diretórios mapeados. São registrados na memória:

```
$ admin@jupiter:~$ docker run -ti --name teste-volumes3 --mount type=tmpfs,target=/teste debian
$ root@58ebc313533a:/# ls
bin   dev  home  lib64	mnt  proc  run	 srv  teste  usr
boot  etc  lib	 media	opt  root  sbin  sys  tmp    var
$ root@58ebc313533a:/# mount | grep /test
tmpfs on /teste type tmpfs (rw,nosuid,nodev,noexec,relatime,uid=1000,gid=1000,inode64)
```

---

### Drivers para Volumes

É possível configurar diversos tipos de drivers para os volumes. Todos os volumes disponíveis estão na seguinte documentação https://docs.docker.com/engine/storage/drivers/select-storage-driver/



