# football.db.rsssf

The [`sportdb` command line tool](https://github.com/geraldb/sport.db.ruby) lets you
load archive data
from the the Rec.Sport.Soccer Statistics Foundation (RSSF)
into your SQL database of choice (sqlite, postgres, mysql, etc.).


## What is the Rec.Sport.Soccer Statistics Foundation (RSSSF)?

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


## How to use

As an example let's load the Campeonato Brasileiro Série A
([`br-brazil/2012.txt`](https://github.com/geraldb/football.db.rsssf/blob/master/br-brazil/2012.txt),
[`br-brazil/2013.txt`](https://github.com/geraldb/football.db.rsssf/blob/master/br-brazil/2013.txt)).


### Setup the database

Step 1: Get a copy of the `world.db` fixtures

    $ git clone git://github.com/geraldb/world.db.git

Step 2: Get a copy of the `br-brazil` fixtures

    $ git clone git://github.com/openfootball/br-brazil.git

Step 3: Let's build the `football.db`

    $ sportdb setup --include ./br-brazil --worldinclude ./world.db


### Load the RSSSF archive data

Step 1: Get a copy of the RSSSF data

    $ git clone git://github.com/geraldb/football.db.rsssf.git

Step 2: Let's load the Campeonato Brasileiro Série A

    $ sportdb update br --include ./football.db.rsssf


That's it.


Note: Before loading RSSSF archive data you will need to add a configuration file
listing all football clubs / teams included in the league.
See the Campeonato Brasileiro Série A
([`br-brazil/2012.yml`](https://github.com/geraldb/football.db.rsssf/blob/master/br-brazil/2012.yml),
[`br-brazil/2013.yml`](https://github.com/geraldb/football.db.rsssf/blob/master/br-brazil/2013.yml))
as an example.


## Questions? Comments?

Send them along to the [Open Sports Database & Friends Forum/Mailing List](http://groups.google.com/group/opensport).
Thanks!

