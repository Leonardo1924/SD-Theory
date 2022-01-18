# Invocação Remota

É possível estruturar uma aplicação distribuída usando como base as interações através da troca de mensagens entre processos

Os problemas são:
    é complicado e chei de detalhes não relevantes
    os programas ficam estruturados em função dos protocolos e da lista de mensagens que sabem processar
    
Muitas linhas de código são repetitivas, não contêm nenhum significado aplicacional específico e referem-se ao processamento 
das comunicações:
    criação de sockets e sua associação aos processos
    criação, preenchimento e interpretação das mensagens
    seleção do código a executar consoante o tipo da mensagem recebida
    gestão de temporizadores/tratamento das falhas
    
Não se poderá automatizar as interações cliente/servidor?

## Invocação Remota de Procedimentos
  Num programa definido numa linguagem imperativa, definem-se funções/procedimentos para executar uma dada operação
  
  Uma extensão natural num ambiente distribuído consiste em permitir a execução de procedimentos noutra máquina
      Ex. RPC
  
  Se os procedimentos estiverem definidos no âmbito de um objeto, chama-se invicação remota de métodos.
      Ex. RMI
  
  ## RPCs
  
  ![imagem](https://user-images.githubusercontent.com/62023102/149953609-66420632-4077-44d0-9110-89a0a36c1046.png)
  
  Modelo 
    - Servidor exporta interface com operações que sabe executar
    - Cliente invoca operações que são executadas remotamente e (normalmente) aguarda pelo resultado.
    
### Propriedades
   - Extensão natural do paradigma imperativo/procedimental a um ambiente distribuído -> cahamada síncrona de funções
   - Esconde detalhes de comunicação (e tarefas repetitivas)
        1) Construção, envio , receção e tratamento de mensagens.
        2) Tratamento básico de erros ( devem ser tratados ao nivel da aplicação).
        3) Heterogeneidade da representação dos dados.

   - Simplifica disponibilização de serviços
        1) Interface bem definida, facilmente documentável e independente dos protocolos de transporte.
        2) Pode ser aumentado com um Sistema de registo e procura de serviços.

RCPs: Como implementar

![imagem](https://user-images.githubusercontent.com/62023102/149968178-0b5a5aaa-b5c7-4672-8478-6717ef8931e4.png)

![imagem](https://user-images.githubusercontent.com/62023102/149968284-db530a9a-e11e-42f7-b3be-f956927baee9.png)

![imagem](https://user-images.githubusercontent.com/62023102/149968337-d9b497c8-0366-437c-9354-d7868c936f8a.png)

![imagem](https://user-images.githubusercontent.com/62023102/149968375-9866fb8f-566c-444b-89ae-c5f33b222099.png)

![imagem](https://user-images.githubusercontent.com/62023102/149968414-1b37b4b6-0832-492e-8e7f-8f248e1e4315.png)

![imagem](https://user-images.githubusercontent.com/62023102/149968473-ddefd0ad-a6fc-48c3-93a4-ae64c944b91c.png)

![imagem](https://user-images.githubusercontent.com/62023102/149968511-50d95db3-7ce7-42fe-aedf-38c02afa5ad6.png)

![imagem](https://user-images.githubusercontent.com/62023102/149968560-bd180e76-0afc-4981-9d10-b4835c05db80.png)

## Automatização do Processo

Nos sistemas de RPC/RMI, o código da comunicação é transparente para a aplicação.
    Stub do cliente inclui funções do cliente que efetuam a comunicação com o servidor para executar o 
    método no servidor.
    Stub do servidor inclui código de comunicação para esperar invocações e executá-las, devolvendo o resultado.
    Em RMI, o stub do cliente é gerado automaticamente.
    
 Stub é um pedaço de código que é usado para converter parâmetros durante uma ligação remota RPC.

## Interface Definition Languages(IDL)
   IDLs são linguagens que permitem definir interfaces de servidores/objetos remotos, especificando:
        Tipos e constantes
        Interface do serviço - assinatura das funções/procedimentos.
      
Os IDLs são usados apenas para definir as interfaces, não o código das operações
    Por vezes, esta distinção é difícil de fazer porque os IDLs estão integrados com linguagem
    Em certos sistemas, a interface pode não ser definida autonomamente
    
## IDLS - AProximações Possíveis
   Usar um sub-conjunto de uma linguagem já existente (EX: RMI)
   
   Definir uma linguagem específica para especificar interfaces dos servidores/obejtos remotos
   
   Necessidade de mapear o IDL e as linguagens de desenvolvimento dos clientes/servidores.
   
## Codificação dos Dados - Problema

Como representar dados trocados entre os clientes e os servidores?

Diferentes sistemas representam os tipos primitivos de formas diferentes
    Inteiros armazenados por ordem diferente em memória
    Diferentes representações para números reais
    Caracteres com diferentes codificações

## Representação dos Dados - Tipos Complexos
   Aplicações manipulam estruturas de dados complexas
     Ex: representadas por grafos de objectos.
     
   Mensagens são sequências de bytes
   
   O que é necessário fazer para propagar estrutura de dados complexa?
        É necessário convertê-la numa sequência de bytes
        Por exemplo, para um objecto é necessário:
            Converter as variáveis internas, incluindo outros objectos
            Necessário lidar com ciclos nas referências
          
Marshalling – processo de codificar do formato interno para o formato rede
Unmarshalling – processo de descodificar do formato rede para o formato interno

## Aproximações À codificação dos dados.
 ### Utilização de formato intermédio independente (network standard representation)
   Emissor converte da representação nativa para a representação da rede
   O receptor converte da representação da rede para a representação standard
        
 ### Utilização do formato do emissor (receiver makes it right)
   Emissor envia usando a sua representação interna e indicando qual ela é
   Receptor, ao receber, faz a conversão para a sua representação
   
## JSON(JavaScript Object Notation)
   Json é uma alternativa ao XML, permite descrever estruturas de dados complexas em formato de texto
   
   Tipos primitivos -> Number, String , Boolean
   Tipos complexos -> Array, Object(mapa chave / valor)
   
## ProtoBuf ( Google Protocol Buffers)
 Define-se um tipo de mensagem através de uma linguagem própria, neutra.
 
 Dados passam na rede em formato binário
 
 Compilador cria código para serializar/deserializar dados estruturados
 
 Resultado: menor dimensão, mais rápido a processar.
 
## Passagem de Objetos Remotos em Parâmetro

   Nos sistemas de RMI é , em geral, possível passar (referências para) objetos remotos em parâmetro (ou como resultado de uma operação)
   
   Em Java RMI pode-se enviar uma referência para um objeto remoto:
        - Passando como parâmetro/resultado uma referência remota – neste caso, uma cópia da referência remota é enviada.
        - Passando como parâmetro/resultado o objecto servidor – neste caso, uma referência para o objecto remoto é enviada (e não o próprio objecto) –> passagem por referência.
        
   Uma referência remota inclui, pelo menos, a seguinte informação:
        Endereço/porta do servidor
        Tipo de servidor
        Identificador Único
        
Nota: A referência remota não deve incluir diratamente a localização do objeto
        
        
 
   
   
   
