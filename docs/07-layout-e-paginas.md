# Layout e páginas

## Estrutura do app

```
┌────────────┬─────────────────────────────────────────────┐
│            │ Barra superior · 52 px (trilha + busca)      │
│  Barra     ├─────────────────────────────────────────────┤
│  lateral   │ Corpo da página (rola por dentro)            │
│  256 / 64  │   Cabeçalho de página                        │
│            │   Blocos, a 24 px um do outro                │
└────────────┴─────────────────────────────────────────────┘
```

A janela não rola: `html`, `body` e a raiz do app têm `height: 100vh; overflow: hidden`. Quem rola é o corpo da página (ou a coluna, nos quadros).

## Barra lateral

| Parte | Valor |
| --- | --- |
| Largura | 256 expandida (`w-64`), 64 recolhida (`w-16`) |
| Fundo | `--sidebar-background` (`#F6F6F9`) com brilho azul difuso no canto superior (`.bc-sidebar` em `tokens.css`) e linha interna de 0,5 px à direita |
| Topo | 52 px com o logo (36 px) e o botão de recolher |
| Abaixo do topo | Seletor de site e botão primário "Criar conteúdo" em largura total |
| Rótulo de grupo | 12/16 500 `text-label-tertiary`, `px-2.5 pt-3.5 pb-1` |
| Item | 32 px (`h-8`), `rounded-lg`, ícone 18 em `text-primary/70`, texto 14/20 |
| Item ativo | `bg-primary/10 text-primary font-medium` |
| Item em hover | `bg-fill-subtle` |
| Recolhida | Botões 44 × 44 no celular e 40 × 40 a partir de 768 px, só com ícone, `aria-label` e `title`; ponto de 6 px no canto para "em breve" (atenção) e "novo" (sucesso) |

A barra nasce recolhida em telas abaixo de 768 px e lembra a escolha da pessoa. Item novo de menu define o ícone que aparece no título da página daquela rota: o ícone do menu e o do título são sempre o mesmo.

## Barra superior

| Parte | Valor |
| --- | --- |
| Caixa | 52 px, `bg-card/80 backdrop-blur-xl`, `border-b border-border`, recuo `pl-4 sm:pl-8` |
| Trilha (breadcrumb) | 13/18: ícone `Home` 16, separador `ChevronRight` 16 em `text-label-tertiary`, item final `text-foreground font-medium`, anteriores `text-muted-foreground` com hover `text-foreground` |
| Busca global | À direita, pill 44/40 em `bg-fill-subtle`, 220 px no desktop, atalho de teclado em chip `rounded-lg` |

## Corpo da página

```tsx
<div className="min-w-0 min-h-0 flex-1 overflow-y-auto p-4 sm:px-8 sm:pt-7 sm:pb-8">
  <div className="mx-auto flex w-full max-w-[1600px] flex-col gap-6">
    {/* cabeçalho + blocos */}
  </div>
</div>
```

| Parte | Valor |
| --- | --- |
| Recuo | 16 no celular; a partir de 640 px: 28 topo, 32 laterais e base |
| Largura máxima | 1600, centralizado |
| Entre blocos | 24 (`gap-6`) |
| Variante quadro | Sem rolagem externa (`overflow-hidden`, `h-full`): a coluna rola por dentro |

CSS puro:

```css
.page-body { flex: 1; min-width: 0; min-height: 0; overflow-y: auto; padding: var(--page-padding-mobile); }
.page-body > .page-inner { max-width: var(--content-max-width); margin: 0 auto; display: flex; flex-direction: column; gap: var(--section-gap); }
@media (min-width: 640px) {
  .page-body { padding: var(--page-padding-top) var(--page-padding-x) var(--page-padding-x); }
}
```

## Cabeçalho de página

Toda página usa o mesmo cabeçalho. Só login, recuperação de senha, seleção de site e página 404 têm título fora dele.

