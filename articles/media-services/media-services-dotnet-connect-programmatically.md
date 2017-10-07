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
# <a name="connecting-toomedia-services-account-using-media-services-sdk-for-net"></a><span data-ttu-id="361bf-103">Łączenie tooMedia konta usług przy użyciu zestawu SDK usługi Media Services dla platformy .NET</span><span class="sxs-lookup"><span data-stu-id="361bf-103">Connecting tooMedia Services Account using Media Services SDK for .NET</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="361bf-104">REST</span><span class="sxs-lookup"><span data-stu-id="361bf-104">REST</span></span>](media-services-rest-connect-programmatically.md)
> * [<span data-ttu-id="361bf-105">.NET</span><span class="sxs-lookup"><span data-stu-id="361bf-105">.NET</span></span>](media-services-dotnet-connect-programmatically.md)
> 
> 

<span data-ttu-id="361bf-106">W tym temacie opisano, jak tooobtain tooMicrosoft połączenie programowe usługi Azure Media Services są programowania z hello SDK usługi Media Services dla platformy .NET.</span><span class="sxs-lookup"><span data-stu-id="361bf-106">This topic describes how tooobtain a programmatic connection tooMicrosoft Azure Media Services when you are programming with hello Media Services SDK for .NET.</span></span>

## <a name="connecting-toomedia-services"></a><span data-ttu-id="361bf-107">Połączenie usług tooMedia</span><span class="sxs-lookup"><span data-stu-id="361bf-107">Connecting tooMedia Services</span></span>
<span data-ttu-id="361bf-108">tooconnect tooMedia usług programowo, możesz musi mieć wcześniej skonfigurowane konto platformy Azure, skonfigurowane na tym koncie usługi Media Services i następnie ponowne skonfigurowanie projektu programu Visual Studio do tworzenia aplikacji z hello SDK usługi Media Services dla platformy .NET.</span><span class="sxs-lookup"><span data-stu-id="361bf-108">tooconnect tooMedia Services programmatically, you must have previously set up an Azure account, configured Media Services on that account, and then set up a Visual Studio project for development with hello Media Services SDK for .NET.</span></span> <span data-ttu-id="361bf-109">Aby uzyskać więcej informacji zobacz ustawień dla rozwoju z hello SDK usługi Media Services dla platformy .NET.</span><span class="sxs-lookup"><span data-stu-id="361bf-109">For more information, see Setup for Development with hello Media Services SDK for .NET.</span></span>

<span data-ttu-id="361bf-110">Na końcu procesu instalacji konta usługi Media Services hello hello, uzyskać następujące hello wymagane wartości połączenia.</span><span class="sxs-lookup"><span data-stu-id="361bf-110">At hello end of hello Media Services account setup process, you obtained hello following required connection values.</span></span> <span data-ttu-id="361bf-111">Użyj tych połączeń programowe toomake tooMedia usług.</span><span class="sxs-lookup"><span data-stu-id="361bf-111">Use these toomake programmatic connections tooMedia Services.</span></span>

* <span data-ttu-id="361bf-112">Nazwa konta usługi Media Services.</span><span class="sxs-lookup"><span data-stu-id="361bf-112">Your Media Services account name.</span></span>
* <span data-ttu-id="361bf-113">Klucz konta usługi Media Services.</span><span class="sxs-lookup"><span data-stu-id="361bf-113">Your Media Services account key.</span></span>

<span data-ttu-id="361bf-114">te wartości, toofind Przejdź toohello portalu zarządzania Azure, wybierz konto usługi multimediów i kliknij pozycję hello "**Zarządzanie KLUCZAMI**" ikonę na powitania dolnej części okna portalu hello.</span><span class="sxs-lookup"><span data-stu-id="361bf-114">toofind these values, go toohello Azure Managment Portal, select your Media Service account, and click on hello “**MANAGE KEYS**” icon on hello bottom of hello portal window.</span></span> <span data-ttu-id="361bf-115">Kliknięcie hello ikona dalej tooeach tekst pola kopie hello wartość toohello schowka systemowego.</span><span class="sxs-lookup"><span data-stu-id="361bf-115">Clicking on hello icon next tooeach text box copies hello value toohello system clipboard.</span></span>

