---
lab:
    title: 'Tworzenie dashboardów w Power BI'
---

# Tworzenie dashboardów w Power BI

## Opis laboratorium

W tym laboratorium utworzysz dashboard **Sales Monitoring** w Power BI Service, bazując na gotowym raporcie.

Poznasz:

- przypinanie (pin) wizuali do dashboardu,
- użycie Q&A do generowania kafelków dashboardu.

**Szacowany czas: 30 minut**

---

## Rozpoczęcie

Pobierz ZIP:

`12-create-dashboard.zip`

Rozpakuj:

**C:\Users\Student\Downloads\12-create-dashboard**

> Do publikacji potrzebujesz przynajmniej Power BI Free.  
> Zaloguj się w przeglądarce: https://app.powerbi.com  

---

# Publikacja raportu

1. W Power BI Service przejdź do **My Workspace**
2. Import → Report → From this computer
3. Wskaż plik **12-Starter-Sales Analysis.pbix**
4. Otwórz raport

---

# Utwórz dashboard

1. W raporcie → strona Overview
2. Slicer Year → FY2020
3. Region → Select All

> Pin zapisuje aktualny kontekst filtrów.
> (Przy filtrach czasowych lepszy relatywny Date slicer.)

4. Najedź na wizual **Sales and Profit Margin by Month**
5. Kliknij pin
6. Dashboard name → **Sales Monitoring**
7. Pin
8. Otwórz My Workspace → Sales Monitoring

Powinien być 1 kafelek.

---

# Dodaj kafelek z Q&A

1. Na dashboardzie kliknij **Ask a question about your data**
2. Usuń tekst i wpisz: **Sales YTD**
3. Widzisz (Blank)

> Sales YTD to miara Time Intelligence – potrzebuje filtru po Date.

4. Dopisz: **in year FY2020**
5. Wynik: około $33M
6. Kliknij Pin Visual
7. Wybierz Sales Monitoring

---

# Dodaj logo jako kafelek

1. Edit → Add a Tile → Image
2. Otwórz:
   **AdventureWorksLogo_DataURL.txt**
3. Wklej URL → Apply
4. Zmień rozmiar

Ułóż:
- logo góra lewa
- pod nim Sales YTD
- po prawej wizual z raportu

---

# Edycja kafelków

## Subtitle

1. Ellipsis (…) → Edit details
2. Subtitle → **FY2020**
3. Apply

## Last refresh

1. Edit details dla kafelka Sales / Profit Margin
2. Display Last Refresh Time = On
3. Apply

---

# Aktualizacja bazy (opcjonalnie)

> Jeśli masz dostęp do AdventureWorksDW2020

1. Uruchom w PowerShell:
   `UpdateDatabase-2-AddSales.ps1`
2. Zatwierdź politykę wykonania

Dane czerwca 2020 zostaną dodane.

---

# Odświeżenie modelu

1. W Power BI Desktop → Sales (PPM) → Refresh Data
2. Save
3. Publish → Replace
4. Zamknij PBI Desktop

---

# Sprawdź dashboard

1. Otwórz Sales Monitoring w PowerBI.com
2. Powinieneś zobaczyć:
   - Refresh NOW
   - miesiąc 2020 Jun

> Jeśli nie – odśwież przeglądarkę (F5)

---

# Koniec laboratorium

Zamknij przeglądarkę.