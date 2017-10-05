---
title: "Łączenie z konta usługi Media Services przy użyciu platformy .NET"
description: "W tym temacie przedstawiono sposób nawiązywania połączenia za pomocą usługi Media Services .NET."
services: media-services
documentationcenter: 
author: juliako
manager: erikre
editor: 
ms.assetid: a8412a29-59dc-44a0-ace0-be79a97dab63
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 09/26/2016
ms.author: juliako
ms.openlocfilehash: 892932116934952265a21ab17aac3434b5760136
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="connecting-to-media-services-account-using-media-services-sdk-for-net"></a>Łączenie z konta usługi Media Services przy użyciu zestawu SDK usługi Media Services dla platformy .NET
> [!div class="op_single_selector"]
> * [REST](media-services-rest-connect-programmatically.md)
> * [.NET](media-services-dotnet-connect-programmatically.md)
> 
> 

W tym temacie opisano sposób uzyskiwania połączenie programowe Microsoft Azure Media Services są programowania się przy użyciu zestawu SDK usługi multimediów dla platformy .NET.

## <a name="connecting-to-media-services"></a>Nawiązywanie połączenia z usługi Media Services
Połącz się z usługi Media Services programowo, możesz musi mieć wcześniej skonfigurowane konto platformy Azure, skonfigurowane na tym koncie usługi Media Services i następnie ponowne skonfigurowanie projektu programu Visual Studio do tworzenia aplikacji przy użyciu zestawu SDK usługi multimediów dla platformy .NET. Aby uzyskać więcej informacji Zobacz Instalator do tworzenia aplikacji przy użyciu zestawu SDK usługi multimediów dla platformy .NET.

Na końcu procesu instalacji konta usługi Media Services uzyskany następujące wartości wymagane połączenia. Użyj tych tworzyć programowe połączenia z usługi Media Services.

* Nazwa konta usługi Media Services.
* Klucz konta usługi Media Services.

Aby znaleźć te wartości, przejdź do portalu zarządzania Azure, wybierz konto usługi multimediów, a następnie kliknij polecenie "**Zarządzanie KLUCZAMI**" ikony w dolnej części okna portalu. Kliknięcie ikony obok każdego pola tekstowego powoduje skopiowanie wartości do schowka systemowego.

## <a name="creating-a-cloudmediacontext-instance"></a>Tworzenie wystąpienia CloudMediaContext
Aby rozpocząć Programowanie w odniesieniu do usługi Media Services, musisz utworzyć **CloudMediaContext** wystąpienia, który reprezentuje kontekstu serwera. **CloudMediaContext** zawiera odwołania do kolekcji ważne, łącznie z zadań, zasobów, plików, zasady dostępu i lokalizatorów.

> [!NOTE]
> **CloudMediaContext** klasa nie jest bezpieczne dla wątków. Należy utworzyć nowe CloudMediaContext na wątku lub zestaw operacji.
> 
> 

CloudMediaContext ma pięć przeciążeń konstruktora. Zalecane jest użycie konstruktorów przyjmujących **MediaServicesCredentials** jako parametr. Aby uzyskać więcej informacji, zobacz **ponowne użycie tokeny usługi kontroli dostępu** znajdujący się na ścieżce. 

W poniższym przykładzie użyto publicznego konstruktora CloudMediaContext(MediaServicesCredentials credentials):

    // _cachedCredentials and _context are class member variables. 
    _cachedCredentials = new MediaServicesCredentials(
                    _mediaServicesAccountName,
                    _mediaServicesAccountKey);

    _context = new CloudMediaContext(_cachedCredentials);


## <a name="reusing-access-control-service-tokens"></a>Ponowne wykorzystywanie tokeny usługi kontroli dostępu
W tej sekcji przedstawiono sposób ponownego użycia tokenów w usłudze kontroli dostępu za pomocą konstruktorów CloudMediaContext MediaServicesCredentials jako parametr.

