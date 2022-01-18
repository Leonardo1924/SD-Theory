# Naming/DHT

## Coordenação

  Sistemas distribuídos são, geralmente, definidos como:
    -> Coleções de elementos computacionais autónomos
    mas
    -> Resultam num sistema singular coerente
    
  É possivel visto que os elementos computacionais coordenam-se de forma a efetuar uma função coerente.
  
## Aprendizagem de Outcomes
  Reconhce a forma como problemas concretos do mundo se mapeiam em problemas genéricos de sistemas distribuídos.
  Recomenda uma solução que serve no ambiente fornecido
    -> Conhece os trade-offs de cada algoritmo
    
 ## Naming
  -> Como encontrar o servidor e os endereços de serviços?
  -> Endereços não são conveninentes para a leitura de humanos
  -> É um desafio nos sistemas distribuídos.
  
## Flat naming:
  Local Server:
    -> Um servidor mantém um map que associa nomes e endereços
    -> Servers registam o nome
    -> Clientes pedem o nome
  
  Broadcast
    -> Envia uma pergunta para toda a rede: " Quem é X?"
    -> Alvo responde: "Sou X."
    
   Não é escalável para um grande número de clientes e servidores
   Não permite autoridade administrativa distribuída
   
## Naming Hierárquico
  LookUp eficiente (aproximadamente log N)
  Permite autoridade administrativa distribuida
  Continua a existir um bottleneck e SPOF no nodo raiz
  
## Hash Table Distribuida(DHT)
  Não existe um nodo raíz
    -> sem bottleneck e SPOF
  Lookup eficiente (aprox. log N)
  
