# Cores

Todas as cores vêm de [`tokens/tokens.css`](../tokens/tokens.css). As cores do tema seguem o padrão shadcn: a variável guarda os canais HSL e o uso é `hsl(var(--nome))`, o que permite opacidade (`hsl(var(--primary) / 0.1)` ou `bg-primary/10`).

O Bocchi Content só tem **tema claro**. Não há valores de tema escuro definidos.

Regra: cor sempre por token (`bg-primary`, `text-muted-foreground`). Hex solto em `className` (`text-[#2E5BAD]`) e paleta crua do Tailwind (`amber-700`, `emerald-500`) são dívida, não padrão.

## Tema

| Token | Classe | HSL | Hex | Uso |
| --- | --- | --- | --- | --- |
| `background` | `bg-background` | `240 20% 98.5%` | `#FAFAFC` | Fundo da área de conteúdo e do modal de detalhe |
| `foreground` | `text-foreground` | `240 3% 12%` | `#1E1E20` | Texto principal, fundo da barra de ações em massa |
| `card` | `bg-card` | `0 0% 100%` | `#FFFFFF` | Card, cabeçalho e rodapé de modal |
| `popover` | `bg-popover` | `0 0% 100%` | `#FFFFFF` | Menu, popover, lista de select |
| `muted` | `bg-muted` | `240 11% 94%` | `#EEEEF1` | Skeleton, separador de lista |
| `muted-foreground` | `text-muted-foreground` | `240 2% 44%` | `#6E6E72` | Subtítulo, meta, descrição, contador |
| `border` | `border-border` | `240 6% 90%` | `#E4E4E7` | Separador (barra superior, rodapé de modal). Nunca em card |
| `input` | `border-input` | `240 6% 83%` | `#D1D1D6` | Borda de campo, select, checkbox, botão outline |
| `primary` | `bg-primary`, `text-primary` | `219 58% 43%` | `#2E5BAD` | Azul Bocchi: ação principal, item ativo, foco, seleção |
| `primary-foreground` | `text-primary-foreground` | `0 0% 100%` | `#FFFFFF` | Texto sobre `primary` |
| `primary-strong` | `hover:bg-primary-strong` | `219 67% 35%` | `#1D4795` | Hover do botão primário |
| `secondary` | `bg-secondary` | `240 6% 93%` | `#ECECEE` | Botão neutro, trilho de progresso |
| `accent` | `bg-accent` | `219 50% 94%` | `#E8EDF7` | Item em foco em menu, select e dropdown |
| `accent-foreground` | `text-accent-foreground` | `219 58% 43%` | `#2E5BAD` | Texto sobre `accent` |
| `destructive` | `bg-destructive` | `3 100% 42%` | `#D60B00` | Botão de perigo (só dentro da confirmação), toast de erro |
| `ring` | `outline-primary` | `219 58% 43%` | `#2E5BAD` | Contorno de foco (2 px) e halo opcional |
| `sidebar-background` | `bg-sidebar` | `240 20% 97%` | `#F6F6F9` | Fundo da barra lateral |
| `sidebar-accent` | `bg-sidebar-accent` | `240 6% 92%` | `#E9E9EC` | Hover na barra lateral |

Derivados de uso frequente:

| Classe | Resultado sobre branco | Uso |
| --- | --- | --- |
| `bg-primary/10` | `#EAEFF7` | Item ativo do menu, badge padrão, botão `tinted` |
| `bg-primary/15` | primary a 15% | Hover do botão `tinted` |
| `ring-primary/20` | `#D5DEEF` | Halo opcional de 4 px por fora do contorno de foco (1,35:1, não substitui o contorno) |
| `text-foreground/80` | `#4B4B4D` | Texto de botão `ghost` e segmento inativo |

## Preenchimentos translúcidos

Funcionam sobre branco e sobre o fundo da página sem trocar de valor.

| Token | Classe | Valor | Uso |
| --- | --- | --- | --- |
| `fill-subtle` | `bg-fill-subtle` | `rgba(118, 118, 128, 0.08)` | Coluna de kanban, trilho de abas e segmentado, hover de `ghost`, rodapé de modal |
| `fill` | `bg-fill` | `rgba(118, 118, 128, 0.12)` | Chip neutro, placeholder de imagem, hover de coluna recolhida |
| `fill-strong` | `bg-fill-strong` | `rgba(118, 118, 128, 0.2)` | Hover de controle cinza |
| `label-tertiary` | `text-label-tertiary` | `rgba(60, 60, 67, 0.38)` (≈ `#B5B5B8`) | Placeholder, ícone apagado. Contraste 2,05:1: **não use em texto que precisa ser lido** |
| `overlay` | `bg-overlay backdrop-blur-sm` | `rgba(15, 23, 42, 0.4)` + blur 4 px | Atrás de modal e confirmação |

## Status

Cores de sistema para estado. Sempre em par: **fundo** com a cor base a 10% a 14% e **texto** no tom escuro. Nunca texto na cor base sobre branco.

