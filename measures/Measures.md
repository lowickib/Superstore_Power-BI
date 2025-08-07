## 📊 DAX Measures Documentation

### 📁 Customers

#### 📌 `Total Customers`

* Total number of unique customers based on order data.

```dax
COALESCE(
    DISTINCTCOUNT(
        DimOrders[Customer ID]
    ), 
    0
)
```



### 📁 Orders

#### 📌 `%YoY Orders Change`

* Year-over-year percentage change in total orders.

```dax
DIVIDE(
    [Total Orders Current Year] - [Total Orders Last Year],
    [Total Orders Last Year]
)
```

#### 📌 `Avg Days Between Orders`

* Average number of days between a customer's orders.

```dax
AVERAGE(
    DimCustomers[Avg Days Between Orders]
)
```

#### 📌 `Monthly Orders Target`

* Monthly target for number of orders – average of the last 3 months × 1.1.

```dax
VAR currentMonth = MAX(DimCalendar[Start of month])
VAR validMonths =
    TOPN(
        3,
        FILTER(
            ALL(DimCalendar[Start of month]),
            DimCalendar[Start of month] < currentMonth &&
           [Total Orders] > 0
        ),
        DimCalendar[Start of month],
        DESC
    )
RETURN 
    ROUNDUP(
        AVERAGEX(
        validMonths,
        [Total Orders]
    ) * 1.1, 0)
```

#### 📌 `Orders 3M Moving Average`

* 3-month moving average of orders.

```dax
DIVIDE(
    CALCULATE(
    [Total orders],
    DATESINPERIOD(DimCalendar[Date], MAX(DimCalendar[Date]), -3, MONTH)
    ),
    3
)
```

#### 📌 `Orders per Customer`

* Number of orders per customer.

```dax
DIVIDE(
    [Total orders],
    [Total Customers],
    0
)
```

#### 📌 `Orders Rolling 12M`

* Total orders in the last 12 months.

```dax
CALCULATE(
    [Total Orders], 
    DATESINPERIOD(DimCalendar[Date], MAX(DimCalendar[Date]), -12, MONTH)
)
```


#### 📌 `Orders Target Gap`

* Difference between the target and the actual number of orders.

```dax
[Monthly Orders Target] - [Total Orders]
```

#### 📌 `Prev Month Total Orders`

* Number of orders in the previous month.

```dax
CALCULATE(
    [Total Orders],
    DATEADD(
        DimCalendar[Date],
        -1,
        MONTH
    )
)
```





#### 📌 `Total Orders`

* Total number of orders.

```dax
COALESCE(
    DISTINCTCOUNT(
        FactSales[Order ID]
    ), 0
)
```

#### 📌 `Total Orders Current Year`

* Total number of orders in the current year.

```dax
CALCULATE(
    [Total Orders],
    FILTER(
        ALL(DimCalendar),
        DimCalendar[Year] = MAX(DimCalendar[Year])
    )
)
```

#### 📌 `Total Orders Last Year`

* Total number of orders in the previous year.

```dax
CALCULATE(
    [Total Orders],
    FILTER(
        ALL(DimCalendar),
        DimCalendar[Year] = MAX(DimCalendar[Year]) - 1
    )
)
```

#### 📌 `YTD Orders`

* Year-to-date total number of orders.

```dax
CALCULATE(
    [Total Orders],
    DATESYTD(
        DimCalendar[Date]
    )
)
```


### 📁 Profit

#### 📌 `%YoY Profit Change`

* Year-over-year percentage change in total profit.

```dax
DIVIDE(
    [Total Profit Current Year] - [Total Profit Last Year],
    [Total Profit Last Year]
)
```

#### 📌 `Monthly Profit Target`

* Monthly target for profit – average of the last 3 valid months × 1.1.

```dax
VAR currentMonth = MAX(DimCalendar[Start of month])
VAR validMonths =
    TOPN(
        3,
        FILTER(
            ALL(DimCalendar[Start of month]),
            DimCalendar[Start of month] < currentMonth &&
           [Total Profit] > 0
        ),
        DimCalendar[Start of month],
        DESC
    )
RETURN 
    AVERAGEX(
        validMonths,
        [Total Profit]
    ) * 1.1
```

#### 📌 `Prev Month Total Profit`

* Total profit in the previous month.

```dax
CALCULATE(
    [Total Profit],
    DATEADD(
        DimCalendar[Date],
        -1,
        MONTH
    )
)
```


#### 📌 `Profit 3M Moving Average`

