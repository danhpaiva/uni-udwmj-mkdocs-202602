# Aula 10 — JavaScript Assíncrono e Consumo de APIs

!!! info "Objetivos da aula"
    - Entender código **síncrono x assíncrono**.
    - Usar **Promises** e **async/await**.
    - Consumir uma **API** com `fetch` e renderizar os dados.

## Síncrono x assíncrono

Código **síncrono** roda linha a linha, esperando cada uma terminar. Buscar dados na internet pode demorar — se fosse síncrono, a página **congelaria**. Por isso essas operações são **assíncronas**: o JS dispara a tarefa e segue em frente, tratando o resultado quando ele chega.

```mermaid
sequenceDiagram
    participant JS as Seu código
    participant API as API (servidor)
    JS->>API: fetch("/usuarios")
    Note over JS: continua rodando...
    API-->>JS: resposta (JSON)
    JS->>JS: atualiza a tela
```

## O que é uma API?

Uma **API** (Application Programming Interface) é um "cardápio" de dados/serviços que um servidor expõe. Você faz uma requisição HTTP a uma **URL (endpoint)** e recebe uma resposta, quase sempre em **JSON**.

```json
{ "id": 1, "nome": "Ana", "email": "ana@exemplo.com" }
```

## fetch com async/await

```js
async function buscarUsuarios() {
  try {
    const resposta = await fetch("https://jsonplaceholder.typicode.com/users");
    if (!resposta.ok) throw new Error("Erro " + resposta.status);
    const usuarios = await resposta.json();
    console.log(usuarios);
  } catch (erro) {
    console.error("Falhou:", erro.message);
  }
}

buscarUsuarios();
```

=== "async/await (recomendado)"
    ```js
    const resposta = await fetch(url);
    const dados = await resposta.json();
    ```
    Lê-se de cima para baixo, como código síncrono.

=== "then/catch (Promises)"
    ```js
    fetch(url)
      .then((r) => r.json())
      .then((dados) => console.log(dados))
      .catch((e) => console.error(e));
    ```
    A forma mais antiga; você ainda vai encontrá-la por aí.

!!! warning "Sempre trate erros"
    Redes falham. Envolva `fetch` em `try/catch` e verifique `resposta.ok` — um `404` **não** dispara erro automaticamente no `fetch`.

## Renderizando os dados na tela

```js
async function listarUsuarios() {
  const resposta = await fetch("https://jsonplaceholder.typicode.com/users");
  const usuarios = await resposta.json();
  const ul = document.querySelector("#lista");

  usuarios.forEach((u) => {
    const li = document.createElement("li");
    li.textContent = `${u.name} — ${u.email}`;
    ul.appendChild(li);
  });
}

listarUsuarios();
```

!!! tip "UX enquanto carrega"
    Mostre um "Carregando..." antes do `await` e troque pelo conteúdo quando os dados chegarem. Lembra da **heurística 1** (visibilidade do status)?

## Verbos HTTP

| Verbo | Uso |
| :---- | :-- |
| `GET` | Ler dados |
| `POST` | Criar |
| `PUT`/`PATCH` | Atualizar |
| `DELETE` | Remover |

```js
await fetch(url, {
  method: "POST",
  headers: { "Content-Type": "application/json" },
  body: JSON.stringify({ nome: "Nova" }),
});
```

## Exercícios

??? abstract "Exercício 1 — Buscador de CEP"
    Usando a API pública **ViaCEP** (`https://viacep.com.br/ws/CEP/json/`), crie um campo onde o usuário digita um CEP e a página exibe a rua, o bairro e a cidade.

??? abstract "Exercício 2 — Galeria de posts"
    Consuma `https://jsonplaceholder.typicode.com/posts`, mostre um "Carregando...", e renderize os 10 primeiros posts como cards. Trate erros de rede.

??? abstract "Exercício 3 — Clima ou piadas"
    Escolha uma API pública gratuita e monte uma página que busca e exibe algo útil (ex.: uma piada aleatória, cotação, etc.), com estado de carregamento e tratamento de erro.

!!! tip "Próxima Parada"
    Seus projetos estão crescendo — hora de organizá-los com **Git, npm e Sass**. Antes, resolva a 👉 [**Lista 10**](../listas/10-lista.md).
