---
title: aaaMFA software development kit aplikacji niestandardowych | Dokumentacja firmy Microsoft
description: "W tym artykule opisano, jak toodownload i użyj hello weryfikacji dwuetapowej tooenable zestawu SDK usługi Azure MFA dla aplikacji niestandardowych."
services: multi-factor-authentication
documentationcenter: 
author: kgremban
manager: femila
editor: yossib
ms.assetid: 1c152f67-be02-42a5-a0c7-246fb6b34377
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/03/2017
ms.author: kgremban
ms.openlocfilehash: 10e02e844bf3928575bfca79dbc34717a31a08b4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="building-multi-factor-authentication-into-custom-apps-sdk"></a><span data-ttu-id="ea559-103">Tworzenie usługi Multi-Factor Authentication w aplikacje niestandardowe (SDK)</span><span class="sxs-lookup"><span data-stu-id="ea559-103">Building Multi-Factor Authentication into Custom Apps (SDK)</span></span>

<span data-ttu-id="ea559-104">Transakcja procesów aplikacji w dzierżawie usługi Azure AD lub hello Hello Azure Multi-Factor Authentication Software Development Kit (SDK) umożliwia tworzenie weryfikacji dwuetapowej bezpośrednio do logowania.</span><span class="sxs-lookup"><span data-stu-id="ea559-104">hello Azure Multi-Factor Authentication Software Development Kit (SDK) lets you build two-step verification directly into hello sign-in or transaction processes of applications in your Azure AD tenant.</span></span>

<span data-ttu-id="ea559-105">Witaj SDK usługi Multi-Factor Authentication jest dostępna w C#, Visual Basic (.NET), Java, Perl, PHP i Ruby.</span><span class="sxs-lookup"><span data-stu-id="ea559-105">hello Multi-Factor Authentication SDK is available for C#, Visual Basic (.NET), Java, Perl, PHP, and Ruby.</span></span> <span data-ttu-id="ea559-106">Witaj SDK udostępnia alokowania otokę weryfikacji dwuetapowej.</span><span class="sxs-lookup"><span data-stu-id="ea559-106">hello SDK provides a thin wrapper around two-step verification.</span></span> <span data-ttu-id="ea559-107">Obejmuje on wszystko, co potrzebne toowrite kodu, w tym pliki kodu źródłowego komentarze, przykładowe pliki i szczegółowe plik ReadMe.</span><span class="sxs-lookup"><span data-stu-id="ea559-107">It includes everything you need toowrite your code, including commented source code files, example files, and a detailed ReadMe file.</span></span> <span data-ttu-id="ea559-108">Każdy zestaw SDK zawiera również certyfikat i klucz prywatny szyfrowania transakcje, które są unikatowe tooyour dostawca uwierzytelniania MFA.</span><span class="sxs-lookup"><span data-stu-id="ea559-108">Each SDK also includes a certificate and private key for encrypting transactions that are unique tooyour Multi-Factor Authentication Provider.</span></span> <span data-ttu-id="ea559-109">Tak długo, jak długo ma dostawcy, możesz pobrać hello zestawu SDK w formatach i języków tyle zgodnie z potrzebami.</span><span class="sxs-lookup"><span data-stu-id="ea559-109">As long as you have a provider, you can download hello SDK in as many languages and formats as you need.</span></span>

<span data-ttu-id="ea559-110">Struktura Hello hello interfejsów API w hello SDK usługi Multi-Factor Authentication jest proste.</span><span class="sxs-lookup"><span data-stu-id="ea559-110">hello structure of hello APIs in hello Multi-Factor Authentication SDK is simple.</span></span> <span data-ttu-id="ea559-111">Należy wywołać interfejs API tooan hello opcja wieloskładnikowego parametrów (takie jak tryb weryfikacji) i danych użytkownika (na przykład toocall numeru telefonu hello lub toovalidate numer PIN hello) jednej funkcji.</span><span class="sxs-lookup"><span data-stu-id="ea559-111">Make a single function call tooan API with hello multi-factor option parameters (like verification mode) and user data (like hello telephone number toocall or hello PIN number toovalidate).</span></span> <span data-ttu-id="ea559-112">Witaj interfejsów API wykonuje wywołanie funkcji hello toohello żądania usługi sieci web opartej na chmurze usługi systemu Azure Multi-Factor Authentication.</span><span class="sxs-lookup"><span data-stu-id="ea559-112">hello APIs translate hello function call into web services requests toohello cloud-based Azure Multi-Factor Authentication Service.</span></span> <span data-ttu-id="ea559-113">Wszystkie wywołania musi zawierać certyfikatu prywatnego toohello odwołania, który znajduje się w każdym zestawu SDK.</span><span class="sxs-lookup"><span data-stu-id="ea559-113">All calls must include a reference toohello private certificate that is included in every SDK.</span></span>

