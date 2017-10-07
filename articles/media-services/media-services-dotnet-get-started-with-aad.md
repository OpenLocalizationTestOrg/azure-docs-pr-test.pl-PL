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
# <a name="use-azure-ad-authentication-tooaccess-azure-media-services-api-with-net"></a>Użyj usługi Azure AD authentication tooaccess interfejsu API usługi Azure Media Services z platformą .NET

Począwszy od windowsazure.mediaservices 4.0.0.4 Azure Media Services obsługuje uwierzytelnianie oparte na usłudze Azure Active Directory (Azure AD). W tym temacie opisano sposób toouse tooaccess uwierzytelniania usługi Azure AD interfejsu API usługi multimediów Azure za pomocą programu Microsoft .NET.

## <a name="prerequisites"></a>Wymagania wstępne

- Konto platformy Azure. Aby uzyskać szczegółowe informacje, zobacz [Bezpłatna wersja próbna systemu Azure](https://azure.microsoft.com/pricing/free-trial/). 
- Konto usługi Media Services. Aby uzyskać więcej informacji, zobacz [Tworzenie konta usługi Azure Media Services przy użyciu portalu Azure hello](media-services-portal-create-account.md).
- Witaj najnowszych [NuGet](https://www.nuget.org/packages/windowsazure.mediaservices) pakietu.
- Znajomość tematu hello [podczas uzyskiwania dostępu do usługi Azure Media usług interfejsu API za pomocą omówienie uwierzytelniania usługi AAD](media-services-use-aad-auth-to-access-ams-api.md). 

Podczas korzystania z uwierzytelniania usługi Azure AD z usługi Azure Media Services, można uwierzytelniać się w jednym z dwóch sposobów:

- **Uwierzytelnianie użytkownika** uwierzytelnia osoby, która używa toointeract aplikacji hello z zasobami usługi Azure Media Services. Interaktywna aplikacja Hello należy najpierw monitują hello poświadczenia użytkownika. Przykładem jest aplikacja konsoli zarządzania, który jest używany przez autoryzowanych użytkowników toomonitor kodowania zadań lub transmisja strumieniowa na żywo. 
- **Uwierzytelnianie głównej usługi** uwierzytelnia usługi. Aplikacje, które zazwyczaj używają tej metody uwierzytelniania są aplikacji uruchamianych demon usługi, usługi warstwy środkowej lub zaplanowanych zadań, takich jak aplikacje sieci web funkcji aplikacji, aplikacji logiki, interfejsów API albo mikrousług.

>[!IMPORTANT]
>Usługa Azure Media obecnie obsługuje model uwierzytelniania w usłudze kontroli dostępu platformy Azure. Kontrola dostępu autoryzacji będzie jednak toobe przestarzałe na 1 czerwca 2018. Firma Microsoft zaleca migracji model uwierzytelniania usługi Azure Active Directory tooan tak szybko, jak to możliwe.

## <a name="get-an-azure-ad-access-token"></a>Uzyskaj token dostępu usługi Azure AD

tooconnect toohello interfejsu API usługi Azure Media Services przy użyciu uwierzytelniania usługi Azure AD, powitania klienta aplikacji musi toorequest token dostępu usługi Azure AD. Jeśli używasz powitania klienta Media Services na platformie .NET SDK, wiele hello szczegóły dotyczące sposobu opakowana i uproszczone dla Ciebie w hello tooacquire token dostępu usługi Azure AD [AzureAdTokenProvider](https://github.com/Azure/azure-sdk-for-media-services/blob/dev/src/net/Client/Common/Common.Authentication/AzureAdTokenProvider.cs) i [AzureAdTokenCredentials ](https://github.com/Azure/azure-sdk-for-media-services/blob/dev/src/net/Client/Common/Common.Authentication/AzureAdTokenCredentials.cs) klasy. 

Na przykład, nie potrzebujesz tooprovide urzędu hello Azure AD, identyfikator URI zasobu usługi Media Services lub native szczegóły aplikacji usługi Azure AD. Są to dobrze znane wartości, które są już skonfigurowane przez hello klasa dostawcy tokenu dostępu usługi Azure AD. 

Jeśli nie używasz zestawu .NET SDK usługi Azure Media Service, zalecane jest użycie hello [Azure AD Authentication Library](../active-directory/develop/active-directory-authentication-libraries.md). Zobacz tooget wartości parametrów hello konieczność toouse z usługi Azure AD Authentication Library [za pomocą ustawień uwierzytelniania Azure tooaccess portalu usługi Azure AD hello](media-services-portal-get-started-with-aad.md).

Istnieje również możliwość zastąpienia hello domyślną implementację hello hello **AzureAdTokenProvider** z własną implementację.

## <a name="install-and-configure-azure-media-services-net-sdk"></a>Instalowanie i konfigurowanie zestawu .NET SDK usługi Azure Media Services

>[!NOTE] 
>Uwierzytelnianie toouse usługi Azure AD z hello .NET SDK usługi Media Services, potrzebne toohave hello najnowszych [NuGet](https://www.nuget.org/packages/windowsazure.mediaservices) pakietu. Ponadto Dodaj toohello odwołanie **Microsoft.IdentityModel.Clients.ActiveDirectory** zestawu. Jeśli korzystasz z istniejącej aplikacji, należy uwzględnić hello **Microsoft.WindowsAzure.MediaServices.Client.Common.Authentication.dll** zestawu. 

1. Utwórz nową aplikację konsoli języka C# w programie Visual Studio.
2. Użyj hello [windowsazure.mediaservices](https://www.nuget.org/packages/windowsazure.mediaservices) tooinstall pakietu NuGet **zestawu .NET SDK usługi Azure Media Services**. 

    tooadd odwołania przy użyciu narzędzia NuGet zająć hello następujące kroki: w **Eksploratora rozwiązań**, kliknij prawym przyciskiem myszy nazwę projektu hello, a następnie wybierz **pakiety zarządzania pakietami NuGet**. Następnie wyszukaj **windowsazure.mediaservices** i wybierz **zainstalować**.
    
    — lub —

    Uruchom hello następujące polecenie w **Konsola Menedżera pakietów** w programie Visual Studio.

        Install-Package windowsazure.mediaservices -Version 4.0.0.4

3. Dodaj **przy użyciu** tooyour kodu źródłowego.

        using Microsoft.WindowsAzure.MediaServices.Client; 

## <a name="use-user-authentication"></a>Uwierzytelnianie użytkownika

tooconnect toohello interfejsu API usługi Azure Media Service z włączoną opcją uwierzytelnienia użytkownika hello, powitania klienta aplikacji musi toorequest hello tokenu usługi Azure AD przy użyciu następujących parametrów:  

- Punkt końcowy dzierżawy usługi Azure AD. Witaj dzierżawy informacje mogą zostać pobrane z hello portalu Azure. Umieść kursor nad hello zalogowanego użytkownika w prawym górnym rogu hello.
- Identyfikator URI zasobu usługi Media Services.
- Identyfikator klienta aplikacji usługi Media Services (macierzysty). 
- Identyfikator URI przekierowania aplikacji usługi Media Services (macierzysty). 

Witaj wartości tych parametrów można znaleźć w **AzureEnvironments.AzureCloudEnvironment**. Witaj **AzureEnvironments.AzureCloudEnvironment** stała pomocnika w tooget zestawu .NET SDK hello jest hello prawo ustawienia zmiennej środowiskowej publicznego Centrum danych Azure. 

Zawiera ustawienia środowiska wstępnie zdefiniowane do uzyskiwania dostępu do usługi Media Services w wyłącznie w centrach danych publicznych hello. W przypadku regionów chmury suwerenne lub dla instytucji rządowych, można użyć **AzureChinaCloudEnvironment**, **AzureUsGovernmentEnvrionment**, lub **AzureGermanCloudEnvironment** odpowiednio.

Witaj poniższy przykład kodu tworzy token:
    
    var tokenCredentials = new AzureAdTokenCredentials("microsoft.onmicrosoft.com", AzureEnvironments.AzureCloudEnvironment);
    var tokenProvider = new AzureAdTokenProvider(tokenCredentials);
  
toostart Programowanie w odniesieniu do usługi Media Services, potrzebne toocreate **CloudMediaContext** wystąpienie reprezentującego hello kontekstu serwera. Witaj **CloudMediaContext** zawiera odwołania do kolekcji tooimportant tym zadań, zasobów, plików, zasady dostępu i lokalizatorów. 

Należy również toopass hello **identyfikator URI dla usługi REST nośnika** toohello **CloudMediaContext** konstruktora. Identyfikator URI zasobu hello tooget dla usługi REST Media Services, logowanie toohello portalu Azure, wybierz konto usługi Azure Media Services, wybierz **dostępu do interfejsu API**, a następnie wybierz **połączyć z użytkownikiem tooAzure Media Services uwierzytelnianie**. 

Witaj Poniższy przykładowy kod tworzy **CloudMediaContext** wystąpienie:

    CloudMediaContext context = new CloudMediaContext(new Uri("YOUR REST API ENDPOINT HERE"), tokenProvider);

Witaj poniższy przykład pokazuje, jak toocreate hello kontekstu token i hello Azure AD:

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
>Jeśli otrzymasz wyjątek mówi "hello serwer zdalny zwrócił błąd: (401) nieautoryzowane" Zobacz hello [kontrola dostępu](media-services-use-aad-auth-to-access-ams-api.md#access-control) części podczas uzyskiwania dostępu do Azure Media Services API, omówienie uwierzytelniania usługi Azure AD.

## <a name="use-service-principal-authentication"></a>Użyj uwierzytelniania głównej usługi
    
tooconnect toohello interfejsu API usługi Azure Media Services z opcją główna usługi hello, Twoja aplikacja warstwy środkowej (interfejs API sieci web lub aplikacji sieci web) powinna toorequests tokenu usługi Azure AD z hello następujące parametry:  

- Punkt końcowy dzierżawy usługi Azure AD. Witaj dzierżawy informacje mogą zostać pobrane z hello portalu Azure. Umieść kursor nad hello zalogowanego użytkownika w prawym górnym rogu hello.
- Identyfikator URI zasobu usługi Media Services.
- Wartości aplikacji w usłudze Azure AD: hello **identyfikator klienta** i **klucz tajny klienta**.

Witaj wartości hello **identyfikator klienta** i **klucz tajny klienta** parametrów można znaleźć w portalu Azure hello. Aby uzyskać więcej informacji, zobacz [wprowadzenie do korzystania z usługi Azure AD uwierzytelnianie przy użyciu hello portalu Azure](media-services-portal-get-started-with-aad.md).

Witaj poniższy przykład kodu tworzy token przy użyciu hello **AzureAdTokenCredentials** konstruktora przyjmującego **AzureAdClientSymmetricKey** jako parametr: 
    
    var tokenCredentials = new AzureAdTokenCredentials("{YOUR Azure AD TENANT DOMAIN HERE}", 
                                new AzureAdClientSymmetricKey("{YOUR CLIENT ID HERE}", "{YOUR CLIENT SECRET}"), 
                                AzureEnvironments.AzureCloudEnvironment);

    var tokenProvider = new AzureAdTokenProvider(tokenCredentials);

Można również określić hello **AzureAdTokenCredentials** konstruktora przyjmującego **AzureAdClientCertificate** jako parametr. 

Aby uzyskać instrukcje dotyczące toocreate i skonfigurować certyfikat w formularzu, które mogą być używane przez usługę Azure AD, zobacz [tooAzure AD w aplikacjach demon z certyfikatami - ręcznego konfigurowania uwierzytelniania](https://github.com/Azure-Samples/active-directory-dotnet-daemon-certificate-credential/blob/master/Manual-Configuration-Steps.md).

    var tokenCredentials = new AzureAdTokenCredentials("{YOUR Azure AD TENANT DOMAIN HERE}", 
                                new AzureAdClientCertificate("{YOUR CLIENT ID HERE}", "{YOUR CLIENT CERTIFICATE THUMBPRINT}"), 
                                AzureEnvironments.AzureCloudEnvironment);

toostart Programowanie w odniesieniu do usługi Media Services, potrzebne toocreate **CloudMediaContext** wystąpienie reprezentującego hello kontekstu serwera. Należy również toopass hello **identyfikator URI dla usługi REST nośnika** toohello **CloudMediaContext** konstruktora. Możesz uzyskać hello **identyfikator URI dla usługi REST nośnika** wartość z zakresu od hello również portalu Azure.

Witaj Poniższy przykładowy kod tworzy **CloudMediaContext** wystąpienie:

    CloudMediaContext context = new CloudMediaContext(new Uri("YOUR REST API ENDPOINT HERE"), tokenProvider);
    
Witaj poniższy przykład pokazuje, jak toocreate hello kontekstu token i hello Azure AD:

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

## <a name="next-steps"></a>Następne kroki

Rozpoczynanie pracy z [przekazywania plików konta tooyour](media-services-dotnet-upload-files.md).
