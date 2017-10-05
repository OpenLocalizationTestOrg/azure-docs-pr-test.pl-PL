---
title: "Uwierzytelnianie wieloskładnikowe software development kit aplikacji niestandardowych | Dokumentacja firmy Microsoft"
description: "W tym artykule przedstawiono sposób pobranie i użycie zestawu SDK usługi Azure MFA, aby włączyć weryfikację dwuetapową dla niestandardowych aplikacji."
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
ms.openlocfilehash: 281f9c61a30a20027f69808600373aa272255ef6
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="building-multi-factor-authentication-into-custom-apps-sdk"></a><span data-ttu-id="ceb3d-103">Tworzenie usługi Multi-Factor Authentication w aplikacje niestandardowe (SDK)</span><span class="sxs-lookup"><span data-stu-id="ceb3d-103">Building Multi-Factor Authentication into Custom Apps (SDK)</span></span>

<span data-ttu-id="ceb3d-104">Azure Multi-Factor Authentication Software Development Kit (SDK) umożliwia tworzenie aplikacji w dzierżawie usługi Azure AD włączono weryfikację dwuetapową bezpośrednio do procesów logowania lub transakcji.</span><span class="sxs-lookup"><span data-stu-id="ceb3d-104">The Azure Multi-Factor Authentication Software Development Kit (SDK) lets you build two-step verification directly into the sign-in or transaction processes of applications in your Azure AD tenant.</span></span>

<span data-ttu-id="ceb3d-105">SDK usługi Multi-Factor Authentication jest dostępna w C#, Visual Basic (.NET), Java, Perl, PHP i Ruby.</span><span class="sxs-lookup"><span data-stu-id="ceb3d-105">The Multi-Factor Authentication SDK is available for C#, Visual Basic (.NET), Java, Perl, PHP, and Ruby.</span></span> <span data-ttu-id="ceb3d-106">Zestaw SDK udostępnia cienką otoką wokół weryfikacji dwuetapowej.</span><span class="sxs-lookup"><span data-stu-id="ceb3d-106">The SDK provides a thin wrapper around two-step verification.</span></span> <span data-ttu-id="ceb3d-107">Obejmuje on wszystko, co potrzebne do pisania kodu, w tym pliki kodu źródłowego komentarze, przykładowe pliki i szczegółowe plik ReadMe.</span><span class="sxs-lookup"><span data-stu-id="ceb3d-107">It includes everything you need to write your code, including commented source code files, example files, and a detailed ReadMe file.</span></span> <span data-ttu-id="ceb3d-108">Każdy zestaw SDK zawiera również certyfikat i klucz prywatny szyfrowania transakcje, które są unikatowe dla dostawcy uwierzytelniania wieloskładnikowego.</span><span class="sxs-lookup"><span data-stu-id="ceb3d-108">Each SDK also includes a certificate and private key for encrypting transactions that are unique to your Multi-Factor Authentication Provider.</span></span> <span data-ttu-id="ceb3d-109">Tak długo, jak długo ma dostawcy, możesz pobrać zestaw SDK w dowolną liczbę języków i formaty zgodnie z potrzebami.</span><span class="sxs-lookup"><span data-stu-id="ceb3d-109">As long as you have a provider, you can download the SDK in as many languages and formats as you need.</span></span>

<span data-ttu-id="ceb3d-110">Struktura interfejsów API w zestawie SDK usługi Multi-Factor Authentication jest proste.</span><span class="sxs-lookup"><span data-stu-id="ceb3d-110">The structure of the APIs in the Multi-Factor Authentication SDK is simple.</span></span> <span data-ttu-id="ceb3d-111">Należy jednej funkcji wywołanie interfejsu API za pomocą opcji wieloskładnikowego parametry (takie jak tryb weryfikacji) i danych użytkownika (na przykład numer telefonu lub numer PIN, aby sprawdzić poprawność).</span><span class="sxs-lookup"><span data-stu-id="ceb3d-111">Make a single function call to an API with the multi-factor option parameters (like verification mode) and user data (like the telephone number to call or the PIN number to validate).</span></span> <span data-ttu-id="ceb3d-112">Interfejsy API wykonuje wywołanie funkcji do żądania usługi sieci web do usługi uwierzytelniania wieloskładnikowego Azure opartej na chmurze.</span><span class="sxs-lookup"><span data-stu-id="ceb3d-112">The APIs translate the function call into web services requests to the cloud-based Azure Multi-Factor Authentication Service.</span></span> <span data-ttu-id="ceb3d-113">Wszystkie wywołania musi zawierać odwołanie do certyfikatu prywatnego, który znajduje się w każdym zestawu SDK.</span><span class="sxs-lookup"><span data-stu-id="ceb3d-113">All calls must include a reference to the private certificate that is included in every SDK.</span></span>

