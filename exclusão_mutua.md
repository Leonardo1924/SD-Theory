# Exlusão Mútua:

Nas zonas críticas não poderão estar nunca processos em simultâneo.

Algoritmo de Peterson

É um algoritmo que garante a exclusão mútua de dois processos.

- boolean flag[2];
- int vez;
- (flag[j] == false || vez = i) => Pi pode entrar na zona crítica.

![imagem](https://user-images.githubusercontent.com/62023102/149848894-15c94f7f-f87b-4513-8634-50e43e8dd032.png)

Livre de DeadLocks
Livre de Starvation
