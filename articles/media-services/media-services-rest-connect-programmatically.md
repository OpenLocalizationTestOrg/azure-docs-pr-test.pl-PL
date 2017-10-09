---
title: "tooMedia aaaConnecting konto usługi za pomocą interfejsu API REST | Dokumentacja firmy Microsoft"
description: "W tym temacie przedstawiono, jak za pomocą usługi tooMedia tooconnect REST API."
services: media-services
documentationcenter: 
author: Juliako
manager: erikre
editor: 
ms.assetid: 79dc64f1-15d8-4a81-b9d9-3d3c44d2e1e8
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 09/26/2016
ms.author: juliako
ms.openlocfilehash: 1d5064a3612dc96f5c5ad910d183d84fb70a3b6a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="connecting-toomedia-services-account-using-media-services-rest-api"></a><span data-ttu-id="6a5bb-103">Łączenie tooMedia konta usług przy użyciu interfejsu API REST usługi multimediów</span><span class="sxs-lookup"><span data-stu-id="6a5bb-103">Connecting tooMedia Services Account using Media Services REST API</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="6a5bb-104">.NET</span><span class="sxs-lookup"><span data-stu-id="6a5bb-104">.NET</span></span>](media-services-dotnet-connect-programmatically.md)
> * [<span data-ttu-id="6a5bb-105">REST</span><span class="sxs-lookup"><span data-stu-id="6a5bb-105">REST</span></span>](media-services-rest-connect-programmatically.md)
> 
> 

<span data-ttu-id="6a5bb-106">W tym temacie opisano, jak tooobtain tooMicrosoft połączenie programowe usługi Azure Media Services są programowania z hello interfejsu API REST usługi multimediów.</span><span class="sxs-lookup"><span data-stu-id="6a5bb-106">This topic describes how tooobtain a programmatic connection tooMicrosoft Azure Media Services when you are programming with hello Media Services REST API.</span></span>

<span data-ttu-id="6a5bb-107">Dwie czynności są wymagane podczas uzyskiwania dostępu do usługi Microsoft Azure Media Services: token dostępu udostępniane przez usługi kontroli dostępu (ACS) Azure i hello identyfikator URI usługi Media Services samej siebie.</span><span class="sxs-lookup"><span data-stu-id="6a5bb-107">Two things are required when accessing Microsoft Azure Media Services: An access token provided by Azure Access Control Services (ACS), and hello URI of Media Services itself.</span></span> <span data-ttu-id="6a5bb-108">Można użyć dowolnego oznacza, że chcesz podczas tworzenia tych żądań tak długo, jak określić hello nagłówka poprawne wartości i przekaż token dostępu hello poprawnie podczas wywoływania metody do usługi Media Services.</span><span class="sxs-lookup"><span data-stu-id="6a5bb-108">You can use any means you want when creating these requests as long as you specify hello correct header values and pass in hello access token correctly when calling into Media Services.</span></span>

<span data-ttu-id="6a5bb-109">Hello następujące kroki opisano hello najczęściej przepływu pracy, gdy za pomocą tooMedia tooconnect interfejsu API REST usług Media hello usług:</span><span class="sxs-lookup"><span data-stu-id="6a5bb-109">hello following steps describe hello most common workflow when using hello Media Services REST API tooconnect tooMedia Services:</span></span>

