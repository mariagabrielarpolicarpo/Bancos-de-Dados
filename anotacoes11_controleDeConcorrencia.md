# Controle de Concorrência 

## Propósitos 

- Garantir a propriedade de isolamento em transações
concorrentes

- Preservar a consistência do banco pela preservação
da consistência na execução das transações


## Bloqueio 

- um bloqueio (lock) é uma variável associda a um 
item de dados(como um arquivo, registro, tupla em uma tabela).
E descreve a condição do item em relação às possíveis operações que podem 
ser aplicadas a ele. 

- geralmente há um bloqueio para cada item no BD

Tipos 
- bloqueio binário
- bloqueios compartilhados/exclusivos


### Bloqueio Binário

Possui dois estados: 

bloqueado - O acesso não é possível quando for solicitado, não dá pra fazer leituras ou gravações.
desbloqueado - O acesso é possível quando solicitado.

Operações atômicas:
- lock_item(x)
- unlock_item(x)


Operação lock_item(x)

B: if(LOCK(X) = 0) then 
	LOCK(X) <- 1 
else {
	wait(until LOCK(X) = 0 and 
	    <the lock manager wakes up 
	     the transaction>)
	goto B
} 


Operação unlock_item(x) 

LOCK(X) <- 0
if <any transaction are waiting> then 
	wake up one of the waiting the transactions;


Para cada transação 

- lock(x) 
	antes de ler(x)/gravar(x)
	se x ainda não tiver lock 
- unlock(x) 
	depois de todas as operações ler(x)/gravar(x)
	apenas se tiver o lock de x


Problema do bloqueio binário

- duas operações que apenas querem ler o item não precisam se bloquear mutuamente, já que não vão fazer alterações




### Bloqueio Compartilhado/Exclusivo 


#### Bloqueio compartilhado (shared lock) 
- utilizado para leitura (read lock) 
- mais de uma transação pode empregá-lo
- impede a requisição de um bloqueio exclusivo

#### Bloqueio exclusivo (exclusive lock) 
- utilizado para gravação (write lock)
- somente uma transação pode solicitá-lo 

#### Matriz de compatibilidade: 


		shared 	exclusive
shared		   S	     N
exclusive 	   N	     N


#### Gerenciador de bloqueio 
- gerencia o bloqueio de itens
- mantém uma tabela de controle de bloqueio

Ex: 
Controle(Transação, Item, Modo, Próximo_item)


Operação rlock(x)/read-locked(x)

B: if LOCK(X) = "unlocked" then { // se estiver desbloqueado, então uma pessoa pode lê-lo e o número de leitores aumenta pra um
   LOCK(X) <- "read-locked" 
   no_of_reads(x) <- 1 
} 
else if LOCK(X) = "read-locked" then // quando já há leitores, incrementa número de leitores sempre que alguém acessar X
     no_of_reads(x)++
else {
	wait (until LOCK(X) = "unlocked" and // não é possível fazer alterações no arquivo até que lock(x) esteja desbloqueado, ou seja, até que não haja mais ninguém lendo
	     <the lock manager wakes up the transaction>)
	goto B
}


Operação wlock(x)


B: if lock(X) = "unlocked" then 
	lock(x) <- "write-locked" 
else {
	wait(until lock(x) = "unlocked" and 
		<the lock manager wakes up the transaction>)
	goto B
}



Operação unlock(x) 

if lock(x) = "write-locked" then {
	lock(x) <- "unlocked"
	wake up one of the transactions, if any 
} 

else if lock(x) = "read-locked" then {
	no_of_reads(x)--
	if no_of_reads(x)= 0 then {
		lock(x) <- "unlocked"; 
		wake up one of the transactions, if any
	}



Para cada transação 

- rlock(x)
antes de read(x)
se ainda não tiver rlock ou wlock

- wlock(x)
antes de read(x) com intenção de write(x)
antes de write(x)
se ainda não tiver wlock 

- unlock(x)
depois de todas as operações ler(X)/gravar(x) 
apenas se tiver o lock de x


### Upgrade e downgrade

lock upgrade
rlock(X) -> wlock(x)
condição: não há outro rlock em x

lock downgrade
wlock(x) -> rlock(x)


## TWO PHASE LOCKING (2PL) 


### Protocolo

- Garante a Serialização
- Protocolo de bloqueio de duas fases
	Fase de crescimento: transação pode obter bloqueios, mas não pode liberar
	Fase de encolhimento: transação pode liberar bloqueios, mas não pode obter




T1 		T2 

wlock(x)
ler(x)
x = x - n
gravar(x)
wlock(y) 
unlock(x) // depois que dá unlock não pode mais dar wlock
		wlock(x)
		ler(x)
		x = x + m 
		gravar(x)
		unlock(x)
ler(y)
y = y + n 
gravar(y)
unlock(y)


## DEADLOCK 
"Ciclo de transações esperamando mutuamente a liberação de locks"

T1 		T2 
		rlock(Q)
		ler(Q)
rlock(x)
ler(x)
		wlock(x)
		***espera***
wlock(Q)
***espera***

vai ficar uma esperando a outra liberar eternamente, esse é o deadlock 

### Tratando deadlocks
- prevenção 
- detecção 


#### Prevenção Conservador/Estático
- bloqueia todos os itens a ser lidos/gravados antes de iniciar a transação 
- livre de deadlock 
- exige pré-declaração


### Estrito e Rigoroso

#### Estrito 
- não libera wlocks até o commit ou abort
- garante schedule estirto (T só lê ou grava valores que foram alterados por transações que já realizaram commit)

#### Rigoroso 
- não libera rlocks/wlocks até o commit ou abort
- mais fácil de implementar que o estrito
