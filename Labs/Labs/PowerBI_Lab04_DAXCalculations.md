# Tworzenie obliczeń DAX w modelach semantycznych

**Opis laboratorium**  
W tym laboratorium utworzysz tabele obliczeniowe, kolumny obliczeniowe i proste miary przy użyciu języka **DAX (Data Analysis Expressions)**.

## W tym laboratorium nauczysz się:
- Tworzyć **tabele obliczeniowe**.
- Tworzyć **kolumny obliczeniowe**.
- Tworzyć **miary**.

**Czas ukończenia:** około 45 minut.

---

# Rozpoczęcie

Pobierz materiały:  
https://github.com/MicrosoftLearning/PL-300-Microsoft-Power-BI-Data-Analyst/raw/Main/Allfiles/Labs/04-create-dax-calculations/04-dax-calculations.zip

Rozpakuj do:  
`C:\Users\Student\Downloads\04-dax-calculations`

Otwórz plik: **04-Starter-Sales Analysis.pbix**

**Uwaga:** Podczas ładowania pliku może pojawić się okno dialogowe logowania. Wybierz **Anuluj**, aby je zamknąć. Zamknij wszelkie inne okna informacyjne. Wybierz **Zastosuj później**, jeśli pojawi się monit o zastosowanie zmian.

---

# Tworzenie tabeli obliczeniowej _Salesperson_

W tym zadaniu utworzysz tabelę obliczeniową **Salesperson** (która będzie miała bezpośrednią relację z tabelą **Sales**).

Tabelę obliczeniową tworzy się, wprowadzając najpierw **nazwę tabeli**, następnie **symbol równości (=)**, a po nim **formułę DAX**, która zwraca tabelę. Nazwa tabeli nie może już istnieć w modelu danych. Prawidłową formułę DAX wprowadza się **na pasku formuły** (autouzupełnianie, IntelliSense, kolorowanie).

1. W Power BI Desktop, w **Widoku raportu**, na wstążce **Modelowanie**, w grupie **Obliczenia**, wybierz **Nowa tabela**.  
2. Na pasku formuły wpisz: `Salesperson =`, naciśnij **Shift+Enter**, wpisz `'Salesperson (Performance)'` i naciśnij **Enter**.

> **Wskazówka:** Wszystkie definicje DAX w tym laboratorium możesz skopiować z pliku `04-dax-calculations\Snippets.txt`.

Ta definicja tworzy kopię danych tabeli **Salesperson (Performance)**. Kopiuje dane; **właściwości modelu** (widoczność, formaty itd.) nie są kopiowane.

W okienku **Dane** zauważ ikonę nowej tabeli z **kalkulatorem** (tabela obliczeniowa).

**Uwaga:** Tabele obliczeniowe materializują wartości, **zwiększają rozmiar** modelu i **przeliczają się** przy odświeżeniu zależności. Nie pobierają danych zewnętrznych (od tego jest Power Query) — przekształcają to, co już jest w modelu.

3. Przełącz się do **Widoku modelu** i zauważ tabelę **Salesperson**.  
4. Utwórz relację: **Salesperson | EmployeeKey → Sales | EmployeeKey**.  
5. Kliknij prawym przyciskiem **nieaktywną** relację (linia przerywana) między **Salesperson (Performance)** i **Sales**, wybierz **Usuń** → **Tak**.  
6. W tabeli **Salesperson** ukryj kolumny (**Jest ukryty = Tak**):
   - EmployeeID  
   - EmployeeKey  
   - UPN
7. Zaznacz tabelę **Salesperson** → **Właściwości → Opis**: *Sprzedawca powiązany ze sprzedażą*.  
   W tabeli **Salesperson (Performance)** ustaw opis: *Sprzedawca powiązany z regionem(ami).*

> Model danych oferuje teraz dwie perspektywy: **Salesperson** do analizy sprzedaży sprzedawcy oraz **Salesperson (Performance)** do analizy sprzedaży w przypisanych regionach.

---

# Tworzenie tabeli _Date_ (Data)

1. Przełącz się do **Widoku tabeli**.  
2. **Narzędzia główne → Obliczenia → Nowa tabela**.  
3. Wprowadź DAX:

```DAX
Date =
CALENDARAUTO(6)
```

- `CALENDARAUTO` skanuje kolumny dat w modelu i tworzy zakres dat obejmujący **pełne lata**.  
- Argument `6` oznacza, że **czerwiec** jest **ostatnim miesiącem roku obrachunkowego**.

Zauważ kolumnę `Date` z wartościami dat (mogą być w formacie mm/dd/rrrr). Na pasku stanu (lewy dół) zobaczysz ~**1826 wierszy** (5 pełnych lat).

---

# Tworzenie kolumn obliczeniowych

Dodasz kolumny umożliwiające filtrowanie/grupowanie po okresach oraz kolumnę do sortowania.

1. **Narzędzia tabel → Nowa kolumna**.

**Kolumna: Year (rok obrachunkowy)**  
```DAX
Year =
"FY" & YEAR('Date'[Date]) + IF(MONTH('Date'[Date]) > 6, 1)
```
Logika: jeśli miesiąc > czerwiec, rok = rok+1 (rok obrachunkowy Adventure Works).

Utwórz (wg Snippets.txt) kolumny: **Quarter**, **Month**.  
Zweryfikuj, że kolumny dodano.

