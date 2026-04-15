---
share: true
---
2026-04-14 21:04
Tags:

---
Source Notebook: `/Users/liyachen/Documents/fang/UNZIP_FOR_NOTEBOOKS_FINAL/13-Support-Vector-Machines/01-SVM-Regression.ipynb`

# Support Vector Machines
## SVM - Regression

The concrete slump test measures the consistency of fresh concrete before it sets. It is performed to check the workability of freshly made concrete, and therefore the ease with which concrete flows. It can also be used as an indicator of an improperly mixed batch.


Our data set consists of various cement properties and the resulting slump test metrics in cm. Later on the set concrete is tested for its compressive strength 28 days later.

Input variables (7)(component kg in one M^3 concrete):
* Cement
* Slag
* Fly ash
* Water
* SP
* Coarse Aggr.
* Fine Aggr.

Output variables (3):
* SLUMP (cm)
* FLOW (cm)
* **28-day Compressive Strength (Mpa)**

Data Source: https://archive.ics.uci.edu/ml/datasets/Concrete+Slump+Test

*Credit: Yeh, I-Cheng, "Modeling slump flow of concrete using second-order regressions and artificial neural networks," Cement and Concrete Composites, Vol.29, No. 6, 474-480, 2007.*

```python
import numpy as np
import pandas as pd
import seaborn as sns
import matplotlib.pyplot as plt
```

```python
df = pd.read_csv('../DATA/cement_slump.csv')
```

```python
df.head()
```

```text
   Cement   Slag  Fly ash  Water    SP  Coarse Aggr.  Fine Aggr.  SLUMP(cm)  \
0   273.0   82.0    105.0  210.0   9.0         904.0       680.0       23.0   
1   163.0  149.0    191.0  180.0  12.0         843.0       746.0        0.0   
2   162.0  148.0    191.0  179.0  16.0         840.0       743.0        1.0   
3   162.0  148.0    190.0  179.0  19.0         838.0       741.0        3.0   
4   154.0  112.0    144.0  220.0  10.0         923.0       658.0       20.0   

   FLOW(cm)  Compressive Strength (28-day)(Mpa)  
0      62.0                               34.99  
1      20.0                               41.14  
2      20.0                               41.81  
3      21.5                               42.08  
4      64.0                               26.82
```

```python
df.corr()['Compressive Strength (28-day)(Mpa)']
```

```text
Cement                                0.445656
Slag                                 -0.331522
Fly ash                               0.444380
Water                                -0.254320
SP                                   -0.037909
Coarse Aggr.                         -0.160610
Fine Aggr.                           -0.154532
SLUMP(cm)                            -0.223499
FLOW(cm)                             -0.124189
Compressive Strength (28-day)(Mpa)    1.000000
Name: Compressive Strength (28-day)(Mpa), dtype: float64
```

```python
sns.heatmap(df.corr(),cmap='viridis')
```

![[assets/images/Support Vector Machines Cell 08 Output 02.png|assets/images/Support Vector Machines Cell 08 Output 02.png]]

```python
df.columns
```

```text
Index(['Cement', 'Slag', 'Fly ash', 'Water', 'SP', 'Coarse Aggr.',
       'Fine Aggr.', 'SLUMP(cm)', 'FLOW(cm)',
       'Compressive Strength (28-day)(Mpa)'],
      dtype='object')
```

## Train | Test Split

Alternatively you could also set this up as a pipline, something like:

    >>> from sklearn.pipeline import make_pipeline
    >>> from sklearn.preprocessing import StandardScaler
    >>> from sklearn.svm import SVR

    >>> clf = make_pipeline(StandardScaler(), SVR())

```python
df.columns
```

```text
Index(['Cement', 'Slag', 'Fly ash', 'Water', 'SP', 'Coarse Aggr.',
       'Fine Aggr.', 'SLUMP(cm)', 'FLOW(cm)',
       'Compressive Strength (28-day)(Mpa)'],
      dtype='object')
```

```python
X = df.drop('Compressive Strength (28-day)(Mpa)',axis=1)
y = df['Compressive Strength (28-day)(Mpa)']
```

```python
from sklearn.model_selection import train_test_split
```

```python
X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.3, random_state=101)
```

```python
from sklearn.preprocessing import StandardScaler
```

```python
scaler = StandardScaler()
```

```python
scaled_X_train = scaler.fit_transform(X_train)
scaled_X_test = scaler.transform(X_test)
```

## Support Vector Machines - Regression

There are three different implementations of Support Vector Regression: SVR, NuSVR and LinearSVR. LinearSVR provides a faster implementation than SVR but only considers the linear kernel, while NuSVR implements a slightly different formulation than SVR and LinearSVR. See [Implementation details](https://scikit-learn.org/stable/modules/svm.html#svm-implementation-details) for further details.

```python
from sklearn.svm import SVR,LinearSVR
```

Setting C: C is 1 by default and it’s a reasonable default choice. If you have a lot of noisy observations you should decrease it: decreasing C corresponds to more regularization.

LinearSVC and LinearSVR are less sensitive to C when it becomes large, and prediction results stop improving after a certain threshold. Meanwhile, larger C values will take more time to train, sometimes up to 10 times longer

Epsilon: https://stats.stackexchange.com/questions/259018/meaning-of-epsilon-in-svm-regression

```python
base_model = SVR()
```

```python
base_model.fit(scaled_X_train,y_train)
```

```text
SVR()
```

```python
base_preds = base_model.predict(scaled_X_test)
```

## Evaluation

```python
from sklearn.metrics import mean_absolute_error,mean_squared_error
```

```python
mean_absolute_error(y_test,base_preds)
```

```text
5.236902091259178
```

```python
np.sqrt(mean_squared_error(y_test,base_preds))
```

```text
6.695914838327133
```

```python
y_test.mean()
```

```text
36.26870967741935
```

## Grid Search in Attempt for Better Model

```python
param_grid = {'C':[0.001,0.01,0.1,0.5,1],
             'kernel':['linear','rbf','poly'],
              'gamma':['scale','auto'],
              'degree':[2,3,4],
              'epsilon':[0,0.01,0.1,0.5,1,2]}
```

```python
from sklearn.model_selection import GridSearchCV
```

```python
svr = SVR()
grid = GridSearchCV(svr,param_grid=param_grid)
```

```python
grid.fit(scaled_X_train,y_train)
```

```text
GridSearchCV(estimator=SVR(),
             param_grid={'C': [0.001, 0.01, 0.1, 0.5, 1], 'degree': [2, 3, 4],
                         'epsilon': [0, 0.01, 0.1, 0.5, 1, 2],
                         'gamma': ['scale', 'auto'],
                         'kernel': ['linear', 'rbf', 'poly']})
```

```python
grid.best_params_
```

```text
{'C': 1, 'degree': 2, 'epsilon': 2, 'gamma': 'scale', 'kernel': 'linear'}
```

```python
grid_preds = grid.predict(scaled_X_test)
```

```python
mean_absolute_error(y_test,grid_preds)
```

```text
2.5128012210762365
```

```python
np.sqrt(mean_squared_error(y_test,grid_preds))
```

```text
3.178210305119858
```


