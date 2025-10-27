---
share: true
---
2025-10-16  16:30
Tags:

```python
sns.pairplot(df, diag_kind='kde')
```

Helps visualize relationships and possible correlations between features.
![[Pasted image 20251016163302.png|Pasted image 20251016163302.png]]

### Define Features & Target

```python
X = df.drop('sales', axis=1)
# This is smart, just drop sales(y) you get all the features, instead of adding each one
y = df['sales']
```

###  Split Train/Test Data

```python
from sklearn.model_selection import train_test_split
X_train, X_test, y_train, y_test = train_test_split(
    X, y, test_size=0.3, random_state=101)
```

### Train the Model

```python
from sklearn.linear_model import LinearRegression
model = LinearRegression()
model.fit(X_train, y_train)
```

- The model “learns” coefficients ( \beta_0, \beta_1, \beta_2, \beta_3 )
    
- Fit is based only on training data!
    

## Evaluation on Test Set

###  Make Predictions

```python
test_predictions = model.predict(X_test)
```

![[Pasted image 20251016165743.png|Pasted image 20251016165743.png]]
```python
from sklearn.metrics import mean_absolute_error, mean_squared_error
MAE = mean_absolute_error(y_test, test_predictions)
MSE = mean_squared_error(y_test, test_predictions)
RMSE = np.sqrt(MSE)
```

> ✅ Lower MAE/MSE/RMSE → better fit  
> ⚠️ Compare to `df['sales'].mean()` for perspective.
> MAE compare to mean(sales)
> MSE RMSE is too large, meaning the data may have outliers

---

## Residual Analysis

**Residual = Actual – Predicted**
You need to use residual plot to test whether it meets the linear relationship.
It is the same as I was been taught in stats class! 4 assumptions of linearity
![[Pasted image 20251027221449.png|Pasted image 20251027221449.png]]
```python
test_residual = y_test - test_predictions

sns.scatterplot(x=y_test,y=test_residual)

plt.axhline(y=0,color='r',ls='--')
```

> Residuals should:
> 
> - Center around zero
>     
> - Have no clear pattern (homoscedasticity)
>     
> - Be approximately normal
>     

```python
sns.displot(test_residual,bins=25,kde=True)
```
![[Pasted image 20251027221511.png|Pasted image 20251027221511.png]]


You can check with a Q-Q plot:
![[Pasted image 20251027221820.png|Pasted image 20251027221820.png]]

```python
import scipy as sp
# Create a figure and axis to plot on

fig, ax = plt.subplots(figsize=(6,8),dpi=100)

# probplot returns the raw values if needed

# we just want to see the plot, so we assign these values to _

_ = sp.stats.probplot(test_residual,plot=ax)
```

---

## 8️⃣ Retrain on Full Data (Optional)

After confirming model performance:

```python
final_model = LinearRegression()
final_model.fit(X, y)
```

> This uses all data for the final version of the model before deployment.

---

## 9️⃣ Interpreting Coefficients

```python
coeff_df = pd.DataFrame(final_model.coef_, X.columns, columns=['Coefficient'])
```

|Feature|Coefficient|Interpretation|
|---|---|---|
|TV|+0.045|+$1000 in TV ads → +45 sales units|
|Radio|+0.188|+$1000 in Radio ads → +188 sales units|
|Newspaper|−0.001|Effect ≈ 0 (no real influence)|

> Always interpret coefficients _holding other variables constant._

---

## 🔟 Making Predictions

```python
campaign = [[149, 22, 12]]
final_model.predict(campaign)
```

> Output = expected sales (in 1000 units).  
> Model cannot tell certainty — only prediction based on past patterns.

---

## 11️⃣ Saving & Loading Models

```python
from joblib import dump, load
dump(final_model, 'sales_model.joblib')
loaded_model = load('sales_model.joblib')
loaded_model.predict(campaign)
```

Useful for deployment or reusing trained models later.

---

## 12️⃣ Summary Table

|Step|Purpose|Key Function|
|---|---|---|
|Split data|Prevent overfitting|`train_test_split`|
|Train model|Learn parameters|`LinearRegression().fit()`|
|Predict|Generate output|`.predict()`|
|Evaluate|Measure accuracy|`mean_absolute_error`, `mean_squared_error`|
|Analyze residuals|Check assumptions|`sns.displot`, `sp.stats.probplot`|
|Save model|Reuse/deploy|`joblib.dump()`|

---

## 13️⃣ Concept Check

✅ Linear regression assumes:

- Linearity
    
- Independence
    
- Homoscedasticity (equal variance of residuals)
    
- Normal residuals
    
- No multicollinearity
    

---

## 🧠 Key Takeaways

- **Don’t train on test data.** Always evaluate on unseen data.
    
- **RMSE** is often the most interpretable metric.
    
- **Residual plots** reveal violations of assumptions.
    
- **Coefficients** must be interpreted in context of feature scales.
    
- **Newspaper ads ≈ noise variable → maybe drop or regularize later.**
    

---

## 🧩 Up Next

→ Learn **Regularization** (Ridge, Lasso, ElasticNet)  
to handle overfitting & feature importance in more complex models.

---

Would you like me to make a **second page** with **visual summaries (graphs + code interpretation)** — so you can have both conceptual and visual sections for Obsidian?