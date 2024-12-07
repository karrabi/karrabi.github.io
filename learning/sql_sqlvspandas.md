### SELECT Command
- **Simple SELECT command**:
  ```sql
  SELECT column1, column2 FROM table;
  ```
  ```python
  df[['column1', 'column2']]
  ```

- **ORDER BY**:
  ```sql
  SELECT * FROM table ORDER BY column1;
  ```
  ```python
  df.sort_values(by='column1')
  ```

- **WHERE Clause**:
  ```sql
  SELECT * FROM table WHERE column1 = 'value';
  ```
  ```python
  df[df['column1'] == 'value']
  ```

### Sub Queries
- **IN**:
  ```sql
  SELECT * FROM table WHERE column1 IN (SELECT column1 FROM table2);
  ```
  ```python
  df[df['column1'].isin(df2['column1'])]
  ```

- **EXISTS**:
  ```sql
  SELECT * FROM table WHERE EXISTS (SELECT 1 FROM table2 WHERE table1.column1 = table2.column1);
  ```
  ```python
  df[df['column1'].isin(df2['column1'])]
  ```

- **ANY**:
  ```sql
  SELECT * FROM table WHERE column1 > ANY (SELECT column1 FROM table2);
  ```
  ```python
  df[df['column1'] > df2['column1'].min()]
  ```

- **ALL**:
  ```sql
  SELECT * FROM table WHERE column1 > ALL (SELECT column1 FROM table2);
  ```
  ```python
  df[df['column1'] > df2['column1'].max()]
  ```

### Aggregate Functions
- **SUM, AVG, COUNT, etc.**:
  ```sql
  SELECT SUM(column1), AVG(column1), COUNT(column1) FROM table;
  ```
  ```python
  df['column1'].sum(), df['column1'].mean(), df['column1'].count()
  ```

### GROUP BY
- **GROUP BY**:
  ```sql
  SELECT column1, COUNT(*) FROM table GROUP BY column1;
  ```
  ```python
  df.groupby('column1').size()
  ```

### HAVING
- **HAVING**:
  ```sql
  SELECT column1, COUNT(*) FROM table GROUP BY column1 HAVING COUNT(*) > 1;
  ```
  ```python
  df.groupby('column1').filter(lambda x: len(x) > 1)
  ```

### UNION / UNION ALL
- **UNION**:
  ```sql
  SELECT column1 FROM table1 UNION SELECT column1 FROM table2;
  ```
  ```python
  pd.concat([df1['column1'], df2['column1']]).drop_duplicates()
  ```

- **UNION ALL**:
  ```sql
  SELECT column1 FROM table1 UNION ALL SELECT column1 FROM table2;
  ```
  ```python
  pd.concat([df1['column1'], df2['column1']])
  ```

### JOIN
- **INNER JOIN**:
  ```sql
  SELECT * FROM table1 INNER JOIN table2 ON table1.column1 = table2.column1;
  ```
  ```python
  pd.merge(df1, df2, on='column1')
  ```

- **LEFT JOIN**:
  ```sql
  SELECT * FROM table1 LEFT JOIN table2 ON table1.column1 = table2.column1;
  ```
  ```python
  pd.merge(df1, df2, on='column1', how='left')
  ```

- **RIGHT JOIN**:
  ```sql
  SELECT * FROM table1 RIGHT JOIN table2 ON table1.column1 = table2.column1;
  ```
  ```python
  pd.merge(df1, df2, on='column1', how='right')
  ```

- **FULL OUTER JOIN**:
  ```sql
  SELECT * FROM table1 FULL OUTER JOIN table2 ON table1.column1 = table2.column1;
  ```
  ```python
  pd.merge(df1, df2, on='column1', how='outer')
  ```

### Window Functions
- **ROW_NUMBER, RANK, DENSE_RANK, etc.**:
  ```sql
  SELECT column1, ROW_NUMBER() OVER (PARTITION BY column2 ORDER BY column3) FROM table;
  ```
  ```python
  df['row_number'] = df.groupby('column2').cumcount() + 1
  ```

### CTE (Common Table Expressions)
- **CTE**:
  ```sql
  WITH cte AS (SELECT * FROM table WHERE column1 = 'value') SELECT * FROM cte;
  ```
  ```python
  cte = df[df['column1'] == 'value']
  ```

### Common Functions
- **String Functions**:
  ```sql
  SELECT UPPER(column1) FROM table;
  ```
  ```python
  df['column1'].str.upper()
  ```

- **Numeric Functions**:
  ```sql
  SELECT ROUND(column1, 2) FROM table;
  ```
  ```python
  df['column1'].round(2)
  ```

- **Date Functions**:
  ```sql
  SELECT DATEADD(day, 1, column1) FROM table;
  ```
  ```python
  df['column1'] + pd.Timedelta(days=1)
  ```
