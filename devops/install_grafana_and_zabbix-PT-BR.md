*Ambiente de testes e experimentação*

Primeiramente precisamos que você tenha conhecimentos em:
**Linux Ubuntu**, **Grafana**, **Zabbix**, **PHP**, **MYSQl**.

O **Grafana** é um *software livre* que permite a criação de *gráficos e visualização de formato de dados métricos*. Ele permite criar *painéis e gráficos* a partir de várias fontes, e neste tutorial vamos aprender a integrar com o **Zabbix**.

O **Zabbix** é um *software livre* de *monitoramento para diversos componentes de TI, incluindo redes, servidores, máquinas virtuais e serviços em nuvem*. O **Zabbix** fornece *métricas de monitoramento*, entre outras, utilização da rede, carga da CPU e consumo de espaço em disco.

Usaremos uma máquina **Ubuntu 18.04**.

# Vamos Começar!

## Instalação do Grafana

Neste primeiro passo, você instalará o Grafana no seu servidor Ubuntu 18.04.

```  
wget -q -O - https://packages.grafana.com/gpg.key | sudo apt-key add -
```

Em seguida, adicione o repositório do Grafana às suas origens de pacotes do APT:

```  
sudo add-apt-repository "deb https://packages.grafana.com/oss/deb stable main"
```

Atualize seu cache do APT para atualizar suas listas de pacotes:

```  
sudo apt update
```

Em seguida, verifique se o Grafana será instalado através do repositório real do Grafana:

```  
apt-cache policy grafana
```

A saída do comando anterior informa a versão do Grafana que você está prestes a instalar e de onde você irá trazer o pacote. Verifique se o candidato à instalação no topo da lista virá do repositório oficial da Grafana em https://packages.grafana.com/oss/deb.

```  
grafana:
  Installed: (none)
  Candidate: 6.3.3
  Version table:
     6.3.3 500
        500 https://packages.grafana.com/oss/deb stable/main amd64 Packages
...
```
### Agora você pode prosseguir com a instalação:

``` 
sudo apt install grafana
``` 

Depois que o Grafana estiver instalado, use systemctl para iniciar o servidor Grafana:

``` 
sudo systemctl start grafana-server
``` 
Em seguida, verifique se o Grafana está em execução, verificando o status do serviço:

```
sudo systemctl status grafana-server
```
Você receberá uma saída semelhante a esta:

```
Output of grafana-server status
● grafana-server.service - Grafana instance
   Loaded: loaded (/usr/lib/systemd/system/grafana-server.service; disabled; vendor preset: enabled)
   Active: active (running) since Tue 2019-08-13 08:22:30 UTC; 11s ago
     Docs: http://docs.grafana.org
 Main PID: 13630 (grafana-server)
    Tasks: 7 (limit: 1152)
...
```

Esta saída contém informações sobre o processo do **Grafana**, incluindo seu status, Identificador do Processo Principal (PID) e muito mais. **active (running)** mostra que o processo está sendo executado corretamente.

Por fim, ative o serviço para iniciar automaticamente o Grafana na inicialização:

```
sudo systemctl enable grafana-server
```

Você receberá a seguinte saída:

```
Output of systemctl enable grafana-server
Synchronizing state of grafana-server.service with SysV service script with /lib/systemd/systemd-sysv-install.
Executing: /lib/systemd/systemd-sysv-install enable grafana-server
Created symlink /etc/systemd/system/multi-user.target.wants/grafana-server.service → /usr/lib/systemd/system/grafana-server.service.
```

**PRONTO!**

Isso confirma que o systemd criou os links simbólicos necessários para iniciar automaticamente o Grafana.

O Grafana agora está instalado e pronto para uso.


## Instalação do Zabbix

*Usarei a versão 5.0 TLS do Zabbix*

Vamos iniciar a instalação. Primeiro, faça o download do pacote que contém o repositório **Zabbix**.
Veja o comando abaixo:

```
sudo wget https://repo.zabbix.com/zabbix/5.0/ubuntu/pool/main/z/zabbix-release/zabbix-release_5.0-1%2Bbionic_all.deb
```

Agora, instale o pacote para adicionar o repositório:

```
sudo dpkg -i zabbix-release_5.0-1+bionic_all.deb
```

Atualize os pacotes:

```
sudo apt-get update
```

Instalação do **banco de dados** **Mysql**

```
sudo apt-get install mysql-server
```

Terminamos de instalar o banco de dados **Mysql**. Agora, vamos instalar o pacote do **Zabbix Server**.
Comando:

