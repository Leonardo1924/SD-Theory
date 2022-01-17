# DeadLocks

O exemplo anteriro do "lost wakeup" é uma instância dum problema geral chamado "deadlock".

Um deadlock é caracterizado pelo bloqueio eterno de uma ou mais threads.

Exemplos de causas de dealock:
  - Thread tenta adquirir um "lock" que nunca é libertado por outra thread.
  - Thread espera por uma notificação de uma outra thread que nunca chega a ser entregue
  - Secções críticas que não executam de forma atómica

## Exemplos:

![imagem](https://user-images.githubusercontent.com/62023102/149847767-a7e72158-7824-4a1d-90f9-da350d5aba0f.png)

- Primeira thread não chama unlock() por alguma razão
- Segunda thread não consegue portanto adquirir o lock

![imagem](https://user-images.githubusercontent.com/62023102/149847881-8f083171-2cf2-4ae8-b047-3b1ccda20bbb.png)

- Neste caso 2 threads esperam pelo término uma da outra.

![imagem](https://user-images.githubusercontent.com/62023102/149847919-9c62dd94-d084-4468-aee5-e142327cb21b.png)

- Neste as 2 thread bloqueiam-se mutuamente porque cada uma detém um lock que a outra precisa de obter para progedir na sua execução.

