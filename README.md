# Used_Vehicles
What Drives (pun intended) the Price of a Used Car?
Applying the CRISP-DM framework to answer the question: What factors make a car more or less expensive? 

## Business Understanding 
The objective is to analyze the determinants of car pricing and consumer preferences in the used car market. Through this exploration, I aim to provide valuable insights for industry stakeholders navigating this dynamic landscape.

The key objective to generating high car prices is to increase profitablity to a used car dealership.  This can be accomplished through several mechanisms: 
- Higher prices directly increase the revenue generated from each sale, leading to higher profit margins while operational overhead costs stay constant. Additionally, - Higher prices can create a perception of value and quality among customers, commanding premium prices for its inventory. 
- Increased profitability from higher prices can enable the dealership to invest in marketing, customer service, and inventory expansion, further solidifying its competitive position in the market.

## Data Understanding
From an original dataset containing information on 3 million used cars the dataset I’m working with has 426,880 rows with 18 columns or features that are numeric, categorical, and unstructured objects.
### Data Understanding and Features Related to the Business

- While the average price of a car may vary slightly from one geographic region or state to another, an owner of a used car dealership cannot easily relocate they dealership.  For this reason, the “region” and “state” columns will not be useful to this analysis. 
- Some vehicle “types” which are not likely to be sold at a used car dealership such as "offroad", "bus", "other" were removed.  
- After analysing the uniques values of the column "title_status" I've determining that car dealers will only be interested in cars with "clean" as the “title_status” since all other title status such as salvage or for-parts would identify cars that a used car dealer will not have on their lot nor sale.  These should be removed.  
- 28724 unique “models” indicating unstructured data.  I see that the key model description is found in the first word of this field.  By removed extra words to reduce to 4976 unique models. This is stil too many unique values to be useful in the analysis and data models.  
  - Encoding a feature with over 4000 unique values into categorical variables might not be the most effective approach in many cases due to several reasons:
    - High Cardinality: Having over 6000 unique values implies high cardinality, which can lead to a significant increase in dimensionality after encoding. This can make the dataset computationally expensive to process and may cause issues such as the curse of dimensionality.
    - Sparsity: High cardinality features often result in sparse matrices after one-hot encoding. This means that most of the encoded features will be zeros, leading to inefficiency in terms of memory usage and computational resources.
    - Model Complexity: Including a large number of one-hot encoded features may lead to overfitting, especially if the number of samples in the dataset is limited compared to the number of features.

## Data Preparation and Visulalization
<pre>
Code Used: Python
Packages: Pandas, plotly, matplotlib, seaborn
</pre>

Explored the unique values, counts, and null values for all features
- All NaN values in the 'condition' column have been replaced with 'good'  (170, 204)
- Count of 'salvage' values in 'condition' column: 225 - I will remove these rows
- Alot of values are missing in “drive” and does not account for all-wheel-drive and have two values for 4wd and fwd.  Since it is missing 130k values I will remove this column
-Transmission.  78.5% are automatic.  0.62 % is Nan values.  This column does not appear to provide distinguishable insights that would determine price. 
- Paint_color is missing 126,383.  I attempted to replace null values with car paint colors that tends to be price-neutral, such as white, black, silver, and gray are typically good choices. Since there is still high demensionality in the dataset and color does not significantly drive a high price, this column was removed. 
- Size is missing 72% and Cylinders is missing 42% of the vales.  Remove the Cylinder column.  Keep Size and remove missing rows.
- These tactics of dealing with Nan values is comparable to replacing with a mean value. 
- Filter rows where 'title_status' column contains 'clean' then removed the column since all values in the column are the same: 'clean'
- Rows with missing price, many rows with unbelievable car prices either too high (above $150,000 or too low, under $4,000)

## Data Processing and Modeling
<pre>
Code Used: Python
Packages: Pandas, sklearn, numpy, scipy
Instructions: Please run the notebook in sequence
<<Notebook link>>
</pre>

The goal was to acheive predictive optimization through the utilization of various multiple regression models, including:

- Conducting cross-validation on models
- Performing grid search to optimize hyperparameters
- Interpreting coefficients in models accurately
- Understanding and interpreting evaluation metrics appropriately
- Identifying the chosen evaluation metric
- Providing a clear rationale for the selection of the evaluation metric.

### Next steps and recommendations

More important that car price is profitability or realizing a higher price for a car in relation to the average expectation for that car.  
While an expensive car does not guarantee a more profitable car, we will assume or accept that a car at a higher price will bring in more revenue that cars at a lower price.  We will try to keep all other factors constant. This will still tell us which cars a customer will value based on the fact that they are willing to pay a higher price for it. 

Future exploration: Including time on the lot or number of days til sold would be a good indicator of a cars demand.  A higher demand will drive up price.  Shorter days on the lot will reduce overhead and increase in car volumn will result in increase profits. 








To simplify things,  I eliminate the columns containing object datatypes. I Dropping non-informative columns then saved a copy of the data set to run comparisons.

