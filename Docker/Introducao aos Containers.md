
### O que é um container? 

Basicamente um Container é um isolamento de recursos para um determinado fim.

______________________________________________________________

### chroot

Responsável por isolamento de Files System (FHS)

___

### namespaces

Módulo do Kernel Linux, também responsável pelo isolamento de recursos de um Container, mais propriamente de processos, filesystems, network, usuários etc.

`apt-get install debootstrap -y`   instalação do `debootstrap`, responsável por criar um sistema de arquivos (FHS).

`debootstrap stable /debian http://deb.debian.org/debian`  instalação do sistema de arquivos debian, dentro do diretório `/debian` .

`unshare —help`  manual de criação. O `unshare` é responsável por criar namespaces.

`unshare —mount —uts —ipc —net —map-root-user —user —pid —fork chroot /debian bash` criação de namespace, no diretório `/debian` . Após a criação da namespace, podem ser montados diretórios, como `mount -t proc none /proc`  e podemos visualizar os processos com `ps -ef` . Podemos sair da namespace com `exit` .

`lsns`  listagem de namespaces.

---

### cgroup

Módulo do Kernel Linux responsável pelo isolamento de recursos de um Container, mais propriamente recursos operacionais como CPU, Memória Ram etc. É possível trabalhar cgroups com os comandos abaixo:

`stat -fc %T /sys/fs/cgroup/` checar versão do cgroup. 
`apt-get install cgroup-tools -y` instalação de ferramentas do cgroup. 

`cgcreate —help` manual de criação.

`cgcreate -g cpu,memory:teste` criação de um cgroup de nome `teste`. É possível identificar o cgroup de cpu através do comando `ls /sys/fs/cgroup/teste`

---

### Conceito Copy-on-Write

Temos que ter em mente que é que a imagem do container é read-only. Caso subirmos uma imagem e realizarmos uma alteração, isso não refletirá na imagem, mas somente no estado do container que está rodando.

O conceito é explicado da seguinte forma: "Imaginemos que vou anotar algo em um livro, no momento que vou pressionar a caneta, ele irá gerar uma cópia e nunca irá alterar o original".

No mundo do container, após realizar uma alteração, você estará alterando uma cópia e assim sucessivamente, como se fosse uma pilha de objetos. A primeira é alterável, enquanto as próximas não.

![Introdução ao Docker - Copy-on-Write](copy-on-write.png)

---

### Docker Internals

Abaixo, é possível visualizar todos os recursos que o Docker utiliza para a criação e gerenciamento de um container:

![](docker_internals.png)