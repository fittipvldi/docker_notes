

### Instalação do Docker

Em um ambiente linux, podemos fazer a instalação o download e instalação do Docker Community com o seguinte comando:

`curl -fsSL https://get.docker.com | bash`

Após a instalação, é recomendável deixarmos configurado a opção de rodar os comandos do docker sem a necessidade de ser root, conforme abaixo:

`dockerd-rootless-setuptool.sh install`

Para algumas aplicações, será necessário utilizar a seguinte variável de ambiente:

`export DOCKER_HOST=unix:///run/user/1000/docker.sock`

Também, é possível configurar o docker como ativo, assim que o sistema for iniciado:

`sudo loginctl enable-linger admin`

https://docs.docker.com/engine/install/

---

### Primeiros Comandos

`docker container ls` listagem dos containers em execução

`docker container ls -a` listagem dos containers em execução e parados

docker container run hello-world execução do nosso primeiro container. Ele irá executar parar, informando a seguinte mensagem:

![hello-world](../images/Introdução%20ao%20Docker/hello-world.png)

`docker container run -it ubuntu` execução da imagem ubuntu, interativamente com o container utilizando um terminal tty terminal

`docker container attach <idcontainer>` entrar no container

`docker container run --name <nome_container> -it ubuntu` executar um container, com um nome.

`docker container stop <nome_container>` para a execução do container.

`docker container pause <nome_container>` pausar a execução do container.

`docker container start <nome_container>` iniciar o container.

`docker container rm <nome_container>` remover o container.

`docker container rm -f <nome_container>` remover o container com o "force", caso ele esteja em execução.

`docker container prune` remove todos os containers que estão parados.

Também há alguns atalhos. Ao entrar no container você pode sair dele com `Ctrl + d` . Caso o comando principal rodando nele seja o bash, o container será encerrado. Uma outra alternativa é utilizar o `Ctrl + pq`

---

### Observabilidade

`docker container stats` retorna o consumo do container, dinamicamente.

`docker container status --no-stream` retorna o consumo do container.

`docker container logs <nomecontainer>` retorna o status do container


