---
title: "aaaUse tooaccess uwierzytelniania usługi Azure AD Azure Media Services API z platformą .NET | Dokumentacja firmy Microsoft"
description: "W tym temacie pokazano, jak toouse tooaccess uwierzytelniania usługi Azure Active Directory (Azure AD) usługi Azure Media Services (AMS) interfejsu API za pomocą platformy .NET."
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/17/2017
ms.author: juliako
ms.openlocfilehash: 2f750e460d9e476ad92e96adeac6500cb692cd77
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-ad-authentication-tooaccess-azure-media-services-api-with-net"></a><span data-ttu-id="b6eca-103">Użyj usługi Azure AD authentication tooaccess interfejsu API usługi Azure Media Services z platformą .NET</span><span class="sxs-lookup"><span data-stu-id="b6eca-103">Use Azure AD authentication tooaccess Azure Media Services API with .NET</span></span>

<span data-ttu-id="b6eca-104">Począwszy od windowsazure.mediaservices 4.0.0.4 Azure Media Services obsługuje uwierzytelnianie oparte na usłudze Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="b6eca-104">Starting with windowsazure.mediaservices 4.0.0.4, Azure Media Services supports authentication based on Azure Active Directory (Azure AD).</span></span> <span data-ttu-id="b6eca-105">W tym temacie opisano sposób toouse tooaccess uwierzytelniania usługi Azure AD interfejsu API usługi multimediów Azure za pomocą programu Microsoft .NET.</span><span class="sxs-lookup"><span data-stu-id="b6eca-105">This topic shows you how toouse Azure AD  authentication tooaccess Azure Media Services API with Microsoft .NET.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b6eca-106">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="b6eca-106">Prerequisites</span></span>