<span data-ttu-id="ceb3d-114">Ponieważ interfejsy API nie mają dostępu do użytkowników zarejestrowanych w usłudze Azure Active Directory, musisz podać informacje o użytkowniku w pliku lub bazy danych.</span><span class="sxs-lookup"><span data-stu-id="ceb3d-114">Because the APIs do not have access to users registered in Azure Active Directory, you must provide user information in a file or database.</span></span> <span data-ttu-id="ceb3d-115">Interfejsy API nie udostępniają również funkcje zarządzania użytkownika lub rejestracji, więc jest potrzebne do tworzenia tych procesów do aplikacji.</span><span class="sxs-lookup"><span data-stu-id="ceb3d-115">Also, the APIs do not provide enrollment or user management features, so you need to build these processes into your application.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="ceb3d-116">Aby pobrać zestaw SDK, musisz utworzyć dostawcę usługi Azure Multi-Factor Authentication, nawet jeśli masz licencje usług Azure MFA, AAD Premium lub EMS.</span><span class="sxs-lookup"><span data-stu-id="ceb3d-116">To download the SDK, you need to create an Azure Multi-Factor Auth Provider even if you have Azure MFA, AAD Premium, or EMS licenses.</span></span> <span data-ttu-id="ceb3d-117">Jeśli w tym celu należy utworzyć dostawcy uwierzytelniania wieloskładnikowego Azure i mają już licencji, upewnij się, że tworzenie dostawcy z **każdego włączonego użytkownika** modelu.</span><span class="sxs-lookup"><span data-stu-id="ceb3d-117">If you create an Azure Multi-Factor Auth Provider for this purpose and already have licenses, make sure to create the Provider with the **Per Enabled User** model.</span></span> <span data-ttu-id="ceb3d-118">Następnie połącz dostawcę z katalogiem zawierającym licencje usług Azure MFA, Azure AD Premium lub EMS.</span><span class="sxs-lookup"><span data-stu-id="ceb3d-118">Then, link the Provider to the directory that contains the Azure MFA, Azure AD Premium, or EMS licenses.</span></span> <span data-ttu-id="ceb3d-119">Taka konfiguracja powoduje, że rozliczenie jest przeprowadzane tylko jeśli masz więcej unikatowych użytkowników przy użyciu zestawu SDK niż liczba licencji użytkownika.</span><span class="sxs-lookup"><span data-stu-id="ceb3d-119">This configuration ensures that you are only billed if you have more unique users using the SDK than the number of licenses you own.</span></span>


