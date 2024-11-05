# Filtering and Slicing data in a Pandas Dataframe

### `loc` - Label-Based Selection
The `loc` function is used to select rows and columns by labels or conditional statements. This is helpful when you know the specific row or column names you want to select.

**Syntax**:
```python
DataFrame.loc[row_labels, column_labels]
```

#### Example 1: Selecting by Row and Column Labels
```python
# Select rows with index labels 0 to 10 and columns 'Name' and 'Age'
subset = summer.loc[0:10, ['Name', 'Age']]
print(subset)
```
This selects rows from index 0 to 10 and only the columns labeled "Name" and "Age."

#### Example 2: Conditional Selection with `loc`
```python
# Select female athletes aged 25 or above
female_athletes_25_above = summer.loc[(summer['Sex'] == 'F') & (summer['Age'] >= 25)]
print(female_athletes_25_above)
```
Here, we use `loc` with a condition to filter the dataset, returning rows where both conditions are true.

---

### `iloc` - Index-Based Selection
The `iloc` function is used to select rows and columns by their integer index positions, which is useful when you don’t know the labels but want to select based on their position.

**Syntax**:
```python
DataFrame.iloc[row_indices, column_indices]
```

#### Example 1: Selecting Rows and Columns by Index Position
```python
# Select the first 5 rows and the first 3 columns
subset = summer.iloc[0:5, 0:3]
print(subset)
```
This retrieves rows 0 to 4 and columns 0 to 2 by their index positions.

#### Example 2: Selecting Specific Rows and Columns by Position
```python
# Select rows at positions 10 and 20 and columns at positions 1 and 5
specific_selection = summer.iloc[[10, 20], [1, 5]]
print(specific_selection)
```
In this example, we’re retrieving specific rows and columns using their index positions.

---

### Differences Between `loc` and `iloc`

- **`loc`** is label-based: use it when you want to select by row and column names.
- **`iloc`** is index-based: use it when you want to select by integer location (row and column indices).

### Practice Exercise
Try using `loc` and `iloc` to:
1. Select all athletes who competed in "Basketball" using `loc`.
2. Retrieve rows 50 to 100 and columns 2 to 4 using `iloc`. 

Let me know if you'd like more examples or exercises!


```python
import pandas as pd
import matplotlib.pyplot as plt
```


```python
austin = pd.read_csv(r'C:\Users\abula\Desktop\filess\austin_weather.csv')
seattle = pd.read_csv(r'C:\Users\abula\Desktop\filess\seattle_weather.csv')
summer = pd.read_csv(r'C:\Users\abula\Desktop\3MTT\summer2016.csv')
```

---

# Filtering Data with Pandas

This instructional notebook covers different ways of filtering data with Pandas. We'll explore common filtering techniques and clarify each step to help you understand how to retrieve and view specific data based on conditions.

---

```python
import pandas as pd
import matplotlib.pyplot as plt
```
*We start by importing the necessary libraries:*

- `pandas` (as `pd`): for data manipulation and analysis.
- `matplotlib.pyplot` (as `plt`): for plotting data if needed in later examples.

---

```python
austin = pd.read_csv(r'C:\\Users\\abula\\Desktop\\filess\\austin_weather.csv')
seattle = pd.read_csv(r'C:\\Users\\abula\\Desktop\\filess\\seattle_weather.csv')
summer = pd.read_csv(r'C:\\Users\\abula\\Desktop\\3MTT\\summer2016.csv')
```
*Here, we load three datasets into separate DataFrames:*

- `austin` for Austin's weather data.
- `seattle` for Seattle's weather data.
- `summer` for Summer 2016 Olympic data.

Using `pd.read_csv()`, we read each CSV file from its file path and assign it to a variable.

---

```python
summer.head()
```
*We display the first few rows of the `summer` dataset to get an overview of its structure.*

The `head()` function shows the top 5 rows by default, helping us quickly inspect column names and sample values.

---

# Filtering Data

## Single Condition Filtering

```python
# Example: Filtering athletes aged 25 and above
summer_25_above = summer[summer['Age'] >= 25]
summer_25_above.head()
```
*In this example, we filter the `summer` DataFrame to include only rows where the `Age` column is 25 or greater.*

- The condition `summer['Age'] >= 25` returns a Boolean Series (True or False) for each row.
- By placing this condition inside `summer[...]`, we keep only rows where the condition is True.

---

## Multiple Conditions Filtering

```python
# Example: Filtering female athletes who won a medal
female_medalists = summer[(summer['Sex'] == 'F') & (summer['Medal'].notnull())]
female_medalists.head()
```
*This example demonstrates filtering with multiple conditions using the `&` operator:*

- We use `(summer['Sex'] == 'F')` to select female athletes.
- `(summer['Medal'].notnull())` selects rows where a medal was won (non-null values in `Medal` column).
- Enclose each condition in parentheses, and combine them with `&` (logical AND) to keep rows where both conditions are True.

---

## Filtering with Specific Columns

```python
# Example: Viewing only specific columns after filtering
female_medalists[['Name', 'Sport', 'Medal']].head()
```
*After filtering, you can select specific columns to view.*

- Here, we filter for female medalists, then display only the `Name`, `Sport`, and `Medal` columns using `[['Name', 'Sport', 'Medal']]`.

---

## Exercise

Try experimenting with different filtering conditions to explore the data further:

1. Filter athletes who are 30 years and older.
2. Find all athletes who competed in "Swimming".
3. Identify rows where `Weight` is below 60 kg and `Height` is above 170 cm.

*Use these exercises to practice and reinforce your filtering skills!* 

--- 

If you need further clarification or have additional questions, feel free to ask!


