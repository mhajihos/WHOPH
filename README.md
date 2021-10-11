## WHOPH
## Overview
WHOPH packages is based on The Global Physical Activity Questionnaire which was developed by WHO for physical activity surveillance in countries. It collects information on physical activity participation in three settings (or domains) as well as sedentary behaviour, comprising 16 questions (P1-P16). The domains are:\
• Activity at work\
• Travel to and from places\
• Recreational activities\
WHOPH working only on R 32bit and has 5 dependecies listed in the DESCRIPTION file : survey, RODBC, knitr, dplyr, stringr.

## Installation
```
# install.packages("devtools")
devtools::install_github("mhajihos/WHOPH")
require(WHOPH)
```

## WHOPH_Data
```
WHOPH_Data(Dir,Data,id,weights,strata) # To prepare the dataset
```

    a. Dir is the directory with the STEPS data in ".mdb" ACCESS format. for example: "C:\\Users\\WHOData"\
    b. Data is the names of the dataset. for example: "ARM.STEPS.mdb"\
    c. id is an argument in "svydesign" package. for example: id="PSU"\
    d. weights is an argument in "svydesign" package. for example: weights="WStep1"\
    e. strata is an argument in "svydesign" package. for example: strata="Stratum"
    
An example for WHOPH_Data function is:\
     a. WHOPH_Data(Dir= "C:\\Users\\WHOData",Data= "ARM.STEPS.mdb",id= "PSU",weights= "WStep1",strata= "Stratum")

## As_svy_mean
```
As_svy_mean(Outcome,Group=NULL,Design,Median=FALSE)# For mean and median of any combination of factors
```

    a. Outcome is the outcome of interest. for example: Meet wich shows if the WHO recommendation for physical activity was met or not.\
    b. Group is the group of interest. The default is NULL for when only the outcome variable is in our interest. Group can be any combination of categorical variables.\
       Examples for group can be: ~age4y, ~age4y+sex, ~age4y+UrbanRural+sex, etc.\
    c. Design is the output object of WHOPH_Data function.\
    d. Median is a logical argument. Default is FALSE when we are interested in the weighted average [and 95%CI] value and TRUE for weighted median [and 25%le-75%le] values. 
    
Some examples for As_svy_mean function are:\
        a. As_svy_mean( ~Meet, ~age4y,Design= data) # data is the output of WHOPH_Data function\
        b. As_svy_mean( ~Meet, ~UrbanRural,Design= data) # data is the output of WHOPH_Data function\
        c. As_svy_mean( ~Meet, ~sex,Design= data) # data is the output of WHOPH_Data function\
        d. As_svy_mean( ~Meet, ~age4y+sex,Design= data) # data is the output of WHOPH_Data function\
        e. As_svy_mean( ~Meet, ~UrbanRural+sex,Design= data) # data is the output of WHOPH_Data function\
        f. As_svy_mean( ~Meet, ~age4y+UrbanRural+sex,Design= data) # data is the output of WHOPH_Data function\
        g. As_svy_mean( ~Meet,Design= data) # data is the output of WHOPH_Data function.

Some examples for median with As_svy_mean function are:\
        a. As_svy_mean( ~Ptotalday, ~age4y,Design= data,Median= TRUE)\
        b. As_svy_mean( ~Ptotalday ,~UrbanRural,Design= data,Median= TRUE)\
        c. As_svy_mean( ~Ptotalday, ~sex,Design= data,Median= TRUE)\
        d. As_svy_mean( ~Ptotalday, ~age4y+sex,Design= data,Median= TRUE)\
        e. As_svy_mean( ~Ptotalday ,~UrbanRural+sex,Design= data,Median= TRUE)\
        f. As_svy_mean( ~Ptotalday, ~age4y+UrbanRural+sex,Design= data,Median= TRUE)\
        g. As_svy_mean( ~Ptotalday,Design= data,Median= TRUE).
        

## PtotalCat_svy_mean
```
PtotalCat_svy_mean(Outcome,Group=NULL,Design) # For mean of Total physical activity categories for any combination of factors
```

    a. Outcome is the outcome of interest. PtotalCat is the outcome of interest with three levels "Low", "Moderate", and "High"\
    b. Group is the group of interest. The default is NULL for when only the outcome variable is in our interest. Group can be any combination of categorical variables.\
       Examples for group can be: ~age4y, ~age4y+sex, ~age4y+UrbanRural+sex, etc.\
    c. Design is the output object of WHOPH_Data function.
    
 Example for PtotalCat_svy_mean function are:\
        a. PtotalCat_svy_mean( ~PtotalCat, ~age4y,Design= data)\
        b. PtotalCat_svy_mean( ~PtotalCat, ~UrbanRural,Design= data)\
        c. PtotalCat_svy_mean( ~PtotalCat ,~sex,Design= data)\
        d. PtotalCat_svy_mean( ~PtotalCat, ~age4y+sex,Design= data)\
        e. PtotalCat_svy_mean( ~PtotalCat, ~UrbanRural+sex,Design= data)\
        f. PtotalCat_svy_mean( ~PtotalCat, ~age4y+UrbanRural+sex,Design= data)\
        g. PtotalCat_svy_mean( ~PtotalCat,Design= data).
