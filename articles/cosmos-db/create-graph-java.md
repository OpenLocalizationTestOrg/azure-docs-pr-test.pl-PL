---
title: "Tworzenie bazy danych grafów Azure Cosmos DB przy użyciu języka Java | Microsoft Docs"
description: "Przykładowy kod Java, którego można używać do nawiązywania połączeń z danymi grafu i wykonywania zapytań względem nich w usłudze Azure Cosmos DB za pomocą języka Gremlin."
services: cosmos-db
documentationcenter: 
author: luisbosquez
manager: jhubbard
editor: 
ms.assetid: daacbabf-1bb5-497f-92db-079910703046
ms.service: cosmos-db
ms.custom: quick start connect, mvc
ms.workload: 
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: quickstart
ms.date: 01/08/2018
ms.author: lbosq
ms.openlocfilehash: b28300c4ed0a0c6f35bf49808b8ed12d4e180610
ms.sourcegitcommit: 9a8b9a24d67ba7b779fa34e67d7f2b45c941785e
ms.translationtype: HT
ms.contentlocale: pl-PL
ms.lasthandoff: 01/08/2018
---
# <a name="azure-cosmos-db-create-a-graph-database-using-java-and-the-azure-portal"></a>Azure Cosmos DB: Tworzenie bazy danych grafów przy użyciu języka Java i witryny Azure Portal

Azure Cosmos DB to rozproszona globalnie wielomodelowa usługa bazy danych firmy Microsoft. Usługa Azure Cosmos DB umożliwia szybkie tworzenie i wysyłanie zapytań do zarządzanych baz danych dokumentów, tabel i grafowych. 

