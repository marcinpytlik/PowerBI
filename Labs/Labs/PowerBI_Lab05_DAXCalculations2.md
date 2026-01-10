# Modyfikowanie kontekstu filtru DAX w Power BI

## Opis laboratorium

W tym laboratorium utworzysz miary za pomocą wyrażeń DAX, które modyfikują kontekst filtru przy użyciu funkcji CALCULATE.  
Celem jest zrozumienie, jak zmiana kontekstu filtru wpływa na wyniki obliczeń.

**Czas ukończenia:** około 30 minut.

---

# Rozpoczęcie

Pobierz materiały:  
05-modify-dax-filter-context.zip

Rozpakuj do folderu:  
`C:\Users\Student\Downloads\05-modify-dax-filter-context`

Otwórz plik: **05-Starter-Sales Analysis.pbix**

**Uwaga:**  
- jeśli pojawi się okno logowania → wybierz **Anuluj**  
- zamknij inne okna informacyjne  
- jeśli pojawi się monit o zastosowanie zmian → wybierz **Zastosuj później**

---

# Tworzenie wizualizacji macierzy

1. Utwórz nową stronę raportu (**Strona 3**).
2. Dodaj wizualizację **macierzy**.
3. Rozciągnij ją na całą stronę.
4. W okienku Dane przeciągnij: **Region → Regions**.
5. Dodaj pole **Sales → Sales** do Wartości.
6. Rozwiń całą hierarchię (podwójna rozwidlona strzałka).
7. W formatowaniu znajdź **Układ → Tabelaryczny**.

---

# Modyfikowanie kontekstu filtru

## Miara 1 — Sales All Region

```DAX
Sales All Region =
CALCULATE(
    SUM(Sales[Sales]),
    REMOVEFILTERS(Region)
)
```

Dodaj miarę do macierzy.

---

## Miara 2 — Sales % All Region

```DAX
Sales % All Region =
DIVIDE(
    SUM(Sales[Sales]),
    CALCULATE(
        SUM(Sales[Sales]),
        REMOVEFILTERS(Region)
    )
)
```

Sformatuj jako procent (2 miejsca dziesiętne).

---

## Miara 3 — Sales % Country

```DAX
Sales % Country =
DIVIDE(
    SUM(Sales[Sales]),
    CALCULATE(
        SUM(Sales[Sales]),
        REMOVEFILTERS(Region[Region])
    )
)
```

### Ulepszona wersja:

```DAX
Sales % Country =
IF(
    ISINSCOPE(Region[Region]),
    DIVIDE(
        SUM(Sales[Sales]),
        CALCULATE(
            SUM(Sales[Sales]),
            REMOVEFILTERS(Region[Region])
        )
    )
)
```

---

## Miara 4 — Sales % Group

```DAX
Sales % Group =
DIVIDE(
    SUM(Sales[Sales]),
    CALCULATE(
        SUM(Sales[Sales]),
        REMOVEFILTERS(
            Region[Region],
            Region[Country]
        )
    )
)
```

### Ulepszona wersja:

```DAX
Sales % Group =
IF(
    ISINSCOPE(Region[Region])
        || ISINSCOPE(Region[Country]),
    DIVIDE(
        SUM(Sales[Sales]),
        CALCULATE(
            SUM(Sales[Sales]),
            REMOVEFILTERS(
                Region[Region],
                Region[Country]
            )
        )
    )
)
```

---

# Organizacja modelu

W widoku modelu umieść trzy miary w folderze **Ratios**.

---

# Laboratorium ukończone

Aby zapisać:

1. **Plik → Zapisz jako**
2. **Przeglądaj to urządzenie**
3. Wybierz folder
4. Kliknij **Zapisz**
5. Gdy pojawi się monit o zastosowanie zmian → **Zastosuj**  
