Primeiramente precisamos que você tenha conhecimentos em **React, Node, Java Script, HTML, CSS**.

Você precisa de uma conta no serviço **Firebase**, 

https://firebase.google.com/

Vá para o console do *Firebase*
https://console.firebase.google.com/

![Alt Text](https://dev-to-uploads.s3.amazonaws.com/i/al7ut5behlrybyjsbowz.png)

![Alt Text](https://dev-to-uploads.s3.amazonaws.com/i/t7lz2mm79bon5j78m5fo.png)

Crie um novo projeto com o nome. Pronto, agora que temos o projeto criado podemos utilizar várias ferramentas do **Firebase**, uma delas é a **Hosting**, mas fique livre para utilizar outras,nesse artigo trataremos apenas de hospedagem.

No painel do Firebase clique em **Hosting**

![Alt Text](https://dev-to-uploads.s3.amazonaws.com/i/gmjd2qfth5dbfok6d6ya.png)

Você precisa de um projeto em **React** já pronto, e então faremos a construção (build) desse projeto no hosting da firebase, usaremos também o domínio fornecido por eles, mas claro futuramente podemos alterar.

Você precisará ter o pacote de dependência do **Firebase** para o **Node js**

Instale o pacote do **firebase-tools** globalmente,esse pacote estará instalado no seu computador e não no projeto em si.Esse utilitário do firebase , nos ajudará a executar comandos e conectar aquele projeto que criamos no hosting do firebase.
Execute o comando:

```  
npm install -g firebase-tools

```

Vamos para o console shell, dentro da pasta do projeto *React*

Usarei esse projeto React como exemplo:

https://github.com/guillerbr/ghd-sites

Clone o projeto e entre na pasta:

![Alt Text](https://dev-to-uploads.s3.amazonaws.com/i/urqsuz19egvc6ganer85.png)

Instale a aplicação, pacotes e dependências.

``` 
npm install

```

Dentro da raiz do seu projeto React, digite o comando para a construção (build).

```
npm build

```

Então o **nmp** cria os arquivos estáticos já transpilados e configurados para serem arquivos leves. Após rodar o comando ele criará uma pasta **build** onde estará os arquivos que precisamos.  

![Alt Text](https://dev-to-uploads.s3.amazonaws.com/i/gutrt16chz4mx5yanq70.png)

![Alt Text](https://dev-to-uploads.s3.amazonaws.com/i/rj7fyzrntjqa01o2uglq.png)

Agora precisamos ligar nossa aplicação React ao nosso serviços de Hosting do Firebase.Para isso usaremos o **firebase-tools** que instalamos no começo.
Digite o comando:

```
firebase login

```
Você precisar estar autenticado na conta do Google Firebase com seu navegador, após o comando acima o Google pode pedir alguma verificação para ligar sua aplicação no console Shell, a sua conta no Firebase no navegador. Se o Google abrir o Browser e pedir autenticação da conta. Aceite e conclua a operação.

![Alt Text](https://dev-to-uploads.s3.amazonaws.com/i/b42x44uteveg1obp0ddq.png)

Pronto! O console informa que estou autenticado e informa meu ,
e-mail.

Dentro da raiz do projeto, vamos digitar os comandos para configurações finais.
Digite o comando:

```
firebase init

```

Aceite a confirmação, e terá essas opções no console:

![Alt Text](https://dev-to-uploads.s3.amazonaws.com/i/nn6xf9pp8sn1epn90uie.png)

Escolha a opção:

``` 
Hosting: Configure and deploy Firebase Hosting sites 

```

Agora teremos a nova etapa de configuração:

![Alt Text](https://dev-to-uploads.s3.amazonaws.com/i/7h25svr9g8nsy1pvwu7i.png)

Escolha a opção:

``` 
Use an existing project  

```
Irá aparcer um lista de projetos e seus nomes.Agora precisamos escolher o nome do projeto que criamos no firebase.O meu é **ghdsites2**

![Alt Text](https://dev-to-uploads.s3.amazonaws.com/i/s8c3hvbvwh45nh05yish.png)

Agora cairemos na parte de configuração do diretório público.

![Alt Text](https://dev-to-uploads.s3.amazonaws.com/i/5z9n7jos2ms9v7jwhgps.png)

Agora digite o comando:

``` 
build  

```
Aparecerá essa pergunta:

``` 
Configure as a single-page app (rewrite all urls to /index.html)? (y/N)

```

Escolha a opção: 

```y```

Aparecerá essa pergunta:

```
File build/index.html already exists. Overwrite? (y/N)

```
Escolha a opção: 

```n```

![Alt Text](https://dev-to-uploads.s3.amazonaws.com/i/3ev4meprhtbvzokk7ldw.png)

Agora iremos para a parte final de construção.
Digite o comando:

```
firebase deploy

```

![Alt Text](https://dev-to-uploads.s3.amazonaws.com/i/cq9mnojalpkgu6h98au9.png)


PRONTO!
FINANMENTE!

Depois de fazer todos esse procedimentos, o console do firebase informará que o processo foi finalizado com sucesso e sua aplicação já está hospedada com um domínio e pronta para ser acessada.




Tutorial:
https://www.youtube.com/watch?v=XoxvXleVZV4