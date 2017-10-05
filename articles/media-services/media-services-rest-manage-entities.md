---
title: "Zarządzanie jednostki usługi Media Services z REST | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak zarządzać jednostki usługi Media Services z interfejsu API REST."
author: juliako
manager: cfowler
editor: 
services: media-services
documentationcenter: 
ms.assetid: 95262a32-0f2a-4286-b9e2-1a1ca6399b5b
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/10/2017
ms.author: juliako
ms.openlocfilehash: a336907b605da962f835b8057ac6071f480cd85e
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/29/2017
---
# <a name="managing-media-services-entities-with-rest"></a><span data-ttu-id="a7b10-103">Zarządzanie jednostki usługi Media Services z REST</span><span class="sxs-lookup"><span data-stu-id="a7b10-103">Managing Media Services entities with REST</span></span> 
> [!div class="op_single_selector"]
> * [<span data-ttu-id="a7b10-104">REST</span><span class="sxs-lookup"><span data-stu-id="a7b10-104">REST</span></span>](media-services-rest-manage-entities.md)
> * [<span data-ttu-id="a7b10-105">.NET</span><span class="sxs-lookup"><span data-stu-id="a7b10-105">.NET</span></span>](media-services-dotnet-manage-entities.md)
> 
> 

<span data-ttu-id="a7b10-106">Microsoft Azure Media Services to usługa opartego na interfejsie REST oparty na OData v3.</span><span class="sxs-lookup"><span data-stu-id="a7b10-106">Microsoft Azure Media Services is a REST-based service built on OData v3.</span></span> <span data-ttu-id="a7b10-107">Można dodać, zapytania, aktualizować i usuwać jednostek w taki sam sposób, jak na inne usługi OData.</span><span class="sxs-lookup"><span data-stu-id="a7b10-107">You can add, query, update, and delete entities in much the same way as you can on any other OData service.</span></span> <span data-ttu-id="a7b10-108">W razie potrzeby zostanie wywołana wyjątki.</span><span class="sxs-lookup"><span data-stu-id="a7b10-108">Exceptions will be called out when applicable.</span></span> <span data-ttu-id="a7b10-109">Aby uzyskać więcej informacji o OData, zobacz [dokumentacji protokołu Open Data Protocol](http://www.odata.org/documentation/).</span><span class="sxs-lookup"><span data-stu-id="a7b10-109">For more information on OData, see [Open Data Protocol documentation](http://www.odata.org/documentation/).</span></span>

<span data-ttu-id="a7b10-110">W tym temacie przedstawiono sposób zarządzania jednostki usługi Azure Media Services z REST.</span><span class="sxs-lookup"><span data-stu-id="a7b10-110">This topic shows you how to manage Azure Media Services entities with REST.</span></span>

>[!NOTE]
> <span data-ttu-id="a7b10-111">Począwszy od 1 kwietnia 2017 roku, wszystkie rekordy zadań na Twoim koncie, które są starsze niż 90 dni, będą automatycznie usuwane wraz ze skojarzonymi rekordami zadań podrzędnych nawet wtedy, gdy całkowita liczba rekordów jest mniejsza niż maksymalny limit przydziału.</span><span class="sxs-lookup"><span data-stu-id="a7b10-111">Starting April 1, 2017, any Job record in your account older than 90 days will be automatically deleted, along with its associated Task records, even if the total number of records is below the maximum quota.</span></span> <span data-ttu-id="a7b10-112">Na przykład na 1 kwietnia 2017 dowolnego rekordu zadania konta starsze niż 31 grudnia 2016 r., zostaną automatycznie usunięte.</span><span class="sxs-lookup"><span data-stu-id="a7b10-112">For example, on April 1, 2017, any Job record in your account older than December 31, 2016, will be automatically deleted.</span></span> <span data-ttu-id="a7b10-113">Jeśli chcesz zarchiwizować informacje zadania lub zadanie, można użyć kodu opisanych w tym temacie.</span><span class="sxs-lookup"><span data-stu-id="a7b10-113">If you need to archive the job/task information, you can use the code described in this topic.</span></span>

## <a name="considerations"></a><span data-ttu-id="a7b10-114">Zagadnienia do rozważenia</span><span class="sxs-lookup"><span data-stu-id="a7b10-114">Considerations</span></span>  

<span data-ttu-id="a7b10-115">Podczas uzyskiwania dostępu do obiektów w usłudze Media Services, należy ustawić określonych pól nagłówka i wartości w Twoich żądań HTTP.</span><span class="sxs-lookup"><span data-stu-id="a7b10-115">When accessing entities in Media Services, you must set specific header fields and values in your HTTP requests.</span></span> <span data-ttu-id="a7b10-116">Aby uzyskać więcej informacji, zobacz [ustawień dla rozwoju interfejsu API REST usługi Media](media-services-rest-how-to-use.md).</span><span class="sxs-lookup"><span data-stu-id="a7b10-116">For more information, see [Setup for Media Services REST API Development](media-services-rest-how-to-use.md).</span></span>

## <a name="connect-to-media-services"></a><span data-ttu-id="a7b10-117">Łączenie się z usługą Media Services</span><span class="sxs-lookup"><span data-stu-id="a7b10-117">Connect to Media Services</span></span>

<span data-ttu-id="a7b10-118">Aby uzyskać informacje na temat nawiązywania połączenia z interfejsu API usług AMS, zobacz [dostępu Azure Media Services API przy użyciu uwierzytelniania usługi Azure AD](media-services-use-aad-auth-to-access-ams-api.md).</span><span class="sxs-lookup"><span data-stu-id="a7b10-118">For information on how to connect to the AMS API, see [Access the Azure Media Services API with Azure AD authentication](media-services-use-aad-auth-to-access-ams-api.md).</span></span> 

>[!NOTE]
><span data-ttu-id="a7b10-119">Po pomyślnym połączeniu się https://media.windows.net, otrzymasz 301 przekierowanie, określając inny identyfikator URI usługi multimediów.</span><span class="sxs-lookup"><span data-stu-id="a7b10-119">After successfully connecting to https://media.windows.net, you will receive a 301 redirect specifying another Media Services URI.</span></span> <span data-ttu-id="a7b10-120">Upewnij się kolejne wywołania nowy identyfikator URI.</span><span class="sxs-lookup"><span data-stu-id="a7b10-120">You must make subsequent calls to the new URI.</span></span>

## <a name="adding-entities"></a><span data-ttu-id="a7b10-121">Dodawanie jednostek</span><span class="sxs-lookup"><span data-stu-id="a7b10-121">Adding entities</span></span>
<span data-ttu-id="a7b10-122">Każdy podmiot w usłudze Media Services jest dodawane do zestawu jednostek, takich jak zasoby, za pomocą żądania POST HTTP.</span><span class="sxs-lookup"><span data-stu-id="a7b10-122">Every entity in Media Services is added to an entity set, such as Assets, through a POST HTTP request.</span></span>

<span data-ttu-id="a7b10-123">Poniższy przykład przedstawia sposób tworzenia AccessPolicy.</span><span class="sxs-lookup"><span data-stu-id="a7b10-123">The following example shows how to create an AccessPolicy.</span></span>

    POST https://media.windows.net/API/AccessPolicies HTTP/1.1
    Content-Type: application/json;odata=verbose
    Accept: application/json;odata=verbose
    DataServiceVersion: 3.0
    MaxDataServiceVersion: 3.0
    x-ms-version: 2.11
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=youraccountname&urn%3aSubscriptionId=2f84471d-b1ae-4e75-aa09-010f0fc0cf5b&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1337067658&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=dithjGvlXR9HlyAf5DE99N5OCYkPAxsHIcsTSjm9%2fVE%3d
    Host: media.windows.net
    Content-Length: 74
    Expect: 100-continue

    {"Name": "DownloadPolicy", "DurationInMinutes" : "300", "Permissions" : 1}

## <a name="querying-entities"></a><span data-ttu-id="a7b10-124">Wykonywanie zapytania jednostek</span><span class="sxs-lookup"><span data-stu-id="a7b10-124">Querying entities</span></span>
<span data-ttu-id="a7b10-125">Badanie i wyświetlania jednostek jest proste i obejmuje tylko żądania GET HTTP i opcjonalnie operacje OData.</span><span class="sxs-lookup"><span data-stu-id="a7b10-125">Querying and listing entities is straightforward and only involves a GET HTTP request and optional OData operations.</span></span>
<span data-ttu-id="a7b10-126">Poniższy przykład powoduje pobranie listy wszystkich jednostek MediaProcessor.</span><span class="sxs-lookup"><span data-stu-id="a7b10-126">The following example retrieves a list of all MediaProcessor entities.</span></span>

    GET https://media.windows.net/API/MediaProcessors HTTP/1.1
    Content-Type: application/json;odata=verbose
    Accept: application/json;odata=verbose
    DataServiceVersion: 3.0
    MaxDataServiceVersion: 3.0
    x-ms-version: 2.11
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=youraccountname&urn%3aSubscriptionId=2f84471d-b1ae-4e75-aa09-010f0fc0cf5b&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1337078831&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=suFkxhvPWxQVMjOYelOJfYEWkyTWJCBc02pF0N7NghI%3d
    Host: media.windows.net

<span data-ttu-id="a7b10-127">Można również pobrać jednostki określonych lub wszystkich zestawów jednostek skojarzonych z wybraną jednostką, takich jak w poniższych przykładach:</span><span class="sxs-lookup"><span data-stu-id="a7b10-127">You can also retrieve a specific entity or all entity sets associated with a specific entity, such as in the following examples:</span></span>

    GET https://media.windows.net/API/JobTemplates('nb:jtid:UUID:e81192f5-576f-b247-b781-70a790c20e7c') HTTP/1.1
    Content-Type: application/json;odata=verbose
    Accept: application/json;odata=verbose
    DataServiceVersion: 3.0
    MaxDataServiceVersion: 3.0
    x-ms-version: 2.11
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=youraccountname&urn%3aSubscriptionId=2f84471d-b1ae-4e75-aa09-010f0fc0cf5b&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1336907474&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=OpuY0CeTylqFFcFaP4pKUVGesT4PGx4CP55zDf2zXnc%3d
    Host: media.windows.net

    GET https://media.windows.net/API/JobTemplates('nb:jtid:UUID:e81192f5-576f-b247-b781-70a790c20e7c')/TaskTemplates HTTP/1.1
    Content-Type: application/json;odata=verbose
    Accept: application/json;odata=verbose
    DataServiceVersion: 3.0
    MaxDataServiceVersion: 3.0
    x-ms-version: 2.11
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=youraccountname&urn%3aSubscriptionId=2f84471d-b1ae-4e75-aa09-010f0fc0cf5b&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1336907474&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=OpuY0CeTylqFFcFaP4pKUVGesT4PGx4CP55zDf2zXnc%3d
    Host: media.windows.net

<span data-ttu-id="a7b10-128">Poniższy przykład zwraca tylko właściwość stan wszystkich zadań.</span><span class="sxs-lookup"><span data-stu-id="a7b10-128">The following example returns only the State property of all Jobs.</span></span>

    GET https://media.windows.net/API/Jobs?$select=State HTTP/1.1
    Content-Type: application/json;odata=verbose
    Accept: application/json;odata=verbose
    DataServiceVersion: 3.0
    MaxDataServiceVersion: 3.0
    x-ms-version: 2.11
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=youraccountname&urn%3aSubscriptionId=2f84471d-b1ae-4e75-aa09-010f0fc0cf5b&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1337078831&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=suFkxhvPWxQVMjOYelOJfYEWkyTWJCBc02pF0N7NghI%3d
    Host: media.windows.net

<span data-ttu-id="a7b10-129">Poniższy przykład zwraca wszystkie JobTemplates o nazwie "SampleTemplate."</span><span class="sxs-lookup"><span data-stu-id="a7b10-129">The following example returns all JobTemplates with the name "SampleTemplate."</span></span>

    GET https://media.windows.net/API/JobTemplates?$filter=startswith(Name,%20'SampleTemplate') HTTP/1.1
    Content-Type: application/json;odata=verbose
    Accept: application/json;odata=verbose
    DataServiceVersion: 3.0
    MaxDataServiceVersion: 3.0
    x-ms-version: 2.11
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=youraccountname&urn%3aSubscriptionId=2f84471d-b1ae-4e75-aa09-010f0fc0cf5b&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1337078831&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=suFkxhvPWxQVMjOYelOJfYEWkyTWJCBc02pF0N7NghI%3d
    Host: media.windows.net

> [!NOTE]
> <span data-ttu-id="a7b10-130">$Rozwiń operacja nie jest obsługiwana w usługi Media Services, a także nieobsługiwany LINQ metod opisanych w zagadnienia dotyczące LINQ (usługi danych WCF).</span><span class="sxs-lookup"><span data-stu-id="a7b10-130">The $expand operation is not supported in Media Services as well as the unsupported LINQ methods described in LINQ Considerations (WCF Data Services).</span></span>
> 
> 

## <a name="enumerating-through-large-collections-of-entities"></a><span data-ttu-id="a7b10-131">Wyliczanie za pośrednictwem dużych kolekcjach jednostek</span><span class="sxs-lookup"><span data-stu-id="a7b10-131">Enumerating through large collections of entities</span></span>
<span data-ttu-id="a7b10-132">Podczas wykonywania zapytania jednostek, istnieje limit 1000 jednostek zwracane w tym samym czasie, ponieważ publiczny v2 REST ogranicza wyniki zapytania do 1000 wyników.</span><span class="sxs-lookup"><span data-stu-id="a7b10-132">When querying entities, there is a limit of 1000 entities returned at one time because public REST v2 limits query results to 1000 results.</span></span> <span data-ttu-id="a7b10-133">Użyj **pominąć** i **górnej** do sortowania dużych kolekcji jednostek.</span><span class="sxs-lookup"><span data-stu-id="a7b10-133">Use **skip** and **top** to enumerate through the large collection of entities.</span></span> 

<span data-ttu-id="a7b10-134">Poniższy przykład przedstawia użycie **pominąć** i **górnej** pominąć najpierw 2000 zadań w celu uzyskania obok 1000 zadania.</span><span class="sxs-lookup"><span data-stu-id="a7b10-134">The following example shows how to use **skip** and **top** to skip the first 2000 jobs and get the next 1000 jobs.</span></span>  

    GET https://media.windows.net/api/Jobs()?$skip=2000&$top=1000 HTTP/1.1
    Content-Type: application/json;odata=verbose
    Accept: application/json;odata=verbose
    DataServiceVersion: 3.0
    MaxDataServiceVersion: 3.0
    x-ms-version: 2.11
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=youraccountname&urn%3aSubscriptionId=2f84471d-b1ae-4e75-aa09-010f0fc0cf5b&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1337078831&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=suFkxhvPWxQVMjOYelOJfYEWkyTWJCBc02pF0N7NghI%3d
    Host: media.windows.net

## <a name="updating-entities"></a><span data-ttu-id="a7b10-135">Aktualizowanie jednostek</span><span class="sxs-lookup"><span data-stu-id="a7b10-135">Updating entities</span></span>
<span data-ttu-id="a7b10-136">W zależności od typu jednostki i stanie, który znajduje się w należy zaktualizować właściwości tego obiektu za pomocą poprawki, żądań PUT lub scalania HTTP.</span><span class="sxs-lookup"><span data-stu-id="a7b10-136">Depending on the entity type and the state that it is in, you can update properties on that entity through a PATCH, PUT, or MERGE HTTP requests.</span></span> <span data-ttu-id="a7b10-137">Aby uzyskać więcej informacji o tych operacjach, zobacz [poprawki/PUT/MERGE](https://msdn.microsoft.com/library/dd541276.aspx).</span><span class="sxs-lookup"><span data-stu-id="a7b10-137">For more information about these operations, see [PATCH/PUT/MERGE](https://msdn.microsoft.com/library/dd541276.aspx).</span></span>

<span data-ttu-id="a7b10-138">Poniższy przykład kodu pokazuje, jak zaktualizować właściwość Name z jednostką zasobów.</span><span class="sxs-lookup"><span data-stu-id="a7b10-138">The following code example shows how to update the Name property on an Asset entity.</span></span>

    MERGE https://media.windows.net/API/Assets('nb:cid:UUID:80782407-3f87-4e60-a43e-5e4454232f60') HTTP/1.1
    Content-Type: application/json;odata=verbose
    Accept: application/json;odata=verbose
    DataServiceVersion: 3.0
    MaxDataServiceVersion: 3.0
    x-ms-version: 2.11
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=youraccountname&urn%3aSubscriptionId=2f84471d-b1ae-4e75-aa09-010f0fc0cf5b&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1337083279&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=DMLQXWah4jO0icpfwyws5k%2b1aCDfz9KDGIGao20xk6g%3d
    Host: media.windows.net
    Content-Length: 21
    Expect: 100-continue

    {"Name" : "NewName" }

## <a name="deleting-entities"></a><span data-ttu-id="a7b10-139">Usuwanie jednostek</span><span class="sxs-lookup"><span data-stu-id="a7b10-139">Deleting entities</span></span>
<span data-ttu-id="a7b10-140">Jednostki mogą zostać usunięte w usłudze Media Services przy użyciu żądania DELETE HTTP.</span><span class="sxs-lookup"><span data-stu-id="a7b10-140">Entities can be deleted in Media Services by using a DELETE HTTP request.</span></span> <span data-ttu-id="a7b10-141">W zależności od podmiotu kolejność, w którym usuwania jednostek może być ważne.</span><span class="sxs-lookup"><span data-stu-id="a7b10-141">Depending on the entity, the order in which you delete entities may be important.</span></span> <span data-ttu-id="a7b10-142">Na przykład jednostek, takich jak zasoby wymagają, aby odwołać (lub usuń) wszystkie lokalizatorów, które odwołują się do tego konkretnego trwałego przed usunięciem elementu zawartości.</span><span class="sxs-lookup"><span data-stu-id="a7b10-142">For example, entities such as Assets require that you revoke (or delete) all Locators that reference that particular Asset before deleting the Asset.</span></span>

<span data-ttu-id="a7b10-143">Poniższy przykład przedstawia sposób usuwania lokalizatora, którego użyto do przekazania pliku do magazynu obiektów blob.</span><span class="sxs-lookup"><span data-stu-id="a7b10-143">The following example shows how to delete a Locator that was used to upload a file into blob storage.</span></span>

    DELETE https://media.windows.net/API/Locators('nb:lid:UUID:76dcc8e8-4230-463d-97b0-ce25c41b5c8d') HTTP/1.1
    Content-Type: application/json;odata=verbose
    Accept: application/json;odata=verbose
    DataServiceVersion: 3.0
    MaxDataServiceVersion: 3.0
    x-ms-version: 2.11
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=youraccountname&urn%3aSubscriptionId=2f84471d-b1ae-4e75-aa09-010f0fc0cf5b&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1337067658&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=dithjGvlXR9HlyAf5DE99N5OCYkPAxsHIcsTSjm9%2fVE%3d
    Host: media.windows.net
    Content-Length: 0

## <a name="media-services-learning-paths"></a><span data-ttu-id="a7b10-144">Ścieżki szkoleniowe dotyczące usługi Media Services</span><span class="sxs-lookup"><span data-stu-id="a7b10-144">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="a7b10-145">Przekazywanie opinii</span><span class="sxs-lookup"><span data-stu-id="a7b10-145">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

