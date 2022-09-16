# Espera Ocupada(Busy Waiting)
Ela verifica se a RC está sendo utilizado por processo1 e se um processo2 está tentando entrar na RC, tudo isso com uma contante checagem de valor

## Soluções com busy waiting
1. Desabilitar interrupção
2. Variaveis de Travamento(Lock)
3. Estrita Alternancia
4. Solução de Peterson e Instrução TSL


## Desabilitar Interrupção
Quando um processo entra na RC, ele desabilita todas as suas interrupções do processador.

Impedindo que a CPU de atençao a outro evento.Ou seja, impedindo a mudança de contexto entre os processos.

Uma desvantegem dela é que ela viola a regra 2 do topico `Regras para programação concorrente`, já que ela só funciona no ambiente monoprocessado. E viola a regra 4, onde ele pode esque de habilitar novamente as interrupções.

Em arquitetura multiprocessada ele viola a regra 1.

## Variaveis de Travamento(Lock)
Utiliza uma variavel para permitir ou não a entrada de um processo numa RC.
![Exemplo](./images/Screenshot%20from%202022-09-16%2015-59-42.png)

Nessa figura, existe a variavel `lock` faz função de travamento da RC de um processo. onde se ela for 0, o processo seta ela para 1 e entra na RC e quando sai seta o `lock`para 0. Mas existe o mesmo problema que aquele spool de impressao dos arquivos citado anteriormente.

Onde, se caso ocorra uma interrupção/mudança de contexto no bloco de codigo de processo a seguir, pode ser A ou B, mas vamos tratar que é o do A:
```c
while(lock != 0){
    // se ocorrer aqui
    lock = 1
}
```
Ele para o bloco do A, e começa o bloco do b com `lock = 0`, com isso, ele entra na RC com o processo B e quando haver uma outra mudança de contexto ele volta para o A, que vai entrar tambem na RC. Assim os 2 processos acabam entrando na RC, o que não pode.

Violando assim a regra 1

## Alternancia Explicita
Sempre vai alternando os processos a entrarem na RC.
Nunc um processo entra 2 vezes na região critica.
Utiliza a variavel `turn`para fazer essa alternancia.
![Exemplo](./images/Screenshot%20from%202022-09-16%2016-25-00.png)
Nessa figura, começando do processo A, acontece que a variavel `turn` so atualiza para o valor 1 depois da entrada e saida da RC.  Assim o processo B, poderá entrar na RC e depois troca o `turn` para 0.

As trocas depende da quantidade de processos, onde acaba virando uma lista circular, para volta ao inicio. Sendo tendo trocas de `t0 -> t(n-1) -> t0`.

Assim, existe um problema que se tiver um `tI` que demore de sair da regiao não critica, ele acaba travando toda a sequencia que deseja entrar na RC.
Violando a regra 3.


## Solução de Peterson
Sendo um modelo de solução, ele contem 2 funções: `entra_regiao` e `deixa_regiao`
- Antes do processo entrar na RC:
    - Cada processo chama a `entra_regiao`
    - Ele so entra na RC ,quando a `entra_regiao` retorna liberando ele para entrar
- Quando sai da RC:
    - Ele chama a `deixa_regiao`, para liberar a RC pra outro processo

## Solução de Peterson com TSL
- Faz uso de Hardware
- usa a instrução TSL,RX,lock em assembly
- le o conteudo do lock e armazena no registrador RX
- Operação indivisivel com ajuda do HW, gerando alto custp
- Bloqueia o barramento de memoria
- se `lock == 0`, RC liberada
- se `lock != 0`, RC ocupada
![Exemplo](./images/Screenshot%20from%202022-09-16%2017-09-14.png)
![Exemplo](./images/Screenshot%20from%202022-09-16%2017-12-08.png)

## Exclusao Mutua com Busy Waiting
- Busy Waiting: quando um processo deseja entrar na RC, ele verifica se a entrada é permitida. Se não for, o processo ficará em um laço de espera, até entrar.

- Desvantagens: 
    - derperdiça tempo da CPU
    - Alguns mecanismos são simples
    - Outros são mais caros como o TSL


