## Como instalar o Docker e Docker Compose no Ubuntu 18.04.

**Docker** é uma ótima ferramenta para **automatizar** a implantação de aplicativos **Linux** dentro de **contêineres de software**, mas para tirar o máximo proveito de seu potencial, cada componente de um aplicativo deve ser executado em seu próprio contêiner individual. Para aplicativos complexos com muitos componentes, orquestrar todos os contêineres para inicializar, comunicar e encerrar juntos pode rapidamente se tornar difícil.

## Etapa 1 - Instalando o Docker

O pacote de instalação do Docker disponível no repositório oficial do Ubuntu pode não ser a versão mais recente. Para garantir que teremos a última versão, vamos instalar o Docker a partir do repositório oficial do projeto. Para fazer isto, vamos adicionar uma nova fonte de pacotes, adicionar a chave GPG do Docker para garantir que os downloads são válidos, e então instalar os pacotes.

Primeiro, atualize sua lista atual de pacotes:

```console
sudo apt update

```

Em seguida, instale alguns pacotes de pré-requisitos que permitem que o apt utilize pacotes via HTTPS:

```console
sudo apt install apt-transport-https ca-certificates curl software-properties-common

```

Então adicione a chave GPG para o repositório oficial do Docker em seu sistema:

```console
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -

```

Adicione o repositório do Docker às fontes do APT:

```console
sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu bionic stable"

```

A seguir, atualize o banco de dados de pacotes com os pacotes Docker do repositório recém adicionado:

```console
sudo apt update

```

Certifique-se de que você irá instalar a partir do repositório do Docker em vez do repositório padrão do Ubuntu:

```console
apt-cache policy docker-ce

```

Você verá uma saída como esta, embora o número da versão do Docker possa estar diferente:

```console
docker-ce:
  Installed: (none)
  Candidate: 18.03.1~ce~3-0~ubuntu
  Version table:
     18.03.1~ce~3-0~ubuntu 500
        500 https://download.docker.com/linux/ubuntu bionic/stable amd64 Packages

```

**Ou alguma versão mais recente**

Observe que o docker-ce não está instalado, mas o candidato para instalação é do repositório do Docker para o Ubuntu 18.04 (bionic).

## Finalmente, instale o Docker:

```console
 sudo apt install docker-ce

```

O Docker agora deve ser instalado, o daemon iniciado e o processo ativado para iniciar na inicialização. Verifique se ele está sendo executado:

```console
sudo systemctl status docker

```

A saída deve ser semelhante à seguinte, mostrando que o serviço está ativo e executando:

```console
Output
● docker.service - Docker Application Container Engine
   Loaded: loaded (/lib/systemd/system/docker.service; enabled; vendor preset: enabled)
   Active: active (running) since Thu 2018-07-05 15:08:39 UTC; 2min 55s ago
     Docs: https://docs.docker.com
 Main PID: 10096 (dockerd)
    Tasks: 16
   CGroup: /system.slice/docker.service
           ├─10096 /usr/bin/dockerd -H fd://
           └─10113 docker-containerd --config /var/run/docker/containerd/containerd.toml

```

*A instalação do Docker agora oferece não apenas o serviço Docker (daemon), mas também o utilitário de linha de comando docker ou o cliente Docker. Vamos explorar como usar o comando docker mais adiante neste tutorial.*




## Etapa 2 - Instalando o Docker Compose

```console
 sudo curl -L https://github.com/docker/compose/releases/download/1.21.2/docker-compose-`uname -s`-`uname -m` -o /usr/local/bin/docker-compose

```

A seguir, definiremos as permissões:

```console
sudo chmod +x /usr/local/bin/docker-compose

```

Em seguida, verificaremos se a instalação foi bem-sucedida verificando a versão:

```console
docker-compose --version

```

Isso imprimirá a versão que instalamos:

```console
Output
docker-compose version 1.21.2, build a133471

```

**Ou alguma versão mais recente**

Referências:

https://www.digitalocean.com/community/tutorials/como-instalar-e-usar-o-docker-no-ubuntu-18-04-pt

https://www.digitalocean.com/community/tutorials/how-to-install-docker-compose-on-ubuntu-18-04