```python
summer.head()
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Unnamed: 0</th>
      <th>ID</th>
      <th>Name</th>
      <th>Sex</th>
      <th>Age</th>
      <th>Height</th>
      <th>Weight</th>
      <th>Team</th>
      <th>NOC</th>
      <th>Games</th>
      <th>Year</th>
      <th>Season</th>
      <th>City</th>
      <th>Sport</th>
      <th>Event</th>
      <th>Medal</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>158</td>
      <td>62</td>
      <td>Giovanni Abagnale</td>
      <td>M</td>
      <td>21.0</td>
      <td>198.0</td>
      <td>90.0</td>
      <td>Italy</td>
      <td>ITA</td>
      <td>2016 Summer</td>
      <td>2016</td>
      <td>Summer</td>
      <td>Rio de Janeiro</td>
      <td>Rowing</td>
      <td>Rowing Men's Coxless Pairs</td>
      <td>Bronze</td>
    </tr>
    <tr>
      <th>1</th>
      <td>161</td>
      <td>65</td>
      <td>Patimat Abakarova</td>
      <td>F</td>
      <td>21.0</td>
      <td>165.0</td>
      <td>49.0</td>
      <td>Azerbaijan</td>
      <td>AZE</td>
      <td>2016 Summer</td>
      <td>2016</td>
      <td>Summer</td>
      <td>Rio de Janeiro</td>
      <td>Taekwondo</td>
      <td>Taekwondo Women's Flyweight</td>
      <td>Bronze</td>
    </tr>
    <tr>
      <th>2</th>
      <td>175</td>
      <td>73</td>
      <td>Luc Abalo</td>
      <td>M</td>
      <td>31.0</td>
      <td>182.0</td>
      <td>86.0</td>
      <td>France</td>
      <td>FRA</td>
      <td>2016 Summer</td>
      <td>2016</td>
      <td>Summer</td>
      <td>Rio de Janeiro</td>
      <td>Handball</td>
      <td>Handball Men's Handball</td>
      <td>Silver</td>
    </tr>
    <tr>
      <th>3</th>
      <td>450</td>
      <td>250</td>
      <td>Saeid Morad Abdevali</td>
      <td>M</td>
      <td>26.0</td>
      <td>170.0</td>
      <td>80.0</td>
      <td>Iran</td>
      <td>IRI</td>
      <td>2016 Summer</td>
      <td>2016</td>
      <td>Summer</td>
      <td>Rio de Janeiro</td>
      <td>Wrestling</td>
      <td>Wrestling Men's Middleweight, Greco-Roman</td>
      <td>Bronze</td>
    </tr>
    <tr>
      <th>4</th>
      <td>794</td>
      <td>455</td>
      <td>Denis Mikhaylovich Ablyazin</td>
      <td>M</td>
      <td>24.0</td>
      <td>161.0</td>
      <td>62.0</td>
      <td>Russia</td>
      <td>RUS</td>
      <td>2016 Summer</td>
      <td>2016</td>
      <td>Summer</td>
      <td>Rio de Janeiro</td>
      <td>Gymnastics</td>
      <td>Gymnastics Men's Team All-Around</td>
      <td>Silver</td>
    </tr>
  </tbody>
</table>
</div>




```python
summer.drop(columns= 'Unnamed: 0', axis=1, inplace=True)
```


```python
player_info = summer[['ID', 'Name', 'Sex']]
```


```python
player_info
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>ID</th>
      <th>Name</th>
      <th>Sex</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>62</td>
      <td>Giovanni Abagnale</td>
      <td>M</td>
    </tr>
    <tr>
      <th>1</th>
      <td>65</td>
      <td>Patimat Abakarova</td>
      <td>F</td>
    </tr>
    <tr>
      <th>2</th>
      <td>73</td>
      <td>Luc Abalo</td>
      <td>M</td>
    </tr>
    <tr>
      <th>3</th>
      <td>250</td>
      <td>Saeid Morad Abdevali</td>
      <td>M</td>
    </tr>
    <tr>
      <th>4</th>
      <td>455</td>
      <td>Denis Mikhaylovich Ablyazin</td>
      <td>M</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>2009</th>
      <td>134857</td>
      <td>Zhu Ting</td>
      <td>F</td>
    </tr>
    <tr>
      <th>2010</th>
      <td>135132</td>
      <td>Bojana ivkovi</td>
      <td>F</td>
    </tr>
    <tr>
      <th>2011</th>
      <td>135205</td>
      <td>Shakhobiddin Shokirovich Zoirov</td>
      <td>M</td>
    </tr>
    <tr>
      <th>2012</th>
      <td>135245</td>
      <td>Milenko Zori</td>
      <td>M</td>
    </tr>
    <tr>
      <th>2013</th>
      <td>135525</td>
      <td>Martin Zwicker</td>
      <td>M</td>
    </tr>
  </tbody>
</table>
<p>2014 rows × 3 columns</p>
</div>




```python
player50 = player_info.head(50)
```


