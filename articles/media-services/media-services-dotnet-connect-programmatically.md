---
title: "Konta usług tooMedia aaaConnecting przy użyciu platformy .NET"
description: "W tym temacie przedstawiono sposób tooconnect tooMedia usług budynkach .NET."
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
ms.openlocfilehash: a23bd285f7cae17ae5831e1e50e73947afbb9a3d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="connecting-toomedia-services-account-using-media-services-sdk-for-net"></a>Łączenie tooMedia konta usług przy użyciu zestawu SDK usługi Media Services dla platformy .NET
> [!div class="op_single_selector"]
> * [REST](media-services-rest-connect-programmatically.md)
> * [.NET](media-services-dotnet-connect-programmatically.md)
> 
> 

W tym temacie opisano, jak tooobtain tooMicrosoft połączenie programowe usługi Azure Media Services są programowania z hello SDK usługi Media Services dla platformy .NET.

## <a name="connecting-toomedia-services"></a>Połączenie usług tooMedia
tooconnect tooMedia usług programowo, możesz musi mieć wcześniej skonfigurowane konto platformy Azure, skonfigurowane na tym koncie usługi Media Services i następnie ponowne skonfigurowanie projektu programu Visual Studio do tworzenia aplikacji z hello SDK usługi Media Services dla platformy .NET. Aby uzyskać więcej informacji zobacz ustawień dla rozwoju z hello SDK usługi Media Services dla platformy .NET.

Na końcu procesu instalacji konta usługi Media Services hello hello, uzyskać następujące hello wymagane wartości połączenia. Użyj tych połączeń programowe toomake tooMedia usług.

* Nazwa konta usługi Media Services.
* Klucz konta usługi Media Services.

te wartości, toofind Przejdź toohello portalu zarządzania Azure, wybierz konto usługi multimediów i kliknij pozycję hello "**Zarządzanie KLUCZAMI**" ikonę na powitania dolnej części okna portalu hello. Kliknięcie hello ikona dalej tooeach tekst pola kopie hello wartość toohello schowka systemowego.

## <a name="creating-a-cloudmediacontext-instance"></a>Tworzenie wystąpienia CloudMediaContext
Programowanie w odniesieniu do Media Services potrzebne toocreate toostart **CloudMediaContext** wystąpienie reprezentującego hello kontekstu serwera. Witaj **CloudMediaContext** zawiera odwołania do kolekcji tooimportant tym zadań, zasobów, plików, zasady dostępu i lokalizatorów.

> [!NOTE]
> Witaj **CloudMediaContext** klasa nie jest bezpieczne dla wątków. Należy utworzyć nowe CloudMediaContext na wątku lub zestaw operacji.
> 
> 

CloudMediaContext ma pięć przeciążeń konstruktora. Jest zalecana toouse konstruktorów **MediaServicesCredentials** jako parametr. Aby uzyskać więcej informacji, zobacz hello **ponowne użycie tokeny usługi kontroli dostępu** znajdujący się na ścieżce. 

Witaj poniższym przykładzie użyto publicznego konstruktora CloudMediaContext(MediaServicesCredentials credentials) hello:

    // _cachedCredentials and _context are class member variables. 
    _cachedCredentials = new MediaServicesCredentials(
                    _mediaServicesAccountName,
                    _mediaServicesAccountKey);

    _context = new CloudMediaContext(_cachedCredentials);


## <a name="reusing-access-control-service-tokens"></a>Ponowne wykorzystywanie tokeny usługi kontroli dostępu
W tej sekcji przedstawiono, jak tokeny tooreuse usłudze kontroli dostępu za pomocą konstruktorów CloudMediaContext MediaServicesCredentials jako parametr.

