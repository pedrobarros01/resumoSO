# Threads
Thread é uma linha do processo em execução, sendo obrigatório na composição do processo.

## Modelo de Processo vs de Thread
### Processo
Contém:
    - um espaço de endereçamento
    - agrupamento de recurso(espaço de endereço com texto e dados do programa,arquivos abertos, tratadores de sinais e etc)

### Thread
Contém:
    - um espaço de endereço
    - multiplas linhas de controle
    - Possuem recursos particulares(PC, registradors, pilha)

A diferença entre os modelos seriam que as threads compartilham o espaço de endereçamento entre eles, quanto o processo contém esse espaço unico.

## Vatagens de Threads
- Execução de varias atividades ao mesmo tempo
- Podemos decompo-la em atividades paralelas
- Podemos dividir as threads em CPU-Bound e I/O-Bound
- São mais rapidas em criar e destruir que processos
- Uteis em sistemas de multiplos CPUs -> paralelismo(arq e org 2)

## Exemplos
### Editor de texto
Vamos pensar num editor de texxto(Docs) que tem função de identação, correção, mudança de linha.Ao fazer um paralelo com processo e thread, colocamos todas essas funções do editor como threads de exexução de um processo maior que seria o próprio editor de texto.
![Exemplo](./images/Screenshot%20from%202022-09-16%2010-05-24.png)
### Servidor Web
No servidor web, vai ter uma grande quantidade de thread para, onde cada uma delas vai receber uma requisição de um user diferente, chamadas de threads operario. E terá a thread dispachante que seria aquela que iria passar a requisição para a operário
![Exemplo](./images/Screenshot%20from%202022-09-16%2010-08-58.png)

## Visualmente
3 processos que contem um thread:
![Exemplo](./images/Screenshot%20from%202022-09-16%2010-12-27.png)
Assim, dentro do processo, terá:
![Exemplo](./images/Screenshot%20from%202022-09-16%2010-14-10.png)

Mas num processo com 3 threads:
![Exemplo](./images/Screenshot%20from%202022-09-16%2010-15-01.png)
Dentro dele terá:
![Exemplo](./images/Screenshot%20from%202022-09-16%2010-15-40.png)

## Problemas com a threads
as threads contem 2 problemas principais:
1. Como cada thread pode ter acesso a qualquer endereço de memoria dentro do espaço de endereçamento do processo:
    - uma thread pode ler, escrever, ou apagar a pilha  ou as variaveis globais de outra thread.
    - Ex: a = b + c; x = a + y
2. Necessidade de sincronização na execução, pois pode ser que uma thread dependa de dados de uma outra. Assim não podendo ser executada primeira

## Estados
1. Pronto -> quando so a cpu é necessaria
2. Execução ->  quando ela tem a cpu
3. Bloqueado -> quando aconteceu algum evento nela(I/O, escalonamento, tempo expirou)
![Exemplo](./images/Screenshot%20from%202022-09-16%2010-25-22.png)

## Tipos
1. Modo Usuário
    - Implementadas no espaço de enderaçamento do usuario
    - por meio de uma biblioteca de uma linguagem de prog(java/c)
    - criação e escalonamento são realizados sem que o kernel saiba
    - cada processo possui a tabela de threads
    - ![Exemplo](./images/Screenshot%20from%202022-09-16%2010-50-52.png)
    - Escalonamento:
        - O kernel escolhe um processo e passa o controle a ele, que escolhe uma thread
        - A gerencia de thread fica em nivel de usuario e o kernel so escalona o processo.
        - ![Exemplo](./images/Screenshot%20from%202022-09-16%2010-54-26.png)
    - Existe um mapeamento das thread de nivel de usuario para um thread em nivel de kernel, chamado de modelo N:1
2. Modo Kernel
    - Suportadas diretamente pelo SO
    - o kernel possui as tabelas de threads
    - criar e destruir threads no kernel é mais caro
    - Escalonamento:
        - o kernel escolhe diretamente a thread
        - a thread é quem recebe o quantum, sendo suspensa se excede-lo
        - thread bloqueada por E/S não bloqueia o processo
        - permite multiplas threads em paralelo
        - ![Exemplo](./images/Screenshot%20from%202022-09-16%2011-05-33.png)

3. Hibrido
    - Seguem o modelo N: M, mapeamento de N threads do modo usuario para M threads do modo kernel