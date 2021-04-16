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

Para se prevenir de ataques cross-site scripting (XSS), os cookies _HttpOnly_ são inacessíveis para a API JavaScript Document.cookie (en-US); eles são enviados só para o servidor. Por exemplo, cookies que persistem sessões de servidor não precisam estar disponíves para o JavaScript, e portanto a diretiva _HttpOnly_ deve ser configurada.

_Set-Cookie: id=a3fWa; Expires=Wed, 21 Oct 2015 07:28:00 GMT; Secure; HttpOnly_

Um cookie HttpOnly é uma tag adicionada a um cookie do navegador que impede que os scripts do lado do cliente acessem os dados. Ele fornece uma porta que evita que o cookie especializado seja acessado por qualquer coisa que não seja o servidor. Usar a tag HttpOnly ao gerar um cookie ajuda a reduzir o risco de scripts do lado do cliente acessarem o cookie protegido, tornando esses cookies mais seguros.

O exemplo abaixo mostra a sintaxe usada no cabeçalho de resposta HTTP:

Set-Cookie: `=“[; “=“]` `[; expires=“][; domain=“]` `[; path=“][; secure][; HttpOnly]`

Se o sinalizador HttpOnly for incluído no cabeçalho de resposta HTTP, o cookie não poderá ser acessado por meio do script do lado do cliente. Como resultado, mesmo que exista uma falha de script entre sites (XSS) e um usuário acesse acidentalmente um link que explora a falha, o navegador não revelará o cookie para terceiros.

Aqui está um exemplo - digamos que um navegador detecte um cookie contendo o sinalizador HttpOnly. Se o código do lado do cliente tentar ler o cookie, o navegador retornará uma string vazia como resultado. Isso ajuda a evitar que códigos maliciosos (geralmente cross-site scripting (XSS)) enviem dados para o site de um invasor.

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

Com um _token_ construído e seguro, é matematicamente impossível decodificar a assinatura sem ter o segredo-chave da aplicação. Porém, uma vez em posse do segredo, qualquer aplicação pode decodificar a assinatura e verificar se ela é válida. Isso é feito gerando uma _signature_ utilizando o header e o _payload_ fornecidos pelo cliente para então comparamos essa _signature_ gerada com a presente no _token_ enviado pelo cliente. Uma vez que as assinaturas sejam idênticas, podemos permitir o acesso do cliente a uma área restrita da nossa aplicação.

https://jwt.io/

## SessionStorage e LocalStorage

#### SessionStorage

- A **sessionStorage** é similar ao localStorage , a única diferença é que enquanto os dados armazenados **no localStorage não expiram, os dados no sessionstorage tem os seus dados limpos ao expirar a sessão da página.** A sessão da página dura enquanto o browser está aberto e se mantém no recarregamento da página.

- O armazenamento na Web pode ser visto de maneira simplista como uma melhoria nos cookies, oferecendo uma capacidade de armazenamento muito maior. O tamanho disponível é de 5 MB, o que representa consideravelmente mais espaço para trabalhar do que um cookie típico de 4KB.

- Os dados não são enviados de volta ao servidor para cada solicitação HTTP (HTML, imagens, JavaScript, CSS, etc) — reduzindo a quantidade de tráfego entre o cliente e o servidor.

- Os dados armazenados no localStorage persistem até serem excluídos explicitamente. As alterações feitas são salvas e estão disponíveis para todas as visitas atuais e futuras ao site.

- Funciona na política de mesma origem. Portanto, os dados armazenados só estarão disponíveis na mesma origem.

#### LocalStorage

Usam o _localStorage_ para armazenar variáveis temporárias.

É semelhante ao localStorage.

- As alterações só estão disponíveis por janela (ou em navegadores como o Chrome e o Firefox). As alterações feitas são salvas e disponibilizadas para a página atual, bem como futuras visitas ao site na mesma janela. Depois que a janela é fechada, o armazenamento é excluído

- Os dados estão disponíveis somente dentro da janela / guia na qual foram definidos.

- Os dados não são persistentes, isto é, serão perdidos quando a janela / guia for fechada. Como o localStorage, ele funciona na política de mesma origem. Portanto, os dados armazenados só estarão disponíveis na mesma origem.

##### Considerações Local e Session Storage

Ambos _localStorage e sessionStorage_ se extendem de _Storage_. Não há diferença entre eles, exceto para a não-persistência de _sessionStorage_.

