# Invadindo celular Android usando Msfconsole Msfvenom e Ngrok

Criação Backdoor com o msfvenom de uma simples shell reversa com **Metasploit Framework** e Meterpreter, onde iremos criar um .apk infectado que quando executado na máquina da vítima, cria uma conexão reversa com nossa máquina nos dando permissões de administrador ao seu celular
Irei utilizar o ngrok para fazer um túnel de conexão sem eu ter que abrir portas do roteador para me conectar fora da rede externa.

## ngrok 

```bat 
ngrok tcp 22
```

Utilizar o nosso *FORWARDING TCP* como o *LHOST* e o *12643* como *LPORT*
Lembrando que cada um tem o seu *FORWARDING*



Fontes:

https://medium.com/devshift/invadindo-celular-android-usando-msfvenom-e-ngrok-f646e1e03798