* 3-month moving average of profit.

```dax
DIVIDE(
    CALCULATE(
    [Total Profit],
    DATESINPERIOD(DimCalendar[Date], MAX(DimCalendar[Date]), -3, MONTH)
    ),
    3
)
```


#### 📌 `Profit per Customer`

* Average profit per customer.

```dax
DIVIDE(
    [Total Profit],
    [Total Customers],
    0
)
```

#### 📌 `Profit per Order`

* Average profit per order.

```dax
DIVIDE(
    [Total Profit],
    [Total Orders],
    0
)
```

#### 📌 `Profit Rolling 12M`

* Total profit in the last 12 months.

```dax
CALCULATE(
    [Total Profit], 
    DATESINPERIOD(DimCalendar[Date], MAX(DimCalendar[Date]), -12, MONTH)
)
```



#### 📌 `Profit Target Gap`

* Gap between monthly target and actual profit.

```dax
[Monthly Profit Target] - [Total Profit]
```




#### 📌 `Top 30% of Customers Profit Threshold`

* Value above which the top 30% of customers are contributing in total profit.

```dax
PERCENTILEX.INC(
    ALL(DimCustomers),
    [Total Profit],
    0.7)
```


#### 📌 `Top N Profit`

* Returns profit only for top N selected states or cities.

```dax
VAR n = 'Top N Territory'[Top N Territory Value]

VAR topCities =
    TOPN(n, ALLSELECTED(DimTerritory[City]), [Total Profit by City])

VAR topCitiesInState =
    TOPN(n, FILTER(
        ALLSELECTED(DimTerritory[State], DimTerritory[City]),
        DimTerritory[State] = MAX(DimTerritory[State])
        ), [Total Profit by City])

VAR topStates =
    TOPN(n, ALLSELECTED(DimTerritory[State]), [Total Profit by State])

RETURN
    SWITCH(
        TRUE(),
        ISINSCOPE(DimTerritory[City]) && NOT(ISINSCOPE(DimTerritory[State])),
            CALCULATE([Total Profit by City], KEEPFILTERS(topCities)),

        ISINSCOPE(DimTerritory[City]) && (ISINSCOPE(DimTerritory[State])) && DISTINCTCOUNT(DimTerritory[State]) = 1,
            CALCULATE([Total Profit by City], KEEPFILTERS(topCitiesInState)),

        ISINSCOPE(DimTerritory[State]) && NOT(ISINSCOPE(DimTerritory[City])),
            CALCULATE([Total Profit by State], KEEPFILTERS(topStates)),

        BLANK()
    )
```



#### 📌 `Total Profit`

* Total profit from all sales.

```dax
COALESCE(
    SUM(
        FactSales[Profit]
    ), 0
)
```


#### 📌 `Total Profit by State`

* Total profit by state (ignores city filter).

```dax
CALCULATE(
    SUM(
        FactSales[Profit]),
    REMOVEFILTERS(DimTerritory[City])
)
```

#### 📌 `Total Profit by City`

* Total profit by city (ignores state filter).

```dax
CALCULATE(
    SUM(
        FactSales[Profit]),
    REMOVEFILTERS(DimTerritory[State])
)
```





#### 📌 `Total Profit Current Year`

* Total profit in the current year.

```dax
CALCULATE(
    [Total Profit],
    FILTER(
        ALL(DimCalendar),
        DimCalendar[Year] = MAX(DimCalendar[Year])
    )
)
```

#### 📌 `Total Profit Last Year`

* Total profit in the previous year.

```dax
CALCULATE(
    [Total Profit],
    FILTER(
        ALL(DimCalendar),
        DimCalendar[Year] = MAX(DimCalendar[Year]) - 1
    )
)
```


#### 📌 `YTD Profit`

* Year-to-date total profit.

```dax
CALCULATE(
    [Total Profit],
    DATESYTD(
        DimCalendar[Date]
    )
)
```


### 📁 Sales

#### 📌 `%YoY Sales Change`

* Year-over-year percentage change in total sales.

```dax
DIVIDE(
    [Total Sales Current Year] - [Total Sales Last Year],
    [Total Sales Last Year]
)
```

#### 📌 `Monthly Sales Target`

* Monthly target for sales – average of the last 3 valid months × 1.1.

