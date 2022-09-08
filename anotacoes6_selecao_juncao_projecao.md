# Seleção, Junção e Projeção

## Seleção

Quando eu seleciono alguma coisa no banco de dados, eu posso ter resultados como: 

1) Exatamente igual 
- chave primária 
- outra chave

ex: quero a linha do cliente que tem cpf 645456464
Só existe um resultado para isso

Para esse caso, o hash é muito eficiente, pois o tempo de resposta é uma constante.

2) Faixa 
- Operadores: >, <, >=,<= 
 
Como não são filtrados por uma chave primária, eu vou ter como resultado diversos valores que a faixa abrange

Não tenho como saber a priori os valores que estão na faixa. Não há um registro de ordem, pois os valores estão espalhados. 
Para esse tipo de consulta, a árvore B+ é mais recomendada. (custo: log do tamanho de conjunto de dados que eu tenho)

### Algoritmos de Seleção 

O que um banco de dados pode fazer quando recebe um comando de seleção: 

1) Pesquisa Linear
2) Pesquisa Binária
3)Usar índice primário 
4) Usar índice secundário 
5) Usar índice de agrupamento
6) Usar chave hash 
7) Combinar chave hash com índice primário

### Seletividade 

- valor entre 0 e 1
- n registros
- igualdade atributo único 
1) seletividade: 1/n

### Seletividade Atributo Não Único 

- valores
- i igualmente distribuído
- n/i registros por valor
- seletividade: 1/i
- primeiro as condições com valor menor de seletividade 


## Junção 

Considerando duas tabelas ti e tj que vão passar por um join. Considere as funções: 

- match(ti,tj) - retornam true ou false para a condição de junção
- add-result(ti,tj) - adiciona as tuplas ao resultado do Join no formato esperado. 
- ni - número de tuplas ti
- nj - número de tuplas tj 
- bi - bloco de tuplas ti
- bj - bloco de tuplas tj 

Comparação: ni*nj pares de tuplas 
Leitura de blocos: bi + bj*ni


## Projeção 

- recorte dos campos 
- registros sem duplicatas:
1) SQL-> padrão não eliminar duplicatas
- distinct -> elimina duplicatas
2) Registros com garantia de ser únicos 
- contendo chave primária

3)Registros sem garantia de ser únicos 
- ordenação
- hashing 
