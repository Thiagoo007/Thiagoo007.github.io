# Radar de Licitações

Painel de editais de licitação pública que confere se cada edital respeita o **prazo mínimo de divulgação do art. 55 da Lei nº 14.133/2021**, contado em dias úteis com feriados nacionais.

Projeto de portfólio de **Thiago Moreira** · [github.com/Thiagoo007](https://github.com/Thiagoo007)

## Funcionalidades

- 60 editais fictícios e realistas (órgão, UASG, número 90xxx/AAAA, modalidade, critério, UF, valor, divulgação, abertura), gerados por semente determinística a partir da data de hoje
- Enquadramento automático no art. 55 (I a/b, II a/b/c/d, IV) e no art. 75, §3º, para dispensa eletrônica
- Cálculo da data mínima de abertura em dias úteis (art. 183: exclui o dia do começo), com feriados nacionais e móveis calculados pela Páscoa
- Classificação de cada edital como **regular**, **no limite** (folga ≤ 2 dias úteis) ou **irregular**
- Indicadores: editais no filtro, valor somado, aberturas em 7 dias e prazos irregulares
- Filtros por busca textual, UF, modalidade, faixa de valor e situação, além de ordenação por coluna
- Gráfico em SVG por UF ou modalidade (quantidade ou valor), com destaque dos irregulares
- Agenda das aberturas dos próximos 14 dias
- Detalhe do edital com o passo a passo do cálculo e o calendário do prazo
- Exportação em CSV (copiar e baixar)
- Suíte de 21 autotestes das regras no navegador (aba **Testes** ou `?test`)

## Decisões técnicas

- **Um arquivo, sem build e sem dependências**: HTML, CSS e JavaScript puro. Só as fontes vêm do Google Fonts.
- **Regras separadas da interface**: os módulos `Calendario` e `Regras` são funções puras sobre datas ISO (`AAAA-MM-DD`) em UTC, sem efeito de fuso horário. A UI só consome o resultado, então a lógica poderia ir para um backend sem mudar.
- **Dados reproduzíveis**: PRNG `mulberry32` com semente fixa. A mesma data gera sempre os mesmos editais, e há um teste que garante isso.
- **Acessibilidade**: abas com `role="tab"`, drawer com foco gerenciado e Esc para fechar, foco visível e respeito a `prefers-reduced-motion`.

## Como rodar

Abra o `index.html` no navegador. Para publicar, basta servir a pasta como site estático (GitHub Pages, por exemplo).

> Os dados são fictícios. O projeto não substitui análise jurídica: feriados locais, republicações e prazos específicos de cada edital exigem avaliação do agente de contratação.
