gbm
===
require(gbm)
station <- read.csv("/Users/hanyucen/Downloads/Station_116.csv", header=F, stringsAsFactors=F)
View(station)
attach(station)
names(station)<-c("ID","a.bikes","a.dock","time")
station$ratio<-a.dock/(a.bikes+a.dock)
model<-gbm(formula=ratio~a.bikes+a.dock,data=station, distribution='gaussian',n.trees=2000,interaction.depth=5,shrinkage=0.01,cv.folds=0,keep.data=F)
best_ntree<-gbm.perf(model,method="OOB")
best_ntree
predict(model,as.data.frame(station),n.trees=best_ntree,type='response')
