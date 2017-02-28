---
title: some spark commands
---

Suppose we have tiny dataframe as following

```python
df = spark.createDataFrame([[1, 'Anna'], [2, 'Bryan']], schema=['index', 'name'])
```

We can find row with name `Anna` by using condition or filter

```python
df[df['name'].like('%Anna%')].show()
df.filter(df['name'] == 'Anna').show()
```
