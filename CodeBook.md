Code Book for Course Project
========================================================

### Human Activity Recognition Data
#### Obtained from training and test cases using the Samsung Galaxy S2

-There are 30 subjects in the final dataset

Note: The final dataset is a merging of test and training subject files and only including the mean and standard deviation variable columns, shown here:

```r
testx = read.table("UCI HAR Dataset/test/X_test.txt")
testy = read.table("UCI HAR Dataset/test/y_test.txt")
trainx = read.table("UCI HAR Dataset/train/X_train.txt")
trainy = read.table("UCI HAR Dataset/train/y_train.txt")
test_sub = read.table("UCI HAR Dataset/test/subject_test.txt")
train_sub = read.table("UCI HAR Dataset/train/subject_train.txt")
features = read.table("UCI HAR Dataset/features.txt", stringsAsFactors = FALSE)
labels = read.table("UCI HAR Dataset/activity_labels.txt", stringsAsFactors = FALSE)
df = rbind(cbind(test_sub,testy,testx),cbind(train_sub,trainy,trainx))
colnames(df) = c("subject","activity",features[[2]])
data_points = df[,grep("(^activity$)|(^subject$)|(mean[(][)])|(std[(][)])",names(df))]
```

-Activities are split into six groups

    1. WALKING
    2. WALKING_UPSTAIRS
    3. WALKING_DOWNSTAIRS
    4. SITTING
    5. STANDING
    6. LAYING
    
-The variable data includes body acceleration, gravitational forces,  gyroscopic measures, and jerking movement (acceleration and velocity derived in time), and magnitude values measured by time and frequency.

-The final dataset publishes the mean and standard deviation for all of these variables in a 3-axis structure (x, y, z).

-A naming transformation was done to make the variable names more readable. The transformation is shown here:

```r
names(data_points) = gsub("[-()]","",names(data_points))
names(data_points) = sub("^f","Freq_",names(data_points))
names(data_points) = sub("^t","Time_",names(data_points))
names(data_points) = sub("mean","_Mean",names(data_points))
names(data_points) = sub("std","_StdDev",names(data_points))
names(data_points) = sub("BodyBody","Body",names(data_points))
```

-The full variable list is as follows:

    - Time_BodyAcc_MeanX 
    - Time_BodyAcc_MeanY 
    - Time_BodyAcc_MeanZ 
    - Time_BodyAcc_StdDevX 
    - Time_BodyAcc_StdDevY 
    - Time_BodyAcc_StdDevZ 
    - Time_GravityAcc_MeanX 
    - Time_GravityAcc_MeanY 
    - Time_GravityAcc_MeanZ 
    - Time_GravityAcc_StdDevX 
    - Time_GravityAcc_StdDevY 
    - Time_GravityAcc_StdDevZ 
    - Time_BodyAccJerk_MeanX 
    - Time_BodyAccJerk_MeanY 
    - Time_BodyAccJerk_MeanZ 
    - Time_BodyAccJerk_StdDevX 
    - Time_BodyAccJerk_StdDevY 
    - Time_BodyAccJerk_StdDevZ 
    - Time_BodyGyro_MeanX 
    - Time_BodyGyro_MeanY 
    - Time_BodyGyro_MeanZ 
    - Time_BodyGyro_StdDevX 
    - Time_BodyGyro_StdDevY 
    - Time_BodyGyro_StdDevZ 
    - Time_BodyGyroJerk_MeanX 
    - Time_BodyGyroJerk_MeanY 
    - Time_BodyGyroJerk_MeanZ 
    - Time_BodyGyroJerk_StdDevX 
    - Time_BodyGyroJerk_StdDevY 
    - Time_BodyGyroJerk_StdDevZ 
    - Time_BodyAccMag_Mean 
    - Time_BodyAccMag_StdDev 
    - Time_GravityAccMag_Mean 
    - Time_GravityAccMag_StdDev 
    - Time_BodyAccJerkMag_Mean 
    - Time_BodyAccJerkMag_StdDev 
    - Time_BodyGyroMag_Mean 
    - Time_BodyGyroMag_StdDev 
    - Time_BodyGyroJerkMag_Mean 
    - Time_BodyGyroJerkMag_StdDev 

The original datasets can be found here:
https://d396qusza40orc.cloudfront.net/getdata%2Fprojectfiles%2FUCI%20HAR%20Dataset.zip


