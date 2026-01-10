# Konfigurowanie modelu semantycznego w Power BI
**Opis laboratorium**

W tym laboratorium rozpoczniesz tworzenie modelu danych. Będzie to obejmować tworzenie relacji między tabelami, a następnie konfigurowanie właściwości tabel i kolumn, aby poprawić przyjazność i użyteczność modelu danych. Utworzysz również hierarchie i szybkie miary.

## W tym laboratorium nauczysz się:
- Tworzyć relacje modelu.
- Konfigurować właściwości tabel i kolumn.
- Tworzyć hierarchie.
- Tworzyć szybkie miary.
- Konfigurować relację wiele-do-wielu.

**Ukończenie laboratorium:** około 45 minut.

---

# Rozpoczęcie

Pobierz materiały:  
03-model-data.zip

Rozpakuj do:  
`C:\Users\Student\Downloads\03-model-data`

Otwórz plik:  
`03-Starter-Sales Analysis.pbix`

**Uwaga:** Podczas ładowania pliku może pojawić się okno dialogowe logowania. Wybierz **Anuluj**, aby je zamknąć. Zamknij wszelkie inne okna informacyjne. Wybierz **Zastosuj później**, jeśli pojawi się monit o zastosowanie zmian.

---

# Tworzenie relacji modelu

Plik został skonfigurowany tak, aby nie identyfikować relacji między tabelami (to nie jest domyślne ustawienie), co jest zalecane, aby zapobiec dodatkowej pracy przy tworzeniu prawidłowych relacji dla modelu.

**Notacja pól:** `Tabela | Kolumna` (np. `Product | Category`).

1. W Power BI Desktop, w okienku **Dane**, kliknij prawym przyciskiem myszy pusty obszar i wybierz **Rozwiń wszystko**, aby wyświetlić wszystkie pola tabel.
2. Aby utworzyć wizualizację tabeli, w okienku **Dane**, w tabeli **Product**, zaznacz pole **Category**.
3. Aby dodać kolejną kolumnę do tabeli, w okienku **Dane** zaznacz pole **Sales | Sales**.

Zauważ, że wizualizacja tabeli wyświetla cztery kategorie produktów, a wartość sprzedaży jest taka sama dla każdej z nich i taka sama jak suma całkowita. Problem polega na tym, że tabela opiera się na polach z różnych tabel. Oczekuje się, że każda kategoria produktu wyświetli sprzedaż dla tej kategorii. Jednakże, ponieważ nie ma relacji modelu między tymi tabelami, tabela **Sales** nie jest filtrowana. Teraz dodasz relację, aby propagować filtry między tabelami.

4. Po lewej stronie wybierz ikonę **Widok modelu**, aby przełączyć się do projektanta modelu.
5. Na wstążce **Narzędzia główne** wybierz **Zarządzaj relacjami**.
6. W oknie **Zarządzaj relacjami** zauważ, że nie zdefiniowano jeszcze żadnych relacji.
7. Aby utworzyć relację, wybierz **+ Nowa relacja**.
8. Aby skonfigurować relację z tabeli **Product** do tabeli **Sales**:
   - **Tabela źródłowa**: *Product*
   - **Tabela docelowa**: *Sales*

Zauważ, że następujące właściwości zostały skonfigurowane automatycznie:
- Wybrano kolumny **ProductKey** w każdej tabeli (ta sama nazwa i typ danych). W rzeczywistych danych może być konieczne znalezienie pasujących kolumn o różnych nazwach.
- **Kardynalność**: *Jeden do wielu (1:*)*. Power BI wykrył, że **Product.ProductKey** ma unikalne wartości.
- **Kierunek filtrowania krzyżowego**: *Pojedynczy*. Filtry propagują się ze strony „jeden” do „wielu” (z **Product** do **Sales**).
- **Uaktywnij tę relację**: zaznaczona. Aktywne relacje propagują filtry. Relacje nieaktywne mogą istnieć przy wielu ścieżkach między tabelami i mogą być użyte w obliczeniach.

9. Wybierz **Zapisz** → w oknie **Zarządzaj relacjami** nowa relacja jest na liście → **Zamknij**.

Na diagramie modelu między dwiema tabelami znajduje się teraz łącznik (możesz zmienić położenie tabel, aby wyraźniej zobaczyć relację).

**Jak czytać linię relacji:**
- **1** i **\*** – kardynalność
- **Grot strzałki** – kierunek filtrowania
- **Linia ciągła** – relacja aktywna; **linia przerywana** – nieaktywna
- **Tip:** najedź kursorem na linię, aby podświetlić kolumny

Przełącz się do **Widoku raportu** – wizualizacja tabeli zaktualizuje się i pokaże różne wartości dla każdej kategorii (filtry z **Product** propagują się do **Sales**).

---

# Tworzenie dodatkowych relacji

