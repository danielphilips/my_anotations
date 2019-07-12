## O que é?

O schematics é um framework criado pelo setor de tecnologia no intuito de agilizar e padronizar o processo de desenvolvimento das telas do sistema de modo que todas as funções tenham um padrão de comportamento e navegação. Ele é composto por vários componentes que possuem comportamentos diferenciados para cada necessidade dentro do sistema. Exemplo de componentes: Formulários, Gráficos, DashBoards, Grids e etc.
Ele foi desenvolvido em Javascript (AngularJS), HTML5, Bootstrap, JQuery e entre outras ferramentas de desenvolvimento (Front End), o Back End é desenvolvido em Java.

## Como Funciona?

Engloba os Dicionários de Dados e Objetos. As funções e componentes são criados via cadastro. Este cadastro é feito através da função Dicionário de Objetos (Ctrl+Shift+O) na aba WSchematic.

A tela é renderizada pelo navegador de acordo com a estrutura criada no Schematics exatamente na ordem em que a árvore da função é montada e de acordo com a necessidade em que o usuário vai avançando na estrutura da função. É preciso se atentar que o componente só pode ser acessado via programação no momento em que ele existir.

## Componentes mais utilizados:

Apesar de conter vários tipos de componentes com diferentes comportamentos, os componentes que são utilizados com mais frequência no desenvolvimento de funções são: 

*	WDBPanel (Utilizado para manipular e visualizar o conteúdo de uma tabela.);
*	WCPanel (Utilizado para visualizar conteúdo de uma ou mais tabelas através de Join das tabelas, sem que haja a necessidade de manipular registros.);
*	WDLGPanel (Modais que podem conter diferentes tipos de componentes em sua estrutura, ex: modal para mostrar inconsistencias em uma grid, modal com formulario para alterar o registro que está selecionado);
*	WDynamicForm (Utilizado para criar formulários);
*	WPopUpMenu (Utilizado para criar ações em um PopUp que é acionado ao clicar com o botão direito sobre o componente que contem um WPopUpMenu  como seu filho);
*	WFiltro (Utilizado para ativação dos componentes de acordo com parâmetros);
*	Tab (Utilizada para criar abas de navegação).

## Criando uma função com schematics

