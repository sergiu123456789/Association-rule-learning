# Market Basket Analysis with Apriori

This project applies the **Apriori algorithm** to identify frequent itemsets and association rules from customer purchase data.  
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

⚙️ Steps

Read the Transaction Data

Load CSV file containing product purchases.

Data Transformation

Convert each transaction into a list of products.

Prepare data for the Apriori algorithm.

Apply the Apriori Algorithm

Find frequent itemsets with a given minimum support.

Example: support threshold = 0.5 means the itemset must appear in at least 50% of transactions.

Generate Association Rules

Rules are generated with a minimum confidence level.

Example: milk → bread with confidence 0.8 means 80% of transactions containing milk also contain bread.

Output Predictions

The most likely product combinations are listed, along with their support, confidence, and lift.

🖥️ Example Python Code

import numpy as np
import matplotlib.pyplot as plt
import pandas as pd

# Apply Apriori & Generate rules
from apyori import apriori
rules = apriori(transactions = transactions, min_support = 0.003, min_confidence = 0.2, min_lift = 3, min_length = 2, max_length = 2)

# Putting the results well organised into a Pandas DataFrame

def inspect(results):
    lhs         = [tuple(result[2][0][0])[0] for result in results]
    rhs         = [tuple(result[2][0][1])[0] for result in results]
    supports    = [result[1] for result in results]
    confidences = [result[2][0][2] for result in results]
    lifts       = [result[2][0][3] for result in results]
    return list(zip(lhs, rhs, supports, confidences, lifts))
resultsinDataFrame = pd.DataFrame(inspect(results), columns = ['Left Hand Side', 'Right Hand Side', 'Support', 'Confidence', 'Lift'])

Frequent Itemsets:
   support        itemsets
0     0.75       (bread)
1     0.75        (milk)
2     0.50       (butter)
3     0.50   (bread, milk)
4     0.50  (milk, butter)

Association Rules:
   antecedents consequents  support  confidence      lift
0     (milk)     (bread)     0.50       0.80     1.07
1    (bread)     (milk)      0.50       0.75     1.07
2    (milk)    (butter)     0.50       0.67     1.33

📌 Interpretation

Support: How often the itemset appears in transactions.

Confidence: How often the rule is correct (given the antecedent, how often is the consequent also purchased).

Lift: How much more likely the consequent is purchased when the antecedent is present, compared to random chance.

Example:
(milk) → (bread) with confidence 0.80 means:
80% of the time milk is purchased, bread is purchased too.

🚀 Applications

Product placement in stores.

Cross-selling recommendations in e-commerce.

Targeted promotions.

📚 Requirements

!pip install apyori
