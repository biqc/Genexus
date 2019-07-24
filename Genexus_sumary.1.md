# Deu certo? Deu

# Genexus CheatSheet
## [Transactions]
* São representações de objetos/situações da realidade
* Base da KB, já que todo o banco de dados é baseado nas transações e seus relacionamentos
* Podem conter mais de um nível
* Possível definir fórmulas em seus atributos
	### GIK
	* Padrão de nomenclatura dos atributos (ex: Classe+Atributo -> ClienteNome)
## [Subtypes]
* Atributos baseados em outros atributos
* Usados para especificar a utilização de certos atributos
* Corrigir duplicatas
* ex: ~~ClienteID e ClienteID~~ **X**
  ClienteResponsávelID e ClienteAuxiliarID **&#10004;**
             ^  **Ambos subtipos de ClienteID**  ^
## [Formula]
* Atributos calculados através de funções ou expressões lógicas
* Não são persistidos no banco de dados
  ### Global
  * Aplicado para todos as ocasiões
  ### Inline
  * Existe em parte específica de um objeto e é utilizado quando chamada
## [Rules]
* Definem as regras de determinado objeto e seus componentes
* Onde especificam comportamentos e verificações em determinadas circunstâncias.
* _Error, Msg, Alert, noAccept, Add, Default, etc._
* Podem ser executadas antes ou depois de **validação, gravação ou commit:**
	* **Validação -** Valida todas os comandos a serem executados
	*  **Gravação -** Grava todas as mudanças em buffer
	*  **Commit -** Grava todas as alterações no banco de dados
* Existe validação e gravação de linhas quando a transação tem mais de um level
## [Domains]
* Usados para fazer definições genéricas
* Tipos de dados padronizados que podem ser usados em vários atributos diferentes
* Diminuem divergências de dados
* Economizam tempo
* * (domínio, módulo) -> Ocorre quando o domínio só existe dentro do módulo
## [Procedures]
* São instruções pré definidas
* Podem ser executados sob chamadas de procedimentos
* Podem ter parâmetros de entrada e saída 
  ### Parâmetros
  * **:in** - Definem parâmetros de entrada para a Procedure
  * **:out** - Definem parâmetros de saída para a Procedure
  * Quando recebido um atributo por parâmetro, já é aplicado um filtro baseado no atributo
## [Relatórios]
* Dados sob perspectivas específicas definidas a partir de uma visão padronizada, podendo, ou não, receber parâmetros do usuário solicitante
* Podem ser gerados através de uma saída visual de uma **_procedure_**
* Necessário definir o arquivo de saída e seu formato
## [For each]
* Estrutura de repetição que diz: **"Para cada ocorrência, execute o bloco de instruções"**
* Pode interpretar transações como se fosse um **"select * from transaction"**
* Estrutura de repetição com uma tabela base
* Aceita diversas expressões de condição como: **Where**, **Order**, **Unique**, etc.
  ### For each Aninhados
* Se as transações não se relacionam, gera um **produto cartesiano**
* Se 1 para N, com a transação forte no primeiro nível, é feito um **join** e fica implícito um **where** ligando as duas transações em questão.
* A mesma tabela base nos dois for each e uma cláusula **order** com um atributo da tabela extendida faz um **controle de corte**
## DataSelector
* Armazena um grupo de parâmetros, condições, ordens e clausulas _defined by_, para ser chamado de diversas _queries_, cálculos, etc.
* Reúso de código
* Facilita manutenção, já que a regra está definida em um lugar fixo
* Provém encapsulamento
## [SDT]
* _Structured Data Type_ - Tipo de dado estruturada
* Permite definir estruturas de dados complexas
* Representa dados com estruturas feitas de vários elementos
* Facilita transferência de dados
* Parecido com objetos, mas não permite definir métodos
* Pode ser usado para padronizar parâmetros entrada e saída
  ### Collection
  * Quando o elemento possui múltiplas instâncias
  * O elemento principal se torna um grupo de "Elemento"Item
  * Pode ser definido como _collection_ no próprio SDT ou na variável que é criado com seu domínio
  ### Elementos compostos
  * São elementos definindo um novo grupo de elementos - Uma nova coleção ou um grupo de elementos simples (level)
  * O level inserido pode também ser uma _collection_
