# Welcome to our team project website!

This is a website to showcase our final project for FIN 377 - Data Science for Finance course at Lehigh University.

This project and website was created by Tim DiPalo, Tom Griffith, and Christyan Jean-Charles.

To see the complete project repo, click [here](https://github.com/tdip19/FinalProject).

## Table of contents
1. [Introduction](#introduction)
    1. [Industry Choices](#subsec1-1)
2. [Methodology](#meth)
3. [Section 1](#section2)
    1. [Subsection](#subsec2-1)
    2. [Subsection](#subsec2-2)
4. [Section 1](#section3)
    1. [Subsection](#subsec3-1)
    2. [Subsection](#subsec3-2)
5. [Visualizations and Analysis](#section4)
    1. [Construction](#subsec4-1)
    2. [Manufacturing](#subsec4-2)
    3. [Finance](#subsec4-3)
6. [Findings and Conclusion](#conc)
7. [About the Team](#about)

## Introduction  <a name="introduction"></a>

The main goal of this project is to explore how we can use past data on industry trends and leading indicators to predict future employment and economic trends. We chose to explore this topic because, as we and our peers begin to move into the working world, we believe it is important to understand unemployment as it relates to job security. Especially now with many people predicting a recession, we think it is important to understand the employment trends in popular industries as they relate to economic trends.

### Why we chose these industries: <a name="industries"></a>

**Construction:** This was the inspiration for this project. While exploring topics, Tom stumbled upon this [video](https://www.youtube.com/watch?v=roEljzOKk3I&ab_channel=EPBResearch), detailing how the constuction employment is a significant driver of recessions in the US economy. We originally wanted to explore how different industries drive recessions, but we later decided to switch the angle in which we approached the project, instead researching how economic conditions affect unemployment in different industries. We felt that we should keep the construction industry as a homage to our original inspiration for the project.

**Manufacturing:** As supply chain majors, the manufaturing industy is important to Tim and Tom. Additionally, it is an industry that is very relevant to recent and soon-to-be Lehigh graduates overall.

**Finance:** This one is pretty clear. Since this is a finance class, most of us students are finance majors, and will likely be entering the finance industry soon. Therefore, it is important to understand the potential impact that economic conditions will have on employment rates.

## Methodology <a name="meth"></a>

We began by gathering data. We were able to find most of the employment data we needed from the Bureau of Labor Statistics and the Bureau of Economic Analysis. This was convient because, by getting the data from the same/similar sources, they were all formatted similarly. Therefore, there was minimal work needed to clean the data and prepare it for a merge.

Then, we were able to complete the minimal cleaning of the data so it was ready to merge, then merge it. The merged dataframe can be seen below.

![](pics/Merged_df.png)
<br><br>
Some analysis here

Here is some code that we used to develop our analysis. Blah Blah. [More details are provided in the Appendix](page2).
 
Note that for the purposes of the website, you have to copy this code into the markdown file and  
put the code inside trip backticks with the keyword `python`.

```python
import seaborn as sns 
iris = sns.load_dataset('iris') 

print(iris.head(),  '\n---')
print(iris.tail(),  '\n---')
print(iris.columns, '\n---')
print("The shape is: ",iris.shape, '\n---')
print("Info:",iris.info(), '\n---') # memory usage, name, dtype, and # of non-null obs (--> # of missing obs) per variable
print(iris.describe(), '\n---') # summary stats, and you can customize the list!
print(iris['species'].value_counts()[:10], '\n---')
print(iris['species'].nunique(), '\n---')
```

Notice that the output does NOT show! **You have to copy in figures and tables from the notebooks.**

## Regression Analysis <a name="section2"></a>
Christyan

### Subsection 1 <a name="subsec2-1"></a>
This is a subsection, formatted in heading 3 style

### Subsection 2 <a name="subsec2-2"></a>
This is a subsection, formatted in heading 3 style

## Machine Learning Analysis <a name="section3"></a>

To further analyze the relationship on economic indicators to industry unemployment, we employed different methods of machine learning. Our goal was to train a model to most accurately predict a given level of unemployment in an industry based on certain economic conditions. 

 


### "ML" Method 1: <a name="subsec3-1"></a>
For our first attempt, we created a model that attempts to place a value based on the line best fit using the three variables. 

```python 

X = recession_df[['SP500_Return', 'Percent_Change_in_GDP', 'CPI']]
y = recession_df['Construction_Unemployment_Rate']

model = LinearRegression()
model.fit(X,y)

predictions = model.predict(X) 
recession_df['Predicted_Construction_Unemployment_Rate'] = predictions
```

Since this model does not use any learning of test data. It turns out that it is not that accurate. 

| Industry     | R<sup>2</sup>         |
|--------------|------------|
| Construction | 0.208536   |
| Manufacturing        | 0.222904   |
| Finance          | 0.223606   |


### ML Method 2 <a name="subsec3-2"></a> 


To create a better model for each industry, we used training and testing samples of 70% and 30% of our dataset. We also included a num and cat transformer into the model as well as did preprocessing. 

The code below shows an example of one of our models that outputs the R<sup>2</sup> score, the industry predictions, and the length of the training data:

```python 

X_train_c, X_test_c, y_train_c, y_test_c = train_test_split(
    merged.drop('Construction_Unemployment_Rate', axis=1),
    merged['Construction_Unemployment_Rate'],
    test_size=0.3,
    stratify=merged['Year']
) 

num_transformer = Pipeline(steps=[
    ('scaler', StandardScaler())
])

cat_transformer = Pipeline(steps=[
    ('onehot', OneHotEncoder(handle_unknown='ignore'))
]) 

#Preprocessor
preprocessor = ColumnTransformer(transformers=[
    ('num', num_transformer, ['SP500_Return', 'Percent_Change_in_GDP', 'CPI']),
    ('cat', cat_transformer, ['Year', 'Period'])
]) 

#Define the model as a pipeline of the preprocessor/linear regression model
model_c = Pipeline(steps=[
    ('preprocessor', preprocessor),
    ('regressor', LinearRegression())
]) 

#Train on training data
model_c.fit(X_train_c, y_train_c)

# Predict on the testing data
y_pred_c = model_c.predict(X_test_c)

# Evaluate the model
score_c = model_c.score(X_test_c, y_test_c)
print(f'R^2 score: {score_c}') 

print(y_pred_c)
len(X_train_c)
``` 

This model gave us a much better estimate of unemployment by industry. The highest R<sup>2</sup> was for construction, which supported our intial idea that the construction industry is heavily tied to economic indicators. 

| Industry | R<sup>2</sup> |
|:--------:|:-------------:|
| Construction | 0.8545 |
| Manufacturing | 0.5891 |
| Finance | 0.7938 |




## Plots and Visualization <a name="section4"></a>

To visualize the accuracy of machine learning, we used a scatterplot, a density plot, and a residual plot. These plots all compare the predicted results from our machine learning model to the actual data from our dataset.

### Construction <a name="subsec4-1"></a>

![](pics/scatter_constr.png)
<br><br>
This plot shows how our predicted values for the unemployment (red) correlate with the actual values in the dataset (blue).
<br><br>
![](pics/density_constr.png)
<br><br>
This plot overlays our predicted values for the unemployment (orange) with the actual values in the dataset (blue), showing how closely they correlate.
<br><br>
![](pics/residual_constr.png)
<br><br>
This plot shows how far our predicted values for the unemployment deviate from the actual values in the dataset, with the red line representing 0, or no deviation from eachother. This plot is useful because it additionally colors the points by the timeframe, so we can see which timeframes we predicted more accurately than others.

### Manufacturing <a name="subsec4-2"></a>

![](pics/scatter_manuf.png)
<br><br>
This plot shows how our predicted values for the unemployment (red) correlate with the actual values in the dataset (blue).
<br><br>
![](pics/density_manuf.png)
<br><br>
This plot overlays our predicted values for the unemployment (orange) with the actual values in the dataset (blue), showing how closely they correlate.
<br><br>
![](pics/residual_manuf.png)
<br><br>
This plot shows how far our predicted values for the unemployment deviate from the actual values in the dataset, with the red line representing 0, or no deviation from eachother. This plot is useful because it additionally colors the points by the timeframe, so we can see which timeframes we predicted more accurately than others.

### Finance <a name="subsec4-3"></a>

![](pics/scatter_fin.png)
<br><br>
This plot shows how our predicted values for the unemployment (red) correlate with the actual values in the dataset (blue).
<br><br>
![](pics/density_fin.png)
<br><br>
This plot overlays our predicted values for the unemployment (orange) with the actual values in the dataset (blue), showing how closely they correlate.
<br><br>
![](pics/residual_fin.png)
<br><br>
This plot shows how far our predicted values for the unemployment deviate from the actual values in the dataset, with the red line representing 0, or no deviation from eachother. This plot is useful because it additionally colors the points by the timeframe, so we can see which timeframes we predicted more accurately than others.

## Findings and Conclusion <a name="conc"></a>

**Our final R<sup>2</sup> values are as follows:**

| Industry | R<sup>2</sup> |
|:--------:|:-------------:|
| Construction | 0.8545 |
| Manufacturing | 0.5891 |
| Finance | 0.7938 |

These values are clear in the plots: 

The construction industry has the highest R<sup>2</sup>, and that can be seen through the close correlation between the actual values and our predicted values.

For the manufacturing industry, you can see that there are certain outliers in the actual data that deviate from our predicted results. This can be seen specifically in the scatterplot and the residual plot.

The scatterplot and the residual plot for the finance industry seem to show actual values that deviate significantly from our predicted values, but by looking at the density plot, you can see that the values are closer to eachother than they seem.

Finally, we created a new dataset with randomly generated values for the S&P500 return, change in GDP, and CPI from 2023 to 2033. I created code that ensured those variables stayed within specified values, and that they somewhat correlated with each other as they do in reality. The code that I used to do this is as follows:

```python
# random numbers for 10 years

np.random.seed(1234)

# create list of periods
periods = ['Q01', 'Q02', 'Q03', 'Q04']

# create empty df
data_random_10 = pd.DataFrame(columns=['Year', 'Period', 'SP500_Return', 'Percent_Change_in_GDP', 'CPI'])

# create columns
years = np.repeat(np.arange(2023, 2033), 4)
data_random_10['Year'] = years
data_random_10['Period'] = periods*10

n_quarters = len(years)
data_random_10['SP500_Return'] = np.random.uniform(low=-0.18, high=0.21, size=n_quarters)
data_random_10['Percent_Change_in_GDP'] = np.random.uniform(low=-20, high=25, size=n_quarters)
data_random_10['CPI'] = np.random.uniform(low=200, high=320, size=n_quarters)

data_random_10['Percent_Change_in_GDP'] = data_random_10['Percent_Change_in_GDP'] * (1 + 0.5*data_random_10['SP500_Return'])
data_random_10['CPI'] = data_random_10['CPI'] * (1 + 0.3*data_random_10['SP500_Return'])

data_random_10 = data_random_10.round(2)
data_random_10
```

Now that I created that dataset, I trained our model that we used before on all of the original dataset, to give it the largest sample size possible. Then, I was able to predict unemployment rates for each industry for these randomly generated variables all the way up to 2033. The dataset with the predicted unemployment rates on the randomized values:

![](pics/random_predictions.png)
<br><br>

## About the team <a name="about"></a>

<img src="pics/IMG_7083 (1).jpg" alt="Tim" width="300"/>
<br>
Tim is a junior at Lehigh studying finance and supply chain management.
<br><br>
<img src="pics/IMG-0006.jpg" alt="Tom" width="300"/>
<br>
Tom is a junior at Lehigh studying finance and supply chain management.
<br><br>
<img src="pics/IMG-3108 (1).jpg" alt="Christyan" width="300"/>
<br>
Christyan is a senior at Lehigh studying finance.
<br><br>

## More 

To view the GitHub repo for this website, click [here](https://github.com/donbowen/teamproject).
