# Pandas

### replace : 置換

```python
import pandas as pd

data = pd.raed_csv(xxxx)


# inplace=Trueをつけることで値書き換えができる
data['Sex'].replace(['male','female'], [0, 1], inplace=True)
```

### fillna : 欠損データの穴埋め

```python
data['Age'].fillna(20, inplace=True)
```
* 平均値を穴埋めに使うこともできる
```python
data['Age'].fillna(data['Age'].mean(), inplace=True)
```

* np使って変動させる
```python
age_ave = data['Age'].mean()
age_std = data['Age'].mean()
data['Age'].fillna(np.random.randint(age_ave - age_std, age_ave + age_std), inplace=True)
```



### drop : フレーム削除

```python
data.drop(['Name', 'PassangerId'], axis=1, inplace=True)
```