## <a name="download-the-sdk"></a><span data-ttu-id="ceb3d-120">Pobierz zestaw SDK</span><span class="sxs-lookup"><span data-stu-id="ceb3d-120">Download the SDK</span></span>
<span data-ttu-id="ceb3d-121">Pobieranie zestawu SDK usługi Azure Multi-Factor wymaga [dostawcy uwierzytelniania wieloskładnikowego Azure](multi-factor-authentication-get-started-auth-provider.md).</span><span class="sxs-lookup"><span data-stu-id="ceb3d-121">Downloading the Azure Multi-Factor SDK requires an [Azure Multi-Factor Auth Provider](multi-factor-authentication-get-started-auth-provider.md).</span></span>  <span data-ttu-id="ceb3d-122">Wymaga pełnej Azure subskrypcji, nawet jeśli należą do firmy licencje usługi Azure MFA, Azure AD Premium lub pakietu Enterprise Mobility Suite.</span><span class="sxs-lookup"><span data-stu-id="ceb3d-122">This requires a full Azure subscription, even if Azure MFA, Azure AD Premium, or Enterprise Mobility Suite licenses are owned.</span></span>  <span data-ttu-id="ceb3d-123">Aby pobrać zestaw SDK, przejdź do portalu zarządzania usługi Multi-Factor.</span><span class="sxs-lookup"><span data-stu-id="ceb3d-123">To download the SDK, navigate to the Multi-Factor Management Portal.</span></span> <span data-ttu-id="ceb3d-124">Portalu można osiągnąć dzięki zarządzaniu dostawcy uwierzytelniania wieloskładnikowego bezpośrednio lub przez kliknięcie przycisku **"Przejdź do portalu"** łącze na stronie ustawień usługi MFA.</span><span class="sxs-lookup"><span data-stu-id="ceb3d-124">You can reach the portal either by managing the Multi-Factor Auth Provider directly, or by clicking the **"Go to the portal"** link on the MFA service settings page.</span></span>

