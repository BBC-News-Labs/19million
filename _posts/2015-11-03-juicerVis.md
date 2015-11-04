---
layout: post
title: Media on refugees
---

<a href="http://bl.ocks.org/sytpp/raw/277fd63145785d360193/"><img class="center" src="/img/2015-11-03_rplot1.JPG" width="700"></a>

The 19 Million Project here in Rome addresses the most recent immigration wave into Europe - but not only this. 19 million are refugees who have left their home country because of war and conflict. 

> **"We are talking about the European immigration crisis but this has been going on since long all over the world"**, one speaker pointed out this morning.

We wanted to check out if we can see that in the media coverage. [The Juicer](http://bbcnewslabs.co.uk/projects/juicer/), our home-made news aggregation system allows us to look into this question.

The Juicer has a provisional front end (which isn't public... yet) but its core bit is the a aggregation of news streams via RSS feeds and the extraction of meaningful metadata from these news, all of which can be accessed via [an API](http://docs.bbcnewslabs.co.uk/Juicer-2.html).

The graphic on top shows you that the speaker was right. Migration may be happening all the time but we are talking about it only recently because the mainstream media, including the BBC, has increased its coverage massively since September this year, when [the picture of Aylan Kurdi](http://www.bbc.com/news/world-europe-34133210) went around the world.

The [interactive graphic](http://bl.ocks.org/sytpp/raw/277fd63145785d360193/) shows the number of articles per day and links to the original pages on the respective outlet.

---

The script below shows how we can extract the number of news stories mentioning the word 'refugee' in the text and visualise it.

    library(RCurl)
    library(XML)
    library(jsonlite)
    library(plyr)
    library(reshape)
    library(ggplot2)


The Juicer holds around 400 sources available at the moment, the source IDs stand for individual publications.

    sourceIDs <- c(1, 8, 43, 160, 89)
    sourcestring <- ""
    for(s in sourceIDs){sourcestring <- paste(sourcestring,"&sources%5B%5D=",s, sep="")}
    sourcestring
     
    query = "refugee" 	## --- query string
    
    after = "2015-01-01" 	## --- dates
    before = "2015-11-01"
    
    key = 'xxxxxxxxxxxxx' 	## --- API key
    
    search <- paste("http://data.test.bbc.co.uk/bbcrd-juicer/articles?",
                      "q=", query,
                      "&apikey=", key, 
                      "&recent_first",
                      sourcestring ,
                      "&published_after=",after,"T00:00:00.000Z",
                      "&published_before=",before,"T00:00:00.000Z",    
                      sep="")
      contentJSON <- getURL(search)
      contentDF <- fromJSON(contentJSON) 
      
    articleSource = contentDF$hits$source[,"source-name"]
    articleDate = contentDF$hits$published
    articleTitle = contentDF$hits$title
    write(paste(articleSource, articleDate, articleTitle, sep="\t"),file=paste("JuicerA_", query, "_", total,".meta",sep=""),append=TRUE)

To visualise we use [R's ggplot2](http://ggplot2.org/) library - just to get an idea - and make it pretty and interactive with [D3](http://d3js.org/) later.

    metaDF$helper <- 1
    metaDFsort <- metaDF[order(metaDF$V1),] # sort
    plotDF2 <- ddply(metaDFsort, .(articleDate3), mutate, counter=1:sum(helper))
    
    ggplot(plotDF2, aes(fill=as.factor(V1))) + 
      geom_rect(aes(xmin=as.Date(articleDate3), xmax=as.Date(articleDate3+5), ymin=counter, ymax=counter+0.8)) +
      labs(x="", y="# news articles per week", fill="") +
      ggtitle(paste(total, "news articles with the word '",query, "'", sep=" ")) +
      scale_fill_brewer(palette="Set1") +
      plottheme +
      theme(legend.position="top")






















