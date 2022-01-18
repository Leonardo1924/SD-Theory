# Comunicação 

Os sistemas de operação podem suportar a comunicação de dados entre os diferentes computadores envolvidos num sistema distribuído. (Protocolos mais populares: TCP/IP , HTTP).

![imagem](https://user-images.githubusercontent.com/62023102/149854048-88148383-9939-4891-90d1-ae253f9541c4.png)

  
## UDP 
  - Comunicação por mensagens.
  Mensagens podem-se perder, duplicar e chagar fora de ordem

## IP Multicast (UDP MultiCast)

Comunicação por mensagens com múltiplos recetores.

Cliente envia mensagem para endereço do grupo. Qualquer processo se pode juntar ao grupo para receber mensagens.

Mensagens podem-se perder, duplicar e chegar fora de ordem.

## TCP 

Dados transmitidos como fluxo contínuo.

Dados chegam de forma fiável a menos que o stream seja quebrado.

## HTTP 

Comunicação pedido/resposta sobre TCP, invocando URL

Dados chegam de forma fiável a menos que o stream seja quebrado

## HTTP ASSÍNCRONO

Comunicação pedido/resposta, com resposta a ser recebida de forma assíncrona

## WEB Sockets

Comunicação full-duplex sobre TCP entre clientes e servidores Web
    Permite notificações dos servidores, streaming.
    
# Comunicação no nível MiddleWare

