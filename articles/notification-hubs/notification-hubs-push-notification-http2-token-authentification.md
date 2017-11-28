---
title: "Uwierzytelniania opartego na tokenie (HTTP/2) dla usługi APNS w usłudze Azure Notification Hubs | Dokumentacja firmy Microsoft"
description: "W tym temacie wyjaśniono, jak korzystać z nowego tokenu uwierzytelniania dla usługi APNS"
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
ms.openlocfilehash: 5a21bcd9f12fc3f96b17a556ba15526c35ababe2
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="token-based-http2-authentication-for-apns"></a><span data-ttu-id="df81c-103">Uwierzytelniania opartego na tokenie (HTTP/2) dla usługi APNS</span><span class="sxs-lookup"><span data-stu-id="df81c-103">Token-based (HTTP/2) Authentication for APNS</span></span>
## <a name="overview"></a><span data-ttu-id="df81c-104">Omówienie</span><span class="sxs-lookup"><span data-stu-id="df81c-104">Overview</span></span>
<span data-ttu-id="df81c-105">Ten artykuł zawiera szczegóły dotyczące sposobu zastosowania nowego protokołu APNS HTTP/2 z uwierzytelniania przy użyciu tokenu.</span><span class="sxs-lookup"><span data-stu-id="df81c-105">This article details how to use the new APNS HTTP/2 protocol with token based authentication.</span></span>

<span data-ttu-id="df81c-106">Najważniejsze zalety stosowania nowy protokół obejmują:</span><span class="sxs-lookup"><span data-stu-id="df81c-106">The key benefits of using the new protocol include:</span></span>
-   <span data-ttu-id="df81c-107">Generowania tokenów jest stosunkowo proste wolnego (w porównaniu do certyfikatów)</span><span class="sxs-lookup"><span data-stu-id="df81c-107">Token generation is relatively hassle free (compared to certificates)</span></span>
-   <span data-ttu-id="df81c-108">Nie więcej daty wygaśnięcia — są w formancie tokenów uwierzytelniania i ich odwołań</span><span class="sxs-lookup"><span data-stu-id="df81c-108">No more expiry dates – you are in control of your authentication tokens and their revocation</span></span>
-   <span data-ttu-id="df81c-109">Ładunki można teraz maksymalnie 4 KB</span><span class="sxs-lookup"><span data-stu-id="df81c-109">Payloads can now be up to 4 KB</span></span>
- <span data-ttu-id="df81c-110">Synchroniczne opinii</span><span class="sxs-lookup"><span data-stu-id="df81c-110">Synchronous feedback</span></span>
-   <span data-ttu-id="df81c-111">Możesz teraz najnowsze protokołu firmy Apple — certyfikaty nadal używać protokołu binarny, który jest oznaczony do amortyzacja</span><span class="sxs-lookup"><span data-stu-id="df81c-111">You’re on Apple’s latest protocol – certificates still use the binary protocol, which is marked for deprecation</span></span>

<span data-ttu-id="df81c-112">Za pomocą tego nowego mechanizmu może odbywać się w dwóch krokach za kilka minut:</span><span class="sxs-lookup"><span data-stu-id="df81c-112">Using this new mechanism can be done in two steps in a few minutes:</span></span>
1.  <span data-ttu-id="df81c-113">Uzyskać niezbędne informacje z portalu Apple Developer konta</span><span class="sxs-lookup"><span data-stu-id="df81c-113">Obtain the necessary information from the Apple Developer Account portal</span></span>
2.  <span data-ttu-id="df81c-114">Konfigurowanie Centrum powiadomień przy użyciu nowych informacji</span><span class="sxs-lookup"><span data-stu-id="df81c-114">Configure your notification hub with the new information</span></span>

<span data-ttu-id="df81c-115">Centra powiadomień jest teraz wszystko gotowe do użycia w nowym systemie uwierzytelniania przy użyciu usługi APNS.</span><span class="sxs-lookup"><span data-stu-id="df81c-115">Notification Hubs is now all set to use the new authentication system with APNS.</span></span> 

