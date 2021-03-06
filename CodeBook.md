
# Description

The experiments have been carried out with a group of 30 volunteers within an age bracket of 19-48 years. Each person performed six activities (WALKING, WALKING_UPSTAIRS, WALKING_DOWNSTAIRS, SITTING, STANDING, LAYING) wearing a smartphone (Samsung Galaxy S II) on the waist. Using its embedded accelerometer and gyroscope, we captured 3-axial linear acceleration and 3-axial angular velocity at a constant rate of 50Hz. The experiments have been video-recorded to label the data manually. The obtained dataset has been randomly partitioned into two sets, where 70% of the volunteers was selected for generating the training data and 30% the test data. 

The sensor signals (accelerometer and gyroscope) were pre-processed by applying noise filters and then sampled in fixed-width sliding windows of 2.56 sec and 50% overlap (128 readings/window). The sensor acceleration signal, which has gravitational and body motion components, was separated using a Butterworth low-pass filter into body acceleration and gravity. The gravitational force is assumed to have only low frequency components, therefore a filter with 0.3 Hz cutoff frequency was used. From each window, a vector of features was obtained by calculating variables from the time and frequency domain. See 'features_info.txt' for more details. 

For each record it is provided:

- Triaxial acceleration from the accelerometer (total acceleration) and the estimated body acceleration.
- Triaxial Angular velocity from the gyroscope. 
- A 561-feature vector with time and frequency domain variables. 
- Its activity label. 
- An identifier of the subject who carried out the experiment.


# Dataset

The dataset includes the following files:

- 'features.txt': List of all 561 features.
- 'activity_labels.txt': List of activities (WALKING,WALKING_UPSTAIRS,WALKING_DOWNSTAIRS,SITTING, STANDING, LAYING)

   TEST DATASET
- 'test/X_test.txt': Test set. Observations for each of the features.
- 'test/y_test.txt': Test labels. Number identifying activity from activity_labels.txt
- 'test/subject_test.txt' : Subject who performed the activity. Its range is from 1 to 30. 

  TRAIN DATASET 
- 'train/X_train.txt': Training set. Observations for each of the features.
- 'train/y_train.txt': Training labels. Number identifying activity from activity_labels.txt
- 'train/subject_train.txt': Subject who performed the activity. Its range is from 1 to 30. 

# Analysis

1. Merges the training and the test sets to create one data set.
2. Extracts only the measurements on the mean and standard deviation for each measurement.
3. Uses descriptive activity names to name the activities in the data set
4. Appropriately labels the data set with descriptive variable names.
5. From the data set in step 4, creates a second, independent tidy data set with the average of each variable for each activity and each subject.

# Variables

- datasetTest -> Tidy Dataset with all Test files combined
- datasetTrain -> Tidy Dataset with all Train files combined
- datasetTotal -> Tidy Dataset with two datasets above merged
- SubsetMeanStd -> Tidy Dataset from datasetTotal with subject, activity, and only mean and standard deviation features
- SubsetMeanStdGrouped -> Tidy Dataset from SubsetMeanStd group by subject and activity. One record for each activity and each subject
- SubsetMeanStdGroupedAvg -> Tidy Dataset from SubsetMeanStd summarising all features by average

# Results

Run "run_analysis.R" script to perform the analysis. The results will be located in the next file: "SubsetMeanStdGroupedAvg.txt"

The "README.md" files describes how the script works and how the analysis has been done.
