# Espaços, raios e sombras

## Espaço

Base de 4 px (escala do Tailwind: `1` = 4 px). Os valores que se repetem no app:

| Onde | Valor | Tailwind |
| --- | --- | --- |
| Recuo da página, desktop (a partir de 640 px) | 28 topo, 32 laterais e base | `sm:px-8 sm:pt-7 sm:pb-8` |
| Recuo da página, celular | 16 | `p-4` |
| Largura máxima do conteúdo | 1600 | `max-w-[1600px] mx-auto` |
| Entre blocos da página | 24 | `gap-6` |
| Entre título e ações do cabeçalho | 12 | `gap-3` |
| Entre botões lado a lado | 8 | `gap-2` |
| Entre ícone e texto | 6 a 8 | `gap-1.5`, `gap-2` |
| Entre colunas de kanban | 16 | `gap-4` |
| Dentro da coluna de kanban | 8, cards a 12 | `p-2`, `gap-3` |
| Dentro do card de kanban | 12, linhas a 8 | `p-3 space-y-2` |
| Card de seção | 20 laterais, 16 topo, 20 base | `px-5 pt-4 pb-5` |
| Card genérico (cabeçalho e conteúdo) | 24 | `p-6` |
| Modal | 24, rodapé 24 × 14 | `p-6`, `px-6 py-3.5` |
| Entre campos de formulário | 16 | `space-y-4` ou `grid gap-4` |
| Rótulo até o campo | 8 | `grid gap-2` |

Regras:

- Só múltiplos de 4 (exceção: 2 e 6 para ajuste fino dentro de controle, como `p-0.5` no trilho do segmentado e `py-1.5` em item de menu).
- Prefira `gap` a `space-y` em wrappers de campo: a margem do `space-y` cai em filho oculto (inputs escondidos de select) e desalinha a linha.
- Campos da mesma coluna têm a mesma borda esquerda, a mesma borda direita e a mesma altura.

## Tamanhos de controle

| Controle | Celular | Desktop (a partir de 768 px) | Tailwind |
| --- | --- | --- | --- |
| Botão, campo, select, busca, abas, segmentado | 44 | 40 | `h-11 md:h-10` |
| Botão só de ícone | 44 × 44 | 40 × 40 | `size-11 md:size-10` |
| Segmento dentro do trilho | 40 | 36 | `h-10 md:h-9` |
| Botão pequeno (só em card de kanban ou linha densa) | 32 | 32 | `h-8` |
| Fechar modal, menu de card | 32 × 32 | 32 × 32 | `size-8` |
| Recolher coluna | 24 × 24 | 24 × 24 | `size-6` |
| Checkbox | 16 × 16 | 16 × 16 | `size-4` |
| Switch | 44 × 24 | 44 × 24 | `h-6 w-11` |
| Item do menu lateral | 32 | 32 | `h-8` |

Controles abaixo de 44 px no celular (checkbox, recolher coluna, botão de 32) precisam de área de toque ampliada: o rótulo clicável, a linha inteira ou um pseudo-elemento cobrindo 44 × 44.

## Raios

Três raios. Base `--radius: 0.625rem` (10 px).

| Classe | Valor | Uso |
| --- | --- | --- |
| `rounded-full` | pill | Botão, badge, chip, abas, segmentado, busca, checkbox, avatar, barra em massa, contador |
| `rounded-lg` | 10 px | Campo, select, item de menu, tooltip, aviso dentro de modal, item do menu lateral, skeleton |
| `rounded-xl` | 16 px | Card, coluna de kanban, modal, popover, dropdown, toast, tabela |

Fora do padrão: `rounded` (4), `rounded-sm` (6), `rounded-md` (8), `rounded-2xl` (20), valores da configuração Tailwind v3 do app. O tema v4 deste repositório não gera essas classes (sem erro de build: a classe fica sem efeito).

Concentricidade: elemento dentro de um contêiner com recuo usa o raio menor (card `rounded-xl` com bloco interno `rounded-lg`).

## Sombras

| Token | Valor | Uso |
| --- | --- | --- |
| `shadow-hig-sm` | `0 1px 3px rgba(0,0,0,.04), 0 1px 2px rgba(0,0,0,.06)` | Card em repouso, segmento ativo, item escolhido, bolinha do switch |
| `shadow-hig-md` | `0 4px 12px rgba(0,0,0,.05), 0 1px 3px rgba(0,0,0,.06)` | Card em hover, modal, menu, popover, toast, barra em massa |
| `shadow-segment` | `0 1px 3px rgba(0,0,0,.10), 0 0 0 .5px rgba(0,0,0,.04)` | Reserva para segmento destacado |

## Elevação e superfícies

| Nível | Superfície | Exemplo |
| --- | --- | --- |
| 0 | `bg-background` | Fundo da página |
| 0, agrupado | `bg-fill-subtle rounded-xl` | Coluna de kanban, trilho de abas |
| 1 | `bg-card shadow-hig-sm rounded-xl` | Card, tabela |
| 2 | `bg-card shadow-hig-md rounded-xl` | Card em hover, menu, popover, toast |
| 3 | `bg-card shadow-hig-md rounded-xl` + `bg-overlay` | Modal |

Regras:

- **Card claro não tem borda.** A separação vem da sombra e da diferença entre `bg-card` e `bg-background`.
- Nunca card com sombra dentro de card com sombra. O interno vira `bg-fill-subtle rounded-lg`.
- Borda (`border-border`) só em separador: linha da barra superior, topo do rodapé de modal, entre linhas de lista.

Exemplo (CSS):

```css
.card {
  background: hsl(var(--card));
  border-radius: var(--radius-xl);
  box-shadow: var(--shadow-hig-sm);
  transition: box-shadow 150ms;
}
.card:hover { box-shadow: var(--shadow-hig-md); }
```
