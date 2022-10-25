# Predicting-Fake-Job-Postings
Introduction: 
The main objective of this assignment is to create a system that automatically flags suspicious job postings. 
We are using the training dataset of the Kaggle competition https://www.kaggle.com/datasets/shivamb/real-or-fake-fake-jobposting-prediction. 
We will be cleaning the data and using machine learning algorithms such as Logistic Regression, Linear SVC, Random Forest Classifier and 
Multilayer Perceptron Classifier to predict whether the job is fake or not. 

Explanation:
Imported necessary spark libraries and spark session. Imported csv file with spark.create dataframe.
Started by changing the label column fraudulent into int type.Filtered only 0 and 1 valued fradulent data and removed the rest.
Counted the null values using isnan and isNull to remove any attribute containing null values more than 1%. 
Combined all string data onto a single column "alldata" using concat_ws .Removed everything else but letters and also multiple spaces using regexp_replace. 
Converted all letters into lower case using lower() function.Undersampled the fraudulent column by diving the 0 fraudulent value by 17 to match the ratio of 1 fraudulent value. 
Splited the data into words and used stopwordsRemover function to remove the stop words.CountVectorizer was to used to convert the words into features.
Converted the int data columns using OnehotEncoder into vector columns.Merged the string vectors and int vectors using VectorAssembler into a features column.
Splitted the data in 70:30 ratio of train and test.Used LogisticRegression,LinearSvc,RandomForestClassifier and MultilayerPerceptronClassifier ml algorithms to create models for prediction.
After creating the model, I used MulticlassClassificationEvaluator to get the accuracy and f1 values of each model . 
Also used paramGridBuilder to get accuracy for different parameters and Crossvalidator for 10 fold validation on each model.
The best parameters were recieved using ".bestModel" function and printed each best parameter individually. 

ML models Results:

LogisticRegression:
before crossvalidation:
Prediction Accuracy:  0.8614800759013282
Prediction f1:  0.8614201003972137
after crossvalidation:
Prediction Accuracy:  0.9089184060721063
Prediction f1:  0.9088881769716683
with parameters:
the best maxIter is:  10
the best elasticNetParam is:  0.5
the best regParam is:  0.01

LinearSVC:
before crossvalidation:
Prediction Accuracy:  0.8747628083491461
Prediction f1:  0.8747943765059446
after crossvalidation:
Prediction Accuracy:  0.8785578747628083
Prediction f1:  0.8785884863087947
with parameters:
the best maxIter is:  50
the best threshold is:  0.0
the best regParam is:  0.005

RandomForestClassifier:
before crossvalidation:
Prediction Accuracy:  0.7419354838709677
Prediction f1:  0.7342268951708071
after crossvalidation:
Prediction Accuracy:  0.8538899430740038
Prediction f1:  0.8532729175712896
with parameters:
the best maxDepth is:  20
the best numTrees is:  30

MultilayerPerceptronClassifier:
before crossvalidation:
Prediction Accuracy:  0.8519924098671727
Prediction f1:  0.8520020024780092
after crossvalidation:
Prediction Accuracy:  0.8614800759013282
Prediction f1:  0.8614591277086479
with parameters:
the best maxIter is:  50
the best stepSize is:  0.01
the best blockSize is:  10

Conclusion:

Pre-processing of the csv file in spark data frame is done succesfully by handling missing values(removed columns with more than 1% missing values), undersampling the label(fraudulent) 
column, converting string to words , removing stopwords and converting the data into vectors.Accuracy and F1 values were evaluated along with 10 fold crossvalidation of different parameters.
The best algorithmn in this case was LogisticRegression  with features maxIter as 10,elasticNetParam as 0.5 and regParam as 0.01 with a accuracy of 0.9089184060721063 and f1 score of 0.9088881769716683. 
For our model, RandomForestClassifier performed very poorly before crossvalidation of different parameters. LinearSVC and MultilayerPerceptronClassifier performed slight worse than 
LogisticRegression with respect to accuracy and f1 score.Thus, Created a model to automatically detect whether the job application is fraudulent or not.


Submission Map:
zip files consist of files:-
1) Code folder - Consists of a ipynb file name Final_source_code.ipynb which is the source code to run.
2) Pseudo-code folder - Inside there is a Pseudo_code.txt file with the pseudo code for the spark program.
3) Results - Consists of images and outputs of various phases of program including pre-processing data,prediction accuracy and f1 values.

Instructions to run code:
1) install proper spark version.
2) open the code stored in code/Final_sorce_code.ipynb through a notebook(possibly jupyter notebook).
3) run the program.