```python
player_info.iloc[:50, :2]
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>ID</th>
      <th>Name</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>62</td>
      <td>Giovanni Abagnale</td>
    </tr>
    <tr>
      <th>1</th>
      <td>65</td>
      <td>Patimat Abakarova</td>
    </tr>
    <tr>
      <th>2</th>
      <td>73</td>
      <td>Luc Abalo</td>
    </tr>
    <tr>
      <th>3</th>
      <td>250</td>
      <td>Saeid Morad Abdevali</td>
    </tr>
    <tr>
      <th>4</th>
      <td>455</td>
      <td>Denis Mikhaylovich Ablyazin</td>
    </tr>
    <tr>
      <th>5</th>
      <td>455</td>
      <td>Denis Mikhaylovich Ablyazin</td>
    </tr>
    <tr>
      <th>6</th>
      <td>455</td>
      <td>Denis Mikhaylovich Ablyazin</td>
    </tr>
    <tr>
      <th>7</th>
      <td>465</td>
      <td>Matthew "Matt" Abood</td>
    </tr>
    <tr>
      <th>8</th>
      <td>576</td>
      <td>Alejandro "lex" Abrines Redondo</td>
    </tr>
    <tr>
      <th>9</th>
      <td>608</td>
      <td>Ahmad Abughaush</td>
    </tr>
    <tr>
      <th>10</th>
      <td>690</td>
      <td>Chantal Achterberg</td>
    </tr>
    <tr>
      <th>11</th>
      <td>832</td>
      <td>Nicola Virginia Adams</td>
    </tr>
    <tr>
      <th>12</th>
      <td>837</td>
      <td>Rachael Alexis Adams</td>
    </tr>
    <tr>
      <th>13</th>
      <td>846</td>
      <td>Valerie Kasanita Adams-Vili (-Price)</td>
    </tr>
    <tr>
      <th>14</th>
      <td>1017</td>
      <td>Nathan Ghar-Jun Adrian</td>
    </tr>
    <tr>
      <th>15</th>
      <td>1017</td>
      <td>Nathan Ghar-Jun Adrian</td>
    </tr>
    <tr>
      <th>16</th>
      <td>1017</td>
      <td>Nathan Ghar-Jun Adrian</td>
    </tr>
    <tr>
      <th>17</th>
      <td>1017</td>
      <td>Nathan Ghar-Jun Adrian</td>
    </tr>
    <tr>
      <th>18</th>
      <td>1095</td>
      <td>Cecil Sebastian Afrika</td>
    </tr>
    <tr>
      <th>19</th>
      <td>1107</td>
      <td>Timothy Ernest Victor Kwizera "Tim" Agaba</td>
    </tr>
    <tr>
      <th>20</th>
      <td>1131</td>
      <td>Clarisse Agbegnenou</td>
    </tr>
    <tr>
      <th>21</th>
      <td>1262</td>
      <td>Sandra Aguilar Navarro</td>
    </tr>
    <tr>
      <th>22</th>
      <td>1301</td>
      <td>Sri Wahyuni Agustiani</td>
    </tr>
    <tr>
      <th>23</th>
      <td>1356</td>
      <td>Christian Ahlmann</td>
    </tr>
    <tr>
      <th>24</th>
      <td>1374</td>
      <td>Tontowi Ahmad</td>
    </tr>
    <tr>
      <th>25</th>
      <td>1466</td>
      <td>Matteo Aicardi</td>
    </tr>
    <tr>
      <th>26</th>
      <td>1478</td>
      <td>Rosaria Aiello</td>
    </tr>
    <tr>
      <th>27</th>
      <td>1551</td>
      <td>Oluwafemi "Junior" Ajayi</td>
    </tr>
    <tr>
      <th>28</th>
      <td>1561</td>
      <td>Mobolade Abimbola Ajomale</td>
    </tr>
    <tr>
      <th>29</th>
      <td>1634</td>
      <td>Taha Akgl</td>
    </tr>
    <tr>
      <th>30</th>
      <td>1647</td>
      <td>Murodzhon Kakharovich Akhmadaliyev</td>
    </tr>
    <tr>
      <th>31</th>
      <td>1649</td>
      <td>Artur Kamilevich Akhmatkhuzin</td>
    </tr>
    <tr>
      <th>32</th>
      <td>1682</td>
      <td>Morolake Akinosun</td>
    </tr>
    <tr>
      <th>33</th>
      <td>1683</td>
      <td>Foluke Antinuke Akinradewo</td>
    </tr>
    <tr>
      <th>34</th>
      <td>1716</td>
      <td>Daniel Akpeyi</td>
    </tr>
    <tr>
      <th>35</th>
      <td>1730</td>
      <td>Monica Aksamit</td>
    </tr>
    <tr>
      <th>36</th>
      <td>1858</td>
      <td>Fehaid Al-Deehani</td>
    </tr>
    <tr>
      <th>37</th>
      <td>2112</td>
      <td>Abdullah Al-Rashidi</td>
    </tr>
    <tr>
      <th>38</th>
      <td>2464</td>
      <td>Jo Qesem Ayela Aleh</td>
    </tr>
    <tr>
      <th>39</th>
      <td>2497</td>
      <td>Artur Aleksanyan</td>
    </tr>
    <tr>
      <th>40</th>
      <td>2517</td>
      <td>Milan Aleksi</td>
    </tr>
    <tr>
      <th>41</th>
      <td>2610</td>
      <td>Abdoul Razak Issoufou Alfaga</td>
    </tr>
    <tr>
      <th>42</th>
      <td>2695</td>
      <td>Nia Sifaatihii Ali</td>
    </tr>
    <tr>
      <th>43</th>
      <td>2758</td>
      <td>Alison Conte Cerutti</td>
    </tr>
    <tr>
      <th>44</th>
      <td>2769</td>
      <td>Kimia Alizadeh Zenoorin</td>
    </tr>
    <tr>
      <th>45</th>
      <td>3077</td>
      <td>Ida Alstad</td>
    </tr>
    <tr>
      <th>46</th>
      <td>3174</td>
      <td>Lzaro Jorge lvarez Estrada</td>
    </tr>
    <tr>
      <th>47</th>
      <td>3206</td>
      <td>Yuri Alvear Orjuela</td>
    </tr>
    <tr>
      <th>48</th>
      <td>3537</td>
      <td>Marwa Al-Amri</td>
    </tr>
    <tr>
      <th>49</th>
      <td>3561</td>
      <td>Stanley Amuzie</td>
    </tr>
  </tbody>
</table>
</div>




```python
summer.iloc[:50, 1:6:2]
```


```python
summer.head(2)
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>ID</th>
      <th>Name</th>
      <th>Sex</th>
      <th>Age</th>
      <th>Height</th>
      <th>Weight</th>
      <th>Team</th>
      <th>NOC</th>
      <th>Games</th>
      <th>Year</th>
      <th>Season</th>
      <th>City</th>
      <th>Sport</th>
      <th>Event</th>
      <th>Medal</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>62</td>
      <td>Giovanni Abagnale</td>
      <td>M</td>
      <td>21.0</td>
      <td>198.0</td>
      <td>90.0</td>
      <td>Italy</td>
      <td>ITA</td>
      <td>2016 Summer</td>
      <td>2016</td>
      <td>Summer</td>
      <td>Rio de Janeiro</td>
      <td>Rowing</td>
      <td>Rowing Men's Coxless Pairs</td>
      <td>Bronze</td>
    </tr>
    <tr>
      <th>1</th>
      <td>65</td>
      <td>Patimat Abakarova</td>
      <td>F</td>
      <td>21.0</td>
      <td>165.0</td>
      <td>49.0</td>
      <td>Azerbaijan</td>
      <td>AZE</td>
      <td>2016 Summer</td>
      <td>2016</td>
      <td>Summer</td>
      <td>Rio de Janeiro</td>
      <td>Taekwondo</td>
      <td>Taekwondo Women's Flyweight</td>
      <td>Bronze</td>
    </tr>
  </tbody>
</table>
</div>




