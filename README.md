# Guia de design do Bocchi Content

Padrão visual e de interação do **Bocchi Content**, a ferramenta de gestão de conteúdo da Bocchi Advogados. Este repositório existe para que toda aplicação da Bocchi (interna ou pública) siga as mesmas cores, tipografia, medidas, componentes e regras de texto.

Este guia reflete os padrões do Bocchi Content. Onde o guia corrige algo que o app ainda não segue (contraste e foco), vale o guia para aplicações novas e a diferença fica registrada em [Pendências conhecidas](docs/09-acessibilidade.md#pendências-conhecidas).

Versão 1.0.0 · 17/11/2026 · mantido pela Virtus Design.

## Como usar

### Para quem desenha

1. Leia [Princípios](docs/01-principios.md) e as [Regras rápidas](#regras-rápidas) abaixo.
2. Monte a biblioteca do seu editor de design a partir de [`tokens/tokens.json`](tokens/tokens.json). O arquivo segue o formato W3C Design Tokens; a importação em ferramentas e plugins pode exigir ajuste.
3. Desenhe com as medidas de [Espaços, raios e sombras](docs/04-espacos-raios-sombras.md) e os estados de [Componentes](docs/06-componentes.md). Toda tela entra com versão desktop (1440 px) e celular (390 px).
4. Antes de entregar, passe pela [Checklist de QA](docs/10-qa-checklist.md).

### Como trazer para o seu projeto

Escolha uma das três formas. Em todas, o que o projeto usa é a pasta `tokens/`.

| Forma | Como | Quando |
| --- | --- | --- |
| Copiar | Copie a pasta `tokens/` para o projeto (ex.: `src/styles/tokens/`) e anote a versão do guia no commit | Projeto pequeno, atualização manual |
| Submódulo git | `git submodule add <endereço-deste-repositório> design` e importe `design/tokens/*.css`; atualize com `git submodule update --remote` | Vários projetos que precisam seguir a mesma versão |
| Download | Baixe o pacote da versão (ZIP da tag `v1.0.0`) e extraia `tokens/` | Sem acesso ao git no ambiente do projeto |

Ao atualizar, leia o [CHANGELOG](CHANGELOG.md): versão major pode renomear ou remover token.

### Para quem codifica

O Bocchi Content usa React, Tailwind CSS e componentes no padrão shadcn/ui (Radix). Os tokens servem para qualquer stack.

**Tailwind v4**

```css
@import "tailwindcss";
@import "./tokens/tokens.css";
@import "./tokens/tailwind-theme.css";
```

Com isso `bg-primary`, `text-muted-foreground`, `shadow-hig-sm`, `rounded-xl`, `text-meta` e `bg-status-error/10` passam a existir. `rounded`, `rounded-md`, `rounded-2xl`, `font-bold` e `font-light` deixam de ser gerados de propósito (sem erro de build: a classe só fica sem efeito).

**Tailwind v3** (é a versão que o Bocchi Content usa hoje)

Importe `tokens/tokens.css` no CSS global e estenda o tema no `tailwind.config.ts`. As cores de status, etapa e plataforma são hex; para o modificador de opacidade (`bg-status-error/10`) funcionar no v3, use as variáveis de canais `--nome-rgb` com `<alpha-value>`:

```ts
theme: {
  extend: {
    fontFamily: { sans: ["Ubuntu", "-apple-system", "BlinkMacSystemFont", '"Segoe UI"', "Arial", "sans-serif"] },
    fontWeight: { semibold: "500" },
    borderRadius: { xl: "calc(var(--radius) + 6px)", lg: "var(--radius)" },
    boxShadow: { "hig-sm": "var(--shadow-hig-sm)", "hig-md": "var(--shadow-hig-md)" },
    colors: {
      primary: { DEFAULT: "hsl(var(--primary) / <alpha-value>)", foreground: "hsl(var(--primary-foreground) / <alpha-value>)", strong: "hsl(var(--primary-strong) / <alpha-value>)" },
      // translúcidas: já têm alfa próprio, não aceitam modificador de opacidade
      fill: { DEFAULT: "var(--fill)", strong: "var(--fill-strong)", subtle: "var(--fill-subtle)" },
      "label-tertiary": "var(--label-tertiary)",
      overlay: "var(--overlay)",
      // hex com canais RGB: aceitam bg-status-error/10
      status: {
        error: "rgb(var(--status-error-rgb) / <alpha-value>)",
        "error-text": "rgb(var(--status-error-text-rgb) / <alpha-value>)",
        // warning, success, info, progress, teal e neutral: mesmo padrão
      },
      stage: {
        sent: "var(--stage-sent)",
        processing: "rgb(var(--stage-processing-rgb) / <alpha-value>)",
        // review, scheduled e published: mesmo padrão
      },
      platform: {
        instagram: "rgb(var(--platform-instagram-rgb) / <alpha-value>)",
        // site, wordpress, facebook, youtube, tiktok e other: mesmo padrão
      },
      // demais cores do tema: hsl(var(--nome) / <alpha-value>)
    },
  },
}
```

**CSS puro**

```css
@import "./tokens/tokens.css";

.botao-primario {
  height: var(--control-height-touch);
  padding: 0 16px;
  border-radius: var(--radius-full);
  background: hsl(var(--primary));
  color: hsl(var(--primary-foreground));
  font: var(--font-weight-medium) var(--text-body)/var(--text-body-line-height) var(--font-sans);
}
@media (min-width: 768px) {
  .botao-primario { height: var(--control-height); }
}
```

Fonte: carregue a Ubuntu do Google Fonts só com os pesos 400 e 500.

```html
<link rel="preconnect" href="https://fonts.googleapis.com" />
<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin />
<link href="https://fonts.googleapis.com/css2?family=Ubuntu:wght@400;500&display=swap" rel="stylesheet" />
```

Ícones: [lucide](https://lucide.dev) com `strokeWidth={1.8}`.

## Índice

| Documento | Conteúdo |
| --- | --- |
| [01 · Princípios](docs/01-principios.md) | O que guia cada decisão |
| [02 · Cores](docs/02-cores.md) | Tokens, uso semântico, status, etapas, plataformas |
| [03 · Tipografia](docs/03-tipografia.md) | Família, pesos, escala, regras |
| [04 · Espaços, raios e sombras](docs/04-espacos-raios-sombras.md) | Grade de 4 px, recuos, raios, elevação |
| [05 · Ícones](docs/05-icones.md) | Biblioteca, traço, tamanhos, cor |
| [06 · Componentes](docs/06-componentes.md) | Botão, campo, select, modal, card, badge, kanban, barra em massa, avatar, segmentado, toast, estados de tela |
| [07 · Layout e páginas](docs/07-layout-e-paginas.md) | Cabeçalho, corpo, barra lateral, grades, breakpoints, celular |
| [08 · Texto e tom](docs/08-texto-e-tom.md) | Microcopy, rótulos, erros, pontuação |
| [09 · Acessibilidade](docs/09-acessibilidade.md) | Contraste, foco, teclado, IME, movimento |
| [10 · Checklist de QA](docs/10-qa-checklist.md) | O que conferir antes de publicar uma tela, com as 7 leis de UX |
| [`tokens/`](tokens/) | `tokens.css`, `tailwind-theme.css`, `tokens.json` |

## Regras rápidas

1. Fonte Ubuntu, só pesos 400 e 500. Nunca bold, light ou 600.
2. Nenhum texto abaixo de 12 px.
3. Raios só pill (`rounded-full`), 10 px (`rounded-lg`) e 16 px (`rounded-xl`).
4. Controles com 40 px no desktop e 44 px no celular (`h-11 md:h-10`): botão, campo, select, abas, segmentado, busca.
5. Ícones lucide com traço 1.8, sem quadrado ou círculo decorativo em volta.
6. Cards claros sem borda. Hierarquia por sombra (`shadow-hig-sm`, `shadow-hig-md`) e fundo.
7. Cor sempre por token. Nada de hex solto em classe nem paleta crua do Tailwind.
8. Estado se comunica por cor e palavra (ou ícone) juntos, nunca só por cor.
9. Uma ação principal por área. Ação que publica ou apaga pede confirmação.
10. Mobile first, sem rolagem horizontal da página em 390 px.
11. Foco visível em todo elemento clicável: contorno de 2 px em `primary` com afastamento de 2 px (`focus-visible:outline-2 focus-visible:outline-offset-2 focus-visible:outline-primary`).
12. Enter que envia ou confirma ignora composição de IME (`event.nativeEvent.isComposing`).
13. Textarea cresce com o conteúdo (`field-sizing: content`), com mínimo e máximo.
14. Texto sem travessão, sem vírgula antes de "e" ou "nem", título sem ponto final.
15. Toda tela passa pela checklist de QA e pelas 7 leis de UX antes de publicar.

## Escopo

O Bocchi Content só tem tema claro. Este guia não define tema escuro; uma aplicação que precise dele deve propor os valores e abrir uma nova versão do guia.

## Contribuição

- Mudança de token ou de regra entra como nova versão no [CHANGELOG](CHANGELOG.md) (semver: correção = patch, token novo = minor, token removido ou renomeado = major).
- `tokens.css`, `tailwind-theme.css` e `tokens.json` mudam juntos, com os mesmos valores.
- Commits em português com prefixo semântico (`docs:`, `feat:`, `fix:`).

## Licença

[MIT](LICENSE) · Virtus Design e Bocchi Advogados. As marcas Bocchi e Bocchi Content não estão incluídas na licença.
