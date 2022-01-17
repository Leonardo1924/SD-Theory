# Locks
  Ferramenta que evita que várias threads corram ao mesmo tempo a secção crítica do código.

## Blocos synchronized
  ```Java
    class Counter { 
      int value = 0;
      void increment(){
          synchronized(this) { value++; }
        }
  ```
  Para um bloco synchronized(obj) {... instruções ... }
    1. Uma thread `adquire o primeiro o lock` sobre o objeto. A execução bloqueia se o lock for detido
    por outra thread, e só é retomada depois de adquirido o lock.
    2. Após a aquisição do lock, é executado o código dentro do bloco synchronized.
    3. É libertado no final o lock que tinha sido colocado no obj. Outra thread(apenas uma) bloqueada na mesma região do código 
    poderá agora adquirir o lock.
    
  Um método de instância com o modificador synchronized tem implícita a aquisição de um lock sobre o objeto à a entrada do método 
  a sua libertação no retorno.
  
  Usando o modificador o contador passa a mostrar um comportamento correto e determinista.

## ReentrantLock
    ```Java
    ReentrantLock rl
      = new ReentrantLock();
    
    void increment() {
    rl.lock();
    try {
      value ++;
    }
    finally {
       rl.unlock();
      }
    }
    ```
   - Podemos usar também a biblioteca do java (java.util.concurrent.locks.ReentrantLock) onde operações de aquisição e
   libertação do "lock" são invocadas explicitamente no código fonte e sem validação de âmbito sintático 
   em tempo de compilação
   
   - `Boa prática:` a chamada a `unlock`deve residir num bloco `finally` em associação à região crítica, garantido que é libertado o "lock" em qualquer 
   caso, mesmo quando for lançada uma exceção dentro da região crítica. Em contraste, blocos synchronized garantem de raíz esse comportamento.
   
   ### ReentrantReadWriteLock
   - Permite por sua vez distinguir locks de escrita e locks de leitura
   - `Locks de escrita:` apenas uma thread pode deter o lock de escrita a dada altura. Outras threads à espera de obter o lock de leitura ou de escrita serão bloqueadas.
   - `Lock de leitura:` pode ser detido por várias threads simultaneamente, desde que não haja um lock de escrita. Outras threads à espera de obter o lock de escrita serão bloqueadas, mas não threads que queiram obter o lock de leitura.


    
