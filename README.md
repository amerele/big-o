# 📘 Entender Big O Notation vai fazer você programar melhor!

## 🤔 O que é?

As funções que escrevemos podem se comportar de maneira diferente conforme recebem mais dados.  
Chamamos isso de **escalabilidade**.

A **Big O Notation** é como uma “fórmula” que classifica como o algoritmo funciona em relação a quantidade de dados recebido.
Sua sintaxe lembra as fómulas de matemática da escola:

- `O(n)`
- `O(1)`
- `O(n²)`
- `O(log n)`
- etc.

A letra **O** não importa muito para nós. O que realmente significa algo é o valor dentro dos parênteses:  
ele indica **quantas operações o algoritmo executa para ser concluído**.


## 🔎 Classificando Funções

A seguir, alguns exemplos simples em JavaScript e suas respectivas classificações em Big O:

```js
const numeros = [0, 1, 2, 3, 4, 5, 6, 7, 8, 9];

// Busca no array pelo valor 9
function exemplo1() {
  for (const i = 0; i <= numeros.length - 1; i++) {
    const num = numeros[i];
    if (num === 9) {
      console.log(num);
    }
  }
}

// Mostra o primeiro valor do array
function exemplo2() {
  console.log(numeros[0]);
}

// Soma os números das pontas do array
function exemplo3() {
  for (const i = 0; i <= numeros.length - 1; i++) {
    for (const j = numeros.length - 1; j >= 0; j--) {
      console.log(numeros[i] + numeros[j]);
    }
  }
}
```
<h3>➤ exemplo1() → O(n) 🆗</h3> 
<ul>
  <li>Precisa percorrer o array inteiro.</li>
  <li>Com 10 valores → 10 iterações.</li>
  <li>Se o array tivesse 1000 valores → 1000 iterações.</li>
  <li> Com 1000 valores, demoraria 16 minutos</li>
  <li>É algo proporcionalmente linear.</li>
</ul>

<h3>➤ exemplo2() → O(1) ⚡</h3>
<ul>
  <li>Não percorre o array. Acessa diretamente o valor no índice 0.</li>
  <li>Com 1 milhão de valores → 1 iteração.</li>
  <li> Com 1000 valores, demoraria 1 segundo</li>
  <li>É algo constante.</li>
</ul>

<h3>➤ exemplo3() → O(n²) 🐌</h3> 
<ul>
  <li>Possui dois loops aninhados. Para cada valor do primeiro loop, todo o array é percorrido novamente.</li>
  <li>Com 10 itens: 10 × 10 = 100 iterações.</li>
  <li>Com 100 itens: 100 × 100 = 10.000 iterações.</li>
  <li> Com 1000 valores, demoraria 11 dias, 13 horas e 46 segundos</li>
  <li>É algo quadrático (cresce muito rápido).</li>
</ul>

## ⏬ Outros exemplos
Além dos três citados anteriormente, também possuímos as notações:

<h3>➤ O(log n) </h3>

```
OBS: 
- Logaritmo é quantas vezes um número precisa ser multiplicado para alcançar X.
- Em Big O sempre utilizamos o log na base 2 (binário)
```

<ul>
  <li>Exemplo: Busca Binária, Busca Binária em "árovres balanceadas", filas de prioridade etc...</li>
  <li> Com 1024 valores, levaria 10 iterações</li>
  <li>Cresce logaritmicamente</li>
</ul>

<h3>➤ O(n log n) </h3>
<ul>
  <li>Exemplo: Merge sort, Quick sort, Heap sort</li>
  <li>Com 1024 valores, levaria 10.240 iterações</li>
  <li>Uma busca binária também pode vir a ser O(n log n) em casos onde o array não está ordenado. Ai, seria necessário percorrer todo o array (n) para ordena-lo e depois executar a busca (log n)</li>
</ul>

<h3>➤ O(n!) </h3>
<ul>
  <li>Exemplo: Geração de permutas</li>
  <li>São algoritmos extremamente raros OU ENTÃO foram mal escritos.</li>
  <li>Com apenas 10 valores, 3.628.800 iterações (fatorial de 10) seriam necessárias </li>
</ul>

## ☝🤓 Como saber disso melhora nosso código do dia a dia?

A principal dica é: SAIBA O QUE VOCÊ ESTÁ ESCREVENDO.

Em javascript, utilizamos muito estes métodos:
```js 
.map()
.filter()
.forEach()
.find()
.findIndex()
.reduce()
for (const of)
```

Estes métodos percorrem o array INTEIRO. 

Quando estamos lidando com arrays, temos que tomar muito cuidado para não estragar nossa escalabilidade. Não sabemos o dia de amanhã, então evitem códigos como:
```js
// 1) 
let tags;
for (const user of users){
  for(const tag of user.tags){
    tags.push(tag)
  }
}
```
