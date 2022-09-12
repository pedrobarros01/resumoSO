# Estruturas de SO
Organização do SO é dividida em:
1. Monolítica
2. Micronucleo
3. Camadas
4. Maquina Virtual
## Monolitica
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
