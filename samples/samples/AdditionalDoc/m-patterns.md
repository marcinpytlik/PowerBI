# Power Query M – Najważniejsze Patterns

## Unpivot → Clean → Expand
```M
Unpivoted = Table.UnpivotOtherColumns(Source, {"Category"}, "Attribute", "Value")
```

## Merge (Join)
```M
Merged =
Table.NestedJoin(A, {"Key"}, B, {"Key"}, "Joined", JoinKind.Inner)
```

## Append (Union)
```M
Combined = Table.Combine({Table1, Table2})
```

## Parametryzacja
```M
Parameter = "2024-01-01"
Filtered = Table.SelectRows(Source, each [Date] >= Parameter)
```

## Custom Functions
```M
(x as text) as table =>
let
    Source = Csv.Document(File.Contents(x))
in
    Source
```

## Table.Buffer
```M
Buffered = Table.Buffer(Source)
```

## Error Handling
```M
try [Column] otherwise "Error"
```
