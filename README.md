# Signal-Processing
Signal processing project repo
this is a project of signal processing that classifies respiratory sound files into normal and abnormal.
the project helps in making automatic diagnostic for the different types of the respiratory diseases as (wheeze, crackle,...,etc.) for events and (CAS, DAS, CAS&DAS) for records.
# Dataset:
SPRSound: Open-Source SJTU Paediatric Respiratory Sound Database | IEEE Journals & Magazine | IEEE Xplore.

the records files are in (".wav") format. 
the labels were in json files, for poor quality json files are empty. 
# Reading data
the dataset was a set of records, each record contain multiple of events. A record could contain normal and abnormal.
After importing the needed libraries and got the file of records and file of labels paths 
firstly we listed the directories in the label file directory and creating two dataframes one for records which would contain path of each record and label annotation the other was for events and would contain path, start, end , type, time 
starting to loop on list of directory files of json to read each file and extract the information to put it in the dataframes and set the poor quality records type as poor quality and its time = 0 
# Preprocessing
we noticed that the data events' time varies some may be a second other can range from six to seven seconds so we plotted the boxplot of every disease to determain the outliers. we noticed that the outliers nearly starts from 3.7 seconds so we removed events above 3.7 seconds.
then we started label encoding for normal class in events and records would be "0" and all diseases would be encoded as "1" while poor quality encoded as "2" saving the new dataframe into a csv file.
the poor quality would have been a problem if we countinued to deal with it in our dataset as the events are empty even specialists couldn't classify those poor quality files so we dropped it.
we reseted the index of the dataframe and randomized it.
we decided on dealing with events instead of records as the data of events is much larger than that of records as each record have three events. 
### Data filteration
we applied a bandpass filter to pass a certain frequancy by making two functions the first is to make the bandpass filter with given lowcut, highcut and the other function apply the first function to our data.
### Records splitting
we started to spilt the records into events each record into three events as mentioned before according to the start and the end of each event that information is in the json files. we merged the step of the filteration with the splitting step so the event resulted is filtered. 
### Data balancing
we also determined the difference between class "0", class "1" and deleted it from class "0" as it exceeds the other class to balance the data in each class. then plotted it as a pie chart to make sure the data is balanced.
<img src="https://github.com/SalmaSameh02/Signal-Processing/blob/e7d0cc5f1a9d1971af96b8659d406cb1c05b8d11/chart%20for%20data%20after%20balancing.png">

by dropping poor quality records and spliting the records into events and labeling each event using the json file included which contain start, end and label for poor quality json file is empty. after applying stft and converting to spectogram and spliting it to train, validation, test datasets and processed datasets for each should be ready to be loaded to the model.
# Model
the model used is inception resnetV3 using pytorch to classify autogenerated spectogram.
the model can classify normal with percision 0.96 for train and test while abnormal percision is 0.57 for train and test.
AUC for train_val is 0.8654 and for test is 0.891.
the senstivity, specificity are 0.99, 0.32 respectively.

