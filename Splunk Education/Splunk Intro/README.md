# SPLUNK E-LEARNING — CISCO-SPLUNK

## Introdução ao Splunk

### Objetivos do Curso

- Explorando o Splunk Web
- Executando Pesquisas
- Usando Comandos
- Criando Reports
- Criando Dashboards
- Entendendo Knowledge Objects

---

> **Empresa de Exemplo: Bettercup Games**
> Escritórios em São Francisco, Boston e Londres.

Antigamente, se um cliente fosse contatar o suporte sobre um problema, ele seria passado de um membro para outro, forçando todos a pararem o que estavam fazendo para resolver o problema. Isso ocasionava problemas de gestão de tempo e recursos, frustrando todos, inclusive o cliente.

Mas com o **Splunk Suite of Products**, eles podem usar toda a data do ambiente para resolver problemas em menos tempo.

**César (Trabalhador):** Quando o pedido de suporte chega, ele é automaticamente direcionado para o suporte de aplicação, onde César pesquisa os dados por eventos de tentativas de compra que terminaram em erro, dessa forma ele pode encontrar o evento que se assemelha à experiência do usuário.
Esse evento está ligado a uma *Database query*, a qual pode ser correlacionada a uma entrada no *slow query log*, permitindo que César direcione o problema para o seu admin em minutos, sem ter que envolver o time inteiro.

Mas ainda melhor: e se conseguirmos alertar quando uma transação falhar? Antes mesmo que o próprio cliente contate o suporte técnico? Permitindo que César faça uma triagem do problema antes que o mesmo cause problemas maiores mais tarde.

O Splunk é uma **plataforma de dados unificada** que permite que times trabalhem juntos ou individualmente.

No coração do Splunk existe o **Index**, que contém a *machine data* proveniente de fontes como servidores, dispositivos de rede e aplicações web.

Imagine que o Index é uma fábrica e seus dados são o material bruto. Quando os dados entram, os inspetores trabalham: eles analisam os dados e decidem como processá-los. Quando encontram uma semelhança, nomeiam o dado com um **source type** (`src_type`). Então esse `src_type` é usado para quebrar os dados em eventos únicos (ex: *login error*). A data do ocorrido é identificada e normalizada em um formato consistente.

Quando o dado é ingerido pelo **Index**, ele fica disponível para pesquisa e análise. Ao inserir uma *query* na barra de pesquisa do Splunk, você pode encontrar eventos que contêm valores através de múltiplas fontes de dados.

Resultados de pesquisa podem ser salvos como **reports**, que podem prover percepções continuamente sobre seus dados e podem ser usados para alimentar os painéis de **dashboard**.

Conhecimentos podem ser organizados em datasets estruturados, chamados de **data models**, para assim permitir que usuários visualizem rapidamente dados em *Pivot* sem ter que escrever buscas personalizadas.

---

## Como Usar o Splunk Web

Ao logar no **Splunk Enterprise**, você entrará no *Splunk Home App*. Apps são áreas de trabalho pré-configuradas.

No Splunk existem três funções principais:

> **#IMPORTANTE**
>
> - **Admin:** A função mais poderosa. Pode instalar apps, ingerir dados e criar *knowledge objects* para todos os usuários.
> - **Power:** Pode criar e compartilhar *knowledge objects* com todos os usuários de um app e realizar pesquisas em tempo real.
> - **User:** Apenas pode ver seus próprios *knowledge objects* e os que foram compartilhados com ele.

O **Splunk Cloud** possui similarmente as funções de `sc_admin`, `power` e `user`, assim como funções especiais para cloud: `can_delete`, `token_auth` e `apps`.

### Sumário de Dados

| Campo         | Descrição                                                                                  |
|---------------|--------------------------------------------------------------------------------------------|
| **Hosts**     | Hostname, endereço IP ou nome de domínio qualificado da máquina onde o evento originou.   |
| **Sourcetypes** | Classificação dos dados.                                                                 |
| **Sources**   | Pasta ou caminho de diretório, porta de rede ou script de onde o evento originou.          |

---

## Pesquisa no Splunk

