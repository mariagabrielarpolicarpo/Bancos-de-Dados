# Processamento de Transações

## Vantagens e desvantagens de se permitir acesso concorrente ao banco de dados:

### Vantagens 
- otimização de aceso
- melhor aproveitamento do sistema 
  -> menor tempo ocioso 
- permite colaboração 

### Desvantagens 
- pode gerar inconsistência
- pode reduzir desempenho
- pode ter problemas de bloqueio 


## Conceitos de transação 

- A execução concorrente de programas é essencial para a boa performance do SGBD 
  - acesso a disco é frequente mais lento -> concorrência melhora aproveitamento da CPU 

- Perpesctivas sobre os dados: 
  - programa do usuário -> pode realizar várias operações com os dados
  - SGBD -> se preocupa apenas com leituras e gravações

## Transação e Concorrência

- Transação: visão abstrata do SGBD sobre um programa do usuário 
  - uma sequência de leituras e gravações 
  - Na prática, o controle de transações do banco de dados só se interessa por leituras e gravações.

- Perpesctivas sobre a transação: 
  - usuário -> sua transação sendo executada individualmente
  - SGBD -> concorrência intercalando leituras/gravações de várias transações 


## Estados de Execução 

1) BEGIN_TRANSACTION: se inicia a transação

2) READ OU WRITE: o banco de dados começa a leitura de arquivos

3) END_TRANSACTION: se deu tudo certo, fim da transação

4) COMMIT_TRANSACTION: quando eu fiz o commit, a transação foi efetivamente gravada no banco de dados e a transação é encerrada, mas pode dar um erro no sistema e ocorrer um abort

5) ROLLBACK (ou ABORT): é uma falha, a transação é encerrada



## Problema: Intercalação de reserva

Exemplo: há duas pessoas na biblioteca que querem reservar o mesmo livro ao mesmo tempo. A primeira verifica se o livro está disponível e o sistema responde que sim e fica pensando se reserva esse livro ou não. Enquanto isso a segunda pessoa também percebeu o livro estava livre e reservou e o sistema gravou, ai a primeira pessoa foi e reservou o livro também. Conflito de memória. 

## Plano de Execução 
- O banco de dados intercala as operações, faz operações concorrentes. 

T1 ------------- T2 

ler(x) ------- ler(x)

x = x - n ----- x = x + m

gravar(x)	------ gravar(x)

ler(y)

y = y + n 

gravar(y) 


### Plano de Execução Serial
- Realizo todos os planos de execução de uma transação, depois faço de outra.

T1 		T2 

ler(x)		

x = x - n 		

gravar(x)	

ler(y)

y = y + n 

gravar(y) 

gravar(x)

### Plano de Execução Intercalado 
- As operações da transação vão ocorrendo de forma intercalada.
- Problemas: atualizações podem se perder se não forem feitas da maneira correta. Isso significa que logo que o bd lê o valor de uma variável, ele tem que gravar também. 

ler(x)(T1)	-> x = x - n(T1) -> ler(x)(T2) -> x = x + m(T2) -> gravar(x)(T1)	-> ler(y)(T1) -> gravar(x)(T2) -> y = y + n(T1) -> gravar(y)(T1)

### Plano de Execução (Schedule)
- aplicável a várias transações simultâneas
- lista de ações de conjunto de transações

  -> leitura, gravação, abort, commit
