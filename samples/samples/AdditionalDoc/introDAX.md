# Ściąga z języka DAX — szybki przewodnik

Krótki, praktyczny zestaw najważniejszych elementów języka DAX używanych w Power BI.

---

## 1. Podstawy składni

**Miara:**
```DAX
Total Sales = SUM ( Sales[Sales] )
```

**Kolumna obliczeniowa:**
```DAX
Year =
"FY" & YEAR('Date'[Date]) + IF(MONTH('Date'[Date]) > 6, 1)
```

**Tabela obliczeniowa:**
```DAX
Date = CALENDARAUTO(6)
```

**Zmienne:**
```DAX
Avg Price =
VAR p = AVERAGE(Sales[Unit Price])
RETURN p
```

---

## 2. Konteksty DAX

**Kontekst wiersza:** dotyczy pojedynczego wiersza, występuje w kolumnach i iteratorach.

**Kontekst filtru:** zbiór filtrów, które wpływają na wynik miary.

**Przejście kontekstu:** `CALCULATE` zmienia kontekst filtru.

---

## 3. Miary vs Kolumny vs Tabele

- **Miary** – obliczane dynamicznie, najbardziej optymalne.
- **Kolumny** – materializowane, wykorzystywane w relacjach i sortowaniu.
- **Tabele** – stosowane do kalendarzy, słowników, modelowania semantycznego.

---

## 4. CALCULATE – modyfikowanie kontekstu

```DAX
CALCULATE(<wyrażenie>, <filtry>)
```

**Usuwanie filtrów:**
```DAX
All Sales =
CALCULATE(SUM(Sales[Sales]), REMOVEFILTERS(Sales))
```

**Zachowanie filtrów:**
```DAX
Keep Bikes =
CALCULATE([Total Sales], KEEPFILTERS(Product[Category] = "Bikes"))
```

**Użycie relacji nieaktywnej:**
```DAX
Sales by Ship Date =
CALCULATE([Total Sales], USERELATIONSHIP('Date'[Date], Sales[ShipDate]))
```

**Zmiana kierunku relacji:**
```DAX
CrossFilter Both =
CALCULATE([Total Sales],
          CROSSFILTER(Product[ProductKey], Sales[ProductKey], BOTH))
```

---

## 5. Iteratory

```DAX
Total Cost =
SUMX(Sales, Sales[Quantity] * Sales[Unit Cost])
```

```DAX
Avg by Product =
AVERAGEX(VALUES(Product[Product]), [Total Sales])
```

---

## 6. Wzorce DAX

### % of All:
```DAX
% of All =
DIVIDE([Total Sales],
       CALCULATE([Total Sales], REMOVEFILTERS(ALLSELECTED(Region))))
```

### % of Country:
```DAX
% of Country =
IF(
    ISINSCOPE(Region[Region]),
    DIVIDE(
        [Total Sales],
        CALCULATE([Total Sales], REMOVEFILTERS(Region[Region]))
    )
)
```

### Running total:
```DAX
Sales YTD =
CALCULATE([Total Sales],
          FILTER(ALL('Date'[Date]), 'Date'[Date] <= MAX('Date'[Date])))
```

### YoY:
```DAX
Sales YoY = CALCULATE([Total Sales], DATEADD('Date'[Date], -1, YEAR))
```

---

## 7. Time Intelligence

```DAX
Sales YTD = TOTALYTD([Total Sales], 'Date'[Date], "06/30")
```

```DAX
Same Period Last Year =
CALCULATE([Total Sales], SAMEPERIODLASTYEAR('Date'[Date]))
```

---

## 8. Warunki i wartości puste

```DAX
Margin % = DIVIDE([Profit], [Total Sales])
```

```DAX
Margin % No Blank = COALESCE([Margin %], 0)
```

```DAX
Bucket =
SWITCH(TRUE(),
    [Margin %] >= 0.5, "A",
    [Margin %] >= 0.3, "B",
    [Margin %] >= 0.1, "C",
    "D"
)
```

---

## 9. Dobre praktyki

- Używaj **DIVIDE** zamiast `/`.
- Używaj **VAR** dla czytelności.
- Zawężaj ALL/REMOVEFILTERS tylko do potrzebnych kolumn.
- Unikaj FORMAT() w obliczeniach.
- Ukrywaj kolumny pomocnicze (`IsHidden = True`).

---

## 10. Najczęstsze wzorce

```DAX
Only Detail =
IF(NOT HASONEVALUE(Product[Product]), BLANK(), [Total Sales])
```

```DAX
Title =
"Sales – Country: " & SELECTEDVALUE(Region[Country], "All")
```

```DAX
All Products Sales =
CALCULATE([Total Sales], REMOVEFILTERS(Product))
```

---
