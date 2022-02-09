# Teste-de-qualifica-o
Repositório criado para responder o questionário de teste de qualificação da empresa AML risco reputacional.

A – Com suas palavras explique o que é lavagem de dinheiro.

**Resposta: É o processo de tornar lícito uma entrada de dinheiro com origem ilícita.**

B – O que é Cartão de Pagamento do Governo Federal (CPGF), e qual a sua finalidade

**Resposta: É um cartão criado para o governo federal agilizar compras de bens ou serviços que não dependem de licítação, ou seja, são mais práticas.
A finalidade do cartão de pagamento é adiantar os gastos que se enquadram em "suprimento de fundo", bens e serviços que podem ser feitos para depois haver a prestação de contas.**

C – Quem pode utilizar o CPGF?

**Resposta: Todo servidor e representante ligado ao governo federal.**

D – Qual a URL onde é possível fazer o download dos arquivos do CPGF?

**Resposta: https://www.portaltransparencia.gov.br/download-de-dados**

E – Qual a URL da paǵina com a descrição dos campos (ou dicionário de dados) da CPGF?

**Resposta: https://www.portaldatransparencia.gov.br/pagina-interna/603393-dicionario-de-dados-cpgf**

F – É possível identificar o nome e o documento do portador do CPGF, em todas as
movimentações ou há movimentações onde não é possível identificar o portador?

**Resposta:Não, pois existem portadores sem informação no campo 'nome'.**

G – É possível identificar o Órgão do portador do CPGF?

**Resposta: Sim, Pois o cartão é emitido em nome da unidade gestora com identificação do portador.**

H - Qual o nome do Órgão cujo código é 20402?

**Resposta: Agência espacial Brasileira.**

I - É possível identificar o Nome e Documento (CNPJ) dos favorecidos pela utilização do
CPGF?

**Resposta: Sim, através da tabela.**

J – É possível identificar a data e o valor das movimentações financeiras do CPGF, em
todas as movimentações? Ou há movimentações onde não é possível identificar as datas e
ou valores?

**Resposta:: Não é possível, pois alguns campos estão vazios.**

K (código) – Qual a soma total das movimentações utilizando o CPGF?

**Resposta:R$ 5619007,94**

Código: 
```
select sum(VALOR_TRANSAÇÃO) from cpgf;
```

L (código) – Qual a soma das movimentações sigilosas ?

**Resposta: R$ 3108731,15**

Código: 
```
select sum(VALOR_TRANSAÇÃO) from cpgf 
where TRANSAÇÃO like '%si';
```

M (código) – Qual o Órgão que mais realizou movimentações sigilosas no período e qual o
valor (somado)?

**Resposta: Departamento da polícia federal com um gasto de R$ 1207131,92**

Código: 
```
select NOME_ÓRGÃO, count(NOME_FAVORECIDO), SUM(VALOR_TRANSAÇÃO) from cpgf
where NOME_FAVORECIDO = 'sigiloso'
group by NOME_ÓRGÃO;
```

N (código) – Qual o nome do portador que mais realizou saques no período? Qual a soma
dos saques realizada por ele? Qual o nome do Órgão desse portador?

**Resposta: Portador Rafael Pereira Costa. Soma do saque R$ 24520,00**

Código:
```
select NOME_PORTADOR, count(TRANSAÇÃO), SUM(VALOR_TRANSAÇÃO) as soma from cpgf
where TRANSAÇÃO like 'saqu%'
group by NOME_PORTADOR
order by soma desc;
```

O (código) – Qual o nome do favorecido que mais recebeu compras realizadas utilizando o
CPGF? 

**Resposta: Não há informação sobre o favorecido que mais recebeu compras.**

Código:
```
select NOME_FAVORECIDO, count(TRANSAÇÃO) as num from cpgf
where TRANSAÇÃO like 'compra%'
group by NOME_FAVORECIDO
order by num desc;
```
P - Descreva qual a abordagem utilizada para desenvolver o código para os ítens de K a O.

**Resposta: Primeiro eu tranferi todos os dados para um banco de dados no workbench e utilizei a linguagem no SQL para fazer as filtragens.**
