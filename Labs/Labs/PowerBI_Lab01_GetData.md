# 🧠 Laboratorium Power BI – Pobieranie danych

## Historia laboratorium

To laboratorium ma na celu zapoznanie Cię z aplikacją **Power BI Desktop** oraz sposobami łączenia się z danymi i korzystania z technik podglądu danych w celu zrozumienia charakterystyki i jakości danych źródłowych.

### Cele laboratorium

W tym laboratorium nauczysz się:

- Otwierać program **Power BI Desktop**
- Łączyć się z różnymi źródłami danych
- Wyświetlać podgląd danych źródłowych za pomocą **Power Query**
- Korzystać z funkcji **profilowania danych** w Power Query

⏱️ Szacowany czas ukończenia: **30 minut**

---

## 🔹 Rozpocznij pracę z Power BI Desktop

1. Otwórz przeglądarkę i pobierz plik ZIP:  
   01-get-data.zip z folderu

2. Wypakuj folder do lokalizacji:  
   `C:\Users\Student\Downloads\01-get-data`

3. Otwórz plik:  
   `01-Starter-Sales Analysis.pbix`

> Plik startowy został skonfigurowany do celów laboratorium.  
> Wyłączono w nim automatyczne importowanie i wykrywanie relacji przy pierwszym ładowaniu danych.

---

## 🧩 Pobieranie danych z SQL Server

W tym zadaniu połączysz się z bazą **SQL Server** i zaimportujesz kilka tabel.

1. W Power BI Desktop wybierz **Narzędzia główne → Dane → SQL Server**  
2. W oknie **Baza danych SQL Server** wpisz:
   - **Serwer:** `localhost`
   - **Baza danych:** *(pozostaw puste)*
3. Wybierz **OK**
4. Jeśli pojawi się monit o poświadczenia:
   - Wybierz **Windows → Użyj moich bieżących poświadczeń → Połącz**
5. Jeśli zobaczysz ostrzeżenie o szyfrowaniu połączenia – wybierz **OK**
6. W oknie **Nawigator** rozwiń bazę **AdventureWorksDW2020**

> 💡 Baza danych AdventureWorksDW2020 to wersja edukacyjna AdventureWorksDW2017 dostosowana do celów dydaktycznych.

7. Wybierz tabele:
   - `DimEmployee`
   - `DimEmployeeSalesTerritory`
   - `DimProduct`
   - `DimReseller`
   - `DimSalesTerritory`
   - `FactResellerSales`
8. Kliknij **Przekształć dane**, aby otworzyć **Edytor Power Query**

---

## 🔍 Podgląd danych w Edytorze Power Query

Edytor Power Query umożliwia przeglądanie, analizę i profilowanie danych przed ich załadowaniem do modelu.

1. W okienku **Zapytania** wybierz `DimEmployee`
   - Tabela ma 33 kolumny i 296 wierszy  
   - Ostatnie pięć kolumn zawiera **linki Tabela/Wartość**, reprezentujące relacje  
2. Wybierz **Widok → Podgląd danych → Jakość kolumn**
   - Kolumna `Position` ma **94% pustych wartości (null)**
3. Wybierz **Widok → Podgląd danych → Dystrybucja kolumn**
   - Kolumna `Position`: 4 wartości odrębne, 1 unikatowa  
   - Kolumna `EmployeeKey`: 296 wartości unikatowych  

> 🔑 Kolumny unikatowe są kluczowe dla relacji **jeden-do-wielu** w modelu danych.

4. Sprawdź pozostałe tabele:
   - `DimProduct` – informacje o produktach  
   - `DimReseller` – dane odsprzedawców  
   - `DimSalesTerritory` – regiony sprzedaży  
   - `FactResellerSales` – linie sprzedaży  

5. W `DimReseller` włącz **Profil kolumny** i sprawdź kolumnę `BusinessType`
   - Problem z jakością danych: dwie wartości „Warehouse” i „Ware House”  

6. W `FactResellerSales` sprawdź kolumnę `TotalProductCost`
   - 8% wartości jest **pustych** – problem jakości danych

---

## 📄 Pobieranie danych z pliku CSV

Dodasz nowe zapytania z plików CSV.

1. W **Edytorze Power Query** wybierz:  
   **Narzędzia główne → Nowe źródło → Tekst/CSV**
2. Wskaż folder:  
   `Downloads\01-get-data`
3. Wybierz plik `ResellerSalesTargets.csv` → **Otwórz → OK**
   - Zapytanie: `ResellerSalesTargets`
   - Każdy wiersz = sprzedawca + rok + 12 miesięcznych celów sprzedaży  
   - Braki danych oznaczone myślnikiem `-`
4. Powtórz dla pliku `ColorFormats.csv`
   - Zawiera kolory produktów i kody HEX tła/czcionki  
   - Zapytanie: `ColorFormats`

---

## 💾 Zakończenie laboratorium

1. (Opcjonalnie) Zapisz raport:
   - **Plik → Zapisz jako → Przeglądaj to urządzenie**
   - Nadaj nazwę i zapisz jako `.pbix`
2. Jeśli pojawi się monit o zastosowanie zmian – wybierz **Zastosuj**

Raport Power BI jest gotowy do użycia w kolejnym laboratorium:  
**Modelowanie danych w Power BI Desktop**

---

## ✅ Checklist: Weryfikacja

| # | Krok do sprawdzenia | Status |
|---|----------------------|:------:|
| 1 | Folder `01-get-data` został pobrany i wypakowany | ☐ |
| 2 | Otworzono plik `01-Starter-Sales Analysis.pbix` | ☐ |
| 3 | Połączenie z `localhost` SQL Server zostało ustanowione | ☐ |
| 4 | Zaimportowano 6 tabel z bazy `AdventureWorksDW2020` | ☐ |
| 5 | Włączono **Jakość kolumn** i **Dystrybucję kolumn** w Power Query | ☐ |
| 6 | Zidentyfikowano błędną wartość `Ware House` | ☐ |
| 7 | Dodano zapytania `ResellerSalesTargets` i `ColorFormats` | ☐ |
| 8 | Raport `.pbix` został zapisany | ☐ |

---

> „Dane to paliwo, ale Power Query to silnik, który je rafinuje.”  
> — *SQLManiak Labs, 2025*