```dax
VAR currentMonth = MAX(DimCalendar[Start of month])
VAR validMonths =
    TOPN(
        3,
        FILTER(
            ALL(DimCalendar[Start of month]),
            DimCalendar[Start of month] < currentMonth &&
           [Total Sales] > 0
        ),
        DimCalendar[Start of month],
        DESC
    )
RETURN 
    AVERAGEX(
        validMonths,
        [Total Sales]
    ) * 1.1
```

#### 📌 `Prev Month Total Sales`

* Total sales in the previous month.

```dax
CALCULATE(
    [Total Sales],
    DATEADD(
        DimCalendar[Date],
        -1,
        MONTH
    )
)
```

#### 📌 `Sales 3M Moving Average`

* 3-month moving average of sales.

```dax
DIVIDE(
    CALCULATE(
    [Total Sales],
    DATESINPERIOD(DimCalendar[Date], MAX(DimCalendar[Date]), -3, MONTH)
    ),
    3
)
```

#### 📌 `Sales per Customer`

* Average sales per customer.

```dax
DIVIDE(
    [Total Sales],
    [Total Customers],
    0
)
```

#### 📌 `Sales per Order`

* Average sales per order.

```dax
DIVIDE(
    [Total Sales],
    [Total Orders],
    0
)
```

#### 📌 `Sales Rolling 12M`

* Total sales in the last 12 months.

```dax
CALCULATE(
    [Total Sales], 
    DATESINPERIOD(DimCalendar[Date], MAX(DimCalendar[Date]), -12, MONTH)
)
```


#### 📌 `Sales Target Gap`

* Gap between monthly target and actual sales.

```dax
[Monthly Sales Target] - [Total Sales]
```



#### 📌 `Top 30% of Customers Sales Threshold`

* Value above which the top 30% of customers are contributing in total sales.

```dax
PERCENTILEX.INC(
    ALL(DimCustomers),
    [Total Sales],
    0.7)
```

#### 📌 `Top N Sales`

* Returns sales only for top N selected states or cities.

```dax
VAR n = 'Top N Territory'[Top N Territory Value]

VAR topCities =
    TOPN(n, ALLSELECTED(DimTerritory[City]), [Total Sales by City])

VAR topCitiesInState =
    TOPN(n, FILTER(
        ALLSELECTED(DimTerritory[State], DimTerritory[City]),
        DimTerritory[State] = MAX(DimTerritory[State])
        ), [Total Sales by City])

VAR topStates =
    TOPN(n, ALLSELECTED(DimTerritory[State]), [Total Sales by State])

RETURN
    SWITCH(
        TRUE(),
        ISINSCOPE(DimTerritory[City]) && NOT(ISINSCOPE(DimTerritory[State])),
            CALCULATE([Total Sales by City], KEEPFILTERS(topCities)),

        ISINSCOPE(DimTerritory[City]) && (ISINSCOPE(DimTerritory[State])) && DISTINCTCOUNT(DimTerritory[State]) = 1,
            CALCULATE([Total Sales by City], KEEPFILTERS(topCitiesInState)),

        ISINSCOPE(DimTerritory[State]) && NOT(ISINSCOPE(DimTerritory[City])),
            CALCULATE([Total Sales by State], KEEPFILTERS(topStates)),

        BLANK()
    )
```


#### 📌 `Total Sales`

* Total sales from all sales.

```dax
COALESCE(
    SUM(
        FactSales[Sales]
    ), 0
)
```

#### 📌 `Total Sales by State`

* Total sales by state (ignores city filter).

```dax
CALCULATE(
    SUM(
        FactSales[Sales]),
    REMOVEFILTERS(DimTerritory[City])
)
```

#### 📌 `Total Sales by City`

* Total sales by city (ignores state filter).

```dax
CALCULATE(
    SUM(
        FactSales[Sales]),
    REMOVEFILTERS(DimTerritory[State])
)
```




#### 📌 `Total Sales Current Year`

* Total sales in the current year.

```dax
CALCULATE(
    [Total Sales],
    FILTER(
        ALL(DimCalendar),
        DimCalendar[Year] = MAX(DimCalendar[Year])
    )
)
```

#### 📌 `Total Sales Last Year`

* Total sales in the previous year.

```dax
CALCULATE(
    [Total Sales],
    FILTER(
        ALL(DimCalendar),
        DimCalendar[Year] = MAX(DimCalendar[Year]) - 1
    )
)
```

#### 📌 `YTD Sales`

* Year-to-date total sales.

```dax
CALCULATE(
    [Total Sales],
    DATESYTD(
        DimCalendar[Date]
    )
)
```



### 📁 Slicers

#### 📌 `Products Rank by Selected Measure`

