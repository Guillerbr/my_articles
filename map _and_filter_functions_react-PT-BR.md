Ao final desse artigo seremos capazes de entender e aplicar conhecimento relacionado:

1-Receber dados (objetos Json) uma API.

2-Imprimir os resultados dos dados em uma lista ordenada.

3-Além disso criaremos um motor de busca com o filter,uma função do Java Script.Isso permitirá buscar determinadas informações da API/lista de dados.

Recentemente tive um desafio de pegar os dados de uma API,filtrar,criar uma busca e imprimir em uma página web,usando ReactJS.

O ReactJS é um Biblioteca Java Script para cliente Frontend.

Para isso teremos que usar funções nativas do java script.Funções que nos permitirão fazer,ordenação, manipulação de objetos em Arrays,objetos JSON,em diferentes formatações de objeto.

Referência e documentação do Java Script:

https://developer.mozilla.org/pt-BR/docs/Web/JavaScript

https://www.w3schools.com/jsref/

Função Map do Java Script:

O objeto Map é um mapa simples de chave/valor. Qualquer valor (objeto e valores primitivos) pode ser usado como uma chave ou um valor.

https://developer.mozilla.org/pt-BR/docs/Web/JavaScript/Reference/Global_Objects/Map

Função Filter do Java Script:

O método filter() cria um novo array com todos os elementos que passaram no teste implementado pela função fornecida.

https://developer.mozilla.org/pt-BR/docs/Web/JavaScript/Reference/Global_Objects/Array/filtro

Existem diversos tipos de objetos json que retornam das APIS:

Por volta de todo o objeto/array json:


Interno:

```javascript
{
  "AALR3": {
    "Cresc.5a": "0,48",
    "DY": "0,77%",
    "Div.Brut/Pat.": "1.282.190.000,00",
    "EBITDA": "7,50",
    "EV/EBIT": "14,53",
    "Liq.2m.": "3,22%",
    "Liq.Corr.": "4,67%",
    "Mrg.Liq.": "11,73%",
    "P/Ativ.Circ.Liq.": "-1,96",
    "P/Ativo": "0,542",
    "P/Cap.Giro": "120,35",
    "P/EBIT": "10,34",
    "P/L": "31,51",
    "P/VP": "1,01",
    "PSR": "1,213",
    "Pat.Liq": "7.649.360,00",
    "ROE": "5,57%",
    "ROIC": "1,03",
    "cotacao": "11,00"
  },
  "ABCB4": {
    "Cresc.5a": "0,00",
    "DY": "7,54%",
    "Div.Brut/Pat.": "4.040.730.000,00",
    "EBITDA": "0,00",
    "EV/EBIT": "0,00",
    "Liq.2m.": "13,08%",
    "Liq.Corr.": "0,00%",
    "Mrg.Liq.": "0,00%",
    "P/Ativ.Circ.Liq.": "0,00",
    "P/Ativo": "0,000",
    "P/Cap.Giro": "0,00",
    "P/EBIT": "0,00",
    "P/L": "5,75",
    "P/VP": "0,75",
    "PSR": "0,000",
    "Pat.Liq": "14.177.800,00",
    "ROE": "0,00%",
    "ROIC": "0,00",
    "cotacao": "13,92"
  },
  "ABEV3": {
    "Cresc.5a": "0,05",
    "DY": "4,28%",
    "Div.Brut/Pat.": "61.278.000.000,00",
    "EBITDA": "8,52",
    "EV/EBIT": "10,99",
    "Liq.2m.": "19,22%",
    "Liq.Corr.": "23,17%",
    "Mrg.Liq.": "29,65%",
    "P/Ativ.Circ.Liq.": "-15,58",
    "P/Ativo": "1,771",
    "P/Cap.Giro": "69,03",
    "P/EBIT": "11,55",
    "P/L": "15,29",
    "P/VP": "2,94",
    "PSR": "3,425",
    "Pat.Liq": "485.884.000,00",
    "ROE": "20,61%",
    "ROIC": "1,10",
    "cotacao": "11,45"
  }
}
```

