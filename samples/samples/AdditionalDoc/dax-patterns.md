# DAX Patterns – SQLManiak Turbo Ściąga

## Rolling 12 Months (R12)
```DAX
R12 Sales =
CALCULATE(
    SUM(Sales[Sales]),
    DATESINPERIOD('Date'[Date], MAX('Date'[Date]), -12, MONTH)
)
```

## Year-over-Year (YoY)
```DAX
YoY Growth =
DIVIDE(
    [Total Sales] - CALCULATE([Total Sales], DATEADD('Date'[Date], -1, YEAR)),
    CALCULATE([Total Sales], DATEADD('Date'[Date], -1, YEAR))
)
```

## Month-over-Month (MoM)
```DAX
MoM =
DIVIDE(
    [Total Sales] - CALCULATE([Total Sales], DATEADD('Date'[Date], -1, MONTH)),
    CALCULATE([Total Sales], DATEADD('Date'[Date], -1, MONTH))
)
```

## Ranking
```DAX
Sales Rank =
RANKX(
    ALL('Salesperson'),
    [Total Sales],
    ,
    DESC,
    Dense
)
```

## Percent of Total
```DAX
Sales % Total =
DIVIDE(
    [Total Sales],
    CALCULATE([Total Sales], ALL(Sales))
)
```

## Many-to-Many Bridge Pattern
```DAX
Sales Via Bridge =
CALCULATE(
    [Total Sales],
    CROSSFILTER(Bridge[Key], Fact[Key], Both)
)
```

## Dynamic Segmentation (ABC)
```DAX
Segment =
SWITCH(
    TRUE(),
    [Total Sales] >= 100000, "A",
    [Total Sales] >= 30000, "B",
    "C"
)
```

## Parent-Child Hierarchy
```DAX
Path =
PATH(Employee[EmployeeID], Employee[ManagerID])
```
