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
# <a name="connecting-to-media-services-account-using-media-services-sdk-for-net"></a><span data-ttu-id="1a5e6-103">Łączenie z konta usługi Media Services przy użyciu zestawu SDK usługi Media Services dla platformy .NET</span><span class="sxs-lookup"><span data-stu-id="1a5e6-103">Connecting to Media Services Account using Media Services SDK for .NET</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="1a5e6-104">REST</span><span class="sxs-lookup"><span data-stu-id="1a5e6-104">REST</span></span>](media-services-rest-connect-programmatically.md)
> * [<span data-ttu-id="1a5e6-105">.NET</span><span class="sxs-lookup"><span data-stu-id="1a5e6-105">.NET</span></span>](media-services-dotnet-connect-programmatically.md)
> 
> 

<span data-ttu-id="1a5e6-106">W tym temacie opisano sposób uzyskiwania połączenie programowe Microsoft Azure Media Services są programowania się przy użyciu zestawu SDK usługi multimediów dla platformy .NET.</span><span class="sxs-lookup"><span data-stu-id="1a5e6-106">This topic describes how to obtain a programmatic connection to Microsoft Azure Media Services when you are programming with the Media Services SDK for .NET.</span></span>

## <a name="connecting-to-media-services"></a><span data-ttu-id="1a5e6-107">Nawiązywanie połączenia z usługi Media Services</span><span class="sxs-lookup"><span data-stu-id="1a5e6-107">Connecting to Media Services</span></span>
<span data-ttu-id="1a5e6-108">Połącz się z usługi Media Services programowo, możesz musi mieć wcześniej skonfigurowane konto platformy Azure, skonfigurowane na tym koncie usługi Media Services i następnie ponowne skonfigurowanie projektu programu Visual Studio do tworzenia aplikacji przy użyciu zestawu SDK usługi multimediów dla platformy .NET.</span><span class="sxs-lookup"><span data-stu-id="1a5e6-108">To connect to Media Services programmatically, you must have previously set up an Azure account, configured Media Services on that account, and then set up a Visual Studio project for development with the Media Services SDK for .NET.</span></span> <span data-ttu-id="1a5e6-109">Aby uzyskać więcej informacji Zobacz Instalator do tworzenia aplikacji przy użyciu zestawu SDK usługi multimediów dla platformy .NET.</span><span class="sxs-lookup"><span data-stu-id="1a5e6-109">For more information, see Setup for Development with the Media Services SDK for .NET.</span></span>

<span data-ttu-id="1a5e6-110">Na końcu procesu instalacji konta usługi Media Services uzyskany następujące wartości wymagane połączenia.</span><span class="sxs-lookup"><span data-stu-id="1a5e6-110">At the end of the Media Services account setup process, you obtained the following required connection values.</span></span> <span data-ttu-id="1a5e6-111">Użyj tych tworzyć programowe połączenia z usługi Media Services.</span><span class="sxs-lookup"><span data-stu-id="1a5e6-111">Use these to make programmatic connections to Media Services.</span></span>

* <span data-ttu-id="1a5e6-112">Nazwa konta usługi Media Services.</span><span class="sxs-lookup"><span data-stu-id="1a5e6-112">Your Media Services account name.</span></span>
* <span data-ttu-id="1a5e6-113">Klucz konta usługi Media Services.</span><span class="sxs-lookup"><span data-stu-id="1a5e6-113">Your Media Services account key.</span></span>

<span data-ttu-id="1a5e6-114">Aby znaleźć te wartości, przejdź do portalu zarządzania Azure, wybierz konto usługi multimediów, a następnie kliknij polecenie "**Zarządzanie KLUCZAMI**" ikony w dolnej części okna portalu.</span><span class="sxs-lookup"><span data-stu-id="1a5e6-114">To find these values, go to the Azure Managment Portal, select your Media Service account, and click on the “**MANAGE KEYS**” icon on the bottom of the portal window.</span></span> <span data-ttu-id="1a5e6-115">Kliknięcie ikony obok każdego pola tekstowego powoduje skopiowanie wartości do schowka systemowego.</span><span class="sxs-lookup"><span data-stu-id="1a5e6-115">Clicking on the icon next to each text box copies the value to the system clipboard.</span></span>

