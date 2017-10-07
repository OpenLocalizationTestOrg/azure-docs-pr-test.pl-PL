---
title: "tooSet aaaHow zapasowej komputera do tworzenia usługi Media z platformą .NET"
description: "Dowiedz się więcej o wymaganiach wstępnych hello Media Services przy użyciu hello SDK usługi Media Services dla platformy .NET. Też dowiedzieć się, jak toocreate aplikacji Visual Studio."
services: media-services
documentationcenter: 
author: juliako
manager: cfowler
editor: 
ms.assetid: ec2804c7-c656-4fbf-b3e4-3f0f78599a7f
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 08/23/2017
ms.author: juliako
ms.openlocfilehash: a5a2af3211d8156fd7dea99831fb769df4130d41
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="media-services-development-with-net"></a>Tworzenia usługi Media Services z platformą .NET
[!INCLUDE [media-services-selector-setup](../../includes/media-services-selector-setup.md)]

W tym temacie omówiono sposób toostart tworzenie Media Services aplikacji przy użyciu platformy .NET.

Witaj **zestawu .NET SDK usługi Azure Media Services** biblioteki umożliwia tooprogram względem usługi Media Services przy użyciu platformy .NET. toomake go nawet łatwiejsze toodevelop z platformą .NET, hello **rozszerzenia SDK .NET usługi Azure Media Services** podano biblioteki. Ta biblioteka zawiera zestaw metod rozszerzeń i funkcje pomocnicze, które upraszczają kodu .NET. Zarówno biblioteki są dostępne za pośrednictwem **NuGet** i **GitHub**.

## <a name="prerequisites"></a>Wymagania wstępne
* Konto usługi Media Services w nowej lub istniejącej subskrypcji platformy Azure. Zobacz temat hello [jak tooCreate konta usługi Media Services](media-services-portal-create-account.md).
* Systemy operacyjne: Windows 10, Windows 7, Windows 2008 R2 lub Windows 8.
* Program .NET framework 4.5.
* Program Visual Studio.

## <a name="create-and-configure-a-visual-studio-project"></a>Tworzenie i konfigurowanie projektu programu Visual Studio
W tej sekcji opisano sposób toocreate projektu programu Visual Studio i skonfigurować go do tworzenia usługi Media Services.  W takim przypadku projekt hello jest aplikacji konsolowej C# systemu Windows, ale hello same kroki instalacji pokazane zastosować tooother typy projektów utworzonych dla usługi Media Services w aplikacji (na przykład aplikacji formularzy systemu Windows lub aplikacji sieci Web programu ASP.NET).

W tej sekcji przedstawiono sposób toouse **NuGet** tooadd .NET SDK usługi Media Services rozszerzenia i inne zależnej biblioteki.

