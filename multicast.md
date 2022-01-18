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