> **#IMPORTANTE**
>
> Filtrar uma pesquisa por **tempo** é a maneira mais rápida de obter resultados e uma boa prática. É a forma mais eficiente de limitar os resultados retornados.

**Save As** permite salvar a pesquisa como um *Knowledge Object*.

Comandos que criam estatísticas e visualizações são chamados de **comandos de transformação** — eles transformam dados de eventos em tabelas de dados.

A opção **Job** permite editar, enviar para o background, inspecionar e deletar *Search Jobs*. Ao lado ficam as opções de baixar, compartilhar, pausar, continuar e imprimir jobs.

> **#IMPORTANTE**
>
> Ao compartilhar, um link é gerado. Por padrão, um *search job* fica ativo por **10 minutos** após ser iniciado. Depois desse tempo, o Splunk precisará rodar o job novamente para obter os resultados. Um *shared job*, por outro lado, fica ativo por **7 dias** e será visível para todos com o link.

O **Export** permite exportar em Raw, CSV, XML e JSON.

### Modos de Pesquisa

| Modo          | Descrição                                                                                          |
|---------------|----------------------------------------------------------------------------------------------------|
| **Fast Mode** | *Field Discovery* desativado. Retorna apenas campos padrão e campos necessários para a pesquisa.  |
| **Smart Mode** | Padrão. Desativa comportamentos baseados no tipo de pesquisa que está sendo feita.               |
| **Verbose Mode** | Retorna todos os campos e eventos possíveis, descobrindo todos os campos disponíveis.          |

---

## Explorando Eventos

Eventos pesquisados têm a palavra buscada destacada e são retornados em **ordem cronológica inversa** (do mais recente para o mais antigo). A data é normalizada por `dia/mês/ano` e o horário é determinado pelo **fuso horário definido nas configurações do usuário**.

Ao clicar em um texto, você pode adicioná-lo à pesquisa, excluir eventos que o contenham, ou lançar uma nova pesquisa usando o texto.

Clicando no botão **Info** de um evento, você consegue ver todos os *field events* extraídos, com checkmarks nos campos selecionados.

---

## Usando Termos de Pesquisa

> **#IMPORTANTE**
>
> **Wild Card (`*`):** Procura todos os termos semelhantes que começam com a palavra escrita.
> Exemplo: `fail*` = `failed`, `failure`, `failedpassword`, `failures`, etc.

### Booleanos

> **#IMPORTANTE**
>
> `AND`, `OR` e `NOT` podem ser usados com diversos termos.

```
failed NOT password  → todos os eventos com "failed" sem "password"
failed AND password  → todos os eventos com "failed" e "password"
failed OR password   → todos os eventos com "failed" ou "password"
```

> Sem booleanos, o `AND` é implícito. Exemplo: `failed password` == `failed AND password`

**Ordem de avaliação dos booleanos:**

1. `NOT`
2. `OR`
3. `AND`

`()` podem ser usados para controlar a ordem de avaliação.

