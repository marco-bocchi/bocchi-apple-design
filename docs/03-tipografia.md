# Tipografia

## Família

**Ubuntu**, carregada do Google Fonts, com fallback de sistema:

```css
font-family: Ubuntu, -apple-system, BlinkMacSystemFont, "Segoe UI", Arial, sans-serif;
```

Pesos permitidos: **400** (regular) e **500** (medium). Carregue só esses dois (`family=Ubuntu:wght@400;500`).

- `font-semibold` é remapeado para 500 no tema: a Ubuntu não tem 600 e cairia no 700.
- Nunca `font-bold`, `font-light`, `font-weight: 600` ou `700` em interface.
- Fontes de conteúdo (prévias de post, peças de rede social) seguem a identidade da peça e ficam fora da interface.

## Escala

Sete estilos. Nenhum texto abaixo de 12 px.

| Estilo | Tailwind | Tamanho/linha | Peso | Uso |
| --- | --- | --- | --- | --- |
| Título de página | `text-[20px] leading-[26px] sm:text-[22px] sm:leading-[28px] font-medium` | 20/26 celular · 22/28 desktop | 500 | Só no cabeçalho de página e no título de carregamento longo |
| Título de seção | `text-base font-medium leading-[22px]` | 16/22 | 500 | Card, coluna de kanban, modal, seção de editor |
| Corpo | `text-sm leading-5` | 14/20 | 400 | Texto corrido, campo, célula de tabela |
| Corpo forte | `text-sm font-medium leading-5` | 14/20 | 500 | Botão, rótulo, título de card de kanban, item ativo do menu |
| Meta | `text-[13px] leading-[18px]` | 13/18 | 400 | Subtítulo de página, breadcrumb, dica de coluna, segmentado, rótulo de progresso |
| Legenda | `text-xs font-medium leading-4` | 12/16 | 500 | Badge, contador, cabeçalho de tabela, chip |
| Legenda corrida | `text-xs` | 12/16 | 400 | Data em card, dica secundária |

Com o tema v4 deste repositório, os tamanhos fora do padrão Tailwind ganham nome: `text-title` (22/28), `text-title-mobile` (20/26) e `text-meta` (13/18).

Em CSS puro:

```css
.titulo-pagina {
  font-size: var(--text-title-mobile);
  line-height: var(--text-title-mobile-line-height);
  font-weight: var(--font-weight-medium);
}
@media (min-width: 640px) {
  .titulo-pagina {
    font-size: var(--text-title);
    line-height: var(--text-title-line-height);
  }
}
.meta {
  font-size: var(--text-meta);
  line-height: var(--text-meta-line-height);
  color: hsl(var(--muted-foreground));
}
```

## Regras

- **Caixa de frase** em tudo: "Criar conteúdo", não "Criar Conteúdo" nem "CRIAR CONTEÚDO". Sem caixa alta em rótulo, aba ou cabeçalho de tabela.
- **Títulos sem ponto final.**
- Um `h1` por página, dentro do cabeçalho de página. Seções usam `h2`; card e coluna usam `h2` ou `h3` conforme a hierarquia, sempre no estilo "Título de seção".
- Números que mudam (contador, porcentagem, "3 de 12") usam `tabular-nums` para não pular de largura.
- Texto longo trunca com `line-clamp-2` (título de card) ou `truncate` (nome de coluna). O texto inteiro fica em `title` ou no detalhe.
- Largura de leitura: parágrafo de ajuda até `max-w-xl` (576 px).
- Hierarquia por peso e cor (`text-foreground` vs `text-muted-foreground`), não por tamanho extra. Não crie 15, 18 ou 24 px.
- Título grande não usa `text-wrap: balance`: com largura generosa a quebra natural fica melhor.
- Título com 20 palavras ou mais vira título curto + subtítulo.

## Errado e certo

| Errado | Certo |
| --- | --- |
| `text-[11px]` para caber | `text-xs` (12) e encurtar o texto |
| `font-bold` no título do card | `font-medium` (500) |
| `text-lg` (18) para destacar | `text-base font-medium` (16/22) |
| Rótulo "STATUS" em caixa alta | "Status" |
| "Vídeos Publicados." como título | "Vídeos publicados" |
