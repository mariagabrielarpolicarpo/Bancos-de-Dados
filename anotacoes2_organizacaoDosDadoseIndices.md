# Organização de Dados e Índices

### Arquivos e registros
Arquivos - blocos de dados
Registros - como tuplas. 

### Ordenação Heap, Sequencial e Hash
Heap
- sem ordenação
- gravação em qualquer posição

Sequencial
- gravação em ordem sequencial de acordo com achave de busca

Hash
- cálculo de função de hash sobre atributo para definir posição

Dada a consulta:
SELECT nome FROM Pessoa
WHERE id=146

- Se os dados estão espalhados em disco,precisaríamos acessar todos os blocos do arquivo da tabela Pessoa
- Índices de BDs ajudam neste processo
- Índices de de BDs funcionam como índices
de livros, apontando para a localização do
conteúdo

O índice estrutura os dados, organiza os arquivos e otimiza operações de recuperação

## Entrada de Índice
Entrada de índice (data entry) registros → armazenados em um índice

### Divisões para a entrada de índice
1) k* - registro completo com chave k
2) (k, rid) rid = id do registro de chave k →
3) (k, rid-list) rid-list = lista de registros de chave k

Vantagens das alternativas (2) e (3):
1) mais de um índice para o mesmo arquivo
2)  menor: pode-se carregar mais ou inteiro na memória
3) suporta estruturas mais complexas

### Índices Primários e Secundários
Índice primário ou de agrupamento
- arquivo ordenado sequencialmente
- chave de busca define ordem do arquivo
Índice secundário
- índice de não agrupamento
- índice não necessariamente único

### Índices Densos e Esparsos
Denso
- uma entrada de índice para cada valor de chave
Esparso
- uma entrada índice para mais de um valor de chave
