# Texto e tom

A interface fala português do Brasil, de forma direta e cordial, como um colega que sabe o que está fazendo. Sem jargão técnico, sem juridiquês na interface, sem exclamação.

## Princípios

| Princípio | Como fica |
| --- | --- |
| Diga o que acontece | "Agendar no YouTube", não "Confirmar" |
| Fale com a pessoa | "Você revisou o conteúdo?", não "O usuário deve revisar o conteúdo" |
| Curto | Uma ideia por frase. Botão com até 3 palavras quando possível |
| Concreto | "Os vídeos que já estão no canal continuam lá", não "Esta ação pode ter efeitos" |
| Sem culpa | "Não conseguimos salvar", não "Você digitou errado" |

## Rótulos

- **Botão começa pelo verbo** no infinitivo: "Criar artigo", "Agendar no YouTube", "Tentar de novo", "Excluir 3".
- **Caixa de frase**: só a primeira letra e nomes próprios em maiúscula ("Criar conteúdo", "Vídeo longo", "YouTube").
- O botão que confirma repete o verbo do botão que abriu a confirmação. Abriu com "Excluir", confirma com "Excluir".
- Cancelar dentro de confirmação é "Voltar"; em modal de formulário é "Cancelar".
- Campo tem rótulo visível. Placeholder é exemplo ("Ex.: direito do consumidor"), nunca o rótulo.
- Mesma ação, mesma palavra em todo o app: "Excluir" (nunca "Apagar" ou "Remover" para a mesma coisa), "Agendar", "Publicar", "Arquivar".
- Contagem no rótulo quando a ação atinge vários itens: "Excluir 3", "Tentar de novo (2)".
- Plural certo: "1 selecionado", "3 selecionados". Nunca "1 item(s)".

## Títulos

- Sem ponto final em título de página, seção, card, modal ou coluna.
- Título de confirmação é pergunta: "Excluir 3 cards?", "Você revisou o conteúdo e os vídeos?".
- Título com 20 palavras ou mais vira título curto + subtítulo.

## Mensagens

| Tipo | Título | Descrição |
| --- | --- | --- |
| Sucesso (toast) | O que aconteceu, no passado: "3 cards excluídos" | Só se houver detalhe útil |
| Sucesso parcial | "3 cards excluídos, 1 com erro" | "Tente excluir o restante de novo." |
| Erro de carregamento | "Erro ao carregar o painel" | O que fazer: "Confira a conexão e tente de novo." |
| Erro de ação | "Não foi possível agendar" | Motivo real (mensagem do servidor) + próximo passo |
| Erro de campo | Não tem título | O que corrigir: "Use até 100 caracteres." |
| Vazio | "Nenhum artigo ainda" | Como começar: "Crie o primeiro a partir de uma palavra-chave." |
| Carregando | | "Carregando vídeos…" (com reticências de um caractere) |
| Confirmação | Pergunta | Consequência concreta e quando |

Erro sempre diz **o que houve** e **o que fazer**. Mensagem técnica do servidor aparece quando ajuda a pessoa a resolver; código de erro cru (`500`, `ECONNRESET`) nunca aparece sozinho.

## Pontuação

| Regra | Errado | Certo |
| --- | --- | --- |
| Sem travessão (U+2014) nem meia-risca (U+2013) em texto visível | "Agendado &mdash; amanhã" | "Agendado · amanhã" ou "Agendado para amanhã" |
| Intervalo com "a" | "150&ndash;300 palavras" | "150 a 300 palavras" |
| Separador inline com `·` | "Vídeo longo - 1,2 GB - 32 min" | "Vídeo longo · 1,2 GB · 32 min" |
| Valor vazio com `-` ou célula vazia | "&mdash;" | "-" |
| Sem vírgula antes de "e" | "Revise o texto&#44; e agende" | "Revise o texto e agende" |
| Sem vírgula antes de "nem" | "Não publica&#44; nem agenda" | "Não publica nem agenda" |
| Título sem ponto final | "Vídeos publicados." | "Vídeos publicados" |
| Sem exclamação | "Salvo com sucesso!" | "Alterações salvas" |
| Reticências de um caractere | "Carregando..." | "Carregando…" |
| Número no padrão brasileiro | "1.2 GB", "10:30 AM" | "1,2 GB", "10h30" |
| Data no padrão brasileiro | "11/17/2026" | "17/11/2026" ou "17 de nov." |

Quando a frase pedir vírgula antes de "e", reescreva: divida em duas frases, use ponto e vírgula ou tire a vírgula.

## Antes de publicar

Procure no diff da tela:

```bash
rg -n '\x{2014}|\x{2013}|,\x20(e|nem)\x20' src/
```

Todo resultado em texto visível é corrigido antes do merge.

## Exemplos completos

**Confirmação de exclusão**

- Título: "Excluir 3 cards?"
- Descrição: "Os cards saem do quadro. Os vídeos que já estão no canal continuam lá."
- Botões: "Voltar" · "Excluir"

**Confirmação de publicação**

- Título: "Você revisou o conteúdo e os vídeos?"
- Descrição: "O vídeo fica público no YouTube em 17/11 às 10h."
- Botões: "Voltar" · "Agendar no YouTube"

**Card com falha**

- "Falhou ao enviar. O arquivo passou de 2 GB." + botão "Tentar de novo"
