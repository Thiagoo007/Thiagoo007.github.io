# Motor de Workflow

Máquina de estados para processos com etapas, transições e regras, com editor visual da régua, simulador e métricas. Roda inteiro no navegador: é um único `index.html`, sem build e sem dependências.

**Demo:** abra o `index.html` ou acesse a página publicada no GitHub Pages.

## O que faz

- **Régua editável:** etapas, transições (avanço, retorno, salto, dispensa), dependências e pré-requisitos, desenhados num grafo SVG.
- **Validação do fluxo:** encontra etapas inalcançáveis, etapas sem saída, ciclos que nunca chegam ao fim e retornos que apontam para frente.
- **Simulador:** cria processos e executa operações. Os botões só ficam ativos quando a régua permite, e o motivo é obrigatório em retorno, salto e desfazer.
- **Auditoria imutável:** cada operação vira um evento. Desfazer grava um evento de compensação em vez de apagar o original.
- **Métricas:** tempo médio por etapa com relógio simulado, gargalo destacado e gráfico de barras.
- **Importar e exportar a régua em JSON.**
- **Autotestes:** 25 testes do motor rodam no navegador, na aba Testes.

O exemplo carregado é um fluxo corporativo de compras e reembolsos: Solicitação → Aprovação do gestor → Análise financeira → Cotação → Aprovação da diretoria → Pagamento → Concluído.

## Design

- **Event sourcing leve:** o estado é sempre `projetar(regua, eventos)`, uma função pura.
- **Invariantes:** existe um único ciclo em andamento, só valem transições previstas na régua, e as etapas puladas são gravadas como dispensadas.
- **Operação atômica:** `executar()` valida tudo e devolve um único evento já com as consequências (as etapas dispensadas), sem estado parcial.

## Stack

HTML, CSS e JavaScript puros, com o gráfico em SVG. O estado fica salvo no `localStorage`.

Feito por [Thiago Moreira](https://github.com/Thiagoo007).
