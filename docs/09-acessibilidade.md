# Acessibilidade

Meta: **WCAG 2.2 nível AA** em toda tela. A ferramenta é usada o dia inteiro, em monitor e no celular, por pessoas com visão, mãos e teclados diferentes.

## Contraste

Mínimos: texto normal **4,5:1**. Texto grande (a partir de 24 px em peso regular, ou 18,66 px em negrito) **3:1**. Componentes não textuais (borda de campo, ícone que informa, contorno de foco) **3:1**. Como a escala da casa vai só até 22 px em 500, **todo texto da interface usa 4,5:1**.

Pares medidos com os tokens deste guia:

| Texto | Fundo | Contraste | Uso permitido |
| --- | --- | --- | --- |
| `foreground` `#1E1E20` | branco | 16,6:1 | Todo texto |
| `foreground` | `background` `#FAFAFC` | 16,0:1 | Todo texto |
| `foreground/80` `#4B4B4D` | branco | 8,7:1 | Botão `ghost`, segmento inativo |
| `muted-foreground` `#6E6E72` | branco | 5,1:1 | Texto secundário |
| `muted-foreground` | `background` | 4,9:1 | Texto secundário |
| branco | `primary` `#2E5BAD` | 6,5:1 | Botão primário |
| branco | `primary-strong` `#1D4795` | 8,8:1 | Hover do primário |
| `primary` | `primary/10` | 5,6:1 | Botão `tinted`, badge |
| `primary` | `accent` `#E8EDF7` | 5,6:1 | Item em foco no menu |
| branco | `destructive` `#D60B00` | 5,4:1 | Botão de perigo, toast de erro |
| branco | `foreground` | 16,6:1 | Barra em massa |
| branco a 70% | `foreground` | 8,7:1 | Dica da barra em massa |
| `#D70015` | erro a 10% | 4,7:1 | Chip de erro |
| `#C93400` | atenção a 10% | 4,9:1 | Chip de atenção |
| `#0040DD` | informação a 10% | 6,6:1 | Chip de informação |
| `#8944AB` | em andamento a 10% | 5,3:1 | Chip de em andamento |
| `#1D7633` (`status-success-text`) | sucesso a 10% | 5,2:1 | Chip de sucesso |
| `#0B7570` (`status-teal-text`) | teal a 10% | 5,1:1 | Chip teal |
| `foreground/80` | `fill-subtle` sobre `background` | 8,0:1 | Texto dentro de coluna de kanban e trilho |
| contorno `primary` | branco / `background` | 6,5:1 / 6,3:1 | Contorno de foco |
| `label-tertiary` | branco | 2,05:1 | **Só** placeholder e ícone decorativo |
| borda `input` `#D1D1D6` | branco | 1,5:1 | Borda de campo (ver pendências) |

Ferramenta: regra `color-contrast` do axe (extensão axe DevTools ou `@axe-core/playwright`) em toda tela nova, desktop e celular.

## Pendências conhecidas

Medidas no Bocchi Content em 17/11/2026. Aplicações novas já devem nascer com a correção; o app corrige aos poucos.

| Item | Medida | Correção para aplicação nova |
| --- | --- | --- |
| Texto de sucesso `#248A3D` sobre sucesso a 10% | 4,0:1 | Token `status-success-text` já é `#1D7633` (5,2:1) |
| Texto teal `#0C817B` sobre teal a 10% | 4,3:1 | Token `status-teal-text` já é `#0B7570` (5,1:1) |
| Texto 13 px `muted-foreground` sobre `fill-subtle` (dica de coluna de kanban) | 4,4:1 | `text-foreground/80` (8,0:1) em texto sobre `fill-subtle` |
| Foco só com halo `ring-primary/20` | 1,35:1 | Contorno de 2 px em `primary` afastado 2 px, padrão deste guia (6,5:1) |
| Iniciais brancas em avatar amber, emerald, cyan, teal, orange e fuchsia 500 | 2,2:1 a 3,5:1 | Tons 700 (amber 700 5,0:1; emerald 700 5,5:1; cyan 700 5,4:1; teal 700 5,5:1; orange 700 5,2:1; fuchsia 700 6,3:1) e rose 600 (4,7:1) |
| Borda de campo `input` sobre branco | 1,5:1 | O rótulo visível e o fundo branco sobre `background` identificam o campo; em campo sobre branco puro, borda `#8E8E93` (3,3:1) |
| Toast some em 1 s | Pouco para ler | Toast de sucesso com 4 s; erro fica até a pessoa fechar |

