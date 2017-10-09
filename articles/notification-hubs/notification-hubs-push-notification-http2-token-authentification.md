---
title: "na podstawie aaaToken uwierzytelniania (HTTP/2) dla usługi APNS w usłudze Azure Notification Hubs | Dokumentacja firmy Microsoft"
description: "W tym temacie wyjaśniono, jak tooleverage hello nowy token uwierzytelniania dla usługi APNS"
services: notification-hubs
documentationcenter: .net
author: kpiteira
manager: erikre
editor: 
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: mobile-multiple
ms.devlang: dotnet
ms.topic: article
ms.date: 05/17/2017
ms.author: kapiteir
ms.openlocfilehash: 3353d7f16033ce0b68edec9ee9aeb98f47faa1fa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="token-based-http2-authentication-for-apns"></a><span data-ttu-id="c0787-103">Uwierzytelniania opartego na tokenie (HTTP/2) dla usługi APNS</span><span class="sxs-lookup"><span data-stu-id="c0787-103">Token-based (HTTP/2) Authentication for APNS</span></span>
## <a name="overview"></a><span data-ttu-id="c0787-104">Omówienie</span><span class="sxs-lookup"><span data-stu-id="c0787-104">Overview</span></span>
<span data-ttu-id="c0787-105">Ten artykuł zawiera szczegóły dotyczące sposobu uwierzytelniania opartego na toouse hello nowego APNS HTTP/2 protokołu z tokenem.</span><span class="sxs-lookup"><span data-stu-id="c0787-105">This article details how toouse hello new APNS HTTP/2 protocol with token based authentication.</span></span>

<span data-ttu-id="c0787-106">Witaj klucza przy użyciu nowego protokołu hello zalety:</span><span class="sxs-lookup"><span data-stu-id="c0787-106">hello key benefits of using hello new protocol include:</span></span>
-   <span data-ttu-id="c0787-107">Generowania tokenów jest stosunkowo proste wolnego (toocertificates porównaniu)</span><span class="sxs-lookup"><span data-stu-id="c0787-107">Token generation is relatively hassle free (compared toocertificates)</span></span>
-   <span data-ttu-id="c0787-108">Nie więcej daty wygaśnięcia — są w formancie tokenów uwierzytelniania i ich odwołań</span><span class="sxs-lookup"><span data-stu-id="c0787-108">No more expiry dates – you are in control of your authentication tokens and their revocation</span></span>
-   <span data-ttu-id="c0787-109">Ładunki można teraz się too4 KB</span><span class="sxs-lookup"><span data-stu-id="c0787-109">Payloads can now be up too4 KB</span></span>
- <span data-ttu-id="c0787-110">Synchroniczne opinii</span><span class="sxs-lookup"><span data-stu-id="c0787-110">Synchronous feedback</span></span>
-   <span data-ttu-id="c0787-111">Możesz teraz najnowsze protokołu firmy Apple – certyfikaty nadal używać hello binarne protokołu, który jest oznaczony do amortyzacja</span><span class="sxs-lookup"><span data-stu-id="c0787-111">You’re on Apple’s latest protocol – certificates still use hello binary protocol, which is marked for deprecation</span></span>

<span data-ttu-id="c0787-112">Za pomocą tego nowego mechanizmu może odbywać się w dwóch krokach za kilka minut:</span><span class="sxs-lookup"><span data-stu-id="c0787-112">Using this new mechanism can be done in two steps in a few minutes:</span></span>
1.  <span data-ttu-id="c0787-113">Uzyskaj hello niezbędne informacje z portalu Apple Developer konta hello</span><span class="sxs-lookup"><span data-stu-id="c0787-113">Obtain hello necessary information from hello Apple Developer Account portal</span></span>
2.  <span data-ttu-id="c0787-114">Konfigurowanie Centrum powiadomień przy użyciu nowych informacji hello</span><span class="sxs-lookup"><span data-stu-id="c0787-114">Configure your notification hub with hello new information</span></span>