```python
summer.loc[0:50, ['Name', 'Age', 'Team']]
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Name</th>
      <th>Age</th>
      <th>Team</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Giovanni Abagnale</td>
      <td>21.0</td>
      <td>Italy</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Patimat Abakarova</td>
      <td>21.0</td>
      <td>Azerbaijan</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Luc Abalo</td>
      <td>31.0</td>
      <td>France</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Saeid Morad Abdevali</td>
      <td>26.0</td>
      <td>Iran</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Denis Mikhaylovich Ablyazin</td>
      <td>24.0</td>
      <td>Russia</td>
    </tr>
    <tr>
      <th>5</th>
      <td>Denis Mikhaylovich Ablyazin</td>
      <td>24.0</td>
      <td>Russia</td>
    </tr>
    <tr>
      <th>6</th>
      <td>Denis Mikhaylovich Ablyazin</td>
      <td>24.0</td>
      <td>Russia</td>
    </tr>
    <tr>
      <th>7</th>
      <td>Matthew "Matt" Abood</td>
      <td>30.0</td>
      <td>Australia</td>
    </tr>
    <tr>
      <th>8</th>
      <td>Alejandro "lex" Abrines Redondo</td>
      <td>23.0</td>
      <td>Spain</td>
    </tr>
    <tr>
      <th>9</th>
      <td>Ahmad Abughaush</td>
      <td>20.0</td>
      <td>Jordan</td>
    </tr>
    <tr>
      <th>10</th>
      <td>Chantal Achterberg</td>
      <td>31.0</td>
      <td>Netherlands</td>
    </tr>
    <tr>
      <th>11</th>
      <td>Nicola Virginia Adams</td>
      <td>33.0</td>
      <td>Great Britain</td>
    </tr>
    <tr>
      <th>12</th>
      <td>Rachael Alexis Adams</td>
      <td>26.0</td>
      <td>United States</td>
    </tr>
    <tr>
      <th>13</th>
      <td>Valerie Kasanita Adams-Vili (-Price)</td>
      <td>31.0</td>
      <td>New Zealand</td>
    </tr>
    <tr>
      <th>14</th>
      <td>Nathan Ghar-Jun Adrian</td>
      <td>27.0</td>
      <td>United States</td>
    </tr>
    <tr>
      <th>15</th>
      <td>Nathan Ghar-Jun Adrian</td>
      <td>27.0</td>
      <td>United States</td>
    </tr>
    <tr>
      <th>16</th>
      <td>Nathan Ghar-Jun Adrian</td>
      <td>27.0</td>
      <td>United States</td>
    </tr>
    <tr>
      <th>17</th>
      <td>Nathan Ghar-Jun Adrian</td>
      <td>27.0</td>
      <td>United States</td>
    </tr>
    <tr>
      <th>18</th>
      <td>Cecil Sebastian Afrika</td>
      <td>28.0</td>
      <td>South Africa</td>
    </tr>
    <tr>
      <th>19</th>
      <td>Timothy Ernest Victor Kwizera "Tim" Agaba</td>
      <td>27.0</td>
      <td>South Africa</td>
    </tr>
    <tr>
      <th>20</th>
      <td>Clarisse Agbegnenou</td>
      <td>23.0</td>
      <td>France</td>
    </tr>
    <tr>
      <th>21</th>
      <td>Sandra Aguilar Navarro</td>
      <td>23.0</td>
      <td>Spain</td>
    </tr>
    <tr>
      <th>22</th>
      <td>Sri Wahyuni Agustiani</td>
      <td>21.0</td>
      <td>Indonesia</td>
    </tr>
    <tr>
      <th>23</th>
      <td>Christian Ahlmann</td>
      <td>41.0</td>
      <td>Germany</td>
    </tr>
    <tr>
      <th>24</th>
      <td>Tontowi Ahmad</td>
      <td>29.0</td>
      <td>Indonesia-1</td>
    </tr>
    <tr>
      <th>25</th>
      <td>Matteo Aicardi</td>
      <td>30.0</td>
      <td>Italy</td>
    </tr>
    <tr>
      <th>26</th>
      <td>Rosaria Aiello</td>
      <td>27.0</td>
      <td>Italy</td>
    </tr>
    <tr>
      <th>27</th>
      <td>Oluwafemi "Junior" Ajayi</td>
      <td>20.0</td>
      <td>Nigeria</td>
    </tr>
    <tr>
      <th>28</th>
      <td>Mobolade Abimbola Ajomale</td>
      <td>20.0</td>
      <td>Canada</td>
    </tr>
    <tr>
      <th>29</th>
      <td>Taha Akgl</td>
      <td>25.0</td>
      <td>Turkey</td>
    </tr>
    <tr>
      <th>30</th>
      <td>Murodzhon Kakharovich Akhmadaliyev</td>
      <td>21.0</td>
      <td>Uzbekistan</td>
    </tr>
    <tr>
      <th>31</th>
      <td>Artur Kamilevich Akhmatkhuzin</td>
      <td>28.0</td>
      <td>Russia</td>
    </tr>
    <tr>
      <th>32</th>
      <td>Morolake Akinosun</td>
      <td>22.0</td>
      <td>United States</td>
    </tr>
    <tr>
      <th>33</th>
      <td>Foluke Antinuke Akinradewo</td>
      <td>28.0</td>
      <td>United States</td>
    </tr>
    <tr>
      <th>34</th>
      <td>Daniel Akpeyi</td>
      <td>30.0</td>
      <td>Nigeria</td>
    </tr>
    <tr>
      <th>35</th>
      <td>Monica Aksamit</td>
      <td>26.0</td>
      <td>United States</td>
    </tr>
    <tr>
      <th>36</th>
      <td>Fehaid Al-Deehani</td>
      <td>49.0</td>
      <td>Individual Olympic Athletes</td>
    </tr>
    <tr>
      <th>37</th>
      <td>Abdullah Al-Rashidi</td>
      <td>52.0</td>
      <td>Individual Olympic Athletes</td>
    </tr>
    <tr>
      <th>38</th>
      <td>Jo Qesem Ayela Aleh</td>
      <td>30.0</td>
      <td>New Zealand</td>
    </tr>
    <tr>
      <th>39</th>
      <td>Artur Aleksanyan</td>
      <td>24.0</td>
      <td>Armenia</td>
    </tr>
    <tr>
      <th>40</th>
      <td>Milan Aleksi</td>
      <td>30.0</td>
      <td>Serbia</td>
    </tr>
    <tr>
      <th>41</th>
      <td>Abdoul Razak Issoufou Alfaga</td>
      <td>21.0</td>
      <td>Niger</td>
    </tr>
    <tr>
      <th>42</th>
      <td>Nia Sifaatihii Ali</td>
      <td>27.0</td>
      <td>United States</td>
    </tr>
    <tr>
      <th>43</th>
      <td>Alison Conte Cerutti</td>
      <td>30.0</td>
      <td>Brazil-1</td>
    </tr>
    <tr>
      <th>44</th>
      <td>Kimia Alizadeh Zenoorin</td>
      <td>18.0</td>
      <td>Iran</td>
    </tr>
    <tr>
      <th>45</th>
      <td>Ida Alstad</td>
      <td>31.0</td>
      <td>Norway</td>
    </tr>
    <tr>
      <th>46</th>
      <td>Lzaro Jorge lvarez Estrada</td>
      <td>25.0</td>
      <td>Cuba</td>
    </tr>
    <tr>
      <th>47</th>
      <td>Yuri Alvear Orjuela</td>
      <td>30.0</td>
      <td>Colombia</td>
    </tr>
    <tr>
      <th>48</th>
      <td>Marwa Al-Amri</td>
      <td>27.0</td>
      <td>Tunisia</td>
    </tr>
    <tr>
      <th>49</th>
      <td>Stanley Amuzie</td>
      <td>20.0</td>
      <td>Nigeria</td>
    </tr>
    <tr>
      <th>50</th>
      <td>An Ba-Ul</td>
      <td>22.0</td>
      <td>South Korea</td>
    </tr>
  </tbody>
</table>
</div>




```python
summer.loc[:50, 'Name':'Team']
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Name</th>
      <th>Sex</th>
      <th>Age</th>
      <th>Height</th>
      <th>Weight</th>
      <th>Team</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Giovanni Abagnale</td>
      <td>M</td>
      <td>21.0</td>
      <td>198.0</td>
      <td>90.0</td>
      <td>Italy</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Patimat Abakarova</td>
      <td>F</td>
      <td>21.0</td>
      <td>165.0</td>
      <td>49.0</td>
      <td>Azerbaijan</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Luc Abalo</td>
      <td>M</td>
      <td>31.0</td>
      <td>182.0</td>
      <td>86.0</td>
      <td>France</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Saeid Morad Abdevali</td>
      <td>M</td>
      <td>26.0</td>
      <td>170.0</td>
      <td>80.0</td>
      <td>Iran</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Denis Mikhaylovich Ablyazin</td>
      <td>M</td>
      <td>24.0</td>
      <td>161.0</td>
      <td>62.0</td>
      <td>Russia</td>
    </tr>
    <tr>
      <th>5</th>
      <td>Denis Mikhaylovich Ablyazin</td>
      <td>M</td>
      <td>24.0</td>
      <td>161.0</td>
      <td>62.0</td>
      <td>Russia</td>
    </tr>
    <tr>
      <th>6</th>
      <td>Denis Mikhaylovich Ablyazin</td>
      <td>M</td>
      <td>24.0</td>
      <td>161.0</td>
      <td>62.0</td>
      <td>Russia</td>
    </tr>
    <tr>
      <th>7</th>
      <td>Matthew "Matt" Abood</td>
      <td>M</td>
      <td>30.0</td>
      <td>197.0</td>
      <td>92.0</td>
      <td>Australia</td>
    </tr>
    <tr>
      <th>8</th>
      <td>Alejandro "lex" Abrines Redondo</td>
      <td>M</td>
      <td>23.0</td>
      <td>198.0</td>
      <td>93.0</td>
      <td>Spain</td>
    </tr>
    <tr>
      <th>9</th>
      <td>Ahmad Abughaush</td>
      <td>M</td>
      <td>20.0</td>
      <td>178.0</td>
      <td>68.0</td>
      <td>Jordan</td>
    </tr>
    <tr>
      <th>10</th>
      <td>Chantal Achterberg</td>
      <td>F</td>
      <td>31.0</td>
      <td>172.0</td>
      <td>72.0</td>
      <td>Netherlands</td>
    </tr>
    <tr>
      <th>11</th>
      <td>Nicola Virginia Adams</td>
      <td>F</td>
      <td>33.0</td>
      <td>164.0</td>
      <td>51.0</td>
      <td>Great Britain</td>
    </tr>
    <tr>
      <th>12</th>
      <td>Rachael Alexis Adams</td>
      <td>F</td>
      <td>26.0</td>
      <td>188.0</td>
      <td>81.0</td>
      <td>United States</td>
    </tr>
    <tr>
      <th>13</th>
      <td>Valerie Kasanita Adams-Vili (-Price)</td>
      <td>F</td>
      <td>31.0</td>
      <td>193.0</td>
      <td>120.0</td>
      <td>New Zealand</td>
    </tr>
    <tr>
      <th>14</th>
      <td>Nathan Ghar-Jun Adrian</td>
      <td>M</td>
      <td>27.0</td>
      <td>198.0</td>
      <td>100.0</td>
      <td>United States</td>
    </tr>
    <tr>
      <th>15</th>
      <td>Nathan Ghar-Jun Adrian</td>
      <td>M</td>
      <td>27.0</td>
      <td>198.0</td>
      <td>100.0</td>
      <td>United States</td>
    </tr>
    <tr>
      <th>16</th>
      <td>Nathan Ghar-Jun Adrian</td>
      <td>M</td>
      <td>27.0</td>
      <td>198.0</td>
      <td>100.0</td>
      <td>United States</td>
    </tr>
    <tr>
      <th>17</th>
      <td>Nathan Ghar-Jun Adrian</td>
      <td>M</td>
      <td>27.0</td>
      <td>198.0</td>
      <td>100.0</td>
      <td>United States</td>
    </tr>
    <tr>
      <th>18</th>
      <td>Cecil Sebastian Afrika</td>
      <td>M</td>
      <td>28.0</td>
      <td>175.0</td>
      <td>75.0</td>
      <td>South Africa</td>
    </tr>
    <tr>
      <th>19</th>
      <td>Timothy Ernest Victor Kwizera "Tim" Agaba</td>
      <td>M</td>
      <td>27.0</td>
      <td>193.0</td>
      <td>104.0</td>
      <td>South Africa</td>
    </tr>
    <tr>
      <th>20</th>
      <td>Clarisse Agbegnenou</td>
      <td>F</td>
      <td>23.0</td>
      <td>164.0</td>
      <td>66.0</td>
      <td>France</td>
    </tr>
    <tr>
      <th>21</th>
      <td>Sandra Aguilar Navarro</td>
      <td>F</td>
      <td>23.0</td>
      <td>167.0</td>
      <td>50.0</td>
      <td>Spain</td>
    </tr>
    <tr>
      <th>22</th>
      <td>Sri Wahyuni Agustiani</td>
      <td>F</td>
      <td>21.0</td>
      <td>147.0</td>
      <td>47.0</td>
      <td>Indonesia</td>
    </tr>
    <tr>
      <th>23</th>
      <td>Christian Ahlmann</td>
      <td>M</td>
      <td>41.0</td>
      <td>189.0</td>
      <td>80.0</td>
      <td>Germany</td>
    </tr>
    <tr>
      <th>24</th>
      <td>Tontowi Ahmad</td>
      <td>M</td>
      <td>29.0</td>
      <td>179.0</td>
      <td>72.0</td>
      <td>Indonesia-1</td>
    </tr>
    <tr>
      <th>25</th>
      <td>Matteo Aicardi</td>
      <td>M</td>
      <td>30.0</td>
      <td>192.0</td>
      <td>102.0</td>
      <td>Italy</td>
    </tr>
    <tr>
      <th>26</th>
      <td>Rosaria Aiello</td>
      <td>F</td>
      <td>27.0</td>
      <td>172.0</td>
      <td>74.0</td>
      <td>Italy</td>
    </tr>
    <tr>
      <th>27</th>
      <td>Oluwafemi "Junior" Ajayi</td>
      <td>M</td>
      <td>20.0</td>
      <td>172.0</td>
      <td>79.0</td>
      <td>Nigeria</td>
    </tr>
    <tr>
      <th>28</th>
      <td>Mobolade Abimbola Ajomale</td>
      <td>M</td>
      <td>20.0</td>
      <td>180.0</td>
      <td>62.0</td>
      <td>Canada</td>
    </tr>
    <tr>
      <th>29</th>
      <td>Taha Akgl</td>
      <td>M</td>
      <td>25.0</td>
      <td>192.0</td>
      <td>125.0</td>
      <td>Turkey</td>
    </tr>
    <tr>
      <th>30</th>
      <td>Murodzhon Kakharovich Akhmadaliyev</td>
      <td>M</td>
      <td>21.0</td>
      <td>165.0</td>
      <td>56.0</td>
      <td>Uzbekistan</td>
    </tr>
    <tr>
      <th>31</th>
      <td>Artur Kamilevich Akhmatkhuzin</td>
      <td>M</td>
      <td>28.0</td>
      <td>187.0</td>
      <td>79.0</td>
      <td>Russia</td>
    </tr>
    <tr>
      <th>32</th>
      <td>Morolake Akinosun</td>
      <td>F</td>
      <td>22.0</td>
      <td>163.0</td>
      <td>61.0</td>
      <td>United States</td>
    </tr>
    <tr>
      <th>33</th>
      <td>Foluke Antinuke Akinradewo</td>
      <td>F</td>
      <td>28.0</td>
      <td>191.0</td>
      <td>79.0</td>
      <td>United States</td>
    </tr>
    <tr>
      <th>34</th>
      <td>Daniel Akpeyi</td>
      <td>M</td>
      <td>30.0</td>
      <td>187.0</td>
      <td>80.0</td>
      <td>Nigeria</td>
    </tr>
    <tr>
      <th>35</th>
      <td>Monica Aksamit</td>
      <td>F</td>
      <td>26.0</td>
      <td>183.0</td>
      <td>74.0</td>
      <td>United States</td>
    </tr>
    <tr>
      <th>36</th>
      <td>Fehaid Al-Deehani</td>
      <td>M</td>
      <td>49.0</td>
      <td>178.0</td>
      <td>95.0</td>
      <td>Individual Olympic Athletes</td>
    </tr>
    <tr>
      <th>37</th>
      <td>Abdullah Al-Rashidi</td>
      <td>M</td>
      <td>52.0</td>
      <td>183.0</td>
      <td>83.0</td>
      <td>Individual Olympic Athletes</td>
    </tr>
    <tr>
      <th>38</th>
      <td>Jo Qesem Ayela Aleh</td>
      <td>F</td>
      <td>30.0</td>
      <td>171.0</td>
      <td>58.0</td>
      <td>New Zealand</td>
    </tr>
    <tr>
      <th>39</th>
      <td>Artur Aleksanyan</td>
      <td>M</td>
      <td>24.0</td>
      <td>190.0</td>
      <td>98.0</td>
      <td>Armenia</td>
    </tr>
    <tr>
      <th>40</th>
      <td>Milan Aleksi</td>
      <td>M</td>
      <td>30.0</td>
      <td>193.0</td>
      <td>96.0</td>
      <td>Serbia</td>
    </tr>
    <tr>
      <th>41</th>
      <td>Abdoul Razak Issoufou Alfaga</td>
      <td>M</td>
      <td>21.0</td>
      <td>207.0</td>
      <td>90.0</td>
      <td>Niger</td>
    </tr>
    <tr>
      <th>42</th>
      <td>Nia Sifaatihii Ali</td>
      <td>F</td>
      <td>27.0</td>
      <td>170.0</td>
      <td>65.0</td>
      <td>United States</td>
    </tr>
    <tr>
      <th>43</th>
      <td>Alison Conte Cerutti</td>
      <td>M</td>
      <td>30.0</td>
      <td>203.0</td>
      <td>106.0</td>
      <td>Brazil-1</td>
    </tr>
    <tr>
      <th>44</th>
      <td>Kimia Alizadeh Zenoorin</td>
      <td>F</td>
      <td>18.0</td>
      <td>185.0</td>
      <td>57.0</td>
      <td>Iran</td>
    </tr>
    <tr>
      <th>45</th>
      <td>Ida Alstad</td>
      <td>F</td>
      <td>31.0</td>
      <td>172.0</td>
      <td>60.0</td>
      <td>Norway</td>
    </tr>
    <tr>
      <th>46</th>
      <td>Lzaro Jorge lvarez Estrada</td>
      <td>M</td>
      <td>25.0</td>
      <td>173.0</td>
      <td>60.0</td>
      <td>Cuba</td>
    </tr>
    <tr>
      <th>47</th>
      <td>Yuri Alvear Orjuela</td>
      <td>F</td>
      <td>30.0</td>
      <td>176.0</td>
      <td>70.0</td>
      <td>Colombia</td>
    </tr>
    <tr>
      <th>48</th>
      <td>Marwa Al-Amri</td>
      <td>F</td>
      <td>27.0</td>
      <td>160.0</td>
      <td>58.0</td>
      <td>Tunisia</td>
    </tr>
    <tr>
      <th>49</th>
      <td>Stanley Amuzie</td>
      <td>M</td>
      <td>20.0</td>
      <td>171.0</td>
      <td>85.0</td>
      <td>Nigeria</td>
    </tr>
    <tr>
      <th>50</th>
      <td>An Ba-Ul</td>
      <td>M</td>
      <td>22.0</td>
      <td>169.0</td>
      <td>66.0</td>
      <td>South Korea</td>
    </tr>
  </tbody>
