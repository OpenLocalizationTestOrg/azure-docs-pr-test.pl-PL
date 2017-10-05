---
title: "Użyj MongoChef dla rozwiązania Cosmos Azure DB | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak korzystać z bazy danych Azure rozwiązania Cosmos MongoChef: interfejsu API dla konta bazy danych MongoDB"
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
ms.openlocfilehash: 54c9799bd646b827f602e2ea2f9a15a4fc853f00
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="use-mongochef-with-an-azure-cosmos-db-api-for-mongodb-account"></a><span data-ttu-id="f0938-104">Użyj MongoChef z bazy danych Azure rozwiązania Cosmos: interfejsu API dla konta bazy danych MongoDB</span><span class="sxs-lookup"><span data-stu-id="f0938-104">Use MongoChef with an Azure Cosmos DB: API for MongoDB account</span></span>

<span data-ttu-id="f0938-105">Aby nawiązać połączenie bazy danych Azure rozwiązania Cosmos: interfejsu API dla konta bazy danych MongoDB, musi:</span><span class="sxs-lookup"><span data-stu-id="f0938-105">To connect to an Azure Cosmos DB: API for MongoDB account, you must:</span></span>

* <span data-ttu-id="f0938-106">Pobierz i zainstaluj [MongoChef](http://3t.io/mongochef)</span><span class="sxs-lookup"><span data-stu-id="f0938-106">Download and install [MongoChef](http://3t.io/mongochef)</span></span>
* <span data-ttu-id="f0938-107">Z bazy danych rozwiązania Cosmos Azure ma: interfejsu API dla konta bazy danych MongoDB [ciąg połączenia](connect-mongodb-account.md) informacji</span><span class="sxs-lookup"><span data-stu-id="f0938-107">Have your Azure Cosmos DB: API for MongoDB account [connection string](connect-mongodb-account.md) information</span></span>

## <a name="create-the-connection-in-mongochef"></a><span data-ttu-id="f0938-108">Utwórz połączenie w MongoChef</span><span class="sxs-lookup"><span data-stu-id="f0938-108">Create the connection in MongoChef</span></span>
<span data-ttu-id="f0938-109">Aby dodać bazy danych programu Azure rozwiązania Cosmos: interfejsu API dla konta bazy danych MongoDB MongoChef Menedżera połączeń, wykonaj następujące kroki.</span><span class="sxs-lookup"><span data-stu-id="f0938-109">To add your Azure Cosmos DB: API for MongoDB account to the MongoChef connection manager, perform the following steps.</span></span>

1. <span data-ttu-id="f0938-110">Pobieranie Twojej bazy danych rozwiązania Cosmos Azure: interfejs API dla bazy danych MongoDB informacje o połączeniu z instrukcjami [tutaj](connect-mongodb-account.md).</span><span class="sxs-lookup"><span data-stu-id="f0938-110">Retrieve your Azure Cosmos DB: API for MongoDB connection information using the instructions [here](connect-mongodb-account.md).</span></span>

    ![Zrzut ekranu przedstawiający blok ciągu połączenia](./media/mongodb-mongochef/ConnectionStringBlade.png)
2. <span data-ttu-id="f0938-112">Kliknij przycisk **Connect** aby otworzyć Menedżera połączeń, a następnie przycisk **nowego połączenia**</span><span class="sxs-lookup"><span data-stu-id="f0938-112">Click **Connect** to open the Connection Manager, then click **New Connection**</span></span>

    ![Zrzut ekranu przedstawiający MongoChef Menedżera połączeń](./media/mongodb-mongochef/ConnectionManager.png)
3. <span data-ttu-id="f0938-114">W **nowe połączenie** okna na **serwera** wprowadź hosta (FQDN) Azure DB rozwiązania Cosmos: interfejs API dla konta bazy danych MongoDB i numer portu.</span><span class="sxs-lookup"><span data-stu-id="f0938-114">In the **New Connection** window, on the **Server** tab, enter the HOST (FQDN) of the Azure Cosmos DB: API for MongoDB account and the PORT.</span></span>

    ![Zrzut ekranu przedstawiający kartę MongoChef połączenie Menedżera serwera](./media/mongodb-mongochef/ConnectionManagerServerTab.png)
4. <span data-ttu-id="f0938-116">W **nowe połączenie** okna na **uwierzytelniania** , wybierz pozycję tryb uwierzytelniania **Standard (CR bazy danych MONGODB lub SCARM-SHA-1)** , a następnie wprowadź nazwę użytkownika i hasło.</span><span class="sxs-lookup"><span data-stu-id="f0938-116">In the **New Connection** window, on the **Authentication** tab, choose Authentication Mode **Standard (MONGODB-CR or SCARM-SHA-1)** and enter the USERNAME and PASSWORD.</span></span>  <span data-ttu-id="f0938-117">Zaakceptuj domyślną db uwierzytelniania (Administrator) lub podać własne wartości.</span><span class="sxs-lookup"><span data-stu-id="f0938-117">Accept the default authentication db (admin) or provide your own value.</span></span>

    ![Zrzut ekranu: karta Uwierzytelnianie Menedżera połączeń MongoChef](./media/mongodb-mongochef/ConnectionManagerAuthenticationTab.png)
5. <span data-ttu-id="f0938-119">W **nowe połączenie** okna na **SSL** karcie wyboru **protokołu SSL używany nawiązać** pole wyboru i **akceptować certyfikaty SSL z podpisem własnym serwera**  przycisk radiowy.</span><span class="sxs-lookup"><span data-stu-id="f0938-119">In the **New Connection** window, on the **SSL** tab, check the **Use SSL protocol to connect** check box and the **Accept server self-signed SSL certificates** radio button.</span></span>

    ![Zrzut ekranu: karta SSL Menedżera połączeń MongoChef](./media/mongodb-mongochef/ConnectionManagerSSLTab.png)
6. <span data-ttu-id="f0938-121">Kliknij przycisk **Testuj połączenie** przycisk, aby sprawdzić informacje o połączeniu, kliknij przycisk **OK** powrócić do okna nowe połączenie, a następnie kliknij przycisk **zapisać**.</span><span class="sxs-lookup"><span data-stu-id="f0938-121">Click the **Test Connection** button to validate the connection information, click **OK** to return to the New Connection window, and then click **Save**.</span></span>

    ![Zrzut ekranu przedstawiający okno MongoChef testu połączenia](./media/mongodb-mongochef/TestConnectionResults.png)

## <a name="use-mongochef-to-create-a-database-collection-and-documents"></a><span data-ttu-id="f0938-123">Użyj MongoChef, aby utworzyć bazę danych, kolekcji i dokumentów</span><span class="sxs-lookup"><span data-stu-id="f0938-123">Use MongoChef to create a database, collection, and documents</span></span>
<span data-ttu-id="f0938-124">Aby utworzyć bazę danych, kolekcji i dokumentów za pomocą MongoChef, wykonaj następujące kroki.</span><span class="sxs-lookup"><span data-stu-id="f0938-124">To create a database, collection, and documents using MongoChef, perform the following steps.</span></span>

1. <span data-ttu-id="f0938-125">W **Menedżera połączeń**, zaznacz połączenie i kliknij **Connect**.</span><span class="sxs-lookup"><span data-stu-id="f0938-125">In **Connection Manager**, highlight the connection and click **Connect**.</span></span>

    ![Zrzut ekranu przedstawiający MongoChef Menedżera połączeń](./media/mongodb-mongochef/ConnectToAccount.png)
2. <span data-ttu-id="f0938-127">Kliknij prawym przyciskiem myszy hosta, a następnie wybierz pozycję **dodawania bazy danych**.</span><span class="sxs-lookup"><span data-stu-id="f0938-127">Right click the host and choose **Add Database**.</span></span>  <span data-ttu-id="f0938-128">Podaj nazwę bazy danych, a następnie kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="f0938-128">Provide a database name and click **OK**.</span></span>

    ![Zrzut ekranu opcji MongoChef dodawania bazy danych](./media/mongodb-mongochef/AddDatabase1.png)
3. <span data-ttu-id="f0938-130">Kliknij prawym przyciskiem myszy kliknij bazę danych i wybierz polecenie **Dodaj kolekcji**.</span><span class="sxs-lookup"><span data-stu-id="f0938-130">Right click the database and choose **Add Collection**.</span></span>  <span data-ttu-id="f0938-131">Podaj nazwę kolekcji, a następnie kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="f0938-131">Provide a collection name and click **Create**.</span></span>

    ![Zrzut ekranu opcji MongoChef Dodaj kolekcji](./media/mongodb-mongochef/AddCollection.png)
4. <span data-ttu-id="f0938-133">Kliknij przycisk **kolekcji** menu elementu, następnie kliknij przycisk **Dodawanie dokumentu**.</span><span class="sxs-lookup"><span data-stu-id="f0938-133">Click the **Collection** menu item, then click **Add Document**.</span></span>

    ![Zrzut ekranu przedstawiający element menu MongoChef Dodawanie dokumentu](./media/mongodb-mongochef/AddDocument1.png)
5. <span data-ttu-id="f0938-135">W oknie dialogowym Dodawanie dokumentu, wklej następujący, a następnie kliknij przycisk **Dodawanie dokumentu**.</span><span class="sxs-lookup"><span data-stu-id="f0938-135">In the Add Document dialog, paste the following and then click **Add Document**.</span></span>

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
6. <span data-ttu-id="f0938-136">Dodaj teraz o następującej zawartości innego dokumentu.</span><span class="sxs-lookup"><span data-stu-id="f0938-136">Add another document, this time with the following content.</span></span>

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
7. <span data-ttu-id="f0938-137">Wykonaj przykładowe zapytanie.</span><span class="sxs-lookup"><span data-stu-id="f0938-137">Execute a sample query.</span></span> <span data-ttu-id="f0938-138">Na przykład wyszukaj o nazwisko "Andersen" i zwróć pola stanu i elementów nadrzędnych.</span><span class="sxs-lookup"><span data-stu-id="f0938-138">For example, search for families with the last name 'Andersen' and return the parents and state fields.</span></span>

    ![Zrzut ekranu przedstawiający Mongo Chef wyników zapytania](./media/mongodb-mongochef/QueryDocument1.png)

## <a name="next-steps"></a><span data-ttu-id="f0938-140">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="f0938-140">Next steps</span></span>
* <span data-ttu-id="f0938-141">Zapoznaj się z rozwiązania Cosmos Azure DB: Interfejs API, bazy danych mongodb [przykłady](mongodb-samples.md).</span><span class="sxs-lookup"><span data-stu-id="f0938-141">Explore Azure Cosmos DB: API for MongoDB [samples](mongodb-samples.md).</span></span>
