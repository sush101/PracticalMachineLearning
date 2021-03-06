---
title: "Predict the manner of exercise"
author: "Rathod Sushma"
date: "Wednesday, June 18, 2014"
output: html_document
---
I) AIM :

The aim of the project is to "predict the manner in which people did exercise".

II) Data :

The training data of this project is available here <https://d396qusza40orc.cloudfront.net/predmachlearn/pml-training.csv>. 
The test data is available here <https://d396qusza40orc.cloudfront.net/predmachlearn/pml-testing.csv>.
The data source for this project comes from here <http://groupware.les.inf.puc-rio.br/har>.

The predictor variable is "classe" and there are 158 exploratory variables.
Using one or more predictor variables we got to build a model which predicts the manner in which they did exercise. 

III) Data Pre-Processing :

The following are the preprocessing steps followed for this analysis :

* 1. All the columns which contained "NA's" and missing values have been removed. 
* 2. The column namely "user_name" is removed as it is not relavent predictor for the current analysis. In the same way columns with "timestamp" and "new_window" were removed.
* 3. Finally a check for number of missing values was done which resulted in "Zero" missing values, which is a pretty good start for the analysis !


IV) Exploratory Analysis :

a) Descriptive Statistics :



b) Checking for missing data :


```r
sum(is.na(train))
```

```
## [1] 0
```

c) Exploratory Plots :

The following graph describes the distribution of No.of windows 


```r
plot(train$classe,train$num_window,main="Distribution of no of windows wrt Class",xlab="Classe",ylab="No.of Windows")
```

![plot of chunk unnamed-chunk-3](figure/unnamed-chunk-3.png) 

V) Statistical Prediction/Modelling :

a) Splitting the data :
The actual training data set was randomly splitted (by setting seeds) into three subsets in a ratio of 60, 20 and 20 percentages which were called as train,test and evaluation sets respectively. The model is built using train data set. For testing the accuracy of the model "test" data was used and a best model amongst was selected and finally was used on "evaluation" data. 


 
b) Building decision tree model:

Fitting a tree model using three different types of trees,.i.e by using "rpart", "C5.0","C4.5" on training data.



c) Testing the model :

Here we are going to see which is the more accurate model among the three different types of trees. 


```
## Loading required package: lattice
## Loading required package: ggplot2
```


```r
# Classification matrix for "Cart Model"
confusionMatrix(a1)
```

```
## Loading required package: class
```

```
## Confusion Matrix and Statistics
## 
##    
##       A   B   C   D   E
##   A 939  88  14  73   4
##   B  82 501  39  78  25
##   C   9 116 474  60  24
##   D  30  82  61 432  33
##   E  31 100  36  76 517
## 
## Overall Statistics
##                                         
##                Accuracy : 0.73          
##                  95% CI : (0.715, 0.743)
##     No Information Rate : 0.278         
##     P-Value [Acc > NIR] : <2e-16        
##                                         
##                   Kappa : 0.659         
##  Mcnemar's Test P-Value : <2e-16        
## 
## Statistics by Class:
## 
##                      Class: A Class: B Class: C Class: D Class: E
## Sensitivity             0.861    0.565    0.760    0.601    0.857
## Specificity             0.937    0.926    0.937    0.936    0.927
## Pos Pred Value          0.840    0.691    0.694    0.677    0.680
## Neg Pred Value          0.946    0.879    0.954    0.913    0.973
## Prevalence              0.278    0.226    0.159    0.183    0.154
## Detection Rate          0.239    0.128    0.121    0.110    0.132
## Detection Prevalence    0.285    0.185    0.174    0.163    0.194
## Balanced Accuracy       0.899    0.746    0.848    0.768    0.892
```

```r
# Classification matrix for "C5.0 model"
confusionMatrix(a2)
```

```
## Confusion Matrix and Statistics
## 
##    
##        A    B    C    D    E
##   A 1112    2    1    3    0
##   B    6  707   11    1    0
##   C    0    2  672    9    0
##   D    0    4    6  623    5
##   E    0    3    7    3  747
## 
## Overall Statistics
##                                        
##                Accuracy : 0.984        
##                  95% CI : (0.98, 0.988)
##     No Information Rate : 0.285        
##     P-Value [Acc > NIR] : <2e-16       
##                                        
##                   Kappa : 0.98         
##  Mcnemar's Test P-Value : NA           
## 
## Statistics by Class:
## 
##                      Class: A Class: B Class: C Class: D Class: E
## Sensitivity             0.995    0.985    0.964    0.975    0.993
## Specificity             0.998    0.994    0.997    0.995    0.996
## Pos Pred Value          0.995    0.975    0.984    0.976    0.983
## Neg Pred Value          0.998    0.997    0.992    0.995    0.998
## Prevalence              0.285    0.183    0.178    0.163    0.192
## Detection Rate          0.283    0.180    0.171    0.159    0.190
## Detection Prevalence    0.285    0.185    0.174    0.163    0.194
## Balanced Accuracy       0.996    0.990    0.980    0.985    0.995
```

