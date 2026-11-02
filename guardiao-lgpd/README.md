# Guardião LGPD

Detecta e anonimiza dados pessoais em arquivos CSV ou em texto livre. Tudo roda no navegador: nenhum dado sai da sua máquina.

**Demo:** abra o `index.html` (ou a página do GitHub Pages). Ela já carrega uma base fictícia de 40 clientes.

## O que faz

- **Detecção com validação real:** CPF e CNPJ (dígitos verificadores), cartão (Luhn + bandeira), telefone com DDD brasileiro válido, e-mail, CEP, data de calendário, placa antiga e Mercosul, RG e nome (por coluna).
- **Classificação por coluna:** usa o cabeçalho e uma amostragem dos valores, com um percentual de confiança. Também acha dados pessoais escondidos dentro de campos de texto.
- **Risco de exposição:** score de 0 a 100, com alerta para combinações que permitem reidentificar (nome + CPF, data de nascimento + CEP) e o risco residual depois do tratamento.
- **Mapa de calor:** destaca cada célula com dado pessoal e marca os valores fora do padrão.
- **Tratamento por coluna:**
  - mascarar, no padrão gov para CPF (`***.456.789-**`);
  - pseudonimizar com SHA-256 + salt (Web Crypto), consistente para permitir joins;
  - generalizar (faixa etária, CEP com 5 dígitos, região fiscal do CPF);
  - remover a coluna.
- **Antes e depois** lado a lado, exportação do CSV tratado e relatório de tratamento.
- **35 autotestes** dos validadores e das máscaras, rodando na própria página (aba Testes).

## Stack

HTML, CSS e JavaScript puros, em um único arquivo e sem dependências. Inclui parser de CSV próprio (aspas, `;`, `,`, tab), fallback de SHA-256 em JavaScript e leitura de arquivos em Windows-1252 exportados do Excel.

---
Projeto de portfólio de [Thiago Moreira](https://github.com/Thiagoo007). Os dados de exemplo são fictícios e gerados na hora.
