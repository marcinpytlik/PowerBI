# Git + Power BI – jak sensownie wersjonować raporty

Power BI + Git to trochę trudniejszy związek niż „zwykły” kod, bo klasyczne pliki **PBIX** są binarne.  
Da się jednak ogarnąć:

- wersjonowanie raportów,
- współpracę w zespole,
- sensowne „commit messages”,
- porównywanie zmian (diff),
- integrację z repo (GitHub / Azure DevOps / GitLab).

Ten dokument opisuje **praktyczny workflow**, a nie tylko teorię.

---

## 1. Typy plików Power BI a Git

### 1.1. PBIX – klasyczny raport

- Plik **`.pbix`** to **jeden wielki binarny plik**:
  - definicje raportów,
  - model danych,
  - zapytania (Power Query),
  - relacje, miary, formatowanie.
- Git **nie umie sensownie zrobić diff** na binarce – widzi tylko „zmieniono plik”.

**Konsekwencje:**

- każdy commit z PBIX to „black box”,
- merge konfliktów jest praktycznie niemożliwy,
- jedyna opcja to:
  - trzymać historię wersji,
  - dobra konwencja nazw commitów,
  - dobre tagowanie (np. `v1.0`, `demo-2025-01`).

---

### 1.2. Projekt Power BI – tryb folderowy (`.pbip`)

Nowsze wersje Power BI Desktop pozwalają zapisać raport w trybie:

- **Power BI Project** (`.pbip`) – to tak naprawdę folder z plikami:
  - definicja raportu,
  - definicja modelu,
  - konfiguracja połączeń,
  - JSON-y / TMSL.

**Zaleta:**  
Te pliki są **tekstowe**, więc:

- Git potrafi zrobić diff,
- można robić code review,
- merge konfliktów jest realny do ogarnięcia.

Jeśli masz możliwość – **dla zespołowej pracy lepiej przejść na projekt `.pbip`**.

---

## 2. Minimalna konfiguracja repo do Power BI

Propozycja struktury:

