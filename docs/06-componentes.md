# Componentes

Os componentes do Bocchi Content seguem o padrão shadcn/ui (Radix + Tailwind) com as variantes da casa. Cada seção traz anatomia, estados e quando usar. Valores em px; `44/40` significa 44 no celular e 40 a partir de 768 px.

Estados que todo elemento clicável segue:

| Estado | Regra geral |
| --- | --- |
| Padrão | Cor da variante |
| Hover | Primário escurece para `primary-strong`; cinza e `ghost` ganham `bg-fill-subtle`; card troca `shadow-hig-sm` por `shadow-hig-md` |
| Ativo (pressionado) | `active:scale-[0.98]` no botão |
| Foco (teclado) | Contorno de 2 px em `primary` afastado 2 px: `focus-visible:outline-2 focus-visible:outline-offset-2 focus-visible:outline-primary`. Halo opcional por cima: `focus-visible:ring-4 focus-visible:ring-primary/20`. Campo também troca a borda para `border-primary`. Sobre fundo escuro, `focus-visible:outline-white` |
| Indisponível | `disabled:opacity-50 disabled:pointer-events-none` (campo: `cursor-not-allowed`) |
| Carregando | Controle fica `disabled`, ícone vira `Loader2 animate-spin`, rótulo continua |
| Selecionado | Card: `ring-2 ring-primary`. Segmento: `bg-card shadow-hig-sm` |

## Botão

Pill, texto 14/20 peso 500, `gap-2`, ícone 16, `transition-all`.

```tsx
const base =
  "inline-flex items-center justify-center gap-2 whitespace-nowrap rounded-full text-sm font-medium leading-5 " +
  "transition-all active:scale-[0.98] focus-visible:outline-2 focus-visible:outline-offset-2 focus-visible:outline-primary " +
  "disabled:pointer-events-none disabled:opacity-50 [&_svg]:size-4 [&_svg]:shrink-0";
```

### Variantes

| Variante | Padrão | Hover | Quando usar |
| --- | --- | --- | --- |
| `default` | `bg-primary text-primary-foreground` | `bg-primary-strong` | A ação principal da tela ou do modal. Uma por área |
| `tinted` | `bg-primary/10 text-primary` | `bg-primary/15` | Ação principal dentro de card de kanban, onde o sólido pesaria |
| `secondary` | `bg-secondary text-secondary-foreground` | `bg-secondary/80` | Ação neutra ao lado da principal |
| `outline` | `border border-input bg-card text-foreground` | `bg-fill-subtle` | Ação alternativa em estado vazio ou erro ("Tentar de novo") |
| `ghost` | `text-foreground/80`, sem fundo | `bg-fill-subtle text-foreground` | Cancelar, voltar, ações de barra, botão só de ícone |
| `destructive` | `bg-destructive text-destructive-foreground` | `bg-destructive/90` | Confirmar exclusão dentro da confirmação. Nunca fora dela |
| `link` | `text-primary` | sublinhado (`underline-offset-4`) | Link no meio do texto |

### Tamanhos

| Tamanho | Altura | Recuo | Uso |
| --- | --- | --- | --- |
| `default` | 44/40 (`h-11 md:h-10`) | `px-4` | Padrão de tudo |
| `lg` | 44/40 | `px-6` | CTA isolado |
| `icon` | 44 × 44 / 40 × 40 | | Só ícone; sempre com `aria-label` e `title` |
| `sm` | 32 (`h-8`), texto 12 | `px-3.5` | Só em card de kanban ou linha densa. Nunca em formulário |

### Estados

| Estado | Visual |
| --- | --- |
| Padrão | Tabela de variantes |
| Hover | Tabela de variantes |
| Ativo | Encolhe para 98% |
| Foco | Contorno de 2 px em `primary`, afastado 2 px (halo `ring-primary/20` opcional) |
| Indisponível | Opacidade 50%, sem clique. Se o motivo não for óbvio, `title` explica ("Cancele o agendamento antes de excluir") |
| Carregando | `disabled` + `Loader2` girando no lugar do ícone; o rótulo continua ("Agendar no YouTube"), nunca vira "..." |

```tsx
<Button disabled={isPending}>
  {isPending ? <Loader2 className="animate-spin" strokeWidth={1.8} /> : <CalendarClock strokeWidth={1.8} />}
  Agendar no YouTube
</Button>
```

CSS puro:

```css
.btn { display: inline-flex; align-items: center; gap: 8px; height: 44px; padding: 0 16px;
  border-radius: 9999px; font: 500 14px/20px var(--font-sans); transition: all 150ms; }
.btn:active { transform: scale(0.98); }
.btn:focus-visible { outline: 2px solid hsl(var(--primary)); outline-offset: 2px; }
/* halo opcional: box-shadow: 0 0 0 4px hsl(var(--primary) / 0.2); */
.btn:disabled { opacity: 0.5; pointer-events: none; }
.btn-primary { background: hsl(var(--primary)); color: hsl(var(--primary-foreground)); }
.btn-primary:hover { background: hsl(var(--primary-strong)); }
@media (min-width: 768px) { .btn { height: 40px; } }
```

Rótulo começa pelo verbo, em caixa de frase: "Agendar no YouTube", "Tentar de novo", "Criar conteúdo".

## Campo de texto e área de texto

| Parte | Valor |
| --- | --- |
| Caixa | `h-11 md:h-10 w-full rounded-lg border border-input bg-card px-3 py-2` |
| Texto | 14/20 `text-foreground` |
| Placeholder | `placeholder:text-label-tertiary` (exemplo, nunca instrução essencial) |
| Rótulo | `Label` 14/20 peso 500, 8 px acima do campo |
| Dica ou contador | 12/16 `text-muted-foreground`, à direita do rótulo ("45/100") |
| Área de texto | `min-h-[80px] py-2.5`, mesma borda e foco |

| Estado | Visual |
| --- | --- |
| Padrão | Borda `input` (`#D1D1D6`) |
| Hover | Sem mudança |
| Foco | `border-primary` + contorno padrão (2 px `primary`, afastado 2 px) |
| Indisponível | `opacity-50 cursor-not-allowed` |
| Erro | Borda mantida; mensagem 12/16 em `text-status-error-text` abaixo do campo, ligada por `aria-describedby`, campo com `aria-invalid="true"` |
| Carregando (busca remota) | `Loader2` 16 no lugar do ícone da direita |

```tsx
<Input
  className="h-11 md:h-10 rounded-lg border-input bg-card px-3 text-sm
             placeholder:text-label-tertiary focus-visible:border-primary
             focus-visible:outline-2 focus-visible:outline-offset-2 focus-visible:outline-primary"
/>
```

**Área de texto cresce com o conteúdo** usando `field-sizing: content`, com mínimo e máximo:

```css
textarea.auto {
  field-sizing: content;
  min-height: 80px;
  max-height: 320px;
  overflow-y: auto;
}
```

Em Tailwind: `[field-sizing:content] min-h-20 max-h-80`. Em navegador sem suporte, a área fica com a altura mínima e rola: comportamento aceitável.

**Busca**: `Input` com `Search` 16 à esquerda (`pl-9`), `X` para limpar à direita (`pr-9`) e `aria-label` descritivo ("Buscar vídeos pelo título").

Ação ligada ao campo (adicionar tag) fica **dentro** do campo, nunca um "+" solto ao lado.

## Select

| Parte | Valor |
| --- | --- |
| Gatilho | Igual ao campo: 44/40, `rounded-lg border-input bg-card px-3`, `ChevronDown` 16 a 50% de opacidade |
| Valor vazio | `text-muted-foreground` |
| Lista | `rounded-xl bg-popover shadow-hig-md p-1`, abre 4 px abaixo do gatilho, largura mínima do gatilho |
| Item | `rounded-lg py-1.5 pl-8 pr-2` 14/20; marcado com `Check` 16 à esquerda |
| Separador | `h-px bg-muted -mx-1 my-1` |

| Estado | Visual |
| --- | --- |
| Padrão | Borda `input` |
| Hover (item) | `bg-accent text-accent-foreground` |
| Foco | Gatilho `border-primary` + contorno padrão; item `bg-accent` |
| Indisponível | Gatilho `opacity-50 cursor-not-allowed`; item `opacity-50` sem clique |
| Carregando opções | Item único "Carregando…" em `text-muted-foreground` |

Quando usar: escolha única entre 6 e 15 opções. Até 5 opções curtas: segmentado. Mais de 15: select com busca.

`DropdownMenu` e menu de contexto usam a mesma lista (item `rounded-lg px-2 py-1.5`, ícone 16 com `gap-2`). Item de sair ou excluir em `text-status-error-text`.

## Checkbox e switch

