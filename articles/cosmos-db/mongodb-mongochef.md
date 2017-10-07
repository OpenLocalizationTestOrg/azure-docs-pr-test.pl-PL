---
title: "aaaUse MongoChef dla bazy danych Azure rozwiązania Cosmos | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toouse MongoChef z bazy danych Azure rozwiązania Cosmos: interfejsu API dla konta bazy danych MongoDB"
keywords: mongochef
services: cosmos-db
author: AndrewHoh
manager: jhubbard
editor: 
documentationcenter: 
ms.assetid: 352c5fb9-8772-4c5f-87ac-74885e63ecac
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/23/2017
ms.author: anhoh
ms.openlocfilehash: 4b047797b231c34ccc6f2ed02416525c6228d596
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="use-mongochef-with-an-azure-cosmos-db-api-for-mongodb-account"></a>Użyj MongoChef z bazy danych Azure rozwiązania Cosmos: interfejsu API dla konta bazy danych MongoDB

tooan tooconnect bazy danych Azure rozwiązania Cosmos: interfejsu API dla konta bazy danych MongoDB, musi:

* Pobierz i zainstaluj [MongoChef](http://3t.io/mongochef)
* Z bazy danych rozwiązania Cosmos Azure ma: interfejsu API dla konta bazy danych MongoDB [ciąg połączenia](connect-mongodb-account.md) informacji

## <a name="create-hello-connection-in-mongochef"></a>Utwórz połączenie hello w MongoChef
tooadd Twojego Azure DB rozwiązania Cosmos: interfejsu API dla bazy danych MongoDB konta toohello MongoChef Menedżera połączeń, należy wykonać hello następujące kroki.

1. Pobieranie Twojej bazy danych rozwiązania Cosmos Azure: interfejs API dla bazy danych MongoDB połączenia przy użyciu instrukcji hello [tutaj](connect-mongodb-account.md).

    ![Zrzut ekranu przedstawiający blok ciągu połączenia hello](./media/mongodb-mongochef/ConnectionStringBlade.png)
2. Kliknij przycisk **Connect** tooopen hello Menedżera połączeń, a następnie kliknij przycisk **nowego połączenia**

    ![Zrzut ekranu przedstawiający Menedżera połączeń MongoChef hello](./media/mongodb-mongochef/ConnectionManager.png)
3. W hello **nowe połączenie** okna na powitania **serwera** wprowadź hello hosta (FQDN) hello Azure DB rozwiązania Cosmos: interfejsu API dla portu konta i hello bazy danych MongoDB.

    ![Zrzut ekranu: karta hello MongoChef połączenia Menedżera serwera](./media/mongodb-mongochef/ConnectionManagerServerTab.png)
4. W hello **nowe połączenie** okna na powitania **uwierzytelniania** , wybierz pozycję tryb uwierzytelniania **Standard (CR bazy danych MONGODB lub SCARM-SHA-1)** , a następnie wprowadź hello nazwy użytkownika i HASŁO.  Zaakceptuj hello domyślne uwierzytelnianie db (Administrator) lub podać własne wartości.

    ![Zrzut ekranu przedstawiający kartę hello MongoChef połączenia Menedżer uwierzytelniania](./media/mongodb-mongochef/ConnectionManagerAuthenticationTab.png)
5. W hello **nowe połączenie** okna na powitania **SSL** pozycję Sprawdź hello **tooconnect protokołu SSL używany** pole wyboru i hello **SSL z podpisem własnym serwera Zaakceptuj Certyfikaty** przycisk radiowy.

    ![Zrzut ekranu przedstawiający kartę hello MongoChef połączenia Menedżer protokołu SSL](./media/mongodb-mongochef/ConnectionManagerSSLTab.png)
6. Kliknij hello **Testuj połączenie** toovalidate hello — informacje o połączeniu, kliknij **OK** tooreturn toohello nowe połączenie okna, a następnie kliknij przycisk **zapisać**.

    ![Zrzut ekranu przedstawiający okno połączenia testowego MongoChef hello](./media/mongodb-mongochef/TestConnectionResults.png)

## <a name="use-mongochef-toocreate-a-database-collection-and-documents"></a>Użyj toocreate MongoChef bazy danych, kolekcji i dokumentów
toocreate bazy danych, kolekcji i dokumentów za pomocą MongoChef, należy wykonać hello następujące kroki.

1. W **Menedżera połączeń**, zaznacz hello połączeń i kliknij **Connect**.

    ![Zrzut ekranu przedstawiający Menedżera połączeń MongoChef hello](./media/mongodb-mongochef/ConnectToAccount.png)
2. Host powitania kliknij prawym przyciskiem myszy i wybierz polecenie **dodawania bazy danych**.  Podaj nazwę bazy danych, a następnie kliknij przycisk **OK**.

    ![Zrzut ekranu przedstawiający hello opcja MongoChef dodawania bazy danych](./media/mongodb-mongochef/AddDatabase1.png)
3. Kliknij prawym przyciskiem myszy hello bazy danych i wybierz polecenie **Dodaj kolekcji**.  Podaj nazwę kolekcji, a następnie kliknij przycisk **Utwórz**.

    ![Zrzut ekranu przedstawiający hello opcja MongoChef Dodaj kolekcji](./media/mongodb-mongochef/AddCollection.png)
4. Kliknij przycisk hello **kolekcji** menu elementu, następnie kliknij przycisk **Dodawanie dokumentu**.

    ![Zrzut ekranu przedstawiający hello MongoChef Dodaj element menu](./media/mongodb-mongochef/AddDocument1.png)
5. W oknie dialogowym Dodawanie dokumentu hello Wklej hello poniżej, a następnie kliknij przycisk **Dodawanie dokumentu**.

        {
        "_id": "AndersenFamily",
        "lastName": "Andersen",
        "parents": [
               { "firstName": "Thomas" },
               { "firstName": "Mary Kay"}
        ],
        "children": [
           {
               "firstName": "Henriette Thaulow", "gender": "female", "grade": 5,
               "pets": [{ "givenName": "Fluffy" }]
           }
        ],
        "address": { "state": "WA", "county": "King", "city": "seattle" },
        "isRegistered": true
        }
6. Dodawanie innego dokumentu, tym razem z powitania po zawartości.

        {
        "_id": "WakefieldFamily",
        "parents": [
            { "familyName": "Wakefield", "givenName": "Robin" },
            { "familyName": "Miller", "givenName": "Ben" }
        ],
        "children": [
            {
                "familyName": "Merriam",
                 "givenName": "Jesse",
                "gender": "female", "grade": 1,
                "pets": [
                    { "givenName": "Goofy" },
                    { "givenName": "Shadow" }
                ]
            },
            {
                "familyName": "Miller",
                 "givenName": "Lisa",
                 "gender": "female",
                 "grade": 8 }
        ],
        "address": { "state": "NY", "county": "Manhattan", "city": "NY" },
        "isRegistered": false
        }
7. Wykonaj przykładowe zapytanie. Na przykład wyszukiwanie o hello nazwisko "Andersen" i pola stanu i zwracany hello nadrzędnych.

    ![Zrzut ekranu przedstawiający Mongo Chef wyników zapytania](./media/mongodb-mongochef/QueryDocument1.png)

## <a name="next-steps"></a>Następne kroki
* Zapoznaj się z rozwiązania Cosmos Azure DB: Interfejs API, bazy danych mongodb [przykłady](mongodb-samples.md).
