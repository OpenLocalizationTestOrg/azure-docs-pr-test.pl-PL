---
title: "Samouczek usługi Azure Cosmos DB: Tworzenie, wykonywanie zapytań i przechodzenie w konsoli Apache TinkerPops Gremlin | Microsoft Docs"
description: "Toocreates Szybki Start Azure DB rozwiązania Cosmos wierzchołków, krawędzie i zapytań przy użyciu hello DB Azure rozwiązania Cosmos interfejsu API programu Graph."
services: cosmos-db
author: dennyglee
manager: jhubbard
editor: monicar
ms.assetid: bf08e031-718a-4a2a-89d6-91e12ff8797d
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: terminal
ms.topic: hero-article
ms.date: 07/27/2017
ms.author: denlee
ms.openlocfilehash: 9de64c97fec89c45cecba9e14214db472ec76f57
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmos-db-create-query-and-traverse-a-graph-in-hello-gremlin-console"></a>Azure rozwiązania Cosmos bazy danych: Utwórz zapytanie i przechodzić między nimi wykres w konsoli Gremlin hello

Azure Cosmos DB to rozproszona globalnie wielomodelowa usługa bazy danych firmy Microsoft. Można szybko utworzyć i wyszukiwać dokumentu, klucza i wartości i wykres baz danych, które korzystają z dystrybucji globalne hello i możliwości skalowanie w poziomie na podstawowe hello Azure DB rozwiązania Cosmos. 

