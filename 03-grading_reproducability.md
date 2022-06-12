---
title: "Open peer review of data about the toxicology of pesticedes for bees"
author: "Thijmen van Brenk"
date: "2022-06-12"
output: bookdown::html_document2
---

## Checking reproducability for published papers.

In this assignment, this study [@stroblPositiveCorrelationPesticide2020] will be graded on the criteria for reproducibility.       
And this study [@brewerDiscrepantFindingsRelation2021] will be graded on code readability and reproducibility.
<br>
<br>


### Pesticide influence on consumption rate and survival for bees. 

* Introduction of the paper          

The use of pesticides is one of the main reasons of loss of biodiversity, and the combination of multiple pesticides could even make this worse. In this experiment it is investigated what the sublethal (food consumption) and the lethal (survival) effects of pesticides are on adult female solitary bees, *Osmia bicornis*.       
<br>
To perform these tests, female solitary bees were divided into 4 groups:   

-- pesticide free (control)     
-- Herbicide      
-- Pesticide      
-- Combined (both herbicide and pesticide)      
Their consumption rate and longevity were measured and the data from these two variables are used for analysis.
<br>
<br>
There is no significant difference in survival and consumption between te different groups. there is however a significant positive correlation between the consumption rate and the longevity of these bees.        
<br>        
Now we can grade this paper on the criteria for transparancy. you can find the results in the table below.


* Transparancy criteria grading

| Transparancy<br>criteria | Grading                                        |
|--------------------------|------------------------------------------------|
| Study purpose            | TRUE                                           |
| Data<br>availability     | FALSE<br>Only part of the data is<br>available |
| Data <br>location        | At the beginning/<br>at the end                |
| Study<br>location        | TRUE<br>materials/methods                      |
| Author<br>review         | Location and email<br>are present at the top   |
| Ethics<br>statement      | FALSE                                          |
| Funding<br>statement     | TRUE                                           |
| Code<br>availability     | TRUE                                           |

The part of the data that is available can be accessed through this directory: "data/insects-957898-supplementary.xlsx"

### impact of analysis decisions for episodic memory and retrieval practices.

We will solely focus on the code of this paper to see:       
-- If the code can be understood easily.       
-- If I can reproduce one of the figures.        
-- If there are any bugs/flaws in the code.       

The code is available <span style="color:blue">[in this website](https://osf.io/dgcaz/)</span>        

The code has been copied to a new Rmd file in this repository under the name "_analysis_decisions_code.Rmd".        
The data has been downloaded and is available in this repository under the name "data/AllDataRR.csv"        
<br>        

* Changes made:       

-- Changed the directory in line 11 so it retrieved the data used from this study.        
-- Installed the packages in line 19 and line 180 by deleting the "#" in front of those lines.        
<br>        

* First impression:   

-- (+) Every test is in different chunks which makes readability easier.       
-- (+) Clear comments on what is happening.       
-- (+) Easy to understand code        
-- (-) Chunks dont have names.       
-- (-) The individual results are far away from each other.       
-- (-) The same tests are are performed multiple times, making a function would make chances of mistakes less likely
<br>        

* What this code is trying to achieve      

The first part of the code for this experiment is looking for the correlation between individual and different studies (line 24-174)       
The second part of the code for this experiment is looking at a correlation between the retrieval practice effect and the EM ability with the help of a graph. there are 2 graphs, one where everything is mean centered and one where it isnt.        
<br>        

* Final judgement: (grading goes from 1-5(1 very hard/bad- 5 very easy/good))     

-- Readability = 4        
-- Reproducability = 5        
-- Efficiency = 2       