<span data-ttu-id="c0787-115">Centra powiadomień jest teraz wszystkie zestaw toouse hello nowy system uwierzytelniania przy użyciu usługi APNS.</span><span class="sxs-lookup"><span data-stu-id="c0787-115">Notification Hubs is now all set toouse hello new authentication system with APNS.</span></span> 

<span data-ttu-id="c0787-116">Należy pamiętać, że po migracji z przy użyciu poświadczeń certyfikatu dla usługi APNS:</span><span class="sxs-lookup"><span data-stu-id="c0787-116">Note that if you migrated from using certificate credentials for APNS:</span></span>
- <span data-ttu-id="c0787-117">właściwości tokenu Hello zastąpić certyfikat w naszym systemie</span><span class="sxs-lookup"><span data-stu-id="c0787-117">hello token properties overwrite your certificate in our system,</span></span>
- <span data-ttu-id="c0787-118">ale aplikacji nadal bezproblemowo tooreceive powiadomienia.</span><span class="sxs-lookup"><span data-stu-id="c0787-118">but your application continues tooreceive notifications seamlessly.</span></span>

## <a name="obtaining-authentication-information-from-apple"></a><span data-ttu-id="c0787-119">Uzyskiwanie informacji o uwierzytelnianiu od firmy Apple</span><span class="sxs-lookup"><span data-stu-id="c0787-119">Obtaining authentication information from Apple</span></span>
<span data-ttu-id="c0787-120">uwierzytelniania opartego na tokenach tooenable należy hello następujące właściwości z konta dewelopera firmy Apple:</span><span class="sxs-lookup"><span data-stu-id="c0787-120">tooenable token-based authentication, you need hello following properties from your Apple Developer Account:</span></span>
### <a name="key-identifier"></a><span data-ttu-id="c0787-121">Identyfikator klucza</span><span class="sxs-lookup"><span data-stu-id="c0787-121">Key Identifier</span></span>
<span data-ttu-id="c0787-122">Identyfikator klucza Hello można uzyskać ze strony "Klucze" hello na koncie deweloperów firmy Apple</span><span class="sxs-lookup"><span data-stu-id="c0787-122">hello key identifier can be obtained from hello "Keys" page in your Apple Developer Account</span></span>

![](./media/notification-hubs-push-notification-http2-token-authentification/obtaining-auth-information-from-apple.png)

### <a name="application-identifier--application-name"></a><span data-ttu-id="c0787-123">Identyfikator aplikacji i nazwy aplikacji</span><span class="sxs-lookup"><span data-stu-id="c0787-123">Application Identifier & Application Name</span></span>
<span data-ttu-id="c0787-124">Nazwa aplikacji Hello jest dostępna za pośrednictwem strony identyfikatorów aplikacji hello hello konta dewelopera.</span><span class="sxs-lookup"><span data-stu-id="c0787-124">hello application name is available via hello App IDs page in hello Developer Account.</span></span> 
![](./media/notification-hubs-push-notification-http2-token-authentification/app-name.png)

<span data-ttu-id="c0787-125">Identyfikator aplikacji Hello jest dostępna za pośrednictwem strony szczegółów członkostwa hello hello konta dewelopera.</span><span class="sxs-lookup"><span data-stu-id="c0787-125">hello application identifier is available via hello membership details page in hello Developer Account.</span></span>
![](./media/notification-hubs-push-notification-http2-token-authentification/app-id.png)


