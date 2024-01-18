# Laboratorium 13
# Formaty danych i apache arrow

```{r}
# install.packages("arrow")
# install.packages("xml2")
# install.packages("haven")
# install.packages("jsonlite")
library(jsonlite) #dla plików .json
library(haven) #dla plików .sav
library(xml2) #dla plików .xml i .xsd
library(arrow)
library(dplyr)

```

## Zadanie 1: plik JSON

1.  Pobierz z serwisu Kaggle plik: <https://www.kaggle.com/datasets/rtatman/iris-dataset-json-version>
2.  Zapoznaj się z plikiem otwierając go w notatniku
3.  Wczytaj go (*fromJSON()*) i wyświetl parę pierwszych wierszy

## Zadanie 2: .sav - pliki oprogramowania SPSS

1.  Wczytaj i wyświetl pierwsze wiersze pliku *health_control.sav*

## Zadanie 3: .csv .txt

1.  Wczytaj plik *example.txt (read.csv()).* Sprawdź jaki separator jest wykorzystywany w pliku. Ustaw parametr *na.strings.*
2.  Zapisz wczytane dane to pliku csv

3.  Pojawiający się błąd wynika to z faktu że dane zostały zapisane z kolumną z numerami wierszy, jednak bez jej nazwy. W celu naprawy błędnu można na przykład ręcznie dodać nazwę kolumny edytując plik w notatniku, a następnie wczytać go z parametrem *row.names = 1.*
4.  Zapisz wczytany plik do formatu csv, pomijając indeksy wierszy (*write.csv(), ustaw row.names = FALSE*)
5.  Obejrzyj zapisany plik w notatniku

## Zadanie 4: Pliki XML

XML to format danych oparty o znacznikil. Pliki tego typu można otworzyć np. notatnikim, w celu ręcznego przejrzenia pliku, gdyż dane zapisane są w formacie czytelnym dla ludzi.

1.  Korzystając z pakietu xml2 otwórz plik *cd_catalog.xml (xml_read())*
2.  Wypisz wszystkie tytuły filmów znajdujące się w pliku *(xml_find_all(data, "znacznik/znacznik_wewnatrz_znacznika/..."), xml_text())*
3.  Oblicz ile płyt znajduje się w pliku
4.  Oblicz sumę cen wszystkich płyt (*as.numeric()*)

## Zadanie 5: Plik XML i weryfikowanie szablonem XSD

Często podczas pracy z plikami XML zachodzi poprawność zweryfikowania czy spełnia on wymagania strukturalne i semantyczne. Przydatne jest to na przykład gdy towrzymy funkcję operującą na plikach z różnych źródeł i nie chcemy aby niepoprawne pliki spowodowały błędy. Służą do tego pliki XSD

1.  Korzystając z funkcji xml_validate*()* spawdź czy plik books.xml jest zgodny z schematem
2.  Jeśeli występują jakieś problemy, otwórz plik xml (na przykład w notatniku) i dokonaj stosownych poprawek (jeżeli dodajesz jakieś dane, możesz wybrać dowolne wartości). Następnie przeprowadź walidację raz jeszcze.


## Zadanie 6: Apache arrow vs in memory

Link do pobrania pliku do zadania (ok. 100MB)

<https://aghedupl-my.sharepoint.com/:u:/g/personal/bargaw_agh_edu_pl/EW4FURQwm5tDgfLARz1g_lkBEnLRR82DgZuGFS4qeyuLWw?e=hxxQam>

Zadanie ma na celu porównanie przetwarzania danych w różnych formatach przy użyciu różnych metod:

1.  Wczytaj dane z pliku *organizations-1000000.csv* przy pomocy funkcji *read.csv()*
2.  Wczytaj dane z pliku *organizations-1000000.csv* przy pomocy funkcji *open_dataset()*
3.  Zapisz plik csv w formacie *.parquet. W tym celu użyj funkcji* *write\_*dataset*()*. Jako *dataset* podaj obiekt z wczytanym plikiem csv z punktu 2. Jako *path* ścieżkę gdzie plik ma być zapisany, a fomat ustaw jako *"parquet"*
4.  Wczytaj plik utworzony w poprzednim punkcie (*open_dataset()*).
5.  Sprawdź ile miejsca w pamięci zajmuje każdy z wczytanych obiektów. Zmierz czas jaki jest potrzebny na każdy rodzaj wczytania danych.
6.  Porównaj ile miejsca na dysku zajmuje format csv, a ile parquet
7.  Spawdź ile wierszy danych zawiera analizowany plik csv
8.  Korzystając z pipe operator oblicz sumę danych z kolumny *Number_of_employees* dla każdego z 3 sposobów wczytywania danych. W przypadku plików otwartych z wykorzystaniem pakietu arrow najpierw należy wczytać dane: ... *select(col_name) %\>% collect() %\>% ...*
9.  Zmierz czas wykonania tych obliczeń

### Materiały dodatkowe:

Przykład wykorzystania Apache arrow do obsługi danych ważących 70GB: <https://arrow-user2022.netlify.app>

<https://arrow.apache.org>

<https://global.oup.com/us/companion.websites/9780190616397/resources/spss/>

