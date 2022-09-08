Composição de operações

Closure property
- cada operação recebe tabelas e retorna uma tabela
- operações podem ser compostas

Exemplo: operação_2(operação_1(relação)a)) 


relação_b <- operação_1(relação_a)
relação_c <- operação_2(relação_b) 


SQL p/ Álgebra

Versão SQL

SELECT Codigo, Nome 
FROM PESSOA
WHERE AnoFiliacao = 1990

Versão em álgebra
pi codigo, nome (sigma anofiliacao = 1990 (PESSOA))


Regras de Transformação 

1) Operações seleção conjuntivas podem se converter em cascatas de seleção 
2) Operação de seleção é comutativa
3) A comutação de seleção com projeção só é possível se:
- o resultado da projeção tenha atributos requeridos para seleção
4) Seleção e junção (ou produto cartesiano) são comutativas
- se atributos da seleção são de apenas uma das relações
5) Operações de união e interseção são comutativas (a diferença não é) 
6) Seleção é comutativa com operações de cojunto (união, interseção e diferença)
- sel (A U B) equivale a sel(A) U sel(B) 
7) As operações de junção e produto cartesiano são comutativas
8) As operações de junção, produto cartesiano, união e interseção são associativas (A...B)...C equivale a A...(B...C) 
9) Operações de produto cartesiano + seleção podem ser converter em junção 
10) Cascata de projeções podem ser ignoradas e convertidas na última 
- Pr1(Pr2(Pr3(A))) equivale a Pr1(A) 
11) Operações de projeção e união são comutativas 
- proj (A U B) equivale a proj(A) U proj(B) 
12) Operações de projeção podem ser comutadas com junção (ou produto cartesiano) 
- Relação A -> atributos a1, a2,..., an 
- Relação B ->atributos b1, b2, ..., bm
- L = (a1,..., an, b1,b2...,bm) 
- Condição só contém atributos L
- projL(A junção B) equivale (proj a1,a2, ...,an (A)) junção (proj b1,b2,...bm(B))


Heurísticas

Boas práticas
1) quebrar operações de seleção conjuntivas (1) 
- me dá maior liberdade 
2) mover seleção em direção às folhas (2),(3), (4), (5) e (6) (objetivo de fazer a seleção o mais cedo possível) 
- apenas 1 tabela -> seleção acima da tabela
- duas tabelas -> seleção acima da junção 
3) Operações de seleção mais restritivas devem ser executadas primeiro (5) e (6) 
4) Desmembrar operações de projeção 
5) Mover projeções em direção às folhas
6) Criar operações de projeção apra manter apenas atributos necessários 
7) Identificar subárvore com operações a serem combinadas em um algoritmo 
