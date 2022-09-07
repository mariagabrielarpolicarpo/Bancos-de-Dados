# Armazenamento físico de dados

## Como o banco de dados armazena os dados fisicamente? 

### 1) Onde armazenamos dados? 

- Memória RAM
- Disco (HD ou CD/DVD)
- Fita magnética
- Solid State Drive (SSD) 
  - usa circuitos integrados como a memória - sem partes
mecânicas.
  - retém os dados sem a necessidade de energia
  - interface equivalente à de um disco

**Memória RAM**: rápida/cara. Recomendável para pequena
quantidade de dados,índices, dados temporários etc. 

**Disco Magnético**: relativamente barato/lento. Bom para
grande quantidade de dados, dados institucionais, logs
etc. 

**Fita Magnética**: baixo custo/lenta. Boa para dados de 
backup, dados históricos, logs,etc. <br>

### Hierarquia de Armazenamneto

Armazenamento Primário 
- Operado diretamente pela CPU 
- Exemplos: memória RAM, cache

Armazenamento Secundário 
- Usualmente mais barato e mais lento 
- Não operado diretamente pela CPU 
  - exigem intermediação de armazenamento primário
- Exemplos: disco, fita magnética

O cabeçote do disco, que fica a uma distância mínima do disco, se desloca e grava no disco.

O disco é organizado em trilhas magnéticas. Essas são divididas em blocos menores que são os setores. 

**Setor**(bloco físico): unidade que o disco usa para fazer a leitura e a gravação. 

O bloco físico se liga ao conceito de página.

A página é um espaço de memória que é alocada pelo SO que faz transferência de dados com o bloco físico. 

Os tamanhos de blocos físicos e páginas podem ser diferentes. <br>

### Operação de leitura de um dado no banco de dados para a memória principal 

1) Encontrar bloco X no disco
2) Copia bloco para buffer(esse buffer pode ser uma página)
da memória principal(se ainda não estiver lá) 
3) Copia o item X do buffer para a variável X da memória
principal. 

### Operação de gravação da memória principal para o banco de dados

1) Encontrar bloco X no disco
2) Copia bloco para buffer(esse buffer pode ser uma página) da memória principal(se ainda não estiver lá) 
3) Copia o item X da memória principal para o buffer
4) atualiza o buffer no disco 
