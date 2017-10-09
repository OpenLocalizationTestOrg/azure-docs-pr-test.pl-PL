## <a name="repeatability-during-copy"></a>Powtarzalność podczas kopiowania
Podczas kopiowania danych tooAzure SQL/programu SQL Server z innymi danymi przechowuje jeden powtarzalności tookeep potrzeb w tooavoid zdanie niezamierzone wyników. 

Podczas kopiowania danych tooAzure bazy danych serwera SQL/SQL, działanie kopiowania zostanie przez domyślny APPEND hello zestawu danych toohello zbiornika tabelę domyślnie. Na przykład podczas kopiowania danych z źródła pliku CSV (dane wartości rozdzielonych przecinkami) zawierającego dwa rekordy tooAzure bazy danych SQL/SQL Server, to jakie tabeli hello wygląda jak:

```
ID    Product        Quantity    ModifiedDate
...    ...            ...            ...
6    Flat Washer    3            2015-05-01 00:00:00
7     Down Tube    2            2015-05-01 00:00:00
```

Załóżmy, że znaleziono błędy w pliku źródłowym i ilość zaktualizowane hello przewodu w dół od 2 too4 w pliku źródłowym hello. Wycinek danych hello uruchomić ponownie dla tego okresu, przekonasz się, że dwa nowe rekordy dołączany tooAzure bazy danych serwera SQL/SQL. Witaj poniżej założono, że żadna hello kolumn w tabeli hello nie ma ograniczenia klucza podstawowego hello.

```
ID    Product        Quantity    ModifiedDate
...    ...            ...            ...
6    Flat Washer    3            2015-05-01 00:00:00
7     Down Tube    2            2015-05-01 00:00:00
6    Flat Washer    3            2015-05-01 00:00:00
7     Down Tube    4            2015-05-01 00:00:00
```

tooavoid, konieczne będzie semantyki UPSERT toospecify przez wykorzystanie jednej z hello poniżej 2 mechanizmów podaną poniżej.

> [!NOTE]
> Wycinek można uruchomić ponownie automatycznie w fabryce danych Azure zgodnie z harmonogramem hello zasady ponawiania określone.
> 
> 

### <a name="mechanism-1"></a>Mechanizm 1
Można wykorzystać **sqlWriterCleanupScript** toofirst właściwości wykonania akcji oczyszczania po uruchomieniu wycinek. 

```json
"sink":  
{ 
  "type": "SqlSink", 
  "sqlWriterCleanupScript": "$$Text.Format('DELETE FROM table WHERE ModifiedDate >= \\'{0:yyyy-MM-dd HH:mm}\\' AND ModifiedDate < \\'{1:yyyy-MM-dd HH:mm}\\'', WindowStart, WindowEnd)"
}
```

Witaj skrypt czyszczący będzie można wykonać pierwsze podczas kopiowania dla danego wycinka, co spowoduje usunięcie danych hello z odpowiedniego wycinka toothat hello tabeli SQL. działanie Hello zostanie następnie wstawianie danych hello w hello tabeli SQL. 

Jeśli wycinek hello jest teraz ponownie uruchomić, a następnie można tam znaleźć ilość hello jest aktualizowana jako wymaganą.

```
ID    Product        Quantity    ModifiedDate
...    ...            ...            ...
6    Flat Washer    3            2015-05-01 00:00:00
7     Down Tube    4            2015-05-01 00:00:00
```

Załóżmy, że hello podkładka prosty rekord zostanie usunięte z oryginalnej csv hello. Następnie ponowne uruchomienie wycinek hello dałby w efekcie hello następujące wyniki: 

```
ID    Product        Quantity    ModifiedDate
...    ...            ...            ...
7     Down Tube    4            2015-05-01 00:00:00
```
Żadne nowe miał toobe gotowe. działanie kopiowania Hello uruchomiono hello oczyszczania toodelete hello odpowiednich danych skryptu dla tego wycinka. Następnie on hello danych wejściowych do odczytu z pliku csv hello, (który następnie zawiera tylko 1 rekord) i dodaje go do hello tabeli. 

### <a name="mechanism-2"></a>Mechanizm 2
> [!IMPORTANT]
> w tej chwili sliceIdentifierColumnName nie jest obsługiwana dla usługi Azure SQL Data Warehouse. 

Inny mechanizm tooachieve powtarzalności jest wprowadzenie dedykowanego kolumny (**sliceIdentifierColumnName**) w hello target tabeli. W tej kolumnie mogą być wykorzystane przez fabryki danych Azure tooensure hello źródłowego i docelowego Pozostań zsynchronizowane. Ta metoda działa po elastyczność zmiana lub definiowania schematu SQL tabeli docelowej hello. 

Ta kolumna będzie używany przez fabryki danych Azure na potrzeby celów powtarzalność i w procesie hello fabryki danych Azure nie dokona żadnych schematu zmiany toohello tabeli. Sposób toouse tego podejścia:

1. Zdefiniuj kolumna typu binary (32) w lokalizacji docelowej hello tabeli SQL. Nie powinno być nie ograniczeń dla tej kolumny. Teraz nazwę tej kolumny jako "ColumnForADFuseOnly" w tym przykładzie.
2. Należy użyć go w przypadku działania kopiowania hello w następujący sposób:
   
    ```json
    "sink":  
    { 
   
        "type": "SqlSink", 
        "sliceIdentifierColumnName": "ColumnForADFuseOnly"
    }
    ```

Fabryka danych Azure zostaną wyświetlone w tej kolumnie zgodnie z jego potrzeby tooensure hello źródłowym i docelowym zachować synchronizację. Witaj wartości tej kolumny nie powinna być używana poza tym kontekście przez użytkownika hello. 

Podobne toomechanism 1, działanie kopiowania zostanie automatycznie pierwszy czyszczenie danych hello na powitania, biorąc pod uwagę wycinek z hello docelowej tabeli SQL, a następnie uruchom działanie kopiowania hello zwykle tooinsert hello danych z toodestination źródła dla tego wycinka. 

