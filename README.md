# Multicollinearity-between-Beta-and-Volatility

## 1. Introduction
The problem of multicollinearity in financial modeling, especially in the context of style factors, can lead to numerical instability, distorted factor loadings, and inflated variance inflation factors (VIF). In our case, we aim to analyze the relationship between two specific style factors: beta (market sensitivity) and volatility.

Beta and volatility often exhibit a degree of correlation due to their shared sensitivity to market movements, which can make them partially redundant. As per the provided context, our goal is to orthogonalize volatility relative to beta to mitigate this multicollinearity while retaining useful information unique to each factor.

## 2. Data Collection
We used historical data for Tesla, Inc. (TSLA) as the asset of interest due to its high market sensitivity and inherent volatility. This choice is strategic, as Tesla’s behavior is highly responsive to broader market movements, particularly the S&P 500 (SPX), which serves as our market benchmark. Data for TSLA and SPX was retrieved from Yahoo Finance for the period from January 2020 to January 2023.

## 3. Methodology
   
### Step 1: Calculate Rolling Beta and Volatility

To capture the dynamic relationship between beta and volatility over time, we employed a 60-day rolling window to calculate both metrics:
- Beta: Calculated by regressing TSLA returns on SPX returns within each window, reflecting Tesla’s sensitivity to the market.
- Volatility: Calculated as the standard deviation of TSLA’s returns within each window, representing the asset’s inherent risk over that period.

### Step 2: Check for Multicollinearity

We calculated the correlation between beta and volatility and also computed the Variance Inflation Factor (VIF) to quantify multicollinearity:
- A high VIF (> 5) typically indicates multicollinearity, which can destabilize regression models.
- A positive or strong correlation would suggest redundancy in capturing market exposure through both factors.

### Step 3: Orthogonalization of Volatility

To remove multicollinearity while preserving unique information, we orthogonalized volatility by regressing it on beta and using the residuals as the new orthogonalized volatility. This approach ensures that the orthogonalized volatility is uncorrelated with beta, allowing us to include both factors without redundancy.

## 4. Results
### Initial Correlation and VIF Analysis
-The correlation between Beta and Volatility was found to be 0.36, which is moderate but enough to suggest some multicollinearity.
-The VIF values for beta and volatility were approximately 1.15, indicating low multicollinearity overall. However, this could still impact interpretability in more sensitive models.
### Post-Orthogonalization Analysis
-After orthogonalizing volatility, the correlation between Beta and Orthogonalized Volatility was effectively reduced to 0.00, confirming that orthogonalization successfully removed the linear dependence between the two variables.
-The orthogonalized volatility metric represents the component of volatility that is not captured by beta, thus preserving distinct information about the asset’s behavior.

## 5. Visual Analysis
   
### 1. Original Volatility vs. Beta
Purpose: This scatter plot with a trendline shows the relationship between the original volatility and beta of Tesla over rolling windows.
Key Observations:
- There’s a positive correlation of 0.36 between beta and volatility in this dataset. This positive slope indicates that higher beta values (which represent market sensitivity) are generally associated with higher levels of volatility.
- The red trendline reinforces this upward trend, demonstrating a direct relationship between the two variables.
  
Conclusion: 
The presence of this correlation hints at multicollinearity, which means that volatility and beta share some common information. This multicollinearity can make it challenging to separate the effects of each factor when building predictive models.

### 2. Orthogonalized Volatility vs. Beta
Purpose: This scatter plot shows the relationship between beta and orthogonalized volatility (i.e., volatility with the linear effect of beta removed).
Key Observations:
- After orthogonalization, the correlation between beta and volatility drops to -0.00, which is essentially zero.
- The trendline here is almost flat, indicating no linear relationship between beta and orthogonalized volatility.
- The points are more evenly distributed around the trendline, which supports the notion that we have effectively removed the shared variation.
Conclusion:
Orthogonalization successfully eliminates the multicollinearity issue, allowing volatility to represent purely idiosyncratic volatility not explained by beta.

### 3. Overlay of Original and Orthogonalized Volatility vs. Beta
Purpose: This chart overlays the original and orthogonalized volatilities against beta, allowing for a direct visual comparison.
Key Observations:
- The blue dots represent original volatility, while the green dots represent orthogonalized volatility.
- Original volatility (blue) shows a clear upward trend with increasing beta values, while orthogonalized volatility (green) appears scattered, without a visible trend.
Conclusion: This overlay highlights the impact of orthogonalization in separating volatility’s dependence on beta. Original volatility is highly affected by beta changes, while orthogonalized volatility remains unaffected, reinforcing that orthogonalization removes the influence of beta.

### 4. Histogram of Orthogonalized Volatility
Purpose: This histogram visualizes the distribution of orthogonalized volatility values.
Key Observations:
- The histogram is centered around zero, with a symmetrical distribution.
- The presence of values on both sides of zero indicates that orthogonalized volatility fluctuates around a mean of zero, suggesting no inherent bias toward positive or negative values after removing beta’s influence.
Conclusion: The histogram shows that orthogonalized volatility now represents only the unique portion of volatility that’s unrelated to beta. This new variable is uncorrelated with market sensitivity and can be used independently in models without risking multicollinearity.

### 5. Distribution of Original vs. Orthogonalized Volatility
Purpose: This histogram compares the distributions of original and orthogonalized volatilities.
Key Observations:
- Original Volatility (blue) has a distribution skewed toward higher values, aligning with its correlation with beta.
- Orthogonalized Volatility (green), on the other hand, is more centered and has less variability.
- The original distribution indicates that market factors influence it, while the orthogonalized distribution shows reduced spread, as it no longer captures market sensitivity.
Conclusion: This comparison underscores the effect of orthogonalization, which reduces variability and removes market-related volatility, leaving behind the unique, idiosyncratic component.

### Summary
These plots collectively illustrate the concept of multicollinearity between beta and volatility and how orthogonalization can resolve it:
1. Original Volatility and Beta are positively correlated, indicating multicollinearity.
2. Orthogonalized Volatility removes this relationship, effectively isolating the unique component of volatility.
3. The overlay and distribution plots demonstrate that orthogonalized volatility is uncorrelated with beta and can be used as an independent variable in statistical or financial models, avoiding redundancy and improving model stability.
This process is valuable for refining factor models, allowing you to use each variable independently without overestimating the effect of one due to the influence of the other.


## 7. Conclusion
This analysis demonstrates the value of orthogonalizing style factors to address multicollinearity. By removing the dependency between beta and volatility, we ensure that both factors can be included in a regression or factor model without redundancy, preserving their unique contributions to the model.
The orthogonalized volatility metric now captures the idiosyncratic risk component of Tesla that is not explained by its market sensitivity (beta), thus enabling a clearer interpretation of the impact of each factor.
This approach aligns with the principles discussed in the original text, showing that orthogonalization can be an effective strategy to manage multicollinearity among style factors without losing valuable information.

