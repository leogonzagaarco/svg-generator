# SVG Brand Themer

Ferramenta web que gera variantes coloridas de um mesmo SVG para diferentes marcas, sem precisar abrir editor gráfico.

## O problema

Times de design e marketing que trabalham com um portfólio de marcas (COC, SAS, IS, Positivo, SAE, Conquista, Geekie, Ways, EI, PES, PGS, etc.) constantemente precisam do mesmo asset — uma ilustração, um ícone, um banner — adaptado para a cor de cada marca.

Fazer isso à mão significa:

- Abrir o SVG em um editor (Figma, Illustrator, Inkscape)
- Localizar e trocar a cor da marca em cada ocorrência
- Exportar arquivo por arquivo
- Repetir o processo para cada uma das N marcas

É um trabalho mecânico, repetitivo e propenso a erro (esquecer um path, trocar a cor errada, salvar com nome inconsistente).

## A solução

Uma página HTML única, sem build e sem servidor, que:

1. **Recebe** um SVG por upload ou drag-and-drop
2. **Extrai** todas as cores únicas declaradas via `fill="..."`, ordenadas por frequência
3. **Pergunta** qual delas é a cor da marca (a cor que deve variar entre marcas)
4. **Substitui** essa cor pela cor de cada marca selecionada, preservando o resto do SVG intacto
5. **Entrega** o pacote de variantes com preview e download individual ou em lote, com nomenclatura padronizada (`<base>-<marca>.svg`)

A troca usa regex casando exatamente o atributo `fill="#HEX"` da cor escolhida — outras cores do SVG (traços, fundos secundários, detalhes) não são alteradas.

## Marcas pré-cadastradas

COC, SAS, IS, Positivo, SAE, Conquista, Geekie, Ways, EI, PES e PGS. É possível adicionar marcas customizadas direto pela interface, informando nome e cor.

## Como usar

Abra [index.html](index.html) em qualquer navegador moderno. Não há dependências, instalação ou build — é um arquivo só.

1. Solte o `.svg` na área de upload
2. Clique na cor da marca presente no SVG
3. Selecione as marcas para as quais quer gerar variantes
4. (Opcional) Ajuste o nome base do arquivo
5. Clique em **Gerar variantes** e baixe individualmente ou tudo de uma vez

## Limitações conhecidas

- Só substitui cores declaradas no atributo `fill="#..."`. Cores em `style="fill:..."`, `stroke`, gradientes, ou definidas via CSS não são tocadas.
- Trabalha com hex (`#RGB` ou `#RRGGBB`). Cores em `rgb()`, `hsl()` ou nomes (`red`, `blue`) são ignoradas.
