---
lab:
    title: 'Zabezpieczanie dostępu do danych w Power BI'
---

# Zabezpieczanie dostępu do danych w Power BI

## Opis laboratorium

W tym laboratorium wprowadzisz mechanizm **row-level security (RLS)**, aby handlowiec widział tylko dane sprzedaży dla przypisanego mu regionu. Nauczysz się:

- implementować dynamiczny RLS w Power BI,
- tworzyć i testować rolę używając USERPRINCIPALNAME().

**Szacowany czas: 20 minut**

---

## Rozpoczęcie

Pobierz ZIP:

`11-secure-data.zip`

Rozpakuj do:

**C:\Users\Student\Downloads\11-secure-data**

Otwórz:

**11-Starter-Sales Analysis.pbix**

> Uwaga: przy otwarciu kliknij Cancel i Apply Later gdy pojawi się okno zmian.

---

# Wymuś row-level security

1. Wejdź w **Table view**
2. W Data Pane wybierz tabelę **Salesperson (Performance)**
3. Przejrzyj dane; np. Michael Blythe (281) ma UPN:
   `michael-blythe@adventureworks.com`

> Ten handlowiec odpowiada za regiony:  
> US Northeast, US Central, US Southeast

4. Home → Security → **Manage Roles**
5. New → nazwa roli: `Salespeople`
6. Wybierz tabelę **Salesperson (Performance)**
7. **Switch to DAX editor**
8. Wpisz:

```DAX
[UPN] = USERPRINCIPALNAME()
USERPRINCIPALNAME() zwraca konto użytkownika zalogowanego do raportu.

Save & Close

Testowanie roli
Home → Security → View As

Zaznacz Other User

Wpisz:
michael-blythe@adventureworks.com

Zaznacz rolę Salespeople

OK

Teraz działasz w kontekście użytkownika Michael Blythe.

U góry pojawi się czerwony baner (środowisko testowe)

W tabeli powinna być widoczna tylko sprzedaż Michaela Blythe

Kliknij Stop viewing

Usuń rolę (opcjonalnie)
Home → Manage Roles

… (trzy kropki)

Delete

Confirm

Po publikacji do Power BI Service trzeba przypisać użytkowników w ustawieniach datasetu — tutaj tego nie robimy.

Koniec laboratorium
Możesz zapisać, ale nie jest to wymagane.

Zamknij przeglądarkę

File → Save As

Browse

Zapisz .pbix

Apply (jeśli pyta)

Zamknij Power BI Desktop