---
title: "Introduction"
author: "Thijmen van Brenk"
date: "2022-06-12"
output: bookdown::html_document2
---

# Extra skills

In this section of my portfolio I will show you some of the extra skills I have developed during my data science minor.

## Writing an introduction using Zotero for references        

Writing research papers is a pretty important for the research field, so using references to other papers is crucial for writing a good introduction. Below here you can see an introduction to my project about liquid biopsies, it makes use of multiple references.

Neuroblastoma is the fourth most common tumor in children and presents itself as either a low-risk neuroblastoma or a high-risk neuroblastoma. Determining which risk neuroblastoma is present a tumor biopsy is necessary. [@weiserProgressLiquidBiopsies2019] however these biopsies are very invasive and can only be done a few times even tho the tumor keeps mutating. To counter this problem researchers have become more and more interested in liquid biopsies to be able to track the mutations in the tumor. This is possible because the tumor often excretes DNA into the blood stream which is then used for whole-exome sequencing (WES). these results can be compared with the DNA of the tumor to show how the tumor evolves over time [@chicardWholeExomeSequencingCellFree2018]. because the tumor cells have different properties depending on what part of the tumor they are on it is difficult to show all the mutations based on 1 tumor biopsy as that can have a bias for only that specific part of the tumor where the biopsy was taken from. Liquid biopsies also help with this problem as they sequence all the DNA that has been excreted by the tumor, this makes it possible to spot different mutations in both tumor DNA and cell free DNA (cf-DNA). [@vanpaemelFeasibilityUsingLiquid2022]        
The type of mutations that get the most attention are the copy number variations/aberrations (CNV/CNA) these CNV's can either be very small with just a few kilobases or very big where they cover the whole chromosome. The CNV's are very important as they can give an identification on how pathogenic the tumor is based on the genes it contains, the position of the CNV and the size of the CNV [@riggsTechnicalStandardsInterpretation2020].       
Some hospitals sadly don't have easy ways to analyse the data from all these patients because they do not have the experience with data analysis. This makes the process of analyzing the data a slow and tedious task. Even tho it would be extremely beneficial for the hospitals without data scientists to have the programs available to analyse these results quickly [@valsesiaGrowingImportanceCNVs2013], this takes away the time consuming task of having to analyze every file manually which gives them time to focus on more important things like treating the patient. Sharing these results to other hospitals is equally as important because there is not nearly enough data available to say with certainty how dangerous certain tumors are and if the tumors have been fully removed. With all the data combined the research towards liquid biopsies can evolve quickly making diagnoses easier and more reliable        
In this project we will analyse the tumor DNA and the cfDNA created by WES and will make it reproducible so that Princess maxima centre can easily analyse the data for all their patients.       
To accomplish this we will mostly focus on:       
-- Giving all the CNV's different ID's so they can be easily distinguished from each other.       
-- Showing which cytogenetic band the CNV falls in to.        
-- Making an interactive plot to look up genes easily.        
-- Automatically filtering genes that indicate high risk neuroblastoma's.       
-- Making a high throughput version so that it will analyse multiple datasets at the same time without having to manually insert all the data sets
-- Getting these results quickly and easily so the researcher does not have to focus on how to analyze the data.
