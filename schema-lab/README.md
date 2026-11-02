# Schema Lab

Laboratório de migrations PostgreSQL no padrão Flyway, que roda inteiro no navegador. Você cola as migrations (`-- V1__nome.sql`, `-- V2__...`) e o app mostra:

- **Diagrama ER de cada versão.** Usa uma linha do tempo de V1 a Vn e destaca o que é novo em cada versão. As tabelas podem ser arrastadas com o mouse ou movidas com as setas.
- **Riscos de cada comando**, com severidade e a linha onde aparecem:
  - DROP TABLE e DROP COLUMN;
  - NOT NULL sem DEFAULT em tabela que já existe;
  - ALTER TYPE com reescrita da tabela (aumentar varchar é tratado como seguro);
  - CREATE INDEX sem CONCURRENTLY;
  - FK sem índice e tabela sem PK;
  - RENAME;
  - migration que expande e contrai ao mesmo tempo;
  - SET NOT NULL, FK sem NOT VALID, DEFAULT volátil, UPDATE sem WHERE e CONCURRENTLY dentro de transação.
- **Rollback sugerido** (undo `U{n}__...`) para a versão selecionada, em ordem inversa.
- **Plano de dry-run**: `BEGIN`, timeouts curtos, contagem de linhas, a migration, consultas de conferência e `ROLLBACK`.
- **Painel de testes** com 22 testes automáticos do parser e do linter, que rodam ao abrir a página.

O app abre com um exemplo de e-commerce em 6 migrations, com 8 tabelas: categorias, produtos, clientes, pedidos, itens_pedido, pagamentos, armazéns e estoque. Os riscos foram plantados de propósito.

## Decisões técnicas

O processamento segue cinco etapas: **tokenizer → parser → modelo → regras → render**.

- **Tokenizer e parser próprios, sem dependências.** Tratam strings com `''`, comentários `--` e `/* */`, dollar quoting `$$`, identificadores entre aspas e nomes com schema.
- **Modelo imutável por versão.** Cada migration guarda um retrato completo do schema, então a linha do tempo só troca o retrato exibido. O rollback é gerado comando a comando a partir do estado anterior a cada um.
- **Regras como funções** que comparam o estado antes e depois da migration. Por exemplo, "tabela existente" quer dizer que a tabela já existia antes da migration atual.
- **Diagrama em SVG gerado à mão**, com layout em camadas pela dependência de FK.

## Como rodar

Abra o `index.html` no navegador. Não precisa de build nem de servidor. Também funciona no GitHub Pages.

## Limites

- Cobre DDL de tabela, índice e constraint. Views, funções e triggers são reconhecidos, mas não são modelados.
- O linter avalia o comando, não o volume de dados da sua tabela.

---
Thiago Moreira · [github.com/Thiagoo007](https://github.com/Thiagoo007)