</table>
</div>




```python
summer.head(2)
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>ID</th>
      <th>Name</th>
      <th>Sex</th>
      <th>Age</th>
      <th>Height</th>
      <th>Weight</th>
      <th>Team</th>
      <th>NOC</th>
      <th>Games</th>
      <th>Year</th>
      <th>Season</th>
      <th>City</th>
      <th>Sport</th>
      <th>Event</th>
      <th>Medal</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>62</td>
      <td>Giovanni Abagnale</td>
      <td>M</td>
      <td>21.0</td>
      <td>198.0</td>
      <td>90.0</td>
      <td>Italy</td>
      <td>ITA</td>
      <td>2016 Summer</td>
      <td>2016</td>
      <td>Summer</td>
      <td>Rio de Janeiro</td>
      <td>Rowing</td>
      <td>Rowing Men's Coxless Pairs</td>
      <td>Bronze</td>
    </tr>
    <tr>
      <th>1</th>
      <td>65</td>
      <td>Patimat Abakarova</td>
      <td>F</td>
      <td>21.0</td>
      <td>165.0</td>
      <td>49.0</td>
      <td>Azerbaijan</td>
      <td>AZE</td>
      <td>2016 Summer</td>
      <td>2016</td>
      <td>Summer</td>
      <td>Rio de Janeiro</td>
      <td>Taekwondo</td>
      <td>Taekwondo Women's Flyweight</td>
      <td>Bronze</td>
    </tr>
  </tbody>
</table>
</div>




```python
summer.Sport.nunique()
```




    34




```python
summer.Sport.unique()
```




    array(['Rowing', 'Taekwondo', 'Handball', 'Wrestling', 'Gymnastics',
           'Swimming', 'Basketball', 'Boxing', 'Volleyball', 'Athletics',
           'Rugby Sevens', 'Judo', 'Rhythmic Gymnastics', 'Weightlifting',
           'Equestrianism', 'Badminton', 'Water Polo', 'Football', 'Fencing',
           'Shooting', 'Sailing', 'Beach Volleyball', 'Canoeing', 'Hockey',
           'Cycling', 'Tennis', 'Diving', 'Table Tennis', 'Triathlon',
           'Archery', 'Synchronized Swimming', 'Modern Pentathlon',
           'Trampolining', 'Golf'], dtype=object)




```python
summer.head(2)
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>ID</th>
      <th>Name</th>
      <th>Sex</th>
      <th>Age</th>
      <th>Height</th>
      <th>Weight</th>
      <th>Team</th>
      <th>NOC</th>
      <th>Games</th>
      <th>Year</th>
      <th>Season</th>
      <th>City</th>
      <th>Sport</th>
      <th>Event</th>
      <th>Medal</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>62</td>
      <td>Giovanni Abagnale</td>
      <td>M</td>
      <td>21.0</td>
      <td>198.0</td>
      <td>90.0</td>
      <td>Italy</td>
      <td>ITA</td>
      <td>2016 Summer</td>
      <td>2016</td>
      <td>Summer</td>
      <td>Rio de Janeiro</td>
      <td>Rowing</td>
      <td>Rowing Men's Coxless Pairs</td>
      <td>Bronze</td>
    </tr>
    <tr>
      <th>1</th>
      <td>65</td>
      <td>Patimat Abakarova</td>
      <td>F</td>
      <td>21.0</td>
      <td>165.0</td>
      <td>49.0</td>
      <td>Azerbaijan</td>
      <td>AZE</td>
      <td>2016 Summer</td>
      <td>2016</td>
      <td>Summer</td>
      <td>Rio de Janeiro</td>
      <td>Taekwondo</td>
      <td>Taekwondo Women's Flyweight</td>
      <td>Bronze</td>
    </tr>
  </tbody>
