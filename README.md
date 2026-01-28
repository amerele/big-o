# 📘 Entender Big O Notation vai fazer você 🫵 programar melhor!

## 🎯 Objetivo

Este documento existe para mostrar **de forma simples e prática** como entender Big O Notation ajuda você a escrever **código melhor, mais consciente e mais escalável**.


Nada de matemática pesada. A ideia aqui é **entender o comportamento do código**, não decorar fórmulas.

---

## 🤔 O que é Big O?

As funções que escrevemos podem se comportar de formas muito diferentes conforme recebem mais dados. Chamamos isso de **escalabilidade**.

A **notação Big O** descreve **como o número de operações de um algoritmo cresce** conforme o tamanho da entrada (`n`) aumenta.

Ela normalmente aparece assim:

* `O(1)`
* `O(n)`
* `O(n²)`
* `O(log n)`
* `O(n log n)`

A letra **O** vem de *Order of* (ordem de crescimento). O mais importante é o que está **dentro dos parênteses**, pois ele indica **como o algoritmo escala**, não quanto tempo ele demora em segundos.

> ⚠️ Em Big O, não comparamos tempo real de execução. Comparamos **crescimento**.

---

## 🔎 Classificando funções (com exemplos)

Vamos usar exemplos simples em JavaScript.

```js
const numeros = [0,1,2,3,4,5,6,7,8,9];

// Busca um número no array
function exemplo1() {
  for (let i = 0; i < numeros.length; i++) {
    if (numeros[i] === 9) {
      console.log(numeros[i]);
      return; // para quando encontra
    }
  }
}

// Mostra o primeiro valor do array
function exemplo2() {
  console.log(numeros[0]);
}

// Soma todos os pares possíveis
function exemplo3() {
  for (let i = 0; i < numeros.length; i++) {
    for (let j = 0; j < numeros.length; j++) {
      console.log(numeros[i] + numeros[j]);
    }
  }
}
```

### ➤ `exemplo1()` → **O(n)** 🆗

* Percorre o array até encontrar o valor.
* No **pior caso**, passa por todos os elementos.
* Com 10 valores → até 10 iterações.
* Com 1000 valores → até 1000 iterações.
* Crescimento **linear**.

> 💡 Melhor caso: `O(1)` (se o valor estiver logo no início).

---

### ➤ `exemplo2()` → **O(1)** ⚡

* Não percorre o array.
* Acessa diretamente uma posição específica.
* Com 10, 1000 ou 1 milhão de valores → **1 operação**.
* Crescimento **constante**.

---

### ➤ `exemplo3()` → **O(n²)** 🐌

* Dois loops aninhados.
* Para cada item, percorre o array inteiro novamente.
* Com 10 valores → 10 × 10 = 100 operações.
* Com 100 valores → 100 × 100 = 10.000 operações.
* Crescimento **quadrático** (escala muito rápido).

---

## ⏬ Outras notações comuns

### ➤ **O(log n)**

```md
OBS:
- Log cresce muito lentamente
- A base do log não importa em Big O
```

* Exemplo: **Busca binária**, árvores balanceadas, heaps.
* Com 1024 valores → ~10 operações.
* Extremamente eficiente.

---

### ➤ **O(n log n)**

* Exemplo: Merge Sort, Quick Sort (caso médio), Heap Sort.
* Com 1024 valores → ~10.240 operações.
* Considerado **muito bom** para algoritmos que precisam processar todos os dados.

---

### ➤ **O(n!)** ☠️

* Exemplo: geração de todas as permutações possíveis.
* Escala de forma absurda.
* Com apenas 10 valores → 3.628.800 operações.
* Normalmente indica:

  * um problema muito específico **OU**
  * um algoritmo mal pensado.

---

## 📊 Cheat sheet rápido

|    Notação | Crescimento  | Exemplo típico  |
| ---------: | ------------ | --------------- |
|       O(1) | Constante    | `arr[0]`        |
|   O(log n) | Logarítmico  | Busca binária   |
|       O(n) | Linear       | Loop simples    |
| O(n log n) | Linear + log | Sort eficiente  |
|      O(n²) | Quadrático   | Loops aninhados |
|      O(n!) | Explosivo    | Permutações     |

---

## ☝🤓 Como isso melhora seu código no dia a dia?

A principal regra é simples:

> **Saiba o que você está escrevendo.**

No JavaScript usamos muito:

```js
.map()
.filter()
.forEach()
.find()
.findIndex()
.reduce()
for (const of)
```

A maioria desses métodos percorre o array. Alguns (`find`, `findIndex`) podem parar antes, mas **map/filter/reduce percorrem tudo**.

Pergunte sempre:

* Quantas vezes esse array está sendo iterado?
* Qual o tamanho desse array hoje?
* E se ele crescer 10x? 100x?

---

## 🚨 Armadilhas comuns (evite isso)

```js
// 1) Loop dentro de loop → O(n²)
let tags = [];
for (const user of users) {
  for (const tag of user.tags) {
    tags.push(tag);
  }
}
```

```js
// 2) Requisição assíncrona dentro de loop
for (const user of users) {
  user.tags = await Tags.find({ userId: user.id });
}
```

```js
// 3) find dentro de filter → O(n²)
users.filter(
  (user) => blockedList.find((b) => b.id === user.id)
);
```

```js
// 4) Iterações encadeadas desnecessárias
users
  .map((u) => ({ ...u, active: true }))
  .filter(Boolean)
  .filter((u) => u.active);
```

---

## ✅ Checklist rápido antes de commitar

* Tem loops aninhados?
* Tem chamadas de banco/API dentro de loops?
* Estou iterando o mesmo array várias vezes?
* Posso usar `Set`, `Map` ou outra estrutura melhor?

---

## 🧠 Conclusão

Você **não precisa decorar Big O** para ser um bom dev.

Mas entender **como seu código cresce** te ajuda a:

* evitar gargalos
* escrever códigos mais sólidos
* tomar melhores decisões técnicas
