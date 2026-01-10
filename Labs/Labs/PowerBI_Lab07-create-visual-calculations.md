---
lab:
    title: 'Tworzenie obliczeń wizualnych w Power BI Desktop'
---

# Tworzenie obliczeń wizualnych w Power BI Desktop

## Opis laboratorium

W tym laboratorium utworzysz obliczenia wizualne z użyciem DAX (Data Analysis Expressions).

W tym laboratorium dowiesz się jak:

- tworzyć i edytować obliczenia wizualne,
- używać funkcji PREVIOUS(), RUNNINGSUM() i MOVINGAVERAGE() do porównywania danych między latami,
- stosować opcjonalny parametr Axis podczas porównania,
- stosować parametr Reset, aby dostosować kalkulacje narastające przy wielu poziomach osi.

**To laboratorium zajmie około 30 minut.**

---

## Rozpoczęcie

Pobierz paczkę ZIP:

`07-visual-calculations.zip`

Rozpakuj do folderu:

**C:\Users\Student\Downloads\07-visual-calculations**

Otwórz plik:

**07-Starter-Sales Analysis.pbix**

> Możesz zobaczyć okno logowania – kliknij Cancel. Jeśli będzie pytanie o Apply changes, wybierz Apply Later.

---

## Utwórz wykres kolumnowy

Celem jest wykres kolumnowy pokazujący sprzedaż, koszt i zysk z możliwością porównań rok-do-roku.

1. W panelu **Visualizations** wybierz **Clustered bar chart**.

2. Z tabeli **Date**, przenieś **Year** do **Y-axis**.

3. Z tabeli **Sales**, przenieś **Sales** i **Cost** do **X-axis**.

> PBI automatycznie sumuje pola liczbowe.

4. Z menu sortowania wybierz sortowanie po **Year** rosnąco.

---

## Dodaj obliczenia

1. Zaznacz wykres, wybierz **New visual calculation**.

2. Wpisz:

```DAX
Profit = [Sum of Sales] - [Sum of Cost]
Na dole pojawi się informacja o nowym obliczeniu (kolumna Profit).

W rozwijanym menu New visual calculation wybierz Versus previous, zamień [Field] na [Profit] (dwa razy).

Porównanie wartości z poprzednim rokiem.

Następnie wybierz Running sum, zamień [Field] na [Profit].

Running sum to narastająca suma wartości.

Wybierz Moving average, zamień [Field] na [Profit] i WindowSize na 2.

Moving average = średnia z dwóch kolejnych wartości.

W panelu osi ukryj Sum of Sales, Sum of Cost i Profit, klikając ikonę oka.

Dodaj Running sum oraz Moving average do Tooltips.

Wykres zawiera teraz: Sales, Cost, Profit, Profit vs previous, tooltips Running sum i Moving average.

Utwórz wizual macierzowy
Celem jest porównanie sprzedaży kategorii z pierwszym rokiem.

Dodaj nową stronę raportu → Page 2.

Dodaj wizual Matrix.

Ustaw pola:

Rows: Product | Category

Columns: Date | Year

Values: Sales | Sales

Dodaj obliczenia do macierzy
Wybierz New visual calculation.

Wpisz:

DAX
Skopiuj kod
Versus first = [Sum of Sales] - FIRST([Sum of Sales])
Zauważ różnice w stosunku do pierwszego wiersza.

Zmień wyrażenie na:

DAX
Skopiuj kod
Versus first = [Sum of Sales] - FIRST([Sum of Sales], ROWS)
Nic się nie zmieni – ROWS to domyślny parametr.

Zmień ROWS na COLUMNS:

DAX
Skopiuj kod
Versus first = [Sum of Sales] - FIRST([Sum of Sales], COLUMNS)
Teraz porównujesz każdy rok do pierwszego roku.

Utwórz wykres liniowy
Dodaj stronę → Page 3.

Dodaj Line chart.

Pola:

X-axis: Date | Year i Date | Quarter

Y-axis: Sales | Sales

Dodaj narastającą sumę
W New visual calculation wybierz Running sum.

Zastąp [Field] → [Sum of Sales].

Restart narastania w nowym roku
Zmień:

DAX
Skopiuj kod
Running sum = RUNNINGSUM([Sum of Sales], HIGHESTPARENT)
Teraz narastanie zaczyna się od nowa w każdym roku fiskalnym.

Koniec laboratorium
Możesz zapisać raport, ale nie jest to wymagane.

File → Save As

Browse this device

Wybierz nazwę

Save

Apply jeśli pytanie o zmiany

Zamknij Power BI Desktop.