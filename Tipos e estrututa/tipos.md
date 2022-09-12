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

## Estruturas de SO
Organização do SO é dividida em:
1. Monolítica
2. Micronucleo
3. Camadas
4. Maquina Virtual
### Monolitica
Contém um módulo, ou seja, o SO é um grande bloco que contém tudo que ele precisa.

Tempo de resposta é menor já que tudo(programas) está interligado.

Apresenta 2 tipos de modo:
- Modo Usuario, local das aplicações
- Modo Kernel/Nucleo, local do SO

Exemplos: Windows,Unix, Linux
![Monolitica](./images/Screenshot%20from%202022-09-11%2020-52-02.png)

## Micronucleo/MicroKernel
Consiste em refatorar o kernel, onde torna ele na menor parte possivel da organização.
Tendo só a função de realizar a comunicação entre processos.
E os outros modulos ficam no modo usuário.

![MicroKernel](./images/Screenshot%20from%202022-09-11%2020-55-13.png)

## Camadas
Criar um SO:
1. Modular
    - Divisão de programas complexos em diverso modulos
2. Hierarquico
    - cada modulo vai dependendo dos modulos abaixo dele

Precisa de uma interface bem definida para ocorrer uma conversa entre as camadas superiores e inferiores

![Camada](./images/Screenshot%20from%202022-09-11%2021-07-32.png)
O coração é a alocação de processos

## Maquina virtual
Ela faz varias copias do HW e com isso permite utilizar varios SO dentro dele
Há uma queda de perfomace, já que ela a aplicação precisa passar por 2 níveis para chegar no HW, em vez de 1
![Virtual](./images/Screenshot%20from%202022-09-11%2021-11-10.png)

