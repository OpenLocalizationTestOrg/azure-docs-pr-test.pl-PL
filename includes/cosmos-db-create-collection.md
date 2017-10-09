Można teraz używać narzędzia Eksplorator danych hello w hello Azure toocreate portalu bazy danych i kolekcji. 

1. W portalu Azure, w menu nawigacji po lewej stronie powitania hello kliknij **Eksploratora danych (wersja zapoznawcza)**. 

2. Na powitania **Eksploratora danych (wersja zapoznawcza)** bloku, kliknij przycisk **nowej kolekcji**, a następnie podaj hello następujących informacji:

    ![Witaj bloku Eksploratora danych portalu Azure](./media/cosmos-db-create-collection/azure-cosmosdb-data-explorer.png)

    Ustawienie|Sugerowana wartość|Opis
    ---|---|---
    Identyfikator bazy danych|Zadania|Witaj nazwę nowej bazy danych. Nazwy baz danych muszą zawierać od 1 do 255 znaków i nie mogą zawierać znaków /, \\, #, ? ani mieć spacji na końcu.
    Identyfikator kolekcji|Items|Witaj nazwę nowej kolekcji. Nazwy kolekcji mają hello znak takie same wymagania bazy danych identyfikatorów.
    Pojemność magazynu| Stała (10 GB)|Użyj wartości domyślnej hello. Ta wartość jest hello pojemności hello bazy danych.
    Przepływność|400 RU|Użyj wartości domyślnej hello. Jeśli chcesz opóźnienia tooreduce przepływności hello można zwiększać później.
    Klucz partycji|/category|Klucz partycji, który równomiernie rozdziela danych tooeach partycji. Wybieranie klucza partycji poprawne hello jest ważne w tworzenie kolekcji wydajności. toolearn więcej, zobacz [projektowania partycjonowania](../articles/cosmos-db/partition-data.md#designing-for-partitioning).    
3. Po zakończeniu formularza powitania kliknij **OK**.

Pokazuje Eksploratora danych hello nowej bazy danych i kolekcji. 
