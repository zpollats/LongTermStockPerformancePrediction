# LongTermStockPerformancePrediction

## Overview and Business Problem

For decades, many humans have attempted to predict the stock market. These attempts have varied in nature from predicting individual stock prices to predicting the direction of the overall market. While most argue that it's impossible to beat the market as an individual investor, I believe that with the right tools and technology, individuals can indeed outperform the market. While I believe this idea is possible, the data shows that individual investors' performances are dreadful on average when compared to the broader market. The bar chart below shows that the average investor had annual returns of 1.9% from 1999-2018 while the S&P500 returned 5.6%.

![](images/IndInvInfographic.jpeg)

Currently, to be a well-versed individual investor requires significant time researching companies, listening to earnings calls, and having an understanding of macro-economic trends. Most people do not have the time to become knowledgable on multiple companies that are publicly traded, so it's easier and safer to invest in index funds that track the overall market. But what if there was a tool that could quickly let individual investors know which companies can beat the market over an extended period of time?

## Data Understanding

I have sourced all the required data myself using the SEC's API. I used this API to pull the annual reports (10-K) for public companies from 2009-2012. I could not get any useful data from before 2009 because the SEC didn't require companies to file in XBRL format until then. In the future, I plan to use other methods to acquire and clean data prior to 2009. I stopped collecting data past 2012 because I need a 10 year window to determine if a stock outperformed the market over 10 years based on their financials. 

In terms of metrics that I will use to score the performance of my model, recall will be the most important metric followed by precision. Recall will score how my model does at identifying stocks that do outperform the market. Investors will care more about finding the stocks that can outperform the market rather than correctly identifying those that underperform. Precision will also be a key metric because this gives a score for how accurate our model performs when predicting that a stock does outperform the market. To simplify the metrics I use, I can also use the f1 score as this is the harmonic mean of precision and recall.

![](images/)

## Modeling
For creating my final model to address this problem, I started with a selection of simpler classification models including Logistic Regression, K Nearest Neighbors, and Decision Tree Classifier. From there, I moved onto more complex options including Random Forest Classifier and XGBoost. I created Random Forest models and XGBoost models both with and without SMOTE performed on the data due to a class imbalance. I found that the models performed much better when I synthetically oversampled the minority class (stocks that beat the market).  

![](images/)


### Results

Our final Stacking Classifier model achieved an accuracy on unseen data of 79.0%. We found that our model correctly classified functional and non-functional water pumps better than pumps that were functional needing repair. This can be seen in the grouped bar chart below:

![](images/ClassPredictions.png)

The confusion matrix confirms that our model performs best for functional and non-functional water pumps. One point of concern with our model is that the majority of misclassifications for pumps that are functional needing repair are that the pumps are functional. This means we would be overlooking select water pumps that need repair because our model classifies them as functional. The confusion matrix can be seen below:

![](images/ConfusionMatrix.png)

The ROC curves for each feature class are shown below. As we expected, the AUC score for our functional needs repair class is slightly lower than those of the functional and non-functional classes. 

![](images/ROC.png)


### Limitations

Some limitations that we ran into include:
- Non-Standardized Data: companys' financial documents can use various naming conventions, which makes cleaning the data more cumbersome.
- Time to run models: running multiple GridSearchCV fits can take hours if not days.
- Variety of Filing Formats: the SEC didn't require XBRL data to be filed until 2009, so data prior to this year cannot be accessed in the same manner as data afterwards.

### Next Steps

With more time and resources, here are a few next steps that we would like to pursue for this project:
- Ingest more data: this initial model was built on data from 2009-2012, but there is public market data dating back over 100 years. The first step I will take in improving this model is to intake and clean all available historical data on publicly traded companies. 
- Further tune model: with more time, I could run more grid searches with more hyper parameters included. Some of these grid searches could take multiple days, so I would need significantly more time to optimize the final model.

## Conclusion

In conclusion, using our model will allow the Tanzanian Ministry of Water to optimize their resource allocation by sending maintenance teams to pumps that truly need repairs or are non-functional. In following our model, the Tanzanian Ministry of Water will be able to ensure that non-functional water pumps are out of service for minimal time, which will improve access to potable water for the people of Tanzania. Our model was able to predict the correct class on unseen data approximately 80% of the time. 

## For More Information

See the full analysis in the [Data Cleaning Notebook](working_notebook.ipynb) and the [Modeling Jupyter Notebook](modeling_notebook.ipynb) or review [this presentation](presentation.pdf).

For additional info, you can reach out to me:

- email:    zacharypollatsek@gmail.com
- cell:     (435)655-5233

## Repository Contents
- data
- images
- working_notebooks
- modeling_notebook.ipynb
- working_notebook.ipynb
- .gitignore
- README.md
- LICENSE.md
- presentation.pdf
