# Semaforo
`semaforo` é uma variavel que é utilizada para controlar o acesso a recursos compartilhados.
Sincronizar o uso de recursos em grande quantidade.

Dado N Processos que vão utilizar uma impressora, com a variavel Semaforo, eu faço o seguinte. Cada vez que o processo é utilizado eu decremento o semaforo de forma sincronizada. Os processos que não conseguiram utilizar sao postos para dormir,  Os processos que liberaram a impressora se estão dormindo são acordados para poder utilizar ela.

Conta o numero de recursos ainda disponiveis no sistema.

`semaforo` == 0 -> não ha recurso livre
nenhum wakeup está armazenado, esperando esse recurso

`semaforo` > 0 -> recurso livre
Um ou mais wakeups estão pendentes

## 1° Operação(down)
- Ele indica se um recurso foi utilizado/ ou requisitado.
- Se um determinado processo requisita um recurso ele da um down no recurso, diminuindo o seu semaforo.
- Verifica se o semaforo é maior que 0
    - decrementa o semaforo em 1
- Se for 0, nao tem recurso livre, logo o processo que requisitou é colocado para dormir
- Executada sempre que um processo deseja utilizar um recurso compartilhado

## 2° Operação(Up)
- Se um determinado recurso é liberado do processo que utilizou
- O `semaforo` sofre um incrementação em 1 para liberar o recurso
- Se um recurso for liberado, eu tenho que saber se há processos dormindo nesse semaforo, para assim, escolher um desses processos e desbloque-lo(permitindo assim o uso do down)
- O resultado geral da variavel `semaforo` sempre será 0, já que, ao liberar o recurso, outro processo usrá down, diminuindo a variavel `semaforo`
- Executada sempre que o processo liberar o recurso

## Operações Atomicas
- Uma vez que uma operação se iniciou outro processo não poderá utilizar o semaforo.
    - Até que a operação seja liberada ou bloqueada
- O SO desabilita as interrupções enquanto testa o semaforo
- Cada semaforo é protegida pela syscall TSL
## Tipos de Semaforos
1. Semaforo Geral(counting semaphone)
    - Usado para contagem de recursos
    - Pode tomar qualquer valor inteiro não negativo
    - Funcionamento:
        - Inicializado com o numero de recursos disponiveis.
        - Cada processo que deseja usar o recurso executa o `down`
        - Quando o processo libera o recurso ele executa um `up`
        - Quando o semaforo é 0, quer dizer que todos os recursos estão sendo utilizados.Assim os processos que querem utilizar os recursos são colocados para dormir, e so acordar quando um outro processo der um `up`
2. Semaforo binario ou mutex ou booleano
    - Usado para implementar a exclusão mutua
    - Só pode ser 1 ou 0
    - Funcionamento:
        - Serve para conceder entrada na RC
        - Mutex é um variavel com 2 estados: 1(desbloqueado) e 0(bloqueado)
        - Quando uma thread precisa acessar a RC ele chama o `mutex_lock`
        - Quando termina ele chama `mutex_unlock`

## Implementação de Semaforo
1. Espera Ocupada
    - não é a melhor forma
    - down: espera até que semaforo > 0 e entao decrementa semaforo
    - up: incrementa semaforo
    - ![Exemplo](./images/Screenshot%20from%202022-09-17%2000-11-19.png)
2. Associando uma fila `Q` a cada semaforo `s`
    - Então existe uma fila para cada recurso.
    - down: se `s` > 0, então decrementa `s`(recurso requisitado)
        - Caso contrario, bloqueia o processo e é colocado na fila `Q`
    - up: se a fila estiver vazia então incrementa `s`, se não, acorda o primeiro processo da fila, removendo-o