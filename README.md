# Suicidal Ideation, Adolescence, and Influencing Factors

The rate of suicide has increased in the most recent decades. Between 2007 and 2018, the rate of suicide among ages 10 to 24 increased by almost 60%. Understanding the lives of those experiencing suicidal ideation may allow for targeted campaigns to support those individuals and reduce suicide rates. We propose that suicidal ideation is influenced by a number of factors throughout people’s lives, including age, health, and social support. To answer our relevant research questions and accommodate data limitations, we will build a total of four models. 

The details below document the various files and some notes on running the analysis. Please follow the instructions and code comments to effectively reproduce our analyses. 

**REQUIRED PACKAGES**
The following packages are required for conducting all data analyses and tabling processes. Please install these on your machine. The analyses will load the instance of the particular package:
`mice`, `geepack`, `lme4`, `lmerTest`, `dplyr`, `forccats`, `doBy`, `gt`, `ggplot2`, `tidyr`, `reshape2`, `gtsummary`, `tableone`

**FILE LIST**  
  **RAW DATA** 
  Data was collected in 4 waves of surveys, collected multiple years apart.  
   `21600-0001-Data.rda` - Wave 1 Data  
   `21600-0005-Data.rda` - Wave 2 Data  
   `21600-0008-Data.rda` - Wave 3 Data  
   `21600-0022-Data.rda` - Wave 4 Data  
   These datafiles are all used by the data cleaning process.  
   
  **CLEAN DATA**  
   `data_used_to_reproduce_analysis.csv`: The dataset we used for our original analyses with the original seed has been retained in the Data folder for perfect reproducibility purposes. For perfect reproduction and verification, load this dataset rather than conducting the data cleaning per the `Chunk 3 data Wrangling` chunk in `7430_project_code_full.Rmd`.  
     
  **SCRIPTS**  
   *DATA CLEANING/MODEL ANALYSES*:   
   `7430_project_code_full.R` 
   This file contains all pieces of code for cleaning and preprocessing a dataframe, then running subsequent modeling analyses. Please note that the mice package is used to      impute certain pieces of the data. As this process contains some randomness, the numbers may vary slightly in the final model results based on the chosen seed.  
Also note that if you would like to recreate the exact results of our model, see comments in `Chunk 3 data wrangling` to load the imputed dataframe. However, results by seed only vary slightly.
     
**INSTRUCTIONS**  
In the chunk labeled `set up` please change your working directory to that of the zip file named "Reproducibility", wherever it is stored on your machine. Then select in `Chunk 3 data wrangling` which dataset type you would like to analyze, either Section 1 or Section 2. Then each chunk can be run in order, following the other guidelines contained in this README.

*DATA CLEANING*  
We have two datasets to conduct the analysis with, both within the `Chunk 3 data wrangling` chunk of `7430_project_code_full.Rmd`. You can either generate your own dataset (`suicide <- data`), or read in the original cleaned dataset used for analysis (`read.csv()`). This is due to the randomness implemented by the mice() package. Results may vary slightly if generating your own analysis, but the small amount of missing data results in consistent conclusions. The code defaults to using the dataset generated by the data cleaning process.

There is some additional data manipulation throughout, particularly when models require a modification and testing (M3) or addition of a variable to run (M4). These are explained in each code chunk and summarized in the list below.  

*MODELING ANALYSES*  
The data generation process is followed by multiple modeling analyses. Each analysis is followed by a code chunk that generates a table of results.   
- Model 1 uses `glmer()` to test the effect of age.   
- Model 2 uses `geeglm()` to test the sex effect.
- Model 3 uses `glmer()` to test the effect of each category of weight. Please note that there is a pre-work chunk to verify that the effect of weight is significant before exploring the individual effects of each factor level.
- Model 4 uses `glmer()` to analyze the effect of the support score. Support score is calculated based on a variety of other variables.

*SENSITIVITY ANALYSES*  
Some sensitivity analyses were conducted, listed below:
- Model 2, the GEE model, was tested with different working correlations. A table is generated to verify results.

*Table 1*  
There is code to generate the Table 1 seen in our final report. Please note that this code only generates the numbers for verification. Formatting of Table 1 was conducted in Microsoft Word for readability. Please note that in order to generate Table 1 you need to run the `data cleaning from raw data` chunk. The population is stratified by all time suicidality, where 1 is any suicidal ideation instance and 0 is no instances.  

**ERROR NOTICE**  
Sometimes, RStudio drops pieces of our dataframe and a specific error message appears (`Error in contrasts<-`). This occurs if you try to run code out of order multiple times during analysis. If this occurs, please simply rerun the `Chunk 3 data wrangling` chunk to reload your selected dataset.

**NOTE ON SIGNIFICANCE**  
For some of our models, the generated p-values are too small for R to parse and appear as 0.000e+00 in the model summary tables. Other times R can extract the exact p-value.