[Azure kontroli dostępu Active Directory](https://msdn.microsoft.com/library/hh147631.aspx) (znanej także jako usługa kontroli dostępu lub ACS) jest oparta na chmurze usługi, która zapewnia łatwy sposób uwierzytelniania i autoryzacji użytkowników uzyskujących dostęp do aplikacji sieci web. Microsoft Azure Media Services kontroluje dostęp do swoich usług jednak protokołu OAuth, która wymaga tokenu usługi ACS. Usługa Media Services odbiera tokenów usług ACS z serwera autoryzacji.

Podczas tworzenia przy użyciu zestawu SDK usługi multimediów, użytkownik może nie dotyczyć tokenów, ponieważ zestaw SDK kodu menedżerów je automatycznie. Jednak SDK tokeny ACS w pełni zarządzać co prowadzi do niepotrzebnych żądania tokenu. Żądania tokenów jest czasochłonne i wykorzystuje zasoby klienta i serwera. Ponadto serwer usług ACS ogranicza żądania, jeżeli stawki jest zbyt duża. Limit wynosi 30 żądań na sekundę, zobacz [ograniczenia usługi ACS](https://msdn.microsoft.com/library/gg185909.aspx) więcej szczegółów.

Począwszy od zestawu SDK usługi Media wersji 3.0.0.0, można użyć ponownie tokenów usług ACS. **CloudMediaContext** konstruktorów przyjmujących **MediaServicesCredentials** jako parametr Włącz udostępnianie ACS tokeny od wielu kontekstów. Klasa MediaServicesCredentials hermetyzuje poświadczenia usługi Media Services. Jeśli tokenu usługi ACS jest dostępny, a jego czas wygaśnięcia jest znany, można tworzyć nowe wystąpienie MediaServicesCredentials z tokenem i przekazywany do konstruktora CloudMediaContext. Należy pamiętać, że SDK usługi Media Services automatycznie odświeża tokenów, gdy wygasną. Istnieją dwa sposoby ponowne tokenów usług ACS, jak pokazano w poniższych przykładach.

* Można buforować **MediaServicesCredentials** obiektu w pamięci (na przykład klasa statyczna zmienna). Następnie przekaż obiektu w pamięci podręcznej do konstruktora CloudMediaContext. Obiekt MediaServicesCredentials zawiera tokenu usługi ACS, która może nastąpić, jeśli jest nadal ważny. Jeśli token nie jest prawidłowy, zostaną odświeżone przez zestaw SDK usługi Media za pomocą poświadczeń podanych do konstruktora MediaServicesCredentials.
  
    Należy pamiętać, że **MediaServicesCredentials** obiektu pobiera prawidłowy token po RefreshToken jest wywoływana. **CloudMediaContext** wywołania **RefreshToken** metody w konstruktorze. Jeśli zamierzasz zapisać wartości tokenów w pamięci zewnętrznej, upewnij się sprawdzić, czy wartość TokenExpiration jest prawidłowa, przed zapisaniem danych tokenu. Jeśli nie jest prawidłowy, należy wywołać RefreshToken przed buforowania.
  
        // Create and cache the Media Services credentials in a static class variable.
        _cachedCredentials = new MediaServicesCredentials(_mediaServicesAccountName, _mediaServicesAccountKey);

        // Use the cached credentials to create a new CloudMediaContext object.
        if(_cachedCredentials == null)
        {
            _cachedCredentials = new MediaServicesCredentials(_mediaServicesAccountName, _mediaServicesAccountKey);
        }

        CloudMediaContext context = new CloudMediaContext(_cachedCredentials);

* Można buforować ciąg AccessToken i wartości TokenExpiration. Później można użyć wartości do utworzenia nowego obiektu MediaServicesCredentials z pamięci podręcznej danych tokenu.  Jest to szczególnie przydatne w scenariuszach, gdzie token można bezpiecznie wymieniać między wiele procesów lub komputery.
  
    Poniższe fragmenty kodu wywoływać metod SaveTokenDataToExternalStorage, GetTokenDataFromExternalStorage i UpdateTokenDataInExternalStorageIfNeeded, które nie są zdefiniowane w tym przykładzie. Można zdefiniować tych metod, przechowywanie, pobieranie i aktualizację tokenu danych w pamięci zewnętrznej. 
  
        CloudMediaContext context1 = new CloudMediaContext(_mediaServicesAccountName, _mediaServicesAccountKey);
  
        // Get token values from the context.
        var accessToken = context1.Credentials.AccessToken;
        var tokenExpiration = context1.Credentials.TokenExpiration;
  
        // Save token values for later use. 
        // The SaveTokenDataToExternalStorage method should check 
        // whether the TokenExpiration value is valid before saving the token data. 
        // If it is not valid, call MediaServicesCredentials’s RefreshToken before caching.
        SaveTokenDataToExternalStorage(accessToken, tokenExpiration);
  
    Umożliwia utworzenie MediaServicesCredentials zapisanych wartości tokenu.

        var accessToken = "";
        var tokenExpiration = DateTime.UtcNow;

        // Retrieve saved token values.
        GetTokenDataFromExternalStorage(out accessToken, out tokenExpiration);

        // Create a new MediaServicesCredentials object using saved token values.
        MediaServicesCredentials credentials = new MediaServicesCredentials(_mediaServicesAccountName, _mediaServicesAccountKey)
        {
            AccessToken = accessToken,
            TokenExpiration = tokenExpiration
        };

        CloudMediaContext context2 = new CloudMediaContext(credentials);

    W przypadku, gdy token został zaktualizowany przez SDK usługi Media Services, należy zaktualizować kopię tokenu. 

        if(tokenExpiration != context2.Credentials.TokenExpiration)
        {
            UpdateTokenDataInExternalStorageIfNeeded(accessToken, context2.Credentials.TokenExpiration);
        }


* Jeśli masz wiele kont usługi Media Services (na przykład w przypadku udostępniania celów lub geograficznie dystrybucji obciążenia) może buforować MediaServicesCredentials obiektów przy użyciu kolekcji System.Collections.Concurrent.ConcurrentDictionary (kolekcji obiekt ConcurrentDictionary reprezentuje kolekcję wątkowo pary klucz wartość, które mogą być udostępniane przez wiele wątków jednocześnie). Metoda GetOrAdd umożliwia następnie Uzyskaj buforowanych poświadczeń. 
  
        // Declare a static class variable of the ConcurrentDictionary type in which the Media Services credentials will be cached.  
        private static readonly ConcurrentDictionary<string, MediaServicesCredentials> mediaServicesCredentialsCache = 
            new ConcurrentDictionary<string, MediaServicesCredentials>();

        // Cache (or get already cached) Media Services credentials. Use these credentials to create a new CloudMediaContext object.
        static public CloudMediaContext CreateMediaServicesContext(string accountName, string accountKey)
        {
            CloudMediaContext cloudMediaContext;
            MediaServicesCredentials mediaServicesCredentials;

            mediaServicesCredentials = mediaServicesCredentialsCache.GetOrAdd(
                accountName,
                valueFactory => new MediaServicesCredentials(accountName, accountKey));

            cloudMediaContext = new CloudMediaContext(mediaServicesCredentials);

            return cloudMediaContext;
        }

## <a name="connecting-to-a-media-services-account-located-in-the-north-china-region"></a>Łączenie z kontem usługi Media Services znajdującego się w regionie Chin Północna
Jeśli Twoje konto znajduje się w regionie Chin Północna, użyj Konstruktora następujące:

    public CloudMediaContext(Uri apiServer, string accountName, string accountKey, string scope, string acsBaseAddress)

Na przykład:

    _context = new CloudMediaContext(
        new Uri("https://wamsbjbclus001rest-hs.chinacloudapp.cn/API/"),
        _mediaServicesAccountName,
        _mediaServicesAccountKey,
        "urn:WindowsAzureMediaServices",
        "https://wamsprodglobal001acs.accesscontrol.chinacloudapi.cn");


## <a name="storing-connection-values-in-configuration"></a>Przechowywanie wartości połączenia w konfiguracji
Jest bardzo zalecanym rozwiązaniem do przechowywania wartości połączenia, szczególnie ważne wartości, takie jak nazwa konta i hasło, w konfiguracji. Ponadto jest zalecanym rozwiązaniem do szyfrowania danych poufnych konfiguracji. Plik całą konfigurację można zaszyfrować przy użyciu systemu szyfrowania plików systemu Windows (EFS). Aby włączyć system szyfrowania plików do pliku, kliknij plik prawym przyciskiem myszy, wybierz **właściwości**i włączenia szyfrowania w **zaawansowane** kartę Ustawienia. Lub można utworzyć niestandardowego rozwiązania do szyfrowania przy użyciu konfiguracji chronionych zaznaczonych części pliku konfiguracji. Zobacz [szyfrowania za pomocą konfiguracji chronionych informacji o konfiguracji](https://msdn.microsoft.com/library/53tyfkaw.aspx).

Następujący plik App.config zawiera wartości wymagane połączenia. Wartości w <appSettings> elementu są wymagane wartości, otrzymanych proces konfigurowania konta usługi Media Services.

    <configuration>
      <appSettings>
        <add key="MediaServicesAccountName" value="Media-Services-Account-Name" />
        <add key="MediaServicesAccountKey" value="Media-Services-Account-Key" />
      </appSettings>
    </configuration>


Aby pobrać wartości połączenia z konfiguracji, można użyć **ConfigurationManager** klasy, a następnie przypisać wartości do pola w kodzie:

    private static readonly string _accountName = ConfigurationManager.AppSettings["MediaServicesAccountName"];
    private static readonly string _accountKey = ConfigurationManager.AppSettings["MediaServicesAccountKey"];



## <a name="media-services-learning-paths"></a>Ścieżki szkoleniowe dotyczące usługi Media Services
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Przekazywanie opinii
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

