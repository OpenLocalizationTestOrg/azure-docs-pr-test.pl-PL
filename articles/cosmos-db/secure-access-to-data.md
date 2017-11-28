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
# <a name="securing-access-tooazure-cosmos-db-data"></a><span data-ttu-id="bfe1b-103">Zabezpieczanie danych DB rozwiązania Cosmos tooAzure dostępu</span><span class="sxs-lookup"><span data-stu-id="bfe1b-103">Securing access tooAzure Cosmos DB data</span></span>
<span data-ttu-id="bfe1b-104">Ten artykuł zawiera omówienie zabezpieczania dostępu toodata przechowywane w [bazy danych programu Microsoft Azure rozwiązania Cosmos](https://azure.microsoft.com/services/cosmos-db/).</span><span class="sxs-lookup"><span data-stu-id="bfe1b-104">This article provides an overview of securing access toodata stored in [Microsoft Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/).</span></span>

<span data-ttu-id="bfe1b-105">Azure DB rozwiązania Cosmos wykorzystuje dwa typy kluczy tooauthenticate użytkowników i podaj dostępu tooits danych i zasobów.</span><span class="sxs-lookup"><span data-stu-id="bfe1b-105">Azure Cosmos DB uses two types of keys tooauthenticate users and provide access tooits data and resources.</span></span> 

|<span data-ttu-id="bfe1b-106">Typ klucza</span><span class="sxs-lookup"><span data-stu-id="bfe1b-106">Key type</span></span>|<span data-ttu-id="bfe1b-107">Zasoby</span><span class="sxs-lookup"><span data-stu-id="bfe1b-107">Resources</span></span>|
|---|---|
|[<span data-ttu-id="bfe1b-108">Klucze główne</span><span class="sxs-lookup"><span data-stu-id="bfe1b-108">Master keys</span></span>](#master-keys) |<span data-ttu-id="bfe1b-109">Używany do zasobów administracyjnych: baza danych kont, baz danych użytkowników i uprawnienia</span><span class="sxs-lookup"><span data-stu-id="bfe1b-109">Used for administrative resources: database accounts, databases, users, and permissions</span></span>|
|[<span data-ttu-id="bfe1b-110">Tokeny zasobów</span><span class="sxs-lookup"><span data-stu-id="bfe1b-110">Resource tokens</span></span>](#resource-tokens)|<span data-ttu-id="bfe1b-111">Używany do zasobów aplikacji: kolekcje, dokumenty, załączniki, procedur składowanych, wyzwalaczy i funkcji UDF</span><span class="sxs-lookup"><span data-stu-id="bfe1b-111">Used for application resources: collections, documents, attachments, stored procedures, triggers, and UDFs</span></span>|

<a id="master-keys"></a>

## <a name="master-keys"></a><span data-ttu-id="bfe1b-112">Klucze główne</span><span class="sxs-lookup"><span data-stu-id="bfe1b-112">Master keys</span></span> 

<span data-ttu-id="bfe1b-113">Klucze główne zapewnienia toohello dostępu do wszystkich zasobów administracyjne hello hello konta bazy danych.</span><span class="sxs-lookup"><span data-stu-id="bfe1b-113">Master keys provide access toohello all hello administrative resources for hello database account.</span></span> <span data-ttu-id="bfe1b-114">Klucze główne:</span><span class="sxs-lookup"><span data-stu-id="bfe1b-114">Master keys:</span></span>  
- <span data-ttu-id="bfe1b-115">Podaj tooaccounts dostępu, baz danych użytkowników i uprawnienia.</span><span class="sxs-lookup"><span data-stu-id="bfe1b-115">Provide access tooaccounts, databases, users, and permissions.</span></span> 
- <span data-ttu-id="bfe1b-116">Nie może być używane tooprovide toocollections szczegółowego dostępu i dokumentów.</span><span class="sxs-lookup"><span data-stu-id="bfe1b-116">Cannot be used tooprovide granular access toocollections and documents.</span></span>
- <span data-ttu-id="bfe1b-117">Są tworzone podczas tworzenia hello konta.</span><span class="sxs-lookup"><span data-stu-id="bfe1b-117">Are created during hello creation of an account.</span></span>
- <span data-ttu-id="bfe1b-118">Mogą być generowane w dowolnym momencie.</span><span class="sxs-lookup"><span data-stu-id="bfe1b-118">Can be regenerated at any time.</span></span>

<span data-ttu-id="bfe1b-119">Każde konto składa się z dwóch kluczy głównych: klucz podstawowy i klucz pomocniczy.</span><span class="sxs-lookup"><span data-stu-id="bfe1b-119">Each account consists of two Master keys: a primary key and secondary key.</span></span> <span data-ttu-id="bfe1b-120">Celem Hello dwa klucze jest tak, aby wygenerować lub Przywróć klucze, podając konto tooyour ciągłego dostępu do danych.</span><span class="sxs-lookup"><span data-stu-id="bfe1b-120">hello purpose of dual keys is so that you can regenerate, or roll keys, providing continuous access tooyour account and data.</span></span> 

<span data-ttu-id="bfe1b-121">Dodanie toohello dwa klucze główne hello DB rozwiązania Cosmos konta istnieją dwa klucze tylko do odczytu.</span><span class="sxs-lookup"><span data-stu-id="bfe1b-121">In addition toohello two master keys for hello Cosmos DB account, there are two read-only keys.</span></span> <span data-ttu-id="bfe1b-122">Te klucze tylko do odczytu umożliwiają tylko operacji odczytu na powitania konta.</span><span class="sxs-lookup"><span data-stu-id="bfe1b-122">These read-only keys only allow read operations on hello account.</span></span> <span data-ttu-id="bfe1b-123">Tylko do odczytu kluczy nie zapewnia dostępu tooread uprawnienia zasobów.</span><span class="sxs-lookup"><span data-stu-id="bfe1b-123">Read-only keys do not provide access tooread permissions resources.</span></span>

<span data-ttu-id="bfe1b-124">Podstawowe i pomocnicze, tylko do odczytu, a klucze główne odczytu i zapisu mogą być pobierane i ponownie wygenerowane za pomocą hello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="bfe1b-124">Primary, secondary, read only, and read-write master keys can be retrieved and regenerated using hello Azure portal.</span></span> <span data-ttu-id="bfe1b-125">Aby uzyskać instrukcje, zobacz [wyświetlanie, kopiowanie i ponowne generowanie kluczy dostępu](manage-account.md#keys).</span><span class="sxs-lookup"><span data-stu-id="bfe1b-125">For instructions, see [View, copy, and regenerate access keys](manage-account.md#keys).</span></span>

![Kontrola dostępu (IAM) w hello portal Azure — prezentacja zabezpieczeń bazy danych NoSQL](./media/secure-access-to-data/nosql-database-security-master-key-portal.png)

<span data-ttu-id="bfe1b-127">proces Hello obracanie klucz główny jest proste.</span><span class="sxs-lookup"><span data-stu-id="bfe1b-127">hello process of rotating your master key is simple.</span></span> <span data-ttu-id="bfe1b-128">Przejdź klucz pomocniczy toohello tooretrieve portalu Azure, Zamień klucz podstawowy klucz pomocniczy w aplikacji, a następnie Obróć hello klucza podstawowego w hello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="bfe1b-128">Navigate toohello Azure portal tooretrieve your secondary key, then replace your primary key with your secondary key in your application, then rotate hello primary key in hello Azure portal.</span></span>

![Obracanie klucza głównego w hello portal Azure — prezentacja zabezpieczeń bazy danych NoSQL](./media/secure-access-to-data/nosql-database-security-master-key-rotate-workflow.png)

### <a name="code-sample-toouse-a-master-key"></a><span data-ttu-id="bfe1b-130">Kod przykładowy toouse klucza głównego</span><span class="sxs-lookup"><span data-stu-id="bfe1b-130">Code sample toouse a master key</span></span>

<span data-ttu-id="bfe1b-131">Hello Poniższy przykładowy kod przedstawia sposób toouse DB rozwiązania Cosmos konta punktu końcowego i klucz główny tooinstantiate DocumentClient i utworzyć bazę danych.</span><span class="sxs-lookup"><span data-stu-id="bfe1b-131">hello following code sample illustrates how toouse a Cosmos DB account endpoint and master key tooinstantiate a DocumentClient and create a database.</span></span> 

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

## <a name="resource-tokens"></a><span data-ttu-id="bfe1b-132">Tokeny zasobów</span><span class="sxs-lookup"><span data-stu-id="bfe1b-132">Resource tokens</span></span>

<span data-ttu-id="bfe1b-133">Tokeny zasobów zapewniać dostęp do zasobów aplikacji toohello w bazie danych.</span><span class="sxs-lookup"><span data-stu-id="bfe1b-133">Resource tokens provide access toohello application resources within a database.</span></span> <span data-ttu-id="bfe1b-134">Tokeny zasobów:</span><span class="sxs-lookup"><span data-stu-id="bfe1b-134">Resource tokens:</span></span>
- <span data-ttu-id="bfe1b-135">Podaj kolekcje toospecific dostępu, kluczy partycji, dokumenty, załączniki, procedur składowanych, wyzwalaczy i funkcji UDF.</span><span class="sxs-lookup"><span data-stu-id="bfe1b-135">Provide access toospecific collections, partition keys, documents, attachments, stored procedures, triggers, and UDFs.</span></span>
- <span data-ttu-id="bfe1b-136">Są tworzone, gdy [użytkownika](#users) otrzymuje [uprawnienia](#permissions) tooa określonego zasobu.</span><span class="sxs-lookup"><span data-stu-id="bfe1b-136">Are created when a [user](#users) is granted [permissions](#permissions) tooa specific resource.</span></span>
- <span data-ttu-id="bfe1b-137">Są ponownie tworzone, gdy zasób uprawnienie jest reagować na przez wywołanie POST GET i PUT.</span><span class="sxs-lookup"><span data-stu-id="bfe1b-137">Are recreated when a permission resource is acted upon on by POST, GET, or PUT call.</span></span>
- <span data-ttu-id="bfe1b-138">Użyj tokenu zasób skrótu utworzone specjalnie dla użytkownika hello, zasobów i uprawnienia.</span><span class="sxs-lookup"><span data-stu-id="bfe1b-138">Use a hash resource token specifically constructed for hello user, resource, and permission.</span></span>
- <span data-ttu-id="bfe1b-139">Jest powiązany z okresem ważności można dostosowywać.</span><span class="sxs-lookup"><span data-stu-id="bfe1b-139">Are time bound with a customizable validity period.</span></span> <span data-ttu-id="bfe1b-140">prawidłowy obiekt timespan Hello domyślny to jedna godzina.</span><span class="sxs-lookup"><span data-stu-id="bfe1b-140">hello default valid timespan is one hour.</span></span> <span data-ttu-id="bfe1b-141">Okres istnienia tokenu, jednak może być jawnie określona, zapasowej tooa maksymalnie pięć godzin.</span><span class="sxs-lookup"><span data-stu-id="bfe1b-141">Token lifetime, however, may be explicitly specified, up tooa maximum of five hours.</span></span>
- <span data-ttu-id="bfe1b-142">Podaj bezpieczne toogiving alternatywnych limit hello klucza głównego.</span><span class="sxs-lookup"><span data-stu-id="bfe1b-142">Provide a safe alternative toogiving out hello master key.</span></span> 
- <span data-ttu-id="bfe1b-143">Włącz tooread klientów, zapisu i usuwania zasobów na koncie DB rozwiązania Cosmos hello zgodnie z toohello uprawnienia, które zostały przyznane.</span><span class="sxs-lookup"><span data-stu-id="bfe1b-143">Enable clients tooread, write, and delete resources in hello Cosmos DB account according toohello permissions they've been granted.</span></span>

<span data-ttu-id="bfe1b-144">Można użyć tokenu zasobów (Tworzenie rozwiązania Cosmos bazy danych użytkowników i uprawnienia) zużycia tooprovide tooresources dostępu do bazy danych z rozwiązania Cosmos konta klienta tooa nie może być zaufany za pomocą klucza głównego hello.</span><span class="sxs-lookup"><span data-stu-id="bfe1b-144">You can use a resource token (by creating Cosmos DB users and permissions) when you want tooprovide access tooresources in your Cosmos DB account tooa client that cannot be trusted with hello master key.</span></span>  

<span data-ttu-id="bfe1b-145">Tokeny zasobów rozwiązania cosmos DB zapewniają bezpieczne alternatywę tooread klientów, zapisu i usuwania zasobów na koncie DB rozwiązania Cosmos zgodnie z toohello uprawnienia, które zostały przyznane, bez potrzeby albo wzorzec lub klucz tylko do odczytu.</span><span class="sxs-lookup"><span data-stu-id="bfe1b-145">Cosmos DB resource tokens provide a safe alternative that enables clients tooread, write, and delete resources in your Cosmos DB account according toohello permissions you've granted, and without need for either a master or read only key.</span></span>

<span data-ttu-id="bfe1b-146">Oto wzorca projektowego typowe zgodnie z którymi tokenów zasobów mogą być wymagane, generowane i dostarczyć tooclients:</span><span class="sxs-lookup"><span data-stu-id="bfe1b-146">Here is a typical design pattern whereby resource tokens may be requested, generated, and delivered tooclients:</span></span>

1. <span data-ttu-id="bfe1b-147">Usługi w warstwie pośredniej skonfigurowano tooserve zdjęcia użytkownika tooshare aplikacji mobilnej.</span><span class="sxs-lookup"><span data-stu-id="bfe1b-147">A mid-tier service is set up tooserve a mobile application tooshare user photos.</span></span> 
2. <span data-ttu-id="bfe1b-148">Usługa warstwie pośredniej Hello posiada klucz główny hello hello konto bazy danych rozwiązania Cosmos.</span><span class="sxs-lookup"><span data-stu-id="bfe1b-148">hello mid-tier service possesses hello master key of hello Cosmos DB account.</span></span>
3. <span data-ttu-id="bfe1b-149">Aplikacja zdjęcia Hello jest zainstalowany na urządzeniach przenośnych użytkownika końcowego.</span><span class="sxs-lookup"><span data-stu-id="bfe1b-149">hello photo app is installed on end-user mobile devices.</span></span> 
4. <span data-ttu-id="bfe1b-150">Podczas logowania aplikacja zdjęcia hello ustanawia hello tożsamości użytkownika hello z usługą warstwie pośredniej hello.</span><span class="sxs-lookup"><span data-stu-id="bfe1b-150">On login, hello photo app establishes hello identity of hello user with hello mid-tier service.</span></span> <span data-ttu-id="bfe1b-151">Ten mechanizm określania tożsamości działa wyłącznie toohello aplikacji.</span><span class="sxs-lookup"><span data-stu-id="bfe1b-151">This mechanism of identity establishment is purely up toohello application.</span></span>
5. <span data-ttu-id="bfe1b-152">Po nawiązaniu hello tożsamości usługi warstwie pośredniej hello żądania uprawnień na podstawie tożsamości hello.</span><span class="sxs-lookup"><span data-stu-id="bfe1b-152">Once hello identity is established, hello mid-tier service requests permissions based on hello identity.</span></span>
6. <span data-ttu-id="bfe1b-153">Usługa warstwie pośredniej Hello wysyła aplikacji phone toohello tyłu tokenu zasobów.</span><span class="sxs-lookup"><span data-stu-id="bfe1b-153">hello mid-tier service sends a resource token back toohello phone app.</span></span>
7. <span data-ttu-id="bfe1b-154">aplikacji phone Hello można kontynuować toouse hello zasobów toodirectly tokenu dostępu DB rozwiązania Cosmos zasobów uprawnienia hello określonego przez token zasobu hello oraz interwału hello dozwoloną hello token zasobu.</span><span class="sxs-lookup"><span data-stu-id="bfe1b-154">hello phone app can continue toouse hello resource token toodirectly access Cosmos DB resources with hello permissions defined by hello resource token and for hello interval allowed by hello resource token.</span></span> 
8. <span data-ttu-id="bfe1b-155">Po wygaśnięciu tokenu zasobów hello kolejne żądania odbierania 401 nieautoryzowane wyjątek.</span><span class="sxs-lookup"><span data-stu-id="bfe1b-155">When hello resource token expires, subsequent requests receive a 401 unauthorized exception.</span></span>  <span data-ttu-id="bfe1b-156">W tym momencie aplikacji phone hello ponownie nawiązuje hello tożsamości i żąda nowy token zasobu.</span><span class="sxs-lookup"><span data-stu-id="bfe1b-156">At this point, hello phone app re-establishes hello identity and requests a new resource token.</span></span>

    ![Tokeny zasobów Azure DB rozwiązania Cosmos przepływu pracy](./media/secure-access-to-data/resourcekeyworkflow.png)

<span data-ttu-id="bfe1b-158">Token generowania zasobów i zarządzanie odbywa się przy hello natywnych bibliotek klienckich DB rozwiązania Cosmos; Jednak jeśli używasz REST należy tworzyć hello nagłówki żądania/uwierzytelniania.</span><span class="sxs-lookup"><span data-stu-id="bfe1b-158">Resource token generation and management is handled by hello native Cosmos DB client libraries; however, if you use REST you must construct hello request/authentication headers.</span></span> <span data-ttu-id="bfe1b-159">Aby uzyskać więcej informacji na temat tworzenia nagłówki uwierzytelniania dla pozostałych, zobacz [kontroli dostępu do zasobów DB rozwiązania Cosmos](https://docs.microsoft.com/rest/api/documentdb/access-control-on-documentdb-resources) lub hello [kod źródłowy dla nasze zestawy SDK](https://github.com/Azure/azure-documentdb-node/blob/master/source/lib/auth.js).</span><span class="sxs-lookup"><span data-stu-id="bfe1b-159">For more information on creating authentication headers for REST, see [Access Control on Cosmos DB Resources](https://docs.microsoft.com/rest/api/documentdb/access-control-on-documentdb-resources) or hello [source code for our SDKs](https://github.com/Azure/azure-documentdb-node/blob/master/source/lib/auth.js).</span></span>

<span data-ttu-id="bfe1b-160">Przykładem usługi warstwy środkowej używany toogenerate lub broker tokenów zasobów, zobacz hello [aplikacji ResourceTokenBroker](https://github.com/Azure/azure-documentdb-dotnet/tree/master/samples/xamarin/UserItems/ResourceTokenBroker/ResourceTokenBroker/Controllers).</span><span class="sxs-lookup"><span data-stu-id="bfe1b-160">For an example of a middle tier service used toogenerate or broker resource tokens, see hello [ResourceTokenBroker app](https://github.com/Azure/azure-documentdb-dotnet/tree/master/samples/xamarin/UserItems/ResourceTokenBroker/ResourceTokenBroker/Controllers).</span></span>

<a id="users"></a>

## <a name="users"></a><span data-ttu-id="bfe1b-161">Użytkownicy</span><span class="sxs-lookup"><span data-stu-id="bfe1b-161">Users</span></span>
<span data-ttu-id="bfe1b-162">Rozwiązania cosmos bazy danych użytkowników są skojarzone z bazy danych DB rozwiązania Cosmos.</span><span class="sxs-lookup"><span data-stu-id="bfe1b-162">Cosmos DB users are associated with a Cosmos DB database.</span></span>  <span data-ttu-id="bfe1b-163">Każda baza danych może zawierać zero lub więcej użytkowników DB rozwiązania Cosmos.</span><span class="sxs-lookup"><span data-stu-id="bfe1b-163">Each database can contain zero or more Cosmos DB users.</span></span>  <span data-ttu-id="bfe1b-164">Witaj, jak po przedstawia przykładowy kod toocreate zasób użytkownika DB rozwiązania Cosmos.</span><span class="sxs-lookup"><span data-stu-id="bfe1b-164">hello following code sample shows how toocreate a Cosmos DB user resource.</span></span>

```csharp
//Create a user.
User docUser = new User
{
    Id = "mobileuser"
};

docUser = await client.CreateUserAsync(UriFactory.CreateDatabaseUri("db"), docUser);
```

> [!NOTE]
> <span data-ttu-id="bfe1b-165">Każdy użytkownik DB rozwiązania Cosmos ma właściwość PermissionsLink, które mogą być używane tooretrieve hello lista [uprawnienia](#permissions) skojarzonych z użytkownikiem hello.</span><span class="sxs-lookup"><span data-stu-id="bfe1b-165">Each Cosmos DB user has a PermissionsLink property that can be used tooretrieve hello list of [permissions](#permissions) associated with hello user.</span></span>
> 
> 

<a id="permissions"></a>

## <a name="permissions"></a><span data-ttu-id="bfe1b-166">Uprawnienia</span><span class="sxs-lookup"><span data-stu-id="bfe1b-166">Permissions</span></span>
<span data-ttu-id="bfe1b-167">Zasób uprawnienia DB rozwiązania Cosmos jest powiązany z użytkownikiem DB rozwiązania Cosmos.</span><span class="sxs-lookup"><span data-stu-id="bfe1b-167">A Cosmos DB permission resource is associated with a Cosmos DB user.</span></span>  <span data-ttu-id="bfe1b-168">Każdy użytkownik może zawierać zero lub więcej uprawnień DB rozwiązania Cosmos.</span><span class="sxs-lookup"><span data-stu-id="bfe1b-168">Each user may contain zero or more Cosmos DB permissions.</span></span>  <span data-ttu-id="bfe1b-169">Zasób uprawnienie zapewnia token zabezpieczający tooa dostępu hello potrzeb użytkowników podczas prób tooaccess zasobów określonej aplikacji.</span><span class="sxs-lookup"><span data-stu-id="bfe1b-169">A permission resource provides access tooa security token that hello user needs when trying tooaccess a specific application resource.</span></span>
<span data-ttu-id="bfe1b-170">Istnieją dwa poziomy dostępu, które mogą być udostępniane przez zasób uprawnienia:</span><span class="sxs-lookup"><span data-stu-id="bfe1b-170">There are two available access levels that may be provided by a permission resource:</span></span>

* <span data-ttu-id="bfe1b-171">Wszystko: hello użytkownik ma pełne uprawnienia na powitania zasobów.</span><span class="sxs-lookup"><span data-stu-id="bfe1b-171">All: hello user has full permission on hello resource.</span></span>
* <span data-ttu-id="bfe1b-172">Przeczytaj: hello użytkownik może odczytać tylko zawartość hello hello zasobów, ale nie można wykonać zapisu, aktualizacji lub usuwania operacji dla zasobu hello.</span><span class="sxs-lookup"><span data-stu-id="bfe1b-172">Read: hello user can only read hello contents of hello resource but cannot perform write, update, or delete operations on hello resource.</span></span>

> [!NOTE]
> <span data-ttu-id="bfe1b-173">W kolejności toorun DB rozwiązania Cosmos procedur składowanych hello użytkownik musi mieć hello wszystkie uprawnienia w kolekcji hello, w których hello będzie uruchamiany procedury składowanej.</span><span class="sxs-lookup"><span data-stu-id="bfe1b-173">In order toorun Cosmos DB stored procedures hello user must have hello All permission on hello collection in which hello stored procedure will be run.</span></span>
> 
> 

### <a name="code-sample-toocreate-permission"></a><span data-ttu-id="bfe1b-174">Uprawnienie toocreate przykładowy kod</span><span class="sxs-lookup"><span data-stu-id="bfe1b-174">Code sample toocreate permission</span></span>

<span data-ttu-id="bfe1b-175">Hello Poniższy przykładowy kod przedstawia sposób toocreate zasób uprawnienia do odczytu hello token zasobu hello uprawnienia zasobu i skojarzyć hello uprawnienia z hello [użytkownika](#users) utworzone powyżej.</span><span class="sxs-lookup"><span data-stu-id="bfe1b-175">hello following code sample shows how toocreate a permission resource, read hello resource token of hello permission resource, and associate hello permissions with hello [user](#users) created above.</span></span>

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

<span data-ttu-id="bfe1b-176">Jeśli określono klucza partycji dla kolekcji, następnie hello uprawnienia dla kolekcji, dokumentów i załączników zasobów musi także obejmować hello ResourcePartitionKey w toohello dodanie ResourceLink.</span><span class="sxs-lookup"><span data-stu-id="bfe1b-176">If you have specified a partition key for your collection, then hello permission for collection, document, and attachment resources must also include hello ResourcePartitionKey in addition toohello ResourceLink.</span></span>

### <a name="code-sample-tooread-permissions-for-user"></a><span data-ttu-id="bfe1b-177">Przykładowy kod tooread uprawnienia użytkownika</span><span class="sxs-lookup"><span data-stu-id="bfe1b-177">Code sample tooread permissions for user</span></span>

<span data-ttu-id="bfe1b-178">tooeasily uzyskać wszystkie zasoby uprawnienia skojarzone z określonym użytkownikiem, DB rozwiązania Cosmos udostępnia uprawnienie dla każdego obiektu użytkownika.</span><span class="sxs-lookup"><span data-stu-id="bfe1b-178">tooeasily obtain all permission resources associated with a particular user, Cosmos DB makes available a permission feed for each user object.</span></span>  <span data-ttu-id="bfe1b-179">Witaj poniższy fragment kodu przedstawia sposób tworzenia tooretrieve hello uprawnienia powiązane z użytkownikiem hello powyżej, utworzenia listy uprawnień i wystąpienia nowego wystąpienia klasy DocumentClient w imieniu użytkownika hello.</span><span class="sxs-lookup"><span data-stu-id="bfe1b-179">hello following code snippet shows how tooretrieve hello permission associated with hello user created above, construct a permission list, and instantiate a new DocumentClient on behalf of hello user.</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="bfe1b-180">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="bfe1b-180">Next steps</span></span>
* <span data-ttu-id="bfe1b-181">toolearn więcej informacji na temat zabezpieczeń bazy danych DB rozwiązania Cosmos, zobacz [rozwiązania Cosmos bazy danych: baza danych zabezpieczeń](database-security.md).</span><span class="sxs-lookup"><span data-stu-id="bfe1b-181">toolearn more about Cosmos DB database security, see [Cosmos DB: Database security](database-security.md).</span></span>
* <span data-ttu-id="bfe1b-182">toolearn o zarządzaniu kluczami głównego i tylko do odczytu, zobacz [jak toomanage konta bazy danych Azure rozwiązania Cosmos](manage-account.md#keys).</span><span class="sxs-lookup"><span data-stu-id="bfe1b-182">toolearn about managing master and read-only keys, see [How toomanage an Azure Cosmos DB account](manage-account.md#keys).</span></span>
* <span data-ttu-id="bfe1b-183">tokeny autoryzacji bazy danych Azure rozwiązania Cosmos tooconstruct, zobacz temat toolearn [kontroli dostępu do zasobów DB rozwiązania Cosmos Azure](https://docs.microsoft.com/rest/api/documentdb/access-control-on-documentdb-resources).</span><span class="sxs-lookup"><span data-stu-id="bfe1b-183">toolearn how tooconstruct Azure Cosmos DB authorization tokens, see [Access Control on Azure Cosmos DB Resources](https://docs.microsoft.com/rest/api/documentdb/access-control-on-documentdb-resources).</span></span>
