# Escalonador
O escalonamento é justamente a troca de processos em execução, ele que escolhe quem para e quem é executado

`ele é um processo que escolhe qual o proximo processo a ser executado`

Tendo varias tecnicas/algoritmos para isso

Nivel mais baixo do SO

## Mudança de Contexto
Quando ocorre uma mudança de estado, mas para isso ele precisa(tarefa cara):
1. Salvar as informações do processo que esta deixando / entrando na CPU
2. Salvar os conteudo dos registradores
Para quando ele voltar a ser executado, ele volta com as informações antigas

## Componentes envolvidos
1. Despachante(Dispatcher):
    - aquele vai fazer a mudança de contexto
    - atualiza as informações da tabela de processos
    - processo relativamente rapido(0,1ms)
2. Escalonador(Scheduler):
    - Escolhe a proxima tarefa a ser escolhida para ir pro processador
    - Parte mais demorada

## Quando o escalanador é chamado ?
Quando um novo processo é criado, para saber onde ele vai entrar na fila de execução

Quando um processo chegou ao fim e um novo precisa ser executado

Quando um processo esta bloqueado e algum deve ser executado

## Quando E/S ocorre, o Escalonador deve:
1. Executar o processo que estava esperando esse evento
2. Continuar o processo que já estava sendo executado
3. Executar um terceiro processo que estava pronto

## Categorias do Escalonador
1. Preemptivo
    - Quando o processo para de execução para resolver uma interrupção
    - Provoca uma interrupção forçada de um processo para executar outro
2. Não preemptivo
    - Quando o processo continua a execução independente da interrupção
    - condições de paradas:
        - termine de execitar
        - solicite uma operação E/S
        - libere explicitamente o processador

## Algoritmos de Escalonamento
1. Sistema Batch(Lote)
    - FIFO(First-Come First-Served)
        + Não preemptivo
        + Primeiro que chega é o primeiro a ser executado
        + Segue a ordem de requisição
        + Facil de entender e programar
        + Desvantagem:
            - Ineficiente quando há processos que demoram a sua execução
        ![Chamada](./images/Screenshot%20from%202022-09-12%2001-33-45.png)
        Nessa foto, ele vai seguindo a fila de execução até terminar.
    - SJF(Shortest Job First)
        + Não Preemptivo
        + Escolhe as tarefas mais curtas a serem executadas
        + Deve-se prever o tempo de execução do processo
        + Menor processo da lista é executado primeiro
        + Menor turnAround(médio)
        + Desvantagem:
            - Todos os jobs precisam ser conhecidos de antemão
            - Se jobs curtos começarem a chegar, os mais longos demoram de executar
        ![Chamada](./images/Screenshot%20from%202022-09-12%2001-42-08.png)
        Na foto, a esquerda é FIFO e na direita é SJF, percebe-se que na direita é mais rápido a execução de todos
    - SRTN(Shortest Remaining Time Next)
        + Preemptivo
        + Versao preemptiva do SJF
        + Processos com menor tempo são executados primeiro
        + Ele compara o tempo de execução da nova tarefa com o tempo total da tarefa que esta sendo executada, se for menor ele executa a tarefa nova
        + Desvantagem:
            ![Chamada](./images/Screenshot%20from%202022-09-12%2001-50-34.png)

2. Sistema Interativos
    - Round-Robin
        + Preemptivo
        + Cada processo tem um quantum de tempo
        + Ao final desse tempo, o processo é suspenso e voltado para o final da fila e outro processo é colocado em execução
        + Tambem suspenso em caso de interrupção
        ![Chamada](./images/Screenshot%20from%202022-09-12%2002-47-28.png)
        + Problema:
            - Tempo de chaveamento(dispatcher e sheduler) de processos
        + quantum:
            - Se for muito pequeno, diminui a eficiencia da cpu
            - Se for grande, tempo de resposta é comprometido
    - Por prioridade
        + Preemptivo
        + Cada processo possui uma prioridade
        + O processo de maior prioridade é executado primeiro
        + Prioridades sao atribuidas dinamicamente pelo o sistema ou estaticamente
        ![Chamada](./images/Screenshot%20from%202022-09-12%2002-57-34.png)
        Dentros das filas, os processos sao executados via round-robin
        ![Chamada](./images/Screenshot%20from%202022-09-12%2002-59-37.png)
    - Multipla Filas
        + Preemptivo
        + Tendo varias filas, os processos sao alocados para essas filas de acordo com a quantidade de quantum dado para ele
        + Maior quantum, menor prioridade
        + Menor quantum, maior prioridade
        + O sistema vai dando quantum progressivamente para o processo caso ele nao consiga terminar a execução com quantum que ele tinha
        ![Chamada](./images/Screenshot%20from%202022-09-12%2003-05-45.png)
3. Sistema Tempo Real
    - Hard Real Time
        + Atrasos nao sao tolerados
    - Soft Real Time
        + Atrasados sao eventualmente tolerados

    - Em ambos os casos, o comportamento em
    tempo real é conseguido dividindo o programa em uma
    série de processos, cada um dos quais é previsível e conhecido antecipadamente. Esses processos geralmente
    têm vida curta e podem ser concluídos em bem menos
    de um segundo.

    - Eventos causam execução de processo
    - Eventos podem ser classificados como:
        + Periodicos: ocorrem em intervalos regulares de tempos
        + Aperiodicos: ocorrem em intervalos irregulares de tempos
    - Algoritmos de tempo real pode ser classsificados como:
        + Estaticos: as decisões do escalonamento sao realizados antes do sistema começar a rodar
        + Dinamicos: as decisões de escalonamento sao realizados em tempo de execução
    