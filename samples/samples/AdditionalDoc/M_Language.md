# Ściąga z języka M (Power Query)

## 1) Składnia bazowa
```m
let
    Źródło = Excel.Workbook(File.Contents("C:\dane.xlsx"), null, true),
    Tabela = Źródło{[Item="Sales", Kind="Table"]}[Data],
    ZmienionyTyp = Table.TransformColumnTypes(Tabela, {{"Amount", Int64.Type}, {"Date", type date}}),
    Filtrowane = Table.SelectRows(ZmienionyTyp, each [Amount] > 1000)
in
    Filtrowane
```

## 2) Typy i literały
Proste: number, text, logical, null, date, time, datetime, duration, binary  
Złożone: list, record, table, function  

## 3) Listy
```m
lst = {1,2,3,5,8};
List.Transform(lst, each _ * 10);
List.Sum(lst);
```

## 4) Rekordy
```m
rec = [Id=1, Name="A", Qty=5];
rec[Name];
```

## 5) Tabele
```m
t = #table({"Id","Name","Amount"}, {{1,"A",10},{2,"B",20}});
Table.SelectRows(t, each [Amount] > 10);
```

## 6) Teksty
Text.Upper, Text.Lower, Text.Length, Text.Split, Text.Trim

## 7) Daty i czasy
Date.Year, Date.Month, Date.AddDays, DateTime.LocalNow()

## 8) Number.*
Number.Round, Number.FromText, Number.IsNaN

## 9) try … otherwise
```m
try Number.FromText([Col]) otherwise null
```

## 10) Funkcje użytkownika
```m
(x as number) as number => x * 2
```

## 11) Źródła danych
Excel.Workbook, Csv.Document, Sql.Database, Web.Contents

## 12) Typy i metadane
Table.TransformColumnTypes, Value.Type, Type.Is

## 13) Wzorce
— Clean columns  
— Dynamic filtering  
— Left join + expand  
— Unpivot → Pivot  
— Load all CSV from folder

## 14) Wydajność
— Folding  
— Table.Buffer  
— Redukcja danych na początku

## 15) Najważniejsze funkcje
Table.*, List.*, Text.*, Date.*, Number.*, Record.*, Value.*

## 16) Diagnostyka
Query Dependencies, try/otherwise
