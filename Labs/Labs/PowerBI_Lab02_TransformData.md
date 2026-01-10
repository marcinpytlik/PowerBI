# 🧠 Laboratorium Power BI – Czyszczenie, przekształcanie i ładowanie danych

## Opis laboratorium

W tym laboratorium użyjesz technik **czyszczenia i transformacji danych**, aby rozpocząć kształtowanie modelu danych. Następnie zastosujesz zapytania, aby załadować każde z nich jako tabelę do modelu semantycznego.

### Cele laboratorium

W tym laboratorium nauczysz się:

- Stosować różne **transformacje danych**
- Ładować zapytania do **modelu semantycznego**

⏱️ Szacowany czas ukończenia: **45 minut**

---

## 🔹 Rozpoczęcie

1. Pobierz plik ZIP:  
   02-transform-data.zip

2. Wypakuj folder do lokalizacji:  
   `C:\Users\Student\Downloads\02-transform-data`

3. Otwórz plik:  
   `02-Starter-Sales Analysis.pbix`

> Jeśli pojawi się okno logowania, wybierz **Anuluj** i zamknij wszelkie inne komunikaty.  
> Gdy zostaniesz zapytany o zastosowanie zmian, wybierz **Zastosuj później**.

---

## 👨‍💼 Konfigurowanie zapytania *Salesperson*

1. Otwórz **Edytor Power Query**:  
   **Narzędzia główne → Zapytania → Przekształć dane**
2. W okienku **Zapytania** wybierz `DimEmployee`.
3. Jeśli pojawi się komunikat o połączeniu, wybierz:
   - **Edytuj poświadczenia → Bieżące poświadczenia → OK (połączenie nieszyfrowane)**
4. Zmień nazwę zapytania na **Salesperson**.
5. Wybierz **Zarządzaj kolumnami → Wybierz kolumny → Przejdź do kolumny → Nazwa**.
6. Zlokalizuj kolumnę `SalesPersonFlag` i przefiltruj tylko wiersze z wartością **TRUE**.
7. Usuń zbędne kolumny, pozostawiając tylko:
   - `EmployeeKey`
   - `EmployeeNationalIDAlternateKey`
   - `FirstName`
   - `LastName`
   - `Title`
   - `EmailAddress`
8. Scal kolumny `FirstName` i `LastName` → separator **Spacja** → nowa kolumna **Salesperson**.
9. Zmień nazwy:
   - `EmployeeNationalIDAlternateKey` → `EmployeeID`
   - `EmailAddress` → `UPN`
10. Sprawdź: **5 kolumn / 18 wierszy**

---

## 🌍 Konfigurowanie zapytania *SalespersonRegion*

1. Wybierz zapytanie `DimEmployeeSalesTerritory`.
2. Zmień nazwę zapytania na **SalespersonRegion**.
3. Usuń kolumny `DimEmployee` i `DimSalesTerritory`.
4. Sprawdź: **2 kolumny / 39 wierszy**

---

## 🧱 Konfigurowanie zapytania *Product*

1. Wybierz zapytanie `DimProduct` i zmień nazwę na **Product**.
2. Przefiltruj kolumnę `FinishedGoodsFlag` = **TRUE**.
3. Pozostaw kolumny:
   - `ProductKey`
   - `EnglishProductName`
   - `StandardCost`
   - `Color`
   - `DimProductSubcategory`
4. Rozwiń kolumnę `DimProductSubcategory`:
   - Odznacz **Zaznacz wszystkie**
   - Zaznacz `EnglishProductSubcategoryName` i `DimProductCategory`
   - Odznacz opcję **Użyj oryginalnej nazwy kolumny jako prefiksu**
5. Następnie rozwiń `DimProductCategory` i wybierz tylko `EnglishProductCategoryName`.
6. Zmień nazwy kolumn:
   - `EnglishProductName` → `Product`
   - `StandardCost` → `Standard Cost`
   - `EnglishProductSubcategoryName` → `Subcategory`
   - `EnglishProductCategoryName` → `Category`
7. Sprawdź: **6 kolumn / 397 wierszy**

---

## 🏢 Konfigurowanie zapytania *Reseller*

1. Wybierz zapytanie `DimReseller` i zmień nazwę na **Reseller**.
2. Pozostaw kolumny:
   - `ResellerKey`
   - `BusinessType`
   - `ResellerName`
   - `DimGeography`
3. Rozwiń `DimGeography` i wybierz:
   - `City`
   - `StateProvinceName`
   - `EnglishCountryRegionName`
4. W kolumnie `BusinessType`:
   - Zamień wartość `Ware House` → `Warehouse`
5. Zmień nazwy kolumn:
   - `BusinessType` → `Business Type`
   - `ResellerName` → `Reseller`
   - `StateProvinceName` → `State-Province`
   - `EnglishCountryRegionName` → `Country-Region`
6. Sprawdź: **6 kolumn / 701 wierszy**

---

## 🌎 Konfigurowanie zapytania *Region*

