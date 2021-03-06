# Revisão javascript

- 60 minutos em velocidade de cruzeiro

## Definição

- linguagem criada em... abre a [wikipedia](https://en.wikipedia.org/wiki/JavaScript) aí e veja!
- começou humilde, sem grande importância
- cresceu junto com a internet
- hoje é ubíqua, está [em todo o lugar](https://tessel.io/)

## Aplicação

- interface com o usuário
- servidores em intranets empresariais
- servidores de alta disponibilidade
- sistemas de mensagens assíncronas

## Exemplo

```javascript
console.log("Hello World!");
// alert("Hello World!");
```

- Regras sintáticas mirando o [ES5](https://es5.github.io/) e alguns conceitos do [ES6](http://es6-features.org/)

### Variáveis

```javascript
var x = 2
let y = 3
const z = 4
```

- **var** é escopo de instância. E é velho (a.k.a. *feio*) também, faz evangelista chorar baixinho
- **let** é escopo de bloco. É bonito. Usem
- **const** é de bloco e imutável. A peruada do funcional curte

### Estruturas de controle

```javascript
let a = 10;
let b = 20;
let m = 10;
let i = 10;
let k = 10;

if(a > b){
  // ...
}

switch(m){
  case 5:
    // ...
  break;
  case 10:
    // ...
  break;
  case 15:
    // ...
  break;
  default:
    // ...
  break;
}

for(let j = 0 ; j < 10 ; j++ ){
  // ...
}

while(i-->0){
  console.log(i);
}

do{
  // ...
  k = k -1;
}while(k);
```

- Os valores **0, "", null** e **undefined** funcionam como **false** também
- excetuando o switch, o bloco é opcional se executarmos uma única instrução

### Funções

```javascript
function soma(x,y){
  return x + y;
}

var soma = function(x,y){
  return x + y;
}
```

- funções tem os mesmos direitos de variáveis
- funções podem ser argumentos de outras funções

```javascript
function foo(x){
  console.log(x);
}

function bar(x,y){
  x(y);
}

// uso:

bar(foo,2)
// imprime 2

bar(console.log,2);
// imprime 2 do mesmo jeito

// pode ser anônima também:
bar(function(x){
  console.log(x*x);
},2);
```

- importante observar o escopo de execução (falamos adiante)
- exótico? conheça agora a fat arrow

```javascript
function bar(x,y){
  x(y);
}

bar((x) => console.log(x) ,2)
// imprime 2

// na fat arrow function o retorno é o corpo da função. Exemplo:

function compara(a,b){
  return a - b;
}

let lista = [2,1,3];

lista.sort(compara);
// [1,2,3]

lista.sort((a,b) => a - b)
// [1,2,3] do mesmo jeito
```

- a fat arrow existe nos navegadores mais recentes
- não cria escopo especial como as funções passadas por parâmetro fazem (o 'this' está correto)

### Coleções (mapas e listas)

```javascript
var lista1 = [];
lista1.push(1);
// [1]
lista1.push("Arroz");
// [1,"Arroz"]
lista1.push({a:2});
// [1,"Arroz",{a:2}]
lista1.push([2,3,4]);
// [1,"Arroz",{a:2},[2,3,4]]
lista1.pop();
// [1,"Arroz",{a:2}]
lista1.shift();
// ["Arroz",{a:2}]
lista1.unshift(4);
// [4,"Arroz",{a:2}]

var mapa1 = {a:1};
mapa.b=2;
mapa.c={d:3};
// {a:1, b:2, c:{d:3}}
```

- listas tem o atributo especial **.length** que diz o tamanho delas
- você pode inserir qualquer coisa em listas e mapas. Aqui não tem frescura

```javascript
var lista2 = [5,10,15,20,25,30,35];
var mapa2 = {a:1,b:2,c:3,d:4};

for(let x in lista2)
  console.log(lista2[x]);
// 5,10,15,20,25,30,35
for(let y in mapa2)
  console.log("%s: %s, ",y,mapa2[y]);
// a: 1, b: 2, c: 3, d: 4,
console.log("a" in mapa2)
// true
console.log("e" in mapa2)
// false
```

- mapas e listas tem direito a sintaxe especial no **for**
- o **in** funciona como operador pra testar a existência do membro

### Um pouco de orientação a objetos e o **this** (os problemas relacionados a instância e escopo)

- conceitos relacionados ao **es6** apenas

```javascript
class Shape {
    constructor (id, x, y) {
        this.id = id;
        this.move(x, y);
    }
    move (x, y) {
        this.x = x;
        this.y = y;
    }
}

let s = new Shape(1,0,0);
s.move(3,3);
// Shape {id: 1, x: 3, y: 3}
```

- o **this** é conhecido de quem já viu java. É o mesmo que o **self** da turma do **Python**
- o **new** é o operador de instanciação. Ele chama o contrutor da classe

```javascript
class Rectangle extends Shape {
    constructor (id, x, y, width, height) {
        super(id, x, y)
        this.width  = width
        this.height = height
    }
}
class Circle extends Shape {
    constructor (id, x, y, radius) {
        super(id, x, y)
        this.radius = radius
    }
}

let r = new Rectangle(2,0,0,5,5);
let c = new Circle(3,0,0,6);
console.log(r instanceof Shape);
console.log(c instanceof Shape);
console.log(r instanceof Rectangle);
console.log(c instanceof Circle);
console.log(c instanceof Rectangle);
// true, true, true, true, false
```

- herança de características
- você pode acessar os comportamentos da classe ancestral utilizando o **[super](http://es6-features.org/#BaseClassAccess)**
- note a tipagem. Às vezes é útil!
- apenas reforçando, o **this** aponta para a **instância**!
  - tenho 4 retângulos, cada um tem um this, cada um tem um estado distinto um do outro

## Exercício

- crie no github um repositório chamado Hello-nodejs-aula-1 e crie um arquivo .js para cada conceito visto.
- encontre o código mostrado no git ou em qualquer lugar da internet.
