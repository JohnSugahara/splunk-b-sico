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

#### O que é Splunk Web?