| Parte | Valor |
| --- | --- |
| Ícone | 24 × 24, traço 1.8, `text-primary`, `mt-0.5`, 10 px até o título (`gap-2.5`) |
| Título | `h1` 22/28 500 (20/26 no celular), `text-foreground` |
| Meta | Na mesma linha de base do título, 13/18 `text-muted-foreground` (ex.: "12 itens") |
| Subtítulo | Abaixo, `mt-1`, 13/18 `text-muted-foreground` |
| Ações | À direita, centradas na linha do título, `gap-2`; quebram para baixo no celular |

```tsx
<header className="flex flex-wrap items-center justify-between gap-3">
  <div className="flex min-w-0 items-start gap-2.5">
    <Newspaper className="mt-0.5 size-6 shrink-0 text-primary" strokeWidth={1.8} aria-hidden />
    <div className="min-w-0">
      <div className="flex flex-wrap items-baseline gap-x-2 gap-y-0.5">
        <h1 className="text-[20px] font-medium leading-[26px] sm:text-[22px] sm:leading-[28px]">Artigos</h1>
        <span className="text-[13px] leading-[18px] text-muted-foreground">12 em produção</span>
      </div>
      <p className="mt-1 text-[13px] leading-[18px] text-muted-foreground">Da palavra-chave à publicação no site</p>
    </div>
  </div>
  <div className="flex min-w-0 flex-wrap items-center justify-end gap-2">
    <Button>Criar artigo</Button>
  </div>
</header>
```

## Grades

As combinações `sm:grid-cols-2`, `md:grid-cols-2`, `lg:grid-cols-3` e `xl:grid-cols-4` são as mais usadas no app. Lista de cards em `minmax(280px)` e painel lateral de 360 são a recomendação para telas novas.

| Uso | Desktop | Celular | Tailwind |
| --- | --- | --- | --- |
| Cards de resumo (indicadores) | 3 ou 4 colunas | 1 coluna (2 a partir de 640) | `grid gap-4 sm:grid-cols-2 lg:grid-cols-3 xl:grid-cols-4` |
| Lista de cards | Colunas de 280 px mínimo | 1 coluna | `grid gap-4 grid-cols-[repeat(auto-fill,minmax(280px,1fr))]` |
| Formulário | 2 colunas de campo | 1 coluna | `grid gap-4 md:grid-cols-2` |
| Conteúdo + painel lateral | Conteúdo flexível + painel de 360 | Painel abaixo | `grid gap-6 lg:grid-cols-[1fr_360px]` |
| Kanban | Colunas de 300 a 16 px | Segmentado + coluna única | `flex gap-4 overflow-x-auto` |

## Breakpoints

Padrão do Tailwind, sem breakpoint próprio.

| Nome | A partir de | O que muda |
| --- | --- | --- |
| (base) | 0 | Celular: recuo 16, controles 44, kanban em segmentado, barra lateral recolhida |
| `sm` | 640 px | Recuo da página 28/32, título 22/28, colunas do kanban aparecem, toast vai para baixo à direita |
| `md` | 768 px | Controles passam a 40, barra lateral pode ficar expandida, formulário em 2 colunas |
| `lg` | 1024 px | Painel lateral ao lado do conteúdo, 3 colunas de cards |
| `xl` | 1280 px | 4 colunas de cards |
| `2xl` | 1536 px | Só a largura máxima de 1600 entra em ação |

## Regras para celular

- Desenhe primeiro em **390 px** de largura. Desktop é ampliação.
- **Sem rolagem horizontal da página** em nenhuma largura a partir de 320 px. Rolagem horizontal só dentro de um componente que a pessoa entende como faixa (quadro kanban no desktop, barra em massa, tabela larga em contêiner próprio com `overflow-x-auto`).
- Use `min-w-0` em filhos de flex e grid que têm texto, senão o texto empurra a largura.
- Controles com 44 px de altura e alvos de toque com 44 × 44.
- Ações do cabeçalho quebram linha (`flex-wrap`), nunca encolhem abaixo de 44.
- Modal no celular ocupa a largura com 16 px de margem; rodapé fixo com a ação principal à direita.
- Hover não existe no toque: o que aparece só no hover (checkbox do card, ações de linha) fica sempre visível com `[@media(hover:none)]:opacity-100`.
- Toast aparece no topo.
- Conferir em 390 × 844 e 1440 × 900 antes de publicar.