Frases podem ser buscadas entre aspas: `"frase aleatória"`. Quando a frase contiver aspas, use `\` para escapá-las.

---

## O que são Comandos?

O Splunk possui componentes fundamentais de busca:

| Componente       | Descrição                                                                    |
|------------------|------------------------------------------------------------------------------|
| **Search Terms** | Fundamentais para *search queries*.                                          |
| **Commands**     | Dizem ao Splunk o que fazer com os resultados da pesquisa.                   |
| **Functions**    | Explicam como montar gráficos, computar e avaliar resultados.                |
| **Arguments**    | São as variáveis que aplicamos na função.                                    |
| **Clause**       | Explica como os resultados devem ser agrupados e definidos.                  |

### Exemplo de Splunk Search Language

<div align="center">
  <img src="images/search.png" width="400">
</div>

> **#IMPORTANTE**
>
> O caractere `|` (**pipe**) é usado antes de um comando na pesquisa. Ele cria uma área de comandos para filtrar ainda mais os resultados.

<div align="center">
  <img src="images/casesensitive.png" width="400">
</div>

O Splunk apenas aplicará *case-sensitive* se o nome digitado tiver um valor correspondente. Por exemplo, o campo `host` da imagem acima precisa ser exatamente igual — caso contrário, falhará.

> **#IMPORTANTE**
>
> Usar **tempo** para limitar o retorno de eventos é a maneira mais eficiente de filtrar. Quanto menos dados precisar pesquisar, mais rápido o Splunk será.
>
> Depois do tempo, os campos de **index**, **source**, **host** e **sourcetype** são os mais poderosos em eficiência. Esses campos são extraídos no *index time*, então não precisam ser extraídos a cada pesquisa.

**Boas práticas de pesquisa:**

- Quanto mais específica for a pesquisa, melhores os resultados. Ex: prefira `failed password` a apenas `password`.
- **Inclusão > Exclusão:** pesquisar `"access denied"` é melhor do que `NOT access granted`.
- Quando possível, use operadores `OR` ou `IN` em vez de *wildcards*, pois filtram mais e tornam a pesquisa mais rápida.

---

## O que são Knowledge Objects?

<div align="center">
  <img src="images/KO.png" width="400">
</div>

*Knowledge Objects* são agrupados em **5 categorias**. Eles são úteis por diversos motivos no Splunk:

- Podem ser criados por um usuário e distribuídos para outros, baseado em configurações de permissão.
- Podem ser salvos e reutilizados por diversas pessoas ou múltiplos apps.
- Podem ser utilizados em pesquisas.

**Knowledge Managers** são responsáveis por:

- Supervisionar a criação de *Knowledge Objects*
- Normalizar *event data*
- Implementar convenções de nomenclatura
- Criar *data models*

### Campos (Fields)

<div align="center">
  <img src="images/KOdi.png" width="400">
</div>

Alguns campos são automaticamente extraídos dos dados com base no *sourcetype* selecionado. Mas campos adicionais podem ser extraídos manualmente para adicionar mais insights. **Calculated fields** são adicionados aos eventos no *search time* e fazem cálculos baseados nos valores dos campos existentes.

### Classificações (Classifications)

<div align="center">
  <img src="images/KOdc.png" width="400">
</div>

- **Event types:** Permitem categorizar eventos com base nos termos de pesquisa.
- **Transações:** São grupos de eventos conceitualmente relacionados em um período de tempo.

### Enriquecimento (Enrichment)

<div align="center">
  <img src="images/KOde.png" width="400">
</div>

- **Lookups:** Permitem adicionar outros campos e valores ao evento que não estão no *indexed data*.
- **Workflow Actions:** Permitem criar links entre eventos que interagem com recursos externos ou aprofundam sua pesquisa.

### Normalização (Normalization)

<div align="center">
  <img src="images/KOdn.png" width="400">
</div>

- **Tags:** Permitem designar nomes descritivos para pares chave-valor. São como legendas para seus dados, permitindo pesquisar eventos com valores de campo específicos.
- **Field Aliases:** Fornecem uma maneira de normalizar dados de múltiplas origens. Você pode atribuir um ou mais aliases para cada campo extraído e aplicá-los em campos de uma *lookup table*.

### Data Models

<div align="center">
  <img src="images/KOdm.png" width="400">
</div>

**Data models** são datasets estruturados de forma hierárquica, que podem consistir de eventos, pesquisas e/ou transações.

---

## Criando Reports

E se precisarmos rodar a mesma pesquisa novamente no futuro, ou compartilhá-la com outros usuários? O Splunk torna isso simples com os **reports**.

**Exemplo:** Pesquisar eventos de falha de senha e adicionar contexto geográfico.

<div align="center">
  <img src="images/geocontext.png" width="400">
</div>

Adicionando um pipe com o comando `iplocation src_ip`, conseguimos adicionar contexto geográfico nos eventos retornados. Novos campos serão adicionados na barra lateral.

<div align="center">
  <img src="images/fieldc.png" width="400">
</div>

Expandindo o campo **Country**, conseguimos ver os top 10 acessos por países e também 4 links de report:

- *Top Values*
- *Top Values by Time*
- *Rare Values*
- *Events with this Field*

**Top Values:** Acrescenta o `top command` na pesquisa e permite visualizar os dados em gráfico de barras, coluna, círculo, entre outros.

<div align="center">
  <img src="images/geostats.png" width="400">
</div>

Substituindo o comando na pesquisa pelo `geostats`, podemos usar o contexto do `iplocation command` para plotar os dados em um mapa *cluster* ou *choropleth*.

Para compartilhar facilmente, salve como report pelo menu **Save As → Report**.

Ao salvar, você verá opções de **Título**, **Descrição**, **Conteúdo** e **Time Range Picker**. Sempre siga uma convenção de nomenclatura para manter os reports organizados.

### Permissões de Report

<div align="center">
  <img src="images/editperm.png" width="400">
</div>

> **#IMPORTANTE**
>
> Quando um report é criado, ele é configurado para ser visível **apenas por quem o criou**. Ao mudar o *display setting* para **"App"**, o report é compartilhado com todos os outros usuários do app (nesse caso, *Search & Reporting*).
>
> - A opção **"All Apps"** é restrita apenas para administradores.
> - *Power users* têm permissão de leitura e escrita no report.

Em **Run As**, você pode configurar o report para ser rodado como o dono do report ou como o usuário que está executando. Isso é importante para controle de acesso a dados sensíveis.

### Agendamento de Reports

<div align="center">
  <img src="images/editsche.png" width="400">
</div>

Usando o **Edit Schedule**, é possível configurar reports para serem rodados em intervalos de tempo. Isso pode:

- Reduzir estresse no ambiente causado por rodar novos *ad hoc searches*.
- Ser particularmente benéfico se o report é compartilhado com muitos usuários ou integrado em um dashboard.

**Trigger Actions** permite melhorar a funcionalidade dos reports, por exemplo, enviando os resultados por e-mail.

---

## Criando Dashboards

Visualizações ajudam a contar uma história melhor com seus dados. O Splunk permite visualizá-los de diversas formas.

<div align="center">
  <img src="images/dashpanel.png" width="400">
</div>

Ao salvar uma visualização como dashboard, você tem duas opções de frameworks:

- **Dashboard Clássico**
- **Dashboard Studio**

Atribua um título ao painel (ex: *"Failed Logins By User"*) e confirme o modelo de visualização desejado.

Em **Advanced Panel Settings**, você verá que o painel é alimentado por *Inline Search* e que o **Drilldown** pode ser configurado para tornar seus dashboards interativos — permitindo que usuários explorem dados além do que veem normalmente.

Você pode criar novas pesquisas para enriquecer o dashboard, como ver tentativas de login por tempo na última semana.

<div align="center">
  <img src="images/addpanel.png" width="400">
</div>

Em **+Add Panel**, você pode adicionar novos painéis sem precisar voltar à pesquisa. Selecionando por **Report**, é possível adicionar um report previamente criado (como o de geocontext) ao dashboard.

Em **More Actions**, você pode editar o drilldown e configurar o `onclick` para:

- Link to Search
- Link to Dashboard
- Link to Report
- Link to Custom URL
- Manage Tokens in this Dashboard

---

## Dashboard Studio

No menu de **3 pontos** de um dashboard, é possível cloná-lo no **Dashboard Studio**.

<div align="center">
  <img src="images/dashstudio.png" width="400">
</div>

Ao criar um dashboard no Studio, escolha entre dois layouts:

- **Absolute Layout:** Posicionamento *pixel-perfect* e totalmente personalizável.
- **Grid Layout:** *Snap-to* automático para alinhamento rápido dos painéis em linhas.

O Studio permite personalizar o dashboard selecionando e arrastando as bordas dos painéis, sendo mais visual e intuitivo que o editor XML do dashboard clássico.

<div align="center">
  <img src="images/comp.png" width="400">
</div>

| Modo       | Característica Principal                   |
|------------|--------------------------------------------|
| **Absolute** | Altamente personalizável (*pixel-perfect*) |
| **Grid**     | Simples, rápido e com alinhamento automático |