```
sudo apt-get install zabbix-server-mysql
```
*Digite Y para as configurações*

Criando o banco de dados do Zabbix, logue na console do mysql primeiro. Por padrão, a senha do mysql do root vem em branco. 

```
sudo mysql -u root -p 
```
*Digite a senha do seu user root do mysql*

Estamos logados na console do mysql.
Vamos criar a Database Zabbix. Digite os comandos abaixo:

```
create database zabbix character set utf8 collate utf8_bin;
```
Agora vamos alterar os privilégios do usuário zabbix e do banco de dados zabbix.
Com o comando:

```
grant all privileges on zabbix.* to zabbix@localhost identified by 'zabbix';
```

Vamos importar as tabelas agora, entre no diretório abaixo, digitando o comando:

```
cd /usr/share/doc/zabbix-server-mysq
```

Dentro desse diretório, digite o seguinte comando:

```
zcat create.sql.gz | mysql -uroot zabbix
```

*A importação pode demorar alguns minutos, aguarde...*

Em seguida, **editaremos** o arquivo do **Zabbix Server**. Por padrão, precisaremos editar somente o **DBPassword**.

Você tem que descomentar o parâmetro **DBPassword** removendo o “#” da frente e adicionar a senha **“zabbix”**, porque foi a que criamos, na parte de banco de dados.

Entre no arquivo desse diretório:

```
nano /etc/zabbix/zabbix_server.conf
```

Agora, instalaremos o *PHP*, necessário para o funcionamento correto da parte **WEB do Zabbix**.

```
sudo apt-get install php7.2 php7.2-mysql php7.2-bcmath php7.2-gd php7.2-mbstring php7.2-xml php7.2-gettext php7.2-ldap
```
*Digite S ou Y para configurar corretamente.*

Agora precisamos editar o arquivo **php.ini**.Alterar alguns parâmetros, deixando-os conforme os valores abaixo:

No caminho:

```
nano /etc/php/7.2/apache2/php.ini
```

Altere conforme abaixo:

```
memory_limit = 128MB
post_max_size = 16M
upload_max_filesize = 2M
max_execution_time = 300
max_input_time = 300
date.timezone = America/Sao_Paulo
```

Está quase no final. Vamos instalar o pacote do **Frontend do Zabbix:**

Comando:

```
sudo apt install zabbix-frontend-php zabbix-apache-conf zabbix-agent2
```
*Digite S ou Y para configurar*

Reiniciar Apache Server:

```
sudo service apache2 restart
```

**Ativar Zabbix Server no boot:**

```
sudo systemctl enable zabbix-server
```

**Iniciando Zabbix Server**

```
sudo service zabbix-server start
```

Confira o log para saber se está tudo certo até aqui. Segue comando:

```
sudo tail -f /var/log/zabbix/zabbix_server.log
```

Abra o navegador de sua preferência e acesse **Wizard Frontend** para finalizar a instalação.

*localhost/zabbix*

Se tudo estiver certo irá aparecer a página do cliente *Zabbix*

Clique em *Next step*.

Verifique se todos os utilitários foram instalados com sucesso.