Ten przewodnik Szybki start tworzy prostą grafową bazę danych przy użyciu narzędzi witryny Azure Portal dla usługi Azure Cosmos DB. Ponadto ten przewodnik Szybki start pokazuje, jak szybko utworzyć aplikację konsolową Java przy użyciu bazy danych grafów, korzystając ze sterownika OSS [Gremlin Java](https://mvnrepository.com/artifact/org.apache.tinkerpop/gremlin-driver). Instrukcje podane w tym przewodniku Szybki start można wykonać w dowolnym systemie operacyjnym, w którym można uruchomić oprogramowanie Java. Ten przewodnik Szybki start pozwala zaznajomić się z tworzeniem i modyfikowaniem grafów przy użyciu interfejsu użytkownika lub programowo, zgodnie z preferencjami. 

## <a name="prerequisites"></a>Wymagania wstępne
[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

Ponadto:

* [Zestaw Java Development Kit (JDK) 1.7+](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html)
    * W systemie Ubuntu uruchom polecenie `apt-get install default-jdk`, aby zainstalować zestaw JDK.
    * Upewnij się, że zmienna środowiskowa JAVA_HOME wskazuje folder, w którym zainstalowano zestaw JDK.
* [Pobierz](http://maven.apache.org/download.cgi) i [zainstaluj](http://maven.apache.org/install.html) archiwum binarne [Maven](http://maven.apache.org/)
    * W systemie Ubuntu możesz uruchomić polecenie `apt-get install maven`, aby zainstalować narzędzie Maven.
* [Git](https://www.git-scm.com/)
    * W systemie Ubuntu możesz uruchomić polecenie `sudo apt-get install git`, aby zainstalować usługę Git.

## <a name="create-a-database-account"></a>Tworzenie konta bazy danych

Przed utworzeniem bazy danych grafów musisz utworzyć konto bazy danych Gremlin (Graph) z użyciem usługi Azure Cosmos DB.

[!INCLUDE [cosmos-db-create-dbaccount-graph](../../includes/cosmos-db-create-dbaccount-graph.md)]

## <a name="add-a-graph"></a>Dodawanie grafu

Teraz możesz użyć narzędzia Eksplorator danych w witrynie Azure Portal, aby utworzyć bazę danych grafów. 

1. Kliknij pozycję **Eksplorator danych** > **Nowy graf**.

    Obszar **Dodaj graf** jest wyświetlany po prawej stronie i konieczne może być przewinięcie w prawo w celu wyświetlenia go.

    ![Eksplorator danych witryny Azure Portal, strona Dodaj graf](./media/create-graph-java/azure-cosmosdb-data-explorer-graph.png)

2. Na stronie **Dodaj graf** wprowadź ustawienia dla nowego grafu.

    Ustawienie|Sugerowana wartość|Opis
    ---|---|---
    Identyfikator bazy danych|sample-database|Wprowadź *sample-database* jako nazwę nowej bazy danych. Nazwy baz danych muszą zawierać od 1 do 255 znaków i nie mogą zawierać znaków `/ \ # ?` ani mieć spacji na końcu.
    Identyfikator grafu|sample-graph|Wprowadź *sample-graph* jako nazwę nowej kolekcji. W przypadku nazw grafów obowiązują takie same wymagania dotyczące znaków jak dla identyfikatorów baz danych.
    Pojemność magazynu|Stała (10 GB)|Zmień wartość na **Stała (10 GB)**. Ta wartość to pojemność magazynu bazy danych.
    Przepływność|400 jednostek żądania|Zmień przepływność na 400 jednostek żądania na sekundę (RU/s). Jeśli chcesz zmniejszyć opóźnienie, możesz później przeskalować przepływność w górę.

3. Po wypełnieniu formularza kliknij przycisk **OK**.

## <a name="clone-the-sample-application"></a>Klonowanie przykładowej aplikacji

Teraz przejdźmy do pracy z kodem. Sklonujemy aplikację interfejsu API programu Graph z usługi GitHub, ustawimy parametry połączenia i uruchomimy ją. Zobaczysz, jak łatwo jest pracować programowo z danymi.  

1. Otwórz wiersz polecenia, utwórz nowy folder o nazwie git-samples, a następnie zamknij wiersz polecenia.

    ```bash
    md "C:\git-samples"
    ```

2. Otwórz okno terminala usługi Git, na przykład git bash, i użyj polecenia `cd`, aby przejść do folderu instalacji aplikacji przykładowej.  

    ```bash
    cd "C:\git-samples"
    ```

3. Uruchom następujące polecenie w celu sklonowania przykładowego repozytorium. To polecenie tworzy kopię przykładowej aplikacji na komputerze. 

    ```bash
    git clone https://github.com/Azure-Samples/azure-cosmos-db-graph-java-getting-started.git
    ```

## <a name="review-the-code"></a>Przeglądanie kodu

Ten krok jest opcjonalny. Jeśli chcesz dowiedzieć się, jak zasoby bazy danych są tworzone w kodzie, możesz przejrzeć poniższe fragmenty kodu. Wszystkie fragmenty kodu pochodzą z pliku `Program.java` w folderze C:\git-samples\azure-cosmos-db-graph-java-getting-started\src\GetStarted. W przeciwnym razie możesz od razu przejść do sekcji [Aktualizowanie parametrów połączenia](#update-your-connection-information). 

* Element `Client` języka Gremlin jest inicjowany z poziomu konfiguracji w pliku `src/remote.yaml`.

    ```java
    cluster = Cluster.build(new File("src/remote.yaml")).create();
    ...
    client = cluster.connect();
    ```

* Wykonywanie serii kroków języka Gremlin przy użyciu metody `client.submit`.

    ```java
    ResultSet results = client.submit(gremlin);

    CompletableFuture<List<Result>> completableFutureResults = results.all();
    List<Result> resultList = completableFutureResults.get();

    for (Result result : resultList) {
        System.out.println(result.toString());
    }
    ```

## <a name="update-your-connection-information"></a>Aktualizowanie danych połączenia

Teraz wróć do witryny Azure Portal, aby uzyskać informacje o połączeniu i skopiować je do aplikacji. Te ustawienia umożliwiają aplikacji komunikację z hostowaną bazą danych.

1. W witrynie [Azure Portal](http://portal.azure.com/) kliknij pozycję **Klucze**. 

    Skopiuj pierwszą część wartości identyfikatora URI.

    ![Wyświetlanie i kopiowanie klucza dostępu w witrynie Azure Portal, strona Klucze](./media/create-graph-java/keys.png)
2. Otwórz plik src/remote.yaml i wklej wartość za pośrednictwem elementu `$name$` w `hosts: [$name$.graphs.azure.com]`.

    Wiersz 1 pliku remote.yaml powinien wyglądać podobnie do 

    `hosts: [test-graph.graphs.azure.com]`

3. Zmień element `graphs` na `gremlin.cosmosdb` w wartości `endpoint`. Jeśli konto bazy danych programu Graph zostało utworzone przed 20 grudnia 2017, nie wprowadzaj żadnych zmian wartości punktu końcowego i przejdź do następnego kroku.

    Wartość punktu końcowego powinna wyglądać następująco:

    `"endpoint": "https://testgraphacct.gremlin.cosmosdb.azure.com:443/"`

4. W witrynie Azure Portal użyj przycisku kopiowania, aby skopiować KLUCZ PODSTAWOWY, i wklej go za pośrednictwem elementu `$masterKey$` w `password: $masterKey$`.

    Wiersz 4 pliku remote.yaml powinien wyglądać podobnie do 

    `password: 2Ggkr662ifxz2Mg==`

5. Zmień wiersz 3 pliku remote.yaml z

    `username: /dbs/$database$/colls/$collection$`

    na 

    `username: /dbs/sample-database/colls/sample-graph`

6. Zapisz plik remote.yaml.

## <a name="run-the-console-app"></a>Uruchamianie aplikacji konsolowej

1. W oknie terminalu usługi Git za pomocą polecenia `cd` przejdź do folderu azure-cosmos-db-graph-java-getting-started.

    ```git
    cd "C:\git-samples\azure-cosmos-db-graph-java-getting-started"
    ```

2. W oknie terminala usługi Git użyj następującego polecenia, aby zainstalować wymagane pakiety języka Java.

   ```
   mvn package
   ```

3. W oknie terminala usługi Git użyj następującego polecenia, aby uruchomić aplikację języka Java.
    
    ```
    mvn exec:java -D exec.mainClass=GetStarted.Program
    ```

    W oknie terminalu zostaną wyświetlone wierzchołki dodawane do grafu. 
    
    Jeśli występują błędy przekroczenia limitu czasu, sprawdź, czy zaktualizowano poprawnie informacje o połączeniu w sekcji [Aktualizowanie danych połączenia](#update-your-connection-information), a także spróbuj ponownie uruchomić ostatnie polecenie. 
    
    Po zatrzymaniu działania programu naciśnij klawisz Enter i przejdź z powrotem do witryny Azure Portal w przeglądarce internetowej. 

<a id="add-sample-data"></a>
## <a name="review-and-add-sample-data"></a>Przeglądanie i dodawanie przykładowych danych

Teraz możesz wrócić do Eksploratora danych i zobaczyć wierzchołki dodane do grafu, a także dodać kolejne punkty danych.

1. Kliknij przycisk **Eksplorator danych**, rozwiń opcję **sample-graph**, kliknij pozycję **Graf**, a następnie **Zastosuj filtr**. 

   ![Tworzenie nowych dokumentów w Eksploratorze danych w witrynie Azure Portal](./media/create-graph-java/azure-cosmosdb-data-explorer-expanded.png)

2. Na liście **Wyniki** zwróć uwagę na nowych użytkowników dodanych do grafu. Wybierz użytkownika **ben** i zwróć uwagę, że jest połączony z użytkownikiem robin. Możesz przenosić wierzchołki, przeciągając je i upuszczając, zmieniać powiększenie przy użyciu kółka myszy oraz powiększać rozmiar grafu przy użyciu podwójnej strzałki. 

   ![Nowe wierzchołki grafu w Eksploratorze danych w witrynie Azure Portal](./media/create-graph-java/azure-cosmosdb-graph-explorer-new.png)

3. Dodajmy kilku nowych użytkowników. Kliknij przycisk **Nowy wierzchołek**, aby dodać dane do grafu.

   ![Tworzenie nowych dokumentów w Eksploratorze danych w witrynie Azure Portal](./media/create-graph-java/azure-cosmosdb-data-explorer-new-vertex.png)

4. Wprowadź etykietę *osoba*.

5. Kliknij pozycję **Dodaj właściwość**, aby dodać poszczególne poniższe właściwości. Zauważ, że możesz utworzyć unikatowe właściwości dla każdej osoby w grafie. Tylko klucz id jest wymagany.

    key|wartość|Uwagi
    ----|----|----
    id|ashley|Unikatowy identyfikator wierzchołka. Jeśli nie określono identyfikatora, zostanie on wygenerowany.
    płeć|kobieta| 
    techniczne | java | 

    > [!NOTE]
    > W tym przewodniku Szybki start tworzymy kolekcję niepartycjonowaną. Niemniej jednak, jeśli utworzysz kolekcję partycjonowaną poprzez określenie klucza partycji podczas tworzenia kolekcji, musisz uwzględnić klucz partycji jako klucz w każdym nowym wierzchołku. 

6. Kliknij przycisk **OK**. Może być konieczne rozszerzenie ekranu w celu wyświetlenia przycisku **OK** u dołu ekranu.

7. Kliknij przycisk **Nowy wierzchołek** ponownie i dodaj kolejnego nowego użytkownika. 

8. Wprowadź etykietę *osoba*.

9. Kliknij pozycję **Dodaj właściwość**, aby dodać poszczególne poniższe właściwości:

    key|wartość|Uwagi
    ----|----|----
    id|rakesh|Unikatowy identyfikator wierzchołka. Jeśli nie określono identyfikatora, zostanie on wygenerowany.
    płeć|mężczyzna| 
    szkoła|MIT| 

10. Kliknij przycisk **OK**. 

11. Kliknij przycisk **Zastosuj filtr** przy użyciu domyślnego filtru `g.V()`, aby wyświetlić wszystkie wartości na grafie. Wszyscy użytkownicy będą teraz wyświetlani na liście **Wyniki**. 

    W miarę dodawania większej ilości danych można używać filtrów do ograniczania wyników. Domyślnie Eksplorator danych korzysta z zapytania `g.V()` w celu pobrania wszystkich wierzchołków grafu. Można je zmienić na inne [zapytanie o graf](tutorial-query-graph.md), takie jak`g.V().count()`, aby zwrócić liczbę wszystkich wierzchołków grafu w formacie JSON. W przypadku zmiany filtru zmień filtr ponownie na `g.V()` i kliknij pozycję **Zastosuj filtr**, aby ponownie wyświetlić wszystkie wyniki.

12. Teraz możemy połączyć użytkowników rakesh i ashley. Upewnij się, że użytkownik **ashley** został wybrany na liście **Wyniki**, a następnie kliknij przycisk edycji obok pozycji **Cele** u dołu po prawej. Może być konieczne rozszerzenie okna w celu wyświetlenia obszaru **Właściwości**.

   ![Zmiana celu wierzchołka w grafie](./media/create-graph-java/azure-cosmosdb-data-explorer-edit-target.png)

13. W polu **Cel** wpisz *rakesh*, a w polu **Etykieta krawędzi** wpisz *zna*, a następnie kliknij pole wyboru.

   ![Dodawanie połączenia między użytkownikami ashley i rakesh w Eksploratorze danych](./media/create-graph-java/azure-cosmosdb-data-explorer-set-target.png)

14. Teraz wybierz użytkownika **rakesh** z listy wyników, aby zobaczyć, że użytkownicy ashley i rakesh są połączeni. 

   ![Dwa wierzchołki połączone w Eksploratorze danych](./media/create-graph-java/azure-cosmosdb-graph-explorer.png)

   Na tym kończy się część tego samouczka poświęcona tworzeniu zasobów. Możesz dodać do grafu kolejne wierzchołki, zmodyfikować istniejące wierzchołki lub zmienić zapytania. Teraz przejrzyjmy metryki udostępniane przez usługę Azure Cosmos DB, a następnie wyczyśćmy zasoby. 

## <a name="review-slas-in-the-azure-portal"></a>Przeglądanie umów SLA w witrynie Azure Portal

[!INCLUDE [cosmosdb-tutorial-review-slas](../../includes/cosmos-db-tutorial-review-slas.md)]

## <a name="clean-up-resources"></a>Oczyszczanie zasobów

[!INCLUDE [cosmosdb-delete-resource-group](../../includes/cosmos-db-delete-resource-group.md)]

## <a name="next-steps"></a>Następne kroki

W tym przewodniku Szybki start wyjaśniono sposób tworzenia konta usługi Azure Cosmos DB, tworzenia grafu za pomocą Eksploratora danych i uruchamiania aplikacji. Teraz możesz tworzyć bardziej złożone zapytania i implementować zaawansowaną logikę przechodzenia grafu za pomocą języka Gremlin. 

> [!div class="nextstepaction"]
> [Wykonywanie zapytań przy użyciu języka Gremlin](tutorial-query-graph.md)

