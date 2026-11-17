# Princípios

O Bocchi Content é uma ferramenta de trabalho diário: a equipe pesquisa, escreve, revisa, agenda e publica conteúdo jurídico nela. O desenho serve a essa rotina. Cinco princípios decidem os casos que o guia não cobre.

## 1. A tela faz a pessoa pensar menos

Uma ação principal por área, poucas escolhas visíveis, o próximo passo sempre à vista. Se a tela pede que a pessoa lembre de algo de outra tela, ela está errada.

- Um botão primário (`bg-primary`) por bloco. As outras ações são `ghost`, `secondary` ou `outline`.
- Grupos com até 7 itens. Acima disso: agrupar, buscar ou paginar.
- Tarefa em andamento mostra o que falta ("3 de 5", barra de progresso).

## 2. Calma por padrão, destaque com motivo

Fundo quase branco (`#FAFAFC`), cards brancos sem borda, um único azul de ação (`#2E5BAD`). Cor forte aparece só onde há decisão ou alerta.

- Hierarquia por sombra e fundo, não por borda.
- Cor de status sempre em par: fundo claro do tom + texto escuro do tom.
- Um elemento diferente por tela. Se dois gritam, nenhum é lembrado.

## 3. Um padrão, muitas telas

Toda página usa o mesmo cabeçalho, o mesmo recuo, os mesmos controles. Todo kanban tem as mesmas funções. Quem aprende uma tela já sabe usar a próxima.

- Componente novo só quando nenhum existente resolve. Variação vai para o componente, não para a tela.
- Mesma palavra para a mesma ação em todo o app ("Excluir", nunca "Apagar" em uma tela e "Remover" em outra).

## 4. Medidas fechadas

Nada de "um espaço bonito". Todo valor sai da escala: espaço em múltiplos de 4 px, três raios, duas sombras, sete estilos de texto, controles de 40 e 44 px. Valor fora da escala é dívida.

## 5. Funciona no celular e no teclado

Mobile first: a tela nasce em 390 px e cresce. Todo elemento clicável tem 44 px no toque, foco visível e funciona sem mouse. Quem digita com IME (acentos compostos, teclados asiáticos) não perde texto por um Enter antecipado.

## Como decidir um caso novo

1. Existe componente ou padrão no app que resolve? Use.
2. Existe em outra tela algo parecido? Copie a estrutura e as medidas.
3. Não existe? Proponha com valores da escala, desenhe desktop e celular, passe pela [checklist](10-qa-checklist.md) e registre no [CHANGELOG](../CHANGELOG.md).