## Weryfikacja w raporcie
1. Przełącz się do **Widoku raportu**.  
2. Dodaj nową **Stronę 2**.  
3. Dodaj wizualizację **macierzy**.  
4. Z tabeli **Date** przeciągnij **Year** do **Wierszy**, a potem **Month** pod **Year**.  
5. Rozwiń hierarchię (ikona podwójnej strzałki).

Miesiące sortują się **alfabetycznie**.

**Aby sortować chronologicznie — utwórz MonthKey:**

```DAX
MonthKey =
(YEAR('Date'[Date]) * 100) + MONTH('Date'[Date])
```
Sprawdź, że wartości są liczbami (np. 201707).

- Zaznacz pole **Month** → **Sortuj według kolumny → MonthKey**.  
- Miesiące posortują się chronologicznie.

---

# Ukończenie tabeli _Date_

1. **Ukryj** kolumnę **MonthKey**.  
2. Utwórz hierarchię: prawy klik **Year → Utwórz hierarchię**, nazwij **Fiscal**, dodaj **Quarter**, **Month**.  
3. Utwórz relacje:
   - **Date | Date → Sales | OrderDate**
   - **Date | Date → Targets | TargetMonth**
4. **Ukryj** kolumny:
   - **Sales | OrderDate**
   - **Targets | TargetMonth**

---

# Oznaczanie tabeli _Date_ jako tabeli dat

1. **Widok raportu** → zaznacz tabelę **Date** (nie kolumnę).  
2. **Narzędzia tabel → Kalendarze → Oznacz jako tabelę dat**.  
3. Przełącz suwak **Oznacz jako tabelę dat = Wł**.  
4. **Wybierz kolumnę daty:** `Date` → **Zapisz**.

> Power BI rozumie teraz, że to **oś czasu** modelu. Gdy masz hurtownię, lepiej ładować wymiary dat ze źródła niż tworzyć je DAX-em.

Zapisz plik Power BI Desktop.

---

# Tworzenie prostych miar

Na **Stronie 2** dodaj do macierzy **Sales | Unit Price** — domyślnie **Średnia z Unit Price**.

## Miara: Avg Price
W tabeli **Sales** → prawy klik → **Nowa miara**:

```DAX
Avg Price =
AVERAGE(Sales[Unit Price])
```

Dodaj **Avg Price** do macierzy — wartości jak dla `Unit Price`, ale kontrolowane przez miarę (bez zmiany agregacji przez autorów).

Utwórz (wg Snippets.txt) miary:
- **Median Price**
- **Min Price**
- **Max Price**
- **Orders** *(DISTINCTCOUNT SalesOrderNumber)*
- **Order Lines** *(COUNTROWS Sales)*

### Formatowanie i porządkowanie
- Zaznacz: **Avg Price, Max Price, Median Price, Min Price** → **format: 2 miejsca dziesiętne**, **Folder wyświetlania: Pricing**.  
- **Ukryj kolumnę** `Unit Price` (wymuszenie pracy na miarach).  
- Zaznacz: **Order Lines, Orders** → **separator tysięcy**, **Folder: Counts**.

W wizualizacji usuń **Średnia z Unit Price** (X).  
Rozciągnij macierz i dodaj: **Median Price, Min Price, Max Price, Orders, Order Lines**.  
Sprawdź wyniki i formaty.

---

# Tworzenie dodatkowych (złożonych) miar

Przejdź do **Strony 1** i spójrz na tabelę sprzedawców (po prawej) — zwróć uwagę na **sumę** kolumny *Target*.

1. Zaznacz wizualizację → w **Wizualizacje** usuń *Suma z Target*.  
2. Zmień nazwę kolumny **Targets | Target** na **TargetAmount**.

## Miara: Target
W tabeli **Targets** utwórz miarę:

```DAX
Target =
IF(
    HASONEVALUE('Salesperson (Performance)'[Salesperson]),
    SUM(Targets[TargetAmount])
)
```
- Jeśli filtruje jedna wartość **Salesperson**, zwróć **sumę** targetu dla tej osoby.  
- W przeciwnym razie zwróć **BLANK()** (brak sumy globalnej).

**Format:** 0 miejsc dziesiętnych.  
**Ukryj kolumnę** `TargetAmount` (tabela z samymi miarami trafi na górę listy).  
Dodaj **Target** do tabeli — **suma = BLANK**.

## Miary: Variance i Variance Margin
Utwórz wg Snippets:
- **Variance** (format: 0 miejsc)  
- **Variance Margin** (format: procent, 2 miejsca)

Dodaj je do tabeli i dopasuj rozmiar wizualizacji.

> Jeśli wygląda, że nikt nie osiąga celów, pamiętaj: raport **nie jest filtrowany czasem**. W kolejnym laboratorium (Projektowanie raportu) zbudujesz kontrolki czasu i filtry.

Zapisz plik Power BI Desktop.

---

# Laboratorium ukończone

Możesz zapisać raport (niekonieczne do następnego modułu).

**Zapis:**
1. **Plik → Zapisz jako**  
2. **Przeglądaj to urządzenie**  
3. Wybierz folder i nazwę  
4. **Zapisz**  
Gdy pojawi się monit o zastosowanie oczekujących zmian → **Zastosuj**.
