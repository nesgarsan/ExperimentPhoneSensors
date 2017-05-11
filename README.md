# ExperimentPhoneSensors

#Set Working Directory
setwd("C:/Coursera/Data Science Specialization/Curso3-Getting and Cleaning Data/4.Week4/8.Course Project/UCI HAR Dataset")

# 1.Merges the training and the test sets to create one data set.

#reading files.

activityLabels<-read.table("activity_labels.txt")[ ,2]
features<-read.table("features.txt")[ ,2]
subjectTest<-read.table("./test/subject_test.txt",col.names=c("subject"))
yTest<-read.table("./test/y_test.txt",col.names=c("activityId"))
xTest<-read.table("./test/x_test.txt",col.names=features)

subjectTrain<-read.table("./train/subject_train.txt",col.names=c("subject"))
yTrain<-read.table("./train/y_train.txt",col.names=c("activityId"))
xTrain<-read.table("./train/x_train.txt",col.names=features)

#Join Test Data

datasetTest<-cbind(subjectTest,yTest,xTest)

#Join Train Data

datasetTrain<-cbind(subjectTrain,yTrain,xTrain)

#Merging test and train data to one data set

datasetTotal<-rbind(datasetTrain,datasetTest)


# 2.Extracts only the measurements on the mean and standard deviation for each measurement.

library(dplyr)

SubsetTotal<-select(datasetTotal, matches("(subject|activity|mean|std)"))


# 3.Uses descriptive activity names to name the activities in the data set

activityLabels<-read.table("activity_labels.txt",col.names=c("activityId","activity"))
SubsetMeanStd <- merge(x=SubsetTotal,y=activityLabels,all=TRUE)

#Exclude the activityId field

SubsetMeanStd <- select(SubsetMeanStd , -activityId)

# 4.Appropriately labels the data set with descriptive variable names.

#Get column names

columnNames <-colnames(SubsetMeanStd)

#Replace . with a space

columnNames <-gsub("\\.", " ", columnNames) 

#Delete all spaces in final

columnNames <- gsub("[[:space:]]+$","",columnNames)

#Replace several spaces by only one

columnNames <- gsub("[[:space:]]+"," ",columnNames)

columnNames <- gsub("mean", "Mean", columnNames)
columnNames <- gsub("std", "Std", columnNames)
columnNames <- gsub("^t", "Time ", columnNames)
columnNames <- gsub("^f", "Frequency ", columnNames)
columnNames <- gsub("BodyBody", "Body", columnNames)
columnNames<-gsub("tBody", "Time Body", columnNames)

#Modify column names in dataset

colnames(SubsetMeanStd) <- columnNames 

# 5.From the data set in step 4, creates a second, independent tidy data set with the average of each variable for each activity and each subject.

#Create a table (Dplyr)

SubsetMeanStdGrouped<- tbl_df(SubsetMeanStd)

#Group by subject and activity

SubsetMeanStdGrouped <-group_by(SubsetMeanStdGrouped, subject, activity)

#Calculate the mean for all features 

SubsetMeanStdGroupedAvg<- summarise_each(SubsetMeanStdGrouped, funs(mean))

#Write final file

write.table(SubsetMeanStdGroupedAvg,file="SubsetMeanStdGroupedAvg.txt",row.names=FALSE)