## [Data Provider]
* É um procedimento declarativo,  usado para obter dados em uma estrutura hierárquica (no Gx, SDTs) de forma clara e com esforço mínimo, através da definição de sua saída (_output_)
* **Tudo que é feito com um _Data Provider_ pode ser feito com uma _procedure_, assim como o contrário**
* O data _provider_ é mais fácil de ler e compreender, focado na linguagem de saída; a _procedure_ foca na linguagem de transformação
* Os dados podem ser escritos ou recuperados de um banco de dados
* Aceita cláusulas de consulta para buscar os dados
  ### Facilidades com _Data Providers_
  * Para escrever arquivos _XML_, como em _web services_
  * Preencher **SDTs**, como os usados para vincular _User Controls_, _GxCharts_, etc.
  * Preencher **Business Components**
## [Business Component]
* Quando uma transação é definida como _business component_, é criado um tipo de dado de mesmo nome da transação criada na KB, e variáveis baseadas no novo tipo de dado podem ser definidas em qualquer objeto
* As variáveis baseadas em um _BC_ recebem um conjunto de propriedades correspondentes aos atributos da transação
* Também disponibiliza um conjunto de métodos a fim de executar operações na base de dados
  ### Principais benefícios
  * Garantia de integridade de dados em updates na base de dados
  * Reutilização de código, já que a lógica e as regras definidas na transação são reaproveitadas
  * Todos os objetos Gx podem atualizar a base de dados
  * Pode ser exposto como um _web service_ Rest
  * Etc

## [Global Events]
* Permite definir eventos globais para todos os componentes de uma aplicação
* Todos os componentes podem interagir entre si através de eventos globais porque os mesmo podem ser invocados de qualquer componente, independente do componente que foi definido

## [UTL - Unidade lógica de trabalho]
* _Logical Unit ow Work_(Unidade lógica de trabalho)
* Se refere as operações na base de dados em que todas devem ser totalmente bem sucedidas ou nenhuma deve ser
* É a lógica que envolve o objeto; uma transação é armazenada em níveis mas a **unidade lógica de trabalho** é a transação toda
# [WorkWithPlus]
* Automatiza a geração do FrontEnd
* Tem diversos temas padrões para facilitar o desenvolvimento do projeto
* Deveria ser gerado no início do projeto para encurtar o tempo de importação de dependências
* Pode ser alterado posteriormente
* As configurações são definidas em blocos que não devem e não podem ser alterados na mão, já que, ao aplicar a _pattern_, os dados são sobrescritos 
## Startup Wizard 
* Tem 10 passos para definição rápida do design do _WorkWithPlus_ em uma apliação
* Layout de transações, menus, grids, etc.
* Oferece um sistema de autenticação por login e senha já funcional
* Etc.
## IDE
* Gera diversos objetos para a transação, como _WebPanels_ de _view_, _selection_ e _prompts_
* Tem uma árvore hierárquica(_Hierarchical Tree_)  para cada objeto gerado, organizando seus elementos (ex: Form da transação)
* Apresenta uma _preview_ em tempo real, mostrando um exemplo de como a aplicação será gerada sem a necessidade de reaplicar a pattern ou rodar o programa.
## User Controls
* Objeto oferecido para simplificar o desenvolvimento de controles de usuários e reuso de código
* Permite basear sua aparência em um estilo provido por um designer, framework css, etc.
## Transaction Template
* O template de transação define um padrão de modelo de estrutura para algumas instâncias de transação
* Define um modelo base de layout para as transações
## Web Panel Template
* Define o layout padrão de telas
* Útil quando diversas telas são similares



## VASP
* Verbo, adjetivo, substantivo e predicado

 BPMN, microservices, api, rest
 GAM - genexus auth.. manager
			 - Várias kb podem usar do mesmo gam
			 - o gam em comum é a base de dados gerada e só precisa ser configurada

### Boas Práticas
* Gik
* Usar domínios
* (domínio, módulo) -> Ocorre quando o domínio só existe dentro do módulo
* Todos os atributos podem receber nulo e a regra deve ser definida no sistema, não no db
* Exclusão lógica
* Enums
* Expressões regulares
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTIwNTg3NTU4NzksLTg4MDk5OTI5MV19
-->