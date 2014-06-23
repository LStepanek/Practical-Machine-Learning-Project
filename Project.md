Machine Learning Project
========================================================

We used train and test data provided by Coursera Class and available here:

https://d396qusza40orc.cloudfront.net/predmachlearn/pml-training.csv

https://d396qusza40orc.cloudfront.net/predmachlearn/pml-testing.csv

### Processing
Firstly, working directory was set

```r
setwd("C:/Users/Lubomír Štìpánek/Documents/Data Science Specialization/Practical Machine Learning/Week 3")
```
And the data were loaded

```r
# load data
train.set <- read.csv("pml-training.csv",na.strings=c("NA",""))
```
Some processing due to missing values (NA) was needed

```r
NAs <- apply(train.set,2,function(x) {sum(is.na(x))}) 
clean.train.set <- train.set[,which(NAs == 0)]
```
Subset of clean.train.set is created

```r
library(caret)
```

```
## Loading required package: lattice
## Loading required package: ggplot2
```

```r
train.indicator <- createDataPartition(y = clean.train.set$classe, p=0.4,list=FALSE)
train <- clean.train.set[train.indicator,]
```
Some of the variables were discarted

```r
remove <- grep("timestamp|X|user_name|new_window",names(train))
train <- train[,-remove]
```

### Model of prediction
Let us grow some random forest

```r
modFit <- train(train$classe ~.,data = train,method="rf")
```

```
## 1 package is needed for this model and is not installed. (randomForest). Would you like to try to install it now?
```

```
## Error:
```

```r
modFit
```

```
## Error: object 'modFit' not found
```
Prediction on testing set


```r
test.set<-read.csv("pml-testing.csv",header=TRUE)
predict(modFit,newdata=test.set)
```

```
## Error: object 'modFit' not found
```

Output to submission

```r
pml_write_files = function(x){
  n = length(x)
  for(i in 1:n){
    filename = paste0("problem_id_",i,".txt")
    write.table(x[i],file=filename,quote=FALSE,row.names=FALSE,col.names=FALSE)
  }
}

pml_write_files(answers)
```

```
## Error: object 'answers' not found
```

