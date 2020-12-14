---
title: 'Visualizing Librarian/Faculty Interaction Data with R'
intro: "Visualizing library data using R and visNetwork!"
published: true
date: "2019-07-19"
publish_date: '07-19-2019 00:00'
taxonomy:
    tag:
        - blog
        - r
        - practice
---

Thanks to Jesse Sadler and their
[blog](https://www.jessesadler.com/post/network-analysis-with-r/) for
this information. It was very, very helpful for a novice like me. I
find that I learn best when I have a specific project to practice with,
with tangible goals that I can associate with my work. This is an
example of one such project.

This post is an attempt at using R to develop a process for using
Librarian/Faculty interaction data in a meaningful way. This is part of
a larger project that I’m working on that seeks to build on the
intersection between Libraries, data, and customer relationship
management principles. If we think of library interactions from a
perspective informed by CRM, we can more easily think of librarian’s
work as part of larger networks of scholarship, communication, and
learning. It also implicitly argues that librarians need to think more
about nurturing relationships with faculty, as well as building new ones
with faculty that have been ignored, and rekindling new ones with
faculty who held relationships with librarians that are no longer
around. Network theory lends itself nicely to this approach. So, let’s
dive in.

Plan
----

Today we’ll visualize a sample set of library interaction data using the
visNetwork package. At my library, we use LibInsight Lite to track
various interaction types, including instruction, research help, digital
scholarship support, and so on. The data that we’ll use here has been
randomly generated.

First, we need to define *nodes* and *edges*. Nodes are our nouns
(people). Edges are our verbs (interactions).

We’ll begin by first loading one of two important packages, and then
we’ll load our interaction data, like so:

``` r
library(tidyverse)
```

    ## ── Attaching packages ───────────────────────────────────────────────────────────────────────────────── tidyverse 1.2.1 ──

    ## ✔ ggplot2 3.1.0       ✔ purrr   0.3.2  
    ## ✔ tibble  2.1.1       ✔ dplyr   0.8.0.1
    ## ✔ tidyr   0.8.3       ✔ stringr 1.4.0  
    ## ✔ readr   1.3.1       ✔ forcats 0.4.0

    ## ── Conflicts ──────────────────────────────────────────────────────────────────────────────────── tidyverse_conflicts() ──
    ## ✖ dplyr::filter() masks stats::filter()
    ## ✖ dplyr::lag()    masks stats::lag()

``` r
data <- read_csv("refined-data.csv")
```

    ## Parsed with column specification:
    ## cols(
    ##   id = col_double(),
    ##   Date = col_character(),
    ##   `IP Address` = col_character(),
    ##   `Internal Notes` = col_logical(),
    ##   Instructors = col_character(),
    ##   `Course Number` = col_character(),
    ##   Title = col_character(),
    ##   Faculty = col_character()
    ## )

``` r
data
```

    ## # A tibble: 199 x 8
    ##       id Date  `IP Address` `Internal Notes` Instructors `Course Number`
    ##    <dbl> <chr> <chr>        <lgl>            <chr>       <chr>          
    ##  1   160 8/22… 131.247.152… NA               GenevieYur… POLS 3260      
    ##  2   853 6/13… 131.247.152… NA               AngelTavar… Drop In        
    ##  3   453 2/1/… 131.247.152… NA               LibbieAlda… Drop In        
    ##  4    98 11/2… 131.247.152… NA               RainaReid   <NA>           
    ##  5    72 8/9/… 131.247.153… NA               LawandaPlu… Telephone      
    ##  6   105 1/2/… 131.247.152… NA               RegenaEhrl… <NA>           
    ##  7   184 3/14… 131.247.152… NA               AlisaGreat… <NA>           
    ##  8   219 2/8/… 131.247.152… NA               YevetteCoc… WRTG 3380      
    ##  9   220 2/8/… 131.247.152… NA               GenevieYur… WRTG 2100      
    ## 10   126 1/31… 131.247.152… NA               AngelTavar… WRTG 2100      
    ## # … with 189 more rows, and 2 more variables: Title <chr>, Faculty <chr>

We’ve successfuly loaded our data into our dataframe. Let’s check to see
the object and class types.

``` r
typeof(data)
```

    ## [1] "list"

``` r
class(data)
```

    ## [1] "spec_tbl_df" "tbl_df"      "tbl"         "data.frame"

Next we’ll create the node list from the data table. The *node list* is
a list of unique IDs representing a particular noun. So, for example,
each name - say, Cal Murgu - has a unique ID used to identify it
numerically - 01. We’ll create a list of nodes for names in
“Instructors” and “Faculty.” Another example could me “To” and “From” in
a network of letters. Basically you want to think about the two nodes or
vertices that are interacting with each other through links or edges
(that’s next).

``` r
instructors <- data %>%
  distinct(Instructors) %>%
  rename(label = Instructors)
  
instructors <- mutate(instructors, groups = "Librarians")

instructors
```

    ## # A tibble: 9 x 1
    ##   label          
    ##   <chr>          
    ## 1 GenevieYurick  
    ## 2 AngelTavares   
    ## 3 LibbieAldana   
    ## 4 RainaReid      
    ## 5 LawandaPlunkett
    ## 6 RegenaEhrlich  
    ## 7 AlisaGreathouse
    ## 8 YevetteCockrill
    ## 9 JamesKulick

We pipe (%\>%, which basically means using the output of one function as
an input for another) the data table that we just loaded, specify the
“Instructors” column, and create a new table with those values with
“label” as a column header. We also add a column called "groups" and populate it with the value "Librarians". And again for Faculty.

``` r
faculty <- data %>%
  distinct(Faculty) %>%
  rename(label = Faculty)
  
faculty <- mutate(faculty, groups = "Faculty")
```

Now that we have two dataframes, one for instructors and one for
faculty, we need to join them using the join command.

``` r
nodes <- full_join(instructors, faculty)
nodes
```

Now we have one table with one column which includes the names of every
individual in this network. However, we need to add a column with unique
IDs to this dataframe. To do so we’ll use the *rowid\_to\_column*
function.

``` r
nodes <- nodes %>%
  rowid_to_column("id")

nodes
```

    ## # A tibble: 154 x 2
    ##       id label          
    ##    <int> <chr>          
    ##  1     1 GenevieYurick  
    ##  2     2 AngelTavares   
    ##  3     3 LibbieAldana   
    ##  4     4 RainaReid      
    ##  5     5 LawandaPlunkett
    ##  6     6 RegenaEhrlich  
    ##  7     7 AlisaGreathouse
    ##  8     8 YevetteCockrill
    ##  9     9 JamesKulick    
    ## 10    10 AleciaGatlin   
    ## # … with 144 more rows

Great! 

``` r
nodes <- mutate(nodes, title = label)

nodes
```

    ## # A tibble: 200 x 4
    ##       id label           group title          
    ##    <dbl> <chr>           <chr> <chr>          
    ##  1    95 AleciaGatlin    F-HUM AleciaGatlin   
    ##  2   159 AnnabelleLord   F-HUM AnnabelleLord  
    ##  3   118 AshlieRepp      F-HUM AshlieRepp     
    ##  4   200 BernitaHambrick F-HUM BernitaHambrick
    ##  5   152 BonnieHunsicker F-HUM BonnieHunsicker
    ##  6    23 BrookeCloninger F-HUM BrookeCloninger
    ##  7    92 CaitlinMagers   F-HUM CaitlinMagers  
    ##  8    89 CandiLamothe    F-HUM CandiLamothe   
    ##  9    85 CarltonMaass    F-HUM CarltonMaass   
    ## 10    93 ChanaLefebvre   F-HUM ChanaLefebvre  
    ## # … with 190 more rows

Notice that I added an additional column using the *mutate*
function, with column name “title” and with values that are equal to the
value of the “label” column. You’ll see why that’s important later. 

Now, let’s create the edges table (or links). A very similar process.

``` r

per_act <- data %>%
  group_by(Instructors, Faculty) %>%
  summarise(weight = n()) %>%
  ungroup()

per_act

```

    ## # A tibble: 170 x 3
    ##    Instructors     Faculty           weight
    ##    <chr>           <chr>              <int>
    ##  1 AlisaGreathouse AlvinBodden            1
    ##  2 AlisaGreathouse AmyTicknor             1
    ##  3 AlisaGreathouse BerenicePeaslee        1
    ##  4 AlisaGreathouse BrynnAdrian            1
    ##  5 AlisaGreathouse CaitlinMagers          1
    ##  6 AlisaGreathouse CharoletteEldreth      1
    ##  7 AlisaGreathouse ChristianDant          1
    ##  8 AlisaGreathouse CorettaEhrmann         1
    ##  9 AlisaGreathouse CorinneCurd            2
    ## 10 AlisaGreathouse CraigPonte             2
    ## # … with 160 more rows

First we pipe the *data* table and group two columns, Instructors and
Faculty, using the *group\_by* function. Group\_by doesn’t give us any
quantitative value about what was grouped. The *summarise* function
gives us the weight of the relationship between Instructors and Faculty.
In other words, the summarise function tells us, in this case, how many
times an instructor did *something* with a faculty member.

Here’s another example that helped me understand these two functions, if
you’re still wondering what the hecko.

Let’s say you have a dataframe (df) which has US states (states) and
cities (cities) and population (population) in each city in three
columns.

Running:

``` r
df %>% 
 group_by(state) %>% 
 summarise (pop = sum(population) %\>%
 ungroup()
```

will give you the population rolled up by
state. For more, check this [link](https://www.quora.com/What-does-the-group_by-function-in-R-do).

The problem is that instead of numerical IDs, we have labels denoting
who is an instructor and who is a faculty member. Let’s change labels to
IDs using a *join*.

``` r
edges <- per_act %>% 
  left_join(nodes, by = c("Instructors" = "label")) %>% 
  rename(from = id)

edges <- edges %>% 
  left_join(nodes, by = c("Faculty" = "label")) %>% 
  rename(to = id)
```

What we’re asking here is for R to link (join) the “Instructors” and
“Faculty” label with the label’s unique ID in nodes.

``` r
edges <- select(edges, from, to, weight)
```

For a reason that will become evident in a second, we need to *mutate*
the edges table and add an additional column to describe the type of
activity. For the sake of convenience, I’ve listed all values under
“title” as “instruction,” but in reality these can include research
consultations, committees, venting, etc.

``` r
edges <- mutate(edges, title = "Instruction")

edges
```

    ## # A tibble: 170 x 4
    ##     from    to weight title      
    ##    <dbl> <dbl>  <int> <chr>      
    ##  1     7    45      1 Instruction
    ##  2     7   103      1 Instruction
    ##  3     7   187      1 Instruction
    ##  4     7   145      1 Instruction
    ##  5     7    92      1 Instruction
    ##  6     7    79      1 Instruction
    ##  7     7    54      1 Instruction
    ##  8     7   123      1 Instruction
    ##  9     7    72      2 Instruction
    ## 10     7   136      2 Instruction
    ## # … with 160 more rows

That’s it! So we have a dataframe with three integer columns and one
char column. We can now graph this network!

visNetwork
----------

A simple command for a simple graph.

``` r
library(visNetwork)

visNetwork(nodes, edges)
```


<!-- HTML CODE-->

{{< hp5 "https://calmurgu.com/lessons/net1.html" >}}

This is a great interactive visualization. Notice a few things. When you
hover over a node, a tooltip will show up rendering the value of the
“title” label that we added earlier in the nodes table. More
importantly, colors denote different groups (librarians in blue, etc).

What else can we do? Let’s add bunch of different stuff to make this viz
a little cooler.

``` r
network <- visNetwork(nodes, edges, width="600px", main = "Sample Network", submain = "2016 - 2019 Instruction Interactions", footer = "Fig. 1, minimal example") %>%
  visLegend() %>%
  visGroups(groupname = "Librarian", color = "darkblue", shape = "square") %>%
  visGroups(groupname = "F-HUM", color = "red", shape = "triangle") %>%
  visOptions(highlightNearest = TRUE, selectedBy = "group", nodesIdSelection = TRUE) %>%
  visEdges(arrows = "middle")

network
```

{{< hp5 "https://calmurgu.com/lessons/net2.html" >}}

<!--/html_preserve-->

That’s one nice network. Let’s save and export as an .html page to
share.

``` r
visSave(network, file = "network.html")
```

That’s it!
