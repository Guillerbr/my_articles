# Conhecimentos prévios **Kubernetes** e **Docker**

### Cluster

O Kubernetes coordena um cluster altamente disponível de computadores conectados para funcionar como uma única unidade. As abstrações no Kubernetes permitem implantar aplicativos em contêineres em um cluster sem amarrá-los especificamente a máquinas individuais. Para fazer uso desse novo modelo de implantação, os aplicativos precisam ser empacotados de uma forma que os desacople dos hosts individuais: eles precisam ser colocados em contêineres. Os aplicativos em contêineres são mais flexíveis e disponíveis do que nos modelos de implantação anteriores, nos quais os aplicativos eram instalados diretamente em máquinas específicas como pacotes profundamente integrados ao host. O Kubernetes automatiza a distribuição e o agendamento de contêineres de aplicativos em um cluster de maneira mais eficiente. O Kubernetes é uma plataforma de código aberto e está pronto para produção.

Um cluster Kubernetes consiste em dois tipos de recursos:

O Master coordena o cluster
Os Nodes são os trabalhadores que executam aplicativos

### Pods

### Node

**Um nó é uma VM ou um computador físico que atua como uma máquina de trabalho em um cluster Kubernetes**. *Cada nó tem um Kubelet, que é um agente para gerenciar o nó e se comunicar com o mestre do Kubernetes*. O nó também deve ter ferramentas para lidar com operações de contêiner, como containerd ou **Docker**. Um cluster Kubernetes que lida com o tráfego de produção deve ter no mínimo três nós.

### Master

O mestre é responsável por gerenciar o cluster. O mestre coordena todas as atividades em seu cluster, como programação de aplicativos, manutenção do estado desejado dos aplicativos, escalonamento de aplicativos e lançamento de novas atualizações.

### Container

### Replicaset

# Instalar Kubernetes Ubuntu 18/20

O que é **Kubernetes**

Kubernetes é um sistema de orquestração de contêineres open-source que automatiza a implantação, o dimensionamento e a gestão de aplicações em contêineres.

O que é **Kubectl**

A ferramenta de linha de comando do Kubernetes _kubectl_, permite que você execute comandos em clusters do Kubernetes. **Você pode usar kubectl para implantar aplicativos, inspecionar e gerenciar recursos de cluster e visualizar logs.**

O que é **Minikube**

Como kind, minikube é uma **ferramenta que permite executar o Kubernetes localmente.** _minikube_ executa um cluster Kubernetes em nó único no seu computador pessoal (incluindo PCs Windows, macOS e Linux) para que você possa experimentar o Kubernetes ou para o trabalho de desenvolvimento diário.

Você pode acompanhar o guia oficial Get Started! guia se o seu foco for instalar a ferramenta.

O que é **Kubeadm**

Você pode usar o _kubeadm_ **ferramenta para criar e gerenciar clusters Kubernetes**. Ele executa as ações necessárias para obter um cluster mínimo viável e seguro instalado e funcionando de maneira amigável.


# Instalação no Ubuntu 18/20

Primeiramente instalaremos o **kubectl**

- Documentação Oficial:

https://kubernetes.io/docs/tasks/tools/install-kubectl/

```bat 
curl -LO "https://dl.k8s.io/release/$(curl -L -s https://dl.k8s.io/release/stable.txt)/bin/linux/amd64/kubectl" 
```

Agora:

```bat 
curl -LO "https://dl.k8s.io/$(curl -L -s https://dl.k8s.io/release/stable.txt)/bin/linux/amd64/kubectl.sha256"
```

Instale o **kubectl**:

```bat 
sudo install -o root -g root -m 0755 kubectl /usr/local/bin/kubectl
```

Instalaremos o **minikube** por se tratar de uma ferramenta para testes iniciais usando Kubernetes, para isso não precisaremos usar um cluster com várias máquinas, apenas uma já atenderá nossa necessidade.
Lembrando que precisaremos já ter o **Docker** instalado.

Por padrão, o Minikube não está disponível no repositório padrão do Ubuntu. Portanto, você precisará baixar o pacote binário do Minikube de seu site oficial. Você pode baixá-lo com o seguinte comando:

```bat 
sudo wget https://storage.googleapis.com/minikube/releases/latest/minikube-linux-amd64
``` 

Assim que o download for concluído, copie o binário baixado para o caminho do sistema usando o seguinte comando:

```bat 
sudo cp minikube-linux-amd64 /usr/local/bin/minikube
```

Em seguida, forneça permissão de execução com o seguinte comando:

```bat 
sudo chmod 755 /usr/local/bin/minikube 
```

Agora você pode verificar a versão do Minikube com o seguinte comando:

```bat 
minikube version
```

Você deve obter a seguinte saída:

```bat 
versão do minikube: v1.16.0 commit: 9f1e482427589ff8451c4723b6ba53bb9742fbb1
```

# Instale Kubectl

Em seguida, você precisará instalar o Kubectl e outras ferramentas para gerenciar aplicativos no Kubernetes. Primeiro, adicione a chave GPG com o seguinte comando:

```bat 
sudo curl -s https://packages.cloud.google.com/apt/doc/apt-key.gpg | apt-key add - 
```

Em seguida, adicione o repositório kubectl com o seguinte comando:

```bat 
sudo echo "deb http://apt.kubernetes.io/ kubernetes-xenial main" | tee /etc/apt/sources.list.d/kubernetes.list
```

Assim que o repositório for adicionado, atualize o cache do repositório e instale o Kubectl executando o seguinte comando:

```bat 
apt-get update -y
```

```bat 
apt-get install kubectl kubeadm kubectl -y 
```

Iniciar Minikube

Neste ponto, todos os pacotes necessários estão instalados. Agora você pode iniciar o Minikube com o seguinte comando:

```bat 
minikube start 
```
ou

```bat 
minikube start --driver=none
```

- Caso tenha erro de privilégio do Docker, adicione seu super usuário no _docker_ execute o seguinte comando:

```bat 
adduser MY_USER
```

```bat 
usermod -aG sudo MY_USER
```

```bat 
su - MY_USER
```

Fontes:

https://kubernetes.io/pt/docs/home/

https://kubernetes.io/docs/tasks/tools/install-kubectl/

https://www.howtoforge.com/how-to-install-kubernetes-with-minikube-ubuntu-20-04/

https://computingforgeeks.com/deploy-kubernetes-cluster-on-ubuntu-with-kubeadm/
