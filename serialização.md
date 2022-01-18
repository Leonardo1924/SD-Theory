# Serialização 

- Corresponde a transformação de um objeto Java para uma sequência de bytes.
- Informações de tipo e classe dos objetos são incluídas na forma serializada, permitindo assim a reconstrução dos obejtos sem conhecimento prévio das suas classes.
- Processo recursivo: serializa todos os objetos referenciados pelo objeto em questão
- Classes precisam implementar a inteface Serializable
- Objetos remotos: a referência é serializada.

## Forma de disponibilização ao usuário
  - Classes `ObjectOutputSream` e `ObjectInputStream` e seus respectivos métodos `writeObject` e `readObject`.
  - Classe do objeto implementa a interface Serializable.

## Contéudo do formato serializado
  - Nome da classe
  - Versão da classe ( quando são feitas alterações ) 
  - Referência a outros objetos (handles)
  - Valores das instâncias das variáveis.

Objetos (instância de uma classe Java) e valores de dados primitivos podem ser passados como argumentos e resultados de invocações de método.

### Exemplo 
  ```java
  public class Person implements Serializable{
    private String name;
    private String place;
    private int year;
    public Person(String aName, String aPlace, int aYear){
        name = aName;
        place = aPlace;
        year = aYear;
      } //seguido dos métodos para acessar as variáveis de instância.
    }
  ```
Serialização e desserialização geralmente são operações feitas automaticamente pelo middleware.

Java oferece meios para o programador personalizar a serialização.

Exemplo é o uso da palavra-chave `transient` que serve para informar que uma variável não deve ser serializada
  - Arquivos ou sockets