## <a name="creating-a-cloudmediacontext-instance"></a><span data-ttu-id="361bf-116">Tworzenie wystąpienia CloudMediaContext</span><span class="sxs-lookup"><span data-stu-id="361bf-116">Creating a CloudMediaContext Instance</span></span>
<span data-ttu-id="361bf-117">Programowanie w odniesieniu do Media Services potrzebne toocreate toostart **CloudMediaContext** wystąpienie reprezentującego hello kontekstu serwera.</span><span class="sxs-lookup"><span data-stu-id="361bf-117">toostart programming against Media Services you need toocreate a **CloudMediaContext** instance that represents hello server context.</span></span> <span data-ttu-id="361bf-118">Witaj **CloudMediaContext** zawiera odwołania do kolekcji tooimportant tym zadań, zasobów, plików, zasady dostępu i lokalizatorów.</span><span class="sxs-lookup"><span data-stu-id="361bf-118">hello **CloudMediaContext** includes references tooimportant collections including jobs, assets, files, access policies, and locators.</span></span>

> [!NOTE]
> <span data-ttu-id="361bf-119">Witaj **CloudMediaContext** klasa nie jest bezpieczne dla wątków.</span><span class="sxs-lookup"><span data-stu-id="361bf-119">hello **CloudMediaContext** class is not thread safe.</span></span> <span data-ttu-id="361bf-120">Należy utworzyć nowe CloudMediaContext na wątku lub zestaw operacji.</span><span class="sxs-lookup"><span data-stu-id="361bf-120">You should create a new CloudMediaContext per thread or per set of operations.</span></span>
> 
> 

<span data-ttu-id="361bf-121">CloudMediaContext ma pięć przeciążeń konstruktora.</span><span class="sxs-lookup"><span data-stu-id="361bf-121">CloudMediaContext has five constructor overloads.</span></span> <span data-ttu-id="361bf-122">Jest zalecana toouse konstruktorów **MediaServicesCredentials** jako parametr.</span><span class="sxs-lookup"><span data-stu-id="361bf-122">It is recommended toouse constructors that take **MediaServicesCredentials** as a parameter.</span></span> <span data-ttu-id="361bf-123">Aby uzyskać więcej informacji, zobacz hello **ponowne użycie tokeny usługi kontroli dostępu** znajdujący się na ścieżce.</span><span class="sxs-lookup"><span data-stu-id="361bf-123">For more information, see hello **Reusing Access Control Service Tokens** that follows.</span></span> 

<span data-ttu-id="361bf-124">Witaj poniższym przykładzie użyto publicznego konstruktora CloudMediaContext(MediaServicesCredentials credentials) hello:</span><span class="sxs-lookup"><span data-stu-id="361bf-124">hello following example uses hello public CloudMediaContext(MediaServicesCredentials credentials) constructor:</span></span>

    // _cachedCredentials and _context are class member variables. 
    _cachedCredentials = new MediaServicesCredentials(
                    _mediaServicesAccountName,
                    _mediaServicesAccountKey);

    _context = new CloudMediaContext(_cachedCredentials);


## <a name="reusing-access-control-service-tokens"></a><span data-ttu-id="361bf-125">Ponowne wykorzystywanie tokeny usługi kontroli dostępu</span><span class="sxs-lookup"><span data-stu-id="361bf-125">Reusing Access Control Service Tokens</span></span>
<span data-ttu-id="361bf-126">W tej sekcji przedstawiono, jak tokeny tooreuse usłudze kontroli dostępu za pomocą konstruktorów CloudMediaContext MediaServicesCredentials jako parametr.</span><span class="sxs-lookup"><span data-stu-id="361bf-126">This section shows how tooreuse Access Control Service tokens by using CloudMediaContext constructors that take MediaServicesCredentials as a parameter.</span></span>

