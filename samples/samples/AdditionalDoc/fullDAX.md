# Pełna ściąga DAX – wszystkie funkcje (wersja pełna)

## 1. Funkcje agregujące
SUM – sumuje wartości kolumny.
AVERAGE – oblicza średnią wartości.
MIN – zwraca najmniejszą wartość w kolumnie.
MAX – zwraca największą wartość.
COUNT – liczy wartości liczbowe.
COUNTA – liczy wartości niepuste.
COUNTROWS – liczy wiersze tabeli.
DISTINCTCOUNT – liczy unikalne wartości.
PRODUCT – mnoży wszystkie wartości kolumny.
MEDIAN – mediana z kolumny.
MEDIANX – mediana z wyrażenia iterowanego.
SUMX – sumuje wartości obliczane w iteracji.
AVERAGEX – średnia z wyrażenia iterowanego.

## 2. Funkcje iteratorów X
SUMX – iteruje po tabeli sumując wyrażenie.
AVERAGEX – średnia z wyrażenia.
MINX – minimalna wartość wyrażenia.
MAXX – maksymalna wartość wyrażenia.
COUNTX – licznik wartości spełniających warunek.
COUNTAX – liczy niepuste wartości.
VARX.P – wariancja populacji z iteracji.
VARX.S – wariancja próbki z iteracji.
STDEVX.P – odchylenie standardowe populacji.
STDEVX.S – odchylenie standardowe próbki.
GEOMEANX – średnia geometryczna.

## 3. Funkcje logiczne
IF – zwraca wartość zależnie od warunku.
SWITCH – wybór warunku jak CASE.
AND – logiczne AND.
OR – logiczne OR.
NOT – negacja.
XOR – alternatywa wykluczająca.
COALESCE – pierwszy niepusty argument.
TRUE – zwraca TRUE.
FALSE – zwraca FALSE.

## 4. Funkcje tekstowe
CONCATENATE – łączy dwa teksty.
CONCATENATEX – łączy wiele wartości z tabeli.
LEFT – zwraca znaki od lewej.
RIGHT – znaki od prawej.
MID – fragment tekstu.
LEN – długość tekstu.
UPPER – zamienia na wielkie litery.
LOWER – zamienia na małe litery.
SUBSTITUTE – zamienia fragment tekstu.
REPLACE – podmienia fragment po pozycji.
SEARCH – wyszukuje tekst (niewrażliwe).
FIND – wyszukuje tekst (wrażliwe).
FORMAT – zamienia wartość na tekst.
UNICODE – kod Unicode znaku.
UNICHAR – znak Unicode.

## 5. Funkcje dat i czasu
TODAY – zwraca dzisiejszą datę.
NOW – data i czas.
DATE – buduje datę.
DATEDIFF – różnica w czasie.
YEAR – rok z daty.
MONTH – miesiąc.
DAY – dzień.
HOUR – godzina.
MINUTE – minuta.
SECOND – sekunda.
WEEKNUM – numer tygodnia.
WEEKDAY – dzień tygodnia.
EOMONTH – koniec miesiąca.

## 6. Funkcje Time Intelligence
SAMEPERIODLASTYEAR – ten sam okres poprzedniego roku.
PARALLELPERIOD – równoległy okres przesunięty.
DATEADD – przesuwa zakres dat.
DATESYTD – daty od początku roku.
DATESQTD – od początku kwartału.
DATESMTD – od początku miesiąca.
TOTALYTD – suma narastająco od początku roku.
TOTALQTD – kwartał.
TOTALMTD – miesiąc.
STARTOFYEAR – pierwszy dzień roku.
ENDOFYEAR – ostatni dzień roku.
STARTOFMONTH – pierwszy dzień miesiąca.

## 7. Funkcje filtrujące
CALCULATE – modyfikuje kontekst filtru.
CALCULATETABLE – zwraca tabelę w zmodyfikowanym kontekście.
FILTER – filtruje tabelę.
ALL – usuwa filtry.
ALLEXCEPT – usuwa filtry poza wskazanymi.
ALLSELECTED – usuwa filtry, ale zachowuje selekcję.
REMOVEFILTERS – usuwa wszystkie filtry.
VALUES – unikalne wartości.
DISTINCT – unikalne wiersze.
TOPN – najlepsze N.
USERELATIONSHIP – aktywuje nieaktywną relację.
CROSSFILTER – zmienia kierunek relacji.
TREATAS – narzuca filtr na inną tabelę.
EARLIER – poprzedni kontekst wiersza.

