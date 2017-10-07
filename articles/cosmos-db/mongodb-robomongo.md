---
title: "aaaUse Robomongo dla bazy danych Azure rozwiązania Cosmos | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toouse Robomongo z bazy danych Azure rozwiązania Cosmos: interfejsu API dla konta bazy danych MongoDB"
keywords: robomongo
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
ms.openlocfilehash: 3018243e904015426dc69a69b26fb53421e1fe4f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="use-robomongo-with-an-azure-cosmos-db-api-for-mongodb-account"></a><span data-ttu-id="bcd0b-104">Użyj Robomongo z bazy danych Azure rozwiązania Cosmos: interfejsu API dla konta bazy danych MongoDB</span><span class="sxs-lookup"><span data-stu-id="bcd0b-104">Use Robomongo with an Azure Cosmos DB: API for MongoDB account</span></span>
<span data-ttu-id="bcd0b-105">tooan tooconnect bazy danych Azure rozwiązania Cosmos: interfejs API dla konta bazy danych MongoDB przy użyciu Robomongo, musi:</span><span class="sxs-lookup"><span data-stu-id="bcd0b-105">tooconnect tooan Azure Cosmos DB: API for MongoDB account using Robomongo, you must:</span></span>

* <span data-ttu-id="bcd0b-106">Pobierz i zainstaluj [Robomongo](https://robomongo.org/)</span><span class="sxs-lookup"><span data-stu-id="bcd0b-106">Download and install [Robomongo](https://robomongo.org/)</span></span>
* <span data-ttu-id="bcd0b-107">Z bazy danych rozwiązania Cosmos Azure ma: interfejsu API dla konta bazy danych MongoDB [ciąg połączenia](connect-mongodb-account.md) informacji</span><span class="sxs-lookup"><span data-stu-id="bcd0b-107">Have your Azure Cosmos DB: API for MongoDB account [connection string](connect-mongodb-account.md) information</span></span>

## <a name="connect-using-robomongo"></a><span data-ttu-id="bcd0b-108">Połącz przy użyciu Robomongo</span><span class="sxs-lookup"><span data-stu-id="bcd0b-108">Connect using Robomongo</span></span>
<span data-ttu-id="bcd0b-109">tooadd Twojego Azure DB rozwiązania Cosmos: interfejs API dla bazy danych MongoDB toohello konto połączenia bazy danych MongoDB Robomongo, wykonaj hello następujące kroki.</span><span class="sxs-lookup"><span data-stu-id="bcd0b-109">tooadd your Azure Cosmos DB: API for MongoDB account toohello Robomongo MongoDB Connections, perform hello following steps.</span></span>

1. <span data-ttu-id="bcd0b-110">Pobieranie programu Azure DB rozwiązania Cosmos: interfejsu API, bazy danych MongoDB informacji o koncie połączenia przy użyciu instrukcji hello [tutaj](connect-mongodb-account.md).</span><span class="sxs-lookup"><span data-stu-id="bcd0b-110">Retrieve your Azure Cosmos DB: API for MongoDB account connection information using hello instructions [here](connect-mongodb-account.md).</span></span>

    ![Zrzut ekranu przedstawiający blok ciągu połączenia hello](./media/mongodb-robomongo/connectionstringblade.png)
2. <span data-ttu-id="bcd0b-112">Uruchom *Robomongo.exe*</span><span class="sxs-lookup"><span data-stu-id="bcd0b-112">Run *Robomongo.exe*</span></span>

3. <span data-ttu-id="bcd0b-113">Kliknij przycisk połączenie hello w obszarze **pliku** toomanage połączenia.</span><span class="sxs-lookup"><span data-stu-id="bcd0b-113">Click hello connection button under **File** toomanage your connections.</span></span> <span data-ttu-id="bcd0b-114">Następnie kliknij przycisk **Utwórz** w hello **połączenia bazy danych MongoDB** okna, które zostanie wyświetlone powitalne **ustawienia połączenia** okna.</span><span class="sxs-lookup"><span data-stu-id="bcd0b-114">Then, click **Create** in hello **MongoDB Connections** window, which will open up hello **Connection Settings** window.</span></span>

4. <span data-ttu-id="bcd0b-115">W hello **ustawienia połączenia** okna, wybierz nazwę.</span><span class="sxs-lookup"><span data-stu-id="bcd0b-115">In hello **Connection Settings** window, choose a name.</span></span> <span data-ttu-id="bcd0b-116">Następnie znajdź hello **hosta** i **portu** z informacje o połączeniu w kroku 1, a następnie wprowadź je do **adres** i **portu**odpowiednio .</span><span class="sxs-lookup"><span data-stu-id="bcd0b-116">Then, find hello **Host** and **Port** from your connection information in Step 1 and enter them into **Address** and **Port**, respectively.</span></span>

    ![Zrzut ekranu przedstawiający hello Robomongo Zarządzanie połączeniami](./media/mongodb-robomongo/manageconnections.png)
5. <span data-ttu-id="bcd0b-118">Na powitania **uwierzytelniania** , kliknij pozycję **uwierzytelniania wykonaj**.</span><span class="sxs-lookup"><span data-stu-id="bcd0b-118">On hello **Authentication** tab, click **Perform authentication**.</span></span> <span data-ttu-id="bcd0b-119">Następnie wprowadź bazy danych (domyślna to *Admin*), **nazwy użytkownika** i **hasło**.</span><span class="sxs-lookup"><span data-stu-id="bcd0b-119">Then, enter your Database (default is *Admin*), **User Name** and **Password**.</span></span>
<span data-ttu-id="bcd0b-120">Zarówno **nazwy użytkownika** i **hasło** znajdują się informacje o połączeniu w kroku 1.</span><span class="sxs-lookup"><span data-stu-id="bcd0b-120">Both **User Name** and **Password** can be found in your connection information in Step 1.</span></span>

    ![Zrzut ekranu: karta Uwierzytelnianie Robomongo hello](./media/mongodb-robomongo/authentication.png)
6. <span data-ttu-id="bcd0b-122">Na powitania **SSL** karcie wyboru **protokołu SSL używany**, następnie zmienić hello **metodę uwierzytelniania** za**certyfikatu z podpisem własnym**.</span><span class="sxs-lookup"><span data-stu-id="bcd0b-122">On hello **SSL** tab, check **Use SSL protocol**, then change hello **Authentication Method** too**Self-signed Certificate**.</span></span>

    ![Zrzut ekranu przedstawiający hello Robomongo kartę protokołu SSL](./media/mongodb-robomongo/SSL.png)
7. <span data-ttu-id="bcd0b-124">Na koniec kliknij **testu** tooverify następnie są możliwe tooconnect **zapisać**.</span><span class="sxs-lookup"><span data-stu-id="bcd0b-124">Finally, click **Test** tooverify that you are able tooconnect, then **Save**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="bcd0b-125">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="bcd0b-125">Next steps</span></span>
* <span data-ttu-id="bcd0b-126">Zapoznaj się z rozwiązania Cosmos Azure DB: Interfejs API, bazy danych mongodb [przykłady](mongodb-samples.md).</span><span class="sxs-lookup"><span data-stu-id="bcd0b-126">Explore Azure Cosmos DB: API for MongoDB [samples](mongodb-samples.md).</span></span>
