---
layout: post
title: Give Me Some Credit
---
I did classification.

``
test<-read.csv("cs-test.csv", header=TRUE,sep=",")
train<-read.csv("cs-training.csv",header=TRUE,sep=",")
train$SeriousDlqin2yrs<-factor(train$SeriousDlqin2yrs)
Id<-test[1]
train<-train[-1]
test<-test[-(1:2)]

model1<-C5.0(train[-1],train$SeriousDlqin2yrs)
model2<-C5.0(train[-1],train$SeriousDlqin2yrs, trials = 10)
model1pred<-predict(model1,train)
model2pred<-predict(model2,test)

CrossTable(train$SeriousDlqin2yrs, model1pred,prop.chisq = FALSE, prop.c = FALSE, prop.r = FALSE, dnn = c('actual default', 'predicted default'))
CrossTable(train$SeriousDlqin2yrs, model2pred,prop.chisq = FALSE, prop.c = FALSE, prop.r = FALSE, dnn = c('actual default', 'predicted default'))
submit<-data.frame(Id=Id$X, Probability=model2pred)
write.csv(submit, file = "kaggleentry1.csv", row.names = FALSE)
plot(model2)
``

[My R Code](https://github.com/mbking92/kaggle/blob/master/firstkagglecredit.R) 
