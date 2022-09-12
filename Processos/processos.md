# Processos
Processo é um programa que é colocado em execução

## Diferença entre processo e programa
Processo é a instancia de um programa, ou seja, quando esta em execução e ele possui dados de entrada, saida e um estado(executando, pronto, bloqueado)

## Progrma vs Processo
### Programa
- pode ter varias instancias em execução(em diferentes processos)
- Algoritmo codificado
- Forma como programador ve a tarefa ser executada
### Processo
- é unico
- Codigo acompanhado de dados e estados
- forma como SO ve o um programa e possibilita a sua execução

## Tipos de processo
### Primeiro Plano
- interage diretamente com o usuario
- exemplo: ler arquivo, carregar browser
- especifico
![Chamada](./images/Screenshot%20from%202022-09-12%2000-23-14.png)
### Segundo Plano
- nao tem uma intereção direta com usuario
- generico
- com funções especificas
- exemplo: serviços de impressao, recepção e envio de emails
![Chamada](./images/Screenshot%20from%202022-09-12%2000-26-53.png)

## Componentes de um processo
- Conjunto de instruções
- Espaço de endereçamento(espaço reservado para o processo ler e escrever)
- Contexto de HW(valores que o HW comtem referente ao processo, valores de registradores como o PC, ponteiro de pilha)
- Contexto de software(variaveis, lista de abertura de arquivos, etc)

## Espaço de endereçamento
Esse espaço contem 3 segmentos:
1. Texto: codigo executavel do programa
2. Dados: variaveis
3. Pilha de execução: vai chamando as rotinas que o processo precisa chamar, e depois volta pro inicio


## Tabela de processos
Tabela que indica os processos e seus estados.

COntem informações de contexto de cada processo(ponteiros de arquivo aberto, posição do proximo byte a ser lido).

Contem informações necessarias para trazer o processo de volta, caso ele esteja bloqueado pelo o SO.

Contem os estados de cada processo.

Não guarda o conteudo do espaço de endereçamento

## CAracteristica de um processo
1. CPU-Bound
    - utiliza mais CPU que dispositivo de E/S
    - tempo é definido pelo o ciclos de processador
2. E/S-Bound
    - utiliza mais operações de E/S que a CPU
    - tempo é definido pela a duração das operaçoes E/S

Ideal é ter um equilibrio entre os dois processos
## Ciclo de um processo
Ele pode nascer-executar-morrer
### Criação de um Processo
- Inicialização do sistema
- Execução de uma chamada de sistema para criação de um processo
- Requisoção de um usuario(double-click em um programa)
- Inicialização de um processo em batch
### Execução de um processo
Quando de fato ele ta rodando.
### Finalizando o processo
1. Termino normal(voluntario):
    - a tarefa ser executada é finalizada
    - ao chamar uma syscall de saida
2. Termino por erro(voluntario):
    - O processo sendo executado nao pode ser finalizado.
    Ex: gcc filename.c; o arquivo filename nao existe
3. Termino com erro fatal(involuntario)
    - Causado por algum erro no programa(bug)
4. Termino causado por algum outro processo(involutario), via a chamada a:
    - kill
    - TerminateProcess

## Estados de Processos
1. Executando: quando esta usando a CPU naquele momento
2. Bloqueado: incapaza de executar enquanto um evento externo não ocorrer
3. Pronto: em memoria, pronto para executar(ou continuar a execução), apenas aguardando a disponibilidade do processador
![Chamada](./images/Screenshot%20from%202022-09-12%2001-00-26.png)



