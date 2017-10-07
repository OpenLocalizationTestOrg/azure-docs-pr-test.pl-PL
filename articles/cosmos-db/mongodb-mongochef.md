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
# <a name="use-mongochef-with-an-azure-cosmos-db-api-for-mongodb-account"></a><span data-ttu-id="741f2-104">Użyj MongoChef z bazy danych Azure rozwiązania Cosmos: interfejsu API dla konta bazy danych MongoDB</span><span class="sxs-lookup"><span data-stu-id="741f2-104">Use MongoChef with an Azure Cosmos DB: API for MongoDB account</span></span>

<span data-ttu-id="741f2-105">tooan tooconnect bazy danych Azure rozwiązania Cosmos: interfejsu API dla konta bazy danych MongoDB, musi:</span><span class="sxs-lookup"><span data-stu-id="741f2-105">tooconnect tooan Azure Cosmos DB: API for MongoDB account, you must:</span></span>

* <span data-ttu-id="741f2-106">Pobierz i zainstaluj [MongoChef](http://3t.io/mongochef)</span><span class="sxs-lookup"><span data-stu-id="741f2-106">Download and install [MongoChef](http://3t.io/mongochef)</span></span>
* <span data-ttu-id="741f2-107">Z bazy danych rozwiązania Cosmos Azure ma: interfejsu API dla konta bazy danych MongoDB [ciąg połączenia](connect-mongodb-account.md) informacji</span><span class="sxs-lookup"><span data-stu-id="741f2-107">Have your Azure Cosmos DB: API for MongoDB account [connection string](connect-mongodb-account.md) information</span></span>

## <a name="create-hello-connection-in-mongochef"></a><span data-ttu-id="741f2-108">Utwórz połączenie hello w MongoChef</span><span class="sxs-lookup"><span data-stu-id="741f2-108">Create hello connection in MongoChef</span></span>
<span data-ttu-id="741f2-109">tooadd Twojego Azure DB rozwiązania Cosmos: interfejsu API dla bazy danych MongoDB konta toohello MongoChef Menedżera połączeń, należy wykonać hello następujące kroki.</span><span class="sxs-lookup"><span data-stu-id="741f2-109">tooadd your Azure Cosmos DB: API for MongoDB account toohello MongoChef connection manager, perform hello following steps.</span></span>

1. <span data-ttu-id="741f2-110">Pobieranie Twojej bazy danych rozwiązania Cosmos Azure: interfejs API dla bazy danych MongoDB połączenia przy użyciu instrukcji hello [tutaj](connect-mongodb-account.md).</span><span class="sxs-lookup"><span data-stu-id="741f2-110">Retrieve your Azure Cosmos DB: API for MongoDB connection information using hello instructions [here](connect-mongodb-account.md).</span></span>

    ![Zrzut ekranu przedstawiający blok ciągu połączenia hello](./media/mongodb-mongochef/ConnectionStringBlade.png)
2. <span data-ttu-id="741f2-112">Kliknij przycisk **Connect** tooopen hello Menedżera połączeń, a następnie kliknij przycisk **nowego połączenia**</span><span class="sxs-lookup"><span data-stu-id="741f2-112">Click **Connect** tooopen hello Connection Manager, then click **New Connection**</span></span>

    ![Zrzut ekranu przedstawiający Menedżera połączeń MongoChef hello](./media/mongodb-mongochef/ConnectionManager.png)
3. <span data-ttu-id="741f2-114">W hello **nowe połączenie** okna na powitania **serwera** wprowadź hello hosta (FQDN) hello Azure DB rozwiązania Cosmos: interfejsu API dla portu konta i hello bazy danych MongoDB.</span><span class="sxs-lookup"><span data-stu-id="741f2-114">In hello **New Connection** window, on hello **Server** tab, enter hello HOST (FQDN) of hello Azure Cosmos DB: API for MongoDB account and hello PORT.</span></span>

    ![Zrzut ekranu: karta hello MongoChef połączenia Menedżera serwera](./media/mongodb-mongochef/ConnectionManagerServerTab.png)
4. <span data-ttu-id="741f2-116">W hello **nowe połączenie** okna na powitania **uwierzytelniania** , wybierz pozycję tryb uwierzytelniania **Standard (CR bazy danych MONGODB lub SCARM-SHA-1)** , a następnie wprowadź hello nazwy użytkownika i HASŁO.</span><span class="sxs-lookup"><span data-stu-id="741f2-116">In hello **New Connection** window, on hello **Authentication** tab, choose Authentication Mode **Standard (MONGODB-CR or SCARM-SHA-1)** and enter hello USERNAME and PASSWORD.</span></span>  <span data-ttu-id="741f2-117">Zaakceptuj hello domyślne uwierzytelnianie db (Administrator) lub podać własne wartości.</span><span class="sxs-lookup"><span data-stu-id="741f2-117">Accept hello default authentication db (admin) or provide your own value.</span></span>

    ![Zrzut ekranu przedstawiający kartę hello MongoChef połączenia Menedżer uwierzytelniania](./media/mongodb-mongochef/ConnectionManagerAuthenticationTab.png)
5. <span data-ttu-id="741f2-119">W hello **nowe połączenie** okna na powitania **SSL** pozycję Sprawdź hello **tooconnect protokołu SSL używany** pole wyboru i hello **SSL z podpisem własnym serwera Zaakceptuj Certyfikaty** przycisk radiowy.</span><span class="sxs-lookup"><span data-stu-id="741f2-119">In hello **New Connection** window, on hello **SSL** tab, check hello **Use SSL protocol tooconnect** check box and hello **Accept server self-signed SSL certificates** radio button.</span></span>

    ![Zrzut ekranu przedstawiający kartę hello MongoChef połączenia Menedżer protokołu SSL](./media/mongodb-mongochef/ConnectionManagerSSLTab.png)
6. <span data-ttu-id="741f2-121">Kliknij hello **Testuj połączenie** toovalidate hello — informacje o połączeniu, kliknij **OK** tooreturn toohello nowe połączenie okna, a następnie kliknij przycisk **zapisać**.</span><span class="sxs-lookup"><span data-stu-id="741f2-121">Click hello **Test Connection** button toovalidate hello connection information, click **OK** tooreturn toohello New Connection window, and then click **Save**.</span></span>

    ![Zrzut ekranu przedstawiający okno połączenia testowego MongoChef hello](./media/mongodb-mongochef/TestConnectionResults.png)

## <a name="use-mongochef-toocreate-a-database-collection-and-documents"></a><span data-ttu-id="741f2-123">Użyj toocreate MongoChef bazy danych, kolekcji i dokumentów</span><span class="sxs-lookup"><span data-stu-id="741f2-123">Use MongoChef toocreate a database, collection, and documents</span></span>
<span data-ttu-id="741f2-124">toocreate bazy danych, kolekcji i dokumentów za pomocą MongoChef, należy wykonać hello następujące kroki.</span><span class="sxs-lookup"><span data-stu-id="741f2-124">toocreate a database, collection, and documents using MongoChef, perform hello following steps.</span></span>

1. <span data-ttu-id="741f2-125">W **Menedżera połączeń**, zaznacz hello połączeń i kliknij **Connect**.</span><span class="sxs-lookup"><span data-stu-id="741f2-125">In **Connection Manager**, highlight hello connection and click **Connect**.</span></span>

    ![Zrzut ekranu przedstawiający Menedżera połączeń MongoChef hello](./media/mongodb-mongochef/ConnectToAccount.png)
2. <span data-ttu-id="741f2-127">Host powitania kliknij prawym przyciskiem myszy i wybierz polecenie **dodawania bazy danych**.</span><span class="sxs-lookup"><span data-stu-id="741f2-127">Right click hello host and choose **Add Database**.</span></span>  <span data-ttu-id="741f2-128">Podaj nazwę bazy danych, a następnie kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="741f2-128">Provide a database name and click **OK**.</span></span>

    ![Zrzut ekranu przedstawiający hello opcja MongoChef dodawania bazy danych](./media/mongodb-mongochef/AddDatabase1.png)
3. <span data-ttu-id="741f2-130">Kliknij prawym przyciskiem myszy hello bazy danych i wybierz polecenie **Dodaj kolekcji**.</span><span class="sxs-lookup"><span data-stu-id="741f2-130">Right click hello database and choose **Add Collection**.</span></span>  <span data-ttu-id="741f2-131">Podaj nazwę kolekcji, a następnie kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="741f2-131">Provide a collection name and click **Create**.</span></span>

    ![Zrzut ekranu przedstawiający hello opcja MongoChef Dodaj kolekcji](./media/mongodb-mongochef/AddCollection.png)
4. <span data-ttu-id="741f2-133">Kliknij przycisk hello **kolekcji** menu elementu, następnie kliknij przycisk **Dodawanie dokumentu**.</span><span class="sxs-lookup"><span data-stu-id="741f2-133">Click hello **Collection** menu item, then click **Add Document**.</span></span>

    ![Zrzut ekranu przedstawiający hello MongoChef Dodaj element menu](./media/mongodb-mongochef/AddDocument1.png)
5. <span data-ttu-id="741f2-135">W oknie dialogowym Dodawanie dokumentu hello Wklej hello poniżej, a następnie kliknij przycisk **Dodawanie dokumentu**.</span><span class="sxs-lookup"><span data-stu-id="741f2-135">In hello Add Document dialog, paste hello following and then click **Add Document**.</span></span>

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
6. <span data-ttu-id="741f2-136">Dodawanie innego dokumentu, tym razem z powitania po zawartości.</span><span class="sxs-lookup"><span data-stu-id="741f2-136">Add another document, this time with hello following content.</span></span>

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
7. <span data-ttu-id="741f2-137">Wykonaj przykładowe zapytanie.</span><span class="sxs-lookup"><span data-stu-id="741f2-137">Execute a sample query.</span></span> <span data-ttu-id="741f2-138">Na przykład wyszukiwanie o hello nazwisko "Andersen" i pola stanu i zwracany hello nadrzędnych.</span><span class="sxs-lookup"><span data-stu-id="741f2-138">For example, search for families with hello last name 'Andersen' and return hello parents and state fields.</span></span>

    ![Zrzut ekranu przedstawiający Mongo Chef wyników zapytania](./media/mongodb-mongochef/QueryDocument1.png)

## <a name="next-steps"></a><span data-ttu-id="741f2-140">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="741f2-140">Next steps</span></span>
* <span data-ttu-id="741f2-141">Zapoznaj się z rozwiązania Cosmos Azure DB: Interfejs API, bazy danych mongodb [przykłady](mongodb-samples.md).</span><span class="sxs-lookup"><span data-stu-id="741f2-141">Explore Azure Cosmos DB: API for MongoDB [samples](mongodb-samples.md).</span></span>
