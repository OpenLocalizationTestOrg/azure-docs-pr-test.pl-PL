Po wykonaniu użyć narzędzia Eksplorator danych hello w hello Azure toocreate portalu bazy danych wykresu. 

1. W portalu Azure, w menu nawigacji po lewej stronie powitania hello kliknij **Eksploratora danych (wersja zapoznawcza)**. 
2. W hello **Eksploratora danych (wersja zapoznawcza)** bloku, kliknij przycisk **nowy wykres**, a następnie wypełnij hello strony przy użyciu hello następujących informacji.

    ![Eksplorator danych w hello portalu Azure](./media/cosmos-db-create-graph/azure-cosmosdb-data-explorer.png)

    Ustawienie|Sugerowana wartość|Opis
    ---|---|---
    Identyfikator bazy danych|sample-database|Identyfikator Hello nową bazę danych. Nazwy baz danych muszą zawierać od 1 do 255 znaków i nie mogą zawierać znaków `/ \ # ?` ani mieć spacji na końcu.
    Identyfikator grafu|sample-graph|Identyfikator Hello nowego wykresu. Wykres nazwy mają hello wymagania sam znak jako identyfikatory bazy danych.
    Pojemność magazynu| 10 GB|Pozostaw wartość domyślną hello. Jest to hello pojemności hello bazy danych.
    Przepływność|400 jednostek żądania|Pozostaw wartość domyślną hello. Można zwiększać przepływności hello później Chcąc tooreduce opóźnienia.
    Klucz partycji|/userid|Klucz partycji, który będzie równomierne danych tooeach partycji. Wybieranie hello poprawny klucz partycji to ważne w wydajności tworzenia wykresu, Dowiedz się więcej o w [projektowania partycjonowania](../articles/cosmos-db/partition-data.md#designing-for-partitioning).

3. Gdy formularz hello jest wypełniane, kliknij przycisk **OK**.