* Ranks products dynamically based on the selected KPI measure (Orders, Profit, or Sales).

```dax
SWITCH(
    TRUE,
    SELECTEDVALUE('KPI Measures'[KPI Measures Fields]) = "'Measures Table'[Total Orders]",
    RANKX(
        ALLSELECTED(DimProducts), 
        [Total Orders], , 
        DESC),
    SELECTEDVALUE('KPI Measures'[KPI Measures Fields]) = "'Measures Table'[Total Profit]",
    RANKX(
        ALLSELECTED(DimProducts), 
        [Total Profit], , 
        DESC),
    SELECTEDVALUE('KPI Measures'[KPI Measures Fields]) = "'Measures Table'[Total Sales]",
    RANKX(
        ALLSELECTED(DimProducts), 
        [Total Sales], ,
        DESC)
)
```

#### 📌 `Products Top N by Selected Measure`

* Returns the product ranking if it is within the top N based on the selected KPI; otherwise returns 0.

```dax
VAR ranking =
    SWITCH(
        TRUE,
        SELECTEDVALUE('KPI Measures'[KPI Measures Fields]) = "'Measures Table'[Total Orders]",
        RANKX(
            ALLSELECTED(DimProducts), 
            [Total Orders], , 
            DESC),
        SELECTEDVALUE('KPI Measures'[KPI Measures Fields]) = "'Measures Table'[Total Profit]",
        RANKX(
            ALLSELECTED(DimProducts), 
            [Total Profit], , 
            DESC),
        SELECTEDVALUE('KPI Measures'[KPI Measures Fields]) = "'Measures Table'[Total Sales]",
        RANKX(
            ALLSELECTED(DimProducts), 
            [Total Sales], ,
            DESC)
    )
RETURN
    IF(ranking <= 'Top N Products'[Top N Products Value], 
        ranking, 
        0
    )
```

### 📁 Titles

#### 📌 `Customer RFM Segment Labels`

* Returns the RFM segment name for the selected customer.

```dax
SELECTEDVALUE(
    DimCustomers[RFM Customer Segment]
)
```

#### 📌 `Customer RFM Segment Placeholder`

* Dummy measure to support dynamic titles based on slicers.

```dax
0
```

#### 📌 `Dummy Title`

* Blank placeholder used in report visuals for spacing or toggling purposes.

```dax
""
```

#### 📌 `Top N Products by Selected Measure - Title`

* Dynamic title showing selected Top N products by KPI measure.

```dax
SWITCH(
    TRUE,
    SELECTEDVALUE('KPI Measures'[KPI Measures Fields]) = "'Measures Table'[Total Orders]",
    "Top " &'Top N Products'[Top N Products Value] & " Products by Total Orders",
    SELECTEDVALUE('KPI Measures'[KPI Measures Fields]) = "'Measures Table'[Total Profit]",
    "Top " &'Top N Products'[Top N Products Value] & " Products by Total Profit",
    SELECTEDVALUE('KPI Measures'[KPI Measures Fields]) = "'Measures Table'[Total Sales]",
    "Top " &'Top N Products'[Top N Products Value] & " Products by Total Sales"
)
```

#### 📌 `Top 25 Products by Selected Measure - Title`

* Static title for Top 25 products visual, changing dynamically by KPI.

```dax
SWITCH(
    TRUE,
    SELECTEDVALUE('KPI Measures'[KPI Measures Fields]) = "'Measures Table'[Total Orders]",
    "Top 25 Products by Total Orders",
    SELECTEDVALUE('KPI Measures'[KPI Measures Fields]) = "'Measures Table'[Total Profit]",
    "Top 25 Products by Total Profit",
    SELECTEDVALUE('KPI Measures'[KPI Measures Fields]) = "'Measures Table'[Total Sales]",
    "Top 25 Products by Total Sales"
)
```

#### 📌 `Is Slicer Active`

* Indicates whether a key slicer (Year, Region, or Category) is active.

```dax
VAR yearSlicer = ISFILTERED(DimCalendar[Year])
VAR regionSlicer = ISFILTERED(DimTerritory[Region])
VAR categorySlicer = ISFILTERED(DimProducts[Category])
RETURN
    IF(
        yearSlicer || regionSlicer || categorySlicer,
        1,
        0
    )
```

#### 📌 `Active Slicers Message`

* Returns a multi-line label listing all active slicer selections.

