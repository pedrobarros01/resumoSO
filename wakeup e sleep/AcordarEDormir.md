# Sleep e WakeUp
Para solucinar os altos custos da espera ocupada, foi criado 2 chamadas de sistema chamadas `sleep`e `wakeup`.

Onde elas realizam o bloqueio e o desbloqueio dos processos.

Em vez do processo esta verificando se a RC está ocupada ou não, ele é botado para dormir com o `sleep`enquanto a RC está ocupada.

E quando a RC não está ocupada, usa-se o `wakeup` para "acordar" o processo que estava "dormindo"

## Contextualização do produtor e consumidor
![Exemplo](./images/Screenshot%20from%202022-09-16%2019-37-43.png)

Nessa figura, contém um buffer, produtor e consumidor.
Buffer é aquele que ira conter os dados produzidos(tem tamanho limitado)
Produtor é aquele que ira produzir esses dados
Consumidor é aquele que ira ler esses dados.
Dito isso, encontra-se um problema, caso o buffer atinja seu limite, o que o Produtor faz?
Mesmo paralelo com o consumidor, caso o buffer esteja vazio, o que consumidor vai fazer?
Assim, a solução desse problema, é justamente fazer o Consumidor e/ou Produtor pararem de consumir e/ou produzir durante um certo tempo. Com o `sleep` e `wakeup`. Quando o buffer estiver cheio, o produtor dorme, quando o buffer estiver vazio, o consumidor dorme.

## Implementando o Prod/Cons
- Buffer:
    - contém uma variavel `count` para controlar a quantidade de dados.
- Produtor:
    - Antes de colocar dados no Buffer, o produtor checa o valor de `count` para saber se esta cheio ou nao
    - Se estiver cheio, ele é botado para dormir
    - Caso contrário, `count` é incrementado colocando os dados no Buffer
- Consumidor:
    - Antes de retirar os dados no Buffer, o consumidor checa se `count` esta com 0
    - Se está, ele é botado para dormir
    - Se não, ele retira dados e decrementa `count`
- Sempre testa o outro processo se ele esta acordado, acordando-o se for o caso
![Exemplo](./images/Screenshot%20from%202022-09-16%2020-06-46.png)

## Problema que acontece...
Voltando na figura de cima, imagine que o consumidor está rodando e o count chega a 0, ele vai entrar no if count == 0, mas se ele sofrer uma interrupção antes de chamar sleep. Acontece que o produtor entra em execução, assim preenchendo o buffer. 
Quando a interrupção termina, ele volta para o consumidor e bota ele pra dormir, ativando de volta o produtor.
Assim, o produtor em execução preenche todo buffer ate o seu limite e é colocado para dormir tambem.
Fazendo os 2 dormirem infinitamente.
### Mas existe soluções para tratar isso
A solução é criar um `bit de wakeup` 
Quando o `wakeup` é mandado a um processo ja acordado, esse bit é setado
COm isso, verificamos se o bit esta setado, se for o caso ele é desligado e o processo continua acordado.
MAs é uma solução com muito custo, já que todo processo terá que ter esse bit.