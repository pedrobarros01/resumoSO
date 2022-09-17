# Problemas classicos de comunciação entre processos
Foram criados para ajudar na criação de requisitos para uma boa solução.

Ajudam a modelar um software em paralelo.

## Produtor e Consumidor
- Ajudou a modelar os principais protocolos da internet
- Já foi citado e explicado na aula de `sleep` e `wakeup`
- Tendo 2 entidades: `produtoras` e `consumidoras`
- Sincronização ocorre em função do `buffer`
- ![Exemplo](./images/Screenshot%20from%202022-09-17%2012-27-53.png)
- `Produtor`: cria produtos para armazenar no `buffer`
- `Consumidor`: consome produtos do buffer, diminuindo do prórpio
- Com isso, o buffer cheio o `produtor` dorme, o buffer vazio o `consumidor` dorme

## Jantar dos filosofos
- Dado 5 filosofos(processo) e 5 hashis(RC)
- ![Exemplo](./images/Screenshot%20from%202022-09-17%2012-33-29.png)
- Cada filosofo contem 1 prato
- Cada filosofo precisa de 2 hashis para comer o que tem no prato
- Entre cada par de pratos tem 1 hashi
- os hashis precisam ser compartilhados sincronizadamente entre os filosofos.
- os filosofos comem e pensam, alternadamente
- quando comem, pegam 1 hashi por vez
- se conseguirem pegar 2 hashis, comem por um instante e depois largam os hashis
- mas como evitar que eles fiquem bloqueados ? Precisa de uma sincronização entre eles, onde eles possam comer e não sofrer inaninação
- Solução 1:
    - Alterna entre:
        - 1° pensar
        - 2° pegar os hashis
            - 2.1° pegar o direito(lock direito)
            - 2.2° pegar o direito(lock esquerdo)
            - logico, se tiver os 2 disponiveis
        - 3° comer
        - 4° deixar os hashis
        - ![Exemplo](./images/Screenshot%20from%202022-09-17%2012-43-40.png)
    - Essa solução funciona com um numero limitados de filosofos
    - pode levar a ter uma inanição
    - Problemas que pode ter essa solução:
        - DeadLock - os filosofos pegam um unico hashi ao mesmo tempo e ninguem come    
        - Starvation - os filosofos ficam indefinidamente pegando hashis simultaneamente
- Solução 2:
    - Uso da exclusao mutua
    - Uso do semaforo binario, um mutex
        - Basicamente, pela definição de semaforo mutex, ele ve quem tem interesse em utilizar o hashi, quando um filosofo que tem interesse pega 2 hashis ele da um `down` diminuindo o semaforo para 0. Assim, fazzendo os outros filosofos dormirem, ao liberar 2 hashis, ele da um `up`, liberando para um proximo filosofo.
    - Problema: so um come por vez
- Pra que estudar esse problema:
    - Util para modelar processos que competem por acesso exclusivo de recursos limitados
    - Protocolo da ethernet usa parte desta solução para modelar o envio de dados na rede



## Leitores e Escritores
- Modela acesso a uma base de dados
- Tendo entidades: `leitores` e `escritores`
- `leitores`: leem dados
- `escritores`: escrevem dados
- Se um processo necessita escrever na base de dados, nenhuma outra entidade pode estar tendo acesso a ela, nem mesmo leitura.
- Assim tendo um cenario:
    - Se os `escritores`entram na base dados eles tem que bloquear ela
    - Já nos leitores:
        - Se for o 1° leitor, deve bloquear a base para evitar o `escritor`
        - Se ja houver leitor na base, basta usar ela
        - Ao sair, os leitores devem verificar se ha outro leitor:
            - Se não houver, desbloqueia a base
            - Se houver, deixa bloqueada
- Mas essa solução pode apresentar problema de inanição:
    - Onde esse problema se caracteriza do fato se a base ja estiver bloqueada por leitores e chegar um escritor, ele não pode entrar e vai esperar o acesso, mas se chegar varios e novo leitores e entrarem, o escritor ficara esperando infinitamente.
    - Uma solução pra isso, é você suspender os proximos e novos leitores que querem entrar para assim o escritor, quando sair os que estao dentro da base, poder fazer seu papel dentro da base.