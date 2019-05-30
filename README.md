R program coding descriptoon for Genes document. When pressed "Raw" both the command and description will be displayed together.

#download.file command allows us to download .tsv documents and destfile="gene.tsv" at the end ensures the retrieved data is stored under "gene_tsv" 
download.file("https://raw.githubusercontent.com/markziemann/SLE712_files/master/week10_files/gene_expression.tsv",destfile="gene.tsv")

#To save table under 'm' and read table making the gene accession number the row names; else R automatically assigns row names and hence does not allow us to run any mathematical calculations
m<-read.table("gene.tsv", header=T,row.names=1)

#To show the data stored under 'm'
m

#To make a new column titled Means and add mean values of the other columns in it. 'as.matrix' command ensures the data is read as matrix (only numerical values). However, in this case we know all the means are numerical, hence this command can be omitted. m$Means is the command to make a new column within 'm'. cbind is an alternative command that has similar function.
m$Means<-rowMeans(as.matrix(m))

#To show the data stored under 'm'. This will now show the new column that has been added to 'm'
m

#To arrange the table in descending order based on Means value and save it under 'd'
d<-m[order(-m$Means),]

#'head' command allows selection of first 10 values for data stored under 'd'. If only head (d) was written, it would show the first five results.
head(d,10)

#Select column 3 (i.e. Means) and show genes with average<10. 
(m[which(m[,3]<10),])

#To count the number of rows which have average<10. nrow or dim could be used to count the number of rows
nrow(m[which(m[,3]<10),])

#To draw a pair plot diagram for all the data saved under 'm'
pairs(m)