## <a name="creating-a-cloudmediacontext-instance"></a><span data-ttu-id="1a5e6-116">Tworzenie wystąpienia CloudMediaContext</span><span class="sxs-lookup"><span data-stu-id="1a5e6-116">Creating a CloudMediaContext Instance</span></span>
<span data-ttu-id="1a5e6-117">Aby rozpocząć Programowanie w odniesieniu do usługi Media Services, musisz utworzyć **CloudMediaContext** wystąpienia, który reprezentuje kontekstu serwera.</span><span class="sxs-lookup"><span data-stu-id="1a5e6-117">To start programming against Media Services you need to create a **CloudMediaContext** instance that represents the server context.</span></span> <span data-ttu-id="1a5e6-118">**CloudMediaContext** zawiera odwołania do kolekcji ważne, łącznie z zadań, zasobów, plików, zasady dostępu i lokalizatorów.</span><span class="sxs-lookup"><span data-stu-id="1a5e6-118">The **CloudMediaContext** includes references to important collections including jobs, assets, files, access policies, and locators.</span></span>

> [!NOTE]
> <span data-ttu-id="1a5e6-119">**CloudMediaContext** klasa nie jest bezpieczne dla wątków.</span><span class="sxs-lookup"><span data-stu-id="1a5e6-119">The **CloudMediaContext** class is not thread safe.</span></span> <span data-ttu-id="1a5e6-120">Należy utworzyć nowe CloudMediaContext na wątku lub zestaw operacji.</span><span class="sxs-lookup"><span data-stu-id="1a5e6-120">You should create a new CloudMediaContext per thread or per set of operations.</span></span>
> 
> 

<span data-ttu-id="1a5e6-121">CloudMediaContext ma pięć przeciążeń konstruktora.</span><span class="sxs-lookup"><span data-stu-id="1a5e6-121">CloudMediaContext has five constructor overloads.</span></span> <span data-ttu-id="1a5e6-122">Zalecane jest użycie konstruktorów przyjmujących **MediaServicesCredentials** jako parametr.</span><span class="sxs-lookup"><span data-stu-id="1a5e6-122">It is recommended to use constructors that take **MediaServicesCredentials** as a parameter.</span></span> <span data-ttu-id="1a5e6-123">Aby uzyskać więcej informacji, zobacz **ponowne użycie tokeny usługi kontroli dostępu** znajdujący się na ścieżce.</span><span class="sxs-lookup"><span data-stu-id="1a5e6-123">For more information, see the **Reusing Access Control Service Tokens** that follows.</span></span> 

<span data-ttu-id="1a5e6-124">W poniższym przykładzie użyto publicznego konstruktora CloudMediaContext(MediaServicesCredentials credentials):</span><span class="sxs-lookup"><span data-stu-id="1a5e6-124">The following example uses the public CloudMediaContext(MediaServicesCredentials credentials) constructor:</span></span>

    // _cachedCredentials and _context are class member variables. 
    _cachedCredentials = new MediaServicesCredentials(
                    _mediaServicesAccountName,
                    _mediaServicesAccountKey);

    _context = new CloudMediaContext(_cachedCredentials);


## <a name="reusing-access-control-service-tokens"></a><span data-ttu-id="1a5e6-125">Ponowne wykorzystywanie tokeny usługi kontroli dostępu</span><span class="sxs-lookup"><span data-stu-id="1a5e6-125">Reusing Access Control Service Tokens</span></span>
<span data-ttu-id="1a5e6-126">W tej sekcji przedstawiono sposób ponownego użycia tokenów w usłudze kontroli dostępu za pomocą konstruktorów CloudMediaContext MediaServicesCredentials jako parametr.</span><span class="sxs-lookup"><span data-stu-id="1a5e6-126">This section shows how to reuse Access Control Service tokens by using CloudMediaContext constructors that take MediaServicesCredentials as a parameter.</span></span>

