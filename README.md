# Social-Network-Graph-Link-prediction
<img src = https://learningsolutionsmag.com/assets/images/learningsolutions/110311/image001_110311.png width =1000 >
<p>Facebook did a recruiting challenge some times back on Kaggle where they gave this dataset.Here we are trying to find missing links which we will use for recommending friends or followers or in general recommending connections.Facebook created this to sove their business problem.The dataset is fairly reasonably sized to get a feel and understanding of how Network Analaysis works with Machine Learning in real world scenarios.Facebook has given this problem based on directed graphs which represent users on social network.<p>
  
  
### Problem statement: 
Given a directed social graph, have to predict missing links to recommend users (Link Prediction in graph)

### Business objectives and constraints:  
- No low-latency requirement.
- Probability of prediction is useful to reccommend highest probability link
- We got to suggest connections which are most likely to be correct and we should try and not miss out at any connections
### Data Overview
Taken data from facebook's recruting challenge on kaggle https://www.kaggle.com/c/FacebookRecruiting  
data contains two columns source and destination eac edge in graph 
    - Data columns (total 2 columns):  
    - source_node         int64  
    - destination_node    int64  
### Performance metric for supervised learning:  
- Both precision and recall is important so F1 score is good choice
- Confusion matrix
 
## Approach:
### Mapping the problem into supervised learning problem:
- Mapping this to a binary classification task with 0 implying an absence of an edge and 1 representing the presence as y_i's.Our most important objective here is to get features from a certain pair of vertices(u_i,u_j) such that they can help us in predicting the presence/absence of an edge.
### Data Cleaning and preprocessing:
<br>Cleaning and imputing the missing values,what we found is that in the training data we have information about only those nodes who have a directed edge between them,not about nodes not having any edges between them.So to pose this as a classification problem we need to add all those nodes and add their label as '0'</br>
### Feature engineering:
We curated features like __number of followers and followees of each node__, whether or not a node is __followed back__ by any other nodes, __page rank of individual nodes__, __katz score__, __jaccard index__, __preferential attachment__,__svd features__, __svd dot features__, __adar index__ ,and so on. There were a total of 59 features on which we train and test our model.

### Splitting the data:
<br>There is not timestamp provided for this data. Ideally, if you think about it, we have the dataset for a given time stap t. However, the graph is evolving and changing over time. After 30 days the edge connections might change, because people might have new followers and they may even start to follow new people. In the real word, we would split the data according to time. But, since we do not have any information about time stamp, we will split the data randomly in 80:20 ratio. 80% for training data and 20% for cross validation data.</br>

### Modelling strategy:
Use two Ensemble models and performed hyperparameter tuning along with elastic net regularization to avoid ovverfitting of the data 
__Model 1: Random forest hypertuned using RandomsearchCV__
<img src = https://github.com/yatscool007/Social-Network-Graph-Link-prediction/blob/master/New%20folder/rf_roc_test.PNG height = 300>

__Model 2: XGBoost hypertuned using RandomsearchCV__
<img src =https://github.com/yatscool007/Social-Network-Graph-Link-prediction/blob/master/New%20folder/xgb_roc_test.PNG height = 300 >

## Results:
<img src = https://github.com/yatscool007/Social-Network-Graph-Link-prediction/blob/master/New%20folder/final.PNG>

### Hyperparameter tuning using Randomized Search cross validaion was done for both the models and our f1 score imporved by a small margin for Randomr forest model ,where we got f1 score for training data 0.963 and for test data the score was 0.926
