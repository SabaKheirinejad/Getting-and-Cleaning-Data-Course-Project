Code book for Coursera Getting and Cleaning Data course project

The data set that this code book pertains to is located in the tidy.txt file of this repository.

See the README.md file of this repository for background information on this data set.

The structure of the data set is described in the Data section, its variables are listed in the Variables section, and the transformations that were carried out to obtain the data set based on the source data are presented in the Transformations section.

Data

The tidy.txt data file is a text file, containing space-separated values.

The first row contains the names of the variables, which are listed and described in the Variables section, and the following rows contain the values of these variables.

Variables

Each row contains, for a given subject and activity, 79 averaged signal measurements.

Identifiers

subject

Subject identifier, integer, ranges from 1 to 30.

activity

Activity identifier, string with 6 possible values:

WALKING: subject was walking WALKING_UPSTAIRS: subject was walking upstairs WALKING_DOWNSTAIRS: subject was walking downstairs SITTING: subject was sitting STANDING: subject was standing LAYING: subject was laying Average of measurements

All measurements are floating-point values, normalised and bounded within [-1,1].

Prior to normalisation, acceleration measurements (variables containing Accelerometer) were made in g's (9.81 m.s⁻²) and gyroscope measurements (variables containing Gyroscope) were made in radians per second (rad.s⁻¹).

Magnitudes of three-dimensional signals (variables containing Magnitude) were calculated using the Euclidean norm.

The measurements are classified in two domains:

Time-domain signals (variables prefixed by timeDomain), resulting from the capture of accelerometer and gyroscope raw signals.

Frequency-domain signals (variables prefixed by frequencyDomain), resulting from the application of a Fast Fourier Transform (FFT) to some of the time-domain signals.

Transformations

The zip file containing the source data is located at https://d396qusza40orc.cloudfront.net/getdata%2Fprojectfiles%2FUCI%20HAR%20Dataset.zip.

The following transformations were applied to the source data:

The training and test sets were merged to create one data set.

The measurements on the mean and standard deviation (i.e. signals containing the strings mean and std) were extracted for each measurement, and the others were discarded.

The activity identifiers (originally coded as integers between 1 and 6) were replaced with descriptive activity names (see Identifiers section).

The variable names were replaced with descriptive variable names (e.g. tBodyAcc-mean()-X was expanded to timeDomainBodyAccelerometerMeanX), using the following set of rules: Special characters (i.e. (, ), and -) were removed The initial f and t were expanded to frequencyDomain and timeDomain respectively. Acc, Gyro, Mag, Freq, mean, and std were replaced with Accelerometer, Gyroscope, Magnitude, Frequency, Mean, and StandardDeviation respectively. Replaced (supposedly incorrect as per source's features_info.txt file) BodyBody with Body.

From the data set in step 4, the final data set was created with the average of each variable for each activity and each subject.

The collection of the source data and the transformations listed above were implemented by the run_analysis.R R script (see README.md file for usage instructions).

The run_analysis.R script performs the data preparation and then followed by the 5 steps required as described in the course project’s definition.

1. Download the dataset
 Dataset downloaded and extracted under the folder called UCI HAR Dataset

2. Assign each data to variables
features <- features.txt : 561 rows, 2 columns

The features selected for this database come from the accelerometer and gyroscope 3-axial raw signals tAcc-XYZ and tGyro-XYZ.

activities <- activity_labels.txt : 6 rows, 2 columns

List of activities performed when the corresponding measurements were taken and its codes (labels)

subject_test <- test/subject_test.txt : 2947 rows, 1 column

contains test data of 9/30 volunteer test subjects being observed

x_test <- test/X_test.txt : 2947 rows, 561 columns
contains recorded features test data

y_test <- test/y_test.txt : 2947 rows, 1 columns
contains test data of activities’code labels

subject_train <- test/subject_train.txt : 7352 rows, 1 column
contains train data of 21/30 volunteer subjects being observed

x_train <- test/X_train.txt : 7352 rows, 561 columns
contains recorded features train data

y_train <- test/y_train.txt : 7352 rows, 1 columns
contains train data of activities’code labels

3. Merges the training and the test sets to create one data set
4. 
X (10299 rows, 561 columns) is created by merging x_train and x_test using rbind() function

Y (10299 rows, 1 column) is created by merging y_train and y_test using rbind() function

Subject (10299 rows, 1 column) is created by merging subject_train and subject_test using rbind() function

Merged_Data (10299 rows, 563 column) is created by merging Subject, Y and X using cbind() function

4. Extracts only the measurements on the mean and standard deviation for each measurement
TidyData (10299 rows, 88 columns) is created by subsetting Merged_Data, selecting only columns: subject, code and the measurements on the mean and standard deviation (std) for each measurement

5. Uses descriptive activity names to name the activities in the data set
Entire numbers in code column of the TidyData replaced with corresponding activity taken from second column of the activities variable

6. Appropriately labels the data set with descriptive variable names
code column in TidyData renamed into activities

All Acc in column’s name replaced by Accelerometer

All Gyro in column’s name replaced by Gyroscope

All BodyBody in column’s name replaced by Body

All Mag in column’s name replaced by Magnitude

All start with character f in column’s name replaced by Frequency

All start with character t in column’s name replaced by Time

7. From the data set in step 4, creates a second, independent tidy data set with the average of each variable for each activity and each subject
FinalData (180 rows, 88 columns) is created by sumarizing TidyData taking the means of each variable for each activity and each subject, after groupped by subject and activity.

Export FinalData into tidy.txt file.
