# Arquitetura do sistema

- Organização de um sistema (complexo) em componentes mais simples com funcionalidades/responsabilidades próprias.
- Define os componentes, o que fazem, onde estão e como interagem entre si.
- Terá implicações em diversas propriedades do sistema: desempenho,fiabilidade e segurança do sistema.

![imagem](https://user-images.githubusercontent.com/62023102/149679773-a55be300-0f54-47ef-905e-c707c1deff0e.png)

Sistema em que os processos podem ser dividos em dois tipos, de acordo com o seu modo de operação:
  - Cliente: programa que solicita pedidos a um processo servidor
  - Servidor: programa que executa operações solicitadas pelos clientes enviando-lhes o respetivo resultado.

## Cliente/ Servidores -> Propriedades
  Arquitetura mais simples, muito usada em sistemas pouco exigentes -> ponto de partida para criar sistemas mais complexos
  
  ### Positivo
    - Interação simples facilita implementação
    - Segurança apenas tem de se concentrar no servidor
  
  ### Negativo
    - Servidor é um ponto de falha Único
    - Não escala para além dum dado limite( servidor pode tornar-se ponto de contenção/estrangulamento)
    
## Modelo alternativo para lidar com limitações do modelo cliente/servidor
   Todos os processos têm funcionalidades semelhantes
    - Durante a sua operação podem assumir o papel de clientes e servidores do mesmo serviço em diferentes momentos.
    
 ## Peer-to-Peer: Propriedades
    
   ### Positivo
    - Não existe ponto único de falha ( improvável que todos os pares falhem)
    - Grande potencial de escalabilidade ( + pares --->>>> + recursos)
    - Baixo Custo de Operação ( os pares contribuem c/os recursos)
   
   ### Negativo
      - Interação mais complexa (do que num sistema cliente/servidor) leva a implementações mais complexas
      - Maior número de computadores envolvidos pode colocar questões relativas a heterogeneidade e segurança
      
   ### Apropriado para ambientes em que todos os participantes querem cooperar para fornecer um dado serviço.
   
 