1. <span data-ttu-id="6a5bb-110">Pobieranie tokenu dostępu</span><span class="sxs-lookup"><span data-stu-id="6a5bb-110">Getting an access token</span></span> 
2. <span data-ttu-id="6a5bb-111">Łączenie toohello identyfikator URI usługi multimediów</span><span class="sxs-lookup"><span data-stu-id="6a5bb-111">Connecting toohello Media Services URI</span></span> 
   
   > [!NOTE]
   > <span data-ttu-id="6a5bb-112">Po pomyślnym połączeniu toohttps://media.windows.net, otrzymasz 301 przekierowanie, określając inny identyfikator URI usługi multimediów.</span><span class="sxs-lookup"><span data-stu-id="6a5bb-112">After successfully connecting toohttps://media.windows.net, you will receive a 301 redirect specifying another Media Services URI.</span></span> <span data-ttu-id="6a5bb-113">Należy wykonać kolejne wywołania toohello nowy identyfikator URI.</span><span class="sxs-lookup"><span data-stu-id="6a5bb-113">You must make subsequent calls toohello new URI.</span></span>
   > <span data-ttu-id="6a5bb-114">Otrzymasz również odpowiedź HTTP/1.1 200, która zawiera hello opis metadanych interfejsu API ODATA.</span><span class="sxs-lookup"><span data-stu-id="6a5bb-114">You may also receive a HTTP/1.1 200 response that contains hello ODATA API metadata description.</span></span>
   > 
   > 
