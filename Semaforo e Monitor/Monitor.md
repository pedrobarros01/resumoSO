# Monitor
Primitiva de alto nivel para sincronizar processos e de fácil uso.

Conjunto de procedimentos, variaveis e estruturas de dados agrupados em um mesmo modulo.

O SO faz tudo por você, onde somente um processo pode estar ativo dentro do monitor.

Os outros processos ficam bloqueados ate que o monitor seja liberado.

Depende da linguagem de programação.

O compilador garante a exclusão mutua.

Existe em Java, mas não em C.

Todos os recursos compartilhados entre processos precisam estar dentro do monitor.

Tudo dentro do monitor é sincronizado.

![Exemplo](./images/Screenshot%20from%202022-09-17%2000-32-27.png)

Semantica nova para representar a exclusao mutua


## Limitações de Semaforos e Monitores
- Não sao boas para sistemas distribuidos
- Não proveem sincronização entre processos em maquinsas diferentes
- Monitores depende de uma linguagem de programação


## Monitores e Semaforos são locais(maquinas locais)