```r
# Classification matrix for "C4.5 model"
confusionMatrix(a3)
```

```
## Confusion Matrix and Statistics
## 
##    
##        A    B    C    D    E
##   A 1103   11    1    2    1
##   B    5  706   11    2    1
##   C    1   11  660    6    5
##   D    0    2    7  628    1
##   E    0    4    1    6  749
## 
## Overall Statistics
##                                         
##                Accuracy : 0.98          
##                  95% CI : (0.975, 0.984)
##     No Information Rate : 0.283         
##     P-Value [Acc > NIR] : <2e-16        
##                                         
##                   Kappa : 0.975         
##  Mcnemar's Test P-Value : 0.204         
## 
## Statistics by Class:
## 
##                      Class: A Class: B Class: C Class: D Class: E
## Sensitivity             0.995    0.962    0.971    0.975    0.989
## Specificity             0.995    0.994    0.993    0.997    0.997
## Pos Pred Value          0.987    0.974    0.966    0.984    0.986
## Neg Pred Value          0.998    0.991    0.994    0.995    0.997
## Prevalence              0.283    0.187    0.173    0.164    0.193
## Detection Rate          0.281    0.180    0.168    0.160    0.191
## Detection Prevalence    0.285    0.185    0.174    0.163    0.194
## Balanced Accuracy       0.995    0.978    0.982    0.986    0.993
```

From the above information it is evident that "C5.0 model" gives the best results of accuracy,sensitivity,Pos Pred Value, neg Pred Value and specificity.

So, we can apply tree model, "C5.0" on the evaluation data set.


```r
# C5.0 :
a1<-table(evaluation$classe, predict(dtC50, newdata=evaluation, type="class"))
rceval_c50<-sum(diag(a1))/sum(a1)*100
confusionMatrix(a1)
```

```
## Confusion Matrix and Statistics
## 
##    
##        A    B    C    D    E
##   A 1115    2    0    4    1
##   B    9  754   12    1    0
##   C    0    5  661    5    0
##   D    0    5    5  607    6
##   E    0    2    8    4  718
## 
## Overall Statistics
##                                         
##                Accuracy : 0.982         
##                  95% CI : (0.978, 0.986)
##     No Information Rate : 0.286         
##     P-Value [Acc > NIR] : <2e-16        
##                                         
##                   Kappa : 0.978         
##  Mcnemar's Test P-Value : NA            
## 
## Statistics by Class:
## 
##                      Class: A Class: B Class: C Class: D Class: E
## Sensitivity             0.992    0.982    0.964    0.977    0.990
## Specificity             0.998    0.993    0.997    0.995    0.996
## Pos Pred Value          0.994    0.972    0.985    0.974    0.981
## Neg Pred Value          0.997    0.996    0.992    0.996    0.998
## Prevalence              0.286    0.196    0.175    0.158    0.185
## Detection Rate          0.284    0.192    0.168    0.155    0.183
## Detection Prevalence    0.286    0.198    0.171    0.159    0.187
## Balanced Accuracy       0.995    0.987    0.980    0.986    0.993
```

```r
cat("Sensitivity in evaluation data using c5.0:", rceval_c50,"%" )
```

```
## Sensitivity in evaluation data using c5.0: 98.24 %
```

As we have seen above that tree model "C5.0" gives good results on the evaluation data we can apply the model on 20 new observations, which would predict the type of exercise performed by the people. 

The same preprocessing steps are applied on these 20 new observations, let's say it as Realtest data.


```r
# Preprocessing on testing data :
Realtest <- read.csv("pml-testing.csv",header=T,sep=",",na.string=c("NA",""))
NAs <- apply(Realtest,2,function(x) {sum(is.na(x))})
Realtest <- Realtest[,which(NAs == 0)]
Realtest <- Realtest[,-c(1:6)]
sum(is.na(Realtest))
```

```
## [1] 0
```

```r
# testing our models on test data:
# C5.0 :
predict(dtC50, newdata=Realtest, type="class")
```

```
##  [1] B A B A A E D B A A B C B A E E A B B B
## Levels: A B C D E
```
 


