# Power BI Performance Tuning – Turbo Ściąga

## Import vs DirectQuery
Import = maksymalna wydajność; DirectQuery tylko gdy wymagane.

## Cardinality Killers
GUID-y, teksty, datetime – źródła wysokiej kardynalności.

## Auto Date/Time OFF
Tworzy ukryte tabele – wyłączyć.

## VertiPaq Analyzer
Narzędzie do analizy kompresji i ciężkich kolumn.

## FORMAT() Killer
Niszczy folding i kompresję.

## Remove unused columns
Najprostsza i najskuteczniejsza optymalizacja.
