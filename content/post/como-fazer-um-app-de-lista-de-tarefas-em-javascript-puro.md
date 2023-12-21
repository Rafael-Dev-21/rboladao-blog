---
author: Victor Rafael Pereira Alves
date: 2022-07-04T03:00:00.000Z
comments: true
audio: []
title: "Como fazer um app de lista de tarefas em Javascript puro "
tags:
  - Tutorial
  - TODO list
  - Javascript
video: []
image: /uploads/task.svg
categories:
  - tutoriais/javascript
description: Nesse artigo veremos como fazer um TODO list em Javascript
---
Um dos primeiros programas gráficos que costumam ser recomendados para iniciantes de qualquer linguagem ou framework é a TODO list (lit. lista de tarefas), que é bem simples de fazer. Nesse artigo eu vou mostrar como fazer um em Javascript puro.

![Ícone de tarefa](/uploads/task.svg "Vamos lá")

## Html

Primeiro vamos criar a estrutura html do app. Precisamos de uma lista vazia onde vamos adicionar os arquivos, um input para escrever texto e um botão para adicionar o item à lista.

```html
<!DOCTYPE html>
<html>
  <head>
    <meta charset="utf-8">
    <meta name="viewport" content="width=device-width, initial-scale=1">
    <title>Lista de Tarefas</title>
    <link rel="stylesheet" href="css/style.css">
  </head>
  <body>
    <div id="TODO">
      <h2>Tarefas</h2>
      <input type="text" id="TODO-text">
      <button id="TODO-add">adicionar</button>
      <ul id="TODO-list"></ul>
    </div>
    <script src="js/app.js"></script>
  </body>
</html>
```

## Javascript

Antes de aplicar estilos ao app, vamos fazer o script, função antes da forma. Nosso app é bem simples, temos o input, um botão e uma lista, se clicarmos no botão e o input for válido, adicionamos um item na lista. Temos quatro ações aqui:

1. Clicar no botão adciona um item a lista.
2. Clicar no item marca ou desmarca ele.
3. Cada item tem dois botões: Editar e Deletar.

Primeiro, nós pegamos os elementos com `document.querySelector`:

```js
const input = document.querySelector("#TODO-text");
const adicionar = document.querySelector("#TODO-add");
const lista = document.querySelector("#TODO-list");
```

Então, adicionamos um evento de clique no botão, e checamos se o input é válido.

```js
adicionar.addEventListener("click", () => {
  if(input.value) {
    // resto do código
  }
});
```

Vamos criar um elemento `li`, um `p` e dois elementos `span` dentro do evento, junto com um `input` e um `boolean`.

```js
let item = document.createElement("li");
let texto = document.createElement("span");
let btnEditar = document.createElement("span");
let btnDeletar = document.createElement("span");
let inputEditar = document.createElement("input");

let boolean editar = true;
```

O valor do texto deve ser igual ao conteúdo do nosso input, e quando clicamos nele nós adicionamos ou removemos a classe `checked`. Por fim, colocamos ele no item.

```js
texto.textContent = input.value;
texto.addEventListener("click", () => {
  texto.classList.toggleClass("checked");
});
item.appendChild(texto);
```

Agora vamos ao botão editar, quando clicamos nele, nós copiamos o valor do texto para o input editável e trocamos eles de lugar, se clicamos uma segunda vez nós fazemos o oposto.

```js
btnEditar.textContent = "Editar";
btnEditar.addEventListener("click", () => {
  if(editar) {
    inputEditar.value = texto.textContent;
    li.replaceChild(inputEditar, texto);
    editar = false;
  } else {
    texto.textContent = inputEditar.value;
    li.replaceChild(texto, inputEditar);
    editar = true;
  }
});
item.appendChild(btnEditar);
```

Agora, só falta uma função: deletar. Para isso nós vamos simplesmente remover o item da lista. E com isso falta apenas adicionar o item a lista e esvaziar o input.

```js
btnDeletar.textContent = "Deletar";
btnDeletar.addEventListener("click", () => {
  lista.removeChild(item);
});
item.appendChild(btnDeletar);

lista.appendChild(item);

input.value = "";
```

## CSS

O css é a parte mais complicada para algumas pessoas, então vou deixar ele inteiro abaixo.

```css
#TODO {
  width: min(600px, 100% - 2rem);
}

#TODO-list {
  display: flex;
  flex-direction: column;
  gap: 10px;
  list-style: none;
}

#TODO-list li {
  border: solid black 1px;
  border-radius: 10px;
  padding: 5px;
}

#TODO-list span:not(:last-child) {
  margin-right: 10px;
}

#TODO-list p, #TODO-list input {
  margin: 20px;
}
  
.checked {
  color: red;
  text-decoration: line-through;
}
```

Veja o resultado final:

<https://codepen.io/rafael-dev-21/pen/ExEVwmx>

Deixem um comentário com sugestões de apps.