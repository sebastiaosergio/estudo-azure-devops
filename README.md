# Azure DevOps

baseado na playlist [Primeiros passos Azure DevOps 2021](https://www.youtube.com/watch?v=I9dVHxbRDBw&list=PLMFPOLE2cW1yXGKZ6Mt12P1ewsmmgRQTk) canal do [@juliarruda](https://github.com/julioarruda). 

- Repositorios - **Azure Repos**
- Pipeline de CI CD - **Azure Pipelines**
- Boards, backlogs e work items - **Azure board**
- Git - **Azure Artifacts**
- Testes - **Azure test plan**	

Antes de Azure DevOps...

- TFS - *Team Foundation Services*
- VSO - Visual Studio Online
- VSTS - Visual Studio Team Service
> Renomeou para Azure DevOps por causa da percepção de que seriam utilizados apenas para ferramentas da Microsoft.
> Existem diversas integrações, inclusive de CI e CD. *  


### Conceitos básicos ###
- **CI**: Continuous Integration

Garante a Integração do ciclo de desenvolvimento: ***Plan*** (Planeja), ***Code*** (Codifica/Executa), ***Build*** (Constrói a aplicação) e ***Test*** (Testa a solidez do construído)

- **CD**: Continuous Deployment

Garante a entrega do *Produto final*. Então com a aplicação planejada, codifica, construída e testada chegou a hora de colocar o produto para rodar. Então serão realizadas as etapas de ***Release***: Lançamento de uma versão pronta para *consumo*; ***Deploy***: Entrega da versão para acesso de terceiros e ***Operate***: operacionalização do produto, estabilização da aplicação, monitoramento de seus consumos etc.   

- **Agentes de compilação - Compile agents** 

São "estruturas" utilizadas para compilar sua aplicação. Por exemplo uma máquina já preparada com *runtimes*, *sdks*, *compiladores*, etc.

### Iniciando no Azure DevOps ###

- Azure DevOps é Gratuitos até 5 desenvolvedores

**Após criar conta e logar**
- Logado
- New Organization 
  - Choose host region.

  - Escolha região de hospedagem
- New Project
  - Public / Private
    - Public exibe tudo para todos (repos, board)

  - Detalhes avançados
    - Version Control -> GIT ou TFVC
    - Agile / Basic / CMMI e Scrum (??)

- Dashboard do projeto
   - Pode-se criar vários Dashboards personalizados.
   - Pode-se criar Wikis (com markdown)
   - Repositorios, Pipelines e todos os serviços.
- Repository (ilimitados)
   - Varias opções para importar um projeto existente, criar um novo ou importar de ferramentas de Git de terceiros.

AZURE BOARDS

- Registro e gestão de Backlogs e demandas
   - Work items
    - Demandas/Tarefas
    - Permite comentários 
    - Tipos de item (bug, feature...)
    - Id, Nome, Descrição, Detalhes... Associado ao deployment, relacionamento a um commit... É possível rastrear todo o processo de uma demanda específica. Alta rastreabilidade. É possível gerar um release note (com tudo que foi entregue e todo o processo dos work items)
    - Histórico do item. Anexos.
    - Boards
      - PBI - PRODUCT BACKLOG ITEM
        - Acrescentar diversas tasks
    - Backlogs 
      - Gestão dos Sprints
    - Hierárquia 
      - EPIC -> FEATURES -> PBI
    - Visão das SPRINTS
      - Gestão dos participantes (quantos itens ele faz, datas que não trabalha)

- Queries
    - Buscas avançadas por todo os Boards. Possibilidades gerais. Existe um editor de Queries. Export para Excel, CSV

- Configurações
    - Modificar as colunas
      - Limite de WIP ***WORK IN PROGRESS*** - tarefas em execução
    - Criar regras de ação condicional a ser aplicado nos cards
    - Criar tags
    - Swimlanes 
      - Raias, linhas de separação por determinada regra de organização.

- Tipos de Work items
  - Várias abordagens permitidas SCRUM, AGILE, SCRUM etc.. Também é permitido criar seus tipos. 
  - Existe o Rules (Regras)
    - Permite automatização de regras em determinada ação dos cards. Por exemplo não permitir um card ir para determinada coluna sem antes passar por uma determinada. 
 

AZURE PIPELINES

- Pipelines são linhas de execução quer permitem executar diversas tarefas com o intuito de gerar um deploy.
- Depende de Scripts e Runners
- Runners são executados baseados em Agentes de Serviços que permite executar determinados serviços/tarefas etc... Podem ser instalados em container do Azure ou em on promise.
- Os pipelines podem ser tarefas agendadas também!
- Existem templates de pipeline para facilitar a criação.
- Agent pool
- Sistema operacional que o agent ira usar

[Pesquisa melhor] SONAR CODE (??)

- Pipelines de BUILD - CI
  - Jobs
    - Demands (exigencias do Agent)
    - Task  
      - Restore, Build, Publish...
    - Variables 
      - Como se fosse variaveis de ambiente, env
    - Trigger (igual o processo no MySQL)
      - Agendadas
      - Pós termino do build
    - Permite acompanhar a execução dos jobs. 
    - Gera um artefato - zips do processo.


- Pipelines dee RELEASE - CD - Continue Deployment
  - Releases
    - Permite diversos ambientes (stages)
    - Permite trabalhar com varias clouds
    - Permite gerar autorizações
      - Permite diversas verificações para que o Deploy aconteca (gates)
        - Ex.: Só executa se todos workitems foam concluidos, se a qualidade do codigo esteja em x (Sonar).
    - Depende de um artefato.
    - Permite alterar os workitems
    
PIPELINES EM YML
  - [YAML](https://pt.wikipedia.org/wiki/YAML#:~:text=YAML%20%C3%A9%20um%20formato%20de,Net%20e%20Oren%20Ben%2DKiki.) é um padrão script (um formato de serialização)

MULTISTAGE PIPELINES VERSIONADO

- Environment (Ambiente)
- No YML cria a chave stages: e depois define o -stage
   - chave environment seta em qual ambiente o pipeline será rodado e as configurações serão utilizada.

AZURE PACKAGES

- O que são pacotes??
   - São os serviços prontos que são utilizados dentro da aplicação.
- Azure Packages é um gerenciador privado de pacotes semelhante ao Nuget, NPM, pip, composer (porém privado)
- Todo o gerenciamento de políticas para consumo.. etc
- Cria-se um FEED (Repositórios de pacotes privados)
   - Pode se criar pacotes para toda a aplicação. Por exemplo um pacote que você utiliza na sua aplicação o Azure busca os pacotes e faz o download para dentro de uma nuvem privada. Dependendo da configuração do pacote ele pode ser utilizado por toda a aplicação.