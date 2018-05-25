# Getting-and-Cleaning-Data-Week-4-Assignment
setwd("C:/Users/claurej/Desktop/Coursera/UCI HAR Dataset")

## Read Data
subject_test <- read.table("C:/Users/claurej/Desktop/Coursera/UCI HAR Dataset/test/subject_test.txt")
X_test <- read.table("C:/Users/claurej/Desktop/Coursera/UCI HAR Dataset/test/X_test.txt")
y_test <- read.table("C:/Users/claurej/Desktop/Coursera/UCI HAR Dataset/test/y_test.txt")
subject_train <- read.table("C:/Users/claurej/Desktop/Coursera/UCI HAR Dataset/train/subject_train.txt")
X_train <- read.table("C:/Users/claurej/Desktop/Coursera/UCI HAR Dataset/train/X_train.txt")
y_train <- read.table("C:/Users/claurej/Desktop/Coursera/UCI HAR Dataset/train/y_train.txt")

activity_labels <- read.table("C:/Users/claurej/Desktop/Coursera/UCI HAR Dataset/activity_labels.txt")
features <- read.table("C:/Users/claurej/Desktop/Coursera/UCI HAR Dataset/features.txt")  

## Merge Training and Testing Sets
df <- rbind(X_train,X_test)

## Create subset of mean and standard deviation
Mean_StanDev <- grep("mean()|std()", features[, 2]) 
df <- df[,Mean_StanDev]

## Appropriately label the data set with descriptive variable names
cleanfeatures <- sapply(features[, 2], function(x) {gsub("[()]", "",x)})
names(df) <- cleanfeatures[Mean_StanDev]

## Combine test and train data sets and give labels
subject <- rbind(subject_train, subject_test)
names(subject) <- 'subject'
activity <- rbind(y_train, y_test)
names(activity) <- 'activity'

## Combine all data sets 
df <- cbind(subject,activity, df)

# Use descriptive activity names to name the activities in the data set
act_group <- factor(df$activity)
levels(act_group) <- activity_labels[,2]
df$activity <- act_group

## Create a second, independent tidy data set with the average of each variable for each activity and each subject
install.packages("reshape2")
library("reshape2")

Data <- melt(df,(id.vars=c("subject","activity")))
df2 <- dcast(Data, subject + activity ~ variable, mean)
names(df2)[-c(1:2)] <- paste("[mean of]" , names(df2)[-c(1:2)] )
write.table(df2, "tidy_data.txt", sep = ",")
