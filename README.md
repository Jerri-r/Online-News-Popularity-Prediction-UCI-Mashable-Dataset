# AN6003‑News‑Popularity‑Prediction
Predict news article sharing potential under limited promotion resources

## Project Overview
This is a group course assignment for AN6003. Faced with a hypothetical business challenge of limited promotion budget, this project uses the UCI Mashable Online News dataset to forecast whether an article will become popular (defined as article shares > 1400).

The full workflow includes business problem definition, data cleaning, time‑ordered train‑validation‑test dataset split, exploratory data analysis, model building, benchmark comparison against random guess baseline, and practical editorial promotion recommendations. Three classification models are implemented: Logistic Regression, CART Decision Tree and Random Forest.

## My Contribution: CART Decision‑Tree Model
Existing exploratory analysis told us which variables correlate with article popularity, but did not answer practical questions: what are the critical threshold values for metrics? How should multiple features be weighted and combined for prediction? The CART model was introduced to resolve these gaps by automatically discovering optimal split thresholds and feature combinations.

### Model logic
CART operates through a sequence of yes‑no decision questions. Starting from 48 raw input features, the algorithm selects features and split points recursively to classify articles as either popular or non‑popular. Not all input features are utilised; only 45 candidate features are actually engaged during tree construction.

### Pruning for overfitting mitigation
A fully‑grown decision tree tends to memorise noise and outliers in the training set, resulting in poor generalisation.
I applied **cost‑complexity pruning**:
1. Train the full tree on the training dataset.
2. Use the validation set to identify the optimal complexity parameter (CP).
3. Remove redundant tree branches that bring no improvement in validation performance.
After pruning, effective candidate features were reduced from 45 to 25.
The held‑out test set was used for final unbiased performance verification.

### Feature importance & key predictors
Feature importance analysis reveals the top‑five most influential drivers for news popularity:
1. **Channel**: The category which the article belongs to
2. **kw_avg_avg**: Average share statistics of article keywords
3. **LDA_04**: Latent topic grouping of articles
4. **kw_max_avg**: Maximum share statistics of article keywords
5. **is_weekend**: Whether published on Saturday or Sunday

### CART Model Test‑set Performance
- Baseline random‑guess precision: 43.5%
- CART precision: **61.70%**
- CART prediction accuracy: **65.70%**

Compared with random guessing, CART delivers substantial improvement in identifying potentially popular articles. Note that this project prioritises precision: it measures how many articles flagged as popular are genuinely popular, which directly guides promotion resource allocation.

## Dataset
> UCI Machine Learning Repository: Online News Popularity Data Set
- Total cleaned articles: 39643
- Popular definition: article shares > 1400
- Split strategy: time‑ordered non‑overlapping train / validation / test sets

## Overall Project Key Results
- Random baseline precision: 43.5%
- CART precision: 61.70%
- Logistic Regression precision: 61.95%
- Random Forest precision: 62.25% (best‑performing model)
- Random Forest achieves the highest overall accuracy, nearly doubling the hit rate when selecting the top‑20% articles for promotion.

## Repository Content
