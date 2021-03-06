Description of Project Process
========================================================

### 1. Get data and compile multiple files into one data source
#### Here I set the working directory and read in the training and test files.

```r
setwd("D:\\Courses\\Getting_and_Cleaning_Data")
testx = read.table("UCI HAR Dataset/test/X_test.txt")
testy = read.table("UCI HAR Dataset/test/y_test.txt")

trainx = read.table("UCI HAR Dataset/train/X_train.txt")
trainy = read.table("UCI HAR Dataset/train/y_train.txt")

test_sub = read.table("UCI HAR Dataset/test/subject_test.txt")
train_sub = read.table("UCI HAR Dataset/train/subject_train.txt")

features = read.table("UCI HAR Dataset/features.txt", stringsAsFactors = FALSE)
labels = read.table("UCI HAR Dataset/activity_labels.txt", stringsAsFactors = FALSE)
```

#### Here I merge the data sets and update the column names.

```r
df = rbind(cbind(test_sub,testy,testx),cbind(train_sub,trainy,trainx))
colnames(df) = c("subject","activity",features[[2]])
```

### 2. Extract only the mean and standard deviation for all measurements in the dataset
#### Here I take only the identifying columns, along with all columns representing a mean or standard deviation.

```r
data_points = df[,grep("(^activity$)|(^subject$)|(mean[(][)])|(std[(][)])",names(df))]
```

### 3. Use descriptive activity names in dataset
#### Here I use the names from the activity labels dataset in the large dataset

```r
df$activity = labels[[2]][df$activity]
```

### 4. Use descriptive naming for variables
#### Here I edit the column names to be more clearly readable

```r
names(data_points) = gsub("[-()]","",names(data_points))
names(data_points) = sub("^f","Freq_",names(data_points))
names(data_points) = sub("^t","Time_",names(data_points))
names(data_points) = sub("mean","_Mean",names(data_points))
names(data_points) = sub("std","_StdDev",names(data_points))
names(data_points) = sub("BodyBody","Body",names(data_points))
```

### 5. Create a second, tidy dataset with the averages for all the variables by subject and activity
#### Here I create a new dataset with averages for all variable columns and reassign the activity names, printing the smaller, tidy set out into a txt file.

```r
library("plyr")
df2 = ddply(data_points,.(subject, activity),numcolwise(mean))
df2$activity = labels[[2]][df2$activity]
write.table(df2, file="Project2_Results.txt",row.names=FALSE)
```

#### Thus giving me the wanted result for the course project.