[Azure kontroli dostępu Active Directory](https://msdn.microsoft.com/library/hh147631.aspx) (znanej także jako usługa kontroli dostępu lub ACS) to usługa oparta na chmurze, która zapewnia prosty sposób uwierzytelniania i autoryzowanie dostępu toogain użytkowników aplikacji sieci web tootheir. Microsoft Azure Media Services kontroluje dostęp usługi tooits jednak protokołu OAuth, która wymaga tokenu usługi ACS. Usługa Media Services odbiera hello ACS tokenów z serwera autoryzacji.

Podczas tworzenia z hello SDK usługi Media Services, można wybrać toonot transakcji z tokenami hello, ponieważ hello menedżerów kod zestawu SDK je automatycznie. Jednak dzięki czemu hello zestawu SDK w pełni zarządzać hello ACS tokeny potencjalnych klientów toounnecessary żądań dotyczących tokenów. Żądania tokenów jest czasochłonne i wykorzystuje zasoby powitania klienta i serwera. Ponadto serwer usług ACS hello ogranicza żądań hello Jeśli częstotliwość hello jest zbyt wysoka. Witaj limit wynosi 30 żądań na sekundę, zobacz [ograniczenia usługi ACS](https://msdn.microsoft.com/library/gg185909.aspx) więcej szczegółów.

Począwszy od zestawu SDK usługi Media Services w wersji 3.0.0.0 hello, można użyć ponownie hello ACS tokenów. Witaj **CloudMediaContext** konstruktorów przyjmujących **MediaServicesCredentials** jako parametr włączyć udostępniania hello ACS tokeny od wielu kontekstów. Witaj MediaServicesCredentials klasa hermetyzuje hello poświadczenia usługi Media Services. Jeśli tokenu usługi ACS jest dostępny, a jego czas wygaśnięcia jest znany, można utworzenia nowego wystąpienia MediaServicesCredentials z tokenem hello i przekaż go konstruktora toohello CloudMediaContext. Należy pamiętać, że hello SDK usługi Media Services automatycznie odświeża tokenów, gdy wygasną. Istnieją dwa sposoby tooreuse tokenów usług ACS, jak pokazano w poniższych przykładach hello.

* Może buforować hello **MediaServicesCredentials** obiektu w pamięci (na przykład klasa statyczna zmienna). Przekazuj konstruktora CloudMediaContext toohello obiektów hello w pamięci podręcznej. Obiekt MediaServicesCredentials Hello zawiera tokenu usługi ACS, która może nastąpić, jeśli jest nadal ważny. Jeśli hello token jest nieprawidłowy, zostaną odświeżone przez hello SDK usługi Media Services przy użyciu poświadczeń hello danego toohello MediaServicesCredentials konstruktora.
  
    Należy pamiętać, że hello **MediaServicesCredentials** obiektu pobiera prawidłowy token po hello RefreshToken jest wywoływana. Witaj **CloudMediaContext** hello wywołania **RefreshToken** metody w Konstruktorze hello. Jeśli planujesz toosave hello wartości tokenów tooan zewnętrznych urządzeń pamięci masowej, upewnij się toocheck czy hello TokenExpiration wartość jest prawidłowa przed zapisaniem danych tokenu hello. Jeśli nie jest prawidłowy, należy wywołać RefreshToken przed buforowania.
  
        // Create and cache hello Media Services credentials in a static class variable.
        _cachedCredentials = new MediaServicesCredentials(_mediaServicesAccountName, _mediaServicesAccountKey);

        // Use hello cached credentials toocreate a new CloudMediaContext object.
        if(_cachedCredentials == null)
        {
            _cachedCredentials = new MediaServicesCredentials(_mediaServicesAccountName, _mediaServicesAccountKey);
        }

        CloudMediaContext context = new CloudMediaContext(_cachedCredentials);

* Można buforować hello AccessToken ciągu i hello TokenExpiration wartości. wartości Hello później może być używane toocreate MediaServicesCredentials nowy obiekt z hello w pamięci podręcznej danych tokenu.  Jest to szczególnie przydatne w scenariuszach, gdzie hello token można bezpiecznie wymieniać między wiele procesów lub komputery.
  
    Witaj poniższe fragmenty kodu wywołać hello SaveTokenDataToExternalStorage, GetTokenDataFromExternalStorage i UpdateTokenDataInExternalStorageIfNeeded metody, które nie są zdefiniowane w tym przykładzie. W pamięci zewnętrznej, można zdefiniować te toostore metod, pobieranie i aktualizacji danych tokenu. 
  
        CloudMediaContext context1 = new CloudMediaContext(_mediaServicesAccountName, _mediaServicesAccountKey);
  
        // Get token values from hello context.
        var accessToken = context1.Credentials.AccessToken;
        var tokenExpiration = context1.Credentials.TokenExpiration;
  
        // Save token values for later use. 
        // hello SaveTokenDataToExternalStorage method should check 
        // whether hello TokenExpiration value is valid before saving hello token data. 
        // If it is not valid, call MediaServicesCredentials’s RefreshToken before caching.
        SaveTokenDataToExternalStorage(accessToken, tokenExpiration);
  
    Użyj hello zapisane wartości tokenów toocreate MediaServicesCredentials.

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

    W przypadku, gdy hello token został zaktualizowany przez hello SDK usługi Media Services, należy zaktualizować hello tokenu kopię. 

        if(tokenExpiration != context2.Credentials.TokenExpiration)
        {
            UpdateTokenDataInExternalStorageIfNeeded(accessToken, context2.Credentials.TokenExpiration);
        }


* Jeśli masz wiele kont usługi Media Services (na przykład w przypadku udostępniania celów lub geograficznie dystrybucji obciążenia) może buforować MediaServicesCredentials obiektów przy użyciu kolekcji System.Collections.Concurrent.ConcurrentDictionary hello (hello Obiekt ConcurrentDictionary kolekcji reprezentuje kolekcję wątkowo pary klucz wartość, które mogą być udostępniane przez wiele wątków jednocześnie). Następnie można hello GetOrAdd metody tooget hello buforowanych poświadczeń. 
  
        // Declare a static class variable of hello ConcurrentDictionary type in which hello Media Services credentials will be cached.  
        private static readonly ConcurrentDictionary<string, MediaServicesCredentials> mediaServicesCredentialsCache = 
            new ConcurrentDictionary<string, MediaServicesCredentials>();

        // Cache (or get already cached) Media Services credentials. Use these credentials toocreate a new CloudMediaContext object.
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

## <a name="connecting-tooa-media-services-account-located-in-hello-north-china-region"></a>Łączenie tooa konta usługi Media Services znajdującego się w regionie Północna Chin hello
Twoje konto znajduje się w regionie Północna Chin hello, należy użyć następującego konstruktora hello:

    public CloudMediaContext(Uri apiServer, string accountName, string accountKey, string scope, string acsBaseAddress)

Na przykład:

    _context = new CloudMediaContext(
        new Uri("https://wamsbjbclus001rest-hs.chinacloudapp.cn/API/"),
        _mediaServicesAccountName,
        _mediaServicesAccountKey,
        "urn:WindowsAzureMediaServices",
        "https://wamsprodglobal001acs.accesscontrol.chinacloudapi.cn");


## <a name="storing-connection-values-in-configuration"></a>Przechowywanie wartości połączenia w konfiguracji
Jest stanowczo zalecane praktyki toostore połączenia wartości, szczególnie poufnych takie jak nazwa konta i hasło w konfiguracji. Jest także zalecana praktyka tooencrypt poufne dane konfiguracyjne. Plik konfiguracji całego hello można szyfrować przy użyciu hello Windows System szyfrowania plików (EFS). Wybierz tooenable systemu szyfrowania plików w pliku, kliknij prawym przyciskiem myszy plik hello, **właściwości**i włączenia szyfrowania w hello **zaawansowane** kartę Ustawienia. Lub można utworzyć niestandardowego rozwiązania do szyfrowania przy użyciu konfiguracji chronionych zaznaczonych części pliku konfiguracji. Zobacz [szyfrowania za pomocą konfiguracji chronionych informacji o konfiguracji](https://msdn.microsoft.com/library/53tyfkaw.aspx).

Hello następującego pliku App.config zawiera hello wymagane wartości połączenia. Witaj wartości hello <appSettings> hello wymagane wartości, które masz od procesu konfiguracji konta usługi Media Services hello są elementu.

    <configuration>
      <appSettings>
        <add key="MediaServicesAccountName" value="Media-Services-Account-Name" />
        <add key="MediaServicesAccountKey" value="Media-Services-Account-Key" />
      </appSettings>
    </configuration>


wartości połączenia tooretrieve z konfiguracji, można użyć hello **ConfigurationManager** klasy, a następnie przypisz hello toofields wartości w kodzie:

    private static readonly string _accountName = ConfigurationManager.AppSettings["MediaServicesAccountName"];
    private static readonly string _accountKey = ConfigurationManager.AppSettings["MediaServicesAccountKey"];



## <a name="media-services-learning-paths"></a>Ścieżki szkoleniowe dotyczące usługi Media Services
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Przekazywanie opinii
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