Istnieje łatwiejszy sposób tworzenia relacji: *przeciągnij i upuść* kolumny na diagramie modelu.

1. Przełącz się do **Widoku modelu**.
2. Z tabeli **Reseller** przeciągnij kolumnę **ResellerKey** na kolumnę **Sales | ResellerKey**.
   - **Ważne:** Jeśli kolumna „nie chce” się przeciągnąć, kliknij inną kolumnę, wróć do właściwej i spróbuj ponownie.
3. W oknie **Nowa relacja** przejrzyj konfigurację i wybierz **Zapisz**.
4. Utwórz kolejne relacje metodą „drag&drop”:
   - **Region | SalesTerritoryKey → Sales | SalesTerritoryKey**
   - **Salesperson | EmployeeKey → Sales | EmployeeKey**
5. Na diagramie uporządkuj tabele tak, by **Sales** było centralnie, a powiązane tabele wokół. Niepołączone tabele umieść z boku.
6. Zapisz plik.

---

# Konfigurowanie tabeli Product

W tym zadaniu dodasz hierarchię i folder wyświetlania.

## Hierarchia
1. **Widok modelu** → tabela **Product**.
2. Prawy klik **Category** → **Utwórz hierarchię**.
3. W **Właściwościach** zmień **Nazwa** na **Products**.
4. W **Hierarchia** dodaj poziomy: **Subcategory**, **Product** (→ **Zastosuj**).  
   W okienku **Dane** rozwiń hierarchię **Products**, aby zobaczyć poziomy.

## Folder wyświetlania
1. Zaznacz **Background Color Format**.
2. Z wciśniętym **Ctrl** zaznacz **Font Color Format**.
3. W **Właściwościach** ustaw **Folder wyświetlania** na **Formatting**.
4. Obie kolumny pojawią się teraz w folderze *Formatting* (logiczna organizacja pól).

---

# Konfigurowanie tabeli Region

1. Utwórz hierarchię **Regions** z poziomami:
   - **Group**
   - **Country**
   - **Region**
2. Zaznacz kolumnę **Country** (kolumna, nie poziom hierarchii).
3. **Właściwości → Zaawansowane → Kategoria danych**: **Kraj/Region**.

*Kategoryzacja danych* pomaga Power BI (np. przy wizualizacjach map).

---

# Konfigurowanie tabeli Reseller

## Hierarchie
- **Resellers**: **Business Type**, **Reseller**
- **Geography**: **Country-Region**, **State-Province**, **City**, **Reseller**

## Kategorie danych
- **Country-Region** → *Kraj/Region*
- **State-Province** → *Stan lub prowincja*
- **City** → *Miasto*

---

# Konfigurowanie tabeli Sales

## Opisy
- Kolumna **Cost** → **Opis**: *Na podstawie kosztu standardowego*  
  (opisy widoczne jako tooltip w okienku Dane / w modelu)

## Formatowanie i agregacje
- **Quantity** → **Separator tysięcy** = *Tak*
- **Unit Price** → **Miejsca dziesiętne** = *2*
- **Unit Price** → **Podsumuj według** = *Średnia*  
  (cena jednostkowa to stawka; średnia jest właściwsza niż suma)

---

# Masowa aktualizacja właściwości

## Ukrywanie kolumn
Zaznacz kolumnę **Product | ProductKey**, a następnie z **Ctrl** zaznacz:
- **Region | SalesTerritoryKey**
- **Reseller | ResellerKey**
- **Sales | EmployeeKey**
- **Sales | ProductKey**
- **Sales | ResellerKey**
- **Sales | SalesOrderNumber**
- **Sales | SalesTerritoryKey**
- **Salesperson | EmployeeID**
- **Salesperson | EmployeeKey**
- **Salesperson | UPN**
- **SalespersonRegion | EmployeeKey**
- **SalespersonRegion | SalesTerritoryKey**
- **Targets | EmployeeID**

Ustaw **Jest ukryty** = *Tak* (kolumny techniczne pod relacje / RLS / obliczenia).

## Formatowanie wartości
Zaznacz:
- **Product | Standard Cost**
- **Sales | Cost**
- **Sales | Sales**

Ustaw **Miejsca dziesiętne** = *0*.

---

# Eksplorowanie interfejsu modelu

Przełącz się do **Widoku raportu** i zwróć uwagę:
- Kolumny, hierarchie i poziomy to pola do wizualizacji.
- Widoczne są tylko pola istotne dla raportu.
- Tabela **SalespersonRegion** jest ukryta (wszystkie pola ukryte).
- Pola przestrzenne (w **Region**, **Reseller**) mają ikonę globu.
- Pola z symbolem **sigma (Ʃ)** domyślnie się sumują.
- Tooltip z opisem pojawia się dla **Sales | Cost**.
- Rozwiń **Sales | OrderDate** – widać **Hierarchię dat** (automatyczną). Podobnie **Targets | TargetMonth**.

