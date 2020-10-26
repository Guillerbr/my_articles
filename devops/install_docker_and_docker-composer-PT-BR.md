## Como instalar o Docker e Docker Compose no Ubuntu 18.04.

**Docker** é uma ótima ferramenta para **automatizar** a implantação de aplicativos **Linux** dentro de **contêineres de software**, mas para tirar o máximo proveito de seu potencial, cada componente de um aplicativo deve ser executado em seu próprio contêiner individual. Para aplicativos complexos com muitos componentes, orquestrar todos os contêineres para inicializar, comunicar e encerrar juntos pode rapidamente se tornar difícil.

### Etapa 1 - Instalando o Docker Compose

```bash sudo curl -L https://github.com/docker/compose/releases/download/1.21.2/docker-compose-`uname -s`-`uname -m` -o /usr/local/bin/docker-compose ```

A seguir, definiremos as permissões:

```sudo chmod +x /usr/local/bin/docker-compose```

Em seguida, verificaremos se a instalação foi bem-sucedida verificando a versão:

``` ```
