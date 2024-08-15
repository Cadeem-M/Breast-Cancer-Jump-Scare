# Breast Cancer Jump Scare

<p align="center">
<img src="Resources\Images\Breast_cancer_pic1" width="800px">
</p>

## Overview 

Team 5 - Jaskirat Singh, Aditya Singh Thakur, Cadeem Musgrove and Lucas Perez - has the goal of understanding breast cancer *********. Specifically, we want to analyze how well we can predict survival rates and treatment types to patients given their cancer type. To go about this, we create various models using METABRIC_RNA_Mutation.csv to select target variables such as "overall_survival" and "treatment_type". 

--- overall survival vs neoplasm_histologic_grade When a patient's histological grade is on the file, can we predict overall survival based on the model?

outcome of breast cancer treatment type vs cancer type

What type of cancer treatment can we predict from our model based on the type of cancer diagnosis given to a patient? ---

****

## Analysis and Results

* Data Processing:

1) First we use spark to read in the data set saved on an S3 bucket.

2) The data set initially had had 693 columns. The first two questions we wanted to answer did not require them so to begin cleaning the data, we dropped all columns except the first 31. 

<p align="center">
<img src="Resources\Images\Screenshot 2024-08-14 174710.png" width="500px">
</p>

3) To analyze a patients survival we used a logistic regression as a baseline and compared the results to a random forrest model.

- Ran a logistic regression using target: 'overall_survival and
 features: 'chemotherapy', 'hormone_therapy', 'radio_therapy', 'tumor_size', 'tumor_stage', 'age_at_diagnosis',
           'type_of_breast_surgery_BREAST CONSERVING', 'type_of_breast_surgery_MASTECTOMY', 'inferred_menopausal_state_Post'

<p align="center">
<img src="Resources\Images\Screenshot 2024-08-14 113753.png" width="350px">
</p>

- Logistic regression results

<p align="center">
<img src="Resources\Images\Screenshot 2024-08-14 181448.png" width="350px">
</p>

- Ran a Random Forest Model using target **********

<p align="center">
<img src="Resources\Images\Screenshot 2024-08-14 113925.png" width="350px">
</p>

- Logistic regression results ********************************

<p align="center">
<img src="Resources\Images\Screenshot 2024-08-14 181448.png" width="350px">
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
<img src="Resources\Images\Screenshot 2024-08-14 194527.png" width="350px">
</p>

- An Accuracy of 52% suggest the model struggles to make predictions that align with actual outcomes


- Sequential Models:
<p align="center">
<img src="Resources\Images\Screenshot 2024-08-14 182652.png" width="350px">
</p>

<p align="center">
<img src="Resources\Images\Screenshot 2024-08-14 113925.png" width="350px">
</p>

<img src="Resources\Images\Screenshot 2024-08-14 192555.png" width="350px">
</p> 

<p align="center">
<img src="Resources\Images\Screenshot 2024-08-14 113925.png" width="350px">
</p> *********** needs results.


- This model uses 3 layers (2 hidden, 1 outter).
    Layer 1 -> 64 neurons 
    Layer 2 -> 32 neurons (half of layer 1 as we try to approach 8 neuron for our final layer)
    Layer 3 -> 8 neurons (one neuron for each treatment type)

- We start by using epochs = 40

- This model uses relu as the activation function within the hidden layers and it uses softmax as the function for the outter layer as it attempts to solve the multi-classification problem.

- This model was able to achieve 72.9% accuracy. **********************

* Attempting to Improve the Sequential Model

-  The number of starting neurons were increased from 64 to 128 and an additional layer was added to help the model capture more patterns in the data. Additionally, 2 dropout layers were added to help regularize the model by reducing the chance that the model overfits to the data. 


<p align="center">
<img src="Resources\Images\Screenshot 2024-08-14 182728.png" width="350px">
</p>

- Epochs were increased from **** to **** to ***** to allow for more learning time

<p align="center">
<img src="Resources\Images\Screenshot 2024-08-14 193627.png" width="350px">
</p>

<p align="center">
<img src="Resources\Images\Screenshot 2024-08-14 193707.png" width="350px">
</p>

- The accuracy of the new model is about *****

<p align="center">
<img src="Resources\Images\Screenshot 2024-08-14 193707.png" width="350px">
</p> **** needs results


## Summary

We set out to asnwer 3 questions in this project **** **** ***. Thus, we tackled each question by trying to model the answers provided in our original data set. For our model of *, our logistic regression had an accuracy of 62%. To Try improving on this we did a random survival forest and found the accuracy of **%. ** [discuss if an improvement and ways to improve. ]

For our model of **, our logistic regression returned an accuracy of 52% which suggests it is not a very good model for predicting outcomes. To improve on this, we applied a Sequential model and got an accuracy of **. To further improve on this we built a more complex Sequential model. By increasing the number of nuerons and layers and adding dropout layers, our complex model finally had an accuracy of **. **[ discuss if an improvement/downgrade and ways to improve. ]

Discuss Jas part *



Acknowldgements


Helpful links/Credits 
https://www.youtube.com/watch?v=f579O7Ef8C0 - How to Upload Pandas DataFrame Directly to S3 Bucket AWS python boto3

https://stackoverflow.com/questions/53898836/export-dataframe-as-csv-file-from-google-colab-to-google-drive - saving a csv in colab