---
title: "Parametry połączenia aaaMongoDB konta bazy danych Azure rozwiązania Cosmos | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak tooconnect tooan aplikacji z bazy danych MongoDB bazy danych Azure rozwiązania Cosmos konta przy użyciu ciągu połączenia bazy danych MongoDB."
keywords: "Parametry połączenia bazy danych mongodb"
services: cosmos-db
author: AndrewHoh
manager: jhubbard
editor: 
documentationcenter: 
ms.assetid: e36f7375-9329-403b-afd1-4ab49894f75e
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/12/2017
ms.author: anhoh
ms.openlocfilehash: c0b81cb49a10e09e3f02411b91731c7f980ec47d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="connect-a-mongodb-application-tooazure-cosmos-db"></a>Połączenia bazy danych MongoDB aplikacji tooAzure DB rozwiązania Cosmos
Dowiedz się, jak tooconnect tooan aplikacji z bazy danych MongoDB bazy danych Azure rozwiązania Cosmos konta przy użyciu ciągu połączenia bazy danych MongoDB. Następnie można użyć bazy danych Azure rozwiązania Cosmos bazy danych jako dane hello magazynu dla aplikacji bazy danych MongoDB. 

Ten samouczek zawiera dwa sposoby tooretrieve ciągu połączenia:

- [Witaj szybki start — metoda](#QuickstartConnection), do użycia z programem .NET, Node.js, powłoka bazy danych MongoDB, Java i Python sterowniki
- [Witaj metody ciąg połączenia niestandardowych](#GetCustomConnection), do użycia z innych sterowników

## <a name="prerequisites"></a>Wymagania wstępne

- Konto platformy Azure. Jeśli nie masz konta platformy Azure, Utwórz [bezpłatne konto platformy Azure](https://azure.microsoft.com/free/) teraz. 
- Konto usługi Azure Cosmos DB. Aby uzyskać instrukcje, zobacz [tworzenie aplikacji sieci web interfejsu API bazy danych MongoDB z platformą .NET i portalu Azure hello](create-mongodb-dotnet.md).

## <a id="QuickstartConnection"></a>Pobierz ciąg połączenia bazy danych MongoDB hello przy użyciu hello szybki start
1. W przeglądarce internetowej, zaloguj się toohello [portalu Azure](https://portal.azure.com).
2. W hello **bazy danych Azure rozwiązania Cosmos** bloku, wybierz hello API dla konta bazy danych MongoDB. 
3. W lewym okienku hello hello konta bloku, kliknij przycisk **szybki start**. 
4. Wybierz platformy (**.NET**, **Node.js**, **powłoki MongoDB**, **Java**, **Python**). Jeśli nie widzisz, Twoje sterownika lub narzędzia na liście, nie martw się — firma Microsoft stale dokumentu więcej wstawki kodu połączenia. Wprowadź uwagi poniżej na jakie chcesz toosee. toolearn jak toocraft własne połączenia odczytu [uzyskać informacje o parametrach połączenia konta hello](#GetCustomConnection).
5. Skopiuj i Wklej hello fragment kodu w aplikacji bazy danych MongoDB.

    ![Bloku szybki start](./media/connect-mongodb-account/QuickStartBlade.png)

## <a id="GetCustomConnection"></a>Pobierz toocustomize ciąg połączenia bazy danych MongoDB hello
1. W przeglądarce internetowej, zaloguj się toohello [portalu Azure](https://portal.azure.com).
2. W hello **bazy danych Azure rozwiązania Cosmos** bloku, wybierz hello API dla konta bazy danych MongoDB. 
3. W lewym okienku hello hello konta bloku, kliknij przycisk **ciąg połączenia**. 
4. Witaj **ciąg połączenia** zostanie otwarty blok. Ma ona wszystkie hello informacje niezbędne tooconnect toohello konta za pośrednictwem sterownika bazy danych mongodb, w tym ciągu połączenia preconstructed.

    ![Blok ciągu połączenia](./media/connect-mongodb-account/ConnectionStringBlade.png)

## <a name="connection-string-requirements"></a>Wymagania dotyczące ciąg połączenia
> [!Important]
> Azure DB rozwiązania Cosmos ma wymogi ograniczeniami zabezpieczeń. Azure konta DB rozwiązania Cosmos wymagają uwierzytelniania i zapewnienia bezpiecznej komunikacji za pośrednictwem *SSL*. 
>
>

Azure DB rozwiązania Cosmos obsługuje hello standardowe bazy danych MongoDB format ciągu połączenia identyfikator URI, za pomocą paru specyficznych wymagań: konta bazy danych Azure rozwiązania Cosmos wymagają uwierzytelniania i zapewnienia bezpiecznej komunikacji za pośrednictwem protokołu SSL. Tak format ciągu połączenia hello jest:

    mongodb://username:password@host:port/[database]?ssl=true

Ten ciąg Hello wartości są dostępne w hello **ciąg połączenia** bloku przedstawiona wcześniej:

* Nazwa użytkownika (wymagane): Nazwa konta bazy danych Azure rozwiązania Cosmos.
* Hasło (wymagane): hasło konta bazy danych Azure rozwiązania Cosmos.
* Host (wymagane): nazwa FQDN hello konta bazy danych Azure rozwiązania Cosmos.
* Port (wymagane): 10255.
* Bazy danych (opcjonalnie): używa bazy danych hello hello połączenia. Jeśli baza danych jest dostępne, hello domyślna baza danych jest "test".
* Protokół SSL = true (wymagane)

Rozważmy na przykład konto hello pokazano hello **ciąg połączenia** bloku. Jest prawidłowe parametry połączenia:

    mongodb://contoso123:0Fc3IolnL12312asdfawejunASDF@asdfYXX2t8a97kghVcUzcDv98hawelufhawefafnoQRGwNj2nMPL1Y9qsIr9Srdw==@anhohmongo.documents.azure.com:10255/mydatabase?ssl=true

## <a name="next-steps"></a>Następne kroki
* Dowiedz się, jak za[Użyj MongoChef](mongodb-mongochef.md) z interfejsu API Azure rozwiązania Cosmos bazy danych dla konta bazy danych MongoDB.
* Eksploruj hello interfejsu API Azure rozwiązania Cosmos DB bazy danych mongodb, wyświetlając [przykłady](mongodb-samples.md).
