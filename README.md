# Predicting Housing Prices Using PCA and Linear Regression

## Overview

This project explores the combination of Principal Component Analysis (PCA) and Linear Regression to model and predict housing prices. Housing datasets often contain multiple interrelated variables—such as square footage, number of bedrooms, and proximity to the city—that may introduce multicollinearity into models and degrade interpretability. PCA helps solve this by transforming the original variables into a smaller set of orthogonal components that retain most of the original information.

Once PCA is applied and the essential variance is preserved, a linear regression model is built using these principal components to predict housing prices. This ensures that the predictive model is not only statistically sound but also computationally efficient and interpretable. The approach aligns with real-world decision-making needs in urban planning, property investment, and real estate analytics.

---

## Project Objectives

- **Primary Goal**: To accurately predict property prices using PCA-transformed features and assess the viability of using a reduced-dimensionality feature space in regression modeling.
- **Use Case**: Provide an efficient modeling framework for real estate professionals and data scientists who work with complex, high-dimensional property datasets.
- **Methodology**: This project involves data preparation, exploratory analysis, standardization, PCA transformation, selection of components, model development with Ordinary Least Squares (OLS), evaluation with MSE/R², and interpretation of results and coefficients.

---

## Research Question

How many principal components are necessary to retain at least 90% of the variance in housing data, and can those components be used to build an accurate linear regression model for predicting housing prices?

---

## Dataset Summary

The dataset contains 7,000 records of residential properties. The analysis focuses on seven continuous variables:

- **SquareFootage**: Total interior floor area
- **NumBathrooms**: Total number of bathrooms
- **NumBedrooms**: Total number of bedrooms
- **BackyardSpace**: Available outdoor area in square feet
- **CrimeRate**: Local crime index
- **SchoolRating**: Average school quality rating in the area
- **DistanceToCityCenter**: Travel distance to the nearest city center in km

These variables cover both structural characteristics and environmental influences on property value.

### Descriptive Statistics

Each variable was analyzed to understand its range, central tendency, and distribution.

| Variable           | Mean     | Std Dev | Min   | Max    | Mode     |
|--------------------|----------|---------|-------|--------|----------|
| SquareFootage      | 1048.95  | 426.01  | 550   | 2874.7 | 550.0    |
| NumBathrooms       | 2.13     | 0.95    | 1     | 5.81   | 1.0      |
| NumBedrooms        | 3.01     | 1.02    | 1     | 7      | 3.0      |
| BackyardSpace      | 511.51   | 279.93  | 0.39  | 1631.4 | 300.08   |
| CrimeRate          | 31.23    | 18.03   | 0.03  | 99.73  | 34.01    |
| SchoolRating       | 6.94     | 1.89    | 0.22  | 10.0   | 10.0     |
| DistanceToCityCenter | 17.48  | 12.02   | 0     | 65.2   | 8.29     |

The variables were all continuous and standardized prior to PCA.

---

## Data Preview

| Price      | SquareFootage | NumBathrooms | NumBedrooms | BackyardSpace | CrimeRate | SchoolRating | DistanceToCityCenter |
|------------|----------------|---------------|--------------|----------------|-----------|----------------|------------------------|
| 308850.12  | 1060.23        | 2.0           | 3            | 502.33         | 30.11     | 7.4            | 12.88                  |
| 194000.00  | 740.00         | 1.0           | 2            | 285.99         | 15.60     | 5.8            | 6.70                   |
| 612000.45  | 1820.67        | 4.0           | 5            | 790.45         | 42.12     | 9.2            | 24.25                  |

---

## PCA Summary

### Why PCA?

PCA was chosen to reduce the dimensionality of the dataset while retaining the majority of the variance. This helps improve computational efficiency, reduce overfitting, and eliminate multicollinearity among the predictors.

### Variance Explained

| Component | Variance Explained |
|-----------|--------------------|
| PC1       | 26.25%             |
| PC2       | 14.63%             |
| PC3       | 14.02%             |
| PC4       | 13.31%             |
| PC5       | 12.34%             |
| PC6       | 11.99%             |
| **Total** | **92.55%**         |

These six principal components were selected for regression modeling, capturing over 90% of the total variance.

---

## Regression Modeling

An Ordinary Least Squares (OLS) regression was performed using the six principal components to predict housing prices.

### Model Details

| Metric              | Value         |
|---------------------|---------------|
| R²                  | 0.5213        |
| Adjusted R²         | 0.5208        |
| F-statistic         | 1015.13       |
| p-value (F-stat)    | 0.0000        |
| MSE (Train Set)     | 10.96M        |
| MSE (Test Set)      | 10.57M        |

All independent variables (principal components) were statistically significant with p-values < 0.01.

---

## Final Model Equation (Simplified)

```
Price ≈ 308279 + 74008*PC1 + 7745*PC2 + 34782*PC3 + 3846*PC4 + 19469*PC5 + 13485*PC6
```

Each coefficient represents the effect of one standardized principal component on the predicted price. Since the components are uncorrelated and scaled, this improves interpretability and model stability.

---

## Tools and Technologies

- **Pandas / NumPy** – For handling and transforming tabular data
- **Scikit-learn** – Used for scaling, PCA, and train-test splitting
- **Matplotlib / Seaborn** – Visual tools for the scree plot and data distributions
- **Statsmodels** – Regression modeling and statistical summaries

---

## Insights and Interpretation

- **PCA Component Usefulness**: Each of the retained components made a meaningful contribution to price prediction.
- **Model Generalization**: MSE on training and test sets was closely aligned, suggesting no overfitting.
- **Practical Value**: This model is useful in scenarios where explainability and reduced complexity are prioritized.

---

## Limitations

- **Linear Assumptions**: OLS regression assumes linear relationships, which may not capture all dynamics of housing data.
- **Excluded Features**: The dataset used only continuous variables. Categorical features such as house type or condition could further improve predictions.
- **No Temporal Component**: The model does not consider changes in housing trends over time.

---

## Future Enhancements

- **Nonlinear Models**: Implement Random Forest or Gradient Boosting to capture complex patterns.
- **Feature Engineering**: Add interaction terms or composite indicators like price per square foot.
- **Regularization**: Use Ridge or Lasso regression to control for overfitting in higher-dimensional cases.
- **Integration of Categorical Data**: Include features like region, property type, or amenities.

---

## Conclusion

This project demonstrated the efficacy of using PCA as a preprocessing step for regression modeling. By compressing correlated housing features into principal components, the model retained over 92% of the original data’s variance and achieved strong predictive performance. This approach supports data-driven pricing and investment decisions in real estate while maintaining clarity and interpretability.

