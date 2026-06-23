# SPLUNK E-LEARNING — CISCO-SPLUNK

## Splunk Knowledge Object

### O que são Knowledge Objects?

Por agora sabemos que Knowledge Objects são ferramentas que auxiliam os usuarios a descobrir e analisar dados.
Nesse modulo vamos entrar mais a fundo na criação e manipulação de Knowledge Objects!

Vamos dar uma olhada nos principais tipos de Knowledge Objects e saber no que eles são usados:

Fields;
Field Extractions;
Field Aliases;
Calculated Fields;
Lookups;
Event Types;
Tags;
Workflow Actions;
Reports;
Alerts;
Macros;
Data Models;

#### Fields

Fields ou campos, são os blocos de construção de uma pesquisa Splunk, quando uma pesquisa é rodada todos os fields disponiveis ficam amostra na barra esquerda. Clicar em um desses campos, abre a janela de campos, contendo valores para esse campo.

<div align="center">
  <img src="Images/field.png" width="400">
</div>

Selecionando um valor da janela do field vai adicionalo a sua pesquisa.

#### Fields Extractions

<div align="center">
  <img src="Images/regdeli.png" width="400">
</div>

Enquando diversos fields são extraidos automaticamente da search time, você também pode manualmente extrair campos de seus dados, usando tanto "regex" ou delimitador.

#### Field Aliases

<div align="center">
  <img src="Images/fa.png" width="400">
</div>

Field Aliases permite você normalizar dados ao adicionar um nome alternativo para campos existentes em seus dados.
Esses alieses podem ser particulamente uteis se diversos campos contem valores relacionados em diferentes sourcetypes.

#### Calculated Fields

<div align="center">
  <img src="Images/cf.png" width="400">
</div>

Calculated Fields fazem calculos baseado nos valores de campos existentes, os seus fields name sao criados no search time com os valores supridos pelo resultado de uma Eval Expression, usando valores de campos existentes.

#### Lookups

<div align="center">
  <img src="Images/lu.png" width="400">
</div>

Campos adicionais e valores que não são contidos em seus dados podem ser adicionados para seus eventos usando lookups.

Lookups são baseados em fontes como o CSV, e podem ser configurados para integrar campos adicionais a eventos encontrados em sua pesquisa.

#### Event Types

<div align="center">
  <img src="Images/et.png" width="400">
</div>

Se você se encontra normalmente utilizando a mesma combinação de termos de pesquisa, como uma query de compras web de sucesso, pode ser benéfico para você salvar sua pesquisa como um event type.
Event types te concedem uma maneira de ajuda para catalogar seus dados.
Ao salvar o seu termo de pesquisa como um event type nomeado web_sales, voce pode salvar tempo escrevendo event_type=web_sales para economizar tempo de escrita. 

#### Tags

<div align="center">
  <img src="Images/tag.png" width="400">
</div>

Field-value pairs podem tambem ser salvos como tags. Você pode pensar neles como legendas para seus dados.
Tags podem ser usados em uma pesquisa igual event types, clicando no host value, apenas valores com a tag são retornados.
Event Types e Tags, também podem ser acessados pelo sidebar da esquerda.

#### Workflow Actions

<div align="center">
  <img src="Images/wa.png" width="400">
</div>

Workflow Actions concede links em eventos que interage com recursos externos ou extreita nossas pesquisas.
Eles usam os metodos HTTP GET ou POST, para passar informações para fontes externas, ou pode passar informações devolta para Splunk para performar uma pesquisa secundaria.


#### Reports and Alerts

<div align="center">
  <img src="Images/alert.png" width="400">
</div>

Pesquisas que você roda constantemente podem ser salvas como Reports. Para receber uma notificação quando uma condição de pesquisa aconteça, você pode salvar sua pesquisa como um alerta.
Reports e Alerts salvos são muito poderosos e possuem uma grande gama de alcance de scheduling settings.

#### Macros

<div align="center">
  <img src="Images/macros.png" width="400">
</div>

Macros são search strings, ou porções de search strings que podem ser reutilizados em multiplos lugares dentro do Splunk>.
Similares com event types, eles sao uteis quando voce frequentemente roda pesquisas com requerimentos similares ou com sintaxes complicadas.

Macros permitem você guardar search strings inteiros, incluindo comandos.


#### Data Models

<div align="center">
  <img src="Images/dm.png" width="400">
</div>


Finalmente, Data Models são datasets estruturados hierarquicamente que podem consistir de tres tipos de datasets:
events, searches e/ou transactions.

Data models podem ser utilizados em Pivot, permitindo usuarios explorar dados em uma interface grafica sem nunca ter que entender SSL(Splunk Search Language).

### Knowledge Objects Settings

Criar tipos especificos de Knowledge Objects é fora do escopo deste modulo, nesse segmento vamos focar nas caracteristicas que se aplicam em todos os Knowledge Objects.

#### Desenvolver convenções de nomeação(Naming Conventions)

Desenvolver convenções de nomeação vai nos ajudar e nossos usuarios a saber extamente o que cada Knowledge Object faz, e vai ajudar nosso Splunk Toolbox organizada.
É recomendado que você nomeie objetos usando seis chaves segmentadas.
Grupo, Tipo, Plataforma, Categoria, Tempo e Descrição.

<div align="center">
  <img src="Images/nomea.png" width="400">
</div>

Exemplo, se tivessemos uma Security-Focused Workflow Action que estariamos criando para o time de operações que iria retornar informações sobre o IP de um usuário, nos utilizariamos um **grupo** de "OPS" para operações, um **tipo**  "WFA" ou workflow action, uma **plataforma** de "Network", uma **categoria** de "Segurança", ja que a workflow action não é baseada em tempo, vamos usar "na" em tempo, e uma **descrição** escrita como "IPwhoisAction". 

Agora olhando para nossos Knowledge Objects, podemos ver o que eles fazem, para que servem e o que esperar deles.

#### Permissions

<div align="center">
  <img src="Images/psa.png" width="400">
</div>

Permissões possuem uma função importante na compartilhação de knowledge objects no Splunk.
Existem três maneiras predefinidas que um knowledge object pode ser compartilhado para outros usuarios.
Quando um usuario cria um knowledge object ele é automaticamente settado como privado, apenas disponivel para o usuario que o criou.
Power e Admin podem criar knowledge objects que podem ser compartilhados por todos usuarios do APP, eles podem também permitir outras funções a lerem e editar o objeto ou até mesmo esconder eles por remover permissões de leitura e edição.
E o Admin é a unica função que possui permissão para deixar Knowledge Objects disponivel para TODOS os apps.
Admins também podem ler e editar objetos criados por qualquer função.

### Menaging Knowledge Objects