To szybki start pokazano, jak toocreate konta bazy danych Azure rozwiązania Cosmos, bazy danych i wykres (kontener) przy użyciu hello portalu Azure, a następnie użyj hello [konsoli Gremlin](https://tinkerpop.apache.org/docs/current/reference/#gremlin-console) z [Apache TinkerPop](http://tinkerpop.apache.org) toowork z Wykres danych interfejsu API (wersja zapoznawcza). W tym samouczku Utwórz i zapytania wierzchołków i krawędzi, aktualizowanie właściwości wierzchołków zapytania wierzchołków, przechodzenie przez wykres hello i upuść wierzchołka.

![Azure DB rozwiązania Cosmos z hello Apache Gremlin konsoli](./media/create-graph-gremlin-console/gremlin-console.png)

Konsola Gremlin Hello jest Groovy/Java i działa w systemie Linux, Mac i systemu Windows. Można go pobrać ze hello [lokacji Apache TinkerPop](https://www.apache.org/dyn/closer.lua/tinkerpop/3.2.5/apache-tinkerpop-gremlin-console-3.2.5-bin.zip).

## <a name="prerequisites"></a>Wymagania wstępne

Toohave toocreate subskrypcji platformy Azure, konto bazy danych Azure rozwiązania Cosmos jest wymagane dla tego przewodnika Szybki Start.

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

Należy również tooinstall hello [konsoli Gremlin](http://tinkerpop.apache.org/). Użyj wersji 3.2.5 lub nowszej.

## <a name="create-a-database-account"></a>Tworzenie konta bazy danych

[!INCLUDE [cosmos-db-create-dbaccount-graph](../../includes/cosmos-db-create-dbaccount-graph.md)]

## <a name="add-a-graph"></a>Dodawanie grafu

[!INCLUDE [cosmos-db-create-graph](../../includes/cosmos-db-create-graph.md)]

## <a id="ConnectAppService"></a>Połącz tooyour usługi aplikacji
1. Przed rozpoczęciem hello Gremlin konsoli, Utwórz lub zmodyfikuj plik konfiguracji zdalnego secure.yaml hello w katalogu apache-tinkerpop-gremlin-console-3.2.5/conf hello.
2. Wypełnij ustawienia konfiguracji *host*, *port*, *username*, *password*, *connectionPool* i *serializer*:

    Ustawienie|Sugerowana wartość|Opis
    ---|---|---
    hosty|[***.graphs.azure.com]|Zobacz poniższy zrzut ekranu. Jest to wartość identyfikatora URI Gremlin hello na stronie Przegląd hello hello portalu Azure w nawiasach kwadratowych spacją hello: 443 / usunięty.<br><br>Tę wartość można również pobrać z karty klucze hello, przy użyciu wartości identyfikatora URI hello usuwanie https://, zmieniając toographs dokumentów i usuwanie końcowe hello: 443 /.
    port|443|Ustaw too443.
    nazwa użytkownika|*Twoja nazwa użytkownika*|Witaj zasobów formularza hello `/dbs/<db>/colls/<coll>` gdzie `<db>` jest nazwa bazy danych i `<coll>` oznacza nazwę kolekcji.
    hasło|*Twój klucz podstawowy*| Zobacz drugi zrzut ekranu poniżej. Jest to klucz podstawowy, który można pobrać ze strony klucze hello hello portalu Azure, w polu klucza podstawowego hello. Użyj przycisku Kopiuj hello po lewej stronie powitania hello pole toocopy hello wartość.
    connectionPool|{enableSsl: true}|Ustawienie puli połączeń protokołu SSL.
    serializer|{ className: org.apache.tinkerpop.gremlin.<br>driver.ser.GraphSONMessageSerializerV1d0,<br> config: { serializeResultToString: true }}|Ustaw wartość toothis i usunięcie wszystkich `\n` podziały podczas wklejania hello wartości.

    Dla wartości hostów hello, skopiuj hello **Gremlin URI** wartość z zakresu od hello **omówienie** strony: ![wyświetlanie i kopiowanie wartość identyfikatora URI Gremlin hello na stronie Przegląd hello hello portalu Azure](./media/create-graph-gremlin-console/gremlin-uri.png)

    W przypadku wartości hasła hello, skopiuj hello **klucza podstawowego** z hello **klucze** strony: ![wyświetlanie i kopiowanie kluczy primary key w hello portalu Azure, strony](./media/create-graph-gremlin-console/keys.png)


3. W terminalu, uruchom `bin/gremlin.bat` lub `bin/gremlin.sh` toostart hello [konsoli Gremlin](http://tinkerpop.apache.org/docs/3.2.5/tutorials/getting-started/).
4. W terminalu, uruchom `:remote connect tinkerpop.server conf/remote-secure.yaml` tooconnect tooyour aplikacji usługi.

    > [!TIP]
    > Jeśli wystąpi błąd hello `No appenders could be found for logger` upewnij się, zaktualizowano hello serializator wartość w pliku zdalnego secure.yaml hello, zgodnie z opisem w kroku 2. 

Wspaniale! Teraz, gdy zakończeniu hello instalacji, Zacznijmy niektóre polecenia konsoli.

Wypróbujmy proste polecenie count(). Wpisz następujące hello do konsoli hello w wierszu hello:
```
:> g.V().count()
```

> [!TIP]
> Powiadomienie hello `:>` czy poprzedza hello `g.V().count()` tekst? 
>
> Jest to część polecenia hello potrzebne tootype. Jest ważne podczas korzystania z bazy danych Azure rozwiązania Cosmos hello Gremlin konsoli.  
>
> Pominięcie to `:>` prefiks nakazuje hello tooexecute hello polecenie konsoli lokalnie, często względem wykresu w pamięci.
> Za pomocą tej `:>` informuje tooexecute konsoli hello polecenia zdalnego, w tym przypadku przed DB rozwiązania Cosmos (albo emulatora localhost hello, lub > wystąpienia platformy Azure).


## <a name="create-vertices-and-edges"></a>Tworzenie wierzchołków i krawędzi

Zacznijmy od dodania wierzchołków dla pięciu osób: *Thomas*, *Mary Kay*, *Robin*, *Ben* i *Jack*.

Dane wejściowe (Thomas):

```
:> g.addV('person').property('firstName', 'Thomas').property('lastName', 'Andersen').property('age', 44).property('userid', 1)
```

Dane wyjściowe:

```
==>[id:796cdccc-2acd-4e58-a324-91d6f6f5ed6d,label:person,type:vertex,properties:[firstName:[[id:f02a749f-b67c-4016-850e-910242d68953,value:Thomas]],lastName:[[id:f5fa3126-8818-4fda-88b0-9bb55145ce5c,value:Andersen]],age:[[id:f6390f9c-e563-433e-acbf-25627628016e,value:44]],userid:[[id:796cdccc-2acd-4e58-a324-91d6f6f5ed6d|userid,value:1]]]]
```
Dane wejściowe (Mary Kay):

```
:> g.addV('person').property('firstName', 'Mary Kay').property('lastName', 'Andersen').property('age', 39).property('userid', 2)

```

Dane wyjściowe:

```
==>[id:0ac9be25-a476-4a30-8da8-e79f0119ea5e,label:person,type:vertex,properties:[firstName:[[id:ea0604f8-14ee-4513-a48a-1734a1f28dc0,value:Mary Kay]],lastName:[[id:86d3bba5-fd60-4856-9396-c195ef7d7f4b,value:Andersen]],age:[[id:bc81b78d-30c4-4e03-8f40-50f72eb5f6da,value:39]],userid:[[id:0ac9be25-a476-4a30-8da8-e79f0119ea5e|userid,value:2]]]]

```

Dane wejściowe (Robin):

```
:> g.addV('person').property('firstName', 'Robin').property('lastName', 'Wakefield').property('userid', 3)
```

Dane wyjściowe:

```
==>[id:8dc14d6a-8683-4a54-8d74-7eef1fb43a3e,label:person,type:vertex,properties:[firstName:[[id:ec65f078-7a43-4cbe-bc06-e50f2640dc4e,value:Robin]],lastName:[[id:a3937d07-0e88-45d3-a442-26fcdfb042ce,value:Wakefield]],userid:[[id:8dc14d6a-8683-4a54-8d74-7eef1fb43a3e|userid,value:3]]]]
```

Dane wejściowe (Ben):

```
:> g.addV('person').property('firstName', 'Ben').property('lastName', 'Miller').property('userid', 4)

```

Dane wyjściowe:

```
==>[id:ee86b670-4d24-4966-9a39-30529284b66f,label:person,type:vertex,properties:[firstName:[[id:a632469b-30fc-4157-840c-b80260871e9a,value:Ben]],lastName:[[id:4a08d307-0719-47c6-84ae-1b0b06630928,value:Miller]],userid:[[id:ee86b670-4d24-4966-9a39-30529284b66f|userid,value:4]]]]
```

Dane wejściowe (Jack):

```
:> g.addV('person').property('firstName', 'Jack').property('lastName', 'Connor').property('userid', 5)
```

Dane wyjściowe:

```
==>[id:4c835f2a-ea5b-43bb-9b6b-215488ad8469,label:person,type:vertex,properties:[firstName:[[id:4250824e-4b72-417f-af98-8034aa15559f,value:Jack]],lastName:[[id:44c1d5e1-a831-480a-bf94-5167d133549e,value:Connor]],userid:[[id:4c835f2a-ea5b-43bb-9b6b-215488ad8469|userid,value:5]]]]
```


Następnie dodajmy krawędzie dla relacji między tymi osobami.

Dane wejściowe (Thomas -> Mary Kay):

```
:> g.V().hasLabel('person').has('firstName', 'Thomas').addE('knows').to(g.V().hasLabel('person').has('firstName', 'Mary Kay'))
```

Dane wyjściowe:

```
==>[id:c12bf9fb-96a1-4cb7-a3f8-431e196e702f,label:knows,type:edge,inVLabel:person,outVLabel:person,inV:0d1fa428-780c-49a5-bd3a-a68d96391d5c,outV:1ce821c6-aa3d-4170-a0b7-d14d2a4d18c3]
```

Dane wejściowe (Thomas -> Robin):

```
:> g.V().hasLabel('person').has('firstName', 'Thomas').addE('knows').to(g.V().hasLabel('person').has('firstName', 'Robin'))
```

Dane wyjściowe:

```
==>[id:58319bdd-1d3e-4f17-a106-0ddf18719d15,label:knows,type:edge,inVLabel:person,outVLabel:person,inV:3e324073-ccfc-4ae1-8675-d450858ca116,outV:1ce821c6-aa3d-4170-a0b7-d14d2a4d18c3]
```

Dane wejściowe (Robin -> Ben):

```
:> g.V().hasLabel('person').has('firstName', 'Robin').addE('knows').to(g.V().hasLabel('person').has('firstName', 'Ben'))
```

Dane wyjściowe:

```
==>[id:889c4d3c-549e-4d35-bc21-a3d1bfa11e00,label:knows,type:edge,inVLabel:person,outVLabel:person,inV:40fd641d-546e-412a-abcc-58fe53891aab,outV:3e324073-ccfc-4ae1-8675-d450858ca116]
```

## <a name="update-a-vertex"></a>Aktualizowanie wierzchołka

Ta funkcja pozwala zaktualizować hello *blogu Thomasa* wierzchołka z nowego wiek *45*.

Dane wejściowe:
```
:> g.V().hasLabel('person').has('firstName', 'Thomas').property('age', 45)
```
Dane wyjściowe:

```
==>[id:ae36f938-210e-445a-92df-519f2b64c8ec,label:person,type:vertex,properties:[firstName:[[id:872090b6-6a77-456a-9a55-a59141d4ebc2,value:Thomas]],lastName:[[id:7ee7a39a-a414-4127-89b4-870bc4ef99f3,value:Andersen]],age:[[id:a2a75d5a-ae70-4095-806d-a35abcbfe71d,value:45]]]]
```

## <a name="query-your-graph"></a>Wykonywanie zapytania względem grafu

Teraz uruchommy różne zapytania względem grafu.

Po pierwsze spróbujmy zapytania z filtru tooreturn tylko osoby, które są starsze niż 40 lat.

Dane wejściowe (zapytanie filtru):

```
:> g.V().hasLabel('person').has('age', gt(40))
```

Dane wyjściowe:

```
==>[id:ae36f938-210e-445a-92df-519f2b64c8ec,label:person,type:vertex,properties:[firstName:[[id:872090b6-6a77-456a-9a55-a59141d4ebc2,value:Thomas]],lastName:[[id:7ee7a39a-a414-4127-89b4-870bc4ef99f3,value:Andersen]],age:[[id:a2a75d5a-ae70-4095-806d-a35abcbfe71d,value:45]]]]
```

Następnie Załóżmy projekt hello imię osoby hello, które są starsze niż 40 lat.

Dane wejściowe (zapytanie filtru i projekcji):

```
:> g.V().hasLabel('person').has('age', gt(40)).values('firstName')
```

Dane wyjściowe:

```
==>Thomas
```

## <a name="traverse-your-graph"></a>Przechodzenie grafu

Umożliwia przenoszenie hello wykres tooreturn wszystkie w blogu Thomasa znajomych.

Dane wejściowe (znajomi Thomasa):

```
:> g.V().hasLabel('person').has('firstName', 'Thomas').outE('knows').inV().hasLabel('person')
```

Dane wyjściowe: 

```
==>[id:f04bc00b-cb56-46c4-a3bb-a5870c42f7ff,label:person,type:vertex,properties:[firstName:[[id:14feedec-b070-444e-b544-62be15c7167c,value:Mary Kay]],lastName:[[id:107ab421-7208-45d4-b969-bbc54481992a,value:Andersen]],age:[[id:4b08d6e4-58f5-45df-8e69-6b790b692e0a,value:39]]]]
==>[id:91605c63-4988-4b60-9a30-5144719ae326,label:person,type:vertex,properties:[firstName:[[id:f760e0e6-652a-481a-92b0-1767d9bf372e,value:Robin]],lastName:[[id:352a4caa-bad6-47e3-a7dc-90ff342cf870,value:Wakefield]]]]
```

Następnie zaloguj się hello warstwy następnym wierzchołków. Przenoszenie wszystkich hello znajomych przyjaciół w blogu Thomasa hello tooreturn wykresu.

Dane wejściowe (znajomi znajomych Thomasa):

```
:> g.V().hasLabel('person').has('firstName', 'Thomas').outE('knows').inV().hasLabel('person').outE('knows').inV().hasLabel('person')
```
Dane wyjściowe:

```
==>[id:a801a0cb-ee85-44ee-a502-271685ef212e,label:person,type:vertex,properties:[firstName:[[id:b9489902-d29a-4673-8c09-c2b3fe7f8b94,value:Ben]],lastName:[[id:e084f933-9a4b-4dbc-8273-f0171265cf1d,value:Miller]]]]
```

## <a name="drop-a-vertex"></a>Usuwanie wierzchołka

Umożliwia teraz usunąć wierzchołek z bazy danych wykresu hello.

Dane wejściowe (usunięcie wierzchołka Jacka):

```
:> g.V().hasLabel('person').has('firstName', 'Jack').drop()
```

## <a name="clear-your-graph"></a>Czyszczenie grafu

Na koniec Przyjrzyjmy Wyczyść bazę danych hello wszystkich wierzchołków i krawędzi.

Dane wejściowe:

```
:> g.E().drop()
:> g.V().drop()
```

Gratulacje! Pomyślnie ukończono samouczek interfejsu API programu Graph w usłudze Azure Cosmos DB!

## <a name="review-slas-in-hello-azure-portal"></a>Przejrzyj umowy SLA w hello portalu Azure

[!INCLUDE [cosmosdb-tutorial-review-slas](../../includes/cosmos-db-tutorial-review-slas.md)]

## <a name="clean-up-resources"></a>Oczyszczanie zasobów

Jeśli nie będzie toocontinue toouse tej aplikacji, należy usunąć wszystkie zasoby utworzone przez tego przewodnika Szybki Start w hello portalu Azure z hello następujące kroki:  

1. Z menu po lewej stronie powitania w hello portalu Azure, kliknij przycisk **grup zasobów** a następnie kliknij nazwę hello zasobu hello został utworzony. 
2. Na stronie grupy zasobów, kliknij przycisk **usunąć**, wpisz nazwę hello toodelete zasobów hello w polu tekstowym hello, a następnie kliknij **usunąć**.

## <a name="next-steps"></a>Następne kroki

W tym szybkiego startu kiedy znasz już jak toocreate konto bazy danych Azure rozwiązania Cosmos utworzyć wykres przy użyciu hello Eksploratora danych, tworzyć wierzchołki i krawędzi i przechodzić między nimi przy użyciu konsoli Gremlin hello wykresu. Teraz możesz tworzyć bardziej złożone zapytania i implementować zaawansowaną logikę przechodzenia grafu za pomocą języka Gremlin. 

> [!div class="nextstepaction"]
> [Wykonywanie zapytań przy użyciu języka Gremlin](tutorial-query-graph.md)
