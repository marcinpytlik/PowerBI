---
lab:
    title: 'Analiza danych w Power BI'
---

# Analiza danych w Power BI

## Opis laboratorium

W tym laboratorium utworzysz raport **Sales Exploration**, wykorzystując animowane wykresy rozrzutu (scatter chart) oraz prognozowanie (forecasting).

Poznasz:

- tworzenie animowanego scatter chart,
- używanie wykresu do prognozowania wartości.

**Szacowany czas: 30 minut.**

---

## Rozpoczęcie

Pobierz ZIP:

`10-perform-analytics.zip`

Rozpakuj do:

**C:\Users\Student\Downloads\10-perform-analytics**

Otwórz:

**10-Starter-Sales Analysis.pbix**

> Podczas ładowania może pokazać się logowanie → wybierz Cancel. Zamknij inne okna. Apply Later jeśli pytanie o zmiany.

---

# Utwórz animowany Scatter Chart

1. Dodaj nową stronę → **Scatter Chart**
2. Dodaj wizual **Scatter Chart**
3. Ustaw pełną szerokość strony

> Scatter można animować, gdy dodasz pole do **Play Axis**

4. Pola:
   - X: `Sales | Sales`
   - Y: `Sales | Profit Margin`
   - Legend: `Reseller | Business Type`
   - Size: `Sales | Quantity`
   - Play Axis: `Date | Quarter`

5. W Filters → Filters on this page → dodaj `Product | Category`
6. Filtr → Bikes

7. Naciśnij przycisk **Play**  

Zobacz animację od FY2018 Q1 do FY2020 Q4.

> Każdy bąbelek = typ resellera.  
> Wielkość = wolumen (quantity)  
> Poziom = sprzedaż  
> Wysokość = marża

8. Zaznacz dowolny bubble – zobacz ślad czasowy
9. Zmień filtr na Clothing → zobacz różnicę
10. Zapisz plik

---

# Utwórz prognozę

1. Dodaj stronę → **Forecast**
2. Dodaj wizual **Line Chart**
3. Pola:
   - X-axis: `Date | Date`
   - Y-axis: `Sales | Sales`

4. Filters → dodaj `Date | Year`
5. Filtruj po: **FY2019**, **FY2020**
6. Dodaj też `Product | Category` → filtr Bikes

> Aby budować forecast, potrzebujemy minimum dwóch cykli danych (np. 2 lata)

7. Visualizations → Analytics pane
8. Rozwiń Forecast
9. Forecast → ON

10. Ustaw:
    - Units: Months
    - Forecast length: 1 month
    - Seasonality: 365
    - Confidence interval: 80%
    - Apply

Wizual pokaże przedłużenie o jeden miesiąc poza dane historyczne.

> Szare wypełnienie = przedział niepewności

> Jeśli znasz sezonowość (np. roczną), ustaw liczbę dni, miesięcy, tygodni itp.

11. Zmień filtr na Clothing → porównaj wynik prognozy

---

# Koniec laboratorium

Możesz zapisać, ale nie jest to obowiązkowe.

1. File → Save As  
2. Browse  
3. Nadaj nazwę  
4. Zapisz jako PBIX  
5. Apply (jeśli zapyta)  
6. Zamknij Power BI Desktop