## Foco

- Todo elemento clicável tem foco visível: contorno de 2 px em `primary` afastado 2 px (`focus-visible:outline-2 focus-visible:outline-offset-2 focus-visible:outline-primary`). No Tailwind v3, acrescente `focus-visible:outline` para definir o estilo sólido.
- O halo `focus-visible:ring-4 focus-visible:ring-primary/20` é opcional, por cima do contorno. Sozinho ele dá 1,35:1 e não vale como foco.
- Campo e select também trocam a borda para `border-primary`.
- Sobre fundo escuro (barra em massa), o contorno é branco: `focus-visible:outline-white`.
- `<button>` montado à mão fora da biblioteca de componentes repete as mesmas classes. Prefira `Button variant="ghost" size="icon"`.
- Nunca `outline: none` sem substituto.
- Ordem de foco segue a ordem visual. Nada de `tabindex` positivo.
- Modal prende o foco, começa no primeiro campo (ou na ação principal) e devolve o foco ao botão que o abriu ao fechar.

## Teclado

| Tecla | Comportamento |
| --- | --- |
| Tab / Shift+Tab | Navega entre controles |
| Enter / Espaço | Aciona botão, marca checkbox, alterna switch |
| Esc | Fecha modal, menu, popover; limpa a busca em foco |
| Setas | Navegam dentro de menu, select, abas e segmentado |
| Atalho da busca global | Mostrado no próprio campo |

Arrastar e soltar (kanban) sempre tem alternativa sem arraste: "Mover para" no menu do card e na barra em massa.

## Enter seguro para IME

Quem digita com IME (acentuação composta, teclados chinês, japonês, coreano) confirma a composição com Enter. O Enter que envia, salva ou adiciona tag **ignora** esse momento:

```tsx
onKeyDown={(event) => {
  if (event.nativeEvent.isComposing) return;
  if (event.key === "Enter") {
    event.preventDefault();
    submit();
  }
}}
```

Em JavaScript puro: `if (event.isComposing || event.keyCode === 229) return;`.

## Formulários

- Todo campo tem `<label>` visível ligado por `htmlFor`/`id`.
- Erro: `aria-invalid="true"` no campo e a mensagem ligada por `aria-describedby`.
- Campo obrigatório marcado no rótulo ("Título (obrigatório)") e com `required`.
- `autocomplete` correto em login e dados pessoais.
- Área de texto cresce com o conteúdo (`field-sizing: content`) para a pessoa ver tudo o que escreveu.

## Leitores de tela

- Botão só de ícone: `aria-label` com verbo e objeto ("Excluir vídeo") e `title` igual.
- Ícone ao lado de texto: `aria-hidden`.
- Segmentado e filtros: `role="group"` com `aria-label`, cada botão com `aria-pressed`.
- Barra de progresso: `role="progressbar"` com `aria-valuenow`, `aria-valuemin`, `aria-valuemax` e `aria-label`.
- Contador e mensagens que mudam sozinhas: `aria-live="polite"`.
- Avatar: `aria-label` com o nome completo.
- Checkbox "selecionar todos" com `aria-label="Selecionar todos em Revisão"`.

## Alvos de toque

44 × 44 no celular para todo alvo. Controles menores no visual (checkbox 16, recolher coluna 24, botão de 32) ganham área de toque pelo rótulo clicável, pela linha inteira ou por pseudo-elemento:

```css
.alvo-pequeno { position: relative; }
.alvo-pequeno::after { content: ""; position: absolute; inset: 50% auto auto 50%;
  width: 44px; height: 44px; transform: translate(-50%, -50%); }
```

## Movimento

- Transições curtas: 150 a 200 ms. Nada de animação em loop na interface, a não ser indicador de carregamento.
- Respeite a preferência do sistema:

```css
@media (prefers-reduced-motion: reduce) {
  *, *::before, *::after { animation-duration: 0.01ms !important; transition-duration: 0.01ms !important; }
}
```

Em Tailwind: `motion-safe:animate-in` e `motion-reduce:transition-none`.

## Idioma e zoom

- `<html lang="pt-BR">`.
- Layout aguenta zoom de 200% e texto ampliado sem cortar nem sobrepor.
- Nada de `user-scalable=no` no viewport.