<span data-ttu-id="df81c-116">Należy pamiętać, że po migracji z przy użyciu poświadczeń certyfikatu dla usługi APNS:</span><span class="sxs-lookup"><span data-stu-id="df81c-116">Note that if you migrated from using certificate credentials for APNS:</span></span>
- <span data-ttu-id="df81c-117">token właściwości zastąpić certyfikat w naszym systemie</span><span class="sxs-lookup"><span data-stu-id="df81c-117">the token properties overwrite your certificate in our system,</span></span>
- <span data-ttu-id="df81c-118">Jednak aplikacja będzie nadal otrzymywał powiadomienia bezproblemowo.</span><span class="sxs-lookup"><span data-stu-id="df81c-118">but your application continues to receive notifications seamlessly.</span></span>

## <a name="obtaining-authentication-information-from-apple"></a><span data-ttu-id="df81c-119">Uzyskiwanie informacji o uwierzytelnianiu od firmy Apple</span><span class="sxs-lookup"><span data-stu-id="df81c-119">Obtaining authentication information from Apple</span></span>
<span data-ttu-id="df81c-120">Aby włączyć uwierzytelnianie tokenów, potrzebne są następujące właściwości z konta dewelopera firmy Apple:</span><span class="sxs-lookup"><span data-stu-id="df81c-120">To enable token-based authentication, you need the following properties from your Apple Developer Account:</span></span>
### <a name="key-identifier"></a><span data-ttu-id="df81c-121">Identyfikator klucza</span><span class="sxs-lookup"><span data-stu-id="df81c-121">Key Identifier</span></span>
<span data-ttu-id="df81c-122">Identyfikator klucza można uzyskać ze strony "Klucze" na koncie deweloperów firmy Apple</span><span class="sxs-lookup"><span data-stu-id="df81c-122">The key identifier can be obtained from the "Keys" page in your Apple Developer Account</span></span>

![](./media/notification-hubs-push-notification-http2-token-authentification/obtaining-auth-information-from-apple.png)

### <a name="application-identifier--application-name"></a><span data-ttu-id="df81c-123">Identyfikator aplikacji i nazwy aplikacji</span><span class="sxs-lookup"><span data-stu-id="df81c-123">Application Identifier & Application Name</span></span>
<span data-ttu-id="df81c-124">Nazwa aplikacji jest dostępna za pośrednictwem strony identyfikatorów aplikacji w ramach konta dewelopera.</span><span class="sxs-lookup"><span data-stu-id="df81c-124">The application name is available via the App IDs page in the Developer Account.</span></span> 
![](./media/notification-hubs-push-notification-http2-token-authentification/app-name.png)

<span data-ttu-id="df81c-125">Identyfikator aplikacji jest dostępna za pośrednictwem strony szczegółów członkostwa w konta dewelopera.</span><span class="sxs-lookup"><span data-stu-id="df81c-125">The application identifier is available via the membership details page in the Developer Account.</span></span>
![](./media/notification-hubs-push-notification-http2-token-authentification/app-id.png)