<span data-ttu-id="ea559-114">Ponieważ hello interfejsów API nie mają toousers access zarejestrowane w usłudze Azure Active Directory, musisz podać informacje o użytkowniku w pliku lub bazy danych.</span><span class="sxs-lookup"><span data-stu-id="ea559-114">Because hello APIs do not have access toousers registered in Azure Active Directory, you must provide user information in a file or database.</span></span> <span data-ttu-id="ea559-115">Hello interfejsów API oferuje również funkcje zarządzania rejestracji lub użytkownika, więc należy toobuild tych procesów do aplikacji.</span><span class="sxs-lookup"><span data-stu-id="ea559-115">Also, hello APIs do not provide enrollment or user management features, so you need toobuild these processes into your application.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="ea559-116">toodownload hello zestawu SDK, należy toocreate dostawcy usługi Azure Multi-Factor Authentication, nawet jeśli użytkownik ma licencje usługi Azure MFA, usługi AAD Premium lub pakietu EMS.</span><span class="sxs-lookup"><span data-stu-id="ea559-116">toodownload hello SDK, you need toocreate an Azure Multi-Factor Auth Provider even if you have Azure MFA, AAD Premium, or EMS licenses.</span></span> <span data-ttu-id="ea559-117">W tym celu należy utworzyć dostawcy usługi Azure Multi-Factor Authentication, a już licencji, należy się hello toocreate dostawcy z hello **każdego włączonego użytkownika** modelu.</span><span class="sxs-lookup"><span data-stu-id="ea559-117">If you create an Azure Multi-Factor Auth Provider for this purpose and already have licenses, make sure toocreate hello Provider with hello **Per Enabled User** model.</span></span> <span data-ttu-id="ea559-118">Następnie połącz hello dostawcy toohello katalog, który zawiera hello licencje usługi Azure MFA, Azure AD Premium lub pakietu EMS.</span><span class="sxs-lookup"><span data-stu-id="ea559-118">Then, link hello Provider toohello directory that contains hello Azure MFA, Azure AD Premium, or EMS licenses.</span></span> <span data-ttu-id="ea559-119">Taka konfiguracja powoduje, że rozliczenie jest przeprowadzane tylko jeśli masz więcej unikatowych użytkowników przy użyciu hello SDK niż hello liczbę licencji użytkownika.</span><span class="sxs-lookup"><span data-stu-id="ea559-119">This configuration ensures that you are only billed if you have more unique users using hello SDK than hello number of licenses you own.</span></span>


## <a name="download-hello-sdk"></a><span data-ttu-id="ea559-120">Pobierz hello zestawu SDK</span><span class="sxs-lookup"><span data-stu-id="ea559-120">Download hello SDK</span></span>
<span data-ttu-id="ea559-121">Pobieranie hello zestawu SDK usługi Azure Multi-Factor wymaga [dostawcy uwierzytelniania wieloskładnikowego Azure](multi-factor-authentication-get-started-auth-provider.md).</span><span class="sxs-lookup"><span data-stu-id="ea559-121">Downloading hello Azure Multi-Factor SDK requires an [Azure Multi-Factor Auth Provider](multi-factor-authentication-get-started-auth-provider.md).</span></span>  <span data-ttu-id="ea559-122">Wymaga pełnej Azure subskrypcji, nawet jeśli należą do firmy licencje usługi Azure MFA, Azure AD Premium lub pakietu Enterprise Mobility Suite.</span><span class="sxs-lookup"><span data-stu-id="ea559-122">This requires a full Azure subscription, even if Azure MFA, Azure AD Premium, or Enterprise Mobility Suite licenses are owned.</span></span>  <span data-ttu-id="ea559-123">Witaj toodownload zestawu SDK, przejdź toohello Portal zarządzania usługą Multi-Factor.</span><span class="sxs-lookup"><span data-stu-id="ea559-123">toodownload hello SDK, navigate toohello Multi-Factor Management Portal.</span></span> <span data-ttu-id="ea559-124">Hello portal można osiągnąć przez zarządzanie hello dostawcy uwierzytelniania wieloskładnikowego bezpośrednio lub przez kliknięcie przycisku hello **"Portal toohello Przejdź"** łącze na stronie ustawień usługi MFA hello.</span><span class="sxs-lookup"><span data-stu-id="ea559-124">You can reach hello portal either by managing hello Multi-Factor Auth Provider directly, or by clicking hello **"Go toohello portal"** link on hello MFA service settings page.</span></span>

