Referência:
https://github.com/vaneves/apirus

Crie um novo projeto Laravel,dentro dele, adicione a Apirus ferramenta ao projeto, digite o comando de instalação:

``` composer create-project --prefer-dist vaneves/apirus ```

Se for instalar fora de um projeto Laravel,use o comando:

``` composer create-project --prefer-dist vaneves/apirus meu_projeto```


Entre na pasta **apirus**.
Altere o nome do arquivo .env.exemple para .env

```cp .env.example .env```



No arquivo .env altere as variáveis de ambientes.

``` 
API_URL=http://example.com/api

SOURCE=
DIST=
THEME=
HIGHTLIGHT=  

```

Entre na pasta **apirus**,e depois em DOCS,será nesse diretório que devemos enviar a documentação da nossa API,no formato markdown,para que o interpretador nos forneça uma interface visual e de fácil manipulação e teste.

Dentro do diretório /docs atualize sua documentação enviando seu novo diretório com os arquivos.


![Alt Text](https://dev-to-uploads.s3.amazonaws.com/i/98q6twjnwywskubmcbm0.png)

Dentro da sua pasta **DOCS**,deve ter algo como isso.Arquivos em 
**Markdown** .md que irão formatar os código para que a interface gráfica da ferramenta,possa nos fornecer uma documentação e teste mais amigável.


![Alt Text](https://dev-to-uploads.s3.amazonaws.com/i/1pq1hotfdzbx5ejqmcqs.png)


Após fazer o processo,precisamos buildar as atualizações,digitaremos os seguintes comandos:

Incialmente:

``` php apirus```

E para atualizar a documentação digite esse comando após atualizar seu diretório em /docs. Comando:

``` php apirus --src docs -h monokai```



![Alt Text](https://dev-to-uploads.s3.amazonaws.com/i/ibdk1i01d760s1xo18cm.png)



Pronto,tudo certo,podemos ter como resultado a documentação da api em:

``` http://localhost/meu_projeto/public/ ```


![Alt Text](https://dev-to-uploads.s3.amazonaws.com/i/6tl179cdoe2b49yebrnn.png)


Em desenvolvimento/finalização
Vídeo Tutorial:
https://www.youtube.com/watch?v=qKJX56K6QdY
