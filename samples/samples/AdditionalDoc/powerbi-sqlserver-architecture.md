# Power BI + SQL Server – Architektura SQLManiaka

## Widoki pod Power BI
Twórz widoki: vw_Fact*, vw_Dim* jako warstwę semantyczną.

## Materializowane tabele
Gdy logika jest kosztowna – materializować ETL.

## Indeksy pod DirectQuery
Stosować indeksy kompozytowe i columnstore.

## Query Folding
Unikać operacji łamiących folding, np. FORMAT(), merge po obliczonych kolumnach.

## RLS: SQL vs Power BI
SQL – kontrola danych; Power BI – kontrola wymiarów.

## Hybrid Tables
Idealne dla dużych tabel faktów z częścią historyczną.
