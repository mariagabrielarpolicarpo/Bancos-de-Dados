# Equivalência de Planos 

## Plano Conflito Serializável

### Planos Conflito Equivalentes
- se eu tenho duas transações e a ordem de operações conflitantes for a mesma, eu tenho um plano conflito equivalente. 
- Operações conflitantes: 
1. pertencem a diferentes transações
2. acessam o mesmo item 
3. pelo menos uma grava

### Plano Conflito Serializável 
- equivalente ao plano de conflito serial

## Equivalência de Visão 

### Dois planos S e S' possuem equivalência se:
- possuem as mesmas transações e operações
- No plano S, se há um read(x) em Ti que seja valor original (antes de S) ou gravado por um write(X) em Tj, o mesmo acontece em S'. 
- No plano S, se write(Y) é a última operação em Y a gravar em Tk, o mesmo acontece em S'. 
