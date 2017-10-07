---
title: "aaaLearn jak toosecure dostępu toodata w usłudze Azure DB rozwiązania Cosmos | Dokumentacja firmy Microsoft"
description: "Więcej informacji na temat pojęć dotyczących kontroli dostępu w usłudze Azure DB rozwiązania Cosmos, włączając klucz główny, tylko do odczytu klucze, użytkowników i uprawnienia."
services: cosmos-db
author: mimig1
manager: jhubbard
editor: monicar
documentationcenter: 
ms.assetid: 8641225d-e839-4ba6-a6fd-d6314ae3a51c
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/24/2017
ms.author: mimig
ms.openlocfilehash: fef7f8e14b488f6ceab0f2aa279a1e99d4416f08
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="securing-access-tooazure-cosmos-db-data"></a>Zabezpieczanie danych DB rozwiązania Cosmos tooAzure dostępu
Ten artykuł zawiera omówienie zabezpieczania dostępu toodata przechowywane w [bazy danych programu Microsoft Azure rozwiązania Cosmos](https://azure.microsoft.com/services/cosmos-db/).

Azure DB rozwiązania Cosmos wykorzystuje dwa typy kluczy tooauthenticate użytkowników i podaj dostępu tooits danych i zasobów. 

|Typ klucza|Zasoby|
|---|---|
|[Klucze główne](#master-keys) |Używany do zasobów administracyjnych: baza danych kont, baz danych użytkowników i uprawnienia|
|[Tokeny zasobów](#resource-tokens)|Używany do zasobów aplikacji: kolekcje, dokumenty, załączniki, procedur składowanych, wyzwalaczy i funkcji UDF|

<a id="master-keys"></a>

## <a name="master-keys"></a>Klucze główne 

Klucze główne zapewnienia toohello dostępu do wszystkich zasobów administracyjne hello hello konta bazy danych. Klucze główne:  
- Podaj tooaccounts dostępu, baz danych użytkowników i uprawnienia. 
- Nie może być używane tooprovide toocollections szczegółowego dostępu i dokumentów.
- Są tworzone podczas tworzenia hello konta.
- Mogą być generowane w dowolnym momencie.

Każde konto składa się z dwóch kluczy głównych: klucz podstawowy i klucz pomocniczy. Celem Hello dwa klucze jest tak, aby wygenerować lub Przywróć klucze, podając konto tooyour ciągłego dostępu do danych. 

Dodanie toohello dwa klucze główne hello DB rozwiązania Cosmos konta istnieją dwa klucze tylko do odczytu. Te klucze tylko do odczytu umożliwiają tylko operacji odczytu na powitania konta. Tylko do odczytu kluczy nie zapewnia dostępu tooread uprawnienia zasobów.

Podstawowe i pomocnicze, tylko do odczytu, a klucze główne odczytu i zapisu mogą być pobierane i ponownie wygenerowane za pomocą hello portalu Azure. Aby uzyskać instrukcje, zobacz [wyświetlanie, kopiowanie i ponowne generowanie kluczy dostępu](manage-account.md#keys).

![Kontrola dostępu (IAM) w hello portal Azure — prezentacja zabezpieczeń bazy danych NoSQL](./media/secure-access-to-data/nosql-database-security-master-key-portal.png)

proces Hello obracanie klucz główny jest proste. Przejdź klucz pomocniczy toohello tooretrieve portalu Azure, Zamień klucz podstawowy klucz pomocniczy w aplikacji, a następnie Obróć hello klucza podstawowego w hello portalu Azure.

![Obracanie klucza głównego w hello portal Azure — prezentacja zabezpieczeń bazy danych NoSQL](./media/secure-access-to-data/nosql-database-security-master-key-rotate-workflow.png)

### <a name="code-sample-toouse-a-master-key"></a>Kod przykładowy toouse klucza głównego

Hello Poniższy przykładowy kod przedstawia sposób toouse DB rozwiązania Cosmos konta punktu końcowego i klucz główny tooinstantiate DocumentClient i utworzyć bazę danych. 

```csharp
//Read hello Azure Cosmos DB endpointUrl and authorization keys from config.
//These values are available from hello Azure portal on hello Azure Cosmos DB account blade under "Keys".
//NB > Keep these values in a safe and secure location. Together they provide Administrative access tooyour DocDB account.

private static readonly string endpointUrl = ConfigurationManager.AppSettings["EndPointUrl"];
private static readonly SecureString authorizationKey = ToSecureString(ConfigurationManager.AppSettings["AuthorizationKey"]);

client = new DocumentClient(new Uri(endpointUrl), authorizationKey);

// Create Database
Database database = await client.CreateDatabaseAsync(
    new Database
    {
        Id = databaseName
    });
```

<a id="resource-tokens"></a>

## <a name="resource-tokens"></a>Tokeny zasobów

Tokeny zasobów zapewniać dostęp do zasobów aplikacji toohello w bazie danych. Tokeny zasobów:
- Podaj kolekcje toospecific dostępu, kluczy partycji, dokumenty, załączniki, procedur składowanych, wyzwalaczy i funkcji UDF.
- Są tworzone, gdy [użytkownika](#users) otrzymuje [uprawnienia](#permissions) tooa określonego zasobu.
- Są ponownie tworzone, gdy zasób uprawnienie jest reagować na przez wywołanie POST GET i PUT.
- Użyj tokenu zasób skrótu utworzone specjalnie dla użytkownika hello, zasobów i uprawnienia.
- Jest powiązany z okresem ważności można dostosowywać. prawidłowy obiekt timespan Hello domyślny to jedna godzina. Okres istnienia tokenu, jednak może być jawnie określona, zapasowej tooa maksymalnie pięć godzin.
- Podaj bezpieczne toogiving alternatywnych limit hello klucza głównego. 
- Włącz tooread klientów, zapisu i usuwania zasobów na koncie DB rozwiązania Cosmos hello zgodnie z toohello uprawnienia, które zostały przyznane.

Można użyć tokenu zasobów (Tworzenie rozwiązania Cosmos bazy danych użytkowników i uprawnienia) zużycia tooprovide tooresources dostępu do bazy danych z rozwiązania Cosmos konta klienta tooa nie może być zaufany za pomocą klucza głównego hello.  

Tokeny zasobów rozwiązania cosmos DB zapewniają bezpieczne alternatywę tooread klientów, zapisu i usuwania zasobów na koncie DB rozwiązania Cosmos zgodnie z toohello uprawnienia, które zostały przyznane, bez potrzeby albo wzorzec lub klucz tylko do odczytu.

Oto wzorca projektowego typowe zgodnie z którymi tokenów zasobów mogą być wymagane, generowane i dostarczyć tooclients:

1. Usługi w warstwie pośredniej skonfigurowano tooserve zdjęcia użytkownika tooshare aplikacji mobilnej. 
2. Usługa warstwie pośredniej Hello posiada klucz główny hello hello konto bazy danych rozwiązania Cosmos.
3. Aplikacja zdjęcia Hello jest zainstalowany na urządzeniach przenośnych użytkownika końcowego. 
4. Podczas logowania aplikacja zdjęcia hello ustanawia hello tożsamości użytkownika hello z usługą warstwie pośredniej hello. Ten mechanizm określania tożsamości działa wyłącznie toohello aplikacji.
5. Po nawiązaniu hello tożsamości usługi warstwie pośredniej hello żądania uprawnień na podstawie tożsamości hello.
6. Usługa warstwie pośredniej Hello wysyła aplikacji phone toohello tyłu tokenu zasobów.
7. aplikacji phone Hello można kontynuować toouse hello zasobów toodirectly tokenu dostępu DB rozwiązania Cosmos zasobów uprawnienia hello określonego przez token zasobu hello oraz interwału hello dozwoloną hello token zasobu. 
8. Po wygaśnięciu tokenu zasobów hello kolejne żądania odbierania 401 nieautoryzowane wyjątek.  W tym momencie aplikacji phone hello ponownie nawiązuje hello tożsamości i żąda nowy token zasobu.

    ![Tokeny zasobów Azure DB rozwiązania Cosmos przepływu pracy](./media/secure-access-to-data/resourcekeyworkflow.png)

Token generowania zasobów i zarządzanie odbywa się przy hello natywnych bibliotek klienckich DB rozwiązania Cosmos; Jednak jeśli używasz REST należy tworzyć hello nagłówki żądania/uwierzytelniania. Aby uzyskać więcej informacji na temat tworzenia nagłówki uwierzytelniania dla pozostałych, zobacz [kontroli dostępu do zasobów DB rozwiązania Cosmos](https://docs.microsoft.com/rest/api/documentdb/access-control-on-documentdb-resources) lub hello [kod źródłowy dla nasze zestawy SDK](https://github.com/Azure/azure-documentdb-node/blob/master/source/lib/auth.js).

Przykładem usługi warstwy środkowej używany toogenerate lub broker tokenów zasobów, zobacz hello [aplikacji ResourceTokenBroker](https://github.com/Azure/azure-documentdb-dotnet/tree/master/samples/xamarin/UserItems/ResourceTokenBroker/ResourceTokenBroker/Controllers).

<a id="users"></a>

## <a name="users"></a>Użytkownicy
Rozwiązania cosmos bazy danych użytkowników są skojarzone z bazy danych DB rozwiązania Cosmos.  Każda baza danych może zawierać zero lub więcej użytkowników DB rozwiązania Cosmos.  Witaj, jak po przedstawia przykładowy kod toocreate zasób użytkownika DB rozwiązania Cosmos.

```csharp
//Create a user.
User docUser = new User
{
    Id = "mobileuser"
};

docUser = await client.CreateUserAsync(UriFactory.CreateDatabaseUri("db"), docUser);
```

> [!NOTE]
> Każdy użytkownik DB rozwiązania Cosmos ma właściwość PermissionsLink, które mogą być używane tooretrieve hello lista [uprawnienia](#permissions) skojarzonych z użytkownikiem hello.
> 
> 

<a id="permissions"></a>

## <a name="permissions"></a>Uprawnienia
Zasób uprawnienia DB rozwiązania Cosmos jest powiązany z użytkownikiem DB rozwiązania Cosmos.  Każdy użytkownik może zawierać zero lub więcej uprawnień DB rozwiązania Cosmos.  Zasób uprawnienie zapewnia token zabezpieczający tooa dostępu hello potrzeb użytkowników podczas prób tooaccess zasobów określonej aplikacji.
Istnieją dwa poziomy dostępu, które mogą być udostępniane przez zasób uprawnienia:

* Wszystko: hello użytkownik ma pełne uprawnienia na powitania zasobów.
* Przeczytaj: hello użytkownik może odczytać tylko zawartość hello hello zasobów, ale nie można wykonać zapisu, aktualizacji lub usuwania operacji dla zasobu hello.

> [!NOTE]
> W kolejności toorun DB rozwiązania Cosmos procedur składowanych hello użytkownik musi mieć hello wszystkie uprawnienia w kolekcji hello, w których hello będzie uruchamiany procedury składowanej.
> 
> 

### <a name="code-sample-toocreate-permission"></a>Uprawnienie toocreate przykładowy kod

Hello Poniższy przykładowy kod przedstawia sposób toocreate zasób uprawnienia do odczytu hello token zasobu hello uprawnienia zasobu i skojarzyć hello uprawnienia z hello [użytkownika](#users) utworzone powyżej.

```csharp
// Create a permission.
Permission docPermission = new Permission
{
    PermissionMode = PermissionMode.Read,
    ResourceLink = documentCollection.SelfLink,
    Id = "readperm"
};
  
docPermission = await client.CreatePermissionAsync(UriFactory.CreateUserUri("db", "user"), docPermission);
Console.WriteLine(docPermission.Id + " has token of: " + docPermission.Token);
```

Jeśli określono klucza partycji dla kolekcji, następnie hello uprawnienia dla kolekcji, dokumentów i załączników zasobów musi także obejmować hello ResourcePartitionKey w toohello dodanie ResourceLink.

### <a name="code-sample-tooread-permissions-for-user"></a>Przykładowy kod tooread uprawnienia użytkownika

tooeasily uzyskać wszystkie zasoby uprawnienia skojarzone z określonym użytkownikiem, DB rozwiązania Cosmos udostępnia uprawnienie dla każdego obiektu użytkownika.  Witaj poniższy fragment kodu przedstawia sposób tworzenia tooretrieve hello uprawnienia powiązane z użytkownikiem hello powyżej, utworzenia listy uprawnień i wystąpienia nowego wystąpienia klasy DocumentClient w imieniu użytkownika hello.

```csharp
//Read a permission feed.
FeedResponse<Permission> permFeed = await client.ReadPermissionFeedAsync(
  UriFactory.CreateUserUri("db", "myUser"));
 List<Permission> permList = new List<Permission>();

foreach (Permission perm in permFeed)
{
    permList.Add(perm);
}

DocumentClient userClient = new DocumentClient(new Uri(endpointUrl), permList);
```

## <a name="next-steps"></a>Następne kroki
* toolearn więcej informacji na temat zabezpieczeń bazy danych DB rozwiązania Cosmos, zobacz [rozwiązania Cosmos bazy danych: baza danych zabezpieczeń](database-security.md).
* toolearn o zarządzaniu kluczami głównego i tylko do odczytu, zobacz [jak toomanage konta bazy danych Azure rozwiązania Cosmos](manage-account.md#keys).
* tokeny autoryzacji bazy danych Azure rozwiązania Cosmos tooconstruct, zobacz temat toolearn [kontroli dostępu do zasobów DB rozwiązania Cosmos Azure](https://docs.microsoft.com/rest/api/documentdb/access-control-on-documentdb-resources).