Ele não é o único tipo de retorno Json de APIS,
elas obviamente podem ter arrays de objetos em outros formatos,como:

```javascript
["Go to the store", "Wash the dishes", "Learn some code"];
```

E outros:

```javascript
[
  {
    userId: 1,
    id: 1,
    title: "delectus aut autem",
    completed: false,
  },
  {
    userId: 1,
    id: 2,
    title: "quis ut nam facilis et officia qui",
    completed: false,
  },
  {
    userId: 1,
    id: 3,
    title: "fugiat veniam minus",
    completed: false,
  },
  {
    userId: 1,
    id: 4,
    title: "et porro tempora",
    completed: true,
  },
  {
    userId: 1,
    id: 5,
    title: "laboriosam mollitia et enim quasi adipisci quia provident illum",
    completed: false,
  },
  {
    userId: 1,
    id: 6,
    title: "qui ullam ratione quibusdam voluptatem quia omnis",
    completed: false,
  },
];
```

```javascript
{
    "items": [
        {
            "product": {
                "id": 2321312,
                "name": "Smartphone Apple iPhone 7 128GB",
                "images": [
                    "http://thumbs.buscape.com.br/celular-e-smartphone/smartphone-apple-iphone-7-128gb_600x600-PU98460_1.jpg",
                    "http://thumbs.buscape.com.br/celular-e-smartphone/smartphone-apple-iphone-7-128gb/__200x400-PU98460_2_c.jpg?v=2347575274",
                    "http://thumbs.buscape.com.br/celular-e-smartphone/smartphone-apple-iphone-7-128gb/__200x400-PU98460_3_c.jpg?v=318433138",
                    "http://thumbs.buscape.com.br/celular-e-smartphone/smartphone-apple-iphone-7-128gb/__200x400-PU98460_4_c.jpg?v=33273730"
                ],
                "price": {
                    "value": 3509.10,
                    "installments": 10,
                    "installmentValue": 389.90
                }
            }
        },
        {
            "product": {
                "id": 9971,
                "name": "Smart TV Samsung Série 4 UN32J4300AG 32 polegadas LED Plana",
                "images": [
                    "http://mthumbs.buscape.com.br/tv/smart-tv-samsung-serie-4-un32j4300ag-32-polegadas-led-plana_600x600-PU95547_1.jpg",
                    "http://thumbs.buscape.com.br/__400x400-PU95547_2_c.jpg?v=3988579075",
                    "http://thumbs.buscape.com.br/__400x400-PU95547_4_c.jpg?v=4208003525",
                    "http://thumbs.buscape.com.br/__231312400x400-PU95547_5_c.jpg?v=1473261122"
                ],
                "price": {
                    "value": 1139.90,
                    "installments": 10,
                    "installmentValue": 134.11
                }
            }
        },
        {
            "product": {
                "id": 6717131,
                "name": "Câmera Digital Canon EOS Rebel T5i 18.0 Megapixels",
                "images": [
                    "http://mthumbs.buscape.com.br/camera-digital/canon-eos-rebel-t5i-18-0-megapixels_600x600-PU7bf7b_1.jpg"
                ],
                "price": {
                    "value": 1999.20,
                    "installments": 10,
                    "installmentValue": 235.20
                }
            }
        },
        {
            "product": {
                "id": 6717131,
                "name": "Lenovo IdeaPad 310 80UH0004BR Intel Core i7-6500U 2.5 GHz 8192 MB 1024 GB",
                "images": [
                    "http://mthumbs.buscape.com.br/notebook/lenovo-ideapad-310-80uh0004br-intel-core-i7-6500u-2-5-ghz-8192-mb-1024-gb_600x600-PU98e6e_1.jpg"
                ],
                "price": {
                    "value": 2599.00,
                    "installments": 10,
                    "installmentValue": 259.90
                }
            }
        }
    ]
}

```

E outra:

```javascript
{
"Global Quote": {"01. symbol":"TSLA","02. open":"777.8700","03. high":"789.7500","04. low":"770.7700","05. price":"771.8426","06. volume":"6995867","07. latest trading day":"2020-02-12","08. previous close":"774.3800","09. change":"-2.5374","10. change percent":"-0.3277%"}
}

{
  "Meta Data": {
    "1. Information": "Intraday (5min) open, high, low, close prices and volume",
    "2. Symbol": "IBM",
    "3. Last Refreshed": "2020-04-09 16:00:00",
    "4. Interval": "5min",
    "5. Output Size": "Compact",
    "6. Time Zone": "US/Eastern"
  },
  "Time Series (5min)": {
    "2020-04-09 16:00:00": {
      "1. open": "122.1400",
      "2. high": "122.2100",
      "3. low": "121.4300",
      "4. close": "121.5200",
      "5. volume": "269094"
    },
    "2020-04-09 15:55:00": {
      "1. open": "121.6500",
      "2. high": "122.2300",
      "3. low": "121.2879",
      "4. close": "122.1350",
      "5. volume": "226196"
    },
    "2020-04-09 15:50:00": {
      "1. open": "122.2000",
      "2. high": "122.3800",
      "3. low": "121.5000",
      "4. close": "121.7000",
      "5. volume": "107933"
    }
}

```

A diferença entre esses vários objetos faz com que devamos usar uma forma de código para casa caso.Note que os objetos são diferentes,assim devemos indexar e tratar cada tipo de encapsulamento de objetos JSON como únicos.
Analisando e aplicando as funções e regras corretas,conseguiremos imprimir,buscar e manipular os dados do objeto.

Algumas funções JS que podem ser usados no ReactJS:

Object.values:
O método Object.keys() retorna um array de propriedades enumeraveis de um determinado objeto, na mesma ordem em que é fornecida por um laço for...in (a diferença é que um laço for-in enumera propriedades que estejam na cadeia de protótipos).

https://developer.mozilla.org/pt-BR/docs/Web/JavaScript/Reference/Global_Objects/Object/values

Object.keys:
O método Object.keys() retorna um array de propriedades enumeráveis de um determinado objeto, na mesma ordem em que é fornecida por um laço for...in (a diferença é que um laço for-in enumera propriedades que estejam na cadeia de protótipos).

https://developer.mozilla.org/pt-BR/docs/Web/JavaScript/Reference/Global_Objects/Object/keys

Conceitos e montagem do ciclo de vida no ReactJS.