### <a name="download-from-hello-azure-classic-portal"></a><span data-ttu-id="ea559-125">Pobierz z hello klasycznego portalu Azure</span><span class="sxs-lookup"><span data-stu-id="ea559-125">Download from hello Azure classic portal</span></span>
1. <span data-ttu-id="ea559-126">Zaloguj się toohello [klasycznego portalu Azure](https://manage.windowsazure.com) jako Administrator.</span><span class="sxs-lookup"><span data-stu-id="ea559-126">Sign in toohello [Azure classic portal](https://manage.windowsazure.com) as an Administrator.</span></span>
2. <span data-ttu-id="ea559-127">Po lewej stronie powitania, wybierz **usługi Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="ea559-127">On hello left, select **Active Directory**.</span></span>
3. <span data-ttu-id="ea559-128">Na stronie usługi Active Directory hello na górnym umożliwia hello **dostawców uwierzytelniania wieloskładnikowego**</span><span class="sxs-lookup"><span data-stu-id="ea559-128">On hello Active Directory page, at hello top select **Multi-Factor Auth Providers**</span></span>
4. <span data-ttu-id="ea559-129">U dołu hello wybierz **Zarządzaj**.</span><span class="sxs-lookup"><span data-stu-id="ea559-129">At hello bottom select **Manage**.</span></span> <span data-ttu-id="ea559-130">Zostanie otwarta nowa strona.</span><span class="sxs-lookup"><span data-stu-id="ea559-130">A new page opens.</span></span>
5. <span data-ttu-id="ea559-131">Na powitania po lewej, u dołu hello kliknij **SDK**.</span><span class="sxs-lookup"><span data-stu-id="ea559-131">On hello left, at hello bottom, click **SDK**.</span></span>
   <span data-ttu-id="ea559-132"><center>![Pobierz](./media/multi-factor-authentication-sdk/download.png)</center></span><span class="sxs-lookup"><span data-stu-id="ea559-132"><center>![Download](./media/multi-factor-authentication-sdk/download.png)</center></span></span>
6. <span data-ttu-id="ea559-133">Wybierz język hello i kliknij jeden łączy do pobierania hello.</span><span class="sxs-lookup"><span data-stu-id="ea559-133">Select hello language you want and click one hello associated download links.</span></span>
7. <span data-ttu-id="ea559-134">Zapisz hello pobierania.</span><span class="sxs-lookup"><span data-stu-id="ea559-134">Save hello download.</span></span>

### <a name="download-from-hello-service-settings"></a><span data-ttu-id="ea559-135">Pobierz z hello ustawienia usługi</span><span class="sxs-lookup"><span data-stu-id="ea559-135">Download from hello service settings</span></span>
1. <span data-ttu-id="ea559-136">Zaloguj się toohello [klasycznego portalu Azure](https://manage.windowsazure.com) jako Administrator.</span><span class="sxs-lookup"><span data-stu-id="ea559-136">Sign in toohello [Azure classic portal](https://manage.windowsazure.com) as an Administrator.</span></span>
2. <span data-ttu-id="ea559-137">Po lewej stronie powitania, wybierz **usługi Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="ea559-137">On hello left, select **Active Directory**.</span></span>
3. <span data-ttu-id="ea559-138">Kliknij dwukrotnie wystąpienie usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="ea559-138">Double-click your instance of Azure AD.</span></span>
4. <span data-ttu-id="ea559-139">Na powitania kliknij górny **Konfiguruj**</span><span class="sxs-lookup"><span data-stu-id="ea559-139">At hello top click **Configure**</span></span>
5. <span data-ttu-id="ea559-140">W obszarze usługi Multi-Factor authentication, zaznacz **Zarządzaj ustawieniami usługi**
   ![Pobierz](./media/multi-factor-authentication-sdk/download2.png)</span><span class="sxs-lookup"><span data-stu-id="ea559-140">Under multi-factor authentication, select **Manage service settings**
![Download](./media/multi-factor-authentication-sdk/download2.png)</span></span>
6. <span data-ttu-id="ea559-141">Na stronie ustawień usługi hello u dołu ekranu hello powitania kliknij **Przejdź toohello portal**.</span><span class="sxs-lookup"><span data-stu-id="ea559-141">On hello services settings page, at hello bottom of hello screen click **Go toohello portal**.</span></span> <span data-ttu-id="ea559-142">Zostanie otwarta nowa strona.</span><span class="sxs-lookup"><span data-stu-id="ea559-142">A new page opens.</span></span>
   <span data-ttu-id="ea559-143">![Pobieranie](./media/multi-factor-authentication-sdk/download3a.png)</span><span class="sxs-lookup"><span data-stu-id="ea559-143">![Download](./media/multi-factor-authentication-sdk/download3a.png)</span></span>
7. <span data-ttu-id="ea559-144">Na powitania po lewej, u dołu hello kliknij **SDK**.</span><span class="sxs-lookup"><span data-stu-id="ea559-144">On hello left, at hello bottom, click **SDK**.</span></span>
8. <span data-ttu-id="ea559-145">Wybierz język hello i kliknij jeden łączy do pobierania hello.</span><span class="sxs-lookup"><span data-stu-id="ea559-145">Select hello language you want and click one hello associated download links.</span></span>
9. <span data-ttu-id="ea559-146">Zapisz hello pobierania.</span><span class="sxs-lookup"><span data-stu-id="ea559-146">Save hello download.</span></span>

## <a name="whats-in-hello-sdk"></a><span data-ttu-id="ea559-147">Co to jest w hello zestawu SDK</span><span class="sxs-lookup"><span data-stu-id="ea559-147">What's in hello SDK</span></span>
<span data-ttu-id="ea559-148">Witaj zestaw SDK zawiera hello następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="ea559-148">hello SDK includes hello following items:</span></span>

* <span data-ttu-id="ea559-149">**PLIK README**.</span><span class="sxs-lookup"><span data-stu-id="ea559-149">**README**.</span></span> <span data-ttu-id="ea559-150">W tym artykule wyjaśniono, jak toouse hello interfejsy API uwierzytelniania wieloskładnikowego w nowej lub istniejącej aplikacji.</span><span class="sxs-lookup"><span data-stu-id="ea559-150">Explains how toouse hello Multi-Factor Authentication APIs in a new or existing application.</span></span>
* <span data-ttu-id="ea559-151">**Pliki źródłowe** uwierzytelnianie wieloskładnikowe</span><span class="sxs-lookup"><span data-stu-id="ea559-151">**Source files** for Multi-Factor Authentication</span></span>
* <span data-ttu-id="ea559-152">**Certyfikat klienta** użyć toocommunicate z hello usługi Multi-Factor Authentication</span><span class="sxs-lookup"><span data-stu-id="ea559-152">**Client certificate** that you use toocommunicate with hello Multi-Factor Authentication service</span></span>
* <span data-ttu-id="ea559-153">**Klucz prywatny** hello certyfikatu</span><span class="sxs-lookup"><span data-stu-id="ea559-153">**Private key** for hello certificate</span></span>
* <span data-ttu-id="ea559-154">**Wyniki wywołania.**</span><span class="sxs-lookup"><span data-stu-id="ea559-154">**Call results.**</span></span> <span data-ttu-id="ea559-155">Lista kody rezultatów połączeń.</span><span class="sxs-lookup"><span data-stu-id="ea559-155">A list of call result codes.</span></span> <span data-ttu-id="ea559-156">tooopen ten plik, użyj aplikacji przy użyciu tekstu, takich jak program WordPad.</span><span class="sxs-lookup"><span data-stu-id="ea559-156">tooopen this file, use an application with text formatting, such as WordPad.</span></span> <span data-ttu-id="ea559-157">Użyj hello wywołać tootest kody wyników i rozwiązywania problemów z hello stosowania uwierzytelniania wieloskładnikowego w aplikacji.</span><span class="sxs-lookup"><span data-stu-id="ea559-157">Use hello call result codes tootest and troubleshoot hello implementation of Multi-Factor Authentication in your application.</span></span> <span data-ttu-id="ea559-158">Nie są one kodów stanu uwierzytelniania.</span><span class="sxs-lookup"><span data-stu-id="ea559-158">They are not authentication status codes.</span></span>
* <span data-ttu-id="ea559-159">**Przykłady.**</span><span class="sxs-lookup"><span data-stu-id="ea559-159">**Examples.**</span></span> <span data-ttu-id="ea559-160">Przykładowy kod Podstawowa implementacja pracy usługi Multi-Factor Authentication.</span><span class="sxs-lookup"><span data-stu-id="ea559-160">Sample code for a basic working implementation of Multi-Factor Authentication.</span></span>

> [!WARNING]
> <span data-ttu-id="ea559-161">certyfikat klienta na powitania jest unikatowy certyfikat prywatny wygenerowany specjalnie dla Ciebie.</span><span class="sxs-lookup"><span data-stu-id="ea559-161">hello client certificate is a unique private certificate that was generated especially for you.</span></span> <span data-ttu-id="ea559-162">Udostępnij lub nie utracić tego pliku.</span><span class="sxs-lookup"><span data-stu-id="ea559-162">Do not share or lose this file.</span></span> <span data-ttu-id="ea559-163">Jest tooensuring klucza zabezpieczeń hello komunikacji z usługą Multi-Factor Authentication hello.</span><span class="sxs-lookup"><span data-stu-id="ea559-163">It’s your key tooensuring hello security of your communications with hello Multi-Factor Authentication service.</span></span>

## <a name="code-sample"></a><span data-ttu-id="ea559-164">Przykład kodu</span><span class="sxs-lookup"><span data-stu-id="ea559-164">Code sample</span></span>
<span data-ttu-id="ea559-165">Ten przykładowy kod przedstawia sposób toouse hello interfejsów API w hello Azure Multi-Factor Authentication SDK tooadd Tryb standardowy głosu wywoływania aplikacji tooyour weryfikacji.</span><span class="sxs-lookup"><span data-stu-id="ea559-165">This code sample shows you how toouse hello APIs in hello Azure Multi-Factor Authentication SDK tooadd standard mode voice call verification tooyour application.</span></span> <span data-ttu-id="ea559-166">Telefon hello użytkownika odpowiada tooby naciśnięcie klawisza # hello jest tryb standardowy.</span><span class="sxs-lookup"><span data-stu-id="ea559-166">Standard mode is a telephone call that hello user responds tooby pressing hello # key.</span></span>

<span data-ttu-id="ea559-167">W tym przykładzie użyto hello C# .NET 2.0 SDK usługi Multi-Factor Authentication w podstawowej aplikacji ASP.NET w logice C# po stronie serwera, ale hello proces jest podobny w innych językach.</span><span class="sxs-lookup"><span data-stu-id="ea559-167">This example uses hello C# .NET 2.0 Multi-Factor Authentication SDK in a basic ASP.NET application with C# server-side logic, but hello process is similar in other languages.</span></span> <span data-ttu-id="ea559-168">Ponieważ hello zestaw SDK zawiera pliki źródłowe, pliki wykonywalne nie można skompilować plików hello i odwoływać je lub umieścić je bezpośrednio w aplikacji.</span><span class="sxs-lookup"><span data-stu-id="ea559-168">Because hello SDK includes source files, not executable files, you can build hello files and reference them or include them directly in your application.</span></span>

> [!NOTE]
> <span data-ttu-id="ea559-169">Podczas wdrażania usługi Multi-Factor Authentication, użyj hello dodatkowe metody (Rozmowa telefoniczna lub wiadomości tekstowej) jako dodatkowej lub trzeciorzędny weryfikacji toosupplement metodę uwierzytelniania podstawowego (nazwa użytkownika i hasło).</span><span class="sxs-lookup"><span data-stu-id="ea559-169">When implementing Multi-Factor Authentication, use hello additional methods (phone call or text message) as secondary or tertiary verification toosupplement your primary authentication method (username and password).</span></span> <span data-ttu-id="ea559-170">Te metody nie są zaprojektowane jako metody uwierzytelniania podstawowego.</span><span class="sxs-lookup"><span data-stu-id="ea559-170">These methods are not designed as primary authentication methods.</span></span>

### <a name="code-sample-overview"></a><span data-ttu-id="ea559-171">Omówienie przykładowy kod</span><span class="sxs-lookup"><span data-stu-id="ea559-171">Code Sample Overview</span></span>
<span data-ttu-id="ea559-172">Ten przykładowy kod dla prostą aplikację sieci web pokaz używa połączenia telefonicznego z uwierzytelnianiem # klucza odpowiedzi tooverify hello użytkownika.</span><span class="sxs-lookup"><span data-stu-id="ea559-172">This sample code for a simple web demo application uses a telephone call with a # key response tooverify hello user's authentication.</span></span> <span data-ttu-id="ea559-173">Współczynnik ten telefon jest określany w usłudze Multi-Factor Authentication jako tryb standardowy.</span><span class="sxs-lookup"><span data-stu-id="ea559-173">This telephone call factor is known in Multi-Factor Authentication as standard mode.</span></span>

<span data-ttu-id="ea559-174">Hello kod po stronie klienta nie ma żadnych elementów specyficznych dla usługi Multi-Factor Authentication.</span><span class="sxs-lookup"><span data-stu-id="ea559-174">hello client-side code does not include any Multi-Factor Authentication-specific elements.</span></span> <span data-ttu-id="ea559-175">Ponieważ hello dodatkowych czynników autoryzacji są niezależne od hello podstawowego uwierzytelniania, można dodawać je bez zmieniania hello istniejącego logowania interfejsu.</span><span class="sxs-lookup"><span data-stu-id="ea559-175">Because hello additional authentication factors are independent of hello primary authentication, you can add them without changing hello existing sign-on interface.</span></span> <span data-ttu-id="ea559-176">Hello interfejsów API w hello SDK Multi-Factor umożliwiają dostosowanie hello środowisko użytkownika, ale może nie być konieczny toochange niczego w ogóle.</span><span class="sxs-lookup"><span data-stu-id="ea559-176">hello APIs in hello Multi-Factor SDK let you customize hello user experience, but you might not need toochange anything at all.</span></span>

<span data-ttu-id="ea559-177">Kod po stronie serwera Hello dodaje Tryb standardowy uwierzytelniania w kroku 2.</span><span class="sxs-lookup"><span data-stu-id="ea559-177">hello server-side code adds standard-mode authentication in Step 2.</span></span> <span data-ttu-id="ea559-178">Tworzy obiekt PfAuthParams z parametrami hello, które są wymagane do weryfikacji Tryb standardowy: nazwa_użytkownika, telefonu numer i tryb i hello ścieżki toohello certyfikatu klienta (CertFilePath), który jest wymagany w każdym wywołaniu.</span><span class="sxs-lookup"><span data-stu-id="ea559-178">It creates a PfAuthParams object with hello parameters that are required for standard-mode verification: username, telephone number, and mode, and hello path toohello client certificate (CertFilePath), which is required in each call.</span></span> <span data-ttu-id="ea559-179">Aby demonstracyjne wszystkich parametrów w PfAuthParams, zobacz hello przykładowy plik w hello zestawu SDK.</span><span class="sxs-lookup"><span data-stu-id="ea559-179">For a demonstration of all parameters in PfAuthParams, see hello Example file in hello SDK.</span></span>

<span data-ttu-id="ea559-180">Następnie kod hello przekazuje hello PfAuthParams obiektu toohello pf_authenticate() funkcji.</span><span class="sxs-lookup"><span data-stu-id="ea559-180">Next, hello code passes hello PfAuthParams object toohello pf_authenticate() function.</span></span> <span data-ttu-id="ea559-181">Wartość zwracana Hello wskazuje hello powodzenie lub niepowodzenie uwierzytelniania hello.</span><span class="sxs-lookup"><span data-stu-id="ea559-181">hello return value indicates hello success or failure of hello authentication.</span></span> <span data-ttu-id="ea559-182">Witaj parametrów, callStatus oraz identyfikator błędu, zawierają informacje wynik wywołania dodatkowe.</span><span class="sxs-lookup"><span data-stu-id="ea559-182">hello out parameters, callStatus, and errorID, contain additional call result information.</span></span> <span data-ttu-id="ea559-183">kody rezultatów połączeń Hello są udokumentowane w pliku wyników wywołania hello w hello zestawu SDK.</span><span class="sxs-lookup"><span data-stu-id="ea559-183">hello call result codes are documented in hello call results file in hello SDK.</span></span>

<span data-ttu-id="ea559-184">Ta implementacja minimalnego można pisać w zaledwie kilku wierszach.</span><span class="sxs-lookup"><span data-stu-id="ea559-184">This minimal implementation can be written in a few lines.</span></span> <span data-ttu-id="ea559-185">Jednak w kodzie produkcyjnym, można dołączyć dokładniejsze obsługi błędów kodu dodatkowej bazy danych i lepszą obsługę użytkowników.</span><span class="sxs-lookup"><span data-stu-id="ea559-185">However, in production code, you would include more sophisticated error handling, additional database code, and an enhanced user experience.</span></span>

### <a name="web-client-code"></a><span data-ttu-id="ea559-186">Kod klienta sieci Web</span><span class="sxs-lookup"><span data-stu-id="ea559-186">Web Client Code</span></span>
<span data-ttu-id="ea559-187">Oto Hello kodu klienta sieci web dla strony pokaz.</span><span class="sxs-lookup"><span data-stu-id="ea559-187">hello following is web client code for a demo page.</span></span>

    <%@ Page Language="C#" AutoEventWireup="true" CodeFile="Default.aspx.cs" Inherits="\_Default" %>

    <!DOCTYPE html>

    <html xmlns="http://www.w3.org/1999/xhtml">
    <head runat="server">
    <title>Multi-Factor Authentication Demo</title>
    </head>
    <body>
    <h1>Azure Multi-Factor Authentication Demo</h1>
    <form id="form1" runat="server">

    <div style="width:auto; float:left">
    Username:&nbsp;<br />
    Password:&nbsp;<br />
    </div>

    <div">
    <asp:TextBox id="username" runat="server" width="100px"/><br />
    <asp:Textbox id="password" runat="server" width="100px" TextMode="password" /><br />
    </div>

    <asp:Button id="btnSubmit" runat="server" Text="Log in" onClick="btnSubmit_Click"/>

    <p><asp:Label ID="lblResult" runat="server"></asp:Label></p>

    </form>
    </body>
    </html>


### <a name="server-side-code"></a><span data-ttu-id="ea559-188">Kod po stronie serwera</span><span class="sxs-lookup"><span data-stu-id="ea559-188">Server-Side Code</span></span>
<span data-ttu-id="ea559-189">Uwierzytelnianie wieloskładnikowe hello następującego kodu po stronie serwera, jest skonfigurowany i uruchamiania w kroku 2.</span><span class="sxs-lookup"><span data-stu-id="ea559-189">In hello following server-side code, Multi-Factor Authentication is configured and run in Step 2.</span></span> <span data-ttu-id="ea559-190">Rozmowy telefonicznej użytkownika hello toowhich odpowiada naciskając klawisz # hello jest tryb standardowy (MODE_STANDARD).</span><span class="sxs-lookup"><span data-stu-id="ea559-190">Standard mode (MODE_STANDARD) is a telephone call toowhich hello user responds by pressing hello # key.</span></span>

    using System;
    using System.Collections.Generic;
    using System.Linq;
    using System.Web;
    using System.Web.UI;
    using System.Web.UI.WebControls;

    public partial class \_Default : System.Web.UI.Page
    {
        protected void Page_Load(object sender, EventArgs e)
        {
        }

        protected void btnSubmit_Click(object sender, EventArgs e)
        {
            // Step 1: Validate hello username and password
            if (username.Text != "Contoso" || password.Text != "password")
            {
                lblResult.ForeColor = System.Drawing.Color.Red;
                lblResult.Text = "Username or password incorrect.";
            }
            else
            {
                // Step 2: Perform multi-factor authentication

                // Add call details from hello user database.
                PfAuthParams pfAuthParams = new PfAuthParams();
                pfAuthParams.Username = username.Text;
                pfAuthParams.Phone = "5555555555";
                pfAuthParams.Mode = pf_auth.MODE_STANDARD;

                // Specify a client certificate
                // NOTE: This file contains hello private key for hello client
                // certificate. It must be stored with appropriate file
                // permissions.
                pfAuthParams.CertFilePath = "c:\\cert_key.p12";

                // Perform phone-based authentication
                int callStatus;
                int errorId;

                if(pf_auth.pf_authenticate(pfAuthParams, out callStatus, out errorId))
                {
                    lblResult.ForeColor = System.Drawing.Color.Green;
                    lblResult.Text = "Multi-Factor Authentication succeeded.";
                }
                else
                {
                    lblResult.ForeColor = System.Drawing.Color.Red;
                    lblResult.Text = "Multi-Factor Authentication failed.";
                }
            }

        }
    }
