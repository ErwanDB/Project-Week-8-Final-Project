<img src="https://bit.ly/2VnXWr2" alt="Ironhack Logo" width="100"/>

# Predict Rock Injectivity
*Erwan de Boisjolly*

*[Data analytics bootcamp - Barcelona - June 2020]*

## Content
- [Project Description](#project-description)
- [Hypotheses / Questions](#hypotheses-questions)
- [Dataset](#dataset)
- [Cleaning](#cleaning)
- [Analysis](#analysis)
- [Model Training and Evaluation](#model-training-and-evaluation)
- [Conclusion](#conclusion)
- [Future Work](#future-work)
- [Workflow](#workflow)
- [Organization](#organization)
- [Links](#links)

## Project Description
This project is about predicting rock injectivity: capacity of a rock formation to be fractured. The goal is to predict it from drilling parameters without being intrusive to the drilling process. The final application should allow to enhance completion design of the well.

## Hypotheses / Questions
* Is it possible to model accurately rock injectivity from drilling parameters ?
* What are the most important parameters to predict rock injectivity?
* Do we need more variables ? Are the engineering features such as MSE (Mechanical Specific Energy) useful ?

## Dataset
* Data comes from a shale gas well on which a data science project was already performed to predict torque on bit. This project reuse the same data. Data were already anonymised as a consequence of the previous project. Any remaining information that could relate the data to the client or the well were deleted.
* Data are time series but the time variable is not useful for the study. Data comes with 5 second sampling rate and include basic drilling parameters commonly acquired in every drilling.
* One additional feature and the labels comes from different logs that are depth based.
* Raw data are stored in the data folder of the repository and are splitted in several excel files:
	1. BHA8_lateral.xlsx
	2. GR_injectivity.xlsx

## Cleaning, filtering & wrangling
Data comes time based because the sensors of the drilling rig (platform) are recording all the time.  For this project, drilling data are needed. However there are some times the rig stops the drilling process to perform some repair and maintenance. On those downtimes, sensors are still recording but we don't need those data. We need to segregate those data from the data while the rig is drilling the rock formation.
To do this, unsupervised learning was performed using KMeans algorithm. One of the clusters detected by the algorithm was effectively the drilling data needed for the project.
Fine tuning of the data filtering was done first using an Isolation Forest algorithm. However there were les than 1% noise so the few remaining outliers were removed using manual filters.
Finally, one additional feature and the labels were merge to the dataset. This final merge is responsible of a significant loss of data as the extra logs have a much lower resolution than the time data.  

## Analysis
* Include charts to demonstrate the effect of your work: correlation matrix

* After dropping non-useful columns, feature engineering was done adding three new features: DOC, MSE and DS. Features with high correlation were dropped.
* A shortlist of basic models were first train and evaluated on their scores. From this step, three models came out with good results:
	1. RandomForestRegressor
	2. KNearestNeighbors regressor
	3. GradientBoostingRegressor
* Feature selection was then performed using several algorithm: RandomForest feature importance attribute, ANOVA test, and RFE (recursive feature elimination). From this step, it was decided to drop three features that were downgrading models performances.
One of the learnings on the feature selection is that surface parameter (in opposition to downhole parameters) are most correlated to the target. In fact, surface parameters have less noise, their evolution while drilling are less erratic than downhole parameters signals. For this reason correlation with the target is easier to evaluate. This can be an improvement for preprocessing downhole parameters.

## Model Training and Evaluation
* From the three most promising model mentioned above, hyper parameters  were fine-tuned using cross validation.

Graphs scores

* From the results above, ensemble methods were used to combined the cross validated models. Voting and stacking technics were evaluated and stacking turn to give the best score on the train set.

## Conclusion
* Summarize your results. What do they mean?
* What can you say about your hypotheses?
* Interpret your findings in terms of the questions you try to answer.

## Future Work
Address any questions you were unable to answer, or any next steps or future extensions to your project.

## Workflow
Outline the workflow you used in your project. What were the steps?
How did you test the accuracy of your analysis and/or machine learning algorithm?

## Organization
How did you organize your work? Did you use any tools like a trello or kanban board?

What does your repository look like? Explain your folder and file structure.

## Links
Include links to your repository, slides and trello/kanban board. Feel free to include any other links associated with your project.


[Repository](https://github.com/)  
[Slides](https://slides.com/)  
[Trello](https://trello.com/en)  
