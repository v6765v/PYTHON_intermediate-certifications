__Задача 44: В ячейке ниже представлен код генерирующий DataFrame, которая состоит всего из 1 столбца. Ваша задача перевести его в one hot вид. Сможете ли вы это сделать без get_dummies?__

```
    import random
    lst = ['robot'] * 10
    lst += ['human'] * 10
    random.shuffle(lst)
    data = pd.DataFrame({'whoAmI':lst})
    data.head()
```


```
    whoAmI
0   human
1   human
2   robot
3   human
4   robot
5   robot
6   human
7   robot
8   robot
9   human
10  robot
11  human
12  human
13  robot
14  human
15  human
16  human
17  robot
18  robot
19  robot
```

```
data['tmp'] = 1
data.set_index([data.index, 'whoAmI'], inplace=True)
data = data.unstack(level=-1, fill_value = 0).astype(int)
data.columns = data.columns.droplevel()
data.columns.name = None
print(data)
```

```
    human  robot
0       1      0
1       1      0
2       0      1
3       1      0
4       0      1
5       0      1
6       1      0
7       0      1
8       0      1
9       1      0
10      0      1
11      1      0
12      1      0
13      0      1
14      1      0
15      1      0
16      1      0
17      0      1
18      0      1
19      0      1
```