| Componente | Visual | Quando usar |
| --- | --- | --- |
| Checkbox | 16 px **redondo** (`rounded-full`), `border-input bg-card`. Marcado: `bg-primary border-primary` com `Check` branco. Aceita indeterminado | Seleção (cards, linhas de tabela, "selecionar todos") |
| Switch | 44 × 24, trilho `bg-input` desligado e `bg-primary` ligado, bolinha branca 20 com `shadow-hig-sm` | Ligar e desligar configuração com efeito imediato |

Foco: contorno padrão. Indisponível: `opacity-50 cursor-not-allowed`.

## Modal (Dialog)

| Parte | Valor |
| --- | --- |
| Overlay | `bg-overlay backdrop-blur-sm`, entra com fade de 200 ms |
| Caixa | Centralizada, `w-full max-w-lg bg-card rounded-xl shadow-hig-md p-6`, entra com fade + zoom de 95% para 100% |
| Fechar | Botão 32 × 32 pill em `right-5 top-5`, `X` 16 `text-muted-foreground`, hover `bg-fill-subtle` |
| Cabeçalho | `flex flex-col gap-1.5 pb-4`, título 16/22 500, descrição 14/20 `text-muted-foreground` |
| Corpo | `space-y-4` |
| Rodapé | Cola na base: `-mx-6 -mb-6 mt-4 border-t bg-fill-subtle px-6 py-3.5 rounded-b-xl`, botões à direita com `gap-2`: `ghost` "Cancelar" + primário |

