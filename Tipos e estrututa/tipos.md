# Tipos de SO
Nos baseamos no quesito de compartilhamento de hardware, esses são:
1. SO Monoprogramado ou MonoTarefa
    - Nesse SO só permite a execução dde 1 só programa em um dado periodo de tempo, onde ele fica na memoria RAM até o seu termino
2. SO Multiprogramado ou MultiTarefas
    - Nesse SO permite a execução de varioas programas ao em um periodo de tempo, onde todos ficam na memória.Assim precisando ser mais rico que o primeiro tipo
## SO Monoprogramado ou MonoTarefa
1. os recursos de HW ficam alocados para a execução de 1 só programa

2. Esse sistema utiliza muito mal os rcursos de HW, se por exemplo, um programa utiliza mais o disco, a CPU fica ociosa.

3. O processo(programa que se encontra em execução) dela permite 3 estados:
    - Execução nova -> que começa
    - Execução -> quando utiliza a CPU, mas pode ter a chance de não utilizar ela de fato
    - Termino -> quando termina a execução
![estados](./images/Screenshot%20from%202022-09-11%2020-26-46.png)
4. Vantagens:
    - Simples


## SO Multiprogramado ou MultiTarefas
1. Mantém varios programas em execução

2. Há varias tarefas simultâneas em unico processador: onde uma esta na CPU(rodando), a outra espera

3. Demandam de mecanismo de trocas rápidas de processos

## Tipos de SO MultiTarefas
### Sistema Batch
Consiste em executar um lote(batch) de programas(jobs) de uma só vez.
Jobs é justamente esses programas que serão executados sequencialmente.
Não existe uma interação do usuario e o jobs durante a execução
Ele só dará uma resposta depois da execução

### Sistema Interativo
Há a interação de varios computadores/terminais com um computador(mainframe)
Utiliza os conceitos de Multitarefa e time sharing para poder haver esse compartilhamento
Time-Sharing -> compartilhamento de tempo de processamento para esses varios computadores