```dax
VAR yearSlicerValues =
    IF(ISFILTERED(DimCalendar[Year]),
        CONCATENATE("Year: ", CONCATENATEX(VALUES(DimCalendar[Year]), DimCalendar[Year], ", ")),
        ""
    )
VAR regionSlicerValues =
    IF(ISFILTERED(DimTerritory[Region]),
        CONCATENATE("Region: ", CONCATENATEX(VALUES(DimTerritory[Region]), DimTerritory[Region], ", ")),
        ""
    )
VAR categorySlicerValues =
    IF(ISFILTERED(DimProducts[Category]),
        CONCATENATE("Category: ", CONCATENATEX(VALUES(DimProducts[Category]), DimProducts[Category], ", ")),
        ""
    )
RETURN
    IF(
        (yearSlicerValues = "") && (regionSlicerValues = "") && (categorySlicerValues = ""),
        "No Active Slicers Applied",
        "Applied Slicers - " & yearSlicerValues & UNICHAR(10) & regionSlicerValues & UNICHAR(10) & categorySlicerValues
    )
```



#### 📌 `Selected Measure by Day Name - Title`

* Title for chart displaying selected measure broken down by day of the week.

```dax
SWITCH(
    TRUE,
    SELECTEDVALUE('KPI Measures Time-Based Analysis'[Group Name]) = "Total Orders",
    "Total Orders by Day of Week",
    SELECTEDVALUE('KPI Measures Time-Based Analysis'[Group Name]) = "Total Profit",
    "Total Profit by Day of Week",
    SELECTEDVALUE('KPI Measures Time-Based Analysis'[Group Name]) = "Total Sales",
    "Total Sales by Day of Week"
)
```

#### 📌 `Selected Measure (Totals and MA) by Month - Title`

* Title showing both total and 3-month moving average by month.

```dax
SWITCH(
    TRUE,
    SELECTEDVALUE('KPI Measures Time-Based Analysis'[Group Name]) = "Total Orders",
    "Total Orders and 3M Moving Average by Month",
    SELECTEDVALUE('KPI Measures Time-Based Analysis'[Group Name]) = "Total Profit",
    "Total Profit and 3M Moving Average by Month",
    SELECTEDVALUE('KPI Measures Time-Based Analysis'[Group Name]) = "Total Sales",
    "Total Sales and 3M Moving Average by Month"
)
```

#### 📌 `Selected Measure (RT) by Month - Title`

* Title showing 12-month rolling total for the selected measure.

```dax
SWITCH(
    TRUE,
    SELECTEDVALUE('KPI Measures Time-Based Analysis'[Group Name]) = "Total Orders",
    "Monthly 12-Month Rolling Orders Total",
    SELECTEDVALUE('KPI Measures Time-Based Analysis'[Group Name]) = "Total Profit",
    "Monthly 12-Month Rolling Profit Total",
    SELECTEDVALUE('KPI Measures Time-Based Analysis'[Group Name]) = "Total Sales",
    "Monthly 12-Month Rolling Sales Total"
)
```

#### 📌 `Selected Measure (YTD) by Month - Title`

* Title for year-to-date chart by month based on selected KPI.

```dax
SWITCH(
    TRUE,
    SELECTEDVALUE('KPI Measures Time-Based Analysis'[Group Name]) = "Total Orders",
    "Total Orders YTD",
    SELECTEDVALUE('KPI Measures Time-Based Analysis'[Group Name]) = "Total Profit",
    "Total Profit YTD",
    SELECTEDVALUE('KPI Measures Time-Based Analysis'[Group Name]) = "Total Sales",
    "Total Sales YTD"
)
```

#### 📌 `Top N Locations by Selected Measure - Title`

* Dynamic title for Top N locations visual, depending on selected KPI.

```dax
SWITCH(
    TRUE,
    SELECTEDVALUE('KPI Measures Territory'[KPI Measures Territory Fields]) = "'Measures Table'[Top N Profit]",
    "Top " &'Top N Territory'[Top N Territory Value] & " Locations by Total Profit",
    SELECTEDVALUE('KPI Measures Territory'[KPI Measures Territory Fields]) = "'Measures Table'[Top N Sales]",
    "Top " &'Top N Territory'[Top N Territory Value] & " Locations by Total Sales"
)
```

#### 📌 `Day Name Labels`

* Returns the name of the day from calendar context for use in titles.

```dax
SELECTEDVALUE(
    DimCalendar[Day name]
)
```

#### 📌 `Day Name Placeholder`

* Placeholder measure for dynamic title visuals based on day name.

```dax
0
```
