# Chamada de Sistema
Sendo a porta de entrada do modo kernel, ou seja, instruções que chamam modulo do sistema operacional para este gerenciar o HW e entregar a resposta que a aplicação precisa

Alterna o modo user para o kernel.

São executadas por instruções `traps`(interrupção em nivel de software), onde elas essas traps fazem 3 processos:
1. Manusear a chamada
2. Identifica essa chamada
3. Executar essa chamada
Passando assim de volta a resposta dessa chamada para a aplicação que chamou.
![Chamada](./images/Screenshot%20from%202022-09-11%2023-42-43.png)

Como interrupção normal, ele precisa voltar para o ponto de onde parou

![Chamada](./images/Screenshot%20from%202022-09-11%2023-48-17.png)
![Chamada](./images/Screenshot%20from%202022-09-11%2023-50-35.png)

## Interface da syscalls
Encapsula a complexidade das syscalls para podermos realziar a utilização destas.
Serve para traduzir uma chamada de syscall para qualquer SO 

Motivos:
1. Portabilidade
    - independencia de plataforma
2. Esconder complexidade
3. Acrescimo de funcionalidades