<span data-ttu-id="361bf-127">[Azure kontroli dostępu Active Directory](https://msdn.microsoft.com/library/hh147631.aspx) (znanej także jako usługa kontroli dostępu lub ACS) to usługa oparta na chmurze, która zapewnia prosty sposób uwierzytelniania i autoryzowanie dostępu toogain użytkowników aplikacji sieci web tootheir.</span><span class="sxs-lookup"><span data-stu-id="361bf-127">[Azure Active Directory Access Control](https://msdn.microsoft.com/library/hh147631.aspx) (also known as Access Control Service or ACS) is a cloud-based service that provides an easy way of authenticating and authorizing users toogain access tootheir web applications.</span></span> <span data-ttu-id="361bf-128">Microsoft Azure Media Services kontroluje dostęp usługi tooits jednak protokołu OAuth, która wymaga tokenu usługi ACS.</span><span class="sxs-lookup"><span data-stu-id="361bf-128">Microsoft Azure Media Services controls access tooits services though OAuth protocol that requires an ACS token.</span></span> <span data-ttu-id="361bf-129">Usługa Media Services odbiera hello ACS tokenów z serwera autoryzacji.</span><span class="sxs-lookup"><span data-stu-id="361bf-129">Media Services receives hello ACS tokens from an authorization server.</span></span>

<span data-ttu-id="361bf-130">Podczas tworzenia z hello SDK usługi Media Services, można wybrać toonot transakcji z tokenami hello, ponieważ hello menedżerów kod zestawu SDK je automatycznie.</span><span class="sxs-lookup"><span data-stu-id="361bf-130">When developing with hello Media Services SDK, you can choose toonot deal with hello tokens because hello SDK code managers them for you.</span></span> <span data-ttu-id="361bf-131">Jednak dzięki czemu hello zestawu SDK w pełni zarządzać hello ACS tokeny potencjalnych klientów toounnecessary żądań dotyczących tokenów.</span><span class="sxs-lookup"><span data-stu-id="361bf-131">However, letting hello SDK fully manage hello ACS tokens leads toounnecessary token requests.</span></span> <span data-ttu-id="361bf-132">Żądania tokenów jest czasochłonne i wykorzystuje zasoby powitania klienta i serwera.</span><span class="sxs-lookup"><span data-stu-id="361bf-132">Requesting tokens takes time and consumes hello client and server resources.</span></span> <span data-ttu-id="361bf-133">Ponadto serwer usług ACS hello ogranicza żądań hello Jeśli częstotliwość hello jest zbyt wysoka.</span><span class="sxs-lookup"><span data-stu-id="361bf-133">Also, hello ACS server throttles hello requests if hello rate is too high.</span></span> <span data-ttu-id="361bf-134">Witaj limit wynosi 30 żądań na sekundę, zobacz [ograniczenia usługi ACS](https://msdn.microsoft.com/library/gg185909.aspx) więcej szczegółów.</span><span class="sxs-lookup"><span data-stu-id="361bf-134">hello limit is 30 requests per second, see [ACS Service Limitations](https://msdn.microsoft.com/library/gg185909.aspx) for more details.</span></span>

<span data-ttu-id="361bf-135">Począwszy od zestawu SDK usługi Media Services w wersji 3.0.0.0 hello, można użyć ponownie hello ACS tokenów.</span><span class="sxs-lookup"><span data-stu-id="361bf-135">Starting with hello Media Services SDK version 3.0.0.0, you can reuse hello ACS tokens.</span></span> <span data-ttu-id="361bf-136">Witaj **CloudMediaContext** konstruktorów przyjmujących **MediaServicesCredentials** jako parametr włączyć udostępniania hello ACS tokeny od wielu kontekstów.</span><span class="sxs-lookup"><span data-stu-id="361bf-136">hello **CloudMediaContext** constructors that take **MediaServicesCredentials** as a parameter enable sharing hello ACS tokens between multiple contexts.</span></span> <span data-ttu-id="361bf-137">Witaj MediaServicesCredentials klasa hermetyzuje hello poświadczenia usługi Media Services.</span><span class="sxs-lookup"><span data-stu-id="361bf-137">hello MediaServicesCredentials class encapsulates hello Media Services credentials.</span></span> <span data-ttu-id="361bf-138">Jeśli tokenu usługi ACS jest dostępny, a jego czas wygaśnięcia jest znany, można utworzenia nowego wystąpienia MediaServicesCredentials z tokenem hello i przekaż go konstruktora toohello CloudMediaContext.</span><span class="sxs-lookup"><span data-stu-id="361bf-138">If an ACS token is available and its expiration time is known, you can create a new MediaServicesCredentials instance with hello token and pass it toohello constructor of CloudMediaContext.</span></span> <span data-ttu-id="361bf-139">Należy pamiętać, że hello SDK usługi Media Services automatycznie odświeża tokenów, gdy wygasną.</span><span class="sxs-lookup"><span data-stu-id="361bf-139">Note that hello Media Services SDK automatically refreshes tokens whenever they expire.</span></span> <span data-ttu-id="361bf-140">Istnieją dwa sposoby tooreuse tokenów usług ACS, jak pokazano w poniższych przykładach hello.</span><span class="sxs-lookup"><span data-stu-id="361bf-140">There are two ways tooreuse ACS tokens, as shown in hello examples below.</span></span>

* <span data-ttu-id="361bf-141">Może buforować hello **MediaServicesCredentials** obiektu w pamięci (na przykład klasa statyczna zmienna).</span><span class="sxs-lookup"><span data-stu-id="361bf-141">You can cache hello **MediaServicesCredentials** object in memory (for example, in a static class variable).</span></span> <span data-ttu-id="361bf-142">Przekazuj konstruktora CloudMediaContext toohello obiektów hello w pamięci podręcznej.</span><span class="sxs-lookup"><span data-stu-id="361bf-142">Then, pass hello cached object toohello CloudMediaContext constructor.</span></span> <span data-ttu-id="361bf-143">Obiekt MediaServicesCredentials Hello zawiera tokenu usługi ACS, która może nastąpić, jeśli jest nadal ważny.</span><span class="sxs-lookup"><span data-stu-id="361bf-143">hello MediaServicesCredentials object contains an ACS token that can be reused if it is still valid.</span></span> <span data-ttu-id="361bf-144">Jeśli hello token jest nieprawidłowy, zostaną odświeżone przez hello SDK usługi Media Services przy użyciu poświadczeń hello danego toohello MediaServicesCredentials konstruktora.</span><span class="sxs-lookup"><span data-stu-id="361bf-144">If hello token is not valid, it will be refreshed by hello Media Services SDK using hello credentials given toohello MediaServicesCredentials constructor.</span></span>
  
    <span data-ttu-id="361bf-145">Należy pamiętać, że hello **MediaServicesCredentials** obiektu pobiera prawidłowy token po hello RefreshToken jest wywoływana.</span><span class="sxs-lookup"><span data-stu-id="361bf-145">Note that hello **MediaServicesCredentials** object gets a valid token after hello RefreshToken is called.</span></span> <span data-ttu-id="361bf-146">Witaj **CloudMediaContext** hello wywołania **RefreshToken** metody w Konstruktorze hello.</span><span class="sxs-lookup"><span data-stu-id="361bf-146">hello **CloudMediaContext** calls hello **RefreshToken** method in hello constructor.</span></span> <span data-ttu-id="361bf-147">Jeśli planujesz toosave hello wartości tokenów tooan zewnętrznych urządzeń pamięci masowej, upewnij się toocheck czy hello TokenExpiration wartość jest prawidłowa przed zapisaniem danych tokenu hello.</span><span class="sxs-lookup"><span data-stu-id="361bf-147">If you are planning toosave hello token values tooan external storage, make sure toocheck whether hello TokenExpiration value is valid before saving hello token data.</span></span> <span data-ttu-id="361bf-148">Jeśli nie jest prawidłowy, należy wywołać RefreshToken przed buforowania.</span><span class="sxs-lookup"><span data-stu-id="361bf-148">If it is not valid, call RefreshToken before caching.</span></span>
  
        // Create and cache hello Media Services credentials in a static class variable.
        _cachedCredentials = new MediaServicesCredentials(_mediaServicesAccountName, _mediaServicesAccountKey);

        // Use hello cached credentials toocreate a new CloudMediaContext object.
        if(_cachedCredentials == null)
        {
            _cachedCredentials = new MediaServicesCredentials(_mediaServicesAccountName, _mediaServicesAccountKey);
        }

        CloudMediaContext context = new CloudMediaContext(_cachedCredentials);

* <span data-ttu-id="361bf-149">Można buforować hello AccessToken ciągu i hello TokenExpiration wartości.</span><span class="sxs-lookup"><span data-stu-id="361bf-149">You can also cache hello AccessToken string and hello TokenExpiration values.</span></span> <span data-ttu-id="361bf-150">wartości Hello później może być używane toocreate MediaServicesCredentials nowy obiekt z hello w pamięci podręcznej danych tokenu.</span><span class="sxs-lookup"><span data-stu-id="361bf-150">hello values could later be used toocreate a new MediaServicesCredentials object with hello cached token data.</span></span>  <span data-ttu-id="361bf-151">Jest to szczególnie przydatne w scenariuszach, gdzie hello token można bezpiecznie wymieniać między wiele procesów lub komputery.</span><span class="sxs-lookup"><span data-stu-id="361bf-151">This is especially useful for scenarios where hello token can be securely shared among multiple processes or computers.</span></span>
  
    <span data-ttu-id="361bf-152">Witaj poniższe fragmenty kodu wywołać hello SaveTokenDataToExternalStorage, GetTokenDataFromExternalStorage i UpdateTokenDataInExternalStorageIfNeeded metody, które nie są zdefiniowane w tym przykładzie.</span><span class="sxs-lookup"><span data-stu-id="361bf-152">hello following code snippets call hello SaveTokenDataToExternalStorage, GetTokenDataFromExternalStorage, and UpdateTokenDataInExternalStorageIfNeeded methods that are not defined in this example.</span></span> <span data-ttu-id="361bf-153">W pamięci zewnętrznej, można zdefiniować te toostore metod, pobieranie i aktualizacji danych tokenu.</span><span class="sxs-lookup"><span data-stu-id="361bf-153">You could define these methods toostore, retrieve, and update token data in an external storage.</span></span> 
  
        CloudMediaContext context1 = new CloudMediaContext(_mediaServicesAccountName, _mediaServicesAccountKey);
  
        // Get token values from hello context.
        var accessToken = context1.Credentials.AccessToken;
        var tokenExpiration = context1.Credentials.TokenExpiration;
  
        // Save token values for later use. 
        // hello SaveTokenDataToExternalStorage method should check 
        // whether hello TokenExpiration value is valid before saving hello token data. 
        // If it is not valid, call MediaServicesCredentials’s RefreshToken before caching.
        SaveTokenDataToExternalStorage(accessToken, tokenExpiration);
  
    <span data-ttu-id="361bf-154">Użyj hello zapisane wartości tokenów toocreate MediaServicesCredentials.</span><span class="sxs-lookup"><span data-stu-id="361bf-154">Use hello saved token values toocreate MediaServicesCredentials.</span></span>

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

    <span data-ttu-id="361bf-155">W przypadku, gdy hello token został zaktualizowany przez hello SDK usługi Media Services, należy zaktualizować hello tokenu kopię.</span><span class="sxs-lookup"><span data-stu-id="361bf-155">Update hello token copy in case hello token was updated by hello Media Services SDK.</span></span> 

        if(tokenExpiration != context2.Credentials.TokenExpiration)
        {
            UpdateTokenDataInExternalStorageIfNeeded(accessToken, context2.Credentials.TokenExpiration);
        }


* <span data-ttu-id="361bf-156">Jeśli masz wiele kont usługi Media Services (na przykład w przypadku udostępniania celów lub geograficznie dystrybucji obciążenia) może buforować MediaServicesCredentials obiektów przy użyciu kolekcji System.Collections.Concurrent.ConcurrentDictionary hello (hello Obiekt ConcurrentDictionary kolekcji reprezentuje kolekcję wątkowo pary klucz wartość, które mogą być udostępniane przez wiele wątków jednocześnie).</span><span class="sxs-lookup"><span data-stu-id="361bf-156">If you have multiple Media Services accounts (for example, for load sharing purposes or Geo-distribution) you can cache MediaServicesCredentials objects using hello System.Collections.Concurrent.ConcurrentDictionary collection (hello ConcurrentDictionary collection represents a thread-safe collection of key/value pairs that can be accessed by multiple threads concurrently).</span></span> <span data-ttu-id="361bf-157">Następnie można hello GetOrAdd metody tooget hello buforowanych poświadczeń.</span><span class="sxs-lookup"><span data-stu-id="361bf-157">You can then use hello GetOrAdd method tooget hello cached credentials.</span></span> 
  
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

## <a name="connecting-tooa-media-services-account-located-in-hello-north-china-region"></a><span data-ttu-id="361bf-158">Łączenie tooa konta usługi Media Services znajdującego się w regionie Północna Chin hello</span><span class="sxs-lookup"><span data-stu-id="361bf-158">Connecting tooa Media Services account located in hello North China region</span></span>
<span data-ttu-id="361bf-159">Twoje konto znajduje się w regionie Północna Chin hello, należy użyć następującego konstruktora hello:</span><span class="sxs-lookup"><span data-stu-id="361bf-159">If your account is located in hello North China region, use hello following constructor:</span></span>

    public CloudMediaContext(Uri apiServer, string accountName, string accountKey, string scope, string acsBaseAddress)

<span data-ttu-id="361bf-160">Na przykład:</span><span class="sxs-lookup"><span data-stu-id="361bf-160">For example:</span></span>

    _context = new CloudMediaContext(
        new Uri("https://wamsbjbclus001rest-hs.chinacloudapp.cn/API/"),
        _mediaServicesAccountName,
        _mediaServicesAccountKey,
        "urn:WindowsAzureMediaServices",
        "https://wamsprodglobal001acs.accesscontrol.chinacloudapi.cn");


## <a name="storing-connection-values-in-configuration"></a><span data-ttu-id="361bf-161">Przechowywanie wartości połączenia w konfiguracji</span><span class="sxs-lookup"><span data-stu-id="361bf-161">Storing Connection Values in Configuration</span></span>
<span data-ttu-id="361bf-162">Jest stanowczo zalecane praktyki toostore połączenia wartości, szczególnie poufnych takie jak nazwa konta i hasło w konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="361bf-162">It is a highly recommended practice toostore connection values, especially sensitive values such as your account name and password, in configuration.</span></span> <span data-ttu-id="361bf-163">Jest także zalecana praktyka tooencrypt poufne dane konfiguracyjne.</span><span class="sxs-lookup"><span data-stu-id="361bf-163">Also, it is a recommended practice tooencrypt sensitive configuration data.</span></span> <span data-ttu-id="361bf-164">Plik konfiguracji całego hello można szyfrować przy użyciu hello Windows System szyfrowania plików (EFS).</span><span class="sxs-lookup"><span data-stu-id="361bf-164">You can encrypt hello entire configuration file by using hello Windows Encrypting File System (EFS).</span></span> <span data-ttu-id="361bf-165">Wybierz tooenable systemu szyfrowania plików w pliku, kliknij prawym przyciskiem myszy plik hello, **właściwości**i włączenia szyfrowania w hello **zaawansowane** kartę Ustawienia. Lub można utworzyć niestandardowego rozwiązania do szyfrowania przy użyciu konfiguracji chronionych zaznaczonych części pliku konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="361bf-165">tooenable EFS on a file, right-click hello file, select **Properties**, and enable encryption in hello **Advanced** settings tab. Or you can create a custom solution for encrypting selected portions of a configuration file by using protected configuration.</span></span> <span data-ttu-id="361bf-166">Zobacz [szyfrowania za pomocą konfiguracji chronionych informacji o konfiguracji](https://msdn.microsoft.com/library/53tyfkaw.aspx).</span><span class="sxs-lookup"><span data-stu-id="361bf-166">See [Encrypting Configuration Information Using Protected Configuration](https://msdn.microsoft.com/library/53tyfkaw.aspx).</span></span>

<span data-ttu-id="361bf-167">Hello następującego pliku App.config zawiera hello wymagane wartości połączenia.</span><span class="sxs-lookup"><span data-stu-id="361bf-167">hello following App.config file contains hello required connection values.</span></span> <span data-ttu-id="361bf-168">Witaj wartości hello <appSettings> hello wymagane wartości, które masz od procesu konfiguracji konta usługi Media Services hello są elementu.</span><span class="sxs-lookup"><span data-stu-id="361bf-168">hello values in hello <appSettings> element are hello required values that you got from hello Media Services account setup process.</span></span>

    <configuration>
      <appSettings>
        <add key="MediaServicesAccountName" value="Media-Services-Account-Name" />
        <add key="MediaServicesAccountKey" value="Media-Services-Account-Key" />
      </appSettings>
    </configuration>


<span data-ttu-id="361bf-169">wartości połączenia tooretrieve z konfiguracji, można użyć hello **ConfigurationManager** klasy, a następnie przypisz hello toofields wartości w kodzie:</span><span class="sxs-lookup"><span data-stu-id="361bf-169">tooretrieve connection values from configuration, you can use hello **ConfigurationManager** class and then assign hello values toofields in your code:</span></span>

    private static readonly string _accountName = ConfigurationManager.AppSettings["MediaServicesAccountName"];
    private static readonly string _accountKey = ConfigurationManager.AppSettings["MediaServicesAccountKey"];



## <a name="media-services-learning-paths"></a><span data-ttu-id="361bf-170">Ścieżki szkoleniowe dotyczące usługi Media Services</span><span class="sxs-lookup"><span data-stu-id="361bf-170">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="361bf-171">Przekazywanie opinii</span><span class="sxs-lookup"><span data-stu-id="361bf-171">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

