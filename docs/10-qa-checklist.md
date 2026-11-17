# Checklist de QA

Toda tela nova ou alterada passa por esta lista antes de ir para produção. Confira no ambiente de homologação (não só na máquina local), em **1440 × 900** e **390 × 844**. Item que não passa é corrigido ou vira exceção escrita no pedido de revisão, com motivo.

## 1. Tokens e medidas

- [ ] Cores só por token. Nenhum hex em `className`, nenhuma paleta crua do Tailwind (`amber-500`, `slate-700`).
- [ ] Fonte Ubuntu, pesos 400 e 500. Nenhum `font-bold`, `font-light`, 600 ou 700.
- [ ] Nenhum texto abaixo de 12 px. Tamanhos só da escala (12, 13, 14, 16, 20, 22).
- [ ] Raios só `rounded-full`, `rounded-lg`, `rounded-xl`.
- [ ] Controles com 40 px no desktop e 44 px no celular (botão, campo, select, abas, segmentado, busca).
- [ ] Campos da mesma coluna com a mesma borda esquerda, borda direita e altura. Controles da mesma linha alinhados no mesmo eixo (tolerância 1 px).
- [ ] Espaços em múltiplos de 4. Recuo da página 16 no celular, 28/32 no desktop.
- [ ] Cards claros sem borda. Nenhum card com sombra dentro de card com sombra.
- [ ] Ícones lucide com traço 1.8, no tamanho da tabela, sem contêiner decorativo.

## 2. Estrutura

- [ ] Página usa o cabeçalho padrão: ícone do menu, título, meta ou subtítulo, ações à direita.
- [ ] Um `h1` por página.
- [ ] Uma ação principal (`bg-primary`) por área.
- [ ] Ação que publica ou exclui abre confirmação com pergunta no título e consequência na descrição.
- [ ] Kanban tem busca, contador, seleção por card, selecionar todos da coluna, barra em massa, recolher coluna e versão de celular com segmentado.

## 3. Estados

- [ ] Hover, foco, ativo e indisponível em cada controle novo.
- [ ] Carregando: spinner com texto, skeleton na forma do conteúdo, ou botão com `Loader2` e rótulo mantido.
- [ ] Vazio: ícone, título, frase de como começar, botão que resolve.
- [ ] Erro: o que houve, o que fazer, botão "Tentar de novo". Erro de campo abaixo do campo.
- [ ] Texto muito longo testado (título de 120 caracteres, nome sem espaço): trunca sem quebrar o layout.
- [ ] Lista com 0, 1 e 200 itens conferida.

## 4. Celular

- [ ] Sem rolagem horizontal da página em 390 px e em 320 px.
- [ ] Alvos de toque com 44 × 44.
- [ ] O que aparece só no hover fica visível no toque.
- [ ] Ações do cabeçalho quebram linha sem encolher.

## 5. Acessibilidade

- [ ] Contraste conferido com axe (`color-contrast`) nas duas larguras.
- [ ] Tudo acessível por teclado, na ordem visual, com foco visível: contorno de 2 px em `primary` afastado 2 px (branco sobre fundo escuro).
- [ ] Modal prende o foco, fecha com Esc e devolve o foco.
- [ ] Botão só de ícone com `aria-label` e `title`.
- [ ] Campo com `<label>`; erro com `aria-invalid` e `aria-describedby`.
- [ ] Enter que envia ignora composição de IME (`isComposing`).
- [ ] Área de texto cresce com o conteúdo (`field-sizing: content`).
- [ ] Estado nunca comunicado só por cor.
- [ ] Movimento respeita `prefers-reduced-motion`.

## 6. Texto

- [ ] Botões começam pelo verbo, em caixa de frase.
- [ ] Títulos sem ponto final.
- [ ] Sem travessão nem meia-risca. Sem vírgula antes de "e" ou "nem". Sem exclamação.
- [ ] Números, datas e horas no padrão brasileiro.
- [ ] Mesma palavra para a mesma ação que no resto do app.

Busca automática nos arquivos alterados:

```bash
rg -n '\x{2014}|\x{2013}|,\x20(e|nem)\x20' src/
rg -n 'text-\[1[01]px\]|rounded-md|rounded-2xl|font-bold|font-light|strokeWidth=\{2' src/
rg -n 'className="[^"]*#[0-9a-fA-F]{3,6}' src/
```

## 7. As 7 leis de UX

Responda SIM, NÃO ou EXCEÇÃO para cada uma, com a evidência em uma linha (medida, contagem ou print).

| # | Lei | O que diz | Regra de QA | Como medir |
| --- | --- | --- | --- | --- |
| 1 | Fitts | Alvo grande e perto é clicado mais rápido | Ação principal com 40 px no desktop e 44 no celular, perto de onde a tarefa termina (fim do formulário, rodapé do modal), não isolada na ponta oposta | `getBoundingClientRect()` do botão principal; distância vertical até o último campo de até 120 px |
| 2 | Hick | Mais opções, decisão mais lenta | Uma ação primária por bloco; menus e grupos com até 7 itens visíveis; opção padrão marcada quando a escolha é óbvia | Contar botões `bg-primary` visíveis por bloco (máximo 1) e itens por menu (máximo 7) |
| 3 | Zeigarnik | Tarefa incompleta puxa o retorno | Fluxo de mais de uma etapa mostra o que falta; tarefa começada aparece de novo no topo ("Continuar revisão") | Existe `role="progressbar"`, passos numerados ou texto "X de N" |
| 4 | Jakob | A pessoa espera o padrão que já conhece | Logo no topo à esquerda, conta no canto, busca com lupa, X para fechar, trilha no topo, menu à esquerda | Conferência visual contra a tabela de [ícones convencionais](05-icones.md#ícones-convencionais) |
| 5 | Gradiente de meta | Perto do fim, mais motivação | Progresso visível em fluxo com etapas; começa acima de zero quando algo já foi feito | Barra ou passos presentes e com valor inicial correto |
| 6 | Von Restorff | O diferente é lembrado | Um único destaque por tela (o CTA em cor cheia); badges e alertas não competem com ele | Contar elementos com fundo `primary` cheio no viewport (máximo 1 por bloco) |
| 7 | Miller | Memória curta guarda 7 ± 2 itens | Grupos de até 7; formulário longo dividido em etapas ou seções; informação necessária fica visível | Contar filhos diretos de listas e grupos de opções (alerta entre 8 e 9, falha acima) |

Resumo na ordem: ação principal perto e grande, menos escolhas, tarefa à vista, padrões conhecidos, progresso visível, um destaque só, uma decisão por vez.

Modelo para colar no pedido de revisão:

```markdown
| Lei | Resultado | Evidência |
| --- | --- | --- |
| Fitts | SIM | Botão "Agendar" 40 px desktop, 44 celular, 16 px abaixo do último campo |
| Hick | SIM | 1 primário no rodapé; menu do card com 5 itens |
| Zeigarnik | SIM | "2 de 4 etapas" no topo do modal |
| Jakob | SIM | X no canto do modal, lupa na busca |
| Gradiente de meta | EXCEÇÃO | Tela de etapa única |
| Von Restorff | SIM | Só o botão "Agendar" em azul cheio |
| Miller | SIM | 6 campos em 2 seções |
```
