# Aula 03 — Layouts Modernos: Flexbox e Grid

!!! info "Objetivos da aula"
    - Alinhar e distribuir elementos com **Flexbox** (1 dimensão).
    - Montar layouts bidimensionais com **CSS Grid**.
    - Saber **quando** usar cada um.

## Flexbox vs Grid: o resumo

=== "Flexbox — 1 dimensão"
    Organiza itens em **uma linha OU uma coluna**. Ideal para: barras de navegação, botões alinhados, centralização.

    ```css
    .barra {
      display: flex;
      justify-content: space-between; /* eixo principal */
      align-items: center;           /* eixo cruzado */
      gap: 16px;
    }
    ```

=== "Grid — 2 dimensões"
    Organiza itens em **linhas E colunas** ao mesmo tempo. Ideal para: layout da página, galerias, dashboards.

    ```css
    .galeria {
      display: grid;
      grid-template-columns: repeat(3, 1fr);
      gap: 16px;
    }
    ```

## Anatomia do Flexbox

```mermaid
graph LR
    A[flex-container] --> B[item 1]
    A --> C[item 2]
    A --> D[item 3]
```

Propriedades no **container**:

| Propriedade | O que controla |
| :---------- | :------------- |
| `flex-direction` | `row` (padrão) ou `column` |
| `justify-content` | Alinhamento no eixo principal |
| `align-items` | Alinhamento no eixo cruzado |
| `flex-wrap` | Se os itens quebram linha |
| `gap` | Espaço entre itens |

!!! tip "Centralizar de vez"
    O clássico "centralizar tudo" em uma linha:
    ```css
    .centro {
      display: flex;
      justify-content: center;
      align-items: center;
      min-height: 100vh;
    }
    ```

## CSS Grid na prática

```css
.layout {
  display: grid;
  grid-template-columns: 200px 1fr;   /* menu fixo + conteúdo fluido */
  grid-template-rows: auto 1fr auto;  /* header, main, footer */
  grid-template-areas:
    "header header"
    "menu   main"
    "footer footer";
  min-height: 100vh;
}
header { grid-area: header; }
nav    { grid-area: menu; }
main   { grid-area: main; }
footer { grid-area: footer; }
```

!!! info "A unidade `fr`"
    `fr` = *fraction*. `1fr 2fr` divide o espaço livre em 3 partes: a segunda coluna fica com o dobro da primeira. É a base dos layouts fluidos.

## Grid responsivo sem media query

```css
.cards {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(240px, 1fr));
  gap: 16px;
}
```

Os cards se reorganizam sozinhos conforme a largura da tela — um aperitivo da próxima aula.

## Exercícios

??? abstract "Exercício 1 — Barra de navegação"
    Crie um `<nav>` com o logo à esquerda e 3 links à direita, tudo alinhado verticalmente ao centro, usando **apenas Flexbox**.

??? abstract "Exercício 2 — Layout Holy Grail"
    Reproduza com **Grid** um layout com `header`, `footer`, um menu lateral e a área de conteúdo, usando `grid-template-areas`.

??? abstract "Exercício 3 — Galeria adaptável"
    Monte uma galeria de 6 imagens que exiba 3 colunas no desktop e se reduza automaticamente em telas menores, usando `auto-fit` + `minmax`.

!!! tip "Próxima Parada"
    Seus layouts já se adaptam um pouco — na próxima aula assumimos o controle total com **Mobile First** e media queries. Antes, encare a 👉 [**Lista 03**](../listas/03-lista.md).
