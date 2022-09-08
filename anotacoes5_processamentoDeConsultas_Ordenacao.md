# Processamento de Consultas e Ordenação

Quando o SGBD faz uma consulta SQL - ele transforma aquilo em álgebra relacional estendida e inclui operadores como count, sum e max; 

SELECT Codigo, Nome 
FROM Pessoa
WHERE AnoFiliacao = (SELECT MIN(AnoFiliacao) FROM PESSOA)

O SQL divide essa consulta em dois blocos em que resolve 
separadamente e depois junta.

BLOCO 1:
 
SELECT Codigo, Nome 
FROM Pessoa
WHERE AnoFiliacao = (referencia 2)

BLOCO 2: 

SELECT MIN(AnoFiliacao) FROM PESSOA

## Ordenação 

Como usar ordenação para evitar duplicatas? 
Ao ordenar, registros iguais ficam juntos, aí é possível remover. 

### Algoritmos de ordenação 

- bubble sort; quick sort; merge sort; heap sort; selection sort;insertion sort; 

quick, merge e heap - geralmente são mais eficientes

Merge sort - melhor ordenação para dados que estão em disco, considerando que não consigo colocar todo o conjunto de dados na memória de uma única vez.
