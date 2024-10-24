# DataScienceChallenge
A small data science challenge oriented to predict if a new employee with quit or not within three months of the hiring process.

## Objective

In this project, there are three main .csv files:  **ocean_challenge.csv**, **empresa_challenge.csv** and **dropout_90_dias_challenge.csv**. This files have specific behavior, which are explained as follows:

### ocean_challenge.csv

```
- `email_identifier` is the column that contains the used ID instead of the personal email of the person.
- `Meta` column contains the recruiting platform feedback. It includes a list of a personality test questions, the unique answer options (5 different options) and a selection boolean (only one is chosen). It also has a score key with the scoring results per selection.
- `Meta` structure:
1). `score`: Object with the personality test scores obtained.
1.1). Every object key is one of the following "measured skills": __Extroversion__, __Agreeableness__, __Conscentiousness__, __EmotionaStability__ and __OpennessToExperience__.
1.2). `total`: Score obtained (max. 50).
1.3). `percentage`: Scored obtained measured in percentage.
2. It's in `json` format.
```

### empresa_challenge.csv

```
- `email_identifier` behaves similar to the previous csv.
- Every row represents a month for a person (counted to the last day of their cycle).
- The cycle last day chosen is 2023-12-09.
```

### dropout_90_dias_challenge.csv

```
- `performace_group` is the target variable. '1' means that the person left the company before 90 days and '0' means otherwise.
```

## Technologies and approach

### Technologies

This challenge is solved using a Python Notebook, was first developed in Jupyter Notebooks and later tested and finished in Google Colab. Additionally, the following frameworks were used:
```
a). `pandas`
b). `numpy`
c). `json`
d). `sklearn`
```

### Approach

This project is divided in three sections. Each one is oriented to address an specific stage of the data working process.

**1. Data processing stage**

In this section, a part of the ELT process is developed. All three of the csv files are properly added and loaded to the notebook in order to be manipulated and transformed using pandas. The main challenge on this section is the relationships that must be found between all three files. Also, working with the `json` format represented a challenge. 
There are six cells that have the **# ------- OMITIDO ---------#** comment, which means that that step is not taken into consideration for further stages. Those cells are directly related to the personality test results processing. They are not considered because no broad relationship was found and, considering it, would have created a lot of `NULL` values and caused problems in further transformations and stages.

**2. Machine Learning stage**

In this section, we import the required SciKitLearn libraries for the data split and algorithm training. First, we separate the __target variable__ from the __features__ and define what information is categorical and what information is numerical. Later, whe preprocess the data with `StandardScaler` for the numerical features and `OneHotEncoder` for the categorical ones.
After that is done, we select an algorithm to train. In this case, `RandomForest` is selected with 100 estimators and a `random_state` of 42. Afterwards, a pipeline is defined and the _Train/Test Split_ is done, considering 30% of the data as the __test set__.
We finish this stage by training the model with `pipeline.fit()`, verifying the predictions using `pipeline_predict()` and printing the **Accuracy** (obtaining __0.8708827404479579__ in this case) and the **Classification Report**:


![image](https://github.com/user-attachments/assets/b203f497-1aa7-4da9-8483-e6c00784babd)


**3. Model testing stage**

Three tests are proposed in this project. The first one takes the values of a person that would NOT leave the company in the next 3 months, obtaining a correct prediction. The second test considers data really CLOSE to a person that would leave the company in three months after hiring and, in this case, the algorithm predicts that the test person could leave within 3 months. The last test was made considering data of a person that would INDEED leave the company in three months after getting hired and the algorithm predicted correctly that the person had this tendency.

## Conclusions

This project developed a small pipeline oriented to predict if a person would leave the company within 3 months of getting hired. The results were very accurate and all three tests developed where passed. This can be further developed to enhance the hiring processes of companies and reduce the hiring of people with high rotation tendency in the early stages of the hiring process. 
