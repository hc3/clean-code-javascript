# clean-code-javascript

## Table of Contents
  1. [Introduction](#introdução)
  2. [Variables](#variaveis)
  3. [Functions](#functions)
  4. [Objects and Data Structures](#objects-and-data-structures)
  5. [Classes](#classes)
  6. [Testing](#testing)
  7. [Concurrency](#concurrency)
  8. [Formatting](#formatting)
  9. [Comments](#comments)

## introdução
![Humorous image of software quality estimation as a count of how many expletives
you shout when reading code](http://www.osnews.com/images/comics/wtfm.jpg)

Software engineering principles, from Robert C. Martin's book
[*Clean Code*](https://www.amazon.com/Clean-Code-Handbook-Software-Craftsmanship/dp/0132350882),
Esse texto é baseado no livro Princípios de engenharia de software, do autor Robert C. Matin’s book, adaptado para javascript.
Esse texto não é um style guide, é um guia para ler, entender , aplicar e refatorar o software em javascript 


Nem todos os princípios abordados aqui devem ser seguidos a risca, e não existe aqui uma solução universal, aqui vamos encontrar orientações e nada a mais, mas orientações baseadas na experiência e outros programadores e dos autores do *Clean Code*.

A engenharia de software é uma área bastante nova que não tem mais que 50 anos, e nós já aprendemos muito nesse tempo, um dia quem sabe quando a engenharia de software for tão antiga quanto a engenharia de construção por exemplo, vamos ter soluções mais definitivas.

Mais uma coisa, sabendo que isso não vai fazer você imediatamente se tornar um grande desenvolvedor e trabalhar com esses padrões são significa que você não vai errar, cada pedaço de código começa com um primeiro rascunho como argila molhada.

## **Variaveis**
### Use nomes de variáveis ​​significativas e pronunciáveis

**Ruim:**
```javascript
var yyyymmdstr = moment().format('YYYY/MM/DD');
```

**Bom**:
```javascript
var yearMonthDay = moment().format('YYYY/MM/DD');
```
**[⬆ back to top](#table-of-contents)**

### Use o mesmo vocabulário para o mesmo tipo de variável

**Ruim:**
```javascript
getUserInfo();
getClientData();
getCustomerRecord();
```

**Bom**:
```javascript
getUser();
```
**[⬆ back to top](#table-of-contents)**

### Usar nomes pesquisáveis
Nós vamos ler mais código do que escrever, então é preciso que o código seja legível e pesquisável.

**Ruim:**
```javascript
// Que merda que é o 525600 ?
for (var i = 0; i < 525600; i++) {
  runCronJob();
}
```

**Bom**:
```javascript
// Declare uma constante maiuscula.
var MINUTES_IN_A_YEAR = 525600;
for (var i = 0; i < MINUTES_IN_A_YEAR; i++) {
  runCronJob();
}
```
**[⬆ back to top](#table-of-contents)**

### Usar variáveis ​​explicativas
**Ruim:**
```javascript
let cityStateRegex = /^(.+)[,\\s]+(.+?)\s*(\d{5})?$/;
saveCityState(cityStateRegex.match(cityStateRegex)[1], cityStateRegex.match(cityStateRegex)[2]);
```

**Bom**:
```javascript
let cityStateRegex = /^(.+)[,\\s]+(.+?)\s*(\d{5})?$/;
let match = cityStateRegex.match(cityStateRegex)
let city = match[1];
let state = match[2];
saveCityState(city, state);
```
**[⬆ back to top](#table-of-contents)**

### Evite o mapeamento mental
Explicit é melhor do que implícito.

**Ruim:**
```javascript
var locations = ['Austin', 'New York', 'San Francisco'];
locations.forEach((l) => {
  doStuff();
  doSomeOtherStuff();
  ...
  ...
  ...
  // espera, o que é  `l` novamente?
  dispatch(l);
});
```

**Bom**:
```javascript
var locations = ['Austin', 'New York', 'San Francisco'];
locations.forEach((location) => {
  doStuff();
  doSomeOtherStuff();
  ...
  ...
  ...
  dispatch(location);
});
```
**[⬆ back to top](#table-of-contents)**

### Don't add unneeded context
If your class/object name tells you something, don't repeat that in your
variable name.

**Bad:**
```javascript
var Car = {
  carMake: 'Honda',
  carModel: 'Accord',
  carColor: 'Blue'
};

function paintCar(car) {
  car.carColor = 'Red';
}
```

**Good**:
```javascript
var Car = {
  make: 'Honda',
  model: 'Accord',
  color: 'Blue'
};

function paintCar(car) {
  car.color = 'Red';
}
```
**[⬆ back to top](#table-of-contents)**

### Short-circuiting is cleaner than conditionals

**Bad:**
```javascript
function createMicrobrewery(name) {
  var breweryName;
  if (name) {
    breweryName = name;
  } else {
    breweryName = 'Hipster Brew Co.';
  }
}
```

**Good**:
```javascript
function createMicrobrewery(name) {
  var breweryName = name || 'Hipster Brew Co.'
}
```
**[⬆ back to top](#table-of-contents)**
