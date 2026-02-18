---
layout: default
title: Welcome to football.db.rsssf
---

# {{ page.title }}

<div class="toc" markdown="1">
Contents:

* [What's News (in 2026)?](#news)
* [What's the Rec.Sport.Soccer Statistics Foundation (RSSSF)?](#rsssf)
* [Background - What's (semi-)structured text?](#structured) 
* [Questions? Comments?](#questions)
</div>

<!--
* [How to use](#usage)
    * [Read in the RSSSF archive data](#read)
-->

## What's News (in 2026)?   {#news}

Note - there's no more plan / efforts to turn or "distill the conventions" 
from the Rec.Sport.Soccer Statistics Foundation (RSSF) match schedules & results into a structured text format with a context-free grammar (and lexer & parser).  Sorry, there are just too many variants, quirks and styles.

The good news - in most cases, yes, you can convert the RSSSF match schedules & results 
using its own "ad-hoc" formats (mostly depending on the original author) into the Football.TXT format,
that is, a structured text format with a context-free grammar (and lexer & parser) built on purpose from scratch / zero - 
either "by hand" or with your own little search & replace scripts or why not 
with the help of latest and greatest large language models (LLMs)?

Tip:  For samples of RSSSF pages (incl. the Premier League, FA Cup, Club World Cup, European Championship, and more) converted to the structured Football.TXT format 
(for easy parsing and exporting to JSON, CSV, SQL and friends),
see the `/rsssf` folder in the 
[`/euro`](https://github.com/openfootball/euro/tree/master/rsssf), 
[`/england`](https://github.com/openfootball/england/tree/master/rsssf) repos and others.



<!--

The [`sportdb` command line tool](https://github.com/sportdb) lets you
read in  league & cup match results & schedules in (semi-) structured text
from the the Rec.Sport.Soccer Statistics Foundation (RSSF)
into your SQL database of choice (SQLite, PostgreSQL, etc.).

-->



## What's the Rec.Sport.Soccer Statistics Foundation (RSSSF)?    {#rsssf}

The RSSSF collects and offers football (soccer) league & cup match results & schedules
from all over the world online in a (semi-)structured text format. Example (RSSSF before):

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

or using an alternate format style (RSSSF before):

```
Round 1
[May 25]
Vasco da Gama   1-0 Portuguesa
 (Carlos Tenório 47)
Vitória         2-2 Internacional
 (Maxi Biancucchi 2, Gabriel Paulista 11 - Diego Forlán 29, Fred 63)
Corinthians     1-1 Botafogo
 (Paulinho 73 - Rafael Marques 24)
[May 26]
Grêmio          2-0 Náutico         [played in Caxias do Sul-RS]
 (Zé Roberto 15, Elano 70)
Ponte Preta     0-2 São Paulo
 (Lúcio 9, Jádson 44 p)
Criciúma        3-1 Bahia
 (Matheus Ferraz 45+1, Lins 46, João Vítor 82 - Diones 72)
Santos          0-0 Flamengo        [played in Brasília-DF]
Fluminense      2-1 Atlético/PR     [played in Macaé-RJ]
 (Rafael Sóbis 15 p, Samuel 53 - Manoel 28)
Cruzeiro        5-0 Goiás
 (Diego Souza 5, Bruno Rodrigo 30, Nílton 40,79, Borges 42)
Coritiba        2-1 Atlético/MG
 (Deivid 53, Arthur 90+1 - Diego Tardelli 51)
```





Yes, you can!  Let's convert the sample to the Football.TXT format:

```
▪ Round 1
May 25
  Vasco da Gama   1-0 Portuguesa
    (Carlos Tenório 47')
  Vitória         2-2 Internacional
    (Maxi Biancucchi 2', Gabriel Paulista 11'; Diego Forlán 29', Fred 63')
  Corinthians     1-1 Botafogo
    (Paulinho 73'; Rafael Marques 24')
May 26
  Grêmio          2-0 Náutico         [played in Brasília-DF]
    (Zé Roberto 15', Elano 70')
  Ponte Preta     0-2 São Paulo
    (Lúcio 9', Jádson 44'p)
  Criciúma        3-1 Bahia
    (Matheus Ferraz 45'+1', Lins 46', João Vítor 82'; Diones 72')
  Santos          0-0 Flamengo        [played in Brasília-DF]
  Fluminense      2-1 Atlético/PR     [played in Macaé-RJ]
    (Rafael Sóbis 15'p, Samuel 53'; Manoel 28')
  Cruzeiro        5-0 Goiás
    (Diego Souza 5', Bruno Rodrigo 30', Nílton 40',79', Borges 42')
  Coritiba        2-1 Atlético/MG
    (Deivid 53', Arthur 90'+1'; Diego Tardelli 51')
```

What's changed? <br>
-  Start round lines with a round marker `▪`.
-  Do NOT enclose date headers / lines with square brackets `[]`. 
-  Enclose goal lines with parentheses, that is, `()` instead of square brackets `[]`


Football.TXT Format Notes -  Yes, the minute marker `'` is optional
and the separator for goals of team home/away is `;` or `-`.
Let's try:

```
▪ Round 1
May 25
  Vasco da Gama   1-0 Portuguesa     (Carlos Tenório 47)
  Vitória         2-2 Internacional  (Maxi Biancucchi 2, Gabriel Paulista 11 - Diego Forlán 29, Fred 63)
  Corinthians     1-1 Botafogo       (Paulinho 73 - Rafael Marques 24)
May 26
  Grêmio          2-0 Náutico       [played in Brasília-DF]
                         (Zé Roberto 15, Elano 70)
  Ponte Preta     0-2 São Paulo      (Lúcio 9, Jádson 44p)
  Criciúma        3-1 Bahia          (Matheus Ferraz 45+1, Lins 46, João Vítor 82 - Diones 72)
  Santos          0-0 Flamengo      [played in Brasília-DF]
  Fluminense      2-1 Atlético/PR   [played in Macaé-RJ]
                         (Rafael Sóbis 15p, Samuel 53 - Manoel 28)
  Cruzeiro        5-0 Goiás          (Diego Souza 5, Bruno Rodrigo 30, Nílton 40,79, Borges 42)
  Coritiba        2-1 Atlético/MG    (Deivid 53, Arthur 90+1 - Diego Tardelli 51)
```


or the max goal version style (RSSSF before):

```
Round 1
[May 25]
Vasco da Gama   1-0 Portuguesa
 [1-0 Carlos Tenório 47]
Vitória         2-2 Internacional
 [1-0 Maxi Biancucchi 2, 2-0 Gabriel Paulista 11, 2-1 Diego Forlán 29, 2-2 Fred 63]
Corinthians     1-1 Botafogo
 [1-0 Rafael Marques 24, 1-1 Paulinho 73]
[May 26]
Grêmio          2-0 Náutico         [played in Caxias do Sul-RS]
 [1-0 Zé Roberto 15, 2-0 Elano 70]
Ponte Preta     0-2 São Paulo
 [0-1 Lúcio 9, 0-2 Jádson 44 p]
...
```






[Find out more about the Rec.Sport.Soccer Statistics Foundation (RSSSF) »](https://www.rsssf.com)


<!--

## How to use  {#usage}

### Read in the RSSSF (semi-)structured text archive data   {#read}

As an example let's read in the Campeonato Brasileiro Série A
([`brazil/2012`](https://github.com/rsssf/brazil/blob/master/2012),
[`brazil/2013`](https://github.com/rsssf/brazil/blob/master/2013), et al).


Step 1: Get a copy of the RSSSF data

    $ git clone git://github.com/rsssf/brazil.git

Step 2: Let's read in the Campeonato Brasileiro Série A

    $ sportdb build ./rsssf/brazil


That's it.

-->

<!--
Note: Before loading RSSSF archive data you will need to add a configuration file
listing all football clubs / teams included in the league.
See the Campeonato Brasileiro Série A
([`brazil/2012/seriea.yml`](https://github.com/rsssf/brazil/blob/master/2012/seriea.yml),
[`brazil/2013/seriea.yml`](https://github.com/rsssf/brazil/blob/master/2013/seriea.yml))
as an example.
-->



## Background - What's (semi-) structured text?    {#structured}

Q: How does the "magic" work? 

A: If the text follows the Football.TXT (structured text) format conventions than you can use
the Football.TXT lexer & parser machinery to "automagically" break-up the text into its (semantic) parts, that is, tokens (that build-up the parse tree and more) resulting in:

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

For more, see the [Football.TXT format, level 1 & 2 specs »](https://openfootball.github.io/spec/)


{% include questions.md %}
