# Breast Cancer Jump Scare

<p align="center">
<img src="Resources\Images\Breast_cancer_pic2.jpg" width="800px">
</p>

## Overview 

Team 5 - Jaskirat Singh, Aditya Singh Thakur, Cadeem Musgrove and Lucas Perez - the goal of the project is to get a deeper understanding on breast cancer and the treatment given to patients and their survivability rates. We want to further dive into the nuances of the the treatment types and the type of cancer. To go about this, we create various models using a METABRIC_RNA_Mutation.csv retreived from kaggle to select target variables such as "overall_survival" and "treatment_type". 


## Analysis and Results

* Data Processing:

1) First we use spark to read in the data set saved on an S3 bucket.

2) The data set initially had had 693 columns. The first two questions we wanted to answer did not require them so to begin cleaning the data, we dropped all columns except the first 31. 

<p align="center">
<img src="Resources\Images\Screenshot 2024-08-14 174710.png" width="600px">
</p>

3) To analyze a patients survival chances we used a logistic regression as a baseline and then created a random forrest model to further look at a patients survival chances given a time period.

- Ran a logistic regression using target: 'overall_survival and
 features: 'chemotherapy', 'hormone_therapy', 'radio_therapy', 'tumor_size', 'tumor_stage', 'age_at_diagnosis',
           'type_of_breast_surgery_BREAST CONSERVING', 'type_of_breast_surgery_MASTECTOMY', 'inferred_menopausal_state_Post'

<p align="center">
<img src="Resources\Images\Screenshot 2024-08-14 113753.png" width="600px">
</p>

- Logistic regression had a 62% accuracy

<p align="center">
<img src="Resources\Images\Screenshot 2024-08-14 181448.png" width="600px">
</p>


- Random Survival Forest Model 

<p align="center">
<img src="Resources\Images\Screenshot 2024-08-14 113925.png" width="600px">
</p>

- With the Random Survival Forest model, we managed to create a data frame that predicted a patients odds of survial at 180, 365, 545 and 730 days.

<p align="center">
<img src="Resources\Images\Screenshot 2024-08-14 212739.png" width="600px">
</p>



4) To analyze and predict treatment types, we created 2 Sequential neural networks via tensorflow and did a logistic regression. The first network and the regression model are baselines and the second network makes adjustments to our layers and neurons in an attempt to improve upon the network's model.

-   target: treatment_type" 
    features: 'age_at_diagnosis', 'type_of_breast_surgery', 'cancer_type',
       'cancer_type_detailed', 'cellularity', 'pam50_+_claudin-low_subtype',
       'cohort', 'er_status_measured_by_ihc', 'er_status',
       'neoplasm_histologic_grade', 'her2_status_measured_by_snp6',
       'her2_status', 'tumor_other_histologic_subtype',
       'inferred_menopausal_state', 'integrative_cluster',
       'primary_tumor_laterality', 'lymph_nodes_examined_positive',
       'mutation_count', 'nottingham_prognostic_index', 'oncotree_code',
       'overall_survival_months', 'overall_survival', 'pr_status',
       'tumor_size',

- logistic regression:

<p align="center">
<img src="Resources\Images\Screenshot 2024-08-14 194527.png" width="600px">
</p>

- An Accuracy of 52% suggest the model struggles to make predictions that align with actual outcomes


- Sequential Models:
<p align="center">
<img src="Resources\Images\Screenshot 2024-08-14 182652.png" width="600px">
</p>

<p align="center">
<img src="Resources\Images\Screenshot 2024-08-14 113925.png" width="600px">
</p>

<img src="Resources\Images\Screenshot 2024-08-14 192555.png" width="600px">
</p> 

<p align="center">
<img src="Resources\Images\Screenshot 2024-08-14 233414.png" width="600px">
</p> 


- This model uses 3 layers (2 hidden, 1 outter).
    Layer 1 -> 64 neurons 
    Layer 2 -> 32 neurons (half of layer 1 as we try to approach 8 neuron for our final layer)
    Layer 3 -> 8 neurons (one neuron for each treatment type)

- We start by using epochs = 40

- This model uses relu as the activation function within the hidden layers and it uses softmax as the function for the outter layer as it attempts to solve the multi-classification problem.

- This model was able to achieve 57% accuracy. 

* Attempting to Improve the Sequential Model

-  The number of starting neurons were increased from 64 to 128 and an additional layer was added to help the model capture more patterns in the data. Additionally, 2 dropout layers were added to help regularize the model by reducing the chance that the model overfits to the data. 


<p align="center">
<img src="Resources\Images\Screenshot 2024-08-14 182728.png" width="600px">
</p>

- Epochs were increased from 10 to 75 to  100 to allow for more learning time

<p align="center">
<img src="Resources\Images\Screenshot 2024-08-14 192555.png" width="600px">
</p>

<p align="center">
<img src="Resources\Images\Screenshot 2024-08-14 193627.png" width="600px">
</p>

<p align="center">
<img src="Resources\Images\Screenshot 2024-08-14 193707.png" width="600px">
</p>

- The accuracy of the new model remains 57%

<p align="center">
<img src="Resources\Images\Screenshot 2024-08-14 233437.png" width="600px">
</p> 


## Summary

Our group set out to get a deeper understanding of breast cancer patient's treatment and survivability rates. Thus, we tackled our goal by trying to model the data provided in our original data set. For our model of patients surviving with cancer, our logistic regression had an accuracy of 62% which suggests room for improvement. Then to gain more insight, we did a random survival forest model to look at a patients survivability given a time period into the future. 

For our model of cancer treatment, our logistic regression returned an accuracy of 52% which suggests it is not a very good model for predicting outcomes. To improve on this however, we applied a Sequential model and tried making improvementes upon it. Initially, our first Sequential got an accuracy of 57% using 3 layers and 64 initial neurons. To further improve on this, we built a more complex Sequential model by increasing the number of initial nuerons to 128 and increasing layer to 5 ( 3 hidden layers with neurons and 2 dropout layers). Our complex model's accuracy remained at 57%. Perhaps we could have looked at reducing the number of features to get better results. 




## Credits 
Alharbi, R. 2020. Breast Cancer Gene Expression Profiles (METABRIC) (Version 1) [Data set]. Kaggle.
    https://www.kaggle.com/datasets/raghadalharbi/breast-cancer-gene-expression-profiles-metabric/data

(2023). *Breast Cancer: Be Aware and Take Action*[Infographic]. Trios Health. 
    https://www.trioshealth.org/news/breast-cancer-be-aware-and-take-action


## Helpful links
https://www.youtube.com/watch?v=f579O7Ef8C0 - How to Upload Pandas DataFrame Directly to S3 Bucket AWS python boto3

https://stackoverflow.com/questions/53898836/export-dataframe-as-csv-file-from-google-colab-to-google-drive - saving a csv in colab


## S3 links to our datasets
cleaned data set (31 columns): https://project4-group5-cadeem-bucket.s3.us-east-2.amazonaws.com/Cleaned_Breast_Cancer_data.csv

Predicted Survivability Dataframe: https://project4-group5-cadeem-bucket.s3.us-east-2.amazonaws.com/Patients_survival.csv

Uncleaned Data set: https://project4-group5-cadeem-bucket.s3.us-east-2.amazonaws.com/METABRIC_RNA_Mutation.csv

## Tableau link to visualizations
https://public.tableau.com/app/profile/lucas.perez7848/viz/Breast_Cancer_Jump_Scare_17236965875940/BreastCancerTreatmentsandSurvival?publish=yes
