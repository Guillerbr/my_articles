Primeiramente precisamos que você tenha conhecimentos em:
**Linux**, **Grafana**, **Zabbix**.

O **Grafana** é um software livre que permite a visualização de formato de dados métricos. Ele permite criar painéis e gráficos a partir de várias fontes, e neste tutorial vamos aprender a integrar com o **Zabbix**.

Usaremos uma máquina **Ubuntu 18.04**.

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



Referências:

https://alexanderzobnin.github.io/grafana-zabbix/

https://www.digitalocean.com/community/tutorials/how-to-install-and-secure-grafana-on-ubuntu-18-04-pt

https://medium.com/zabbix-brasil/integrando-zabbix-e-grafana-d46de4d1526d

