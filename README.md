# Iniciando com Domain Driven Design, CQRS e EventSourcing

Para este artigo, estará sendo apresentado exemplos em C# utilizando Dotnet Core 3.1

## Introdução

Atualmente, os sistemas devem estar sempre preparados para a grande quantidade de demandas e para isso é necessário ter conhecimento em frameworks, design patterns, padrões de projetos e por fim, ter conhecimento em arquitetura. Com isto, o **DDD** e **CQRS** recebe muito destaque por solucionar problemas de domínios complexos e desempenho.
Neste artigo será apresentado um pouco sobre como utilizar CQRS com DDD. Com isto, sempre surgem algumas duvidas, como: Quando devo utilizar? Quais as vantagens e desvantagens? Devo utilizar duas bases de dados? se acalmeee, tudo será esclarecido. 

## Caso de Uso - Transferencia Bancaria

O exemplo será aplicado em cima de um contexto de sistema bancário especificamente em um sistema de Saldo onde existem varias transações como:
- transferência
- saque
- deposito
- extrato
- pagamento 

Será implementadas apenas as transações de **transferência** e **extrato**.
Em um modelo tradicional seria criado uma base de dados com uma tabela chamada Saldo como é ilustrado abaixo.

![](https://raw.githubusercontent.com/rafaeldias97/MicroServiceExample/master/files/tradicional.png)

Nota-se que neste cenario serão realizadas varias transações no banco de dados, devido a grande quantidade de demandas, naturalmente vem a necessidade de escalar o serviço de sistema de conta, porém, os recursos do banco de dados se tornariam concorrentes trazendo travamentos, lentidões e deadlocks.

![](https://raw.githubusercontent.com/rafaeldias97/MicroServiceExample/master/files/dbfailed.png)

A primeira solução que iria vir, seria escalar verticalmente, adicionando mais recursos no seu servidor, contudo seria uma solução um pouco mais custosa.

------------ imagem escalar banco verticalmente custo ---------------

## CQRS - command query responsibility segregation

Então, se pensarmos como arquitetos e tirarmos um pouco da responsabilidade da infra, poderemos criar algo como um banco de dados master/slave.

------------ Imagem Banco Master Slave ---------------

Com isto, chegamos a estrutura do **CQRS (command query responsibility segregation)** do português **(Separação entre comando e consulta)**. O CQRS é um padrão de arquitetura em que como o nome é autoexplicativo é separado em dois objetos de **leitura/commands** e **escrita/query**. Não é necessário o uso de dois bancos de dados porém, para ter o máximo de desempenho é ideal ter pelo menos duas bases dependendo do caso, um para escrita e outra para leitura, sendo que existem varias formas de implementar o CQRS.

Para o modelo que estará sendo ilustrando, será utilizado dois bancos de dados. O banco de dados de escrita e outro para leitura. Lembrando que o CQRS deve ser utilizado apenas em sistemas onde a **concorrência é alta** e contenha **altas requisições de leitura e escrita em uma mesma base de dados**, caso contrário o aumento da complexidade de codig,o seria desnecessário visto que, não haverá ganhos significativos na performace.


---##Aumento da complexidade na implementação, é muito importante em uma equipe o conhecimento de DDD (Domain Driven Design), logo não devo utilizar CQRS em todos os cenários ##----








