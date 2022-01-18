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

Implementa sistema de comunicação recorrendo às primitivas de comunicação base

Fornece propriedades adicionais, atrasando a entrega das mensagens

`Definição:` Entrega de uma mensagem num sistema de comunicação representa a ação do sistema disponibilizar a mensagem para ser lida pelas aplicações

Atrasar a entrega de uma mensagem pode, por exemplo, permitir que a ordem de entrega das mensagens seja diferente da ordem de chegada.

## Pontos importantes na comunicação MiddleWare
   - Tipo de Interação
   - Sincronização
   - Persistência
   - Fiabilidade

## Tipo de Interação
  Comunicação uni-direcional -> Comunicação apenas num sentido: emissor -> recetor
  Comunicação bi-direcional -> Comunicação nos dois sentidos
  
## Sincronização
  `Comunicação assíncrona:` o emissor só fica bloqueado até o seu pedido de envio ser tomado em consideração.
  O recetor fica bloqueado até ser possível receber dados:
    Em geral, o sistema de comunicação do recetor armazena (algumas) mensagens caso não exista nenhum recetor bloqueado no momento da sua receção. Assim, funciona com um buffer entre o emissor e o recetor.
    É possivel variante em que o recetor não fica bloqueado e devolve um erro ou a receção é efetuada em segundo plano.
    
   `Comunicação síncrona:`
        O emissor fica bloqueado até:
          - o recetor "receber" os dados - comunicação síncrona unidirecional
          - receber a resposta do recetor - comunicação pedido/ resposta ou cliente / servidor
        O recetor fica bloqueado até ser possível consumir dados.
        
## Persistência 
 `Comunicação volátil:` Mensagens apenas são encaminhadas se o recetor existir e estiver a executar, caso contrário são destruídas.
 
 `Comunicação persistente:` Mensagens são guardadas pelo sistema de comunicação até serem consumidas pelos destinatários, que podem não estar a executar. Mensagens são guardadas num recetáculo independente do recetor.
 
## Fiabilidade

  `Comunicação fiável:` O sistema garante a entrega das mensagens em caso de falha temporária.
  
  `Comunicação não-fiável:` em caso de falha, as mensagens podem-se perder.

## Comunicação Síncrona Unidirecional --- Exemplo.
  ![imagem](https://user-images.githubusercontent.com/62023102/149928801-bbadde99-8566-4c7e-a5f8-72079eb9bbfc.png)
  
  O emissor fica bloqueado à espera de o receptor estar disposto a receber a mensagem.
  Implementação exige envio de mensagem com informação de recepção para o emissor.