1. Wybierz `DimSalesTerritory` i zmień nazwę na **Region**.
2. Odfiltruj `SalesTerritoryAlternateKey` ≠ 0.
3. Pozostaw kolumny:
   - `SalesTerritoryKey`
   - `SalesTerritoryRegion`
   - `SalesTerritoryCountry`
   - `SalesTerritoryGroup`
4. Zmień nazwy:
   - `SalesTerritoryRegion` → `Region`
   - `SalesTerritoryCountry` → `Country`
   - `SalesTerritoryGroup` → `Group`
5. Sprawdź: **4 kolumny / 10 wierszy**

---

## 💰 Konfigurowanie zapytania *Sales*

1. Wybierz `FactResellerSales` i zmień nazwę na **Sales**.
2. Pozostaw kolumny: `SalesOrderNumber`, `OrderDate`, `ProductKey`, `ResellerKey`, `EmployeeKey`, `SalesTerritoryKey`, `OrderQuantity`, `UnitPrice`, `TotalProductCost`, `SalesAmount`, `DimProduct`
3. Rozwiń `DimProduct` → wybierz tylko `StandardCost`.
4. Dodaj kolumnę niestandardową:  
   **Formuła:** `if [TotalProductCost] = null then [OrderQuantity] * [StandardCost] else [TotalProductCost]`
5. Usuń kolumny `TotalProductCost` i `StandardCost`.
6. Zmień nazwy: `OrderQuantity` → `Quantity`, `UnitPrice` → `Unit Price`, `SalesAmount` → `Sales`
7. Zmień typy danych: `Quantity` → Liczba całkowita, `Unit Price`, `Sales`, `Cost` → Stała liczba dziesiętna
8. Sprawdź: **10 kolumn / 999+ wierszy**

---

## 🎯 Konfigurowanie zapytania *Targets*

1. Wybierz `ResellerSalesTargets` i zmień nazwę na **Targets**.
2. Anuluj przestawienie innych kolumn (pozostaw `Year` i `EmployeeID`).
3. Zastosuj filtr w kolumnie `Value`, aby usunąć wartości `-`.
4. Zmień nazwy: `Attribute` → `MonthNumber`, `Value` → `Target`
5. Zamień w `MonthNumber` wartość `M` → *(pusta)*, typ danych: **Liczba całkowita**
6. Dodaj kolumnę z przykładów → wpisz `7/1/2017`, utwórz `TargetMonth`
7. Usuń `Year` i `MonthNumber`, zmień typy: `Target` → Stała liczba dziesiętna, `TargetMonth` → Data
8. Pomnóż `Target` × 1000
9. Sprawdź: **3 kolumny / 809 wierszy**

---

## 🎨 Konfigurowanie zapytania *ColorFormats*

1. Wybierz zapytanie `ColorFormats`.
2. Wybierz **Użyj pierwszego wiersza jako nagłówków**.
3. Sprawdź: **3 kolumny / 10 wierszy**

---

## 🔗 Aktualizowanie zapytania *Product* (scalanie z ColorFormats)

1. Wybierz `Product`.
2. Wybierz **Połącz → Scal zapytania**.
3. Połącz kolumnę `Color` z `ColorFormats.Color`, typ sprzężenia: **Zewnętrzne lewe**.
4. Rozwiń `ColorFormats` → dołącz `Background Color Format`, `Font Color Format`.
5. Sprawdź: **8 kolumn / 397 wierszy**

---

## ⚙️ Aktualizowanie zapytania *ColorFormats* (wyłączenie ładowania)

1. Wybierz zapytanie `ColorFormats`.
2. W **Ustawieniach zapytania → Wszystkie właściwości** odznacz **Włącz ładowanie do raportu**.

---

## 🧾 Przegląd końcowego produktu

| Nazwa zapytania     | Ładowanie |
|----------------------|-----------|
| Salesperson          | ✔️ |
| SalespersonRegion    | ✔️ |
| Product              | ✔️ |
| Reseller             | ✔️ |
| Region               | ✔️ |
| Sales                | ✔️ |
| Targets              | ✔️ |
| ColorFormats         | ❌ |

---

## ✅ Checklist: Weryfikacja

| # | Krok do sprawdzenia | Status |
|---|----------------------|:------:|
| 1 | Folder `02-transform-data` został wypakowany | ☐ |
| 2 | Otworzono plik `02-Starter-Sales Analysis.pbix` | ☐ |
| 3 | Utworzono i przefiltrowano zapytanie `Salesperson` | ☐ |
| 4 | Utworzono `SalespersonRegion`, `Product`, `Reseller`, `Region` | ☐ |
| 5 | Zastosowano kolumnę `Cost` w zapytaniu `Sales` | ☐ |
| 6 | Utworzono kolumnę `TargetMonth` w zapytaniu `Targets` | ☐ |
| 7 | Scalono `Product` z `ColorFormats` | ☐ |
| 8 | Wyłączono ładowanie `ColorFormats` | ☐ |
| 9 | Załadowano dane do modelu Power BI | ☐ |

---

> „Transformacja to sztuka — im czystsze dane, tym głębszy wgląd.”  
> — *SQLManiak Labs, 2025*