![](https://i.imgur.com/WJkrumc.png)

Para acessar a função que foi criada: http://dev.tasy.whebdc.com.br
Ao logar no sistema acessar "Função Schematic" passando como parâmetro o código da função schematic criada.

## Ativações

Os componentes (WCPanel e WDBPanel) podem ser ativados por 5 formas: Através de código de ativação (Apenas WDBP), filtro, action, view e vazia. Todas as ativações por view, filtro e código de ativação devem ser realizadas via schematics.
As ativações que devem ocorrer via código-fonte são aquelas que ocorrem após alguma ação do usuário. Exemplo: Após clicar no ok de um WDLG que modifique o registro, e após isso o wdbpanel ou as linhas selecionadas precisem ser reativadas.

## Ativar por código de ativação (WDBP/WCP):

Esta ativação é utilizada quando a query de restrição não é dinâmica. O cadastro é realizado através da pasta Activation do componente WDBPanel. Recebe parâmetros de ativação conforme pasta parâmetros.
Para definir qual código de ativação será utilizado é necessário selecionar este código na pasta Component e garantir que não tenha nenhuma action cadastrada na aba properties.
Em componentes WCPanel a pasta activation permite apenas o cadastro dos parâmetros de ativação.

![](https://i.imgur.com/X7nyjT7.png)

Para vincular o código de ativação com o componente é preciso inserir o código no campo "Ativação padrão" na aba "Component".

![](https://i.imgur.com/pTtTI3t.png)

## Ativação diretamente na view (WDBP)

A ativação pode ser feita diretamente pela view, geralmente é utilizada em casos onde não possui filtro de ativação e quando a restrição não será alterada dinamicamente.

![](https://i.imgur.com/hLo1p1A.png)

## Ativação por filtro (WDBP/WCP)

É possível cadastrar restrições para cada atributo do filtro que esta dentro de um WCP ou WDBP. Para realizar o cadastro será preciso acessar o objeto do filtro e no cadastro do atributo inserir a restrição no campo "Restrição usada na action:", é preciso se atentar ao campo "Utilizar campo na restrição da action:" pois este deve estar marcado com a opção 'Restrição personalizada'.

![](https://i.imgur.com/nZ5PaO1.png)

## Ativar via action(WCP, WDBP)

Para fazer ativações onde a restrição depende de condições de variáveis, deve-se utilizar actions. Actions permitem trabalhar com a query de ativação de forma dinâmica. Para definir que um WDBPanel utiliza action para ser ativado, basta incluir o caminho da action na aba properties do componente no schematics.
O campo action sobrescreve todas as ativações vinculadas a um componente. Ou seja, se um WDBPanel possui a ativação via código e também o campo action definido, ele será ativado via action ignorando a ativação via código.

![](https://i.imgur.com/BLmpmgi.png)

Para vincular a action no componente é preciso cadastrar o namedAction nas propriedades do mesmo. Para isto o campo "Action" deverá conter o nome da action criada no backend.

![](https://i.imgur.com/k8Z5e43.png)

## Ativar vazio (WDBP, WCP)

A ativação vazia ocorre quando em um primeiro momento o analista/programador deseja que o grid não traga registros. Para fazer isto via schematics, basta utilizar o campo Ativar Vazio da pasta properties.

![](https://i.imgur.com/kqTAzb5.png)

## WPopUpMenu

O componente WPopUpMenu é utilizado para criar ações em um popup para que sejam realizados ações  geralmente utilizando o(s) registro(s) selecionados na grid. Este compontente pode possuir uma ou mais opções de ações, estas ações possuem dois comportamentos: State e Action.
- state: é o evento utilizado para realizar a habilitação da opção em tela;
- action: é o evento onde é realizada a ação para que a opção foi criada;
Estes comportamentos podem ser programados tanto em código fonte quanto pelo schematics. Somente são implementados via código fonte em caso de complexidade da implementação onde não é possível programar via schematics. Exemplos:
no caso do state: É preciso realizar uma consulta e comparar o resultado para habilitar;
no caso da action: realizar uma consulta e após o resultado executar uma procedure, perguntar algo para o usuário, adicionar loader a ação;
É possível identificar se os eventos das opções foram implementados via schematics. Abaixo segue os anexos com as legendas para cada particularidade:

![](https://i.imgur.com/Tfri6oN.png)

![](https://i.imgur.com/rJjUZz7.png)

* É preciso se atentar pois qualquer ação realizada via código fonte no caso das opções do WPopUpMenus irão sobreescrever a programação no schematics.

## Implementação via código fonte: 
Abaixo segue um exemplo de como ficaria uma opção de WPopUpMenu realizada via código fonte já modularizada:

![](https://i.imgur.com/0kJhQyv.png)

## Controllers na camada dev

Controller é utilizado para implementação da regra de negócio na camada de desenvolvimento. Onde através dos eventos que são registrados para cada componente é possível adicionar regras específicas para cada componente de acordo com a necessidade de cada funcionalidade do sistema. O controller dos componentes são identificados por sua sequencia cadastrada no schematics, ou seja o controller que contém a sequencia do componente registrada é o controller do respectivo componente.

* Sequencia do componente no schematics:
 
![](https://i.imgur.com/0kJhQyv.png)


## Registrando a sequencia no controller:

No sistema tasy é possível registrar o controller de um componente de 3 formas, inicialmente era importado diretamente o arquivo no arquivo index da função e registrado uma function para retornar os eventos, após foi criado o TasyApp para melhorar a forma que estava sendo implementada, porém com o crescimento do sistema descobriu-se que as duas formas demandavam muita memória e então foi criado o ODIN, esta ferramenta foi criada para que o sistema pudesse trabalhar com baixo consumo de memória além de se tornar muito mais rápido.

* Registrado o controller com ODIN:

![](https://i.imgur.com/x0TQKqx.png)

* Registrando o controller com TasyAPP:

![](https://i.imgur.com/QpPRzfy.png)