### <a name="download-from-the-azure-classic-portal"></a><span data-ttu-id="ceb3d-125">Pobierz z klasycznego portalu Azure</span><span class="sxs-lookup"><span data-stu-id="ceb3d-125">Download from the Azure classic portal</span></span>
1. <span data-ttu-id="ceb3d-126">Zaloguj się do [klasycznego portalu Azure](https://manage.windowsazure.com) jako administrator.</span><span class="sxs-lookup"><span data-stu-id="ceb3d-126">Sign in to the [Azure classic portal](https://manage.windowsazure.com) as an Administrator.</span></span>
2. <span data-ttu-id="ceb3d-127">W obszarze po lewej stronie wybierz pozycję **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="ceb3d-127">On the left, select **Active Directory**.</span></span>
3. <span data-ttu-id="ceb3d-128">Na stronie usługi Active Directory na górnym umożliwia **dostawców uwierzytelniania wieloskładnikowego**</span><span class="sxs-lookup"><span data-stu-id="ceb3d-128">On the Active Directory page, at the top select **Multi-Factor Auth Providers**</span></span>
4. <span data-ttu-id="ceb3d-129">U dołu wybierz **Zarządzaj**.</span><span class="sxs-lookup"><span data-stu-id="ceb3d-129">At the bottom select **Manage**.</span></span> <span data-ttu-id="ceb3d-130">Zostanie otwarta nowa strona.</span><span class="sxs-lookup"><span data-stu-id="ceb3d-130">A new page opens.</span></span>
5. <span data-ttu-id="ceb3d-131">Po lewej stronie u dołu, kliknij przycisk **SDK**.</span><span class="sxs-lookup"><span data-stu-id="ceb3d-131">On the left, at the bottom, click **SDK**.</span></span>
   <span data-ttu-id="ceb3d-132"><center>![Pobierz](./media/multi-factor-authentication-sdk/download.png)</center></span><span class="sxs-lookup"><span data-stu-id="ceb3d-132"><center>![Download](./media/multi-factor-authentication-sdk/download.png)</center></span></span>
6. <span data-ttu-id="ceb3d-133">Wybierz język i kliknij jeden łączy do pobierania.</span><span class="sxs-lookup"><span data-stu-id="ceb3d-133">Select the language you want and click one the associated download links.</span></span>
7. <span data-ttu-id="ceb3d-134">Zapisz pobrany plik.</span><span class="sxs-lookup"><span data-stu-id="ceb3d-134">Save the download.</span></span>

### <a name="download-from-the-service-settings"></a><span data-ttu-id="ceb3d-135">Pobierz z ustawienia usługi</span><span class="sxs-lookup"><span data-stu-id="ceb3d-135">Download from the service settings</span></span>
1. <span data-ttu-id="ceb3d-136">Zaloguj się do [klasycznego portalu Azure](https://manage.windowsazure.com) jako administrator.</span><span class="sxs-lookup"><span data-stu-id="ceb3d-136">Sign in to the [Azure classic portal](https://manage.windowsazure.com) as an Administrator.</span></span>
2. <span data-ttu-id="ceb3d-137">W obszarze po lewej stronie wybierz pozycję **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="ceb3d-137">On the left, select **Active Directory**.</span></span>
3. <span data-ttu-id="ceb3d-138">Kliknij dwukrotnie wystąpienie usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="ceb3d-138">Double-click your instance of Azure AD.</span></span>
4. <span data-ttu-id="ceb3d-139">Kliknij pozycję **Konfiguruj** u góry strony</span><span class="sxs-lookup"><span data-stu-id="ceb3d-139">At the top click **Configure**</span></span>
5. <span data-ttu-id="ceb3d-140">W obszarze usługi Multi-Factor authentication, zaznacz **Zarządzaj ustawieniami usługi**
   ![Pobierz](./media/multi-factor-authentication-sdk/download2.png)</span><span class="sxs-lookup"><span data-stu-id="ceb3d-140">Under multi-factor authentication, select **Manage service settings**
![Download](./media/multi-factor-authentication-sdk/download2.png)</span></span>
6. <span data-ttu-id="ceb3d-141">Na stronie ustawień usługi, w dolnej części ekranu, kliknij opcję **Przejdź do portalu**.</span><span class="sxs-lookup"><span data-stu-id="ceb3d-141">On the services settings page, at the bottom of the screen click **Go to the portal**.</span></span> <span data-ttu-id="ceb3d-142">Zostanie otwarta nowa strona.</span><span class="sxs-lookup"><span data-stu-id="ceb3d-142">A new page opens.</span></span>
   <span data-ttu-id="ceb3d-143">![Pobieranie](./media/multi-factor-authentication-sdk/download3a.png)</span><span class="sxs-lookup"><span data-stu-id="ceb3d-143">![Download](./media/multi-factor-authentication-sdk/download3a.png)</span></span>
7. <span data-ttu-id="ceb3d-144">Po lewej stronie u dołu, kliknij przycisk **SDK**.</span><span class="sxs-lookup"><span data-stu-id="ceb3d-144">On the left, at the bottom, click **SDK**.</span></span>
8. <span data-ttu-id="ceb3d-145">Wybierz język i kliknij jeden łączy do pobierania.</span><span class="sxs-lookup"><span data-stu-id="ceb3d-145">Select the language you want and click one the associated download links.</span></span>
9. <span data-ttu-id="ceb3d-146">Zapisz pobrany plik.</span><span class="sxs-lookup"><span data-stu-id="ceb3d-146">Save the download.</span></span>

## <a name="whats-in-the-sdk"></a><span data-ttu-id="ceb3d-147">Co to jest w zestawie SDK</span><span class="sxs-lookup"><span data-stu-id="ceb3d-147">What's in the SDK</span></span>
<span data-ttu-id="ceb3d-148">Zestaw SDK zawiera następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="ceb3d-148">The SDK includes the following items:</span></span>

* <span data-ttu-id="ceb3d-149">**PLIK README**.</span><span class="sxs-lookup"><span data-stu-id="ceb3d-149">**README**.</span></span> <span data-ttu-id="ceb3d-150">Opisano sposób korzystania z interfejsów API uwierzytelniania wieloskładnikowego w nowej lub istniejącej aplikacji.</span><span class="sxs-lookup"><span data-stu-id="ceb3d-150">Explains how to use the Multi-Factor Authentication APIs in a new or existing application.</span></span>
* <span data-ttu-id="ceb3d-151">**Pliki źródłowe** uwierzytelnianie wieloskładnikowe</span><span class="sxs-lookup"><span data-stu-id="ceb3d-151">**Source files** for Multi-Factor Authentication</span></span>
* <span data-ttu-id="ceb3d-152">**Certyfikat klienta** używanej do komunikacji z usługą Multi-Factor Authentication</span><span class="sxs-lookup"><span data-stu-id="ceb3d-152">**Client certificate** that you use to communicate with the Multi-Factor Authentication service</span></span>
* <span data-ttu-id="ceb3d-153">**Klucz prywatny** certyfikatu</span><span class="sxs-lookup"><span data-stu-id="ceb3d-153">**Private key** for the certificate</span></span>
* <span data-ttu-id="ceb3d-154">**Wyniki wywołania.**</span><span class="sxs-lookup"><span data-stu-id="ceb3d-154">**Call results.**</span></span> <span data-ttu-id="ceb3d-155">Lista kody rezultatów połączeń.</span><span class="sxs-lookup"><span data-stu-id="ceb3d-155">A list of call result codes.</span></span> <span data-ttu-id="ceb3d-156">Aby otworzyć ten plik, za pomocą aplikacji formatowanie tekstu, takich jak program WordPad.</span><span class="sxs-lookup"><span data-stu-id="ceb3d-156">To open this file, use an application with text formatting, such as WordPad.</span></span> <span data-ttu-id="ceb3d-157">Kody rezultatów połączeń umożliwia testowanie i rozwiązywanie problemów stosowania uwierzytelniania wieloskładnikowego w aplikacji.</span><span class="sxs-lookup"><span data-stu-id="ceb3d-157">Use the call result codes to test and troubleshoot the implementation of Multi-Factor Authentication in your application.</span></span> <span data-ttu-id="ceb3d-158">Nie są one kodów stanu uwierzytelniania.</span><span class="sxs-lookup"><span data-stu-id="ceb3d-158">They are not authentication status codes.</span></span>
* <span data-ttu-id="ceb3d-159">**Przykłady.**</span><span class="sxs-lookup"><span data-stu-id="ceb3d-159">**Examples.**</span></span> <span data-ttu-id="ceb3d-160">Przykładowy kod Podstawowa implementacja pracy usługi Multi-Factor Authentication.</span><span class="sxs-lookup"><span data-stu-id="ceb3d-160">Sample code for a basic working implementation of Multi-Factor Authentication.</span></span>

> [!WARNING]
> <span data-ttu-id="ceb3d-161">Certyfikat klienta jest unikatowy certyfikat prywatny wygenerowany specjalnie dla Ciebie.</span><span class="sxs-lookup"><span data-stu-id="ceb3d-161">The client certificate is a unique private certificate that was generated especially for you.</span></span> <span data-ttu-id="ceb3d-162">Udostępnij lub nie utracić tego pliku.</span><span class="sxs-lookup"><span data-stu-id="ceb3d-162">Do not share or lose this file.</span></span> <span data-ttu-id="ceb3d-163">Jest kluczem do zapewnienia bezpieczeństwa komunikacji z usługą Multi-Factor Authentication.</span><span class="sxs-lookup"><span data-stu-id="ceb3d-163">It’s your key to ensuring the security of your communications with the Multi-Factor Authentication service.</span></span>

## <a name="code-sample"></a><span data-ttu-id="ceb3d-164">Przykład kodu</span><span class="sxs-lookup"><span data-stu-id="ceb3d-164">Code sample</span></span>
<span data-ttu-id="ceb3d-165">Ten przykładowy kod przedstawia sposób dodawania Tryb standardowy głosu wywołania weryfikacji do aplikacji przy użyciu interfejsów API w zestawie SDK Azure Multi-Factor Authentication.</span><span class="sxs-lookup"><span data-stu-id="ceb3d-165">This code sample shows you how to use the APIs in the Azure Multi-Factor Authentication SDK to add standard mode voice call verification to your application.</span></span> <span data-ttu-id="ceb3d-166">Tryb standardowy jest telefon użytkownika reaguje na naciśnięcie przycisku #.</span><span class="sxs-lookup"><span data-stu-id="ceb3d-166">Standard mode is a telephone call that the user responds to by pressing the # key.</span></span>

<span data-ttu-id="ceb3d-167">W tym przykładzie użyto C# .NET 2.0 SDK usługi Multi-Factor Authentication w podstawowej aplikacji ASP.NET w logice C# po stronie serwera, ale ten proces przypomina w innych językach.</span><span class="sxs-lookup"><span data-stu-id="ceb3d-167">This example uses the C# .NET 2.0 Multi-Factor Authentication SDK in a basic ASP.NET application with C# server-side logic, but the process is similar in other languages.</span></span> <span data-ttu-id="ceb3d-168">Ponieważ zestaw SDK zawiera pliki źródłowe, pliki wykonywalne nie można skompilować plików i ich odwołania lub umieścić je bezpośrednio w aplikacji.</span><span class="sxs-lookup"><span data-stu-id="ceb3d-168">Because the SDK includes source files, not executable files, you can build the files and reference them or include them directly in your application.</span></span>

> [!NOTE]
> <span data-ttu-id="ceb3d-169">Podczas wdrażania usługi Multi-Factor Authentication, należy użyć dodatkowe metody (Rozmowa telefoniczna lub wiadomości tekstowej) jako dodatkowej lub trzeciorzędny weryfikacji uzupełnienie metodę uwierzytelniania podstawowego (nazwa użytkownika i hasło).</span><span class="sxs-lookup"><span data-stu-id="ceb3d-169">When implementing Multi-Factor Authentication, use the additional methods (phone call or text message) as secondary or tertiary verification to supplement your primary authentication method (username and password).</span></span> <span data-ttu-id="ceb3d-170">Te metody nie są zaprojektowane jako metody uwierzytelniania podstawowego.</span><span class="sxs-lookup"><span data-stu-id="ceb3d-170">These methods are not designed as primary authentication methods.</span></span>

### <a name="code-sample-overview"></a><span data-ttu-id="ceb3d-171">Omówienie przykładowy kod</span><span class="sxs-lookup"><span data-stu-id="ceb3d-171">Code Sample Overview</span></span>
<span data-ttu-id="ceb3d-172">Ten przykładowy kod dla prostą aplikację sieci web pokaz używa połączenia telefonicznego z odpowiedzią klucza # do weryfikacji uwierzytelniania użytkownika.</span><span class="sxs-lookup"><span data-stu-id="ceb3d-172">This sample code for a simple web demo application uses a telephone call with a # key response to verify the user's authentication.</span></span> <span data-ttu-id="ceb3d-173">Współczynnik ten telefon jest określany w usłudze Multi-Factor Authentication jako tryb standardowy.</span><span class="sxs-lookup"><span data-stu-id="ceb3d-173">This telephone call factor is known in Multi-Factor Authentication as standard mode.</span></span>

<span data-ttu-id="ceb3d-174">Kod po stronie klienta nie ma żadnych elementów specyficznych dla usługi Multi-Factor Authentication.</span><span class="sxs-lookup"><span data-stu-id="ceb3d-174">The client-side code does not include any Multi-Factor Authentication-specific elements.</span></span> <span data-ttu-id="ceb3d-175">Czynniki dodatkowego uwierzytelniania są niezależne od podstawowego uwierzytelniania, dlatego można dodać je bez zmiany istniejącego interfejsu logowania jednokrotnego.</span><span class="sxs-lookup"><span data-stu-id="ceb3d-175">Because the additional authentication factors are independent of the primary authentication, you can add them without changing the existing sign-on interface.</span></span> <span data-ttu-id="ceb3d-176">Interfejsy API w zestawie SDK usługi Multi-Factor umożliwiają dostosowanie środowiska użytkownika, ale nie może być konieczne wprowadzanie zmian w ogóle.</span><span class="sxs-lookup"><span data-stu-id="ceb3d-176">The APIs in the Multi-Factor SDK let you customize the user experience, but you might not need to change anything at all.</span></span>

<span data-ttu-id="ceb3d-177">Kod po stronie serwera dodaje Tryb standardowy uwierzytelniania w kroku 2.</span><span class="sxs-lookup"><span data-stu-id="ceb3d-177">The server-side code adds standard-mode authentication in Step 2.</span></span> <span data-ttu-id="ceb3d-178">Tworzy obiekt PfAuthParams z parametrami, które są wymagane do weryfikacji Tryb standardowy: nazwa_użytkownika, telefonu numer oraz trybu i ścieżkę do certyfikatu klienta (CertFilePath), który jest wymagany w każdym wywołaniu.</span><span class="sxs-lookup"><span data-stu-id="ceb3d-178">It creates a PfAuthParams object with the parameters that are required for standard-mode verification: username, telephone number, and mode, and the path to the client certificate (CertFilePath), which is required in each call.</span></span> <span data-ttu-id="ceb3d-179">Pokaz wszystkich parametrów w PfAuthParams na ten temat można znaleźć w pliku przykładzie w zestawie SDK.</span><span class="sxs-lookup"><span data-stu-id="ceb3d-179">For a demonstration of all parameters in PfAuthParams, see the Example file in the SDK.</span></span>

<span data-ttu-id="ceb3d-180">Następnie kod przekazuje obiekt PfAuthParams funkcji pf_authenticate().</span><span class="sxs-lookup"><span data-stu-id="ceb3d-180">Next, the code passes the PfAuthParams object to the pf_authenticate() function.</span></span> <span data-ttu-id="ceb3d-181">Zwracana wartość wskazuje powodzenie lub niepowodzenie uwierzytelniania.</span><span class="sxs-lookup"><span data-stu-id="ceb3d-181">The return value indicates the success or failure of the authentication.</span></span> <span data-ttu-id="ceb3d-182">Parametry, callStatus oraz identyfikator błędu zawierają informacje wynik wywołania dodatkowe.</span><span class="sxs-lookup"><span data-stu-id="ceb3d-182">The out parameters, callStatus, and errorID, contain additional call result information.</span></span> <span data-ttu-id="ceb3d-183">Kody rezultatów połączeń są rejestrowane w pliku wyników wywołania w zestawie SDK.</span><span class="sxs-lookup"><span data-stu-id="ceb3d-183">The call result codes are documented in the call results file in the SDK.</span></span>

<span data-ttu-id="ceb3d-184">Ta implementacja minimalnego można pisać w zaledwie kilku wierszach.</span><span class="sxs-lookup"><span data-stu-id="ceb3d-184">This minimal implementation can be written in a few lines.</span></span> <span data-ttu-id="ceb3d-185">Jednak w kodzie produkcyjnym, można dołączyć dokładniejsze obsługi błędów kodu dodatkowej bazy danych i lepszą obsługę użytkowników.</span><span class="sxs-lookup"><span data-stu-id="ceb3d-185">However, in production code, you would include more sophisticated error handling, additional database code, and an enhanced user experience.</span></span>

### <a name="web-client-code"></a><span data-ttu-id="ceb3d-186">Kod klienta sieci Web</span><span class="sxs-lookup"><span data-stu-id="ceb3d-186">Web Client Code</span></span>
<span data-ttu-id="ceb3d-187">Poniżej znajduje się kod klienta sieci web dla strony demonstracyjnej.</span><span class="sxs-lookup"><span data-stu-id="ceb3d-187">The following is web client code for a demo page.</span></span>

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


### <a name="server-side-code"></a><span data-ttu-id="ceb3d-188">Kod po stronie serwera</span><span class="sxs-lookup"><span data-stu-id="ceb3d-188">Server-Side Code</span></span>
<span data-ttu-id="ceb3d-189">W poniższym kodzie po stronie serwera Multi-Factor Authentication jest skonfigurowany i uruchom w kroku 2.</span><span class="sxs-lookup"><span data-stu-id="ceb3d-189">In the following server-side code, Multi-Factor Authentication is configured and run in Step 2.</span></span> <span data-ttu-id="ceb3d-190">Tryb standardowy (MODE_STANDARD) jest połączeń telefonicznych, do którego użytkownik odpowiada, naciskając klawisz #.</span><span class="sxs-lookup"><span data-stu-id="ceb3d-190">Standard mode (MODE_STANDARD) is a telephone call to which the user responds by pressing the # key.</span></span>

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
            // Step 1: Validate the username and password
            if (username.Text != "Contoso" || password.Text != "password")
            {
                lblResult.ForeColor = System.Drawing.Color.Red;
                lblResult.Text = "Username or password incorrect.";
            }
            else
            {
                // Step 2: Perform multi-factor authentication

                // Add call details from the user database.
                PfAuthParams pfAuthParams = new PfAuthParams();
                pfAuthParams.Username = username.Text;
                pfAuthParams.Phone = "5555555555";
                pfAuthParams.Mode = pf_auth.MODE_STANDARD;

                // Specify a client certificate
                // NOTE: This file contains the private key for the client
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
