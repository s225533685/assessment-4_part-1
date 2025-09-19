---
author: "Ameeta"
date: "2025-09-19"
output: pdf_document
---
This project analyzes the gexpression level of different genes 
---
title: "Assessment 4_Part 1"
author: "Ameeta"
date: "2025-09-17"
output: pdf_document
---

Download file for geneexpression.tsv
The link for raw file were copied from the github and then downloaded in R-markdown using te following download.file function and then the file was saved in geneexpression.tsv using destfile argument.
```{r}
# download the gene expression file
download.file("https://raw.githubusercontent.com/ghazkha/Assessment4/refs/heads/main/gene_expression.tsv", destfile =  "geneexpression.tsv")
```

Read in the file, making the gene identifiers the row names. Show a table of values for the first six genes.
The downloaded file was read using the read.table function. and then it was saved to gene_data. Following that, the first 6 rows containing 6 gene-identifier were displayed using the head function. 
```{r}
# Read the downloaded file
gene_data <- read.table("geneexpression.tsv",     # path to the file 
                        header=TRUE,       # indicates first row of the file contains column names 
                        sep = "\t",        # \t is the standard for tsv files 
                        row.names = 1,    #indicates that first colum contains row names
                        stringsAsFactors = FALSE )  # keep as plain character strings

# display the first 6 genes of the file
head(gene_data, 6) # 6 inidcates number of rows to be displayed 
```
Step 2: A new column was created by the name meanexpression for the mean of the other columns. Then the means were calculated using rowMeans functions and output was saved in $meanofcolumns in gene_data file.

```{r}
gene_data$meanexpression <- rowMeans(gene_data) # rowMeans calculate means across all columns for each row
head(gene_data, 6)
```
Step 3: List the 10 genes with the highest mean expression
Firstly, the meanexpression in gene_data were ordered in the descending order using order function and then it was saved in gene_data_sorted file. After that, first 10 rows containing 10 genes with highest meanexpression were displayed in gene_data_sorted using a drop argument to ensure the datas are obtained in table format and not in vector format. 

```{r}
#Step 5: Listing 10 genes with the higest mean expression
# order the "meanexpression" of the gene-data in descending order and save in gene_data-sorted file
gene_data_sorted <- gene_data[order(-gene_data$meanexpression), ] # order(-gene_data$meanofcolumns) sorts the meanexpression in descending order
# show 10 genes with the highest mea expression values 
gene_data_sorted[1:10, "meanexpression", drop = FALSE] # drop =FALSE ensures datas are expressed in data frame format and not vector 
```
Step 4. Determine the number of genes with a mean <10
The genes with meanexpression less than 10 was determined using a logical vector and then it was saved in gene_data_mean_10. Then the total number of genes with a meanexpression below 10 was calculated by summing the vectors.  
```{r}
# create logical vectors for genes with meanexpression <10
gene_data_mean_10 <- gene_data_sorted$meanexpression <10
# count the total number of genes with mean <10 
sum(gene_data_mean_10)
```
step 5: Make a histogram plot of the mean values and include it into your report.
A histogram was generated using hist function to represent the mean of expression level of each genes where x-axis represent the mean expression values and y-axis represent the number of genes within each mean expression range (bin). As shown in the graph, the majority of the genes have a very low mean expression as indicated by the tallest bin near zero. However, there are a few genes which has extremely higher mean expression (5e+05) but appeared to be empty due to the dominance by the tall bar for low gene expression. 
```{r}
# Step 6: Histogram of mean values of gene expression
data(gene_data)
hist(gene_data$meanexpression, # data to be plotted
     xlab="mean expression", # label for the x-axis 
     main="mean value of gene expression") # Main title of the histogram 
```

