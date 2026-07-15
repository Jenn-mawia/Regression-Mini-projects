# Tips Analysis — Predicting Restaurant Tips

This project looks at the classic tips dataset (244 restaurant bills) to
answer a simple question: what are the predictors of the size of a tip and can we predict
it from the bill?

## The data

- The data contains rows of restaurant meals. Each row represents one meal, with the total bill, the amount of tip, the sex of the person paying the bill, whether they smoke or do not smoke, the day of the week, the time of the day(lunch or dinner) and the total number of people that ate at the restaurant. 

> - The data did not have missing values. 
  - Only one duplicate row was found but since there was no unique ID to tell the two entries apart, it was kept rather than dropped. 

## Cleaning and outliers

Outliers were checked using the IQR rule. 
- A few large bills and tips sit outside the usual range, but with only 244 rows, removing them would shrink the dataset too much for training, so they were kept.

## Data analysis and exploration results

- Total bill and tip are both skewed to the right — most meals are modest, with a handful of big spenders stretching the tail.
- The sample data is imbalanced: more men than women, more non-smokers than smokers, and more dinners than lunches.
- The scatter plots and correlation matrix show a clear positive relationship between the total bill and the tip (correlation 0.68). Party size also moves with the tip (0.49), though bigger parties also run up bigger bills.

## Modeling

The categorical columns were one-hot encoded before modeling, then a linear regression was
trained on 75% of the data and tested on the remaining 25%.

**Performance on the test set:**

- RMSE: 0.93 — the model's predictions are off by about $0.93 on average
- R²: 0.35 — the model explains roughly a third of the variation in tips

That's a reasonable result for such a small dataset. 

## What matters most

- Looking at the model's coefficients, party **size**(total number of people that ate in a single bill) has the largest single coefficient: each extra person at the table adds about $0.21 to the
predicted tip, holding everything else constant. 
- Non-smokers and Friday meals are associated with slightly higher tips and men tip marginally
more than women.

The total bill's coefficient looks small (about $0.10 per dollar) because
it is measured per dollar rather than per person or per category — but since
bills vary far more than any other feature, it carries the strongest overall
relationship with tips in the data. In plain terms: tips grow steadily with
the bill (roughly 10 cents per extra dollar) and larger parties(group sizes) add a
little more on top.

## Conclusion

- Tips in this dataset are mostly a story about the bill(**total amount paid**) and the party/group **size**:bigger bills and bigger tables mean bigger tips. 
- Who is paying(male or female), whether they smoke and when they eat(lunch or dinner) make only small differences once the bill is accounted for.