| Estado | Visual |
| --- | --- |
| Abrindo e fechando | Fade + zoom, 200 ms |
| Foco | Vai para o primeiro campo; sem campo, para o botão principal. Tab fica preso no modal. Esc fecha |
| Enviando | Botão principal em carregando, "Cancelar" indisponível, Esc e clique fora não fecham |
| Erro de envio | Aviso dentro do modal acima do rodapé (ver [Aviso](#aviso-em-linha)); o modal não fecha |

Quando usar: tarefa curta que não precisa sair da tela (editar, configurar, revisar um item). Tarefa longa ou com várias etapas vira página.

**Modal de detalhe** (revisar um item do kanban): `max-w-4xl max-h-[92vh] flex flex-col overflow-hidden bg-background p-0`; cabeçalho branco `px-6 pt-6 pb-4` com meta 12/16 500 e título 16/22 `line-clamp-2`; corpo rolando por dentro `px-4 sm:px-6 py-4`; rodapé branco fixo `px-4 sm:px-6 py-3` com a ação principal. O modal tem endereço próprio: abre pela URL do item e fecha voltando para a lista.

### Confirmação (AlertDialog)

| Parte | Valor |
| --- | --- |
| Caixa | `max-w-md rounded-xl`, sem botão de fechar |
| Cabeçalho | `px-6 pt-6 pb-5`, título 16/22 em forma de pergunta, descrição 14/20 com a consequência concreta |
| Rodapé | `border-t bg-fill-subtle px-6 py-3.5`: "Voltar" (`ghost`) + ação com o mesmo verbo do botão que abriu |

Obrigatória antes de **publicar** ou **excluir**. Excluir usa `destructive` e a contagem no título ("Excluir 3 cards?"). A descrição diz o que some e o que não some ("Os vídeos que já estão no canal continuam lá.").

## Card

| Parte | Valor |
| --- | --- |
| Caixa | `rounded-xl bg-card shadow-hig-sm`, **sem borda** |
| Cabeçalho e conteúdo | `p-6` (conteúdo `pt-0`) |
| Título | 16/22 500 |
| Descrição | 14/20 `text-muted-foreground` |
| Card de seção (dentro de modal ou página densa) | Ícone 16 + título 16/22 + subtítulo 13/18, ações à direita, `px-5 pt-4 pb-5` |

| Estado | Visual |
| --- | --- |
| Padrão | `shadow-hig-sm` |
| Hover (só card clicável) | `shadow-hig-md` |
| Foco (card clicável) | Contorno padrão |
| Selecionado | `ring-2 ring-primary` |
| Indisponível | `opacity-50`, sem hover |
| Carregando | `Skeleton` no lugar do conteúdo, mesma altura |

Card branco vai sobre `bg-background` ou `bg-fill-subtle`. Card dentro de card: o interno vira `bg-fill-subtle rounded-lg`, sem sombra.

## Badge, chip e contador

| Tipo | Classes | Uso |
| --- | --- | --- |
| Badge `default` | `rounded-full px-2.5 py-0.5 text-xs font-medium bg-primary/10 text-primary` | Categoria, destaque leve |
| Badge `secondary` | `bg-fill text-foreground` | Rótulo neutro |
| Badge `destructive` | `bg-destructive/10 text-destructive` | Problema |
| Badge `outline` | `ring-1 ring-inset ring-border text-foreground` | Rótulo discreto em fundo branco |
| Chip de status | `rounded-full px-2 py-0.5 text-xs font-medium` + fundo do tom a 10% + texto escuro do tom, ícone 16 opcional | Estado de item ([cores de status](02-cores.md#status)) |
| Contador | `rounded-full bg-card px-2 py-0.5 text-xs font-medium text-muted-foreground tabular-nums` | Quantidade em coluna, aba ou menu |
| Selo "novo", "beta", "em breve" | Pill 12/16 500, fundo claro do tom (sucesso, informação, atenção) | Item de menu ou funcionalidade |

Badge **informa, não é clicável**: sem hover, sem foco. Para filtrar, use o segmentado.

## Controle segmentado e abas

Um desenho só para abas de página, filtros e troca de vista.

| Parte | Valor |
| --- | --- |
| Trilho | `rounded-full bg-fill-subtle p-0.5 gap-0.5`, altura 44/40 |
| Segmento | `h-10 md:h-9 rounded-full px-3.5`; texto 13/18 500 no segmentado, 14/20 500 nas abas |
| Variante largura total | Segmentos iguais (`flex-1`), trilho até `max-w-[340px]` ou o `max-w` da tela |

| Estado | Visual |
| --- | --- |
| Padrão | `text-foreground/80` sem fundo |
| Hover | `text-foreground` |
| Ativo (selecionado) | `bg-card text-foreground shadow-hig-sm` |
| Foco | Contorno padrão |
| Indisponível | `opacity-50`, sem clique |

```tsx
<div role="group" aria-label="Vista" className="flex h-11 items-center gap-0.5 rounded-full bg-fill-subtle p-0.5 md:h-10">
  <button aria-pressed="true"  className="h-10 rounded-full px-3.5 text-[13px] leading-[18px] font-medium bg-card text-foreground shadow-hig-sm md:h-9">Semana</button>
  <button aria-pressed="false" className="h-10 rounded-full px-3.5 text-[13px] leading-[18px] font-medium text-foreground/80 hover:text-foreground md:h-9">Mês</button>
</div>
```

Quando usar: 2 a 5 opções curtas sempre visíveis (mês, semana ou dia; tabela ou kanban; etapa do kanban no celular). Filtro de exclusão aceita vários ligados; nada ligado = mostra tudo. Mais de 5 opções: select.

Abas com conteúdo montado o tempo todo (`forceMount`) escondem a inativa com `data-[state=inactive]:hidden`.

## Avatar

| Tipo | Valor |
| --- | --- |
| Usuário (iniciais) | Círculo `rounded-full` de 32 (`size-8`) ou 24 (`size-6`), iniciais 12/16 500 brancas, `ring-2 ring-card`, cor fixa por usuário (id módulo 8 da paleta) |
| Conta com foto | `size-10` ou `size-8`, `rounded-full object-cover`. Imagem que falha cai nas iniciais em `bg-fill-subtle text-muted-foreground` |
| Grupo | Avatares sobrepostos com `-space-x-2`, o anel branco separa um do outro |

Paleta do app: rose 500, amber 500, emerald 500, cyan 500, primary, fuchsia 500, orange 500, teal 500. Em aplicação nova use os tons 600 ou 700 (ver [Acessibilidade](09-acessibilidade.md#pendências-conhecidas)): várias cores 500 não dão contraste para letra branca de 12 px.

Sempre com `title` e `aria-label` com o nome completo. Avatar não é botão; se abrir menu de conta, o botão em volta tem 44/40 e foco visível.

## Toast

| Parte | Valor |
| --- | --- |
| Caixa | `rounded-xl p-6 pr-8 shadow-hig-md`, até 420 px |
| Posição | Canto inferior direito no desktop, topo no celular |
| Título | 14/20 500 |
| Descrição | 14/20 a 90% de opacidade |
| Variantes | `default` branco (`bg-card`); `destructive` vermelho sólido com texto branco |
| Fila | Um por vez |

Quando usar: confirmar o resultado de uma ação que a pessoa acabou de fazer ("3 cards excluídos, 1 com erro"). Não use toast para erro que pede ação: erro com ação fica na tela, ao lado do que falhou.

Texto: título diz o que aconteceu; descrição diz o detalhe ou o próximo passo ("Tente enviar de novo."). Erro mostra a mensagem do servidor quando houver.

## Aviso em linha

Bloco dentro de modal ou card: `rounded-lg px-3 py-2.5`, fundo do tom a 10%, texto 14/20 no tom escuro, ícone 16 à esquerda. Use para aviso que vale enquanto a tela estiver aberta ("A capa ainda não foi gerada").

## Tabela e lista

| Parte | Valor |
| --- | --- |
| Contêiner | `rounded-xl bg-card shadow-hig-sm` |
| Cabeçalho | `h-10 px-4` 12/16 500 `text-muted-foreground`, fixo com `sticky top-0 bg-card` |
| Célula | `px-4 py-3` 14/20 |
| Seleção | Primeira coluna com checkbox; cabeçalho com "selecionar todos" (indeterminado quando parcial) |
| Linha vazia | Uma célula com `colSpan` e "Nada aqui" centralizado, 14/20 `text-muted-foreground` |
| Valor vazio | `-` ou célula vazia, nunca travessão |
| Separador entre linhas | `border-b border-border` |

## Kanban

Todo quadro tem as mesmas funções: **busca, contador, seleção por card, selecionar todos da coluna, barra de ações em massa, recolher coluna e versão de celular com segmentado**.

### Barra do quadro

Linha acima das colunas: texto de ajuda 14/20 `text-muted-foreground` à esquerda (até `max-w-xl`); à direita busca (300 px no desktop, `min-w-[180px]` no celular), contador "3 de 12" 12/16 `tabular-nums` quando há termo de busca, botão principal. Busca filtra por título em todas as colunas; vazia esconde o contador.

### Coluna

| Parte | Valor |
| --- | --- |
| Contêiner | `section`, `w-[300px] shrink-0 rounded-xl bg-fill-subtle p-2`, altura total, rola por dentro |
| Cabeçalho | `px-1.5 py-1`, em linha com `gap-2`: checkbox "selecionar todos" (só com cards), ponto de 10 px da [cor da etapa](02-cores.md#etapas-do-kanban), nome 16/22 500 `truncate`, botão recolher 24 × 24, contador |
| Dica | 13/18 `text-muted-foreground`, alinhada ao nome (`pl-[42px]` com checkbox, `pl-[18px]` sem) |
| Lista | `flex flex-col gap-3 p-1 pt-2 overflow-y-auto` |
| Vazia | "Nada aqui" 12/16 `text-label-tertiary` |

| Estado | Visual |
| --- | --- |
| Padrão | `bg-fill-subtle` |
| Alvo de arraste | `ring-2 ring-primary` |
| Recolhida | Faixa de 48 px (`w-12`): ponto 8 px no topo, nome 16/22 na vertical, contador pill 20 px embaixo. Hover `bg-fill`. Clicar em qualquer ponto expande |
| Vazia | Nasce recolhida; arrastar sobre ela expande |

O estado recolhido é salvo por quadro.

### Card do kanban

| Parte | Valor |
| --- | --- |
| Contêiner | `article`, `group relative overflow-hidden rounded-xl bg-card shadow-hig-sm` |
| Capa | Largura total no topo (`aspect-video` para vídeo, `aspect-[8/3]` para carrossel). Sem capa: `bg-fill` com ícone 32 `text-label-tertiary` |
| Corpo | `p-3 space-y-2`: título 14/20 500 `line-clamp-2`; meta 13/18 `text-muted-foreground` com ícones 16; chips de status; barra de progresso |
| Rodapé | Ação principal `Button size="sm" variant="tinted"` à esquerda; menu `MoreHorizontal` (`ghost`, 32) à direita. Botão direito abre o mesmo menu |
| Seleção | Checkbox em `absolute left-2 top-2 z-10` |

| Estado | Visual |
| --- | --- |
| Padrão | `shadow-hig-sm`, checkbox invisível |
| Hover | `shadow-hig-md`, checkbox aparece |
| Foco | Contorno padrão no card ou na ação |
| Selecionado | `ring-2 ring-primary`, checkbox marcado |
| Modo seleção | Com algo selecionado, clicar no card alterna a seleção em vez de abrir |
| Processando | Capa com `Loader2` 24 girando; barra de progresso com rótulo 13/18 e porcentagem `tabular-nums`, trilho `h-1.5 rounded-full bg-fill`, preenchimento `bg-primary`, `role="progressbar"` |
| Falhou | Texto 12/16 `text-status-error-text` com `CircleAlert` 16 e a mensagem (`line-clamp-2`), botão "Tentar de novo" |

O checkbox fica visível sempre que houver seleção e em tela de toque (`[@media(hover:none)]:opacity-100`).

### Celular

Abaixo de 640 px as colunas somem. Entra um segmentado com as etapas e a contagem ("Revisão (2)"), uma linha "Selecionar todos em Revisão" com 44 px de altura e os cards em coluna única. A barra em massa é a mesma.

## Barra de ações em massa

Aparece quando há pelo menos um item selecionado.

| Parte | Valor |
| --- | --- |
| Posição | Flutua sobre o quadro: `absolute bottom-6 left-1/2 -translate-x-1/2 z-30`, `max-w-[calc(100%-2rem)]`, entra com fade + subida de 8 px em 200 ms |
| Caixa | `bg-foreground text-white rounded-full shadow-hig-md pl-4 pr-1.5 py-1.5`, rola na horizontal por dentro se faltar espaço |
| Ordem | "N selecionados" 14/20 500 com divisória · dica 12/16 `text-white/70` · "Mover para" (menu abre para cima) · ações do quadro · Excluir · divisória · `X` limpar seleção (32 × 32) |
| Ação | `rounded-full px-3 py-1.5` 14/20, ícone 16 com `gap-1.5`, hover `bg-white/10`; Excluir com hover `bg-destructive/90` |

| Estado | Visual |
| --- | --- |
| Padrão | Ações em branco |
| Hover | `bg-white/10` (Excluir: `bg-destructive/90`) |
| Foco | Contorno branco de 2 px (`focus-visible:outline-white`): o `primary` sobre o fundo escuro dá 2,5:1 |
| Indisponível | `opacity-50`; `title` diz o motivo |
| Carregando | Ações travadas, `Loader2` no lugar do ícone de "Mover para"; texto de progresso "Excluindo 3 de 8" |

Ação mostra quantos itens atinge ("Excluir 3", "Tentar de novo (2)"). Item que não se aplica é ignorado e o toast diz quantos. Excluir em massa sempre abre confirmação com a contagem no título.

## Estados de tela

### Carregando

| Caso | Padrão |
| --- | --- |
| Lista ou quadro | Linha centralizada: `Loader2` 16 girando + "Carregando vídeos…" 14/20 `text-muted-foreground` |
| Bloco com forma conhecida | `Skeleton` (`animate-pulse rounded-lg bg-muted`) com a mesma altura do conteúdo final |
| Processamento longo | Tela de espera com anel girando de 160 px, círculo azul com ícone branco, título 22/28 500, mensagem 13/18 que troca a cada 4 s, progresso real quando houver e opção de "deixar rodando" |
| Botão | `Loader2` no lugar do ícone, `disabled` |

### Vazio

Centro da área: ícone 32 `text-label-tertiary`, título 16/22 500, uma frase 14/20 `text-muted-foreground` dizendo como começar, botão da ação que resolve (`outline` ou primário). Coluna vazia: "Nada aqui", 12/16.

```tsx
<div className="flex flex-col items-center gap-2 py-16 text-center">
  <FileText className="size-8 text-label-tertiary" strokeWidth={1.8} aria-hidden />
  <h2 className="text-base font-medium leading-[22px]">Nenhum artigo ainda</h2>
  <p className="max-w-sm text-sm text-muted-foreground">Crie o primeiro a partir de uma palavra-chave.</p>
  <Button variant="outline" className="mt-2">Criar artigo</Button>
</div>
```

### Erro

| Caso | Padrão |
| --- | --- |
| Tela | Ícone 32 `text-status-error-text`, título 16/22 500 ("Erro ao carregar o painel"), frase 14/20 `text-muted-foreground`, `Button variant="outline"` "Tentar de novo" |
| Card | Texto 12/16 vermelho com `CircleAlert` 16 e a mensagem do servidor, botão "Tentar de novo" |
| Dentro de modal | [Aviso em linha](#aviso-em-linha) no tom de erro |
| Campo | Mensagem 12/16 abaixo do campo (ver [Campo de texto](#campo-de-texto-e-área-de-texto)) |
| Ação concluída com falha | Toast `destructive` |
