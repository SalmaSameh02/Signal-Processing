# Signal-Processing
Signal processing project repo
this is a project of signal processing that classifies respiratory sound files into normal and abnormal.
the project helps in making automatic diagnostic for the different types of the respiratory diseases as wheeze, crackle,...,etc.
# Dataset:
SPRSound: Open-Source SJTU Paediatric Respiratory Sound Database | IEEE Journals & Magazine | IEEE Xplore.
# Reading data
the dataset was a set of records, each record contain multiple of events. A record could contain normal and abnormal.
After importing the needed libraries and got the file of records and file of labels paths 
firstly we listed the directories in the label file directory and creating two dataframes one for records which would contain path of each record and label annotation the other was for events and would contain path, start, end , type, time 
starting to loop on list of directory files of json to read each file and extract the information to put it in the dataframes and set the poor quality records type as poor quality and its time = 0 
# Preprocessing
by dropping poor quality records and spliting the records into events and labeling each event using the json file included which contain start, end and label for poor quality json file is empty. after applying log stft and converting to spectogram and spliting it to train, validation, test datasets and processed datasets for each should be ready to be loaded to the model.
the model used is inception resnetV3 using pytorch to classify autogenerated spectogram.
the model can classify normal with percision 0.96 for train and test while abnormal percision is 0.57 for train and test.
AUC for train_val is 0.8654 and for test is 0.891.
the senstivity, specificity are 0.99, 0.32 respectively.
# Model
