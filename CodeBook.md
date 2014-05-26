CodeBook from Getting and Cleaning Data
==========================
Run_analysis.R Opens the data and creates 2 tidy datas according to instructions.

The R script File is completely commented so you can read the file or the CodeBook

1. First Step: Merges the training and the test sets to create one data set.
According to README.txt in UCI HAR Dataset we have:
 - 'train/X_train.txt': Training set.
 - 'test/X_test.txt':   Test set.
 - So we have to merge mXtest and mXtrain from Script file

2. Second Step: Extracts only the measurements on the mean and standard deviation for each measurement. 
	logiMean<-grepl("mean()",mfeatures[,2],fixed=TRUE) will have an boolean array if the entry has mean() on it.
	
	The result is a 10299 x 68 data frame according to step 1.
	All entries are values normalized according to the owners of the data.

3. Uses descriptive activity names to name the activities in the data set:
   Reading the .txt of ativity labels will tell us which names they use.
 - walking
 - walkingupstairs
 - walkingdownstairs
 - sitting
 - standing
 - laying
 We need to map 1,2,3,4,5,6 values into walking, walkinggupstaris,...,laying
	
4. Appropriately labels the data set with descriptive activity names. 
 - All atributes converted to lower case and eliminating () according to sintax problems of R.
 - Then we merge the Subject table (poeple that made the experiment) with activitie table and values table.
   cleaned <- cbind(mSubject, mYmerged, mXmerged)
 - Writing the table
   write.table(cleaned, "tidy_data_1.txt")
 - Subject IDs are integers between 1 and 30 inclusive.
Names of the attributes are similar to the following:
 - tbodyacc-mean-x 
 - tbodyacc-mean-y 
 - tbodyacc-mean-z 
 - tbodyacc-std-x 
 - tbodyacc-std-y 
 - tbodyacc-std-z 
 - tgravityacc-mean-x 
 - tgravityacc-mean-y
	
5. Finally, the script creates a 2nd, independent tidy data set with the average
 of each measurement for each activity and each subject of all atributes.
 - I asume that I need ALL the atributes. Thats why I don't use merged data but all data in mAll.
 - When I select all the atributes I merge as step 3 but all values.
 - Then I need 180 rows because we have 6 activities and 30 users.
 - The result is saved as tidy_averages.txt, a 180x70 data frame, where as before,
  - the first column contains subject IDs, the second column contains activity names (see below),
and then the averages for each of the 66 attributes are in columns 3...70.
