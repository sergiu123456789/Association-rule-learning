# Market Basket Analysis with Eclat

This project applies the **Eclat algorithm** to identify frequent itemsets and association rules from customer purchase data.  
It predicts **product combinations** that are most likely to appear together based on historical transactions.

---

## 📂 Input Data

The input file contains transactions where each row corresponds to the items bought by a single customer.  
Example (`transactions.csv`):

```csv
milk,bread,butter
bread,eggs
milk,bread
milk,bread,butter,eggs
``` 
## ⚙️ Steps

Read the Transaction Data

Load CSV file containing product purchases.

Data Transformation

Convert each transaction into a list of products.

Prepare data for the Eclat algorithm.

Apply the Eclat Algorithm

Find frequent itemsets with a given minimum support.

Example: support threshold = 0.5 means the itemset must appear in at least 50% of transactions.

Output Predictions

The most likely product combinations are listed, along with their support

## 🖥️ Example Python Code
```python
import numpy as np
import matplotlib.pyplot as plt
import pandas as pd
```
# Apply Eclat & Generate rules
```python
transactions = []
for i in range(0, 7501):
  transactions.append([str(dataset.values[i,j]) for j in range(0, 20)])
from apyori import apriori
rules = apriori(transactions = transactions, min_support = 0.003, min_confidence = 0.2, min_lift = 3, min_length = 2, max_length = 2)
results = list(rules)
```
# Putting the results well organised into a Pandas DataFrame
```python
def inspect(results):
    lhs         = [tuple(result[2][0][0])[0] for result in results]
    rhs         = [tuple(result[2][0][1])[0] for result in results]
    supports    = [result[1] for result in results]
    return list(zip(lhs, rhs, supports))
resultsinDataFrame = pd.DataFrame(inspect(results), columns = ['Product 1', 'Product 2', 'Support'])
```
Frequent Itemsets:
```csv
   support        itemsets
0     0.75       (bread)
1     0.75       (milk)
2     0.50       (butter)
3     0.50       (bread, milk)
4     0.50       (milk, butter)
```
Association Rules:
```csv
   antecedents consequents  support 
0    (milk)     (bread)      0.50      
1    (bread)     (milk)      0.50      
2    (milk)     (butter)     0.50      
```
## 📌 Interpretation

Support: How often the itemset appears in transactions.

## 🚀 Applications

Product placement in stores.

Cross-selling recommendations in e-commerce.

Targeted promotions.

## 📚 Requirements

!pip install apyori
