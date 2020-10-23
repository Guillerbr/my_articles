Partindo do princípio que você domine parcialmente o que é **Nodejs, Reactjs, Java Script, HTML,CSS**, nesse artigo tentarei detalhar todo o processo para criarmos uma página totalmente responsiva, sendo aceita e modificada conforme as dimensões da tela do usuário.

Isso quer dizer que projetaremos um **frontend** moderno para qualquer tamanho de tela, desde celulares a monitores e tabletes, nosso site se ajustará ao tamanho da tela do dispositivo, aumentando assim a qualidade da usabilidade.

A responsividade é um dos pilares de um bom desenvolvedor frontend, tenha como amiga sempre!
O conceito de **responsividade** é : *Se adaptar ao meio*

O conceito que usaremos é o de **Media Queries** juntamente com **Reactjs** e um pacote bastante conhecido, **styled-components** para estilização.


  ![Alt Text](https://dev-to-uploads.s3.amazonaws.com/i/17lit7kkimacuu6r360q.png)

Criei um novo projeto react e iniciei o projeto com os *comandos*:

```

npx create-react-app my-app
cd my-app
npm start

```
Instale as dependências **Styled Components e React Router Dom** 

```
 yarn add styled-components 

```

```
 yarn add react-router-dom

```

![Alt Text](https://dev-to-uploads.s3.amazonaws.com/i/ky8znvjsh5g7blmkyf6f.png)

Dentro da estrutura de pastas, crie sua arquitetura assim:

![Alt Text](https://dev-to-uploads.s3.amazonaws.com/i/isv6gfizwdopaks5v6o4.png)

Cria um pasta chamada **styles** dentro da pasta **src**.Agora dentro da pasta styles , crie um arquivo **globals.js**.
Dentro dele cole o esse código:

```javascript

import { createGlobalStyle } from 'styled-components';

export default createGlobalStyle`
  * {
    margin: 0;
    padding: 0;
    outline: 0;
    box-sizing: border-box;
  }
  body {
    -webkit-font-smoothing: antialiased !important;
  }
  body html #root {
    height: 100%;
  }
`;

```

Agora dentro da pasta **src** ,crie uma pasta chamada **components** e dentro dela outra chamada **header**

Dentro da pasta **header** crie dois arquivos: **index.js** e **styles.js**

Dentro de **index.js** como o seguinte código:

 ```javascript

import React from "react";
import { Container } from "./styles";

export default function Header() {
  return (
    <Container>
      <img
        src="http://www.pngmart.com/files/2/Zelda-Link-PNG-Clipart.png"
        alt="Logo"
      />
      <button type="button">Acessar</button>
    </Container>
  );
}

```

Dentro de **styles.js** com o seguinte código:

 ```javascript

import styled from "styled-components";

export const Container = styled.div`
  position: sticky;
  top: 0;
  background-color: #fff;
  width: 100%;
  max-width: 1168px;
  display: flex;
  justify-content: space-between;
  align-items: center;
  z-index: 10;
  padding: 0 24px;
  margin: 40px auto 0;
  overflow: hidden;
  button {
    text-transform: uppercase;
    font-weight: bold;
    width: 240px;
    background: #73678a;
    border-width: initial;
    border-style: none;
    border-radius: 5px;
    cursor: pointer;
    height: 54px;
    transition: background 0.2s;
    font-size: 16px;
    color: white;
    &:hover {
      background: #795a8b;
    }
  }

  @media (max-width: 800px) {
    flex-direction: column;
    position: relative;
  }

  @media (max-width: 800px) {
    button {
      margin-left: 0px;
      margin-top: 10px;
      background: #100f12;
      border-radius: 5px;
    }
  }
`;


 ```
No arquivo **styles.js**:

Se atente para a tag **@media** elas são as responsáveis pela mágica no processo de se adaptar ao tamanho da tela.

 ```
 @media (max-width: 800px) {
    flex-direction: column;
    position: relative;
  }

  @media (max-width: 800px) {
    button {
      margin-left: 0px;
      margin-top: 10px;
      background: #100f12;
      border-radius: 5px;
    }
  }

 ```

Agora vamos finalizar a configuração no arquivo **App.js**
Digite o seguinte código:

```javascript

import React from "react";
import { BrowserRouter } from "react-router-dom";


//import Routes from './routes';
import GlobalStyle from "./styles/globals";

//components and pages
import Header from "./components/header";

export default function App() {
  return (
    <BrowserRouter>
      <Header />
      {/* <Routes /> */}
      <GlobalStyle />
    </BrowserRouter>
  );
}


```


Pronto!
Se tudo estiver certo poderá ver que a página **responsiva**
readaptando conforme seu tamanho.

![Alt Text](https://dev-to-uploads.s3.amazonaws.com/i/8uvtilimj5xam97z72be.png)

![Alt Text](https://dev-to-uploads.s3.amazonaws.com/i/22jlmnd85qlqb0zfqo9x.png)

![Alt Text](https://dev-to-uploads.s3.amazonaws.com/i/wb579q0wqexmld4d6094.png)

![Alt Text](https://dev-to-uploads.s3.amazonaws.com/i/nwotql2gv9rqtysm6wdz.png)






Tutorial:

https://medium.com/reactbrasil/utilizando-media-queries-no-react-com-styled-components-f0f3160f3f01

https://dev.to/carloscne/criando-paginas-responsivas-e-adaptativas-com-react-e-styled-components-1gje

https://alistapart.com/article/responsive-web-design/

https://developer.mozilla.org/en-US/docs/Web/CSS/Media_Queries/Using_media_queries#Media_features

https://www.youtube.com/watch?v=yU7jJ3NbPdA

https://www.youtube.com/watch?v=gYak6y7rbRw