3. <span data-ttu-id="6a5bb-115">Po kolejnych interfejsu API wywołania toohello nowego adresu URL.</span><span class="sxs-lookup"><span data-stu-id="6a5bb-115">Post your subsequent API calls toohello new URL.</span></span> 
   
    <span data-ttu-id="6a5bb-116">Na przykład jeśli po wypróbowaniu tooconnect, masz następujące hello:</span><span class="sxs-lookup"><span data-stu-id="6a5bb-116">For example, if after trying tooconnect, you got hello following:</span></span>
   
        HTTP/1.1 301 Moved Permanently
        Location: https://wamsbayclus001rest-hs.cloudapp.net/api/
   
    <span data-ttu-id="6a5bb-117">Należy zadać programu późniejsze toohttps://wamsbayclus001rest-hs.cloudapp.net/api/ wywołania interfejsu API.</span><span class="sxs-lookup"><span data-stu-id="6a5bb-117">You should post your subsequent API calls toohttps://wamsbayclus001rest-hs.cloudapp.net/api/.</span></span>

    >[!NOTE]
    ><span data-ttu-id="6a5bb-118">Limit różnych zasad usługi AMS wynosi 1 000 000 (na przykład zasad lokalizatorów lub ContentKeyAuthorizationPolicy).</span><span class="sxs-lookup"><span data-stu-id="6a5bb-118">There is a limit of 1,000,000 policies for different AMS policies (for example, for Locator policy or ContentKeyAuthorizationPolicy).</span></span> <span data-ttu-id="6a5bb-119">Należy używać hello tym samym identyfikatorze zasad, jeśli używasz zawsze hello sam dni / dostęp uprawnień, na przykład zasady dla lokalizatorów, które są przeznaczone tooremain w miejscu przez długi czas (zasady — przekazywanie).</span><span class="sxs-lookup"><span data-stu-id="6a5bb-119">You should use hello same policy ID if you are always using hello same days / access permissions, for example, policies for locators that are intended tooremain in place for a long time (non-upload policies).</span></span> <span data-ttu-id="6a5bb-120">Aby uzyskać więcej informacji, zobacz [ten](media-services-dotnet-manage-entities.md#limit-access-policies) temat.</span><span class="sxs-lookup"><span data-stu-id="6a5bb-120">For more information, see [this](media-services-dotnet-manage-entities.md#limit-access-policies) topic.</span></span>

## <a name="access-control-address"></a><span data-ttu-id="6a5bb-121">Adres kontroli dostępu</span><span class="sxs-lookup"><span data-stu-id="6a5bb-121">Access control address</span></span>
<span data-ttu-id="6a5bb-122">Adres kontroli dostępu do usługi Media Services jest https://wamsprodglobal001acs.accesscontrol.windows.net, z wyjątkiem Chin Północna regionu, w których jest https://wamsprodglobal001acs.accesscontrol.chinacloudapi.cn.</span><span class="sxs-lookup"><span data-stu-id="6a5bb-122">Media Services access control address is https://wamsprodglobal001acs.accesscontrol.windows.net, except for North China region, where it is https://wamsprodglobal001acs.accesscontrol.chinacloudapi.cn.</span></span>

## <a name="getting-an-access-token"></a><span data-ttu-id="6a5bb-123">Pobieranie tokenu dostępu</span><span class="sxs-lookup"><span data-stu-id="6a5bb-123">Getting an access token</span></span>
<span data-ttu-id="6a5bb-124">tooaccess Media Services bezpośrednio za pomocą hello interfejsu API REST, pobrać token dostępu z usługi kontroli dostępu i używać go podczas każdego żądania HTTP, wprowadzone do usługi hello.</span><span class="sxs-lookup"><span data-stu-id="6a5bb-124">tooaccess Media Services directly through hello REST API, retrieve an access token from ACS and use it during every HTTP request you make into hello service.</span></span> <span data-ttu-id="6a5bb-125">Token ten jest podobny tokenów tooother udostępniane przez usługi ACS na podstawie oświadczeń dostępu podany w nagłówku hello żądania HTTP i przy użyciu protokołu hello OAuth v2.</span><span class="sxs-lookup"><span data-stu-id="6a5bb-125">This token is similar tooother tokens provided by ACS based on access claims provided in hello header of an HTTP request and using hello OAuth v2 protocol.</span></span> <span data-ttu-id="6a5bb-126">Nie trzeba innych wymagań wstępnych przed bezpośredniego połączenia usługi tooMedia.</span><span class="sxs-lookup"><span data-stu-id="6a5bb-126">You do not need any other prerequisites before directly connecting tooMedia Services.</span></span>

<span data-ttu-id="6a5bb-127">Witaj poniższy przykład przedstawia nagłówek żądania HTTP hello i tooretrieve treść, używać tokenu.</span><span class="sxs-lookup"><span data-stu-id="6a5bb-127">hello following example shows hello HTTP request header and body used tooretrieve a token.</span></span>

<span data-ttu-id="6a5bb-128">**Nagłówek**:</span><span class="sxs-lookup"><span data-stu-id="6a5bb-128">**Header**:</span></span>

    POST https://wamsprodglobal001acs.accesscontrol.windows.net/v2/OAuth2-13 HTTP/1.1
    Content-Type: application/x-www-form-urlencoded
    Host: wamsprodglobal001acs.accesscontrol.windows.net
    Content-Length: 120
    Expect: 100-continue
    Connection: Keep-Alive
    Accept: application/json


<span data-ttu-id="6a5bb-129">**Treść**:</span><span class="sxs-lookup"><span data-stu-id="6a5bb-129">**Body**:</span></span>

<span data-ttu-id="6a5bb-130">Należy tooprove wartości client_id i client_secret hello w treści hello tego żądania; client_id i client_secret odpowiadają toohello AccountName i AccountKey wartości, odpowiednio.</span><span class="sxs-lookup"><span data-stu-id="6a5bb-130">You need tooprove hello client_id and client_secret values in hello body of this request; client_id and client_secret correspond toohello AccountName and AccountKey values, respectively.</span></span> <span data-ttu-id="6a5bb-131">Te wartości są dostarczane tooyou przez usługę Media Services, po skonfigurowaniu konta.</span><span class="sxs-lookup"><span data-stu-id="6a5bb-131">These values are provided tooyou by Media Services when you set up your account.</span></span> 

<span data-ttu-id="6a5bb-132">Należy pamiętać, że hello AccountKey dla konta usługi Media Services musi być zakodowane w adresie URL (zobacz [kodowanie procent](http://tools.ietf.org/html/rfc3986#section-2.1) w przypadku używania go jako wartość client_secret hello w żądanie tokenu dostępu.</span><span class="sxs-lookup"><span data-stu-id="6a5bb-132">Note that hello AccountKey for your Media Services account must be URL-encoded (see [Percent-Encoding](http://tools.ietf.org/html/rfc3986#section-2.1) when using it as hello client_secret value in your access token request.</span></span>

    grant_type=client_credentials&client_id=ams_account_name&client_secret=URL_encoded_ams_account_key&scope=urn%3aWindowsAzureMediaServices


<span data-ttu-id="6a5bb-133">Na przykład:</span><span class="sxs-lookup"><span data-stu-id="6a5bb-133">For example:</span></span> 

    grant_type=client_credentials&client_id=amstestaccount001&client_secret=wUNbKhNj07oqjqU3Ah9R9f4kqTJ9avPpfe6Pk3YZ7ng%3d&scope=urn%3aWindowsAzureMediaServices


<span data-ttu-id="6a5bb-134">Witaj poniższy przykład przedstawia hello odpowiedź HTTP, która zawiera dostępu hello tokenu w treści odpowiedzi hello.</span><span class="sxs-lookup"><span data-stu-id="6a5bb-134">hello following example shows hello HTTP response that contains hello access token in hello response body.</span></span>

    HTTP/1.1 200 OK
    Cache-Control: no-cache, no-store
    Pragma: no-cache
    Content-Type: application/json; charset=utf-8
    Expires: -1
    request-id: a65150f5-2784-4a01-a4b7-33456187ad83
    X-Content-Type-Options: nosniff
    Strict-Transport-Security: max-age=31536000; includeSubDomains
    Date: Thu, 15 Jan 2015 08:07:20 GMT
    Content-Length: 670

    {  
       "token_type":"http://schemas.xmlsoap.org/ws/2009/11/swt-token-profile-1.0",
       "access_token":"http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=amstestaccount001&urn%3aSubscriptionId=z7f19258-2233-4ca2-b1ae-193798e2c9d8&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1421330840&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=uf69n82KlqZmkJDNxhJkOxpyIpA2HDyeGUTtSnq1vlE%3d",
       "expires_in":"21600",
       "scope":"urn:WindowsAzureMediaServices"
    }


> [!NOTE]
> <span data-ttu-id="6a5bb-135">Zalecane jest toocache hello "' access_token '" i "expires_in" wartości tooan magazynu zewnętrznego.</span><span class="sxs-lookup"><span data-stu-id="6a5bb-135">It is recommended toocache hello "access_token " and "expires_in " values tooan external storage.</span></span> <span data-ttu-id="6a5bb-136">później można pobrać z magazynu hello i używać ponownie w wywołaniach interfejsu API REST usługi Media Hello danych tokenu.</span><span class="sxs-lookup"><span data-stu-id="6a5bb-136">hello token data could later be retrieved from hello storage and re-used in your Media Services REST API calls.</span></span> <span data-ttu-id="6a5bb-137">Jest to szczególnie przydatne w scenariuszach, gdzie hello token można bezpiecznie wymieniać między wiele procesów lub komputery.</span><span class="sxs-lookup"><span data-stu-id="6a5bb-137">This is especially useful for scenarios where hello token can be securely shared among multiple processes or computers.</span></span>
> 
> 

<span data-ttu-id="6a5bb-138">Upewnij się, że wartość "expires_in" hello toomonitor dostępu hello tokenu i zaktualizuj wywołaniach interfejsu API REST przy nowe tokeny, zgodnie z potrzebami.</span><span class="sxs-lookup"><span data-stu-id="6a5bb-138">Make sure toomonitor hello "expires_in" value of hello access token and update your REST API calls with new tokens as needed.</span></span>

### <a name="connecting-toohello-media-services-uri"></a><span data-ttu-id="6a5bb-139">Łączenie toohello identyfikator URI usługi multimediów</span><span class="sxs-lookup"><span data-stu-id="6a5bb-139">Connecting toohello Media Services URI</span></span>
<span data-ttu-id="6a5bb-140">główny Hello identyfikator URI dla usługi Media Services to https://media.windows.net/.</span><span class="sxs-lookup"><span data-stu-id="6a5bb-140">hello root URI for Media Services is https://media.windows.net/.</span></span> <span data-ttu-id="6a5bb-141">Początkowo należy połączyć toothis identyfikator URI, a można przywrócić 301 przekierowanie odpowiedzi, powinny być toohello wezwań nowy identyfikator URI.</span><span class="sxs-lookup"><span data-stu-id="6a5bb-141">You should initially connect toothis URI, and if you get a 301 redirect back in response, you should make subsequent calls toohello new URI.</span></span> <span data-ttu-id="6a5bb-142">Ponadto nie należy używać wszelka logika automatycznego przekierowania/wykonania w Twoich żądań.</span><span class="sxs-lookup"><span data-stu-id="6a5bb-142">In addition, do not use any auto-redirect/follow logic in your requests.</span></span> <span data-ttu-id="6a5bb-143">Zlecenia HTTP i treści żądania nie zostaną przekazane toohello nowy identyfikator URI.</span><span class="sxs-lookup"><span data-stu-id="6a5bb-143">HTTP verbs and request bodies will not be forwarded toohello new URI.</span></span>

<span data-ttu-id="6a5bb-144">Należy pamiętać, że hello głównego adresu URI do przekazywania i pobierania plików zasobów jest https://yourstorageaccount.blob.core.windows.net/, gdzie nazwa konta magazynu hello jest hello samym kluczem, używane podczas Konfiguracja konta usługi Media Services.</span><span class="sxs-lookup"><span data-stu-id="6a5bb-144">Note that hello root URI for uploading and downloading Asset files is https://yourstorageaccount.blob.core.windows.net/ where hello storage account name is hello same one you used during your Media Services account setup.</span></span>

<span data-ttu-id="6a5bb-145">Witaj poniższy przykład przedstawia HTTP żądania toohello Media Services głównego identyfikatora URI (https://media.windows.net/).</span><span class="sxs-lookup"><span data-stu-id="6a5bb-145">hello following example demonstrates HTTP request toohello Media Services root URI (https://media.windows.net/).</span></span> <span data-ttu-id="6a5bb-146">Żądanie hello pobiera 301 przekierowanie w odpowiedzi.</span><span class="sxs-lookup"><span data-stu-id="6a5bb-146">hello request gets a 301 redirect back in response.</span></span> <span data-ttu-id="6a5bb-147">Witaj kolejne żądanie używa hello nowy identyfikator URI (https://wamsbayclus001rest-hs.cloudapp.net/api/).</span><span class="sxs-lookup"><span data-stu-id="6a5bb-147">hello subsequent request is using hello new URI (https://wamsbayclus001rest-hs.cloudapp.net/api/).</span></span>     

<span data-ttu-id="6a5bb-148">**Żądanie HTTP**:</span><span class="sxs-lookup"><span data-stu-id="6a5bb-148">**HTTP Request**:</span></span>

    GET https://media.windows.net/ HTTP/1.1
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=amstestaccount001&urn%3aSubscriptionId=z7f19258-6753-4ca2-b1ae-193798e2c9d8&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1421500579&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=ElVWXOnMVggFQl%2ft9vhdcv1qH1n%2fE8l3hRef4zPmrzg%3d
    x-ms-version: 2.11
    Accept: application/json
    Host: media.windows.net


<span data-ttu-id="6a5bb-149">**Odpowiedź HTTP**:</span><span class="sxs-lookup"><span data-stu-id="6a5bb-149">**HTTP Response**:</span></span>

    HTTP/1.1 301 Moved Permanently
    Location: https://wamsbayclus001rest-hs.cloudapp.net/api/
    Server: Microsoft-IIS/8.5
    request-id: 987d7652-497a-44e5-b815-f492e02aef97
    x-ms-request-id: 987d7652-497a-44e5-b815-f492e02aef97
    X-Powered-By: ASP.NET
    Strict-Transport-Security: max-age=31536000; includeSubDomains
    Date: Sat, 17 Jan 2015 07:44:53 GMT
    Content-Length: 164

    <html><head><title>Object moved</title></head><body>
    <h2>Object moved too<a href="https://wamsbayclus001rest-hs.cloudapp.net/api/">here</a>.</h2>
    </body></html>


<span data-ttu-id="6a5bb-150">**Żądanie HTTP** (przy użyciu hello nowy identyfikator URI):</span><span class="sxs-lookup"><span data-stu-id="6a5bb-150">**HTTP Request** (using hello new URI):</span></span>

    GET https://wamsbayclus001rest-hs.cloudapp.net/api/ HTTP/1.1
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=amstestaccount001&urn%3aSubscriptionId=z7f19258-2233-4ca2-b1ae-193798e2c9d8&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1421500579&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=ElVWXOnMVggFQl%2ft9vhdcv1qH1n%2fE8l3hRef4zPmrzg%3d
    x-ms-version: 2.11
    Accept: application/json
    Host: wamsbayclus001rest-hs.cloudapp.net


<span data-ttu-id="6a5bb-151">**Odpowiedź HTTP**:</span><span class="sxs-lookup"><span data-stu-id="6a5bb-151">**HTTP Response**:</span></span>

    HTTP/1.1 200 OK
    Cache-Control: no-cache
    Content-Length: 1250
    Content-Type: application/json;odata=minimalmetadata;streaming=true;charset=utf-8
    Server: Microsoft-IIS/8.5
    request-id: 5f52ea9d-177e-48fe-9709-24953d19f84a
    x-ms-request-id: 5f52ea9d-177e-48fe-9709-24953d19f84a
    X-Content-Type-Options: nosniff
    DataServiceVersion: 3.0;
    X-Powered-By: ASP.NET
    Strict-Transport-Security: max-age=31536000; includeSubDomains
    Date: Sat, 17 Jan 2015 07:44:52 GMT

    {"odata.metadata":"https://wamsbayclus001rest-hs.cloudapp.net/api/$metadata","value":[{"name":"AccessPolicies","url":"AccessPolicies"},{"name":"Locators","url":"Locators"},{"name":"ContentKeys","url":"ContentKeys"},{"name":"ContentKeyAuthorizationPolicyOptions","url":"ContentKeyAuthorizationPolicyOptions"},{"name":"ContentKeyAuthorizationPolicies","url":"ContentKeyAuthorizationPolicies"},{"name":"Files","url":"Files"},{"name":"Assets","url":"Assets"},{"name":"AssetDeliveryPolicies","url":"AssetDeliveryPolicies"},{"name":"IngestManifestFiles","url":"IngestManifestFiles"},{"name":"IngestManifestAssets","url":"IngestManifestAssets"},{"name":"IngestManifests","url":"IngestManifests"},{"name":"StorageAccounts","url":"StorageAccounts"},{"name":"Tasks","url":"Tasks"},{"name":"NotificationEndPoints","url":"NotificationEndPoints"},{"name":"Jobs","url":"Jobs"},{"name":"TaskTemplates","url":"TaskTemplates"},{"name":"JobTemplates","url":"JobTemplates"},{"name":"MediaProcessors","url":"MediaProcessors"},{"name":"EncodingReservedUnitTypes","url":"EncodingReservedUnitTypes"},{"name":"Operations","url":"Operations"},{"name":"StreamingEndpoints","url":"StreamingEndpoints"},{"name":"Channels","url":"Channels"},{"name":"Programs","url":"Programs"}]}



> [!NOTE]
> <span data-ttu-id="6a5bb-152">Po pobraniu hello nowy identyfikator URI, który jest hello identyfikator URI, który powinien być toocommunicate używane z programem Media Services.</span><span class="sxs-lookup"><span data-stu-id="6a5bb-152">Once you get hello new URI, that is hello URI that should be used toocommunicate with Media Services.</span></span> 
> 
> 

## <a name="media-services-learning-paths"></a><span data-ttu-id="6a5bb-153">Ścieżki szkoleniowe dotyczące usługi Media Services</span><span class="sxs-lookup"><span data-stu-id="6a5bb-153">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="6a5bb-154">Przekazywanie opinii</span><span class="sxs-lookup"><span data-stu-id="6a5bb-154">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

