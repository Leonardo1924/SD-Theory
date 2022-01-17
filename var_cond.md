# Uso de notificações em monitores e de variáveis de condição

## Sincronização usando notificações

![imagem](https://user-images.githubusercontent.com/62023102/149845431-3a13f4d8-d5cd-4944-8fe5-b17d6da82d27.png)

- Além do suporte de  "locks" via monitores  em blocos synchronized, em java temos métodos baseados em notificações sobre monitores definidos na classe java.lang.Object.
- `obj.wait():` Leva a que a thread em contexto bloqueie à espera de uma notificação sobre o monitor de obj - tipicamente existe uma "condição de espera" associada.
- `obj.notify() e obj.notifyAll():` permitem entregar notificações a threads à espera de uma notificação em obj.
- Estes métodos podem servir para coordenação entre threads, como veremos através de um exemplo.

![imagem](https://user-images.githubusercontent.com/62023102/149845814-c1b25c17-6825-48d4-abe7-72750a7bb427.png)

- Fila com capacidade limitada, implementando internamente a estratégia de "array circular" e usual disciplina FIFO.
- `add()` deve bloquear enquanto fila estiver cheia.
- `remove()` deve bloquear enquanto fila está vazia.

![imagem](https://user-images.githubusercontent.com/62023102/149845974-f54a806f-df26-4622-9597-20e53092fa57.png)

obj.wait() - execução padrão para a thread em contexto
  1. Liberta o "lock" sobre obj e bloqueia. A thread é adicionada ao conjunto de espera - "wait-set" - de obj
  2. Aguarda envio de notificação associada ao obj.
  3. Depois de recebida a notificação, o "lock" tem de ser readquirido antes de finalmente wait() retornar.

obj.notify() e obj.notifyAll()
  - notify(): entrega notificação sobre obj a apenas uma das threads no "wait-set" de obj - a escolha é não-determinista.
  - notifyAll(): entrega notificação sobre obj a todas as threads no "wait-se" de obj.

## Padrão de espera com wait()
![imagem](https://user-images.githubusercontent.com/62023102/149846386-84f55b1b-0173-48ab-9993-7cd6665c4697.png)

O padrão de espera com wait deve ser do tipo acima!

Por duas razões:
  1. A recepção de uma notificação pode ser aguardada por várias threads com condições de espera distintas. 
  Cada thread deve portanto verificar que a sua condição de espera se verifica ou não após cada
retorno de wait().
  2. Existe a possibilidade de “notificações espúrias”, isto é, wait() pode retornar “espontaneamente” sem que tenha havido qualquer notificação! 
  O evento é raro mas possível. 

## Aplicação do ReentrantLock no exemplo anterior.

A fila pode na mesma ter apenas um "lock" associado. Podemos no entanto distinguir as condições de fila cheia e vazia explicitamente através de variáveis de condição (Condition).

Condition define métodos:
  - await() como funciomamento análogo a Object.wait()
  - Signal() e SignalAll() com funciomaneto análogo a Object.notify e Object.notifyAll()

O código fica mais "arrumado" e a sua análise fica facilitada

![imagem](https://user-images.githubusercontent.com/62023102/149847136-ee980b23-d92b-4015-9676-8abe37398427.png)

No entanto isto levanta questões, por exemplo, precisamos sempre de entregar notificações ou apenas quando a fila "deixa de estar vazia" ou "deixa de estar cheia" ? 

Por exemplo será correto ter em add() o seguinte: 
  ```java
    if(Size == 1)
      notEmpty.Signal();
   ```
 ![imagem](https://user-images.githubusercontent.com/62023102/149847346-b428f453-7981-4812-87ab-0057245025b4.png)

- Introduzimos um bug, levando a execuções com um problema conhecido como "lost wakeup". Note que acima t4 pode adquirir o lock antes de t2 o readquirir via await().

Aparecem assim problemas como "DeadLocks".
