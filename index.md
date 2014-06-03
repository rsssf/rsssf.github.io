---
layout: default
title: Welcome to football.db.rsssf
---

# {{ page.title }}

<div class="toc" markdown="1">
Contents:

* [What's the Rec.Sport.Soccer Statistics Foundation (RSSSF)?](#rsssf)
* [How to use](#usage)
    * [Setup the database](#setup)
    * [Load the RSSSF archive data](#load)
* [Questions? Comments?](#questions)
</div>


The [`sportdb` command line tool](https://github.com/geraldb/sport.db.ruby) lets you
load archive data
from the the Rec.Sport.Soccer Statistics Foundation (RSSF)
into your SQL database of choice (SQLite, PostgreSQL, etc.).


## What's the Rec.Sport.Soccer Statistics Foundation (RSSSF)?    {#rsssf}

The RSSSF collects and offers football (soccer) league tables
from all over the world online in plain text.

Example:

~~~
Round 1
[May 25]
Vasco da Gama   1-0 Portuguesa
 [Carlos Tenório 47']
Vitória         2-2 Internacional
 [Maxi Biancucchi 2', Gabriel Paulista 11'; Diego Forlán 29', Fred 63']
Corinthians     1-1 Botafogo
 [Paulinho 73'; Rafael Marques 24']
[May 26]
Grêmio          2-0 Náutico         [played in Caxias do Sul-RS]
 [Zé Roberto 15', Elano 70']
Ponte Preta     0-2 São Paulo
 [Lúcio 9', Jádson 44'p]
Criciúma        3-1 Bahia
 [Matheus Ferraz 45'+1', Lins 46', João Vítor 82'; Diones 72']
Santos          0-0 Flamengo        [played in Brasília-DF]
Fluminense      2-1 Atlético/PR     [played in Macaé-RJ]
 [Rafael Sóbis 15'p, Samuel 53'; Manoel 28']
Cruzeiro        5-0 Goiás
 [Diego Souza 5', Bruno Rodrigo 30', Nílton 40',79', Borges 42']
Coritiba        2-1 Atlético/MG
 [Deivid 53', Arthur 90'+1'; Diego Tardelli 51']
~~~

[Find out more about the Rec.Sport.Soccer Statistics Foundation (RSSSF) »](http://www.rsssf.com)



## How to use  {#usage}

As an example let's load the Campeonato Brasileiro Série A
([`br-brazil/2012`](https://github.com/rsssf/br-brazil/blob/master/2012),
[`br-brazil/2013`](https://github.com/rsssf/br-brazil/blob/master/2013)).


### Setup the database   {#setup}

Step 1: Get a copy of the `world.db` fixtures

    $ git clone git://github.com/openmundi/world.db.git

Step 2: Get a copy of the `br-brazil` fixtures

    $ git clone git://github.com/openfootball/br-brazil.git

Step 3: Let's build the `football.db`

    $ sportdb setup teams --include ./openfootball/br-brazil --worldinclude ./openmundi/world.db


### Load the RSSSF archive data   {#load}

Step 1: Get a copy of the RSSSF data

    $ git clone git://github.com/rsssf/br-brazil.git

Step 2: Let's load the Campeonato Brasileiro Série A

    $ sportdb update --include ./rsssf/br-brazil


That's it.


Note: Before loading RSSSF archive data you will need to add a configuration file
listing all football clubs / teams included in the league.
See the Campeonato Brasileiro Série A
([`br-brazil/2012/seriea.yml`](https://github.com/rsssf/br-brazil/blob/master/2012/seriea.yml),
[`br-brazil/2013/seriea.yml`](https://github.com/rsssf/br-brazil/blob/master/2013/seriea.yml))
as an example.


{% include questions.md %}
