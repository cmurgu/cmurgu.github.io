---
title: 'Representing Sentiment Scores of Specific Locations with Original Music. An exercise in musicdh'
intro: ""
published: true
date: "2020-01-31"
publish_date: '01-31-2020 00:00'
taxonomy:
    tag:
        - blog
---

In Spring 2020, I had the opportunity to co-sponsor an independent study project for 2nd year student at New College. The objective seemed simple enough: study the intersection of music and the digital humanities and produce a project that represents that intersection. It seems to me that the fields of musicology and music composition have not been affected by the digital humanities to the same degree as other fields. With respect to the latter, perhaps this is because composition turned towards the digital decades ago. To be sure, work is being done in the field of musicDH: [Frontiers in Digital Humanities]( https://www.frontiersin.org/journals/digital-humanities/sections/digital-musicology) have published about a dozen articles on the topic, and there are several interesting projects, such as the [Listening Experience Database]( https://led.kmi.open.ac.uk/) that open up rich opportunities for digital musicology. This is where we found ourselves in late December. 

Of all the different techniques in natural language processing, we were most intrigued by sentiment analysis due to the innate sentimentality of music. How could we bring natural language processing and original composition together? Our plan was as follows.

**Step 1**

Identify locations on the New College campus (the library, the bayfront, the dorms, etc), and survey a group of students about how those locations make them feel. 

**Step 2**

Using NLTK/TextBlob, derive a sentiment score for each response (from -1 to +1) and average the score of each location to identify a composite sentiment score.

**Step 3**

Determine 5 unique mood thresholds in your sentiment range (for example, -0.2 to 0.2 represents a ‘neutral’ sentiment) and compose original music that represents that sentiment. 

**Step 4**

Finally, map the locations on Leaflet as polygons. Using the [Buzz library]( http://buzz.jaysalvat.com/documentation/), assign a mouseover event to fade-in the music that correlates to the composite sentiment of each location, and a mouseout event to fade-out the music as the cursor leaves the polygon. 

**Stretch Goal**

Visualize the sentiment breakdown of each location in a tooltip or marker. 

You can see the result below (or click [here](https://dss.ncf.edu/class/ISP/musicdh)).

{{< hp5 "https://dss.ncf.edu/class/ISP/musicdh" >}}

As you hover your cursor over each location, music will begin to fade-in (adjust your volume!). Each piece of music is an original composition that represents a particular sentiment for the student that composed it. Ultimately, this project at once flirts with objective measurement (i.e., attempting to determe a sentiment score) while at once leaving room for subjective interpretation (creating a piece of music based on something as fickle and unique as an emotional response). 


In a subsequent meeting, my colleague [Mark Dancigers](http://dancigers.com/) made the following fascinating point about data in general and this project in particular. We collect data because it helps us make (in theory) the most effective decisions viz. a problem, and numbers/tables/graphs are fantastic vehicles of representation (i.e., doctors require data to make decisions regarding a patient's wellbeing). The act of abstraction simplifies the act of problemsolving. However, abstracting data into music works to complicate the above by introducing subjectivity in the act of reception (imagine if a physician had to make decisions based on a musical representation of a patient's cholesterol level, complicated by the fact that the music was composed by someone other than the physician). 

Ultimately, this project sits somewhere in the middle between public art and research into natural language processing and reception. It's also a (successful, if you ask me) example of how short project sprints with diverse teammembers can yield fantastic prototypes and generate potentially fruitful areas of research and creative expression.




