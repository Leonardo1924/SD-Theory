Sistema Distribuído 

## Introdução:
Um sistema distribuído é um conjunto de componentes hardware e software interligados através de uma infraestrutura de comunicações, que cooperam e se coordenam entre si apenas pela troca de mensagens, para a execução de aplicações distribuídas.

### Motivações Dos Sistemas Distribuídos 
  - Acesso generalizado sem restrições de localização
  - Partilha de recursos distribuídos pelos diferentes utilizadores
  - Distribuição da carga – melhoria do desempenho
  - Tolerância a falhas – melhoria da disponibilidade

### Flexibilidade e adaptabilidade
  - Decomposição de um sistema complexo num conjunto de sistemas mais simples.
    
## Características Fundamentais
  - Componentes do sistema executam de forma concorrente -> paralelismo real
    Necessidade de coordenação entre os vários componentes.

### Falhas independentes das componentes e das comunicações
  -	Impossível determinar se existe uma falha dum componente ou do sistema de comunicações.
  - Necessidade de tratar as falhas.

## Ausência de relógio global 
  - existem limites para a precisão da sincronização dos relógios locais.
  - Impossível usar relógios locais para ordenar globalmente todos os eventos.

### Implicações 
  - Nenhum componente tem um visão exata instantânea do estado global de todo o sistema.
	- Os componentes têm uma visão parcial do estado global do sistema
	- Os componentes do sistema estão distribuídos e só podem cooperar através da troca de mensagens, as quais levam um tempo não nulo a propagarem-se.

  - Na presença de falhas, o estado global pode tornar-se incoerente, i.e., as visões parciais do estado global podem tornar-se incoerentes. Por exemplo, réplicas de um objeto podem ficar incoerentes.

## Algumas características que queremos garantir num Sistema Distribuído
  - Abertura
  - Transparência
  - Segurança
  - Escala

### Abertura
A abertura de um sistema determina o modo como pode ser estendido e reimplementado.

Sistemas abertos
	Interfaces e modelo (incluído protocolos de comunicação) conhecidos
	Evolução controlada por organismos de normalização independentes ou consórcios industriais 
	Permite a interoperação de componentes com diferentes implementações.
Sistemas proprietários 
	Podem ser modificados pelo seu “dono”.
 
 ### Transparência
	A transparência (da distribuição) é a propriedade relativa a “esconder” ao utilizador e ao programador das aplicações a separação física dos elementos que compõem um sistema distribuído.
	Simplicidade e flexibilidade são objetivos
Em certas circunstância, a transparência total é indesejável… Por exemplo, o que fazer em caso de falha?

### Segurança 

   - Necessidade de proteger os recursos e informação gerida num sistema distribuído 
	 - Recursos têm valor para os seus utilizadores
### Segurança tem três componentes:
	  - Confidencialidade: indivíduos não autorizados não podem obter informação
		- Integridade: dados não podem ser alterados ou corrompidos
		- Disponibilidade: acesso aos dados deve continuar disponível
    
 #### Aspetos envolvidos 
		Autenticação dos parceiros
		Canais Seguros
		Prevenção de Denial-of-Service Attacks

## Escala
A Escala de um sistema distribuído é o âmbito que o mesmo abrange assim como o número de componentes.
	
  A escala de um sistema tem várias facetas:
	- Recursos e utilizadores 
	- Âmbito geográfico (rede local, país, mundo, …)
	- Âmbito administrativo (uma organização, interorganizações)
	
  Um sistema capaz de escalar (escalável) é um sistema que continua eficaz quando há um aumento significativo do número de recursos e utilizadores, i.e., em que não é necessário alterar a implementação dos componentes e da forma de interação dos mesmos

### Como Lidar com a Escala?
	- Divisão de um componente em partes e a sua distribuição
	- Replicação e caching (problema da consistência entre réplicas e caches)
  
  Para reduzir dependências entre componentes utilizamos meios de comunicação assíncronos (não bloqueantes).
Para simplificar o sistema utilizamos meios de designação universais (independentes da localização e dos recursos).

## Avarias, Erros e Falhas

Os componentes de um sistema podem falhar, i.e.,comportar-se de forma não prevista e não de acordo com
a especificação devido a erros (por exemplo a presença de ruído num canal de comunicação ou um erro de software) ou avarias (mecanismo que que entra em mau funcionamento).
  Num sistema distribuído, as falhas são geralmente parciais (num componente do sistema) e independentes

Um componente em falha pode induzir uma mudança de estado incorreta noutro componente, levando eventualmente o sistema a falhar, i.e., a ter um comportamento não de acordo com a sua especificação.

  