**Ważne:** Rok obrotowy Adventure Works zaczyna się **1 lipca**, ale automatyczne hierarchie dat używają **roku kalendarzowego**.

## Wyłączenie automatycznej daty/godziny
**Plik → Opcje i ustawienia → Opcje → Bieżący plik → Ładowanie danych → Analiza czasowa → odznacz „Automatyczna data/godzina”.**  
Po wyłączeniu automatyczne hierarchie dat znikają.

---

# Tworzenie szybkich miar

## Miara **Profit**
1. Prawy klik na tabelę **Sales** → **Nowa szybka miara**.
2. **Wybierz obliczenie**: *Odejmowanie* (Operacje matematyczne).
3. **Wartość podstawowa**: *Sales | Sales*.
4. **Wartość do odjęcia**: *Sales | Cost*.
5. **Dodaj** → zmień nazwę miary na **Profit**.  
   (Miary mają ikonę kalkulatora. Nazwę możesz też zmienić F2 / dwuklik.)

## Miara **Profit Margin**
1. Jeśli w menu nie ma szybkiej miary – użyj wstążki **Narzędzia główne → Obliczenia**.
2. **Dzielenie**:  
   - **Licznik**: *Sales | Profit*  
   - **Mianownik**: *Sales | Sales*
3. Nazwij miarę: **Profit Margin**.  
4. Zaznacz miarę → **Narzędzia miar** → **Format**: *Wartość procentowa, 2 miejsca*.

## Test
- Zaznacz istniejącą wizualizację tabeli na stronie.
- Dodaj miary **Profit** i **Profit Margin**.
- Poszerz wizualizację i zweryfikuj wyniki oraz format.

---

# Relacja wiele-do-wielu

W relacji **Salesperson ↔ Sales** istnieje dodatkowy związek poprzez regiony. Sprzedawca może należeć do wielu regionów, a region może mieć wielu sprzedawców. Do analizy przyda się tabela pośrednia **SalespersonRegion**.

## Kroki
1. Widok raportu → dodaj tabelę z polami:  
   - **Salesperson | Salesperson**  
   - **Sales | Sales**
2. Zauważ, że **Michael Blythe** ma ~9 mln sprzedaży.
3. **Widok modelu** → umieść **SalespersonRegion** między **Region** i **Salesperson**.

## Utwórz relacje
- **Salesperson | EmployeeKey → SalespersonRegion | EmployeeKey**
- **Region | SalesTerritoryKey → SalespersonRegion | SalesTerritoryKey**

## Kierunek filtrowania dwukierunkowego
1. Edytuj relację **Region ↔ SalespersonRegion** (dwuklik na linię).
2. **Kierunek filtrowania krzyżowego**: *Obydwa*.
3. Zaznacz **Zastosuj filtr zabezpieczeń w obu kierunkach**.
4. **Zapisz** – relacja ma teraz podwójny grot strzałki.

## Rozwiązanie niejednoznaczności ścieżek
Ponieważ istnieją dwie możliwe ścieżki propagacji z **Salesperson** do **Sales**, wyłącz jedną z relacji:

1. Edytuj relację **Salesperson ↔ Sales**.
2. Odznacz **Uaktywnij tę relację** → **Zapisz**.

Teraz filtry przechodzą jedyną aktywną ścieżką (przez tabelę pośrednią).  
Wróć do raportu – **Michael Blythe ≈ 22 mln**.

> Uwaga: Przy relacjach M2M suma sprzedaży sprzedawców może przekraczać sumę całkowitą (wielokrotne zliczanie). Np. **Brian Welcker** jako dyrektor sprzedaży „dziedziczy” sprzedaż wszystkich regionów – wynik jest poprawny.

## Zmiana nazwy tabeli
W **Widoku modelu** → tabela **Salesperson** → **Nazwa**: **Salesperson (Performance)**.

---

# Relacja z tabelą Targets

1. Utwórz relację: **Salesperson (Performance) | EmployeeID → Targets | EmployeeID**.
2. W raporcie dodaj **Targets | Target** do wizualizacji tabeli.
3. Zmień rozmiar wizualizacji, by widzieć wszystkie kolumny.

**Uwaga:**  
- Brak filtra czasu – cele zawierają przyszłe miesiące.  
- Cele **nie są addytywne** (nie sumują się). Ukryj total albo zastosuj DAX.

Zapisz plik Power BI Desktop.

---

# Laboratorium ukończone

Możesz zapisać raport, choć nie jest to konieczne do następnego modułu.

**Zapis do pliku:**
1. **Plik → Zapisz jako**.
2. **Przeglądaj to urządzenie**.
3. Wybierz folder, nadaj nazwę.
4. **Zapisz** (jeśli pojawi się monit o zastosowanie zmian – **Zastosuj**).
