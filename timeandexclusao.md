# Tempo e ordenação de eventos

Num sistema distribído é impossível sincronizar os relógios de vários computadores a menos dum dado valor

Assim, é impossível usar o valor do relógio em diferentes computadores para saber a ordem dos eventos.

Num sistema distribuido, estamos em geral interessados em conhecer as relações de causalidade,i.e, saber quais os eventos que podem ter causado outros eventos.
  Pode ser um problema com 
    -> Ficheiros Partilhados
    -> Certos algoritmos

O relógio deverá ser ajustado com pequenas incrementações durante um longo período de tempo tornando-o mais rápido ou mais lento.

Na práica, existem alguns fatores imprevisíveis:
    -> Atrasos de transmissão
    -> Atrasos de processamento
    
 A melhor forma é ajustar com base num estimativa do delay de uma mensagem 
 
 ## Network time protocol (NTD)
   -> Assume que os delays são iguais = ((T2 * (-T1) + (T4 - T3))/2
   -> Repete várias vezes o processo e escolhe o delay mais pequeno
 
 ## Reference Base Synchronization (RBS):
   -> Assume que existe true broadcast medium ( delay aprox 0)
   
## Exlusão Mútua
  Solução num sistema distribuido?
  
  Considera-se:
    -> Número de saltos de mensagem necessários para entrar na secção crítica
    -> Balanceamento da carga
    
  Queue centralizada mantida por um coordenador
    -> 1 round-trip para entrar/ carga assimétrica
    
  Troca de um token num anel
    n/2 saltos para entrar/carga simétrica

  É dificil alcançar um algoritmo distribuído:
    -> Como os pedidos de locks concorrentes são recebidos por destinos diferentes em ordens diferentes,
    a segurança não é garantida.
    
  Aproveitar os relógios sincronizados
    Assumir ϛ > delay da transmissão + skew
    Considerarapenas mensagens entre t e ϛ, ordenadas através de uma timestamp.
    
 
Num sistema distribuído, como anteriormente mencionado, estamos interessados em conhecer as relações de causalidade.

Aperece então a relação "aconteceu antes" que capta a propriedade: 
  O evento e1 aconteceu antes de e2 se e1 pode ter causado e2.

![imagem](https://user-images.githubusercontent.com/62023102/149984808-ed080311-5106-409a-8a7e-3e70a4f2c2fa.png)

Num dado processo, a relação aconteceu antes pode definir-se pela ordem local de execução dos eventos locais.

## Relogios Lógicos (Lamport 1978)

Um relógio lógico é um contador monotonicamente crescente, usado para atribuir uma estampilha temporar a um evento.

Cada processo i, mantém um relógio lógico Li, que atualiza da seguinte forma:
  1) Seja e um evento executado no processo i, faz-se:
      Li := Li + X ( X > 0)
      T(e) := Li, com T(e) a estampilha temporal atribuída ao evento e.
  
  2) Se e = send(m), aplica-se a regra anterior e envia-se (m,t), com t = T(send(m))

  3) Se e = receive(m,t), faz-se Li = max(Li,t) e, de seguida, aplica-se a regra base 1