```text
.
├── reports/
│   ├── sales-analysis/
│   │   ├── SalesAnalysis.pbix        # główny raport (binarny)
│   │   ├── SalesAnalysis.pbit        # template (opcjonalnie)
│   │   └── README.md                 # opis raportu
│   └── executive-dashboard/
│       └── ExecutiveDashboard.pbix
├── docs/
│   ├── POWERBI_GIT_GUIDE.md          # ten plik :)
│   └── REPORTS_CATALOG.md            # katalog raportów
└── .gitignore
Przykładowy .gitignore:

gitignore
Skopiuj kod
# Pliki tymczasowe Power BI / Windows
~$*
*.tmp
*.lock
*.bak
*.log

# IDE itp.
.vscode/
.idea/
*.user

# Jeżeli trzymasz dane do testów lokalnych
/data/*
!data/README.md
3. Wersjonowanie PBIX – zdrowy workflow
PBIX jest binarny, ale można z niego zrobić sensowny proces Gitowy, jeśli będziesz trzymał się kilku zasad.

3.1. Zasada „jeden właściciel na raz”
PBIX nie lubi pracy równoległej na tym samym pliku.

Rekomendowany model:

konkretna osoba „checkoutuje” plik do pracy,

dopóki nie skończy, inni nie grzebią w tym samym PBIX,

po skończonych zmianach:

commit,

push,

opis w changelogu / README.

Dobrze działa:

osobna gałąź feature na większe zmiany,

merge do main po akceptacji.

Przykład nazw branchy:

text
Skopiuj kod
feature/pbi-sales-add-ytd-measures
feature/pbi-exec-dashboard-redesign
bugfix/pbi-filter-sync-region
3.2. Konwencja commitów
Przykłady commit messages dla raportu:

text
Skopiuj kod
feat(pbi-sales): dodano miary Sales YTD i Sales YoY Growth
feat(pbi-exec): nowy układ strony Overview + karty KPI
fix(pbi-sales): poprawka slicera Region – filtruje wszystkie strony
refactor(pbi-model): uporządkowano foldery display w modelu
docs(pbi-sales): dodano opis miar do README.md
Dzięki temu w logu Gita:

wiesz, co się zmieniło,

możesz wrócić do konkretnej wersji raportu,

widać ewolucję modelu.

3.3. Tagowanie istotnych wersji
Dla ważnych milestone’ów:

bash
Skopiuj kod
git tag -a pbi-sales-v1.0 -m "Wersja produkcyjna Sales Analysis – luty 2026"
git push origin pbi-sales-v1.0
Możesz mieć:

tagi produkcyjne,

tagi demo,

tagi warsztatowe (np. dla studentów).

4. Git + Power BI Project (.pbip)
Jeśli korzystasz z projektu, struktura może wyglądać tak:

text
Skopiuj kod
reports/
  sales-analysis/
    SalesAnalysis.pbip
    definition.pbir
    model.bim
    report.json
    connections.json
Tu wchodzi pełna moc Gita:

normalne diffy na JSON/TMSL,

code review w pull requestach,

komentarze do zmian w modelu.

4.1. Przykład PR review checklist (dla .pbip)
W opisie PR:

 jakie strony / wizuale zmieniono

 jakie miary dodano/zmodyfikowano

 czy zmienił się model (relacje, kolumny, typy danych)

 czy są noweźródła danych / połączenia

 czy usunięto stare miary / pola (breaking change?)

5. Dodatkowe artefakty do trzymania w Git
Z samym PBIX warto trzymać również:

5.1. Dokumentację raportu
reports/sales-analysis/README.md:

markdown
Skopiuj kod
# Sales Analysis – opis raportu

## Cel
Analiza sprzedaży wg roku fiskalnego, regionu, kategorii produktu.

## Strony
- Overview – KPI, trend miesięczny, rozbicie po regionach
- Profit – marża wg okresu
- My Performance – widok handlowca (RLS)

## Główne miary
- Sales
- Sales YTD
- Sales YoY Growth
- Profit
- Profit Margin

## Wersjonowanie
- v1.0 – wdrożenie produkcyjne (2026-02-10)
- v1.1 – dodano RLS (Salesperson)
5.2. Skrypty i definicje miar
Jeżeli definiujesz miary z głowy lub kopiujesz z labów (jak te nasze: YTD, YoY, itp.), warto trzymać je również w:

osobnym pliku .dax,

albo w .md z fragmentami kodu.

Przykład:

reports/sales-analysis/measures/SalesMeasures.dax

dax
Skopiuj kod
Sales =
SUM ( Sales[Sales] )

Sales YTD =
TOTALYTD (
    [Sales],
    'Date'[Date],
    "6-30"
)

Sales YoY Growth =
VAR SalesPriorYear =
    CALCULATE (
        [Sales],
        PARALLELPERIOD ( 'Date'[Date], -12, MONTH )
    )
RETURN
    DIVIDE ( [Sales] - SalesPriorYear, SalesPriorYear )
To daje:

szybki podgląd historii zmian miar,

możliwość dzielenia się „snippetami” z innymi,

łatwe porównanie wersji.

6. Przykładowy workflow GIT + Power BI (PBIX)
Praktyczny scenariusz pracy nad raportem:

Utwórz brancha

bash
Skopiuj kod
git checkout -b feature/pbi-sales-add-time-intelligence
Otwórz PBIX, wprowadź zmiany

dodajesz miary YTD, YoY, itd.

modyfikujesz strony raportu

Aktualizujesz dokumentację

measures/*.dax

README.md

Commit

bash
Skopiuj kod
git status
git add reports/sales-analysis/SalesAnalysis.pbix
git add reports/sales-analysis/measures/SalesMeasures.dax
git add reports/sales-analysis/README.md

git commit -m "feat(pbi-sales): dodano miary YTD i YoY + aktualizacja dokumentacji"
Push + PR

bash
Skopiuj kod
git push origin feature/pbi-sales-add-time-intelligence
otwierasz PR,

w opisie wpisujesz co konkretnie zmieniono w raporcie,

ew. robisz review sam sobie (jeśli GitHub dla 1 osoby 😉).

Merge do main

7. Rekomendacje „produkcyjne”
Jeżeli planujesz:

raporty produkcyjne dla firmy

lub materiały szkoleniowe (np. dla studentów)

to:

Trzymaj PBIX / PBIP w jednym miejscu (np. reports/).

Do każdego raportu:

README,

changelog (w README lub osobno),

miary w plikach tekstowych.

Taguj wersje produkcyjne.

Nie rozwijaj wielu branchy naraz na tym samym PBIX – to proszenie się o konflikty.

Jeżeli możesz – testowo przejdź na Project (PBIP) dla jednego raportu i zobacz, czy pasuje Ci styl pracy.

8. TL;DR – skrót dla niecierpliwych
PBIX = binarka → Git służy głównie do historii i backupu, nie do diffów.

Dodatkowo trzymaj:

dokumentację (.md),

skrypty miar (.dax),

strukturę repo (reports/, docs/).

Feature branch → zmiany → commit → PR → merge.

Przy intensywnej pracy zespołowej rozważ Power BI Project (.pbip).