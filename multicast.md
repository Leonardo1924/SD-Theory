# MultiCast

Na comunicação indireta , as mensagens não são endereçadas a processos de forma direta ou explícita.
  
  O envio e a recepção das mensagens está desacoplado, no espaço e no tempo
  
  O emissor e o(s) receptor(es) podem não se conhecer;
  O emissor e o(s) receptor(es) podem não executar em simultâneo;
  
A comunicação/interação é suportada por recurso a outras entidades
    - comunicação em grupo
    - message queues

# Formas de Comunicação

`Ponto a Ponto ou Unicast:` -> entre um emissor e um único recetor

## Multi-Ponto 

  broadcast ou difusão total [1xn] – envio de uma mensagem de um emissor para todos os receptores
  
  multicast ou comunicação em grupo ou difusão parcial [1xk ≤ n] – um emissor para um grupo de receptores
  
  funcional ou anycasting [1x1 de n] – envio de uma mensagem de um emissor para um de múltiplos possíveis receptores
  
  geocast [1xk de n] – envio de uma mensagem de um emissor para os
receptores de uma dada área geográfica

## Comunicação Multi-Ponto : TCP/IP
  A comunicação em difusão total, parcial e difusão funcional podem ser suportados diretamente ao nível da rede TCP/IP.
  
  ![imagem](https://user-images.githubusercontent.com/62023102/150003049-0702d90e-1807-4614-9202-de25f14f6dbd.png)
  
## Caracterização do MultiCast: Fiabilidade
   Multicast não fiável (unreliable multicast) – em caso de falha, não existem garantias sobre a entrega das mensagem aos vários elementos do grupo.
   
   Multicast fiável (reliable multicast) – uma mensagem enviada para um grupo ou é entregue a todos os membros correctos (que não falham) ou a nenhum.
   
   Uniform agreement: se algum processo que falha entrega a mensagem, todos os processos correctos devem entregar a mensagem.
   
## CARACTERIZAÇÃO DO MULTICAST: ORDEM
  Sem ordem – as mensagens podem ser entregues por diferentes ordens em diferentes processos.
  
  Ordem FIFO – as mensagens de um processo são entregues pela ordem de emissão em todos os processos
  
  Ordem causal – se m1 pode causar m2, m1 deve ser entregue sempre antes de m2
  
  Se duas mensagens forem emitidas pelo mesmo processo, considera-se que o envio da primeira pode causar o envio da segunda
  
  A entrega da primeira deve acontecer antes da entrega da segunda
  
  Se duas mensagens forem emitidas em processos diferentes, a primeira pode causar a segunda se for entregue antes do envio da segunda (ou transitivamente incluindo outras mensagens)
  
  Se uma mensagem não pode causar a outra, qualquer ordem de entrega respeita a ordem causal
  
  
   
