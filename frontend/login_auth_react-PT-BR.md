# Autenticação Cookies HTTP, HTTP Only, JWT, SessionStorage, LocalStorage com ReactJs UI e Nodejs API.

## Visão geral

O objetivo desta artigo é apresentar, discutir e fornecer técnicas de mitigação específicas sobre as melhores práticas de autenticação e sessão de usuários, usando _Cookies, Http Only, JWT, Sessão, LocalStorage, e outros métodos._

## Cookies Http

Um cookie HTTP (um cookie web ou cookie de navegador) é um pequeno fragmento de dados que um servidor envia para o navegador do usuário. O navegador pode armazenar estes dados e enviá-los de volta na próxima requisição para o mesmo servidor. Normalmente é utilizado para identificar se duas requisições vieram do mesmo navegador — ao manter um usuário logado, por exemplo. Ele guarda informações dinâmicas para o protocolo HTTP sem estado.

#### Cookies são usados principalmente para três propósitos:

##### Gerenciamento de sessão:

Logins, carrinhos de compra, placar de jogos ou qualquer outra atividade que deva ser guardada por um servidor.

##### Personalização:

Preferências de usuário, temas e outras configurações.

##### Rastreamento:

Registro e análise do comportamento de um usuário.

## Http Only

![Alt Text](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/oqh0wmupnkvrq8vp8ig8.png)

#### O que é HttpOnly?

Acordo com a Microsoft Developer Network , HttpOnly é um sinalizador adicional incluído em um cabeçalho de resposta HTTP Set-Cookie. Usar o sinalizador HttpOnly ao gerar um cookie ajuda a mitigar o risco de o script do lado do cliente acessar o cookie protegido (se o navegador oferecer suporte).

## JWT

![Alt Text](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/bjpz9k516q6cxhps8xo0.png)

#### Autenticação de usuário utilizando o mecanismo chamado JWT (JSON Web Token)

Estratégia de autenticação para APIs em REST simples e segura. Trata-se de um padrão aberto para autenticações web e é totalmente baseada em requests JSON entre o cliente e servidor. Seu mecanismo de autenticação funciona da seguinte maneira:

- O cliente faz uma solicitação uma única vez ao enviar as credenciais de login e senha;

- O servidor valida as credenciais e, se tudo estiver certo, ele retorna para o cliente um JSON com um token que codifica dados de um usuário logado no sistema;

- Após receber o token, o cliente pode armazená-lo da forma que preferir, seja por LocalStorage, Cookie ou outros mecanismos de armazenamento do lado do cliente;

- Toda vez que o cliente acessa uma rota que requere autenticação, ele apenas envia esse token para a API para autenticar e liberar os dados de consumo;

- O servidor sempre valida esse token para permitir ou bloquear uma solicitação de cliente.
  
###### JWT (JSON Web Token) é um método RCT 7519 padrão da indústria para realizar autenticação entre duas partes por meio de um token assinado que autentica uma requisição web. Esse token é um código em Base64 que armazena objetos JSON com os dados que permitem a autenticação da requisição.

Com um *token* construído e seguro, é matematicamente impossível decodificar a assinatura sem ter o segredo-chave da aplicação. Porém, uma vez em posse do segredo, qualquer aplicação pode decodificar a assinatura e verificar se ela é válida. Isso é feito gerando uma *signature* utilizando o header e o *payload* fornecidos pelo cliente para então comparamos essa *signature* gerada com a presente no *token* enviado pelo cliente. Uma vez que as assinaturas sejam idênticas, podemos permitir o acesso do cliente a uma área restrita da nossa aplicação.

https://jwt.io/

## SessionStorage e LocalStorage

Armazenar um token de usuário.Nesta etapa, você armazenará o token do usuário. Você implementará diferentes opções de armazenamento de *tokens* e aprenderá as implicações de segurança de cada abordagem. Por fim, você aprenderá como diferentes abordagens mudarão a experiência do usuário à medida que ele abre novas guias ou fecha uma sessão.

Ao final desta etapa, você poderá escolher uma abordagem de armazenamento com base nos objetivos de seu aplicativo.


**Links e Referências:**

https://owasp.org/www-community/HttpOnly

https://developer.mozilla.org/pt-BR/docs/Web/HTTP/Cookies

https://developer.mozilla.org/en-US/docs/Web/API/IndexedDB_API

https://developer.mozilla.org/en-US/docs/Web/API/Web_Storage_API

https://www.taniarascia.com/full-stack-cookies-localstorage-react-express/

https://www.digitalocean.com/community/tutorials/how-to-add-login-authentication-to-react-applications#prerequisites
