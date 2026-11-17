# Ícones

## Biblioteca e traço

- [lucide](https://lucide.dev) (`lucide-react` no React), **sempre** com `strokeWidth={1.8}`.
- Marcas de rede social (Instagram, YouTube, TikTok, Facebook, WordPress) podem usar o logo oficial da marca em gráficos e legendas; em botões e menus, o ícone lucide equivalente.
- Sem quadrado, círculo ou pílula decorativa em volta do ícone. O ícone fica direto sobre a superfície.

```tsx
import { CalendarClock } from "lucide-react";

<CalendarClock className="size-4" strokeWidth={1.8} aria-hidden />
```

## Tamanhos

| Contexto | Tamanho | Classe |
| --- | --- | --- |
| Botão, campo, chip, item de menu, meta de card | 16 | `size-4` (o botão já força `[&_svg]:size-4`) |
| Menu lateral | 18 | `size-[18px]` |
| Título de página | 24 | `size-6 text-primary` |
| Estado vazio, erro, área de soltar arquivo | 28 a 32 | `size-7`, `size-8` |
| Carregando dentro de botão | 16 | `Loader2 size-4 animate-spin` |
| Carregando em capa de card | 24 | `Loader2 size-6 animate-spin` |

## Cor

| Situação | Cor |
| --- | --- |
| Junto de texto | Mesma cor do texto (`currentColor`) |
| Título de página | `text-primary` |
| Menu lateral | `text-primary/70`, ativo `text-primary` |
| Estado vazio | `text-label-tertiary` |
| Erro | `text-status-error-text` |
| Separador de breadcrumb | `text-label-tertiary` |

## Ícones convencionais

Use o ícone que a pessoa já conhece de outros sistemas.

| Ação | Ícone lucide |
| --- | --- |
| Fechar, limpar | `X` |
| Buscar | `Search` |
| Mais ações | `MoreHorizontal` |
| Excluir | `Trash2` |
| Carregando | `Loader2` |
| Erro | `CircleAlert` ou `TriangleAlert` |
| Sucesso | `CheckCircle2` |
| Marcado | `Check` |
| Abrir lista | `ChevronDown` |
| Avançar na trilha | `ChevronRight` |
| Recolher coluna | `ChevronsLeft` |
| Agendado | `Clock3` |
| Mover | `LayoutGrid` |
| Início | `Home` |
| Bloqueado | `Lock` |

## Acessibilidade

- Ícone ao lado de texto: `aria-hidden`.
- Botão só de ícone: `aria-label` com o verbo ("Excluir vídeo") e `title` com o mesmo texto.
- Ícone que carrega informação sozinho (status sem palavra): `role="img"` e `aria-label`. Prefira sempre juntar a palavra.

## Errado e certo

| Errado | Certo |
| --- | --- |
| `strokeWidth={2}` (padrão do lucide) | `strokeWidth={1.8}` |
| Ícone dentro de `div` cinza `rounded-lg p-2` | Ícone direto, 24 a 32 px |
| Ícone de 20 px dentro de botão | 16 px |
| Ícone diferente do menu no título da página | O mesmo ícone do item de menu |
