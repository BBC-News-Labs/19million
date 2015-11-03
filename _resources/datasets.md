---
layout: post
title: Datasets
description: n=all, right
---

We're already coming across a lot of data, from very different sources. Let's try to keep of track of all this.

---

### UNHCR

The United Nations High Commissioner for Refugees has a nice [data portal](http://data.unhcr.org/), which sums up all its missions. For this event, the [Mediterranean portal](http://data.unhcr.org/mediterranean/regional.php) is by far the most useful, documenting routes and sea arrivals - as well as keeping up to date the number of dead and missing persons.

There's a lot in there, including a [documented and free](http://data.unhcr.org/wiki/index.php/API_Documentation) API. Check out [Aendrew's Postman collection](https://gist.githubusercontent.com/aendrew/d7189c1322dd275cdf0c/raw/65363fc9568d2a6875eb1ebaf125df3fe3216e2f/UNHCR.json.postman_collection), by the way.

### Eurostat

The Commission's statistical agency keeps records of a bunch of things, including of asylum applications and first instance decisions in the EU-28. Here's their [September 2015 quarterly report](http://ec.europa.eu/eurostat/statistics-explained/index.php/Asylum_quarterly_report), as well as [a ton more data](http://ec.europa.eu/eurostat/statistics-explained/index.php/Asylum_quarterly_report#Further_Eurostat_information), and [the full dataset](http://appsso.eurostat.ec.europa.eu/nui/show.do) (complete with its silly webapp).

[John Burn-Murdoch](https://twitter.com/jburnmurdoch) used [this R package](https://cran.r-project.org/web/packages/SmarterPoland/SmarterPoland.pdf) yesterday for his workshop - which will automate fetching the data. Here's a [link to John's R script](https://gist.github.com/johnburnmurdoch/5424442fd49d67f6672e).

### World Bank

The World Bank has a dataset running from 1981 to 2014 called "[Refugee population by country or territory of asylum](http://data.worldbank.org/indicator/SM.POP.REFG)." The data can be grabbed in XLS, XML, and CSV format.
