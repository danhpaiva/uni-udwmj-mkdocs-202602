# Aula 08 — JavaScript: Fundamentos da Linguagem

!!! info "Objetivos da aula"
    - Declarar **variáveis** e usar **tipos** de dados.
    - Escrever **condições**, **laços** e **funções**.
    - Trabalhar com **arrays** e **objetos**.

## Onde o JavaScript roda

```html
<!-- No fim do <body>, para o HTML já existir -->
<script src="app.js"></script>
```

!!! tip "Console é seu amigo"
    Abra o **DevTools** (`F12`), aba *Console*. Tudo que você imprimir com `console.log()` aparece ali. É onde você vai depurar o tempo todo.

## Variáveis e tipos

```js
let idade = 20;          // pode mudar
const nome = "Ana";      // constante
let ativo = true;        // boolean

console.log(typeof idade); // "number"
```

| Tipo | Exemplo |
| :--- | :------ |
| `number` | `42`, `3.14` |
| `string` | `"texto"`, `'aspas'` |
| `boolean` | `true`, `false` |
| `array` | `[1, 2, 3]` |
| `object` | `{ nome: "Ana" }` |
| `undefined` / `null` | ausência de valor |

!!! danger "Use const por padrão"
    Prefira `const`; troque para `let` só quando precisar reatribuir. **Evite `var`** — ela tem regras de escopo confusas e legadas.

## Condições

```js
const nota = 7;

if (nota >= 9) {
  console.log("Excelente");
} else if (nota >= 6) {
  console.log("Aprovado");
} else {
  console.log("Recuperação");
}
```

!!! warning "== x ==="
    Sempre use `===` (compara valor **e** tipo). `==` faz conversões traiçoeiras: `0 == ""` é `true`, mas `0 === ""` é `false`.

## Laços

=== "for"
    ```js
    for (let i = 0; i < 5; i++) {
      console.log(i);
    }
    ```

=== "for...of"
    ```js
    const cores = ["azul", "verde"];
    for (const cor of cores) {
      console.log(cor);
    }
    ```

=== "while"
    ```js
    let n = 3;
    while (n > 0) {
      console.log(n);
      n--;
    }
    ```

## Funções

```js
// declaração
function soma(a, b) {
  return a + b;
}

// arrow function
const dobro = (x) => x * 2;

console.log(soma(2, 3)); // 5
console.log(dobro(10));  // 20
```

## Arrays e objetos

```js
const alunos = ["Ana", "Bruno", "Carla"];
alunos.push("Diego");          // adiciona
console.log(alunos.length);    // 4

const carro = { marca: "Fiat", ano: 2022 };
console.log(carro.marca);      // "Fiat"
carro.cor = "prata";           // adiciona propriedade
```

Métodos de array que você usará muito:

```js
const numeros = [1, 2, 3, 4];
const pares = numeros.filter((n) => n % 2 === 0); // [2, 4]
const emDobro = numeros.map((n) => n * 2);        // [2, 4, 6, 8]
```

## Exercícios

??? abstract "Exercício 1 — Calculadora de média"
    Escreva uma função que receba um array de notas e retorne a média, imprimindo "Aprovado" (≥ 6) ou "Reprovado".

??? abstract "Exercício 2 — FizzBuzz"
    De 1 a 30, imprima o número; se múltiplo de 3, "Fizz"; de 5, "Buzz"; de ambos, "FizzBuzz".

??? abstract "Exercício 3 — Catálogo"
    Crie um array de objetos `produto` (nome, preço). Use `filter` para listar os que custam menos de R$ 50 e `map` para gerar um array só com os nomes.

!!! tip "Próxima Parada"
    Você sabe a lógica — agora vamos **mexer na página de verdade** manipulando o DOM. Antes, resolva a 👉 [**Lista 08**](../listas/08-lista.md).
