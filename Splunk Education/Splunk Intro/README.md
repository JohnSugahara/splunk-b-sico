# SPLUNK E-LEARNING, CISCO-SPLUNK>

## Introduction Splunk

### Objetivos Do Curso
Exploring Splunk Web
Running Searches
Using Commands
Creationg Reports
Creating Dashboards
Understanding Knowledge Objects

*Vamos Assumir uma Empresa Bettercup Games*
Offices in
Sao Francisco
Boston
e Londres

Antigamente se um cliente fosse contatar o suporte sobre um problema, o problema seria dado de um membro para poutro, os foraçando a parar tudo que estavam fazendo para resolver o problema, o que, ocasionava em problemas de gestão de tempo e recursos, e frustando todos inclusive o cliente.

Mas com o Splunk Suite of Products, eles podem usar toda a data do ambiente para resolver em menos tempo.
Ceasar(Trabalhador): Quando o pedido de suporte vem, ele é automaticamente direcionado para um application support, aonde Ceaser pesquisa os dados por eventos de tentativas que compra que terminaram em erro, dessa forma ele pode achar o evento que se assemelha a experiência do usuario. 
Esse evento está ligado a um Database query, a qual pode ser correlatada a uma entrada na slow query log, permitindo Caesar direcionar esse problema para o seu admin em minutos, sem ter que envolver o time inteiro.

Mas melhor que isso, e se conseguirmos alertar quando uma transação falhar?
Antes mesmo que o proprio cliente contate o suporte tecnico? Permitindo que Caesar faça uma triagem do problema, antes que o mesmo cause problemas maiores mais tarde.

Splunk é uma plataforma de dados unificada, que permite times trabalharem juntos ou individualmente.

No coração do Splunk existe o Index, que contem sua machine data de fontes, como servers, network devices, e aplicações web

Imagine que o Index é uma fabrica e seus dados o material cru, quando dados entram os inspetores trabalham, eles olham pros dados e decidem como processar eles, quando eles encontram uma semelhança ele nomeam o dado com um source type(src_type), então esse src_type é usada para quebrar os dados em eventos unicos(login error), a data do ocorrido sao indentificados e normlizados em um formato consistente.

Quando o dado é ingerido pelo INDEX, ele fica disponivel para pesquisa e analise.
Ao entrar uma query na barra de pesquisa do Splunk voce pode encontrar eventos que contem valores atraves de multiplos fontes de dados. 

Resultados de pesquisa podem ser salvos como reports, que podem prover percepções continuamente em seus dados e pode ser usado para potencializar os paneis de dashboard.

Conhecimentos podem ser organizados em datasets estruturados, chamados de data models. Para assim permitir que usuarios visualizem rapidamente data em Pivot sem ter que escrever escritas de pesquisa costumizadas. 

---

#### Como usar o splunk web?

Ao logar no splunk> enterprises você entrara no splunk home app, app's são areas de trabalho pré configuradas.

No splunk existem três funções principais:

Admin: A função mais poderosa, pode instalar apps, ingerir dados e criar para todos usuarios knowledge objects.
Power: A função Power, pode criar e compartilhar knowledge objects com todos usuarios de um app e realizar pesquisas em tempo real. 
User: O usuario, apenas pode ver os seus proprios knowledge objects e os que foram compartilhados com eles.

Splunk Cloud similarmente possui as funções de sc_admin, power e user, assim como funções expeciais para cloud como can_delete, token_auth e apps.

Sumario de dados:

Hosts: É o Hostname, endereço IP ou nome qualificado de dominio da maquina que o evento originou.

Sourcetypes: É a classificação dos dados.

Sources: É a pasta ou caminho de diretorio, network port, ou script da onde o evento originou.

#### Pesquisa no Splunk.

Filtrar uma pesquisa por tempo é a maneira mais rápida para ter resultados e uma boa prática.

Save As, permite salvar a pesquisa como um Knowledge Object.

Comandos que criam estatisticas e visualizações são chamandos de comandos de transformação. Esses são comandos que transforma dados de eventos em tabela de dados.

A opção "Job" permite você editar, mandar para o background, inspecionar e deletar Search Jobs.
Ao lado a opções de baixar, compartilhar, pausar, continuar e imprimir jobs.

Ao compartilhar um link é gerado, naturalmente um search job vai ficar ativo por 10 minutos depois de ter sido iniciado, depois de 10 minutos, splunk, tera que rodar o job novamente para obter os resultados. Um shared job por outro lado fica ativo por 7 dias e vai ser visivel para todos com o link.

O Export permite exportar em raw, CSV, XML e JSON.
Existem três modos de pesquisar no search mode.

Fast Mode: Field Discovery é desativado para esse modo, apenas retorna informações de default fields e fields necessarios para sua pesquisa.

Smart Mode: O Default Smart Mode, vai desativar comportamento baseado no tipo de pesquisa que voce está fazendo.

Verbose Mode: Retorna toda field e event dada possivel, descobrindo todos os field que pode.

#### Explorando Eventos.

Eventos quando pesquisados tem a palavra pesquisada grifada e retornada em ordem cronologica inversa(o mais recente para o mais antigo).
Enquanto a data é normalizada por (dia)/(mês)(ano) o horario é determinado pela sua timezone.
Ao clicar em um texto você pode adicionar ele a pesquisa, excluir eventos que o contenham na pesquisa ou lançar uma nova pesquisa usando o texto.

Clicando no botão info de um evento você é capaz de ver todos os field events extraidos, com checkmarks nos fields selecionados.

### Usando termos de pesquisa.

Wild Card: É um termo usado para um tipo de pesquisa que procura todos os semelhantes que começam com a palavra escrita, exemplo:
fail* = failed, failure, failedpassword, failures etc ...

**BOOLEANOS:** AND, OR e NOT, podem ser usados com diversos termos.

failed NOT password == todos eventos failed sem password
failed AND password == todos eventos com failed e password
failed OR password == todos eventos de failed ou password.

Sem booleanos o AND é implicito, exemplo

faile password == failed AND password.

Ordem de avaliação dos booleanos:

1. NOT, 2. OR, 3. AND

"()" podem ser usados para controlar a ordem e avaliação.

Frases podem ser achadas se pesquisado como "frase aleatoria".
Quando pesquisar algo que possui ", voce pode usar \ para sair do ", considerando ele como pesquisa e nao frase.

### O que são comandos?