![Alt Text](https://dev-to-uploads.s3.amazonaws.com/i/qwngubsyjff113t2upkd.png)

Clique em *Next step*.

**Configure DB connection**

*Digite a senha que usamos para nosso banco de dados **zabbix***.

*A senha é: **zabbix***

![Alt Text](https://dev-to-uploads.s3.amazonaws.com/i/qc3v55koko0c2i8i4z73.png)


Digite um nome qualquer para seu projeto *Zabix*

Agora vamos para a instalação final:

![Alt Text](https://dev-to-uploads.s3.amazonaws.com/i/7pox9emxmo1wre87k6qv.png)

Clique em *Next step*.

**Instalado com Sucesso!**

![Alt Text](https://dev-to-uploads.s3.amazonaws.com/i/yo9g978ebc0zpul3kep7.png)

**Vamos logar com o usuário e senha padrão do Zabbix**

user: Admin
pass: zabbix

## PRONTO!

Se tudo estiver instalado corretamente, você chegará nessa tela após o login.

![Alt Text](https://dev-to-uploads.s3.amazonaws.com/i/ovl48smmow9z1tffvgie.png)



# Integração

## Instalando o plugin do *Zabbix* no *Grafana*

O plugin pode ser instalado através de um utilitário de linha de comando do *Grafana* chamado **grafana-cli**, usando os comandos abaixo:

```
grafana-cli plugins install alexanderzobnin-zabbix-app
systemctl restart grafana-server
```
**Em versões mais recentes Grafana 7+ e Zabbix plugin 4+ é necessário incluir o parâmetro abaixo no arquivo de configuração grafana.ini**. 
Abaixo da sessão [plugins], atenção para o nome que deve terminar com **datasource**.

```
[plugins]
allow_loading_unsigned_plugins = alexanderzobnin-zabbix-datasource
```

Posteriormente reiniciando o serviço do Grafana, após a instalação é necessário habilitar o plugin na interface do Grafana, como na imagem abaixo.

Dentro do painel do Grafana.Em **plugins**:

![Alt Text](https://dev-to-uploads.s3.amazonaws.com/i/a578psfj4f3dnhse0e1l.png)

Digite *zabbix* na procura de *plugins*.

![Alt Text](https://dev-to-uploads.s3.amazonaws.com/i/8vorary49pmlxsdth7l5.png)

### Selecione, Habilite, Instale e Configure.

**Configurando o Datasource**

Ao finalizar o processo de instalação do **plugin**, estará disponível a opção de criar datasource do tipo Zabbix. 
No Grafana os datasources são separados essa flexibilidade permite criar orgs separadas por clientes com datasources independentes.

No painel do Grafana em *Data Sources*

![Alt Text](https://dev-to-uploads.s3.amazonaws.com/i/osgazwcqfz287yrb7n7q.png)

*Selecione o Zabbix*

### Configuração

![Alt Text](https://dev-to-uploads.s3.amazonaws.com/i/wiixvlx95shi4cpdesyc.png)

![Alt Text](https://dev-to-uploads.s3.amazonaws.com/i/kflkf9ebt9j98bylukop.png)

Nessa página de configuração, devemos informar os dados do usuário do *zabbix* criado nas etapas anteriores.
O usuário é *Admin* e a senha é *zabbix*.

**Name**: Defina um nome para esse datasource.

**URL**: A url que responde pela API do Zabbix.

**Access**: O tipo de acesso que será realizado, Server indica que as requisições serão realizadas pelo backend do Grafana, partindo do Grafana Server, browser as requisições são realizadas a partir do navegador do usuário. Vale ressaltar que se escolhida a opção browser, o cliente também necessita ter acesso a interface web do Zabbix, uma vez que as requisições irão partir diretamente do cliente para o servidor Zabbix.

**Trends**: Selecione se quiser que o plugin também utilize dados armazenados na tabela trends.

**After**: O período que o plugin irá considerar para buscar da tabela trends, ex: se configurado para 4d , quando selecionado um intervalo de tempo maior do que 4 dias os dados serão recuperados da tabela trends.

**Range**: O intervalo de tempo no qual o plugin deverá buscar os dados da tabela trends, ex: se configurado para 3d , quando o intervalo selecionado for maior que 3 dias, os dado serão recuperados da tabela trends, mesmo que sejam dados anteriores a 4 dias configurado no passo anterior.

Essas são as principais configurações para ter uma integração funcional, para outras configurações pode ser consultada a documentação do plugin em: https://alexanderzobnin.github.io/grafana-zabbix/configuration/

**Salve e Teste**

**Se tudo der certo você receberá um status de ok, informando a conexão bem sucedida, em verde**

# Criação dos painéis de dashboard Grafana

Agora é preciso criar os painéis de dashboard do **Grafana** e configurar com o **Zabbix Server**.


...EM CONSTRUÇÃO...



## Fontes de Referência:

https://alexanderzobnin.github.io/grafana-zabbix/

https://www.digitalocean.com/community/tutorials/how-to-install-and-secure-grafana-on-ubuntu-18-04-pt

https://medium.com/zabbix-brasil/integrando-zabbix-e-grafana-d46de4d1526d

https://techexpert.tips/pt-br/zabbix-pt-br/zabbix-5-instalacao-no-ubuntu-linux/

https://blog.remontti.com.br/4014

Doc Instalação Zabbix-Ubuntu:

https://noto-site.s3.us-east-2.amazonaws.com/EBOOK/Ebook+2+Zabbix+5.0.+vers%C3%A3o+1.pdf?utm_source=leadlovers&utm_medium=email&utm_campaign=%5BFunil%20Inicial%5D%20&utm_content=NOTO%20-%20Bnus%20Zabbix

## Videos:

https://www.youtube.com/watch?v=pJIHeG0kJNM&feature=emb_title

https://www.youtube.com/watch?v=eUh3jQ3n9Wk