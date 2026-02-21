### Primeiro Dockerfile

O dockerfile é um arquivo de instruções para criação de uma imagem de container.

Para melhor organização, na pasta home do meu usuário criei o diretório Dockerfiles. Posteriormente criei o meu primeiro Dockerfile:

![](../Pasted%20image%2020260220015815.png)

Segue definições para criação do nosso primeiro Dockerfile:

`FROM` imagem base para criação do container
`RUN` no processo de criação, estou atualizando a árvore de repositórios e instalando o webserver nginx
`EXPOSE` expondo a porta 80
`CMD` após o comando estar pronto, executa o comando

`docker image build -t webserver:1.0 .` criação da imagem webserver:1.0, a partir do diretório atual

---

### Segundo Dockerfile

No próximo exemplo, temos as seguintes definições:

![](../Pasted%20image%2020260220022406.png)

