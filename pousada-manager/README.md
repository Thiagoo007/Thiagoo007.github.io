# Pousada Manager

Sistema de gestão da Pousada Recanto do Cerrado, uma pousada fictícia de 10 quartos. Roda direto no navegador, em um único `index.html`, sem servidor e sem dependências, e funciona no GitHub Pages.

## O que o sistema faz

- **Ocupação:** mapa de quartos × dias, com 30 dias navegáveis. As reservas aparecem como barras coloridas por status.
- **Nova reserva:** validação ao vivo de conflito de datas (sem overbooking), capacidade do quarto, mínimo de diárias em feriado e no Réveillon e check-in em data passada. Mostra o valor noite a noite e sugere os quartos livres no período.
- **Estadia:** check-in, lançamento de consumo (frigobar, café colonial, lavanderia), fechamento de conta com forma de pagamento e check-out antecipado, que cobra só as noites usadas.
- **Painel:** ocupação, ADR, RevPAR e faturamento do mês, gráfico de ocupação diária, desempenho por tipo de quarto e movimento do dia.
- **Atendimento:** chatbot no estilo WhatsApp que entende datas e número de pessoas em português, consulta a disponibilidade real, calcula o preço e cria a reserva.
- **Testes:** 29 autotestes das regras de negócio, que rodam ao abrir a página.

## Como rodar

Abra o `index.html` no navegador. Os dados ficam no `localStorage`, e o botão "Restaurar dados de exemplo" gera as reservas de novo a partir de uma semente fixa.

## Arquitetura

- `R`: regras puras (tarifa, conflitos, validação, métricas).
- `Bot`: leitura de texto (intenção, datas, pessoas) e respostas.
- Interface: renderização e eventos, sempre passando pelas regras antes de alterar o estado.

A aba "Sobre o projeto" mostra como a regra de overbooking ficaria no PostgreSQL, com uma constraint `EXCLUDE USING gist` sobre `daterange`.

Projeto de [Thiago Moreira](https://github.com/Thiagoo007).
