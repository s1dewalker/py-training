# py-training: Practise

## Pandas + NumPy
1. To drop duplicates | `drop_duplicates`
```python
drivers['driver_id'].drop_duplicates(inplace = True)
```
<br/>

2. Null handling | `isnull`, `fillna`, `dropna`
```python
vehicles.isnull().sum()   # to count the number of null
vehicles.fillna(0, inplace = True)   # to fill values
vehicles.dropna()   # to drop
```
<br/>

3.1. Data Categorization | `.loc[condition, 'col']`
```python
drivers.loc[drivers['rating'] >= 4, 'Status'] = "Elite"
```
<br/>

3.2. Data Categorization | `fn = lambda` and `apply(fn)`
```python
cat_status = lambda x: "Elite" if x >= 4 else "Poor" if x<=2 else "Average"
drivers['Status'] = drivers['rating'].apply(cat_status)
```
<br/>

4.1. Simple group to check size
```python
drivers.groupby(['Status']).size()
```
<br/>

4.2. Grouping or aggregating data | partition by = groupby
```python
rides_grouped = rides_time.groupby('driver_id').agg(
    total_time = ('Time', 'sum'),
    average_fare = ('fare_amount', 'mean')
).reset_index()
```
<br/>

4.3. over(order by ) = .rank(ascending = False)
```python
rides_grouped['rank'] = rides_grouped['total_time'].rank(method = 'dense', ascending = False)
```
<br/>

5. Filtering based on condition
```python
elites_available = drivers.loc[(drivers['Status'] == "Elite") & (drivers['available'] == True)]
```
<br/>

6. Ranking | dense 1,1,2 | min 1,1,3
```python
elites_available['rating'].rank(method = 'dense', ascending = False)
```
<br/>

7.1. Joins | merge() (SQL-like Joins)
```python
drivers_vehicles = pd.merge(drivers, vehicles, how = "left", on = 'vehicle_id')
```
<br/>

7.2. Joins | concat() (Stacking Datasets)
```python
# Stack datasets vertically (like UNION in SQL)
df_concat = pd.concat([drivers, vehicles], axis=0)  # axis=0 → Rows

df_concat = pd.concat([drivers, vehicles], axis=1)  # axis=1 → Columns
```
<br/>

8. Finding index
```python
# Find the row index where driver_id is 2
index = rides[rides['driver_id'] == 2].index
```
<br/>

9. NumPy | Reverse a list
```python
u_col_list[:10][::-1]
```
<br/>

10. Converting to vectors | `.reshape(R,C)`

arr.reshape(-1, 1) | column vector | FIGURE OUT ROWS (-1), I WANT COLUMN AS 1 SO 1D COLUMN VECTOR (1) <br/>

When using -1 in .reshape(), NumPy will figure out the appropriate size for that dimension based on the total number of elements in the array and the other specified dimensions.
```python
# Convert into a column vector (189, 1)
reshaped_arr = arr.reshape(-1, 1)
```

```python
# Convert into a row vector
reshaped_arr = arr.reshape(1, -1)
```
<br/>

#### [View code](https://github.com/s1dewalker/py-training/blob/main/py_Training.ipynb)
<br/><br/>

## Fn + lamda

#### [View code](https://github.com/s1dewalker/py-training/blob/main/py_training_fn_lmbda.ipynb)
