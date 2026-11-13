# Concrete Compressive Strength Prediction

Predicting concrete compressive strength (MPa) from mix proportions and curing age using machine learning.

## Dataset
UCI Concrete Compressive Strength dataset: 1,030 samples, 8 input features
(cement, slag, fly ash, water, superplasticizer, coarse aggregate, fine aggregate, age).

## Approach
1. Explored the data (shape, types, missing values, ranges).
2. 80/20 train-test split (random_state=42).
3. Baseline: Linear Regression.
4. Feature engineering: water-cement ratio (Abrams' law) and log(age).
5. Random Forest (200 trees) and 5-fold shuffled cross-validation.
6. Error analysis by age band and feature importance.

## Results (held-out test set)
| Model | R2 | RMSE (MPa) |
|---|---|---|
| Linear Regression, raw features | 0.628 | 9.80 |
| Linear Regression, + engineered features | 0.833 | 6.56 |
| Random Forest, raw features | 0.881 | 5.53 |
| Random Forest, + engineered features | 0.888 | 5.38 |

5-fold shuffled CV (Random Forest): mean R2 = 0.906 +/- 0.014.

## Key findings
- Engineered features raised Linear Regression R2 from 0.63 to 0.83; Random Forest gained little (0.881 to 0.888), likely because trees learn non-linearity themselves.
- Water-cement ratio was the most important feature, consistent with Abrams' law.
- Error was highest for 7-28 day mixes (MAE about 4.2 MPa) and lowest for 90+ days (about 2.9 MPa).
- The dataset is ordered: CV without shuffling gave an unstable fold (negative R2), fixed with shuffled K-fold.

## Limitations
- The dataset may contain the same mix tested at several ages, so a random split can be optimistic. A group-based split was not tested.
- Lab data may not transfer to site conditions.

## How to run
Open `concrete_strength_prediction.ipynb` in Google Colab and run all cells.
