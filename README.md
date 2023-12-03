# Power BI Notes




### DAX Formulas

By using Data Analysis Expressions (DAX), you can add three types of calculations to your semantic model:

- Calculated tables
- Calculated columns
- Measures



Power BI models only allow one active relationship between tables, which in the model diagram is indicated as a solid line.



#### Calculated tables

Calculated tables can be useful in various scenarios:

- Date tables = to apply special time filters known as time intelligence
- Role-playing dimensions = when two model tables have multiple relationships
- What-if analysis = allow report users to select or filter by values that are stored in the calculated table

> A calculated table can't connect to external data, always imported.

It increases the model storage size 



#### Calculated columns

The formula is evaluated for each table row and it returns a single value.

The formula is evaluated when the semantic model is refreshed or table is queried.

![dax-fields-pane-calculated-column-ss](.\images\dax-fields-pane-calculated-column-ss.png)

#### Measures

Measures are evaluated at query time. Their results are never stored in the model.

Measures are evaluated at query time



**Ship Date** calculated table that duplicates the **Date** table data

```
Ship Date = 'Date'
```

Table References

the table name is enclosed within single quotation marks



Column References

the column name must be enclosed within square brackets preceding it with its table name

```
Revenue = SUM(Sales[Sales Amount])
```



Measure references

the measure name must be enclosed within square brackets

```
Profit = [Revenue] - [Cost]
```



```
Revenue YoY % =
DIVIDE(
    [Revenue]
        - CALCULATE(
            [Revenue],
            SAMEPERIODLASTYEAR('Date'[Date])
    ),
    CALCULATE(
        [Revenue],
        SAMEPERIODLASTYEAR('Date'[Date])
    )
)
```



DAX Data Types

Model data types aren't the same as DAX data types, though a direct relationship exists between them.

![dax-data-types.png](images\dax-data-types.png)

BLANK data type

The BLANK data type deserves a special mention. DAX uses BLANK for both database NULL and for blank cells in Excel. BLANK doesn't mean zero. Perhaps it might be simpler to think of it as the *absence of a value*.



### Work with DAX functions

