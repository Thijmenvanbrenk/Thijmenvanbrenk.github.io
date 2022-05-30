---
title: "Open peer review of data about the toxicology of pesticedes for bees"
author: "Thijmen van Brenk"
date: "2022-05-30"
output: bookdown::html_document2
---

## Checking reproducability for published papers.

in this assignment, this study [@stroblPositiveCorrelationPesticide2020] will be graded on the criteria for reproducibility.       
and this study [@brewerDiscrepantFindingsRelation2021] will be graded on code readability and reproducibility.
<br>
<br>


### Pesticide influence on consumption rate and survival for bees. 

* introduction of the paper          

the use of pesticides is one of the main reasons of loss of biodiversity, and the combination of multiple pesticides could even make this worse. in this experiment it is investigated what the sublethal (food consumption) and the lethal (survival) effects of pesticides are on adult female solitary bees, *Osmia bicornis*.       
<br>
to perform these tests, female solitary bees were divided into 4 groups:   

-- pesticide free (control)     
-- herbicide      
-- pesticide      
-- combined (both herbicide and pesticide)      
their consumption rate and longevity were measured and the data from these two variables are used for analysis.
<br>
<br>
there is no significant difference in survival and consumption between te different groups. there is however a significant positive correlation between the consumption rate and the longevity of these bees.


* transparancy criteria grading

| transparancy<br>criteria | grading                                        |
|--------------------------|------------------------------------------------|
| study purpose            | TRUE                                           |
| data<br>availability     | FALSE<br>only part of the data is<br>available |
| data <br>location        | at the beginning/<br>at the end                |
| study<br>location        | TRUE<br>materials/methods                      |
| author<br>review         | location and email<br>are present at the top   |
| ethics<br>statement      | FALSE                                          |
| funding<br>statement     | TRUE                                           |
| code<br>availability     | TRUE                                           |

The part of the data that is available can be accessed through this directory: "data/insects-957898-supplementary.xlsx"

### impact of analysis decisions for episodic memory and retrieval practices.

we will solely focus on the code of this paper to see:       
-- If the code can be understood easily.       
-- If I can reproduce one of the figures.        
-- If there are any bugs/flaws in the code.       

the code is available <span style="color:blue">[in this website](https://osf.io/dgcaz/)</span>        

the code has been copied to a new Rmd file in this repository under the name "_analysis_decisions_code.Rmd"        
the data has been downloaded and is available in this repository under the name "data/AllDataRR.csv"        
<br>        

* changes made:       

-- changed the directory in line 11 so it retrieved the data used from this study.        
-- installed the packages in line 19 and line 180.        
<br>        

* first impression:   

-- (+) every test is in different chunks which makes readability easier.       
-- (+) clear comments on what is happening.       
-- (+) easy to understand code        
-- (-) chunks dont have names.       
-- (-) the individual results are far away from each other.       
-- (-) the same tests are set of tests are performed multiple times, making a function would make chances of mistakes less likely
<br>        

* what this code is trying to achieve      

the first part of the code for this experiment is looking for the correlation between individual and different studies (line 24-174)       
the second part of the code for this experiment is looking at a correlation between the retrieval practice effect and the EM ability with the help of a graph. there are 2 graphs, one where everything is mean centered and one where it isnt.        
<br>        

* final judgement: (grading goes from 1-5(1 very hard/bad- 5 very easy/good))     

-- readability = 4        
-- reproducability = 5        
-- efficiency = 2       