### <a name="authentication-token"></a><span data-ttu-id="c0787-126">Token uwierzytelniania</span><span class="sxs-lookup"><span data-stu-id="c0787-126">Authentication token</span></span>
<span data-ttu-id="c0787-127">można pobrać tokenu uwierzytelniania powitania po wygenerowaniu tokenu dla aplikacji.</span><span class="sxs-lookup"><span data-stu-id="c0787-127">hello authentication token can be downloaded after you generate a token for your application.</span></span> <span data-ttu-id="c0787-128">Aby uzyskać szczegółowe informacje o sposobie toogenerate to token, zobacz zbyt[dokumentacja dla deweloperów firmy Apple](http://help.apple.com/xcode/mac/current/#/dev11b059073?sub=dev1eb5dfe65).</span><span class="sxs-lookup"><span data-stu-id="c0787-128">For details on how toogenerate this token, refer too[Apple’s Developer documentation](http://help.apple.com/xcode/mac/current/#/dev11b059073?sub=dev1eb5dfe65).</span></span>

## <a name="configuring-your-notification-hub-toouse-token-based-authentication"></a><span data-ttu-id="c0787-129">Konfigurowanie powiadomień Centrum toouse tokenów uwierzytelniania</span><span class="sxs-lookup"><span data-stu-id="c0787-129">Configuring your notification hub toouse token-based authentication</span></span>
### <a name="configure-via-hello-azure-portal"></a><span data-ttu-id="c0787-130">Konfigurowanie za pomocą hello portalu Azure</span><span class="sxs-lookup"><span data-stu-id="c0787-130">Configure via hello Azure portal</span></span>
<span data-ttu-id="c0787-131">tooenable token na podstawie uwierzytelniania w portalu hello logowania toohello portalu Azure, przejdź tooyour Centrum powiadomień > Usługi powiadomień > APNS panel.</span><span class="sxs-lookup"><span data-stu-id="c0787-131">tooenable token based authentication in hello portal, log in toohello Azure portal and go tooyour Notification Hub > Notification Services > APNS panel.</span></span> 

<span data-ttu-id="c0787-132">Brak nową właściwość — *tryb uwierzytelniania*.</span><span class="sxs-lookup"><span data-stu-id="c0787-132">There is a new property – *Authentication Mode*.</span></span> <span data-ttu-id="c0787-133">Wybranie Token umożliwia tooupdate koncentrator z wszystkie hello odpowiednie właściwości tokenu.</span><span class="sxs-lookup"><span data-stu-id="c0787-133">Selecting Token allows you tooupdate your hub with all hello relevant token properties.</span></span>

![](./media/notification-hubs-push-notification-http2-token-authentification/azure-portal-apns-settings.png)

- <span data-ttu-id="c0787-134">Wprowadź właściwości hello, pobierane z konta dewelopera firmy Apple</span><span class="sxs-lookup"><span data-stu-id="c0787-134">Enter hello properties you retrieved from your Apple developer account,</span></span> 
- <span data-ttu-id="c0787-135">Wybierz tryb aplikacji (środowisko produkcyjne lub piaskownicy)</span><span class="sxs-lookup"><span data-stu-id="c0787-135">choose your application mode (Production or Sandbox)</span></span> 
- <span data-ttu-id="c0787-136">Kliknij przycisk Zapisz tooupdate swoje poświadczenia usługi APNS.</span><span class="sxs-lookup"><span data-stu-id="c0787-136">click Save tooupdate your APNS credentials.</span></span> 

### <a name="configure-via-management-api-rest"></a><span data-ttu-id="c0787-137">Konfigurowanie za pomocą interfejsu API (REST) do zarządzania</span><span class="sxs-lookup"><span data-stu-id="c0787-137">Configure via Management API (REST)</span></span>

<span data-ttu-id="c0787-138">Można użyć naszych [API zarządzania](https://msdn.microsoft.com/library/azure/dn495827.aspx) tooupdate notification hub toouse tokenów uwierzytelniania.</span><span class="sxs-lookup"><span data-stu-id="c0787-138">You can use our [management APIs](https://msdn.microsoft.com/library/azure/dn495827.aspx) tooupdate your notification hub toouse token-based authentication.</span></span>
<span data-ttu-id="c0787-139">W zależności od tego, czy w przypadku konfigurowania aplikacji hello jest piaskownicy lub produkcji aplikacja (określone w danych konta dewelopera Apple) użyj jednej z odpowiednich punktów końcowych hello:</span><span class="sxs-lookup"><span data-stu-id="c0787-139">Depending on whether hello application you’re configuring is a Sandbox or Production app (specified in your Apple Developer Account), use one of hello corresponding endpoints:</span></span>

- <span data-ttu-id="c0787-140">Punkt końcowy piaskownicy: [https://api.development.push.apple.com:443/3/urządzenia](https://api.development.push.apple.com:443/3/device)</span><span class="sxs-lookup"><span data-stu-id="c0787-140">Sandbox Endpoint: [https://api.development.push.apple.com:443/3/device](https://api.development.push.apple.com:443/3/device)</span></span>
- <span data-ttu-id="c0787-141">Punkt końcowy produkcji: [https://api.push.apple.com:443/3/urządzenia](https://api.push.apple.com:443/3/device)</span><span class="sxs-lookup"><span data-stu-id="c0787-141">Production Endpoint: [https://api.push.apple.com:443/3/device](https://api.push.apple.com:443/3/device)</span></span>

> [!IMPORTANT]
> <span data-ttu-id="c0787-142">Uwierzytelnianie na podstawie tokenu wymaga wersji interfejsu API: **2017 04 lub nowszym**.</span><span class="sxs-lookup"><span data-stu-id="c0787-142">Token-based authentication requires an API version of: **2017-04 or later**.</span></span>
> 
> 

<span data-ttu-id="c0787-143">Oto przykład tooupdate żądania PUT Centrum przy użyciu uwierzytelniania opartego na tokenie:</span><span class="sxs-lookup"><span data-stu-id="c0787-143">Here’s an example of a PUT request tooupdate a hub with token-based authentication:</span></span>


        PUT https://{namespace}.servicebus.windows.net/{Notification Hub}?api-version=2017-04
          "Properties": {
            "ApnsCredential": {
              "Properties": {
                "KeyId": "<Your Key Id>",
                "Token": "<Your Authentication Token>",
                "AppName": "<Your Application Name>",
                "AppId": "<Your Application Id>",
                "Endpoint":"<Sandbox/Production Endpoint>"
              }
            }
          }
        

### <a name="configure-via-hello-net-sdk"></a><span data-ttu-id="c0787-144">Konfigurowanie za pomocą hello zestawu .NET SDK</span><span class="sxs-lookup"><span data-stu-id="c0787-144">Configure via hello .NET SDK</span></span>
<span data-ttu-id="c0787-145">Można skonfigurować swoją Centrum toouse uwierzytelniania na podstawie tokenu przy użyciu naszych [najnowszego klienta SDK](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/1.0.8).</span><span class="sxs-lookup"><span data-stu-id="c0787-145">You can configure your hub toouse token based authentication using our [latest client SDK](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/1.0.8).</span></span> 

<span data-ttu-id="c0787-146">Oto przykładowy kod, pokazujący hello poprawne użycie:</span><span class="sxs-lookup"><span data-stu-id="c0787-146">Here’s a code sample illustrating hello correct usage:</span></span>


        NamespaceManager nm = NamespaceManager.CreateFromConnectionString(_endpoint);
        string token = "YOUR TOKEN HERE";
        string keyId = "YOUR KEY ID HERE";
        string appName = "YOUR APP NAME HERE";
        string appId = "YOUR APP ID HERE";
        NotificationHubDescription desc = new NotificationHubDescription("PATH tooYOUR HUB");
        desc.ApnsCredential = new ApnsCredential(token, keyId, appId, appName);
        desc.ApnsCredential.Endpoint = @"https://api.development.push.apple.com:443/3/device";
        nm.UpdateNotificationHubAsync(desc);

## <a name="reverting-toousing-certificate-based-authentication"></a><span data-ttu-id="c0787-147">Trwa przywracanie toousing uwierzytelniania opartego na certyfikatach</span><span class="sxs-lookup"><span data-stu-id="c0787-147">Reverting toousing certificate-based authentication</span></span>
<span data-ttu-id="c0787-148">Możesz przywrócić w żadnego uwierzytelniania opartego na certyfikatach toousing czasu przy użyciu dowolnego poprzedniego certyfikatu hello — metoda i przekazywanie zamiast hello tokenu właściwości.</span><span class="sxs-lookup"><span data-stu-id="c0787-148">You can revert at any time toousing certificate-based authentication by using any preceding method and passing hello certificate instead of hello token properties.</span></span> <span data-ttu-id="c0787-149">Akcja hello spowoduje zastąpienie wcześniej zapisanych poświadczeń.</span><span class="sxs-lookup"><span data-stu-id="c0787-149">That action overwrites hello previously stored credentials.</span></span>
