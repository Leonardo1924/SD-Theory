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
