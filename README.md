

## Overview and Business Problem

### Business Understanding
Water Problems in Tanzania, like many countries in Sub-Saharan Africa, faces significant challenges related to water supply and quality. The country struggles with uneven distribution and inadequate infrastructure. Many rural areas, in particular, experience severe water scarcity, which impacts health, agriculture, and economic development. The main issues include limited access to safe drinking water, inadequate sanitation, and frequent droughts, which exacerbate water shortages and affect food security. According to reports, only about 57% of the population has access to basic water services, and the situation is even more dire in rural regions where women and children often have to travel long distances to fetch water from unprotected sources, which are often contaminated and unsafe.

Water Well Projects in Tanzania
To address these critical issues, numerous water well projects have been initiated by the Tanzanian government, non-governmental organizations (NGOs), and international aid agencies. These projects aim to provide sustainable access to clean and safe water, primarily in underserved rural areas. The construction of water wells, including boreholes and shallow wells, is a common solution. These wells tap into underground aquifers to provide a reliable source of clean water. Many projects also incorporate the installation of hand pumps and mechanized pumps to improve water retrieval efficiency.

The challenges faced after implementing water well projects in Tanzania revolve around maintenance and sustainability, water quality, community involvement, financial constraints, environmental factors, and coordination with broader water management efforts. These projects encounter issues like the lack of expertise for maintenance, water contamination risks, insufficient community engagement, funding uncertainties, environmental impacts on water availability, and the need for integrated water resource management strategies. Overcoming these challenges demands a comprehensive approach combining technical solutions, community empowerment, sustainable financing, and holistic water management to ensure the long-term success of water well projects in Tanzania.


### Business Problem
We are tasked with developing a prediction tool that will predict water pumps in need of repair. We used the data provided in an iterative modeling process to create a final classification model or tool that can be used by development organizations to predict whether or not a pump is in need of repair before the pump fails. This tool will enable development organizations to appropriately allocate resources in dispatching repair teams.

Being a data science consulting company we have been hired by the Tanzanian Ministry of Water to create a prediction model to help classify whether water pumps are in need of repair (functional, functional but in need of repairs or non-functional). We have been hired to help reduce the possibility of the above mentioned challenges from occuring as it leads to waste of the Ministry's resources and only send out repair teams to pumps that only need of repairs or are non-functional.

 Main object is to maximize accuracy and  recall to ensure the people of Tanzania have access to potable water and few pumps that are non-functional or in need of repairs are over looked.


## Data Understanding

The data is sourced from Taarifa and the Tanzanian Ministry of Water. Data utilized can be found here: https://www.drivendata.org/competitions/7/pump-it-up-data-mining-the-water-table/data/

For the purposes of our evaluation, we are utilizing the Training Set Labels and Training Set Values, which include data from 59,400 pumps. Our cleaned data contains information from 59,028 pumps. Some of the features that are included in this dataset include location/geography data, installation data, as well as how the pumps are managed. 

We can see that our dataset has a class imbalance problem because the majority of the pumps are either functional or non-functional; we have very little data on pumps designated as functional but needing repair. The bar chart below shows this class imbalance:

![](images/C:\Users\Bee\Documents\GitPrac\DSC-PH-3-project\images\Well_Status_bar_Chart.png)

## Modeling
For creating our final model to address this problem, we started with a selection of simpler classification models including Logistic Regression, K Nearest Neighbors, and Decision Tree Classifier. From there, we moved onto more complex options including Random Forest Classifier and XGBoost. Ultimately, we found that using a Stacking Classifier composed of a Random Forest Classifier and XGBoost performed the best through cross validation. The image below shows our CV scores for 5 folds for various models: 

![](images/ModelAccuracyScores.png)

### Rationale

Our rational for using a Stacking Classifier was to use the strengths of both a Random Forest Classifier and XGBoost in one model. We found that a default Random Forest Classifier and XGBoost both performed relatively well in a cross validation, so we combined these models into one using a Stacking Classifier. 

### Results

Our final Stacking Classifier model achieved an accuracy on unseen data of 79.0%. We found that our model correctly classified functional and non-functional water pumps better than pumps that were functional needing repair. This can be seen in the grouped bar chart below:

![](images/ClassPredictions.png)

The confusion matrix confirms that our model performs best for functional and non-functional water pumps. One point of concern with our model is that the majority of misclassifications for pumps that are functional needing repair are that the pumps are functional. This means we would be overlooking select water pumps that need repair because our model classifies them as functional. The confusion matrix can be seen below:

![](images/ConfusionMatrix.png)

The ROC curves for each feature class are shown below. As we expected, the AUC score for our functional needs repair class is slightly lower than those of the functional and non-functional classes. 

![](images/ROC.png)


### Limitations

Some limitations that we ran into include:
- Class Imbalance: there are very few data points with Function Needs Repair.
- Time to run models: running multiple GridSearchCV fits can take hours if not days.
- Lack of domain expertise: we are not well versed in what factors for water pumps contribute to its ability to function or not

### Next Steps

With more time and resources, here are a few next steps that we would like to pursue for this project:
- Treat problem as binary classification: given that a pump labeled "Functional needs Repair" could become non-functional at any time, we could label these pumps as non-functional. Thus, if our model predicts it is non-functional, a maintenance crew will still go check to pump to perform repairs.
- Further tune model: with more time, we could run more grid searches with more hyper parameters included. Some of these grid searches could take multiple days, so we would need significantly more time to optimize the final Stacking Classifier.
- Explore other models: in this project, we used Logistic Regression, KNN, Decision Tree Classifier, Random Forest Classifier, XGBoost, and Stacking Classifier models. We could look into other boosting models as well as simple neural networks to better predict our data set classes.
- Consult with a domain expert to achieve a better understanding of the water crisis plaguing Tanzania and how the functionality of water pumps relates to this issue. 

## Conclusion

In conclusion, using our model will allow the Tanzanian Ministry of Water to optimize their resource allocation by sending maintenance teams to pumps that truly need repairs or are non-functional. In following our model, the Tanzanian Ministry of Water will be able to ensure that non-functional water pumps are out of service for minimal time, which will improve access to potable water for the people of Tanzania. Our model was able to predict the correct class on unseen data approximately 80% of the time. 

## For More Information

See the full analysis in the [Data Cleaning Notebook](\DSC-PH-3-project\index.ipynb) and the [Modeling Jupyter Notebook](\DSC-PH-3-project\modeling_notebook.ipynb) or review [this presentation](presentation.pdf).



## Repository Contents
- data
- images
- notebooks
- README.md
- presentation.pdf