</table>
</div>




```python
# filtering the data frame for participants from italy.
summer[summer['Team'] == 'Italy']
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>ID</th>
      <th>Name</th>
      <th>Sex</th>
      <th>Age</th>
      <th>Height</th>
      <th>Weight</th>
      <th>Team</th>
      <th>NOC</th>
      <th>Games</th>
      <th>Year</th>
      <th>Season</th>
      <th>City</th>
      <th>Sport</th>
      <th>Event</th>
      <th>Medal</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>62</td>
      <td>Giovanni Abagnale</td>
      <td>M</td>
      <td>21.0</td>
      <td>198.0</td>
      <td>90.0</td>
      <td>Italy</td>
      <td>ITA</td>
      <td>2016 Summer</td>
      <td>2016</td>
      <td>Summer</td>
      <td>Rio de Janeiro</td>
      <td>Rowing</td>
      <td>Rowing Men's Coxless Pairs</td>
      <td>Bronze</td>
    </tr>
    <tr>
      <th>25</th>
      <td>1466</td>
      <td>Matteo Aicardi</td>
      <td>M</td>
      <td>30.0</td>
      <td>192.0</td>
      <td>102.0</td>
      <td>Italy</td>
      <td>ITA</td>
      <td>2016 Summer</td>
      <td>2016</td>
      <td>Summer</td>
      <td>Rio de Janeiro</td>
      <td>Water Polo</td>
      <td>Water Polo Men's Water Polo</td>
      <td>Bronze</td>
    </tr>
    <tr>
      <th>26</th>
      <td>1478</td>
      <td>Rosaria Aiello</td>
      <td>F</td>
      <td>27.0</td>
      <td>172.0</td>
      <td>74.0</td>
      <td>Italy</td>
      <td>ITA</td>
      <td>2016 Summer</td>
      <td>2016</td>
      <td>Summer</td>
      <td>Rio de Janeiro</td>
      <td>Water Polo</td>
      <td>Water Polo Women's Water Polo</td>
      <td>Silver</td>
    </tr>
    <tr>
      <th>58</th>
      <td>4575</td>
      <td>Oleg Antonov</td>
      <td>M</td>
      <td>28.0</td>
      <td>198.0</td>
      <td>88.0</td>
      <td>Italy</td>
      <td>ITA</td>
      <td>2016 Summer</td>
      <td>2016</td>
      <td>Summer</td>
      <td>Rio de Janeiro</td>
      <td>Volleyball</td>
      <td>Volleyball Men's Volleyball</td>
      <td>Silver</td>
    </tr>
    <tr>
      <th>80</th>
      <td>6624</td>
      <td>Diana Bacosi</td>
      <td>F</td>
      <td>33.0</td>
      <td>175.0</td>
      <td>85.0</td>
      <td>Italy</td>
      <td>ITA</td>
      <td>2016 Summer</td>
      <td>2016</td>
      <td>Summer</td>
      <td>Rio de Janeiro</td>
      <td>Shooting</td>
      <td>Shooting Women's Skeet</td>
      <td>Gold</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>1843</th>
      <td>125813</td>
      <td>Alessandro Velotto</td>
      <td>M</td>
      <td>21.0</td>
      <td>186.0</td>
      <td>85.0</td>
      <td>Italy</td>
      <td>ITA</td>
      <td>2016 Summer</td>
      <td>2016</td>
      <td>Summer</td>
      <td>Rio de Janeiro</td>
      <td>Water Polo</td>
      <td>Water Polo Men's Water Polo</td>
      <td>Bronze</td>
    </tr>
    <tr>
      <th>1851</th>
      <td>126248</td>
      <td>Luca Vettori</td>
      <td>M</td>
      <td>25.0</td>
      <td>200.0</td>
      <td>95.0</td>
      <td>Italy</td>
      <td>ITA</td>
      <td>2016 Summer</td>
      <td>2016</td>
      <td>Summer</td>
      <td>Rio de Janeiro</td>
      <td>Volleyball</td>
      <td>Volleyball Men's Volleyball</td>
      <td>Silver</td>
    </tr>
    <tr>
      <th>1852</th>
      <td>126330</td>
      <td>Giuseppe Vicino</td>
      <td>M</td>
      <td>23.0</td>
      <td>195.0</td>
      <td>95.0</td>
      <td>Italy</td>
      <td>ITA</td>
      <td>2016 Summer</td>
      <td>2016</td>
      <td>Summer</td>
      <td>Rio de Janeiro</td>
      <td>Rowing</td>
      <td>Rowing Men's Coxless Fours</td>
      <td>Bronze</td>
    </tr>
    <tr>
      <th>1858</th>
      <td>126933</td>
      <td>Elia Viviani</td>
      <td>M</td>
      <td>27.0</td>
      <td>177.0</td>
      <td>70.0</td>
      <td>Italy</td>
      <td>ITA</td>
      <td>2016 Summer</td>
      <td>2016</td>
      <td>Summer</td>
      <td>Rio de Janeiro</td>
      <td>Cycling</td>
      <td>Cycling Men's Omnium</td>
      <td>Gold</td>
    </tr>
    <tr>
      <th>1988</th>
      <td>134145</td>
      <td>Ivan Zaytsev</td>
      <td>M</td>
      <td>27.0</td>
      <td>204.0</td>
      <td>100.0</td>
      <td>Italy</td>
      <td>ITA</td>
      <td>2016 Summer</td>
      <td>2016</td>
      <td>Summer</td>
      <td>Rio de Janeiro</td>
      <td>Volleyball</td>
      <td>Volleyball Men's Volleyball</td>
      <td>Silver</td>
    </tr>
  </tbody>
</table>
<p>70 rows × 15 columns</p>
</div>




```python
# filtering for just male participants
male_players = summer[summer['Sex'] == 'M']
```


```python
# filtering for participants that are above 30.
summer[summer['Age'] >= 30]
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>ID</th>
      <th>Name</th>
      <th>Sex</th>
      <th>Age</th>
      <th>Height</th>
      <th>Weight</th>
      <th>Team</th>
      <th>NOC</th>
      <th>Games</th>
      <th>Year</th>
      <th>Season</th>
      <th>City</th>
      <th>Sport</th>
      <th>Event</th>
      <th>Medal</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>2</th>
      <td>73</td>
      <td>Luc Abalo</td>
      <td>M</td>
      <td>31.0</td>
      <td>182.0</td>
      <td>86.0</td>
      <td>France</td>
      <td>FRA</td>
      <td>2016 Summer</td>
      <td>2016</td>
      <td>Summer</td>
      <td>Rio de Janeiro</td>
      <td>Handball</td>
      <td>Handball Men's Handball</td>
      <td>Silver</td>
    </tr>
    <tr>
      <th>10</th>
      <td>690</td>
      <td>Chantal Achterberg</td>
      <td>F</td>
      <td>31.0</td>
      <td>172.0</td>
      <td>72.0</td>
      <td>Netherlands</td>
      <td>NED</td>
      <td>2016 Summer</td>
      <td>2016</td>
      <td>Summer</td>
      <td>Rio de Janeiro</td>
      <td>Rowing</td>
      <td>Rowing Women's Quadruple Sculls</td>
      <td>Silver</td>
    </tr>
    <tr>
      <th>11</th>
      <td>832</td>
      <td>Nicola Virginia Adams</td>
      <td>F</td>
      <td>33.0</td>
      <td>164.0</td>
      <td>51.0</td>
      <td>Great Britain</td>
      <td>GBR</td>
      <td>2016 Summer</td>
      <td>2016</td>
      <td>Summer</td>
      <td>Rio de Janeiro</td>
      <td>Boxing</td>
      <td>Boxing Women's Flyweight</td>
      <td>Gold</td>
    </tr>
    <tr>
      <th>13</th>
      <td>846</td>
      <td>Valerie Kasanita Adams-Vili (-Price)</td>
      <td>F</td>
      <td>31.0</td>
      <td>193.0</td>
      <td>120.0</td>
      <td>New Zealand</td>
      <td>NZL</td>
      <td>2016 Summer</td>
      <td>2016</td>
      <td>Summer</td>
      <td>Rio de Janeiro</td>
      <td>Athletics</td>
      <td>Athletics Women's Shot Put</td>
      <td>Silver</td>
    </tr>
    <tr>
      <th>23</th>
      <td>1356</td>
      <td>Christian Ahlmann</td>
      <td>M</td>
      <td>41.0</td>
      <td>189.0</td>
      <td>80.0</td>
      <td>Germany</td>
      <td>GER</td>
      <td>2016 Summer</td>
      <td>2016</td>
      <td>Summer</td>
      <td>Rio de Janeiro</td>
      <td>Equestrianism</td>
      <td>Equestrianism Mixed Jumping, Team</td>
      <td>Bronze</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>1969</th>
      <td>132899</td>
      <td>Tatyana Vladimirova Yerokhina</td>
      <td>F</td>
      <td>31.0</td>
      <td>185.0</td>
      <td>73.0</td>
      <td>Russia</td>
      <td>RUS</td>
      <td>2016 Summer</td>
      <td>2016</td>
      <td>Summer</td>
      <td>Rio de Janeiro</td>
      <td>Handball</td>
      <td>Handball Women's Handball</td>
      <td>Gold</td>
    </tr>
    <tr>
      <th>1976</th>
      <td>133130</td>
      <td>Saori Yoshida</td>
      <td>F</td>
      <td>33.0</td>
      <td>157.0</td>
      <td>55.0</td>
      <td>Japan</td>
      <td>JPN</td>
      <td>2016 Summer</td>
      <td>2016</td>
      <td>Summer</td>
      <td>Rio de Janeiro</td>
      <td>Wrestling</td>
      <td>Wrestling Women's Featherweight, Freestyle</td>
      <td>Silver</td>
    </tr>
    <tr>
      <th>1982</th>
      <td>133592</td>
      <td>Olga Sergeyevna Zabelinskaya (Sukhoruchenkova-)</td>
      <td>F</td>
      <td>36.0</td>
      <td>175.0</td>
      <td>61.0</td>
      <td>Russia</td>
      <td>RUS</td>
      <td>2016 Summer</td>
      <td>2016</td>
      <td>Summer</td>
      <td>Rio de Janeiro</td>
      <td>Cycling</td>
      <td>Cycling Women's Individual Time Trial</td>
      <td>Silver</td>
    </tr>
    <tr>
      <th>1984</th>
      <td>133685</td>
      <td>Mariel Leigh Zagunis</td>
      <td>F</td>
      <td>31.0</td>
      <td>173.0</td>
      <td>72.0</td>
      <td>United States</td>
      <td>USA</td>
      <td>2016 Summer</td>
      <td>2016</td>
      <td>Summer</td>
      <td>Rio de Janeiro</td>
      <td>Fencing</td>
      <td>Fencing Women's Sabre, Team</td>
      <td>Bronze</td>
    </tr>
    <tr>
      <th>1989</th>
      <td>134170</td>
      <td>Vasilij bogar</td>
      <td>M</td>
      <td>40.0</td>
      <td>189.0</td>
      <td>98.0</td>
      <td>Slovenia</td>
      <td>SLO</td>
      <td>2016 Summer</td>
      <td>2016</td>
      <td>Summer</td>
      <td>Rio de Janeiro</td>
      <td>Sailing</td>
      <td>Sailing Men's One Person Heavyweight Dinghy</td>
      <td>Silver</td>
    </tr>
  </tbody>
</table>
<p>348 rows × 15 columns</p>
</div>




```python
summer[summer['Height'] > 160]
```


```python
summer[(summer['Team'] == 'Italy') & (summer['Sex'] == 'M')]
```


```python
# Filtering conditions with or (|)
(summer['Medal'] == 'Gold') | (summer['Medal'] == 'Silver')
```




    0       False
    1       False
    2        True
    3       False
    4        True
            ...  
    2009     True
    2010     True
    2011     True
    2012     True
    2013    False
    Name: Medal, Length: 2014, dtype: bool




```python
# filtering for male participants that won gold or females that won silver.
summer[(summer['Sex'] == 'M') & ((summer['Medal'] == 'Gold') | (summer['Medal'] == 'Silver'))]
```




    0       False
    1       False
    2        True
    3       False
    4        True
            ...  
    2009    False
    2010    False
    2011     True
    2012     True
    2013    False
    Length: 2014, dtype: bool


