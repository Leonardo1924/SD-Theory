# Acordo 

## Commit Transacional 
  Coordenação de múltiplas ações irreversíveis ao longo de um sistema dsitribuído
  Transações distribuídas com 2-phase commit(2PC) suportam o acrdo em sistemas com falhas
    Limitado ao crash-recovery
   Muito utilizado no middleware em contexto empresarial para a integração da aplicação
 
 ## Replicação
  Mantém diversas cópias acerca dos mesmos dados ous serviços
    -> Distribui a carga para permitir escalabilidade
    -> Tolera falhas do servidor
    
  Solução naive: escrever e depois propagar
    -> divergente
    -> volta atrás no tempo
    -> não é ft
  
  2PC = Avança para a próxima fase quando possuir todos os dados (tolera reboots, mas não crashes)
  
  ## Quorum
  
  Regras para dados replicados:
    -> Nr + Nn > N -> os readers obtêm o último valor
    -> Nw . N/2 -> Conflito entre writers concorrentes
    
  Regras adicionais para tolerar falhas assumindo no máximo f falhas:
    -> Nr + f <= N -> readers nunca bloqueiam
    -> Nw + f <= N -> writers nunca bloqueiam
    
  Pode ser configurado para assegurar ambos ou nenhum
  
  A solução típica é possuir uma maioria.
   -> Nr = nw = f + 1
   N = 2f + 1 
   
 ## Eleição do Lider ( Bully Algotithm)
 
 O processo que pretende ser o líder (suspeita que não existe um lider), faz broadcast do seu endereço para todos os outros
 Se for recebido um endereço > local,  conhece-se o novo lider
 Se endereço recebido < local, faz-se broadcast do endereço local (bully)
 Assim sendo, podem existir múltiplos lideres ou nenhum
 
 ## Consenso 
  Problema de acordo distribuido em que os processos propõem alternativo e decidem da seguinte forma:
    -> Todas os participantes corretos obtém uma decisão
    -> Todas as decisões são iguais
    -> a decisão é uma das alternativas propostas
    
  Como resolver o problema?
    -> 2PC + Quorum + Bully = Consenso Paxos
    
## Paxos
   Processos têm 3 roles principais:
   -> Proposers(com um lider) -> coordenam a votação
   -> Acceptors -> votam acerca de uma decisão
   -> Learners -> informados acerca da da decisão
  Normalmente, cada participante recebe os 3 roles
  

1ª fase é a eleiçãõ do lider + leitura quorum
  Um proposer tenta tornar-se lider
  Utiliza (time, id) para efetuar o bully aos outros -> Propose (1a)
  O acceptor promete esquecer os líderes anteriores -> Promise (1b)

Um lider é estabelecido com a maioria das promessas e usa o valor lido ou , caso não haja nenhum, a sua própria opinião como valor candidato

2ª fase é o quorum write:
  -> Accept(2a)
      
      O lider impõe a sua própria decisão
  
  -> Accept(2b)
    
     Aceite se o lider não foi deposto
     O acceptor confirma a decisão ao líder e aos learners
  
  Ao receber a maioria das mensagens a decisão está feita
  Pode sempre recuperar de uma minoria de processos falhados caso exista um líder confiável

Piores casos?
  Não há lideres confiáveis (sistema instável)
  Mais do que uma minoria de falhas ( falhas catastróficas)

Nota: Em ambos os casos o algoritmo para mas não produz decisões inconsistentes.

Aplicações do Consenso

  Replicated State Machine : Réplicas executam a mesma sequência de comandos
     -> Clientes emitem comandos para os proposers
     -> Learners executam cada pedido decidido como sendo o seguinte e enviam a(s) resposta(s) aos clientes
  
  Comunicação de grupo: Acordo em processos operacionais que recebem cada mensagem
    -> A decisão é da responsabilidade dos membros do grupo e as mensagens são vistas por todos os participantes.
    
    
        

