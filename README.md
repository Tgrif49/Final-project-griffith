# Welcome to our team project website!

This is a website to showcase our final project for FIN 377 - Data Science for Finance course at Lehigh University.

This project and website was created by Tim DiPalo, Tom Griffith, and Christyan Jean-Charles.

To see the complete project repo, click [here](https://github.com/tdip19/FinalProject).

## Table of contents
1. [Introduction](#introduction)
2. [Methodology](#meth)
3. [Section 2](#section2)
    1. [Subsection](#subsec2-1)
    2. [Subsection](#subsec2-2)
4. [Analysis Section](#section3)
5. [Summary](#summary)

## Introduction  <a name="introduction"></a>

The main goal of this project is to explore how we can use past data on industry trends and leading indicators to predict future employment and economic trends. We chose to explore this topic because, as we and our peers begin to move into the working world, we believe it is important to understand unemployment as it relates to job security. Especially now with many people predicting a recession, we think it is important to understand the employment trends in popular industries as they relate to economic trends.

Why we chose these industries:

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

## Machine Learning Analysis <a name="section2"></a>
Christyan

### Subsection 1 <a name="subsec2-1"></a>
This is a subsection, formatted in heading 3 style

### Subsection 2 <a name="subsec2-2"></a>
This is a subsection, formatted in heading 3 style

## Plots and Visualization <a name="section3"></a>

Here are some graphs that we created in our analysis. We saved them to the `pics/` subfolder and include them via the usual markdown syntax for pictures.

![](pics/plot1.png)
<br><br>
Some analysis here
<br><br>
![](pics/plot2.png)
<br><br>
More analysis here.
<br><br>
![](pics/plot3.png)
<br><br>
More analysis.

## Summary of Findings <a name="summary"></a>

Blah blah



## About the team
<img src="pics/IMG_7083 (1).jpg" alt="Tim" width="300"/>
<br>
Tim is a junior at Lehigh studying finance and supply chain management.
<br><br><br>
<img src="pics/IMG-0006.jpg" alt="Tom" width="300"/>
<br>
Tom is a junior at Lehigh studying finance and supply chain management.
<br><br><br>
<img src="pics/IMG-3108 (1).jpg" alt="Christyan" width="300"/>
<br>
Christyan is a senior at Lehigh studying finance.


## More 

To view the GitHub repo for this website, click [here](https://github.com/donbowen/teamproject).
