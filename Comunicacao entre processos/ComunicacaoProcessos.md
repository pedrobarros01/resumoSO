# Comunicação entre processos
Processos precisam saber comunicar com outros processos, para poder trabalhar coletivamente e alcança um resultado e objetivo em comum.

Ela é mais eficiente, se for estruturada e não utilizar interrupções

Mas qualquer comunicação gera conflito, um exemplo disso é quando `processo1` vai tentar se comunicar com o `processo2`que não esta pronto ainda de se comunicar. Essa comunicação é feita por `system calls`, onde o `processo1` é botado pra dormir até que o `processo2` esteja pronto para assim acordar o processo1 e realizar a comunicação.

Existe uma sincronização adequada para ocorrer a comunicação
## Condições de corrida
- Os processos se comunicam atraves de uma area de armazenamento comum
- Essa area pode estar na memoria principal(ex: variaveis em comum entre 2 threads ou pode ser um arquivo compartilhado)
- ![Exemplo](./images/Screenshot%20from%202022-09-16%2012-14-38.png)
```
nessa figura, o processo origem envia um dado X para a area comum e o processo destino vai pegar esse dado X para ele. Mas precisa ver uma syncronização entre eles para o processo destino poder saber exatamente se o dado X está disponivel.
```
- Mas existe problema que se chama `condição de corrida`:
    - acontece quando 2 ou mais processos tentam acessa recursos compartilhados concorrentememte(acessar ao mesmo tempo)
    ```
    a = d + c
    x = a * y(a variavel 'a' é compartilhada, chamada de região critica ou condição de corrida)
    ```
## Exemplo de condição de corrida
1. Fila de impressão de arquivo:
    - Imagine 2 processos(A e B) querendo colocar seus arquivos na fila.
    - Bora dizer que o processo A começa a executar, quando ele ta executando ele le a variavel da fila que indica onde pode inserir o arquivo para impressão, mas ele sofre uma preempção.
    - O processo B começa a sua execução e le essa mesma variavel e consegue botar o seu arquivo no indice da fila indicada pela a variavel e incrementa essa variavel.
    -Quando o processo A volta, ele esta com o indice antigo guardado. Assim ao colocar o arquivo nessse indice da fila ele sobrepõe o arquivo do processo B, ferrando tudo.

## Exclusão mutua e região critica
- Região critica: local onde são efetuados acessos a recursos compartilhados entre 2 ou mais processos.
- Exclusão mutua: Restrição de outros processos a entrarem na região critica quando ja tem um processo nela.
Só um processo pode acessa essa região critica de cada vez.
Quando um processo entra na RC(região critica), ele só pode sair de execução quando ele sai da RC. assim podendo realizar a exclusao mutua.
![Exemplo](./images/Screenshot%20from%202022-09-16%2013-14-55.png)
![Exemplo](./images/Screenshot%20from%202022-09-16%2013-21-35.png)
Assim com a exclusao mutua e a regra de o processo so sair em preempção quando sair da RC, temos uma solução de syncronização entre processos.
- Essa solução é valida para threads, já que elas compartilham o mesmo recurso tambem

## Regras para programação concorrente (p/1 uma boa solução)
1. Dois processos nunca podem estar simultaneamente dentro da RC
2. Não se pod fazer suposições em relação a velocidade  e os numeros da CPUs(nao pode funcionar so pra multicore ou singlecore, tem que ser nos dois )
3. Um processo que esta fora da RC não pode bloquear um processo que quer entrar na RC(só pode bloquar caso um esteja na rc)
4. Um processo não pode sofrer inanição(esperar infinitamente para entrar na região RC)

## Soluções de Exclusao Mutua
1.Busy WAiting
2. Primitivas de sleep/wakeup
3. Semaforos
4. Monitores
