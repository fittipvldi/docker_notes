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

### Segundo Dockerfile - COPY | WORKDIR | ENV

No próximo exemplo, temos as seguintes definições:

![](../Pasted%20image%2020260220022406.png)

`COPY` cópia do arquivo local para o container
`WOKDIR` diretório de início
`ENV` criação de variáveis de ambiente

---

### Terceiro Dockerfile - LABEL | ENTRYPOINT

![](../Pasted%20image%2020260220234000.png)

`LABEL` etiqueta para identificação
`ENTRYPOINT` comando principal para execução do container. Depois que o entrypoint é definido, o `CMD` serve apenas como parâmetros para o `ENTRYPOINT`

---

### Quarto Dockerfile - ADD | HEALTHCHECK

![](../Pasted%20image%2020260221015435.png)

`ADD` No exemplo foi utilizado como download de pacote para um diretório em específico.

Agora, no exemplo abaixo, ele está trazendo um pacote comprimido do host e descompactando dentro do container:

![](../Pasted%20image%2020260221020447.png)

`HEALTHCHECK` retorna o status do container, combinado com o que você definiu como healthcheck. No exemplo, definimos que o curl para o localhost deve retornar em até dois segundos, senão ele encerra o container.

É possível identificar o status como "healthy"

![](../Pasted%20image%2020260221015236.png)


![](../Pasted%20image%2020260221133814.png)


No dia 31/01/2026 iniciei minha participação no **#PICK2026** (Programa Intensivo de Containers e Kubernetes), que é uma mentoria da [LINUXtips](https://www.linkedin.com/in/fittipaldi-henrique/#), com foco no aprendizado em **#Docker**, **#Kubernetes**, **#ArgoCD**, entre outras atividades como a preparação pra certificação **#CKA** da [The Linux Foundation](https://www.linkedin.com/in/fittipaldi-henrique/#).

  

Nas primeiras semanas já me impressionei com a quantidade de conteúdo disponibilizado, nem encerramos o mês e já estamos aprendendo sobre Kubernetes 🫨! Também, o que deixa tudo mais interessante são as interassões e dinâmicas em turma, que tornam o aprendizado constante e sempre com aquela cobrança interna de estar atualizado no conteúdo pra conseguir contribuir nos desafios e tentar ajudar os demais colegas.

  

Hoje tivemos uma interação em grupo junto com o pessoal da mentoria **#DescomplicandoKubernetes** (um salve especial pro meu colega [Lucas Gonella](https://www.linkedin.com/in/fittipaldi-henrique/#) que está nessa turma) e tivemos um questionário e uma dinâmica em grupo sobre Docker e Kubernetes, que olha kkkkk foi desafiador, mas que deu pra sair com o sentimento de "quero ser o cara nisso".

  

Nos próximos mêses espero postar alguns conteúdos pra vocês sobre essa mentoria que está sendo fera demais!

  

Gostaria de agradecer demais o [Jeferson Fernando](https://www.linkedin.com/in/fittipaldi-henrique/#) por juntar tantas pessoas em prol de um mesmo objetivo. Você faz e fez muito para a Comunidade e sempre será refência nisso. Obrigado por dar acessibilidade e realmente descomplicar assuntos técnicos.