A não-persistência como descrito acima é no sentido de que _sessionStorage_ se faz disponível apenas para a janela que criou os dados até que tal janela seja fechada, ao abrir outra janela(ou aba) tais dados não estarão disponíveis.

Em contrapartida de _sessionStorage_, ao criar dados em _localStorage_ esses dados estarão disponíveis para qualquer aba/janela mesmo que o usuário encerre a janela, reinicie o sistema, etc.

Um exemplo, vamos supor que você deseja salvar o nome de usuário e senha para realizar um login, é provável que você opte por armazenar esses dados em sessionStorage por motivos de segurança e salvar as configurações de usuário em localStorage.

# Aplicação Real

Armazenar um token de usuário.Nesta etapa, você armazenará o token do usuário. Você implementará diferentes opções de armazenamento de _tokens_ e aprenderá as implicações de segurança de cada abordagem. Por fim, você aprenderá como diferentes abordagens mudarão a experiência do usuário à medida que ele abre novas guias ou fecha uma sessão.

Ao final desta etapa, você poderá escolher uma abordagem de armazenamento com base nos objetivos de seu aplicativo.

Existem várias opções para armazenar _tokens_. Cada opção tem custos e benefícios. Resumidamente, as opções são: armazenar na memória _JavaScript_, armazenar _sessionStorage_, armazenar _localStorage_ e armazenar em um cookie . A principal compensação é a segurança. Qualquer informação armazenada fora da memória do aplicativo atual é _vulnerável a ataques de Cross-Site Scripting (XSS)_ . _O perigo é que, se um usuário mal-intencionado é capaz de carregar código em sua aplicação, ele pode acessar localStorage, sessionStorage e qualquer cookie que também é acessível a sua aplicação_. O benefício dos métodos de armazenamento sem memória é que você pode reduzir o número de vezes que um usuário precisará efetuar login para criar uma melhor experiência do usuário.

Este tutorial irá cobrir _sessionStorage e localStorage_, uma vez que estes são mais modernos do que usar cookies.

# Aplicação do Mundo Real

Armazenar um token de usuário.Nesta etapa, você armazenará o token do usuário. Você implementará diferentes opções de armazenamento de _tokens_ e aprenderá as implicações de segurança de cada abordagem. Por fim, você aprenderá como diferentes abordagens mudarão a experiência do usuário à medida que ele abre novas guias ou fecha uma sessão.

Ao final desta etapa, você poderá escolher uma abordagem de armazenamento com base nos objetivos de seu aplicativo.

Existem várias opções para armazenar _tokens_. Cada opção tem custos e benefícios. Resumidamente, as opções são: armazenar na memória _JavaScript_, armazenar _sessionStorage_, armazenar _localStorage_ e armazenar em um cookie . A principal compensação é a segurança. Qualquer informação armazenada fora da memória do aplicativo atual é _vulnerável a ataques de Cross-Site Scripting (XSS)_ . _O perigo é que, se um usuário mal-intencionado é capaz de carregar código em sua aplicação, ele pode acessar localStorage, sessionStorage e qualquer cookie que também é acessível a sua aplicação_. O benefício dos métodos de armazenamento sem memória é que você pode reduzir o número de vezes que um usuário precisará efetuar login para criar uma melhor experiência do usuário.

Este tutorial irá cobrir _sessionStorage e localStorage_, uma vez que estes são mais modernos do que usar cookies.

- Armazenamento de Sessão
  Para testar os benefícios de armazenamento fora da memória, converta o armazenamento na memória para sessionStorage.

# Usando o cliente frontend ReactJs para interfaces para o usuário.

- Você deve ter conhecimentos básicos e intermediários sobre _ReactJs_ para compreender mais facilmente a implantação se um serviço de autenticação _segura_ _moderna_ _da comunidade_ para logar e deslogar um usuário em um sistema web.

## Quais são as vulnerabilidades?

Ambos os métodos vêm com possíveis problemas de segurança relacionados.

**Links e Referências:**

https://owasp.org/www-community/HttpOnly

https://developer.mozilla.org/en-US/docs/Web/API/Document/cookie

https://developer.mozilla.org/pt-BR/docs/Web/HTTP/Cookies

https://developer.mozilla.org/en-US/docs/Web/API/IndexedDB_API

https://developer.mozilla.org/en-US/docs/Web/API/Web_Storage_API

https://www.taniarascia.com/full-stack-cookies-localstorage-react-express/

https://www.digitalocean.com/community/tutorials/how-to-add-login-authentication-to-react-applications#prerequisites
