## OLTP Online Transaction Processing 

- bancos de dados tradicionais 
- operações de inserção, atualização e exclusão em pequenas partes do banco

## OLAP Online Analytical Processing 

- operações de extração, recuperação e análise de dados

Data Warehouse - termo para esses bancos que são especializados em coletar esses dados e usar para análise 

- otimizada para a recuperação de dados 

## Índice Mapa de Bits - quando o foco é a análise

- facilita consultas sobre chaves múltiplas

- cada índice é baseado em uma chave 

- muito usado para o tipo de pesquisa em que você combina múltiplas chaves e cada índice é baseado em uma chave.

- mapa de bits sobre atributo A e relação r:

1) mapa de bits = array de bits
2) tamanho do array = número de registros de r
3) um mapa de bits para cada valor de A

## Armazenamento por coluna - quando o foco é análise

### Bancos de Dados Orientados a colunas

Todos os dados de uma mesma coluna são armazenados juntos fisicamente. 