Para trazer os dados corretamente na tela do usuário devemos
usar os conceitos de Component,Stateful/Stateless, Props,State,setState(),ComponentDidMount,ComponentWillReceiveProps,Arrow Functions,Funções de onClick,Funções Anônimas,Funções de Evento handleChange(e), { entre outras técnicas e funções.
Depois iremos renderizar os dados na tela.

É muito importante sabermos o id ou indexador do item que queremos buscar,assim será mais fácil escolher qual tipo de sintaxe usar,mas tudo estará em volta dos conceitos de:

ReactJS código fonte:

```javascript
class App extends React.Component {
  constructor(props) {
    /*	 
	
	  state = {
    stockdata: [],
    namestock: []
  };    
	
	*/

    super(props);
    this.state = {
      list: ["Go to the store", "Wash the dishes", "Learn some code"],

      stockdata: [],
      namestock: [],

      //  stockdata: Object.values(res),
      //  namestock: Object.keys(res)
    };
    this.addItem = this.addItem.bind(this);
    this.removeItem = this.removeItem.bind(this);
  }

  addItem(e) {
    // Prevent button click from submitting form
    e.preventDefault();

    // Create variables for our list, the item to add, and our form
    let list = this.state.list;
    const newItem = document.getElementById("addInput");
    const form = document.getElementById("addItemForm");

    // If our input has a value
    if (newItem.value != "") {
      // Add the new item to the end of our list array
      list.push(newItem.value);
      // Then we use that to set the state for list
      this.setState({
        list: list,
      });
      // Finally, we need to reset the form
      newItem.classList.remove("is-danger");
      form.reset();
    } else {
      // If the input doesn't have a value, make the border red since it's required
      newItem.classList.add("is-danger");
    }
  }

  removeItem(item) {
    // Put our list into an array
    const list = this.state.list.slice();
    // Check to see if item passed in matches item in array
    list.some((el, i) => {
      if (el === item) {
        // If item matches, remove it from array
        list.splice(i, 1);
        return true;
      }
    });
    // Set state to list
    this.setState({
      list: list,
    });
  }

  render() {
    return (
      <div className="content">
        <div className="container">
          <section className="section">
            <List items={this.state.list} delete={this.removeItem} />
          </section>
          <hr />
          <section className="section">
            <form className="form" id="addItemForm">
              <input
                type="text"
                className="input"
                id="addInput"
                placeholder="Something that needs ot be done..."
              />
              <button className="button is-info" onClick={this.addItem}>
                Add Item
              </button>
            </form>
          </section>
        </div>
      </div>
    );
  }
}

class List extends React.Component {
  constructor(props) {
    super(props);
    this.state = {
      filtered: [],
    };
    this.handleChange = this.handleChange.bind(this);
  }

  componentDidMount() {
    /*
		
		fetch("http://localhost:5000")
      .then(res => res.json())
      .then(res => {
        this.setState({
          stockdata: Object.values(res),
          namestock: Object.keys(res)
        });
        //console.log(this.state.stockdata);
      });
			
		*/

    this.setState({
      filtered: this.props.items,
      //filtered: this.props.stockdata,
      //filtered: this.props.namestock
    });
  }

  componentWillReceiveProps(nextProps) {
    this.setState({
      filtered: nextProps.items,
    });
  }

  handleChange(e) {
    // Variable to hold the original version of the list
    let currentList = [];
    // Variable to hold the filtered list before putting into state
    let newList = [];

    // If the search bar isn't empty
    if (e.target.value !== "") {
      // Assign the original list to currentList
      currentList = this.props.items;

      // Use .filter() to determine which items should be displayed
      // based on the search terms
      newList = currentList.filter((item) => {
        // change current item to lowercase
        const lc = item.toLowerCase();
        // change search term to lowercase
        const filter = e.target.value.toLowerCase();
        // check to see if the current list item includes the search term
        // If it does, it will be added to newList. Using lowercase eliminates
        // issues with capitalization in search terms and search content
        return lc.includes(filter);
      });
    } else {
      // If the search bar is empty, set newList to original task list
      newList = this.props.items;
    }
    // Set the filtered state based on what our rules added to newList
    this.setState({
      filtered: newList,
    });
  }

  render() {
    return (
      <div>
        <input
          type="text"
          className="input"
          onChange={this.handleChange}
          placeholder="Search..."
        />
        <ul>
          {this.state.filtered.map((item) => (
            <li key={item}>
              {item} &nbsp;
              <span
                className="delete"
                onClick={() => this.props.delete(item)}
              />
            </li>
          ))}
        </ul>
      </div>
    );
  }
}

ReactDOM.render(<App />, document.getElementById("app"));
```

Exemplos:

Exemplos CodePen-CodeSandBox:

https://codepen.io/Guillerbr/pen/oNjgpod

https://codesandbox.io/s/filter-react-search-function-api-data-gxtqk

Fontes:

https://medium.com/@programadriano/javascript-entendendo-a-diferen%C3%A7a-entre-map-x-foreach-366a77fc7e82

https://medium.com/@programadriano/javascript-conhecendo-map-filter-e-reduce-ce072d8f0ec5

https://medium.com/@marcellguilherme/aprenda-tudo-sobre-reduce-ou-fold-fd71de86ce53

https://dev.to/iam_timsmith/lets-build-a-search-bar-in-react-120j

https://desenvolvimentoparaweb.com/javascript/map-filter-reduce-javascript/

https://www.w3schools.com/jsref/

https://developer.mozilla.org/pt-BR/docs/Web/JavaScript/Reference/Global_Objects/Map

https://developer.mozilla.org/pt-BR/docs/Web/JavaScript/Reference/Global_Objects/Array/filtro

https://developer.mozilla.org/pt-BR/docs/Web/JavaScript/Reference/Global_Objects/Object/keys

https://developer.mozilla.org/pt-BR/docs/Web/JavaScript/Reference/Global_Objects/Object/values
