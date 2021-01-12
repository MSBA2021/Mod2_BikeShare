A boosted tree iteratively fits trees where each tree tries to correct the errors of all of the previous trees (summed together). This is a very powerful machine learning technique, and read ISL 8.2.3. Boosted trees have all of the same parameters as regression trees, and additionally they have the following two parameters.
  * `n_estimators`: This is the number of trees used for the final model. The more trees, the more likely the model is to overfit.
  * `learning_rate`: This is a parameter that determines how much weight is given to each tree (it is the lambda in ISL). The larger this number, the more likely the model is to overfit.

A regression tree has a few possible parameters that can be tuned.
  * `max_depth`: This sets the maximum number of splits between the top of the tree and any leaf. A smaller number means a smaller tree, and therefore a tree that is less likely to overfit.
  * `min_samples_split`: This sets the number of samples that must be in a leaf for the leaf to be a candidate for a split. A larger number means a smaller tree. This must be greater than or equal to 2.
  * `min_samples_leaf`: This is identical to `min_samples_split`, but this is how many samples have to be left in each leaf after the split. This must be greater than or equal to 1. Generally, you tune either `min_samples_leaf` or `min_samples_split`, not both. They do such similar things that it is quite redundant.
  * `max_features`: This is a parameter that tunes how many features a regression tree will consider when it is splitting a node. A value between 0 and 1 will tell it to use only a random fraction of the possible nodes when it's considering a split. E.g., if you have 10 variables, and you set this to `.3`, then each time the algorithm is deciding to split a leaf, it will pick three random variables and only select from one of those. This will keep a tree from focusing too heavily on certain variables by forcing it to include information from other variables in the decision process. A smaller value means a tree that is generally less likely to overfit. If you set it to `None`, then it will consider all variables at each split (this is the default).
  * `min_impurity_decrease`: This parameter sets how much the evaluation criteria has to go down before it will split a node. A larger value means there is a higher threshold before a node can be split, so this will lead to a smaller (and less overfit) tree.
  * `ccp_alpha`: This is the _cost complexity pruning alpha_ discussed in Chapter 8.1 of ISL on tree pruning. The higher the `ccp_alpha`, the more pruning will happen on the tree and the more regularized the tree will be. The default value is `0`, which implies that the tree will not be pruned. Another discussion can be found [here](https://scikit-learn.org/stable/modules/tree.html#minimal-cost-complexity-pruning).
  
  . With a random forest, the goal is to have them do well on average (take advantage of the wisdom of crowds), so we likely will want each of our individual trees to be significantly simpler in our random forest then with the regression tree. We also want our trees to be diverse (i.e., we don't want them all to make the same mistakes). The best way to do that is to force them to use different features using the `max_features` parameter. While we can tune `max_features` for an individual regression tree, it becomes much more important for a random forest.

The random forest has one additional parameter that the regression tree doesn't have, `n_estimators`, or the number of trees in the forest. Do you need to worry about overfitting if you have too many trees? Think about this and come to class prepared to discuss.
  
  
  
  
  
  
  
  
  
  
  
  

It is very helpful to play around with these parameters to get a sense for what they do. For more information, you can find the documenation for the `sklearn` implementation of `DecisionTreeRegressor` [here](https://scikit-learn.org/stable/modules/generated/sklearn.tree.DecisionTreeRegressor.html). Note that you don't have to set all of these parameters. They have default values, and you can leave them at the default.




Topic:      Random Forests and Boosted Trees

Case:       Kaggle’s Bike Sharing Demand Competition (QA-0828)

Data:       Available from Kaggle (necessary files are train.csv, test.csv, and sampleSubmission.csv)

Code:       BikeStarter.ipynb

Assignment:

1. Read the case.
2. Download the training (train.csv) and testing (test.csv) sets and the sample submission file (sampleSubmission.csv) from Kaggle at https://www.kaggle.com/c/bike-sharing-demand. You will need to sign up for Kaggle in order to do this.
3. Visualize the training set in Tableau. Which features may be good predictors? Are there any features you would like to engineer? Come to class ready to share visualizations.
4. Do the readings at the links provided in the starter code to learn about random forests and boosted trees: read Chapter 8 from Introduction to Statistical Learning (ISL). Come to class ready to discuss random forests, bagging, and boosting as well as the various ways in which tree based models can be tuned.
5. Use the Python starter code provided to build a predictive model.
6. Extend the starter code to include additional features in your model.
7. Submit your best predictions to Kaggle. Enter your teams RMSLE that you received from Kaggle in the google sheet at https://docs.google.com/spreadsheets/d/1Aa1Q3eFirUNAgsaC8J4kxti-FrMGDrMVIsfLRyCjJAQ/edit?usp=sharing.
8. Be prepared to show your notebook and discuss your team's modeling strategy. A prize will go to the top ranking team.