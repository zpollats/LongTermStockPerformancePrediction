# LongTermStockPerformancePrediction

## Overview and Business Problem

For decades, many humans have attempted to predict the stock market. These attempts have varied in nature from predicting individual stock prices to predicting the direction of the overall market. While most argue that it's impossible to beat the market as an individual investor, I believe that with the right tools and technology, individuals can indeed outperform the market.

Currently, to be a well-versed individual investor requires significant time researching companies, listening to earnings calls, and having an understanding of macro-economic trends. Most people do not have the time to become knowledgable on multiple companies that are publicly traded, so it's easier and safer to invest in index funds that track the overall market. But what if there was a tool that could quickly let individual investors know which companies can beat the market over an extended period of time?

## Data Understanding

I have sourced all the required data myself using the SEC's API. I used this API to pull the annual reports (10-K) for public companies from 2009-2012. I could not get any useful data from before 2009 because the SEC didn't require companies to file in XBRL format until then. In the future, I plan to use other methods to acquire and clean data prior to 2009. I stopped collecting data past 2012 because I need a 10 year window to determine if a stock outperformed the market over 10 years based on their financials. 

![](images/)

## Modeling
For creating our final model to address this problem, we started with a selection of simpler classification models including Logistic Regression, K Nearest Neighbors, and Decision Tree Classifier. From there, we moved onto more complex options including Random Forest Classifier and XGBoost. Ultimately, we found that using a Stacking Classifier composed of a Random Forest Classifier and XGBoost performed the best through cross validation. The image below shows our CV scores for 5 folds for various models: 

![](images/)

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

See the full analysis in the [Data Cleaning Notebook](notebooks/data_cleaning.ipynb) and the [Modeling Jupyter Notebook](notebooks/modeling_notebook.ipynb) or review [this presentation](presentation.pdf).

For additional Zach Pollatsek as follows:

- Zach:    zacharypollatsek@gmail.com, (435)655-5233

## Repository Contents
- data
- images
- notebooks
- .gitignore
- README.md
- LICENSE.md
- presentation.pdf
