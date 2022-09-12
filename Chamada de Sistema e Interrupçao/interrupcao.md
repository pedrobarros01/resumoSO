# Interrupção de Hardware
São interrupções que não sao causadas por aplicações, ou seja, são causadas em nivel externo/HW
exemplo:
1. um sinal eletrico no HW
    - causa: dispositivos E/S ou o clock
O tratamento é exatamente o mesmo que o trap, volta pro mesmo local que parou.
![Chamada](./images/Screenshot%20from%202022-09-12%2000-05-02.png)

## Interrupção vs Trap
### Interrupção
- Evento externo ao processador, ou seja, do HW.
- Gerada por dispositivos que precisam do SO.
- Não precisa estar relacionada ao processo que estã 
rodando
### Traps
- Evento interno ao processador, ou seja, via Software.
- Causados pelo o processo corrente no processador(seja por chamada do SO ou por instrução ilegal)