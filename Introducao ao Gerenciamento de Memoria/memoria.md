# Gerenciamento de memoria
Idealmente, os programadores querem que a memoria seja:
- Grande
- Rápida
- Não volátil
- De baixo custo

Entretanto, a tecnologia atual nao suporta esse ideal, pois existe uma infinidade de processos que querem compartilhar a memoria de forma concorrente e paralela.

## Hierarquia de memoria
![Memoria](./images/Screenshot%20from%202022-09-25%2016-49-49.png)
Um exemplo: Um processador acessa a memoria de registrador mais rápida que a memória principal.
Entretanto, a memoria principal(RAM) tem mais tamanho(bytes) que o registrador.

Cache é uma memória intermediária entre a RAM e a cpu, pela a hierarquia, ele tem um acesso mais rápido que a RAM mas tem pouco tamanho. Ela contém niveis Lx, que podem mudar essa velocidade e tamanho.

A RAM, considerada memoria principal, quanto maiores são memorias que vão prover uma maior e melhor area de execução de programas.

Os armazenamentos persistente, não volátil Disk, são memorias que os dados continuam armazenados e não excluido, mesmo desligando o computador.

Unidades de backup, utilizados para backup

## Tarefa do Gerenciador de memoria
- Gerenciar a hierarquia de `memória`
    - Gerenciar os espaços livres e ocupados
    - Alocar e localizar processos/dados na `memória`
- Controlar partes que estão em uso e as que não estão
    - Realizar um mapeamento para dizer quais partes estão em uso e as que não estão
    - Alocar `memória` aos processos, quando haver necessidade
    - Liberar `memória` quando um processo termina de utilizar
- Tratar o problema de swapping
    - que é tirar o conteudo da memoria principal e colocar no disco, fazendo assim o inverso tambem
    - RAM <----> Disk

Todo esse trabalho é feito por um modulo do SO que se chama gerenciador de recursos.

## Gerencia de memoria - Monoprogramação
![Memoria](./images/Screenshot%20from%202022-09-25%2017-11-48.png)
- A) usados em  mainframes, SO se encontra na RAM
- B) Usados em alguns handhelds(smartphone), o SO se encontra na memoria de apenas de leitor
- C) Primeiros computadores pessoais, SO se encontra na RAM no endereço 0, e os drives de dispositivos sao armazenados em memoria de apenas de leitura

## Gerencia de memoria - Multiprogramação
Como podemos fazer n processos armazenar na mémoria?

### Partições
Uma forma para isso é, dividir a memoria em varias partições:
- Com tamanho fixo, mas não igual
- Ao chegar um job, ponha ele na fila
- O espaço que sobrar não será utilizado
- ![Memoria](./images/Screenshot%20from%202022-09-25%2017-23-20.png)

Entretanto, temos um problema com isso ae, como fazer cada processo ter sua parte sem que invada a parte do outro.

Exemplo: um processo A vai utilizar o endereço 28 da parte dele, mas se não utilizar nenhuma medida de segurança ele pode invadir o endereço 28 do outro processo B.

Para isso, existe 2 registradores, onde 1 vai armazenar a base(endereço onde ele foi armazenado na RAM) e o outro o limite da partição.

A conta é simples: base + tamanho do programa = limite da partição, ou seja, essa conta da o limite máximo que que seu progrma pode acessar em endereço de memória.

### MMU (Memory Management Unity)
é um dispositivo de HW, que transforma endereços logicos em fisicos

Endereços logicos são os endereços que mostram como o processo trabalha(intervalo que o processo utiliza para o trabalho)

Endereço fisico, é o endereço real que o processo foi alocado.

Um programa manipula endereços lógicos(virtuais) e nunca vê endereços fisicos reais.


## Memoria particionada - Tipos
- Particioes fixas(alocação estatica)
    - São alocadas no boot do sistema, no inicio do sistema
    - Tamanho e numeros de partições são fixos (estáticos)
    - Tendem a desperdiçar memória
    - Mais simples
- Particoes variaveis(alocação dinamica)
    - São alocadas em tempo de execução
    - Otimiza a utilização da memoria, mas complica a alocação e liberação
    - Partições sao alocadas dinamicamente
    - ![Memoria](./images/Screenshot%20from%202022-09-25%2017-45-35.png)
        - Como é alocada em tempo de execução, temos que no inicio do sistema não contem partições, mas o processo A entra em execução, assim ocupando uma partição, o B e o C a mesma coisa.
        - Quando o A para de executar, ele libera a partição, quando o D chega, ele compara pra ver se cabe na partição, se sim, ele entra. E assim vai.

## Swapping
Seria a transferencia de dados/paginas/partições entre a memoria principal e uma memoria secundaria(disco)
- Swap-Out
    - Da memoria principal para o disco
- Swap-In
    - Do disco para o memoria principal
![Memoria](./images/Screenshot%20from%202022-09-25%2017-57-17.png)

## Estruturas para Gerenciar a Memoria
Para fazer gerenciamento de espaço de memoria:
- Usando o mapa de bits:
    - Mémoria é dividia em unidades de alocação
    - Unidade pode conter vários Kb
    - Cada unidade corresponde um bit no bitmap:
        - 0 -> livre
        - 1 -> ocupado
    - Basicamente, ele vai setando o bit para cada bloco de memoria ocupado
    - EXemplo: quando um processo vai ocupar uma partição, ele seta 1 para os blocos que o processo ocupou da partição e 0 oara os que não ocupou visto na letra b
- Lista Encadeada
    - Manter uma lista ligada de segmentos de memorias livres e alocados
    - Por ser uma lista encadeada, ela contem uma estrutura/tipo para armazenar
    - Esse tipo/Estrutura é formada por:
        - Tipo: P | H -> indica se é um processo que ocupou(P) ou se esta vazio como um buraco(H)
        - DadoInicio -> se for P, ela indica o endereço de incio a ser ocupado, se for H, indica qual o primeiro endereço livre
        - DadoFinal -> se for P, indica o endereço máximo que o processo ocupa, se for H, indica o tamanho livre em blocos.
![Memoria](./images/Screenshot%20from%202022-09-25%2018-05-37.png)

## Algoritmos de Alocação
- Primeira Escolha
    - Percorre a lista ate que encontre o primeiro bloco que caiba
- Melhor escolha
    - Busca a lista inteira e toma a menor partição
    - Escolher a area que melhor se encaixa no processo
- Pior escolha
    - Busca a lista inteira  para tomar a maior partição
    - Ele de fato escolhe a maior partição
![Memoria](./images/Screenshot%20from%202022-09-25%2018-14-11.png)






