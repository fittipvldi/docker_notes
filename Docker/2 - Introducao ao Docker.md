
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

### Primeiros Comandos - Operação

`docker container ls` listagem dos containers em execução.

`docker container ls -a` listagem dos containers em execução e parados.

docker container run hello-world execução do nosso primeiro container. Ele irá executar parar, informando a seguinte mensagem:

![hello-world](../images/2%20-%20Introdução%20ao%20Docker/hello-world.png)

`docker container run -ti ubuntu` execução da imagem ubuntu, interativamente com o container utilizando um terminal tty terminal.

`docker container attach <id_container>` entrar no container.

`docker container run --name <nome_container> -ti ubuntu` executar um container, com um nome utilizando a imagem do ubuntu.

`docker container create --name <nome_container> -ti ubuntu` criando um container, sem inicializa-lo

`docker container stop <nome_container>` para a execução do container.

`docker container pause <nome_container>` pausar a execução do container.

`docker container start <nome_container>` iniciar o container.

`docker container rm <nome_container>` remover o container.

`docker container rm -f <nome_container>` remover o container com o "force", caso ele esteja em execução.

`docker container prune` remove todos os containers que estão parados.

Também há alguns atalhos. Ao entrar no container você pode sair dele com `Ctrl + d` . Caso o comando principal rodando nele seja o bash, o container será encerrado. Uma outra alternativa é utilizar o `Ctrl + pq`.

---

### Observabilidade

`docker container stats` retorna o consumo do container, dinamicamente.

`docker container stats --no-stream` retorna o consumo do container.

`docker container logs <nome_container>` retorna o status do container.

`docker inspect <nome_container>` retorna todos os dados de construção do container.

`docker history <imagem_container>` retorna todas as layers da imagem.

---

### Imagens

`docker image ls` retorna todas imagens locais que foram utilizadas.

`docker image rm <id_imagem>` remoção de imagem local.

`docker image inspect <nome_id_imagem>` retorna todos os dados da criação da imagem.

`docker pull centos:7` baixa a imagem do centos:7 para seu registry local.

`docker image prune` remove todos os lixos, relacionados a imagens no host local.

---

### Dettached e Exec

`docker container run -d --name webserver nginx` execução de um novo container, como um deamon, com o nome webserver utilizando a imagem do nginx.

Quando iniciamos um container dessa forma não estamos tendo interatividade com ele. Caso queiramos entrar dentro do container, podemos rodar o comando `docker attach webserver`.

Como a imagem do nginx o que está rodando lá dentro não é o bash, não conseguimos realizar um interação com o terminal, utilizando o attach:

![](../images/2%20-%20Introdução%20ao%20Docker/docker_container_ls_2.png)

![](../images/2%20-%20Introdução%20ao%20Docker/docker_container_attach_webserver.png)

Caso queiramos ter uma interatividade com o container utilizando o bash, podemos utilizar o `docker container exec -ti webserver bash` e assim, será possível utilizar o terminal dentro do container:

![](../images/2%20-%20Introdução%20ao%20Docker/docker_container_exec_ti_webserver_bash.png)

---

### Publish

`docker container run -d -p 8080:80 --name webserver nginx` execução de um container, no modo deamon publicando a porta 8080 do meu host da porta 80 do serviço.

Em PORTS qualquer endereço pode chegar na porta 8080 com o protocolo TCP. Dentro do container a porta 8080 está apontada para a porta 80.

![](../images/2%20-%20Introdução%20ao%20Docker/docker_container_ls_3.png)

Em um navegador, é possível acessar o serviço, através da porta 8080:

![](../images/2%20-%20Introdução%20ao%20Docker/nginx_url.png)