| Papel | Base (fundo, barra, ponto) | Texto | Fundo a 10% | Exemplos |
| --- | --- | --- | --- | --- |
| Erro | `#FF3B30` | `#D70015` | `bg-status-error/10` | Falhou, crítico, esgotado |
| Atenção | `#FF9500` | `#C93400` | `bg-status-warning/10` | Na fila, em breve, aviso de capa |
| Sucesso | `#34C759` | `#1D7633` | `bg-status-success/10` | Publicado, novo, tudo em dia |
| Informação | `#007AFF` | `#0040DD` | `bg-status-info/10` | Agendado |
| Em andamento | `#AF52DE` | `#8944AB` | `bg-status-progress/10` | Publicando |
| Teal (categoria) | `#00C7BE` | `#0B7570` | `bg-status-teal/10` | Tom extra para tipo de conteúdo |
| Neutro | `#8E8E93` | `text-muted-foreground` | `bg-fill` | Cancelado, sem dado |

Exemplo (Tailwind):

```tsx
<span className="inline-flex items-center gap-1 rounded-full bg-status-error/10 px-2 py-0.5 text-xs font-medium text-status-error-text">
  <TriangleAlert className="size-4" strokeWidth={1.8} aria-hidden /> Falhou
</span>
```

Exemplo (CSS):

```css
.chip-erro {
  background: color-mix(in srgb, var(--status-error) 10%, transparent);
  color: var(--status-error-text);
}
```

### Rótulos de status

Mesmo status, mesma palavra e mesma cor em todo o app. As seis primeiras linhas são as do calendário editorial do Bocchi Content; as demais seguem a mesma lógica de cor.

| Status | Rótulo | Cor |
| --- | --- | --- |
| `scheduled` | Agendado | Informação |
| `queued` | Na fila | Atenção |
| `uploading` | Enviando | Em andamento |
| `publishing` | Publicando | Em andamento |
| `published` | Publicado | Sucesso |
| `failed` | Falhou | Erro |
| `cancelled` | Cancelado | Neutro |
| `draft` | Rascunho | Neutro |
| `ready` | Pronto | Sucesso |
| `generating` | Gerando | Em andamento |
| `pending` | Pendente | Atenção |
| `approved` | Aprovado | Sucesso |
| `rejected` | Rejeitado | Erro |
| `archived` | Arquivado | Neutro |
| `connected` / `needs_reauth` / `disconnected` | Conectado / Reconectar / Desconectado | Sucesso / Atenção / Erro |

Status sem rótulo conhecido aparece como veio do sistema; valor vazio aparece como `-`, nunca travessão.

### Tipos de conteúdo

| Tipo | Rótulo | Cor | Ícone lucide |
| --- | --- | --- | --- |
| Artigo | Artigo | Informação | `Newspaper` |
| Reel | Reel | Atenção | `Video` |
| Vídeo longo | Vídeo longo | Erro | `MonitorPlay` |
| Post de feed | Post | Sucesso | `Image` |
| Story | Story | Teal | `Instagram` |
| Carrossel | Carrossel | Em andamento | `Layers` |

## Etapas do kanban

Ponto de 10 px (`size-2.5 rounded-full`) antes do nome da coluna; 8 px na coluna recolhida.

| Etapa | Token | Valor |
| --- | --- | --- |
| Enviado | `bg-stage-sent` | `#6E6E72` a 50% |
| Em processo | `bg-stage-processing` | `#2E5BAD` |
| Revisão | `bg-stage-review` | `#F59E0B` |
| Agendado | `bg-stage-scheduled` | `#10B981` |
| Publicado | `bg-stage-published` | `#30B0C7` |

## Plataformas

Cor de marca de cada rede. Use **só** em ícone de marca, ponto de legenda ou barra de gráfico, nunca como fundo de botão ou texto corrido.

| Plataforma | Token | Valor |
| --- | --- | --- |
| Site | `platform-site` | `#2A78D6` |
| WordPress (ícone de destino) | `platform-wordpress` | `#0071A4` |
| Instagram | `platform-instagram` | `#E4405F` |
| Facebook | `platform-facebook` | `#1877F2` |
| YouTube | `platform-youtube` | `#FF0000` |
| TikTok | `platform-tiktok` | `#010101` |
| Outras | `platform-other` | `#9CA3AF` |

## Gráficos

Séries na ordem `chart-1` a `chart-5`: `#2E5BAD`, `#33C758`, `#FF9500`, `#6188D1`, `#7ECE92`. Mais de 5 séries: agrupe em "Outras". Faixas de estoque e prazo usam as cores de status (crítico erro, atenção, ok sucesso, longo informação, estendido em andamento).

## Proibido

- Cor como única forma de passar estado. Junte palavra ou ícone.
- Texto na cor base de status (`#FF9500` sobre branco tem 2,2:1).
- `label-tertiary` em texto que a pessoa precisa ler.
- Gradientes decorativos em cards e botões. O único gradiente é o brilho da barra lateral (`.bc-sidebar`).
