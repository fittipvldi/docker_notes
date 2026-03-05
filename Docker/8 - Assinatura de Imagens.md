### Por quê?

A assinatura de imagens é importante para validarmos que foi certa pessoa ou entidade que realizou a criação daquela imagem. Isso evita o download de imagens não reconhecidas e com malwares aplicados.

A ferramenta de assinatura a ser utilizada será o cosign, através do repositório https://github.com/sigstore/cosign

Após a instalação, para criação de um par de chaves, siga o comando abaixo:

```
$ admin@jupiter:~/Downloads$ cosign generate-key-pair
Enter password for private key:
Enter password for private key again:
Private key written to cosign.key
Public key written to cosign.pub
```

Para a assinatura da imagem, ela já deve estar alocada em um registry, nesse caso pode ser no DockerHub. Então, segue assinatura utilizando a chave privada:

```
$ admin@jupiter:~/Downloads$ cosign sign --key cosign.key fittipvldi/go-teste:1.0
WARNING: Image reference fittipvldi/go-teste:1.0 uses a tag, not a digest, to identify the image to sign.
    This can lead you to sign a different image than the intended one. Please use a
    digest (example.com/ubuntu@sha256:abc123...) rather than tag
    (example.com/ubuntu:latest) for the input to cosign. The ability to refer to
    images by tag will be removed in a future release.

Enter password for private key:
```

É possível identificar a associação da chave no DockerHub:

![](../images/8%20-%20Assinatura%20de%20Imagens/Pasted%20image%2020260301210616.png)

Com a chave pública, é possível validar a imagem:

```
$ admin@jupiter:~/Downloads$ cosign verify --key cosign.pub fittipvldi/go-teste:1.0

Verification for index.docker.io/fittipvldi/go-teste:1.0 --
The following checks were performed on each of these signatures:
  - The cosign claims were validated
  - Existence of the claims in the transparency log was verified offline
  - The signatures were verified against the specified public key

[{"critical":{"identity":{"docker-reference":"index.docker.io/fittipvldi/go-teste:1.0"},"image":{"docker-manifest-digest":"sha256:6594e94cfdea9c7d279d7318c3ad4201c543777be9a489779d0847f27f32aa8e"},"type":"https://sigstore.dev/cosign/sign/v1"},"optional":{}}]
```

