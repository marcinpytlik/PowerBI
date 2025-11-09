# Power BI – Zasady Modelowania SQLManiaka

## Star Schema
Zalecany układ modelu: fakt + wymiary.

## Jedna tabela Date
Wszystkie fakty powinny być powiązane z jedną datą.

## Relacje jednokierunkowe
Dwukierunkowe tylko gdy konieczne (RLS/bridge).

## Kolumny ukryte, miary widoczne
Zwiększa czytelność i wymusza prawidłowe agregacje.

## Foldery wyświetlania
Porządkują model i poprawiają komfort pracy analityków.

## Opisy pól
Tworzą samoopisujący się model.
