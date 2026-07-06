# Aula 13 — Desenvolvimento Mobile Híbrido e Multiplataforma

!!! info "Objetivos da aula"
    - Diferenciar apps **nativos, híbridos e PWA**.
    - Entender o modelo **multiplataforma**.
    - Transformar uma web app em **PWA** instalável.

## Três caminhos para um app

=== "Nativo"
    Escrito na linguagem da plataforma (Kotlin/Java no Android, Swift no iOS). **Máximo desempenho** e acesso total ao hardware, mas exige **um código por plataforma**.

=== "Híbrido / Multiplataforma"
    **Um código** roda em Android e iOS. Ferramentas como **Ionic/Capacitor** e **React Native** empacotam tecnologias web (ou próximas) em um app instalável.

=== "PWA"
    Um **site** que se comporta como app: instalável, funciona offline e envia notificações. Sem loja de apps. É o caminho mais próximo do que já sabemos.

| Critério | Nativo | Híbrido | PWA |
| :------- | :----- | :------ | :-- |
| Base de código | Uma por SO | Única | Única |
| Loja de apps | Sim | Sim | Não (opcional) |
| Acesso a hardware | Total | Bom (plugins) | Limitado |
| Custo/velocidade | Alto | Médio | Baixo |

!!! info "Escreva uma vez, rode em todo lugar"
    A promessa do multiplataforma é reduzir custo e tempo mantendo **uma** base de código. O preço costuma ser um pequeno teto de desempenho e dependência de plugins para recursos nativos.

## Do site ao app: Capacitor

O **Capacitor** (do time do Ionic) empacota seu HTML/CSS/JS em um projeto nativo:

```bash
npm install @capacitor/core @capacitor/cli
npx cap init
npx cap add android
npx cap open android   # abre no Android Studio
```

## PWA: o meio mais acessível

Uma PWA precisa de dois ingredientes:

**1. Manifesto** (`manifest.json`) — descreve o app:

```json
{
  "name": "Minha PWA",
  "short_name": "PWA",
  "start_url": "/",
  "display": "standalone",
  "background_color": "#ffffff",
  "theme_color": "#7c4dff",
  "icons": [{ "src": "icon-192.png", "sizes": "192x192", "type": "image/png" }]
}
```

**2. Service Worker** — um script que roda em segundo plano e permite cache/offline:

```js
// sw.js
self.addEventListener("install", (e) => {
  e.waitUntil(
    caches.open("v1").then((cache) => cache.addAll(["/", "/index.html", "/style.css"]))
  );
});

self.addEventListener("fetch", (e) => {
  e.respondWith(caches.match(e.request).then((r) => r || fetch(e.request)));
});
```

Registrando no HTML:

```js
if ("serviceWorker" in navigator) {
  navigator.serviceWorker.register("/sw.js");
}
```

!!! warning "HTTPS obrigatório"
    Service Workers só funcionam em **HTTPS** (ou `localhost`). O GitHub Pages já serve por HTTPS — perfeito para testar.

## Exercícios

??? abstract "Exercício 1 — Comparação fundamentada"
    Escolha um app que você usa e argumente qual abordagem (nativo, híbrido ou PWA) faria mais sentido para ele, considerando custo, hardware e público.

??? abstract "Exercício 2 — Manifesto"
    Crie um `manifest.json` para uma página sua, com nome, ícones e cores. Linke-o no `<head>` e verifique na aba *Application* do DevTools se o app é "instalável".

??? abstract "Exercício 3 — Offline básico"
    Adicione um Service Worker que faça cache dos arquivos principais. Teste desligando a rede no DevTools e recarregando a página.

!!! tip "Próxima Parada"
    Mudamos de assunto: começa nossa jornada por **jogos digitais**, e ela começa com... matemática! Antes, resolva a 👉 [**Lista 13**](../listas/13-lista.md).
