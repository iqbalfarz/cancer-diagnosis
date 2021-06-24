# Personalized Medicine: Redefining Cancer Treatment
Cancer Diagnosis using Machine Learning

## How to Run?
<pre>
1. download dataset and jupyter notebook.
2. put dataset and jupyter notebook in the same folder.
3. Extract the dataset and run the jupyter notebook.
</pre>

## Business Problem
### Description
In this competition you will develop algorithms to classify genetic mutations based on clinical evidence (text).

There are nine different classes a genetic mutation can be classified on.

This is not a trivial task since interpreting clinical evidence is very challenging even for human specialists. Therefore, modeling the clinical evidence (text) will be critical for the success of your approach.

Both, training and test, data sets are provided via two different files. One (training/test_variants) provides the information about the genetic mutations, whereas the other (training/test_text) provides the clinical evidence (text) that our human experts used to classify the genetic mutations. Both are linked via the ID field.

Therefore the genetic mutation (row) with ID=15 in the file training_variants, was classified using the clinical evidence (text) from the row with ID=15 in the file training_text

Finally, to make it more exciting!! Some of the test data is machine-generated to prevent hand labeling. You will submit all the results of your classification algorithm, and we will ignore the machine-generated samples. 

__source:__[Click to see Official problem statement](https://www.kaggle.com/c/msk-redefining-cancer-treatment/)

__Context:__[click to read the context](https://www.kaggle.com/c/msk-redefining-cancer-treatment/discussion/35336#198462)

__Problem statement:__
Classify the given genetic variations/mutations based on evidence from text-based clinical literature.

### Source/Useful Links
Some articles and reference blogs about the problem statement.

* __Blog 1:__ [Click to read blog](https://www.forbes.com/sites/matthewherper/2017/06/03/a-new-cancer-drug-helped-almost-everyone-who-took-it-almost-heres-what-it-teaches-us/#2a44ee2f6b25)
* __YouTube video 1:__[Click to watch video](https://www.youtube.com/watch?v=UwbuW7oK8rk)
* __YouTube video 2:__[Click to watch video 2](https://www.youtube.com/watch?v=qxXRKVompI8)

### Real-world/Business objectives and constraints 
* No low-latency requirement
* Interpretability is important
* Errors can be very costly 
* Probability of a data-point belonging to each class is needed.

## Machine Learning Problem Formulation

### Data 
#### Data Overview
- Source: [click to download the dataset](https://www.kaggle.com/c/msk-redefining-cancer-treatment/data)
- We have two data files: one conatins the information about the genetic mutations and the other contains the clinical evidence (text) that human experts/pathologists use to classify the genetic mutations.
- Both these data files are have a common column called ID
- Data file's information:
    - training_variants(ID, Gene, Variations, class)
    - training_text(ID, Text)

__training_variants__:
ID,Gene,Variation,Class<br>
0,FAM58A,Truncating Mutations,1 <br>
1,CBL,W802*,2 <br>
2,CBL,Q249E,2 <br>
...
__training_text__:
<hr>
ID,Text <br>
0||Cyclin-dependent kinases (CDKs) regulate a variety of fundamental cellular processes. CDK10 stands out as one of the last orphan CDKs for which no activating cyclin has been identified and no kinase activity revealed. Previous work has shown that CDK10 silencing increases ETS2 (v-ets erythroblastosis virus E26 oncogene homolog 2)-driven activation of the MAPK pathway, which confers tamoxifen resistance to breast cancer cells. The precise mechanisms by which CDK10 modulates ETS2 activity, and more generally the functions of CDK10, remain elusive. Here we demonstrate that CDK10 is a cyclin-dependent kinase by identifying cyclin M as an activating cyclin. Cyclin M, an orphan cyclin, is the product of FAM58A, whose mutations cause STAR syndrome, a human developmental anomaly whose features include toe syndactyly, telecanthus, and anogenital and renal malformations. We show that STAR syndrome-associated cyclin M mutants are unable to interact with CDK10. Cyclin M silencing phenocopies CDK10 silencing in increasing c-Raf and in conferring tamoxifen resistance to breast cancer cells. CDK10/cyclin M phosphorylates ETS2 in vitro, and in cells it positively controls ETS2 degradation by the proteasome. ETS2 protein levels are increased in cells derived from a STAR patient, and this increase is attributable to decreased cyclin M levels. Altogether, our results reveal an additional regulatory mechanism for ETS2, which plays key roles in cancer and development. They also shed light on the molecular mechanisms underlying STAR syndrome.Cyclin-dependent kinases (CDKs) play a pivotal role in the control of a number of fundamental cellular processes (1). The human genome contains 21 genes encoding proteins that can be considered as members of the CDK family owing to their sequence similarity with bona fide CDKs, those known to be activated by cyclins (2). Although discovered almost 20 y ago (3, 4), CDK10 remains one of the two CDKs without an identified cyclin partner. This knowledge gap has largely impeded the exploration of its biological functions. CDK10 can act as a positive cell cycle regulator in some cells (5, 6) or as a tumor suppressor in others (7, 8). CDK10 interacts with the ETS2 (v-ets erythroblastosis virus E26 oncogene homolog 2) transcription factor and inhibits its transcriptional activity through an unknown mechanism (9). CDK10 knockdown derepresses ETS2, which increases the expression of the c-Raf protein kinase, activates the MAPK pathway, and induces resistance of MCF7 cells to tamoxifen (6). ... 

### Mapping the real-world problem to an ML problem

#### Type of Machine Learning Problem
<pre>
There are nine different classes a genetic mutation can be classified into=>Multi-class classification.
</pre>

#### Performance Metric
source: [click to see the performance metric on kaggle official](https://www.kaggle.com/c/msk-redefining-cancer-treatment#evaluation)
__Metric(s):__
- Multi-class Logloss
- confusion matrix

#### Machine Learning Objectives and Constraints
__Objective:__ Predict the probability of each data-point belonging to each of the nine classes.

__constraints:__
- Interpretability
- class probabilities are needed.
- Penalize the errors in class probabilities=> metric is log-loss.
- No Latency constraints.

### Train, CV, and Test Datasets
split the dataset randomly into three parts train, cross_validation, and test with 64%, 16%, 20% of data respectively.

## EDA(Exploratory Data Analysis)
Explore **Gene** and **Variation** Data.

__Top occured Gene__
![image](https://user-images.githubusercontent.com/32350208/123088149-02cfc400-d443-11eb-9426-d91067e6cbff.png)

__Top 20 most occured Variation__
![image](https://user-images.githubusercontent.com/32350208/123088243-209d2900-d443-11eb-8dc4-2535d0935fb0.png)

__Frequency of each class__
![image](https://user-images.githubusercontent.com/32350208/123088480-66f28800-d443-11eb-9d22-25ec176e84fa.png)

### WordClouds

- wordcloud of class 1:![image](https://user-images.githubusercontent.com/32350208/123088629-9acdad80-d443-11eb-9453-d41c78f04314.png)
- wordcloud of class 2: ![image](https://user-images.githubusercontent.com/32350208/123088670-a7520600-d443-11eb-8a20-111d67a54f1a.png)
- wordcloud of class 3: ![image](https://user-images.githubusercontent.com/32350208/123088719-b769e580-d443-11eb-95ba-cccadecdb547.png)
- wordcloud of class 4: ![image](https://user-images.githubusercontent.com/32350208/123088772-c6e92e80-d443-11eb-8776-b36785f6a359.png)
- wordcloud of class 5: ![image](https://user-images.githubusercontent.com/32350208/123088824-d8cad180-d443-11eb-8be2-613ec2ccd8d9.png)
- wordcloud of class 6: ![image](https://user-images.githubusercontent.com/32350208/123088887-e97b4780-d443-11eb-9433-86dc6c268bd7.png)
- wordcloud of class 7: ![image](https://user-images.githubusercontent.com/32350208/123088995-057ee900-d444-11eb-9887-a5caeb11cccb.png)
- wordcloud of class 8: ![image](https://user-images.githubusercontent.com/32350208/123089091-20e9f400-d444-11eb-9380-70a217e40a50.png)


## Feature Engineering
As we have done all the text preprocessing now lets go to introduce some feature so that this hidden features can be easily understandable for the model and can perform good.
source:
- Simple feature engineering: [click to see blog](https://www.kaggle.com/sudalairajkumar/simple-feature-engg-notebook-spooky-author)
- Brief insight on genetic variations: [click to read the blog](https://www.kaggle.com/dextrousjinx/brief-insight-on-genetic-variations)
- Extensive text data feature engineering: [Click to read the blog](https://www.kaggle.com/shivamb/extensive-text-data-feature-engineering)


- For each engineered feature we train model and analyse whether the feature is useful or not.
- ![image](https://user-images.githubusercontent.com/32350208/123090537-e2553900-d445-11eb-874a-e1b2b56d7811.png)

- ![image](https://user-images.githubusercontent.com/32350208/123090578-ef722800-d445-11eb-98ef-937cfd091f25.png)

### Featurize Categorical variable
There are two ways to featurize the categorical variable.
- **One-hot encoding**: [Click to know one-hot encoding](https://machinelearningmastery.com/why-one-hot-encode-data-in-machine-learning/)
- **Response coding**: [Click to know response coding](https://www.kaggle.com/questions-and-answers/61046)

### Featurize text into vector:
- **Bag of Word(BOW)**
- **TF-IDF: Term Frequency-Inverse Document Frequency**

## Machine Learning Modeling
I tried many ML Algorithms
- **Naive Bayes**
- __KNN__
- __Logistic Regression__
- __Linear SVM__
- __Random Forest__
- __Stacking of models__
- __Maximum Voting Classifier__

_**Logistic Regression worked well.**_

### ML Modeling Performance
![image](https://user-images.githubusercontent.com/32350208/123094842-fe0f0e00-d44a-11eb-936b-d14025668148.png)

## Procedure followed to solve this problem
1. We have loaded/readed the data into pandas dataframe 
2. Found that some special char, multiple space b/w words so used text preprocessing/data cleaning
3. Did EDA for better understanding of data and found that some insights out of it although It is medical data and for better understanding of data we need to have some good knowledge in molecular biology or to be more specific domain knowledge. 
4. Extracted some feature out of text data as well as from the others features(Gene, Variation) also and did some visualization to understand whether it has some value or not.
5. We have also checked for distribution of the class labels among train,test, and validation data.
6. After this, built a random model and generated 9 class probability randomely such that they sum to 1 to ensure that whatever model we built on top of this the loss will be always less and got log-loss ~2.5 from this random model.
7. Featurize categorical feature into numerical using onehotencoding and response coding and used both featurized vector to predict class label.
8. We also build other models with each and every individual engineered feature and check for whether they will be helpful or not in prediction and found that they are helpful.
9. On the text features we have used bow and tfidf and choose top 3k features and then stacked all the features on top of each other.
10. Now it's time to build model but before we built, first tuned the hyperparameter and then started with baseline model naive bays and obtained train loss ~ 0.9, test loss ~1.15 and validataion loss ~1.9.
11. And then again tuned hyperparameter for nearest neighbor and got slightly better or same accurcy than naive bays.
12. We tried naive bayes, nearest neighbor, logistic regression, linear SVM, random forest, stack 3 models(logistic regression, linear svm, naive bayes) and then used voting model and for each and every model did hyperparameter tuning, showed % of missclassified point, showed confusion matrix, precision, recall in a heatmap and the most important given interpretation(i.e. why the given gene and mutation comes under class 4 or whatever) for each model.



## Credit:
- [Applied AI Course:](https://www.appliedaicourse.com): For teaching in-depth Machine Learning, Deep Learning, and end-to-end problem solving.
 
