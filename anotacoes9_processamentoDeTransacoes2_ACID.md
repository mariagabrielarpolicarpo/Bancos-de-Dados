# Processamento de Transações 

## ACID 

### Propriedades 

- **Atomicidade**: todas as operações da transação acontecem ou nenhuma acontece. Ex das operações bancárias que não podem ser incompletas. 
- Preservação de **Consistência**: após uma execução completa, o BD tem que passar de um estado consistente para outro. 
- **Isolamento**: uma transação deve ser executada como se estivesse isolada das demais. Se uma transação de uma afetar a outra, então eu tenho um problema.
- **Durabilidade**: se uma transação é efetivada, seu efeito persiste. 

### Consistência DELETE/CASCADE

Eu tenho duas tabelas. Em uma eu tenho a coluna com a minha chave primária e a outra eu tenho a coluna com essa chave primária que está referenciando a primeira tabela. Se eu quero excluir uma tupla, eu não posso por exemplo excluir a da primeira tabela e depois excluir da segunda, pois vai gerar inconsitência no banco de dados, já que a tupla da segunda tabela está apontando para um local que não existe. Uma das opções de resolver essa problemática é a realização da exclusão em cascada, então eu não vou ter duas transações de exclusão, mas as duas exclusões sendo feitas na mesma transação. 

## O que o Banco de Dados precisa fazer para garantir o ACID?

### Plano de Execução Restaurável 

- **Plano Restaurável**: Uma variável realiza commit somente depois que todas as transações cujos valores que a variável leu realizam commit.
- **Plano Livre de Cascata(cascadeless)**: A variável só lê valores que foram alterados por transações que já realizaram commit. 
- **Plano Estrito**: A variável só lê/grava valores que foram alterados por transações que já realizaram commit

### Plano Serial e Serializável

#### Plano Serial
- Transações completas são executas em série. 
- Não há intercalação de operações entre transações
- É um plano correto. Não vai dar os problemas de intercalação. 

#### Plano Serializável
- Equivalente a algum plano serial. 
- É intercalável, para obter a mesma eficácia do plano serial, ele lê e grava as transações antes de partir para uma próxima. 

### Grafo de Precedência

- Para cada transação, crie um nó no grafo. 
- Ocorre somente quando há gravações.
- Serializável -> sem ciclos 
- Considerando Ti uma operação inicial e Tj uma operação posterior a Ti. Para cada caso, temos: 
1. Ti -> gravar(x) e depois Tj-> ler(x) 
2. Ti -> ler(x) e depois Tj-> gravar(x)
3. Ti -> gravar(x) e depois Tj -> gravar(x)
