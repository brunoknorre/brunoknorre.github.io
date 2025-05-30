---
layout: post
title: "Introdução às Window Functions em SQL"
date: 2025-05-29
categories: [SQL, banco-de-dados]
tags: [sql, window-functions, analytics]
author: Bruno Knorre
---

## O que são Window Functions?

Sabe quando você quer fazer um cálculo em SQL, tipo uma média ou uma soma, mas sem perder os dados originais? Tipo, você quer ver o salário de cada funcionário *e* a média do departamento ao mesmo tempo? Então... é aí que entram as **Window Functions** (ou funções de janela).

Essas funções são super úteis porque permitem que a gente faça esses cálculos em "janelas" de dados, sem precisar agrupar tudo e sumir com os detalhes das linhas.

Com elas, dá pra fazer ranking, comparar valores entre linhas e até calcular totais acumulados — tudo isso mantendo cada linha da tabela visível no resultado.

---

## Por que usar Window Functions?

Imagina que você tem uma tabela com várias vendas e quer saber quanto cada vendedor vendeu *e* o total vendido por mês. Com funções agregadas normais (`SUM`, `AVG`, etc.), você teria que agrupar os dados, o que esconderia as linhas individuais.

Com Window Functions, isso não acontece. Você consegue:

- **Ver a média por grupo sem esconder os dados individuais** (tipo a média salarial por departamento).
- **Criar rankings** (tipo quem vendeu mais em cada time).
- **Comparar dados entre linhas**, tipo ver quanto as vendas aumentaram ou diminuíram de um mês pro outro.

Ou seja, mais controle, mais clareza e mais flexibilidade nas suas análises.

---

## Exemplo simples: Média Salarial por Departamento

Vamos ver um exemplo bem direto:
```sql
SELECT  
  nome,  
  departamento,  
  salario,  
  AVG(salario) OVER (PARTITION BY departamento) AS media_departamento  
FROM funcionarios;
```
O que tá acontecendo aqui:

- A função `AVG(salario)` tá calculando a média de salário.
- O `OVER` diz que isso é uma função de janela (sem ele seria uma agregação comum).
- O `PARTITION BY departamento` faz com que a média seja calculada dentro de cada departamento.

No fim, você continua vendo cada funcionário com seu salário, mas agora também aparece a média do departamento ali do lado. Muito útil!

---

## Entendendo as partes principais das Window Functions

Pra usar essas funções com confiança, é bom entender três partes principais:

- **OVER()**: é obrigatório, porque indica que a função é de janela.
- **PARTITION BY**: divide os dados em "grupos", como se fossem mini-tabelas dentro da sua consulta.
- **ORDER BY**: organiza as linhas dentro de cada grupo, essencial pra funções que dependem de ordem, tipo `ROW_NUMBER()` ou `LAG()`.

---

## Onde isso é útil na prática?

Tem várias situações do dia a dia em que as Window Functions ajudam MUITO. Aqui vão algumas:

- **Rankings de desempenho**: por exemplo, quem são os top 3 vendedores por região.
- **Somas acumuladas**: tipo, quanto foi vendido até certo ponto no mês.
- **Comparações entre linhas**: ver se a venda desse mês foi maior que a do mês passado.
- **Análises por grupo**: como cada cliente se comporta dentro de uma categoria, por exemplo.

---

## E o que mais dá pra fazer?

Tem muita coisa legal que dá pra explorar com Window Functions. Algumas das funções mais comuns são:

- `ROW_NUMBER()`: numera as linhas dentro de um grupo (ótimo pra rankings simples).
- `RANK()`: parecida com a de cima, mas trata empates de forma diferente.
- `LAG()` e `LEAD()`: pegam o valor da linha anterior ou da próxima, super úteis pra comparar.

---

Se você nunca usou Window Functions, minha dica é: começa testando com exemplos simples e vai brincando. Você vai ver como elas abrem um mundo novo dentro do SQL.

Qualquer dúvida, sugestão ou só pra trocar uma ideia, deixa um comentário aí. Vamos aprendendo juntos :)