## 8. Funkcje tabelaryczne
ADDCOLUMNS – dodaje nowe kolumny.
SELECTCOLUMNS – wybiera kolumny.
SUMMARIZE – grupowanie starego typu.
SUMMARIZECOLUMNS – grupowanie zgodne z modelem.
GROUPBY – grupowanie z CURRENTGROUP.
CURRENTGROUP – bieżąca grupa w GROUPBY.
ROW – buduje tabelę jednowierszową.
CROSSJOIN – iloczyn kartezjański.
UNION – łączy tabele pionowo.
INTERSECT – część wspólna.
EXCEPT – różnica zbiorów.
NATURALINNERJOIN – naturalny join.
NATURALLEFTOUTERJOIN – left join.

## 9. Funkcje informacyjne
ISBLANK – sprawdza pustą wartość.
ISNUMBER – liczba.
ISTEXT – tekst.
ISLOGICAL – TRUE/FALSE.
ISEMPTY – tabela bez wierszy.
ISERROR – błąd w obliczeniu.
CONTAINS – zawiera wiersz spełniający warunek.
SELECTEDVALUE – jedna wybrana wartość.

## 10. Funkcje matematyczne/statystyczne
ABS – wartość bezwzględna.
ROUND – zaokrąglenie.
ROUNDUP – w górę.
ROUNDDOWN – w dół.
INT – część całkowita.
TRUNC – ucięcie bez zaokrągleń.
MOD – reszta z dzielenia.
POWER – potęga.
SQRT – pierwiastek.
LOG – logarytm.
LOG10 – log dziesiętny.
RANDBETWEEN – losowa liczba.
STDEV.P – odchylenie populacji.
STDEV.S – próbki.
VAR.P – wariancja populacji.
VAR.S – wariancja próby.

## 11. Funkcje relacyjne
RELATED – wartość z relacji 1:*.
RELATEDTABLE – wiersze z relacji *:1.
LOOKUPVALUE – odpowiednik VLOOKUP.
USERELATIONSHIP – aktywuje relację.
CROSSFILTER – kierunek filtracji.
TREATAS – nakłada filtr z innej tabeli.

## 12. Funkcje hierarchii
PATH – ścieżka hierarchii.
PATHITEM – element ścieżki.
PATHLENGTH – długość ścieżki.
PATHCONTAINS – czy ścieżka zawiera element.

## 13. Funkcje konwersji
INT – konwersja na int.
VALUE – tekst → liczba.
DATEVALUE – tekst → data.
TIMEVALUE – tekst → czas.

## 14. Funkcje logiczne
IF – warunek.
SWITCH – wiele warunków.
AND – koniunkcja.
OR – alternatywa.
NOT – negacja.

## 15. Funkcje kontekstowe
EARLIER – poprzedni kontekst.
ISINSCOPE – w zakresie hierarchii.
HASONEVALUE – jedna wartość.
HASONEFILTER – jeden filtr.

## 16. Funkcje statystyczne tabel
COUNTROWS – liczba wierszy.
DISTINCTCOUNT – liczba unikalnych.
ISFILTERED – czy filtrowana.

## 17. Funkcje tabel wirtualnych
SUMMARIZE – grupowanie.
SUMMARIZECOLUMNS – grupowanie nowoczesne.
FILTER – filtrowanie.
VALUES – unikalne wartości.

## 18. Funkcje geograficzne
ST_DISTANCE – odległość geograficzna.
ST_WITHIN – czy obiekt mieści się w innym.

## 19. Funkcje inline
VAR – zmienna.
RETURN – zwrot wartości.
DEFINE – definicje zapytań DAX.
EVALUATE – wykonanie zapytania.

## 20. Funkcje specjalne
UTCNOW – czas UTC.
UTCTODAY – data UTC.
ERROR – generuje błąd.
