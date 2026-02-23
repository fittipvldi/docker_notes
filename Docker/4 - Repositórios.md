O principal repositório do Docker é o DockerHub, localizado no seguinte endereço:https://hub.docker.com/. Por padrão é lá onde realizamos o download das imagens e caso criarmos uma conta, é possível definirmos o nosso repositório e realizarmos o upload da nossa própria imagem.

Após a criação da conta no Dockerhub, é possível configurarmos nossa conta localmente, conforme abaixo:

```
% admin@jupiter:~/Dockerfiles/go_teste3$ docker login -u fittipvldi

i Info → A Personal Access Token (PAT) can be used instead.
         To create a PAT, visit https://app.docker.com/settings


Password:

WARNING! Your credentials are stored unencrypted in '/home/admin/.docker/config.json'.
Configure a credential helper to remove this warning. See
https://docs.docker.com/go/credential-store/

Login Succeeded
```


