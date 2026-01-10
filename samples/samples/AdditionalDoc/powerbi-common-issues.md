# Kronika Błędów Power BI – Diagnostyka

## Powolne odświeżanie
Najczęstsze przyczyny: brak query folding, duża kardynalność, nieoptymalne transformacje.

## Auto Date/Time
Powoduje powstawanie ukrytych tabel dat – najlepiej wyłączyć.

## Cardinality Mismatch
Złe relacje 1:* prowadzą do fałszywych wyników i dużych modeli.

## SUMX vs SUM
SUMX iteruje po wierszach, SUM nie iteruje – częsty powód błędów.

## FORMAT() jako killer
FORMAT() psuje kompresję i wydajność oraz łamie folding.