Alternatywnie można uzyskać hello najnowsze bitów .NET SDK usługi Media Services z usługi GitHub ([github.com/Azure/azure-sdk-for-media-services](https://github.com/Azure/azure-sdk-for-media-services) lub [github.com/Azure/azure-sdk-for-media-services-extensions](https://github.com/Azure/azure-sdk-for-media-services-extensions)), utworzenie rozwiązania hello i dodawanie projektu klienta toohello odwołania hello. Wszystkie zależności niezbędne hello uzyskać pobrane i wyodrębnione automatycznie.

1. Utwórz nową aplikację konsoli języka C# w programie Visual Studio. Wprowadź hello **nazwa**, **lokalizacji**, i **Nazwa rozwiązania**, a następnie kliknij przycisk OK.
2. Utworzenie rozwiązania hello.
3. Użyj **NuGet** tooinstall i Dodaj **rozszerzenia SDK .NET usługi Azure Media Services** (**windowsazure.mediaservices.extensions**). Podczas instalacji tego pakietu instalowany jest również zestaw **.NET SDK usługi Media Services** oraz dodawane są wszystkie inne wymagane zależności.
   
    Upewnij się, że masz hello najnowszą wersję programu NuGet. Aby uzyskać dodatkowe instrukcje instalacji i informacje, zobacz [NuGet](http://nuget.codeplex.com/).
4. W Eksploratorze rozwiązań kliknij prawym przyciskiem myszy nazwę projektu hello hello, a następnie wybierz pakiety zarządzania pakietami NuGet.
   
    zostanie wyświetlone okno dialogowe Zarządzanie pakietami NuGet Hello.
5. W galerii Online hello, wyszukaj rozszerzenia MediaServices Azure, wybierz rozszerzenia SDK .NET usługi Azure Media Services, a następnie kliknij przycisk Zainstaluj hello.
   
    Projekt Hello jest modyfikowany i odwołuje się do toohello rozszerzenia SDK usługi Media Services .NET, SDK .NET usługi Media Services, i są dodawane innych zestawów zależnych.
6. toopromote czyszczący Środowisko deweloperskie, należy wziąć pod uwagę umożliwiające przywracanie pakietów NuGet. Aby uzyskać więcej informacji, zobacz [Przywracanie pakietu NuGet "](http://docs.nuget.org/consume/package-restore).
7. Dodaj odwołanie za**System.Configuration** zestawu. Ten zestaw zawiera hello System.Configuration. **ConfigurationManager** klasy czyli pliki konfiguracji używane tooaccess (na przykład App.config).
   
    odwołania tooadd za pomocą okna dialogowego Zarządzanie odwołaniami hello, kliknij prawym przyciskiem myszy nazwę projektu hello w Eksploratorze rozwiązań hello. Następnie wybierz Dodaj i odwołania.
   
    zostanie wyświetlone okno dialogowe Zarządzanie odwołaniami Hello.
8. W obszarze zestawów struktury .NET Znajdź i wybierz zestawu System.Configuration hello i naciśnij przycisk OK.
9. Otwórz plik App.config hello i Dodaj *appSettings* pliku toohello sekcji.     
   
    Ustaw wartości hello, które są potrzebne tooconnect toohello Media Services API. Aby uzyskać więcej informacji, zobacz [hello dostępu do interfejsu API usługi Azure Media Services przy użyciu uwierzytelniania usługi Azure AD](media-services-use-aad-auth-to-access-ams-api.md). 

    Jeśli używasz [uwierzytelnianie użytkownika](media-services-use-aad-auth-to-access-ams-api.md#types-of-authentication) pliku konfiguracji, prawdopodobnie będzie mieć wartości domeny dzierżawy usługi Azure AD i hello punkt końcowy interfejsu API REST usługi AMS.
    
    >[!Important]
    >Większość przykładów kodu w dokumentacji usługi Azure Media Services hello zestawu, użyj typu (interactive) użytkownika toohello tooconnect uwierzytelniania interfejsu API usług AMS. Ta metoda uwierzytelniania będzie działać do zarządzania i monitorowania natywnych aplikacji: aplikacje mobilne, aplikacje systemu Windows i aplikacji konsoli. Ta metoda uwierzytelniania nie jest odpowiedni dla serwera, usługi sieci web, interfejsów API typu aplikacji.  Aby uzyskać więcej informacji, zobacz [hello dostępu do interfejsu API usług AMS przy użyciu uwierzytelniania usługi Azure AD](media-services-use-aad-auth-to-access-ams-api.md).

        <configuration>
        ...
            <appSettings>
              <add key="AADTenantDomain" value="YourAADTenantDomain" />
              <add key="MediaServiceRESTAPIEndpoint" value="YourRESTAPIEndpoint" />
            </appSettings>

        </configuration>

10. Zastąp istniejący hello **przy użyciu** instrukcje hello początku pliku Program.cs hello hello następującego kodu.
           
        using System;
        using System.Configuration;
        using System.IO;
        using Microsoft.WindowsAzure.MediaServices.Client;
        using System.Threading;
        using System.Collections.Generic;
        using System.Linq;

W tym momencie wszystko jest gotowe toostart opracowanie aplikacji usługi Media Services.    

## <a name="example"></a>Przykład

W tym miejscu jest mała przykład łączy toohello AMS interfejsu API, który zawiera listę wszystkich dostępnych procesorów nośnika.
    
    class Program
    {
        // Read values from hello App.config file.
        private static readonly string _AADTenantDomain =
            ConfigurationManager.AppSettings["AADTenantDomain"];
        private static readonly string _RESTAPIEndpoint =
            ConfigurationManager.AppSettings["MediaServiceRESTAPIEndpoint"];
    
        private static CloudMediaContext _context = null;
        static void Main(string[] args)
        {
            var tokenCredentials = new AzureAdTokenCredentials(_AADTenantDomain, AzureEnvironments.AzureCloudEnvironment);
            var tokenProvider = new AzureAdTokenProvider(tokenCredentials);
    
            _context = new CloudMediaContext(new Uri(_RESTAPIEndpoint), tokenProvider);
    
            // List all available Media Processors
            foreach (var mp in _context.MediaProcessors)
            {
                Console.WriteLine(mp.Name);
            }
    
        }

##<a name="next-steps"></a>Następne kroki

Teraz [możesz połączyć toohello interfejsu API usług AMS](media-services-use-aad-auth-to-access-ams-api.md) i uruchomić [tworzenie](media-services-dotnet-get-started.md).


## <a name="media-services-learning-paths"></a>Ścieżki szkoleniowe dotyczące usługi Media Services
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Przekazywanie opinii
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

