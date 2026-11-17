# Changelog

Formato baseado em [Keep a Changelog](https://keepachangelog.com/pt-BR/1.1.0/). Versionamento [semântico](https://semver.org/lang/pt-BR/): correção de texto ou valor = patch, token ou regra nova = minor, token removido ou renomeado = major.

## [1.0.0] · 17/11/2026

### Adicionado

- Guia completo em `docs/`: princípios, cores, tipografia, espaços, raios e sombras, ícones, componentes, layout, texto e tom, acessibilidade e checklist de QA com as 7 leis de UX.
- Tokens extraídos do Bocchi Content em três formatos com os mesmos valores: `tokens/tokens.css` (variáveis CSS), `tokens/tailwind-theme.css` (bloco `@theme inline` do Tailwind v4) e `tokens/tokens.json` (formato W3C Design Tokens).
- Cores de status, etapas do kanban, tipos de conteúdo e plataformas.
- Lista de pendências de contraste conhecidas no app, com a correção recomendada para aplicações novas.
- Correções em relação ao app, já nos tokens: texto de sucesso `#1D7633` e teal `#0B7570` (5:1 ou mais sobre o fundo a 10%) e foco com contorno de 2 px em `primary`.
- Canais RGB (`--nome-rgb`) para as cores de status, etapa e plataforma, que permitem modificador de opacidade no Tailwind v3.
