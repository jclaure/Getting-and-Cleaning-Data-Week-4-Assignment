Getting and Cleaning Data Week 4 Assignment

Course Project:
1. Merge the training and the test sets to create one data set.
2. Extract only the measurements on the mean and standard deviation for each measurement.
3. Use descriptive activity names to name the activities in the data set
4. Appropriately label the data set with descriptive activity names.
5. Create a second, independent tidy data set with the average of each variable for each activity and each subject.

Repo Contents:
1. run_analysis.R: the script needed to run the assignment.
2. CodeBook.md: the codebook that indicates all the variables and summaries calculated, along with units, and any other relevant information.

Steps to Complete Assignment:
1. Download the data set to a folder in your local drive, set as your working directory. 
2. Place run_analysis.R in your working directory. 
3. Run the script to get the resulting tidy_date.txt file. (In order to create the new txt file, this script requires the reshape2 package, if it is not installed in your system, it will automaticaly install.)
