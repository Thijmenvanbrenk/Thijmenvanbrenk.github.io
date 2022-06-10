---
title: "developing in epidemiology"
author: "Thijmen"
output: bookdown::html_document2
---

## Creating an epidemiology map

With the infrastructure we have created to make it easier for people to connect, we have also made the infrastructure for diseases to spread. Many of these diseases cause allot of trouble and can weaken whole societies, just take a look at SARS-COV-19. To figure out how these diseases spread is essential to figure out how a pathogen behaves. Figuring this out gives us the possibility to take precautions so it does not happen again, as can be seen by this report from the [CDC.](https://www.cdc.gov/eis/downloads/epidemiology-factsheet.pdf)        
In my future i want to be able to process epidemiological data to figure out where a disease originated, how it spread to different people and make this data easily readable for non data scientists with the help of shiny.       
To learn these skills i have made a small plan for a few steps i want to go through:
1.    Find a suitable outbreak with available data.       
2.    Process the data to get simple phylogenetic trees.        
3.    Add regions to these trees.       
4.    Put these trees over a geographical map to see location.        
5.    Make these geopgraphicals maps interactive for easy visibility.       
<br>        

### Finding an outbreak

To be able and actually to create phylogenetic trees i need to have some data available to me.        
I dont want a massive amount of data like from the covid pandemic because this would be too much data to process while this is only for my own learning purpose.        
the NCBI has a very detailed database of different virus variation, for this exercise i will be using [MERS coronavirus complete cds nucleotides](https://www.ncbi.nlm.nih.gov/genome/viruses/variation/) with as selections human hosts and S genome regions.









```r
library(adegenet)
library(here)
library(tidyverse)

dna <- fasta2DNAbin(file = here("data/MERS_nucleotides.fa"))
dna

annot <- read.csv(here("data/MERS_annotation.csv"))

library(ape)
D <- dist.dna(dna, model = "TN93")
length(D)

temp <- as.data.frame(as.matrix(D))
table.paint(temp, cleg=0, clabel.row=.5, clabel.col=.5)


tre <- nj(D)
class(tre)

h_cluster <- hclust(D, method = "average", members = NULL) # method = average is used for UPGMA, members can be equal to NULL or a vector with a length of size D
plot(h_cluster, cex = 0.6, show.tip = F)

tre <- ladderize(tre)

plot(tre, cex = 0.6)

annot <- annot %>% separate(collection_date, into = c("collection_date"), sep = 4)
annot$collection_date <- as.numeric(annot$collection_date)

plot(tre, show.tip=FALSE, main = "Unrooted NJ tree") # gets rid of the labels on the end, refer to the first tree depicted above
title("Unrooted NJ tree")
myPal <- colorRampPalette(c("red","yellow","green","blue"))
tiplabels(annot$collection_date, bg=num2col(annot$collection_date, col.pal=myPal), cex=.5) #we use the annot dataset to get our years
temp <- pretty(2013:2019, 2)
legend("bottomleft", fill=num2col(temp, col.pal=myPal), leg=temp, ncol=2)

tre2 <- root(tre, out = 1)
tre2 <- ladderize(tre2)

x <- as.vector(D)
y <- as.vector(as.dist(cophenetic(tre2)))
plot(x, y, xlab="original pairwise distances", ylab="pairwise distances on the tree", main="Is NJ appropriate?", pch=20, col=transp("black",.1), cex=3)
abline(lm(y~x), col="red")



tre3 <- as.phylo(hclust(D,method="average"))
y <- as.vector(as.dist(cophenetic(tre3)))
plot(x, y, xlab="original pairwise distances", ylab="pairwise distances on the tree", main="Is UPGMA appropriate?", pch=20, col=transp("black",.1), cex=3)
abline(lm(y~x), col="red")

cor(x, y)^2





myBoots <- boot.phylo(tre2, dna, function(e) root(nj(dist.dna(e, model = "TN93")),1))

myBoots


plot(tre2, show.tip=FALSE, edge.width=2)
title("NJ tree + bootstrap values")
tiplabels(frame="none", pch=20, col=transp(num2col(annot$collection_date, col.pal=myPal),.7), cex=3, fg="transparent")

axisPhylo()
temp <- pretty(2013:2019, 5)
legend("topright", fill=transp(num2col(temp, col.pal=myPal),.7), leg=temp, ncol=2)
nodelabels(myBoots, cex=.6)
```

