# Horário disponível

OBS: Todos BR. Fuso de +/- 3 horas para mais em PT.

* 09:30 - 12:00 (2 horas e meia)
* 14:00 - 19:00 (5 horas)

# Frentes de atuacão (por ordem de prioridade)

* Leandro - Graphql/App/Site
* Diego - Site/Graphql/App

 # Itens para dev

- **Item 1 - Alterar formulário que edita/cria algoritmos**. Consiste em adicionar um novo nivel de variacão nos campos, com o campo período, adicionar um toggle para identificar se o algoritmo possui ou não odds, e os valores caso possua, e corrigir a definicão de live ou pre-live, que deve ser um toggle entre os dois. Os dados dos campos no banco estão na tabela algorithm_target. Essa funcão pode continuar completamente dentro do SQL. O XD pode ser encontrado em: https://xd.adobe.com/view/30acaa0b-cd68-4d17-a47f-180e01a51a58-65ff/screen/23aa2679-5620-425e-9800-7430dea55aab/. E o componente se localiza em My Algorithms > Botão New. A tarefa deve ser feita na branch feat/new_algorithm_form. Aqui são os seguintes passos para poder concluir a tarefa:
    1. [**SITE**] Portar todo o componente existente para o novo layout.  Aqui precisamos ver com o Tiago para ele verificar com a Desginer se já existe um componente com os novos HTML de campos novos/alterados, ou se será preciso criar, para poder dizer o tempo necessário. **Horas necessárias**: 2 Horas.
    2. [**SITE**] Criar ajax e toggle de campos para o novo nível (periodo, campo cd_target_period) e alterar demais campos conforme o valor selecionado para esse campo. Aqui, precisa verificar se os campos seguintes estão seguindo o toggle de period corretamente, validando em banco e mandando a query e resultados dela para pelo menos 3 variacões de filtros. **Horas necessárias**: 4 Horas.
    3. [**SITE**] Converter o campo de type (pré live ou live) para o novo formato de toggle, e garantir que o restante dos filtros varie também de acordo com esse toggle, mandando pelo menos 2 exemplos de queries, seus resultados e o efeito disso no frontend. **Horas necessárias**: 3 Horas.
    4. [**SITE**] Adicionar o toggle e campo de Odds. Garantir 2 coisas, a primeira é que quando não houver ODDS, os campos de min e max do ODD irão ser desabilitados no frontend, e que o campo fl_odd será definido de acordo com o toggle (Não = 0, Sim = 1), e também se max e min do odd serão alterados no banco. Mandar print (no banco, e no frontend) de exemplo de um algoritmo iniciando com odd igual a Não. Depois nesse mesmo algoritmo, alterar para sim e definir max e min, em seguida, alterar para não (aqui, o unico campo que mudará no banco é o fl_odd), e por ultimo o print alterando de volta para 1. **Horas necessárias**: 3 Horas.
    5. [**SITE**]  Garantir que todo o processo descrito funciona tanto para criar quanto para editar um algoritmo. **Horas necessárias**: 1 Horas.


- **Item2 - Alterar listagem de algoritmos**. Consiste em alterar a listagem de algoritmos personal e system, localizados respectivamente nas telas Algorithms > My Algorithms, e Algoritms > System Algorithms. Como essa listagem existe no app, ja existe uma function graphql para servir de base para essa tarefa, que será copiada e sua cópia modificada conforme precisarmos de dados para a nova tela. A function existente é a algorithms, e a nova será algorithmsV2. Nessa function nova, precisará implementar os seguintes filtros: Se está buscando por HalfTime, FullTime ou ambos; Se está buscando por live ou pre-live; Se está buscando apenas o que o usuário está seguindo, apenas os que NÃO está seguindo, ou ambos; E se está buscando por algoritmos que batam com um nome especifico (campo de pesquisa do nome). No retorno dessa nova function, serão inseridos os dados edges->node->follow->simple (Boolean, indica se está seguindo no modo telegram simple), alterar o parametro edges->node->follow->detail (Boolean, indica se está seguindo no modo telegram detail) e adicionar o edges->node->follow->app (Boolean, indica se está seguindo no app). O XD para a task pode ser encontrado em: https://xd.adobe.com/view/30acaa0b-cd68-4d17-a47f-180e01a51a58-65ff/screen/fec94845-3e9e-44f3-916f-ce17e91d3f28 e https://xd.adobe.com/view/30acaa0b-cd68-4d17-a47f-180e01a51a58-65ff/screen/63d678a3-beb5-414f-9124-50c74705098b. Fazer na branch feat/new_algorithms_list. A checklist para essa task é:
    1. [**GRAPHQL**] Copiar a function algorithms para algorithmsV2, e separar todos os handlers, resolvers, types, schemas, etc para possibilitar alterar elas de forma separadas. **Horas necessárias**: 4 horas.
    2. [**GRAPHQL**] Na nova function adicionar os filtros descritos acima. Aqui é importante pedir ver com o Tiago qualquer dúvida relacionada a tabela que será buscada e campos caso haja alguma. Mandar o retorno do graphql com pelo menos 5 cenários de filtros diferentes, as queries SQL que essa query graphql fez, e o resultado de ambas as queries, para garantir que está certo. **Horas necessárias**: 2 horas.
    3. [**GRAPHQL**] Adicionar os novos campos e alterar os atuais conforme descrito acima no retorno da nova function. Aqui, mandar os prints de pelo menos 3 retornos diferentes, tanto graphql quanto no sql, e tanto os resultados como as queries feitas em ambos. **Horas necessárias**: 2 horas.
    4. [**SITE**] Verificar com o Tiago se existe a view para a nova tela, caso exista integrar com o existente, caso não exista, criar. **Horas necessárias**: 3 horas.
    5. [**SITE**] Implementar o toggle de filtros de acordo com o a regra que o Tiago descrever. Esses filtros alteram apenas no frontend, conforme a selecão do anterior, muda os demais a frente. **Horas necessárias**: 2 horas.
    6. [**SITE**] Implementar a busca via graphql, usando os filtros. Enviar aqui os prints do filtro no frontend, da query graphql que está fazendo e o retorno bruto do graphql (não é necessário confirmar no banco pois isso é feito no passo 2). **Horas necessárias**: 2 horas.
    7. [**GRAPHQL**] Criar mutation para seguir/deixar de seguir um algoritmo. Enviar query de UPDATE, e antes e depois do algoritmo no banco de dados, com execucão da mutation. **Horas necessárias**: 3 horas.
    8. [**GRAPHQL**] Criar mutation para definir quais tipos de notificacão o usuário deseja receber, pode ser telegram simple, telegram detail e app, todas booleanas. Aqui é importante que uma mesma mutation altere todas para o novo estado. Mandar mesmos prints do item 7. **Horas necessárias**: 4 horas.
    9. [**SITE**] Criar ajax para consumir as mutations conforme cliques nas checkboxes de cada algoritmo. Mandar print do frontend antes e depois, e do banco de dados para o algoritmo antes e depois do clique também. **Horas necessárias**: 3 horas.

-  **Item 3 - Alterar formulário de regras para cada algorithm**. Essa tarefa consiste em corrigir o toggle de campos disponiveis ao mudar X campo na hora de editar/adicionar regras a um algoritmo. Fazer essa tarefa na branch feat/algorithm_rule_toggle. O checklist para a tarefa é:
    1. Corrigir toggle de campos, de acordo com a regra ser passada no JIRA [INSERIR_JIRA_AQUI] pelo Tiago. A regra de campos já foi apresentada via reunião, e a estivamativa para adicão, é de 5 Horas.

