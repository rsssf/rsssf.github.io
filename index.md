---
layout: default
title: Welcome to football.db.rsssf
---

# {{ page.title }}

<div class="toc" markdown="1">
Contents:

* [What's the Rec.Sport.Soccer Statistics Foundation (RSSSF)?](#rsssf)
* [How to use](#usage)
    * [What's the (semi-)structured text?](#structured)
    * [Read in the RSSSF (semi-)structured text archive data](#read)
* [Questions? Comments?](#questions)
</div>


The [`sportdb` command line tool](https://github.com/sport.db) lets you
read in  league & cup match results & schedules in (semi-) structured text
from the the Rec.Sport.Soccer Statistics Foundation (RSSF)
into your SQL database of choice (SQLite, PostgreSQL, etc.).



## What's the Rec.Sport.Soccer Statistics Foundation (RSSSF)?    {#rsssf}

The RSSSF collects and offers football (soccer) league & cup match results & schedules
from all over the world online in a (semi-)structured text format. Example:

```
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
```

[Find out more about the Rec.Sport.Soccer Statistics Foundation (RSSSF) »](http://www.rsssf.com)




## How to use  {#usage}

As an example let's read in the Campeonato Brasileiro Série A
([`br-brazil/2012`](https://github.com/rsssf/br-brazil/blob/master/2012),
[`br-brazil/2013`](https://github.com/rsssf/br-brazil/blob/master/2013)).


### What's the (semi-) structured text?    {#structured}

If the text follows the RSSSF (structured text) format conventions than you can use
the (sportdb) RSSSF parser (& tokenizer) to break-up the text into its (semantic) parts - resulting in:

``` ruby
[[:round, "Round 1"]],
[[:date, "May 25"]],
[[:team, "Vasco da Gama"], [:score, "1-0"], [:team, "Portuguesa"]],
  [[:player, "Carlos Tenório"], [:minute, "47'"]],
[[:team, "Vitória"], [:score, "2-2"], [:team, "Internacional"]],
  [[:player, "Maxi Biancucchi"],[:minute, "2'"],[:","],
   [:player, "Gabriel Paulista"],[:minute, "11'"],[:";"],
   [:player, "Diego Forlán"],[:minute, "29'"],[:","],
   [:player, "Fred"],[:minute, "63'"]],
[[:team, "Corinthians"], [:score, "1-1"], [:team, "Botafogo"]],
  [[:player, "Paulinho"], [:minute, "73'"], [:";"], 
   [:player, "Rafael Marques"], [:minute, "24'"]],
[[:date, "May 26"]],
[[:team, "Grêmio"], [:score, "2-0"], [:team, "Náutico"], [:note, "played in Caxias do Sul-RS"]],
  [[:player, "Zé Roberto"], [:minute, "15'"], [:","], 
   [:player, "Elano"], [:minute, "70'"]],
[[:team, "Ponte Preta"], [:score, "0-2"], [:team, "São Paulo"]],
  [[:player, "Lúcio"], [:minute, "9'"], [:","], 
   [:player, "Jádson"], [:minute, "44'"], [:pen, "p"]],
[[:team, "Criciúma"], [:score, "3-1"], [:team, "Bahia"]],
  [[:player, "Matheus Ferraz"],[:minute, "45'+1'"],[:","],
   [:player, "Lins"],[:minute, "46'"],[:","],
   [:player, "João Vítor"],[:minute, "82'"],[:";"],
   [:player, "Diones"],[:minute, "72'"]],
[[:team, "Santos"], [:score, "0-0"], [:team, "Flamengo"], [:note, "played in Brasília-DF"]],
[[:team, "Fluminense"], [:score, "2-1"], [:team, "Atlético/PR"], [:note, "played in Macaé-RJ"]],
  [[:player, "Rafael Sóbis"],[:minute, "15'"],[:pen, "p"],[:","],
   [:player, "Samuel"],[:minute, "53'"],[:";"],
   [:player, "Manoel"],[:minute, "28'"]],
[[:team, "Cruzeiro"], [:score, "5-0"], [:team, "Goiás"]],
  [[:player, "Diego Souza"],[:minute, "5'"],[:","],
   [:player, "Bruno Rodrigo"],[:minute, "30'"],[:","],
   [:player, "Nílton"],[:minute, "40'"],[:","],[:minute, "79'"],[:","],
   [:player, "Borges"],[:minute, "42'"]],
[[:team, "Coritiba"], [:score, "2-1"], [:team, "Atlético/MG"]],
  [[:player, "Deivid"],[:minute, "53'"],[:","],
   [:player, "Arthur"],[:minute, "90'+1'"],[:";"],
   [:player, "Diego Tardelli"],[:minute, "51'"]]] 
```

### Reald in the RSSSF (semi-)structured text archive data   {#read}

Step 1: Get a copy of the RSSSF data

    $ git clone git://github.com/rsssf/brazil.git

Step 2: Let's read in the Campeonato Brasileiro Série A

    $ sportdb build ./rsssf/brazil


That's it.

<!--
Note: Before loading RSSSF archive data you will need to add a configuration file
listing all football clubs / teams included in the league.
See the Campeonato Brasileiro Série A
([`br-brazil/2012/seriea.yml`](https://github.com/rsssf/br-brazil/blob/master/2012/seriea.yml),
[`br-brazil/2013/seriea.yml`](https://github.com/rsssf/br-brazil/blob/master/2013/seriea.yml))
as an example.
-->


{% include questions.md %}