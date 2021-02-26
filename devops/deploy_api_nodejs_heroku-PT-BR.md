# Deploy NodeJS, Mysql Heroku

## Instalando o Heroku Global

- Não enviar o projeto para deploy com a pasta _node_modules_ no projeto. **Exclua** antes de iniciar esse procedimento.

```bat
npm install -g heroku
```

Crie uma pasta chamada _DEPLOY_ dentro dela coloque seu projeto nodejs.

Logando na conta heroku:

```bat
heroku login
```

![Alt Text](https://dev-to-uploads.s3.amazonaws.com/i/cf9mvdoci8zwpycqhgba.png)

Entre no projeto:

```bat
cd ghd-sites-email-service-node
```

Criando o arquivo _Procfile_ na raiz do projeto:

Digite o codigo:

```bat
web: node server.js
```

![Alt Text](https://dev-to-uploads.s3.amazonaws.com/i/c7nmmy7o237484ebfl31.png)

Iniciando o Git heroku:

```bat
git init
```

```bat
heroku git:remote -a ghd-sites-email-service-node
```

Verificando no git remote:

```bat
git remote -v
```

![Alt Text](https://dev-to-uploads.s3.amazonaws.com/i/bnj43oepi0vhm79dzsoa.png)

Git:

```bat
git add .

```

```bat
git commit -m "frist commit"

```

Deploy Build:

```bat
git push heroku master
```

Sucesso:

```bat
remote: -----> Build succeeded!
remote: -----> Discovering process types
remote:        Procfile declares types -> web
remote:
remote: -----> Compressing...
remote:        Done: 34.3M
remote: -----> Launching...
remote:        Released v3
remote:        https://ghd-sites-email-service-node.herokuapp.com/ deployed to Heroku
remote:
remote: Verifying deploy... done.
To https://git.heroku.com/ghd-sites-email-service-node.git
 * [new branch]      master -> master
```

![Alt Text](https://dev-to-uploads.s3.amazonaws.com/i/n7mn0hjn97gwhi46h9nc.png)

Acessando nosso link da API:
https://ghd-sites-email-service-node.herokuapp.com/v1/ping

![Alt Text](https://dev-to-uploads.s3.amazonaws.com/i/ic9nf70v4gzxm4peayh5.png)





- Fonte:
https://www.youtube.com/watch?v=HyctLjnzUOM&feature=emb_logo
