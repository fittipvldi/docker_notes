### DockerHub

O principal repositório do Docker é o DockerHub, localizado no seguinte endereço:https://hub.docker.com/. Por padrão é lá onde realizamos o download das imagens e caso criarmos uma conta, é possível definirmos o nosso repositório e realizarmos o upload da nossa própria imagem.

Após a criação da conta no Dockerhub, é possível configurarmos nossa conta localmente, conforme abaixo:

```
$ admin@jupiter:~/Dockerfiles/go_teste3$ docker login -u fittipvldi

i Info → A Personal Access Token (PAT) can be used instead.
         To create a PAT, visit https://app.docker.com/settings


Password:

WARNING! Your credentials are stored unencrypted in '/home/admin/.docker/config.json'.
Configure a credential helper to remove this warning. See
https://docs.docker.com/go/credential-store/

Login Succeeded
```

---

### Upload de Imagens

Para que possamos enviar imagens ao nosso registry, ao criarmos a imagem é necessário conciliarmos um padrão, como no exemplo:

```
$ admin@jupiter:~/Dockerfiles$ docker build -t fittipvldi/teste:1.0 .
```

Caso queiramos redefinir o nome de uma imagem que já criamos podemos utilizar:


```
$ admin@jupiter:~/Dockerfiles$ docker tag fittipvldi/teste:1.0 fitipvldi/teste:2.0
```

O upload de imagens para nosso registry pode ser realizado:

```
$ admin@jupiter:~/Dockerfiles/go_teste3$ docker push fittipvldi/go-teste:1.0
The push refers to repository [docker.io/fittipvldi/go-teste]
4f4fb700ef54: Pushed
0cdfa0c98ed7: Pushed
9fcf25224a38: Pushed
86559b2f7081: Pushed
1.0: digest: sha256:6594e94cfdea9c7d279d7318c3ad4201c543777be9a489779d0847f27f32aa8e size: 855
```