- <span data-ttu-id="b6eca-107">Konto platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="b6eca-107">An Azure account.</span></span> <span data-ttu-id="b6eca-108">Aby uzyskać szczegółowe informacje, zobacz [Bezpłatna wersja próbna systemu Azure](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="b6eca-108">For details, see [Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span> 
- <span data-ttu-id="b6eca-109">Konto usługi Media Services.</span><span class="sxs-lookup"><span data-stu-id="b6eca-109">A Media Services account.</span></span> <span data-ttu-id="b6eca-110">Aby uzyskać więcej informacji, zobacz [Tworzenie konta usługi Azure Media Services przy użyciu portalu Azure hello](media-services-portal-create-account.md).</span><span class="sxs-lookup"><span data-stu-id="b6eca-110">For more information, see [Create an Azure Media Services account using hello Azure portal](media-services-portal-create-account.md).</span></span>
- <span data-ttu-id="b6eca-111">Witaj najnowszych [NuGet](https://www.nuget.org/packages/windowsazure.mediaservices) pakietu.</span><span class="sxs-lookup"><span data-stu-id="b6eca-111">hello latest [NuGet](https://www.nuget.org/packages/windowsazure.mediaservices) package.</span></span>
- <span data-ttu-id="b6eca-112">Znajomość tematu hello [podczas uzyskiwania dostępu do usługi Azure Media usług interfejsu API za pomocą omówienie uwierzytelniania usługi AAD](media-services-use-aad-auth-to-access-ams-api.md).</span><span class="sxs-lookup"><span data-stu-id="b6eca-112">Familiarity with hello topic [Accessing Azure Media Services API with AAD authentication overview](media-services-use-aad-auth-to-access-ams-api.md).</span></span> 

<span data-ttu-id="b6eca-113">Podczas korzystania z uwierzytelniania usługi Azure AD z usługi Azure Media Services, można uwierzytelniać się w jednym z dwóch sposobów:</span><span class="sxs-lookup"><span data-stu-id="b6eca-113">When you're using Azure AD authentication with Azure Media Services, you can authenticate in one of two ways:</span></span>

- <span data-ttu-id="b6eca-114">**Uwierzytelnianie użytkownika** uwierzytelnia osoby, która używa toointeract aplikacji hello z zasobami usługi Azure Media Services.</span><span class="sxs-lookup"><span data-stu-id="b6eca-114">**User authentication** authenticates a person who is using hello app toointeract with Azure Media Services resources.</span></span> <span data-ttu-id="b6eca-115">Interaktywna aplikacja Hello należy najpierw monitują hello poświadczenia użytkownika.</span><span class="sxs-lookup"><span data-stu-id="b6eca-115">hello interactive application should first prompt hello user for credentials.</span></span> <span data-ttu-id="b6eca-116">Przykładem jest aplikacja konsoli zarządzania, który jest używany przez autoryzowanych użytkowników toomonitor kodowania zadań lub transmisja strumieniowa na żywo.</span><span class="sxs-lookup"><span data-stu-id="b6eca-116">An example is a management console app that's used by authorized users toomonitor encoding jobs or live streaming.</span></span> 
- <span data-ttu-id="b6eca-117">**Uwierzytelnianie głównej usługi** uwierzytelnia usługi.</span><span class="sxs-lookup"><span data-stu-id="b6eca-117">**Service principal authentication** authenticates a service.</span></span> <span data-ttu-id="b6eca-118">Aplikacje, które zazwyczaj używają tej metody uwierzytelniania są aplikacji uruchamianych demon usługi, usługi warstwy środkowej lub zaplanowanych zadań, takich jak aplikacje sieci web funkcji aplikacji, aplikacji logiki, interfejsów API albo mikrousług.</span><span class="sxs-lookup"><span data-stu-id="b6eca-118">Applications that commonly use this authentication method are apps that run daemon services, middle-tier services, or scheduled jobs, such as web apps, function apps, logic apps, APIs, or microservices.</span></span>

>[!IMPORTANT]
><span data-ttu-id="b6eca-119">Usługa Azure Media obecnie obsługuje model uwierzytelniania w usłudze kontroli dostępu platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="b6eca-119">Azure Media Service currently supports an Azure Access Control Service  authentication model.</span></span> <span data-ttu-id="b6eca-120">Kontrola dostępu autoryzacji będzie jednak toobe przestarzałe na 1 czerwca 2018.</span><span class="sxs-lookup"><span data-stu-id="b6eca-120">However, Access Control authorization is going toobe deprecated on June 1, 2018.</span></span> <span data-ttu-id="b6eca-121">Firma Microsoft zaleca migracji model uwierzytelniania usługi Azure Active Directory tooan tak szybko, jak to możliwe.</span><span class="sxs-lookup"><span data-stu-id="b6eca-121">We recommend that you migrate tooan Azure Active Directory authentication model as soon as possible.</span></span>

## <a name="get-an-azure-ad-access-token"></a><span data-ttu-id="b6eca-122">Uzyskaj token dostępu usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="b6eca-122">Get an Azure AD access token</span></span>

<span data-ttu-id="b6eca-123">tooconnect toohello interfejsu API usługi Azure Media Services przy użyciu uwierzytelniania usługi Azure AD, powitania klienta aplikacji musi toorequest token dostępu usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="b6eca-123">tooconnect toohello Azure Media Services API with Azure AD authentication, hello client app needs toorequest an Azure AD access token.</span></span> <span data-ttu-id="b6eca-124">Jeśli używasz powitania klienta Media Services na platformie .NET SDK, wiele hello szczegóły dotyczące sposobu opakowana i uproszczone dla Ciebie w hello tooacquire token dostępu usługi Azure AD [AzureAdTokenProvider](https://github.com/Azure/azure-sdk-for-media-services/blob/dev/src/net/Client/Common/Common.Authentication/AzureAdTokenProvider.cs) i [AzureAdTokenCredentials ](https://github.com/Azure/azure-sdk-for-media-services/blob/dev/src/net/Client/Common/Common.Authentication/AzureAdTokenCredentials.cs) klasy.</span><span class="sxs-lookup"><span data-stu-id="b6eca-124">When you use hello Media Services .NET client SDK, many of hello details about how tooacquire an Azure AD access token are wrapped and simplified for you in hello [AzureAdTokenProvider](https://github.com/Azure/azure-sdk-for-media-services/blob/dev/src/net/Client/Common/Common.Authentication/AzureAdTokenProvider.cs) and [AzureAdTokenCredentials](https://github.com/Azure/azure-sdk-for-media-services/blob/dev/src/net/Client/Common/Common.Authentication/AzureAdTokenCredentials.cs) classes.</span></span> 

<span data-ttu-id="b6eca-125">Na przykład, nie potrzebujesz tooprovide urzędu hello Azure AD, identyfikator URI zasobu usługi Media Services lub native szczegóły aplikacji usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="b6eca-125">For example, you don't need tooprovide hello Azure AD authority, Media Services resource URI, or native Azure AD application details.</span></span> <span data-ttu-id="b6eca-126">Są to dobrze znane wartości, które są już skonfigurowane przez hello klasa dostawcy tokenu dostępu usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="b6eca-126">These are well-known values that are already configured by hello Azure AD access token provider class.</span></span> 

<span data-ttu-id="b6eca-127">Jeśli nie używasz zestawu .NET SDK usługi Azure Media Service, zalecane jest użycie hello [Azure AD Authentication Library](../active-directory/develop/active-directory-authentication-libraries.md).</span><span class="sxs-lookup"><span data-stu-id="b6eca-127">If you are not using Azure Media Service .NET SDK, we recommend that you use hello [Azure AD Authentication Library](../active-directory/develop/active-directory-authentication-libraries.md).</span></span> <span data-ttu-id="b6eca-128">Zobacz tooget wartości parametrów hello konieczność toouse z usługi Azure AD Authentication Library [za pomocą ustawień uwierzytelniania Azure tooaccess portalu usługi Azure AD hello](media-services-portal-get-started-with-aad.md).</span><span class="sxs-lookup"><span data-stu-id="b6eca-128">tooget values for hello parameters that you need toouse with Azure AD Authentication Library, see [Use hello Azure portal tooaccess Azure AD authentication settings](media-services-portal-get-started-with-aad.md).</span></span>

<span data-ttu-id="b6eca-129">Istnieje również możliwość zastąpienia hello domyślną implementację hello hello **AzureAdTokenProvider** z własną implementację.</span><span class="sxs-lookup"><span data-stu-id="b6eca-129">You also have hello option of replacing hello default implementation of hello **AzureAdTokenProvider** with your own implementation.</span></span>

## <a name="install-and-configure-azure-media-services-net-sdk"></a><span data-ttu-id="b6eca-130">Instalowanie i konfigurowanie zestawu .NET SDK usługi Azure Media Services</span><span class="sxs-lookup"><span data-stu-id="b6eca-130">Install and configure Azure Media Services .NET SDK</span></span>

>[!NOTE] 
><span data-ttu-id="b6eca-131">Uwierzytelnianie toouse usługi Azure AD z hello .NET SDK usługi Media Services, potrzebne toohave hello najnowszych [NuGet](https://www.nuget.org/packages/windowsazure.mediaservices) pakietu.</span><span class="sxs-lookup"><span data-stu-id="b6eca-131">toouse Azure AD authentication with hello Media Services .NET SDK, you need toohave hello latest [NuGet](https://www.nuget.org/packages/windowsazure.mediaservices) package.</span></span> <span data-ttu-id="b6eca-132">Ponadto Dodaj toohello odwołanie **Microsoft.IdentityModel.Clients.ActiveDirectory** zestawu.</span><span class="sxs-lookup"><span data-stu-id="b6eca-132">Also, add a reference toohello **Microsoft.IdentityModel.Clients.ActiveDirectory** assembly.</span></span> <span data-ttu-id="b6eca-133">Jeśli korzystasz z istniejącej aplikacji, należy uwzględnić hello **Microsoft.WindowsAzure.MediaServices.Client.Common.Authentication.dll** zestawu.</span><span class="sxs-lookup"><span data-stu-id="b6eca-133">If you are using an existing app, include hello **Microsoft.WindowsAzure.MediaServices.Client.Common.Authentication.dll** assembly.</span></span> 

1. <span data-ttu-id="b6eca-134">Utwórz nową aplikację konsoli języka C# w programie Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="b6eca-134">Create a new C# console application in Visual Studio.</span></span>
2. <span data-ttu-id="b6eca-135">Użyj hello [windowsazure.mediaservices](https://www.nuget.org/packages/windowsazure.mediaservices) tooinstall pakietu NuGet **zestawu .NET SDK usługi Azure Media Services**.</span><span class="sxs-lookup"><span data-stu-id="b6eca-135">Use hello [windowsazure.mediaservices](https://www.nuget.org/packages/windowsazure.mediaservices) NuGet package tooinstall **Azure Media Services .NET SDK**.</span></span> 

    <span data-ttu-id="b6eca-136">tooadd odwołania przy użyciu narzędzia NuGet zająć hello następujące kroki: w **Eksploratora rozwiązań**, kliknij prawym przyciskiem myszy nazwę projektu hello, a następnie wybierz **pakiety zarządzania pakietami NuGet**.</span><span class="sxs-lookup"><span data-stu-id="b6eca-136">tooadd references by using NuGet, take hello following steps: in **Solution Explorer**, right-click hello project name, and then select **Manage NuGet packages**.</span></span> <span data-ttu-id="b6eca-137">Następnie wyszukaj **windowsazure.mediaservices** i wybierz **zainstalować**.</span><span class="sxs-lookup"><span data-stu-id="b6eca-137">Then, search for **windowsazure.mediaservices** and select **Install**.</span></span>
    
    <span data-ttu-id="b6eca-138">— lub —</span><span class="sxs-lookup"><span data-stu-id="b6eca-138">-or-</span></span>

    <span data-ttu-id="b6eca-139">Uruchom hello następujące polecenie w **Konsola Menedżera pakietów** w programie Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="b6eca-139">Run hello following command in **Package Manager Console** in Visual Studio.</span></span>

        Install-Package windowsazure.mediaservices -Version 4.0.0.4

3. <span data-ttu-id="b6eca-140">Dodaj **przy użyciu** tooyour kodu źródłowego.</span><span class="sxs-lookup"><span data-stu-id="b6eca-140">Add **using** tooyour source code.</span></span>

        using Microsoft.WindowsAzure.MediaServices.Client; 

## <a name="use-user-authentication"></a><span data-ttu-id="b6eca-141">Uwierzytelnianie użytkownika</span><span class="sxs-lookup"><span data-stu-id="b6eca-141">Use user authentication</span></span>

<span data-ttu-id="b6eca-142">tooconnect toohello interfejsu API usługi Azure Media Service z włączoną opcją uwierzytelnienia użytkownika hello, powitania klienta aplikacji musi toorequest hello tokenu usługi Azure AD przy użyciu następujących parametrów:</span><span class="sxs-lookup"><span data-stu-id="b6eca-142">tooconnect toohello Azure Media Service API with hello user authentication option, hello client app needs toorequest an Azure AD token by using hello following parameters:</span></span>  

- <span data-ttu-id="b6eca-143">Punkt końcowy dzierżawy usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="b6eca-143">Azure AD tenant endpoint.</span></span> <span data-ttu-id="b6eca-144">Witaj dzierżawy informacje mogą zostać pobrane z hello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="b6eca-144">hello tenant information can be retrieved from hello Azure portal.</span></span> <span data-ttu-id="b6eca-145">Umieść kursor nad hello zalogowanego użytkownika w prawym górnym rogu hello.</span><span class="sxs-lookup"><span data-stu-id="b6eca-145">Hover over hello signed-in user in hello upper-right corner.</span></span>
- <span data-ttu-id="b6eca-146">Identyfikator URI zasobu usługi Media Services.</span><span class="sxs-lookup"><span data-stu-id="b6eca-146">Media Services resource URI.</span></span>
- <span data-ttu-id="b6eca-147">Identyfikator klienta aplikacji usługi Media Services (macierzysty).</span><span class="sxs-lookup"><span data-stu-id="b6eca-147">Media Services (native) application client ID.</span></span> 
- <span data-ttu-id="b6eca-148">Identyfikator URI przekierowania aplikacji usługi Media Services (macierzysty).</span><span class="sxs-lookup"><span data-stu-id="b6eca-148">Media Services (native) application redirect URI.</span></span> 

<span data-ttu-id="b6eca-149">Witaj wartości tych parametrów można znaleźć w **AzureEnvironments.AzureCloudEnvironment**.</span><span class="sxs-lookup"><span data-stu-id="b6eca-149">hello values for these parameters can be found in **AzureEnvironments.AzureCloudEnvironment**.</span></span> <span data-ttu-id="b6eca-150">Witaj **AzureEnvironments.AzureCloudEnvironment** stała pomocnika w tooget zestawu .NET SDK hello jest hello prawo ustawienia zmiennej środowiskowej publicznego Centrum danych Azure.</span><span class="sxs-lookup"><span data-stu-id="b6eca-150">hello **AzureEnvironments.AzureCloudEnvironment** constant is a helper in hello .NET SDK tooget hello right environment variable settings for a public Azure Data Center.</span></span> 

<span data-ttu-id="b6eca-151">Zawiera ustawienia środowiska wstępnie zdefiniowane do uzyskiwania dostępu do usługi Media Services w wyłącznie w centrach danych publicznych hello.</span><span class="sxs-lookup"><span data-stu-id="b6eca-151">It contains pre-defined environment settings for accessing Media Services in hello public data centers only.</span></span> <span data-ttu-id="b6eca-152">W przypadku regionów chmury suwerenne lub dla instytucji rządowych, można użyć **AzureChinaCloudEnvironment**, **AzureUsGovernmentEnvrionment**, lub **AzureGermanCloudEnvironment** odpowiednio.</span><span class="sxs-lookup"><span data-stu-id="b6eca-152">For sovereign or government cloud regions, you can use **AzureChinaCloudEnvironment**, **AzureUsGovernmentEnvrionment**, or **AzureGermanCloudEnvironment** respectively.</span></span>

<span data-ttu-id="b6eca-153">Witaj poniższy przykład kodu tworzy token:</span><span class="sxs-lookup"><span data-stu-id="b6eca-153">hello following code example creates a token:</span></span>
    
    var tokenCredentials = new AzureAdTokenCredentials("microsoft.onmicrosoft.com", AzureEnvironments.AzureCloudEnvironment);
    var tokenProvider = new AzureAdTokenProvider(tokenCredentials);
  
<span data-ttu-id="b6eca-154">toostart Programowanie w odniesieniu do usługi Media Services, potrzebne toocreate **CloudMediaContext** wystąpienie reprezentującego hello kontekstu serwera.</span><span class="sxs-lookup"><span data-stu-id="b6eca-154">toostart programming against Media Services, you need toocreate a **CloudMediaContext** instance that represents hello server context.</span></span> <span data-ttu-id="b6eca-155">Witaj **CloudMediaContext** zawiera odwołania do kolekcji tooimportant tym zadań, zasobów, plików, zasady dostępu i lokalizatorów.</span><span class="sxs-lookup"><span data-stu-id="b6eca-155">hello **CloudMediaContext** includes references tooimportant collections including jobs, assets, files, access policies, and locators.</span></span> 

<span data-ttu-id="b6eca-156">Należy również toopass hello **identyfikator URI dla usługi REST nośnika** toohello **CloudMediaContext** konstruktora.</span><span class="sxs-lookup"><span data-stu-id="b6eca-156">You also need toopass hello **resource URI for Media REST Services** toohello **CloudMediaContext** constructor.</span></span> <span data-ttu-id="b6eca-157">Identyfikator URI zasobu hello tooget dla usługi REST Media Services, logowanie toohello portalu Azure, wybierz konto usługi Azure Media Services, wybierz **dostępu do interfejsu API**, a następnie wybierz **połączyć z użytkownikiem tooAzure Media Services uwierzytelnianie**.</span><span class="sxs-lookup"><span data-stu-id="b6eca-157">tooget hello resource URI for Media REST Services, sign in toohello Azure portal, select your Azure Media Services account, select **API access**, and then select **Connect tooAzure Media Services with user authentication**.</span></span> 

<span data-ttu-id="b6eca-158">Witaj Poniższy przykładowy kod tworzy **CloudMediaContext** wystąpienie:</span><span class="sxs-lookup"><span data-stu-id="b6eca-158">hello following code example creates a **CloudMediaContext** instance:</span></span>

    CloudMediaContext context = new CloudMediaContext(new Uri("YOUR REST API ENDPOINT HERE"), tokenProvider);

<span data-ttu-id="b6eca-159">Witaj poniższy przykład pokazuje, jak toocreate hello kontekstu token i hello Azure AD:</span><span class="sxs-lookup"><span data-stu-id="b6eca-159">hello following example shows how toocreate hello Azure AD token and hello context:</span></span>

    namespace AADAuthSample
    {
        class Program
        {
            static void Main(string[] args)
            {
                // Specify your Azure AD tenant domain, for example "microsoft.onmicrosoft.com".
                var tokenCredentials = new AzureAdTokenCredentials("{YOUR AAD TENANT DOMAIN HERE}", AzureEnvironments.AzureCloudEnvironment);
    
                var tokenProvider = new AzureAdTokenProvider(tokenCredentials);
    
                // Specify your REST API endpoint, for example "https://accountname.restv2.westcentralus.media.azure.net/API".
                CloudMediaContext context = new CloudMediaContext(new Uri("YOUR REST API ENDPOINT HERE"), tokenProvider);
    
                var assets = context.Assets;
                foreach (var a in assets)
                {
                    Console.WriteLine(a.Name);
                }
            }
    
        }
    }

>[!NOTE]
><span data-ttu-id="b6eca-160">Jeśli otrzymasz wyjątek mówi "hello serwer zdalny zwrócił błąd: (401) nieautoryzowane" Zobacz hello [kontrola dostępu](media-services-use-aad-auth-to-access-ams-api.md#access-control) części podczas uzyskiwania dostępu do Azure Media Services API, omówienie uwierzytelniania usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="b6eca-160">If you get an exception that says "hello remote server returned an error: (401) Unauthorized," see hello [Access control](media-services-use-aad-auth-to-access-ams-api.md#access-control) section of Accessing Azure Media Services API with Azure AD authentication overview.</span></span>

## <a name="use-service-principal-authentication"></a><span data-ttu-id="b6eca-161">Użyj uwierzytelniania głównej usługi</span><span class="sxs-lookup"><span data-stu-id="b6eca-161">Use service principal authentication</span></span>
    
<span data-ttu-id="b6eca-162">tooconnect toohello interfejsu API usługi Azure Media Services z opcją główna usługi hello, Twoja aplikacja warstwy środkowej (interfejs API sieci web lub aplikacji sieci web) powinna toorequests tokenu usługi Azure AD z hello następujące parametry:</span><span class="sxs-lookup"><span data-stu-id="b6eca-162">tooconnect toohello Azure Media Services API with hello service principal option, your middle-tier app (web API or web application) needs toorequests an Azure AD token with hello following parameters:</span></span>  

- <span data-ttu-id="b6eca-163">Punkt końcowy dzierżawy usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="b6eca-163">Azure AD tenant endpoint.</span></span> <span data-ttu-id="b6eca-164">Witaj dzierżawy informacje mogą zostać pobrane z hello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="b6eca-164">hello tenant information can be retrieved from hello Azure portal.</span></span> <span data-ttu-id="b6eca-165">Umieść kursor nad hello zalogowanego użytkownika w prawym górnym rogu hello.</span><span class="sxs-lookup"><span data-stu-id="b6eca-165">Hover over hello signed-in user in hello upper-right corner.</span></span>
- <span data-ttu-id="b6eca-166">Identyfikator URI zasobu usługi Media Services.</span><span class="sxs-lookup"><span data-stu-id="b6eca-166">Media Services resource URI.</span></span>
- <span data-ttu-id="b6eca-167">Wartości aplikacji w usłudze Azure AD: hello **identyfikator klienta** i **klucz tajny klienta**.</span><span class="sxs-lookup"><span data-stu-id="b6eca-167">Azure AD application values: hello **Client ID** and **Client secret**.</span></span>

<span data-ttu-id="b6eca-168">Witaj wartości hello **identyfikator klienta** i **klucz tajny klienta** parametrów można znaleźć w portalu Azure hello.</span><span class="sxs-lookup"><span data-stu-id="b6eca-168">hello values for hello **Client ID** and **Client secret** parameters can be found in hello Azure portal.</span></span> <span data-ttu-id="b6eca-169">Aby uzyskać więcej informacji, zobacz [wprowadzenie do korzystania z usługi Azure AD uwierzytelnianie przy użyciu hello portalu Azure](media-services-portal-get-started-with-aad.md).</span><span class="sxs-lookup"><span data-stu-id="b6eca-169">For more information, see [Getting started with Azure AD authentication using hello Azure portal](media-services-portal-get-started-with-aad.md).</span></span>

<span data-ttu-id="b6eca-170">Witaj poniższy przykład kodu tworzy token przy użyciu hello **AzureAdTokenCredentials** konstruktora przyjmującego **AzureAdClientSymmetricKey** jako parametr:</span><span class="sxs-lookup"><span data-stu-id="b6eca-170">hello following code example creates a token by using hello **AzureAdTokenCredentials** constructor that takes **AzureAdClientSymmetricKey** as a parameter:</span></span> 
    
    var tokenCredentials = new AzureAdTokenCredentials("{YOUR Azure AD TENANT DOMAIN HERE}", 
                                new AzureAdClientSymmetricKey("{YOUR CLIENT ID HERE}", "{YOUR CLIENT SECRET}"), 
                                AzureEnvironments.AzureCloudEnvironment);

    var tokenProvider = new AzureAdTokenProvider(tokenCredentials);

<span data-ttu-id="b6eca-171">Można również określić hello **AzureAdTokenCredentials** konstruktora przyjmującego **AzureAdClientCertificate** jako parametr.</span><span class="sxs-lookup"><span data-stu-id="b6eca-171">You can also specify hello **AzureAdTokenCredentials** constructor that takes **AzureAdClientCertificate** as a parameter.</span></span> 

<span data-ttu-id="b6eca-172">Aby uzyskać instrukcje dotyczące toocreate i skonfigurować certyfikat w formularzu, które mogą być używane przez usługę Azure AD, zobacz [tooAzure AD w aplikacjach demon z certyfikatami - ręcznego konfigurowania uwierzytelniania](https://github.com/Azure-Samples/active-directory-dotnet-daemon-certificate-credential/blob/master/Manual-Configuration-Steps.md).</span><span class="sxs-lookup"><span data-stu-id="b6eca-172">For instructions about how toocreate and configure a certificate in a form that can be used by Azure AD, see [Authenticating tooAzure AD in daemon apps with certificates - manual configuration steps](https://github.com/Azure-Samples/active-directory-dotnet-daemon-certificate-credential/blob/master/Manual-Configuration-Steps.md).</span></span>

    var tokenCredentials = new AzureAdTokenCredentials("{YOUR Azure AD TENANT DOMAIN HERE}", 
                                new AzureAdClientCertificate("{YOUR CLIENT ID HERE}", "{YOUR CLIENT CERTIFICATE THUMBPRINT}"), 
                                AzureEnvironments.AzureCloudEnvironment);

<span data-ttu-id="b6eca-173">toostart Programowanie w odniesieniu do usługi Media Services, potrzebne toocreate **CloudMediaContext** wystąpienie reprezentującego hello kontekstu serwera.</span><span class="sxs-lookup"><span data-stu-id="b6eca-173">toostart programming against Media Services, you need toocreate a **CloudMediaContext** instance that represents hello server context.</span></span> <span data-ttu-id="b6eca-174">Należy również toopass hello **identyfikator URI dla usługi REST nośnika** toohello **CloudMediaContext** konstruktora.</span><span class="sxs-lookup"><span data-stu-id="b6eca-174">You also need toopass hello **resource URI for Media REST Services** toohello **CloudMediaContext** constructor.</span></span> <span data-ttu-id="b6eca-175">Możesz uzyskać hello **identyfikator URI dla usługi REST nośnika** wartość z zakresu od hello również portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="b6eca-175">You can get hello **resource URI for Media REST Services** value from hello Azure portal as well.</span></span>

<span data-ttu-id="b6eca-176">Witaj Poniższy przykładowy kod tworzy **CloudMediaContext** wystąpienie:</span><span class="sxs-lookup"><span data-stu-id="b6eca-176">hello following code example creates a **CloudMediaContext** instance:</span></span>

    CloudMediaContext context = new CloudMediaContext(new Uri("YOUR REST API ENDPOINT HERE"), tokenProvider);
    
<span data-ttu-id="b6eca-177">Witaj poniższy przykład pokazuje, jak toocreate hello kontekstu token i hello Azure AD:</span><span class="sxs-lookup"><span data-stu-id="b6eca-177">hello following example shows how toocreate hello Azure AD token and hello context:</span></span>

    namespace AADAuthSample
    {
    
        class Program
        {
            static void Main(string[] args)
            {
                var tokenCredentials = new AzureAdTokenCredentials("{YOUR Azure AD TENANT DOMAIN HERE}", 
                                            new AzureAdClientSymmetricKey("{YOUR CLIENT ID HERE}", "{YOUR CLIENT SECRET}"), 
                                            AzureEnvironments.AzureCloudEnvironment);
            
                var tokenProvider = new AzureAdTokenProvider(tokenCredentials);
    
                // Specify your REST API endpoint, for example "https://accountname.restv2.westcentralus.media.azure.net/API".      
                CloudMediaContext context = new CloudMediaContext(new Uri("YOUR REST API ENDPOINT HERE"), tokenProvider);
    
                var assets = context.Assets;
                foreach (var a in assets)
                {
                    Console.WriteLine(a.Name);
                }
    
                Console.ReadLine();
            }
    
        }
    }

## <a name="next-steps"></a><span data-ttu-id="b6eca-178">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="b6eca-178">Next steps</span></span>

<span data-ttu-id="b6eca-179">Rozpoczynanie pracy z [przekazywania plików konta tooyour](media-services-dotnet-upload-files.md).</span><span class="sxs-lookup"><span data-stu-id="b6eca-179">Get started with [uploading files tooyour account](media-services-dotnet-upload-files.md).</span></span>