<span data-ttu-id="1a5e6-127">[Azure kontroli dostępu Active Directory](https://msdn.microsoft.com/library/hh147631.aspx) (znanej także jako usługa kontroli dostępu lub ACS) jest oparta na chmurze usługi, która zapewnia łatwy sposób uwierzytelniania i autoryzacji użytkowników uzyskujących dostęp do aplikacji sieci web.</span><span class="sxs-lookup"><span data-stu-id="1a5e6-127">[Azure Active Directory Access Control](https://msdn.microsoft.com/library/hh147631.aspx) (also known as Access Control Service or ACS) is a cloud-based service that provides an easy way of authenticating and authorizing users to gain access to their web applications.</span></span> <span data-ttu-id="1a5e6-128">Microsoft Azure Media Services kontroluje dostęp do swoich usług jednak protokołu OAuth, która wymaga tokenu usługi ACS.</span><span class="sxs-lookup"><span data-stu-id="1a5e6-128">Microsoft Azure Media Services controls access to its services though OAuth protocol that requires an ACS token.</span></span> <span data-ttu-id="1a5e6-129">Usługa Media Services odbiera tokenów usług ACS z serwera autoryzacji.</span><span class="sxs-lookup"><span data-stu-id="1a5e6-129">Media Services receives the ACS tokens from an authorization server.</span></span>

<span data-ttu-id="1a5e6-130">Podczas tworzenia przy użyciu zestawu SDK usługi multimediów, użytkownik może nie dotyczyć tokenów, ponieważ zestaw SDK kodu menedżerów je automatycznie.</span><span class="sxs-lookup"><span data-stu-id="1a5e6-130">When developing with the Media Services SDK, you can choose to not deal with the tokens because the SDK code managers them for you.</span></span> <span data-ttu-id="1a5e6-131">Jednak SDK tokeny ACS w pełni zarządzać co prowadzi do niepotrzebnych żądania tokenu.</span><span class="sxs-lookup"><span data-stu-id="1a5e6-131">However, letting the SDK fully manage the ACS tokens leads to unnecessary token requests.</span></span> <span data-ttu-id="1a5e6-132">Żądania tokenów jest czasochłonne i wykorzystuje zasoby klienta i serwera.</span><span class="sxs-lookup"><span data-stu-id="1a5e6-132">Requesting tokens takes time and consumes the client and server resources.</span></span> <span data-ttu-id="1a5e6-133">Ponadto serwer usług ACS ogranicza żądania, jeżeli stawki jest zbyt duża.</span><span class="sxs-lookup"><span data-stu-id="1a5e6-133">Also, the ACS server throttles the requests if the rate is too high.</span></span> <span data-ttu-id="1a5e6-134">Limit wynosi 30 żądań na sekundę, zobacz [ograniczenia usługi ACS](https://msdn.microsoft.com/library/gg185909.aspx) więcej szczegółów.</span><span class="sxs-lookup"><span data-stu-id="1a5e6-134">The limit is 30 requests per second, see [ACS Service Limitations](https://msdn.microsoft.com/library/gg185909.aspx) for more details.</span></span>

<span data-ttu-id="1a5e6-135">Począwszy od zestawu SDK usługi Media wersji 3.0.0.0, można użyć ponownie tokenów usług ACS.</span><span class="sxs-lookup"><span data-stu-id="1a5e6-135">Starting with the Media Services SDK version 3.0.0.0, you can reuse the ACS tokens.</span></span> <span data-ttu-id="1a5e6-136">**CloudMediaContext** konstruktorów przyjmujących **MediaServicesCredentials** jako parametr Włącz udostępnianie ACS tokeny od wielu kontekstów.</span><span class="sxs-lookup"><span data-stu-id="1a5e6-136">The **CloudMediaContext** constructors that take **MediaServicesCredentials** as a parameter enable sharing the ACS tokens between multiple contexts.</span></span> <span data-ttu-id="1a5e6-137">Klasa MediaServicesCredentials hermetyzuje poświadczenia usługi Media Services.</span><span class="sxs-lookup"><span data-stu-id="1a5e6-137">The MediaServicesCredentials class encapsulates the Media Services credentials.</span></span> <span data-ttu-id="1a5e6-138">Jeśli tokenu usługi ACS jest dostępny, a jego czas wygaśnięcia jest znany, można tworzyć nowe wystąpienie MediaServicesCredentials z tokenem i przekazywany do konstruktora CloudMediaContext.</span><span class="sxs-lookup"><span data-stu-id="1a5e6-138">If an ACS token is available and its expiration time is known, you can create a new MediaServicesCredentials instance with the token and pass it to the constructor of CloudMediaContext.</span></span> <span data-ttu-id="1a5e6-139">Należy pamiętać, że SDK usługi Media Services automatycznie odświeża tokenów, gdy wygasną.</span><span class="sxs-lookup"><span data-stu-id="1a5e6-139">Note that the Media Services SDK automatically refreshes tokens whenever they expire.</span></span> <span data-ttu-id="1a5e6-140">Istnieją dwa sposoby ponowne tokenów usług ACS, jak pokazano w poniższych przykładach.</span><span class="sxs-lookup"><span data-stu-id="1a5e6-140">There are two ways to reuse ACS tokens, as shown in the examples below.</span></span>

* <span data-ttu-id="1a5e6-141">Można buforować **MediaServicesCredentials** obiektu w pamięci (na przykład klasa statyczna zmienna).</span><span class="sxs-lookup"><span data-stu-id="1a5e6-141">You can cache the **MediaServicesCredentials** object in memory (for example, in a static class variable).</span></span> <span data-ttu-id="1a5e6-142">Następnie przekaż obiektu w pamięci podręcznej do konstruktora CloudMediaContext.</span><span class="sxs-lookup"><span data-stu-id="1a5e6-142">Then, pass the cached object to the CloudMediaContext constructor.</span></span> <span data-ttu-id="1a5e6-143">Obiekt MediaServicesCredentials zawiera tokenu usługi ACS, która może nastąpić, jeśli jest nadal ważny.</span><span class="sxs-lookup"><span data-stu-id="1a5e6-143">The MediaServicesCredentials object contains an ACS token that can be reused if it is still valid.</span></span> <span data-ttu-id="1a5e6-144">Jeśli token nie jest prawidłowy, zostaną odświeżone przez zestaw SDK usługi Media za pomocą poświadczeń podanych do konstruktora MediaServicesCredentials.</span><span class="sxs-lookup"><span data-stu-id="1a5e6-144">If the token is not valid, it will be refreshed by the Media Services SDK using the credentials given to the MediaServicesCredentials constructor.</span></span>
  
    <span data-ttu-id="1a5e6-145">Należy pamiętać, że **MediaServicesCredentials** obiektu pobiera prawidłowy token po RefreshToken jest wywoływana.</span><span class="sxs-lookup"><span data-stu-id="1a5e6-145">Note that the **MediaServicesCredentials** object gets a valid token after the RefreshToken is called.</span></span> <span data-ttu-id="1a5e6-146">**CloudMediaContext** wywołania **RefreshToken** metody w konstruktorze.</span><span class="sxs-lookup"><span data-stu-id="1a5e6-146">The **CloudMediaContext** calls the **RefreshToken** method in the constructor.</span></span> <span data-ttu-id="1a5e6-147">Jeśli zamierzasz zapisać wartości tokenów w pamięci zewnętrznej, upewnij się sprawdzić, czy wartość TokenExpiration jest prawidłowa, przed zapisaniem danych tokenu.</span><span class="sxs-lookup"><span data-stu-id="1a5e6-147">If you are planning to save the token values to an external storage, make sure to check whether the TokenExpiration value is valid before saving the token data.</span></span> <span data-ttu-id="1a5e6-148">Jeśli nie jest prawidłowy, należy wywołać RefreshToken przed buforowania.</span><span class="sxs-lookup"><span data-stu-id="1a5e6-148">If it is not valid, call RefreshToken before caching.</span></span>
  
        // Create and cache the Media Services credentials in a static class variable.
        _cachedCredentials = new MediaServicesCredentials(_mediaServicesAccountName, _mediaServicesAccountKey);

        // Use the cached credentials to create a new CloudMediaContext object.
        if(_cachedCredentials == null)
        {
            _cachedCredentials = new MediaServicesCredentials(_mediaServicesAccountName, _mediaServicesAccountKey);
        }

        CloudMediaContext context = new CloudMediaContext(_cachedCredentials);

* <span data-ttu-id="1a5e6-149">Można buforować ciąg AccessToken i wartości TokenExpiration.</span><span class="sxs-lookup"><span data-stu-id="1a5e6-149">You can also cache the AccessToken string and the TokenExpiration values.</span></span> <span data-ttu-id="1a5e6-150">Później można użyć wartości do utworzenia nowego obiektu MediaServicesCredentials z pamięci podręcznej danych tokenu.</span><span class="sxs-lookup"><span data-stu-id="1a5e6-150">The values could later be used to create a new MediaServicesCredentials object with the cached token data.</span></span>  <span data-ttu-id="1a5e6-151">Jest to szczególnie przydatne w scenariuszach, gdzie token można bezpiecznie wymieniać między wiele procesów lub komputery.</span><span class="sxs-lookup"><span data-stu-id="1a5e6-151">This is especially useful for scenarios where the token can be securely shared among multiple processes or computers.</span></span>
  
    <span data-ttu-id="1a5e6-152">Poniższe fragmenty kodu wywoływać metod SaveTokenDataToExternalStorage, GetTokenDataFromExternalStorage i UpdateTokenDataInExternalStorageIfNeeded, które nie są zdefiniowane w tym przykładzie.</span><span class="sxs-lookup"><span data-stu-id="1a5e6-152">The following code snippets call the SaveTokenDataToExternalStorage, GetTokenDataFromExternalStorage, and UpdateTokenDataInExternalStorageIfNeeded methods that are not defined in this example.</span></span> <span data-ttu-id="1a5e6-153">Można zdefiniować tych metod, przechowywanie, pobieranie i aktualizację tokenu danych w pamięci zewnętrznej.</span><span class="sxs-lookup"><span data-stu-id="1a5e6-153">You could define these methods to store, retrieve, and update token data in an external storage.</span></span> 
  
        CloudMediaContext context1 = new CloudMediaContext(_mediaServicesAccountName, _mediaServicesAccountKey);
  
        // Get token values from the context.
        var accessToken = context1.Credentials.AccessToken;
        var tokenExpiration = context1.Credentials.TokenExpiration;
  
        // Save token values for later use. 
        // The SaveTokenDataToExternalStorage method should check 
        // whether the TokenExpiration value is valid before saving the token data. 
        // If it is not valid, call MediaServicesCredentials’s RefreshToken before caching.
        SaveTokenDataToExternalStorage(accessToken, tokenExpiration);
  
    <span data-ttu-id="1a5e6-154">Umożliwia utworzenie MediaServicesCredentials zapisanych wartości tokenu.</span><span class="sxs-lookup"><span data-stu-id="1a5e6-154">Use the saved token values to create MediaServicesCredentials.</span></span>

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

    <span data-ttu-id="1a5e6-155">W przypadku, gdy token został zaktualizowany przez SDK usługi Media Services, należy zaktualizować kopię tokenu.</span><span class="sxs-lookup"><span data-stu-id="1a5e6-155">Update the token copy in case the token was updated by the Media Services SDK.</span></span> 

        if(tokenExpiration != context2.Credentials.TokenExpiration)
        {
            UpdateTokenDataInExternalStorageIfNeeded(accessToken, context2.Credentials.TokenExpiration);
        }


* <span data-ttu-id="1a5e6-156">Jeśli masz wiele kont usługi Media Services (na przykład w przypadku udostępniania celów lub geograficznie dystrybucji obciążenia) może buforować MediaServicesCredentials obiektów przy użyciu kolekcji System.Collections.Concurrent.ConcurrentDictionary (kolekcji obiekt ConcurrentDictionary reprezentuje kolekcję wątkowo pary klucz wartość, które mogą być udostępniane przez wiele wątków jednocześnie).</span><span class="sxs-lookup"><span data-stu-id="1a5e6-156">If you have multiple Media Services accounts (for example, for load sharing purposes or Geo-distribution) you can cache MediaServicesCredentials objects using the System.Collections.Concurrent.ConcurrentDictionary collection (the ConcurrentDictionary collection represents a thread-safe collection of key/value pairs that can be accessed by multiple threads concurrently).</span></span> <span data-ttu-id="1a5e6-157">Metoda GetOrAdd umożliwia następnie Uzyskaj buforowanych poświadczeń.</span><span class="sxs-lookup"><span data-stu-id="1a5e6-157">You can then use the GetOrAdd method to get the cached credentials.</span></span> 
  
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

## <a name="connecting-to-a-media-services-account-located-in-the-north-china-region"></a><span data-ttu-id="1a5e6-158">Łączenie z kontem usługi Media Services znajdującego się w regionie Chin Północna</span><span class="sxs-lookup"><span data-stu-id="1a5e6-158">Connecting to a Media Services account located in the North China region</span></span>
<span data-ttu-id="1a5e6-159">Jeśli Twoje konto znajduje się w regionie Chin Północna, użyj Konstruktora następujące:</span><span class="sxs-lookup"><span data-stu-id="1a5e6-159">If your account is located in the North China region, use the following constructor:</span></span>

    public CloudMediaContext(Uri apiServer, string accountName, string accountKey, string scope, string acsBaseAddress)

<span data-ttu-id="1a5e6-160">Na przykład:</span><span class="sxs-lookup"><span data-stu-id="1a5e6-160">For example:</span></span>

    _context = new CloudMediaContext(
        new Uri("https://wamsbjbclus001rest-hs.chinacloudapp.cn/API/"),
        _mediaServicesAccountName,
        _mediaServicesAccountKey,
        "urn:WindowsAzureMediaServices",
        "https://wamsprodglobal001acs.accesscontrol.chinacloudapi.cn");


## <a name="storing-connection-values-in-configuration"></a><span data-ttu-id="1a5e6-161">Przechowywanie wartości połączenia w konfiguracji</span><span class="sxs-lookup"><span data-stu-id="1a5e6-161">Storing Connection Values in Configuration</span></span>
<span data-ttu-id="1a5e6-162">Jest bardzo zalecanym rozwiązaniem do przechowywania wartości połączenia, szczególnie ważne wartości, takie jak nazwa konta i hasło, w konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="1a5e6-162">It is a highly recommended practice to store connection values, especially sensitive values such as your account name and password, in configuration.</span></span> <span data-ttu-id="1a5e6-163">Ponadto jest zalecanym rozwiązaniem do szyfrowania danych poufnych konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="1a5e6-163">Also, it is a recommended practice to encrypt sensitive configuration data.</span></span> <span data-ttu-id="1a5e6-164">Plik całą konfigurację można zaszyfrować przy użyciu systemu szyfrowania plików systemu Windows (EFS).</span><span class="sxs-lookup"><span data-stu-id="1a5e6-164">You can encrypt the entire configuration file by using the Windows Encrypting File System (EFS).</span></span> <span data-ttu-id="1a5e6-165">Aby włączyć system szyfrowania plików do pliku, kliknij plik prawym przyciskiem myszy, wybierz **właściwości**i włączenia szyfrowania w **zaawansowane** kartę Ustawienia.</span><span class="sxs-lookup"><span data-stu-id="1a5e6-165">To enable EFS on a file, right-click the file, select **Properties**, and enable encryption in the **Advanced** settings tab.</span></span> <span data-ttu-id="1a5e6-166">Lub można utworzyć niestandardowego rozwiązania do szyfrowania przy użyciu konfiguracji chronionych zaznaczonych części pliku konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="1a5e6-166">Or you can create a custom solution for encrypting selected portions of a configuration file by using protected configuration.</span></span> <span data-ttu-id="1a5e6-167">Zobacz [szyfrowania za pomocą konfiguracji chronionych informacji o konfiguracji](https://msdn.microsoft.com/library/53tyfkaw.aspx).</span><span class="sxs-lookup"><span data-stu-id="1a5e6-167">See [Encrypting Configuration Information Using Protected Configuration](https://msdn.microsoft.com/library/53tyfkaw.aspx).</span></span>

<span data-ttu-id="1a5e6-168">Następujący plik App.config zawiera wartości wymagane połączenia.</span><span class="sxs-lookup"><span data-stu-id="1a5e6-168">The following App.config file contains the required connection values.</span></span> <span data-ttu-id="1a5e6-169">Wartości w <appSettings> elementu są wymagane wartości, otrzymanych proces konfigurowania konta usługi Media Services.</span><span class="sxs-lookup"><span data-stu-id="1a5e6-169">The values in the <appSettings> element are the required values that you got from the Media Services account setup process.</span></span>

    <configuration>
      <appSettings>
        <add key="MediaServicesAccountName" value="Media-Services-Account-Name" />
        <add key="MediaServicesAccountKey" value="Media-Services-Account-Key" />
      </appSettings>
    </configuration>


<span data-ttu-id="1a5e6-170">Aby pobrać wartości połączenia z konfiguracji, można użyć **ConfigurationManager** klasy, a następnie przypisać wartości do pola w kodzie:</span><span class="sxs-lookup"><span data-stu-id="1a5e6-170">To retrieve connection values from configuration, you can use the **ConfigurationManager** class and then assign the values to fields in your code:</span></span>

    private static readonly string _accountName = ConfigurationManager.AppSettings["MediaServicesAccountName"];
    private static readonly string _accountKey = ConfigurationManager.AppSettings["MediaServicesAccountKey"];



## <a name="media-services-learning-paths"></a><span data-ttu-id="1a5e6-171">Ścieżki szkoleniowe dotyczące usługi Media Services</span><span class="sxs-lookup"><span data-stu-id="1a5e6-171">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="1a5e6-172">Przekazywanie opinii</span><span class="sxs-lookup"><span data-stu-id="1a5e6-172">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

