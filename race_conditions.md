# Partilha de memória e race conditions 

Observe o seguinte código 
  ```java
  class Counter{
    int value = 0;
    void increment() { value ++;} <-> int tm = value; //Leitura
                                      value = tmp + 1; //Escrita
    int getValue()   { return value;}
  ```
Assuma que se trata de um contador a ser usado por várias threads.

Problema: Incrementação do value não é atómica, pois decompõem-se em 
    1) Leitura do valor anterior;
    2) Escrita do valor atualizado;
Iremos perceber porque é que o valor do contador pode não refletir o número de incrementos!

Analisando o código percebemos que existe uma condição de corrida ("race condition") sobre o `value`:
Existem operações simultâneas de leitura/escritwa sobre o mesmo item de memória partilhada em que pelo menos uma das operações é uma escrita.

O incremento do valor torna-se então um exemplo de uma secção crítica, isto é , uma região de código onde no máximo uma thread deverá estar ativa.

Devemos portanto garantir que existe exclusão mútua entre threads no acesso à secção crítica.

![imagem](https://user-images.githubusercontent.com/62023102/149841814-2b508d8e-04e1-465d-a256-a05193e1b1ed.png)

- A execução deste código não é determinista e o resultado é por vezes incorreto.

- Em certas configurações o "bug" pode passar despercebido.

