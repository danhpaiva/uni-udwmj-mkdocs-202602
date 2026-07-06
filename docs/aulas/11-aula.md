# Aula 11 — Ferramentas: Git, npm e Pré-processadores CSS

!!! info "Objetivos da aula"
    - Versionar código com **Git** e **GitHub**.
    - Gerenciar dependências com **npm**.
    - Escrever CSS melhor com **Sass**.

## Git: a máquina do tempo do seu código

**Git** registra o histórico do projeto em *commits*, permitindo voltar no tempo, trabalhar em paralelo (*branches*) e colaborar. **GitHub** hospeda esse repositório na nuvem.

```mermaid
graph LR
    W[Working Directory] -->|git add| S[Staging]
    S -->|git commit| L[Repositório local]
    L -->|git push| R[GitHub]
```

Fluxo básico:

```bash
git init                       # inicia o repositório
git add .                      # prepara os arquivos
git commit -m "feat: primeira versão"
git branch -M main
git remote add origin URL_DO_REPO
git push -u origin main
```

| Comando | O que faz |
| :------ | :-------- |
| `git status` | Mostra o que mudou |
| `git log --oneline` | Histórico de commits |
| `git pull` | Traz mudanças do remoto |
| `git clone URL` | Copia um repositório |

!!! tip "Commits que fazem sentido"
    Escreva mensagens no padrão **Conventional Commits**: `feat:`, `fix:`, `docs:`, `style:`, `refactor:`. Ex.: `fix: corrige cálculo da média`.

!!! warning "Nunca versione o node_modules"
    Crie um arquivo **`.gitignore`** com `node_modules/` dentro. Essa pasta é enorme e reconstruída via `npm install`.

## npm: o gerenciador de pacotes

O **npm** vem com o **Node.js** e gerencia bibliotecas do projeto.

```bash
npm init -y                 # cria o package.json
npm install sass            # instala uma dependência
npm install -D vite         # dependência de desenvolvimento
npm run dev                 # roda um script definido
```

O `package.json` guarda as dependências e os *scripts*:

```json
{
  "scripts": {
    "dev": "vite",
    "build:css": "sass scss/main.scss css/style.css"
  },
  "dependencies": { "sass": "^1.77.0" }
}
```

## Pré-processadores CSS: Sass

**Sass** adiciona superpoderes ao CSS (variáveis, aninhamento, mixins) que são **compilados** para CSS comum que o navegador entende.

=== "SCSS (com Sass)"
    ```scss
    $cor-primaria: #7c4dff;

    .card {
      background: $cor-primaria;
      &:hover { opacity: 0.9; }   // aninhamento
      .titulo { font-weight: bold; }
    }
    ```

=== "CSS gerado"
    ```css
    .card { background: #7c4dff; }
    .card:hover { opacity: 0.9; }
    .card .titulo { font-weight: bold; }
    ```

!!! info "CSS moderno também tem variáveis"
    Hoje o próprio CSS tem `--variaveis` (custom properties). Sass ainda brilha por **aninhamento, mixins e funções**, úteis em projetos grandes.

Compilando:

```bash
npm install -D sass
npx sass scss/main.scss css/style.css --watch
```

## Exercícios

??? abstract "Exercício 1 — Repositório do zero"
    Crie um projeto local, inicie o Git, faça 3 commits com mensagens no padrão Conventional Commits e publique no GitHub. Inclua um `.gitignore`.

??? abstract "Exercício 2 — Sass na prática"
    Reescreva um CSS existente seu em SCSS usando **variáveis** (cores, espaçamentos) e **aninhamento**. Compile para CSS e conecte no HTML.

??? abstract "Exercício 3 — Scripts no package.json"
    Configure um `package.json` com um script `build:css` que compile seu Sass. Rode com `npm run build:css` e descreva o resultado.

!!! tip "Próxima Parada"
    Com o ambiente profissional montado, vamos conhecer os **frameworks frontend** e a ideia de componentes. Antes, resolva a 👉 [**Lista 11**](../listas/11-lista.md).