### <a name="authentication-token"></a><span data-ttu-id="df81c-126">Token uwierzytelniania</span><span class="sxs-lookup"><span data-stu-id="df81c-126">Authentication token</span></span>
<span data-ttu-id="df81c-127">Po wygenerowaniu tokenu dla aplikacji można pobrać tokenu uwierzytelniania.</span><span class="sxs-lookup"><span data-stu-id="df81c-127">The authentication token can be downloaded after you generate a token for your application.</span></span> <span data-ttu-id="df81c-128">Aby uzyskać więcej informacji na temat generowania tokenu, zapoznaj się [dokumentacja dla deweloperów firmy Apple](http://help.apple.com/xcode/mac/current/#/dev11b059073?sub=dev1eb5dfe65).</span><span class="sxs-lookup"><span data-stu-id="df81c-128">For details on how to generate this token, refer to [Apple’s Developer documentation](http://help.apple.com/xcode/mac/current/#/dev11b059073?sub=dev1eb5dfe65).</span></span>

## <a name="configuring-your-notification-hub-to-use-token-based-authentication"></a><span data-ttu-id="df81c-129">Konfigurowanie Centrum powiadomień do uwierzytelniania opartego na tokenach</span><span class="sxs-lookup"><span data-stu-id="df81c-129">Configuring your notification hub to use token-based authentication</span></span>
### <a name="configure-via-the-azure-portal"></a><span data-ttu-id="df81c-130">Konfigurowanie portalu Azure</span><span class="sxs-lookup"><span data-stu-id="df81c-130">Configure via the Azure portal</span></span>
<span data-ttu-id="df81c-131">Aby włączyć token uwierzytelniania przy użyciu w portalu, należy zalogować się do portalu Azure i przejdź do Centrum powiadomień > Usługi powiadomień > APNS panel.</span><span class="sxs-lookup"><span data-stu-id="df81c-131">To enable token based authentication in the portal, log in to the Azure portal and go to your Notification Hub > Notification Services > APNS panel.</span></span> 

<span data-ttu-id="df81c-132">Brak nową właściwość — *tryb uwierzytelniania*.</span><span class="sxs-lookup"><span data-stu-id="df81c-132">There is a new property – *Authentication Mode*.</span></span> <span data-ttu-id="df81c-133">Wybieranie Token umożliwia zaktualizowanie koncentrator z odpowiednimi tokenu właściwości.</span><span class="sxs-lookup"><span data-stu-id="df81c-133">Selecting Token allows you to update your hub with all the relevant token properties.</span></span>

![](./media/notification-hubs-push-notification-http2-token-authentification/azure-portal-apns-settings.png)

- <span data-ttu-id="df81c-134">Wprowadź właściwości, które są pobierane z konta dewelopera firmy Apple</span><span class="sxs-lookup"><span data-stu-id="df81c-134">Enter the properties you retrieved from your Apple developer account,</span></span> 
- <span data-ttu-id="df81c-135">Wybierz tryb aplikacji (środowisko produkcyjne lub piaskownicy)</span><span class="sxs-lookup"><span data-stu-id="df81c-135">choose your application mode (Production or Sandbox)</span></span> 
- <span data-ttu-id="df81c-136">Kliknij przycisk Zapisz, aby zaktualizować swoje poświadczenia usługi APNS.</span><span class="sxs-lookup"><span data-stu-id="df81c-136">click Save to update your APNS credentials.</span></span> 

### <a name="configure-via-management-api-rest"></a><span data-ttu-id="df81c-137">Konfigurowanie za pomocą interfejsu API (REST) do zarządzania</span><span class="sxs-lookup"><span data-stu-id="df81c-137">Configure via Management API (REST)</span></span>

<span data-ttu-id="df81c-138">Można użyć naszych [API zarządzania](https://msdn.microsoft.com/library/azure/dn495827.aspx) Aby zaktualizować Centrum powiadomień do uwierzytelniania opartego na tokenie.</span><span class="sxs-lookup"><span data-stu-id="df81c-138">You can use our [management APIs](https://msdn.microsoft.com/library/azure/dn495827.aspx) to update your notification hub to use token-based authentication.</span></span>
<span data-ttu-id="df81c-139">W zależności od tego, czy w przypadku konfigurowania aplikacji jest aplikacja piaskownicy lub produkcji (określone w danych konta dewelopera Apple) użyj jednej z odpowiednich punktów końcowych:</span><span class="sxs-lookup"><span data-stu-id="df81c-139">Depending on whether the application you’re configuring is a Sandbox or Production app (specified in your Apple Developer Account), use one of the corresponding endpoints:</span></span>

- <span data-ttu-id="df81c-140">Punkt końcowy piaskownicy: [https://api.development.push.apple.com:443/3/urządzenia](https://api.development.push.apple.com:443/3/device)</span><span class="sxs-lookup"><span data-stu-id="df81c-140">Sandbox Endpoint: [https://api.development.push.apple.com:443/3/device](https://api.development.push.apple.com:443/3/device)</span></span>
- <span data-ttu-id="df81c-141">Punkt końcowy produkcji: [https://api.push.apple.com:443/3/urządzenia](https://api.push.apple.com:443/3/device)</span><span class="sxs-lookup"><span data-stu-id="df81c-141">Production Endpoint: [https://api.push.apple.com:443/3/device](https://api.push.apple.com:443/3/device)</span></span>

> [!IMPORTANT]
> <span data-ttu-id="df81c-142">Uwierzytelnianie na podstawie tokenu wymaga wersji interfejsu API: **2017 04 lub nowszym**.</span><span class="sxs-lookup"><span data-stu-id="df81c-142">Token-based authentication requires an API version of: **2017-04 or later**.</span></span>
> 
> 

<span data-ttu-id="df81c-143">Oto przykład żądanie PUT, aby zaktualizować Centrum przy użyciu uwierzytelniania opartego na tokenie:</span><span class="sxs-lookup"><span data-stu-id="df81c-143">Here’s an example of a PUT request to update a hub with token-based authentication:</span></span>


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
        

### <a name="configure-via-the-net-sdk"></a><span data-ttu-id="df81c-144">Konfigurowanie za pomocą zestawu .NET SDK</span><span class="sxs-lookup"><span data-stu-id="df81c-144">Configure via the .NET SDK</span></span>
<span data-ttu-id="df81c-145">Można skonfigurować do używania uwierzytelniania na podstawie tokenu przy użyciu Centrum naszych [najnowszego klienta SDK](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/1.0.8).</span><span class="sxs-lookup"><span data-stu-id="df81c-145">You can configure your hub to use token based authentication using our [latest client SDK](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/1.0.8).</span></span> 

<span data-ttu-id="df81c-146">Oto przykładowy kod, pokazujący poprawne użycie:</span><span class="sxs-lookup"><span data-stu-id="df81c-146">Here’s a code sample illustrating the correct usage:</span></span>


        NamespaceManager nm = NamespaceManager.CreateFromConnectionString(_endpoint);
        string token = "YOUR TOKEN HERE";
        string keyId = "YOUR KEY ID HERE";
        string appName = "YOUR APP NAME HERE";
        string appId = "YOUR APP ID HERE";
        NotificationHubDescription desc = new NotificationHubDescription("PATH TO YOUR HUB");
        desc.ApnsCredential = new ApnsCredential(token, keyId, appId, appName);
        desc.ApnsCredential.Endpoint = @"https://api.development.push.apple.com:443/3/device";
        nm.UpdateNotificationHubAsync(desc);

## <a name="reverting-to-using-certificate-based-authentication"></a><span data-ttu-id="df81c-147">Powrót do przy użyciu uwierzytelniania opartego na certyfikatach</span><span class="sxs-lookup"><span data-stu-id="df81c-147">Reverting to using certificate-based authentication</span></span>
<span data-ttu-id="df81c-148">Możesz przywrócić w dowolnym momencie przy użyciu uwierzytelniania opartego na certyfikatach przy użyciu dowolnej metody poprzedniego i przekazywanie certyfikatu zamiast tokenu właściwości.</span><span class="sxs-lookup"><span data-stu-id="df81c-148">You can revert at any time to using certificate-based authentication by using any preceding method and passing the certificate instead of the token properties.</span></span> <span data-ttu-id="df81c-149">Ta akcja spowoduje zastąpienie wcześniej zapisane poświadczenia.</span><span class="sxs-lookup"><span data-stu-id="df81c-149">That action overwrites the previously stored credentials.</span></span>
