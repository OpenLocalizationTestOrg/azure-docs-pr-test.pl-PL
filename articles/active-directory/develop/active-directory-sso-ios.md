---
title: "Jak włączyć logowanie Jednokrotne wielu aplikacji w systemie iOS przy użyciu biblioteki ADAL | Dokumentacja firmy Microsoft"
description: "Jak używać funkcji ADAL zestawu SDK do Włącz rejestrację jednokrotną w aplikacji. "
services: active-directory
documentationcenter: 
author: brandwe
manager: mbaldwin
editor: 
ms.assetid: d042d6da-7503-4e20-bb55-06917de01fcd
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: ios
ms.devlang: objective-c
ms.topic: article
ms.date: 04/07/2017
ms.author: brandwe
ms.custom: aaddev
ms.openlocfilehash: 73b8ed7e6a153a0790f7eae9bd51bb2e554ae72e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-enable-cross-app-sso-on-ios-using-adal"></a><span data-ttu-id="25b19-103">Jak włączyć logowanie Jednokrotne wielu aplikacji w systemie iOS przy użyciu biblioteki ADAL</span><span class="sxs-lookup"><span data-stu-id="25b19-103">How to enable cross-app SSO on iOS using ADAL</span></span>
<span data-ttu-id="25b19-104">Zapewniające pojedynczego logowania jednokrotnego (SSO), aby użytkownicy potrzebują tylko może wprowadzić swoje poświadczenia raz, a te poświadczenia automatycznie działać przez aplikacje teraz jest oczekiwany przez klientów.</span><span class="sxs-lookup"><span data-stu-id="25b19-104">Providing Single Sign-On (SSO) so that users only need to enter their credentials once and have those credentials automatically work across applications is now expected by customers.</span></span> <span data-ttu-id="25b19-105">Trudności przy wprowadzaniu swoją nazwę użytkownika i hasło na małego ekranu, często razy łączyć się przy użyciu dodatkowego składnika (2FA), takich jak rozmowa telefoniczna lub kod wysłana wiadomość SMS, powoduje niezadowolenie szybki, jeśli użytkownik ma w tym celu więcej niż jeden raz na produkt.</span><span class="sxs-lookup"><span data-stu-id="25b19-105">The difficulty in entering their username and password on a small screen, often times combined with an additional factor (2FA) like a phone call or a texted code, results in quick dissatisfaction if a user has to do this more than one time for your product.</span></span>

<span data-ttu-id="25b19-106">Ponadto w przypadku zastosowania platformą tożsamości, które inne aplikacje mogą używać takich jak Accounts Microsoft lub konta służbowego z usługi Office 365, klienci oczekują, że te poświadczenia były dostępne do użycia w swoich aplikacjach niezależnie od dostawcy.</span><span class="sxs-lookup"><span data-stu-id="25b19-106">In addition, if you apply an identity platform that other applications may use such as Microsoft Accounts or a work account from Office365, customers expect that those credentials to be available to use across all their applications no matter the vendor.</span></span>

<span data-ttu-id="25b19-107">Platformy pakietu Microsoft Identity, wraz z nasze zestawy SDK tożsamości Microsoft robi to twarde pracy i daje możliwość doskonale dopasowanych swoich klientów za pomocą rejestracji Jednokrotnej w pakietu aplikacji lub, w przypadku naszego brokera możliwości i wystawcy uwierzytelnienia aplikacji, we wszystkich danych z urządzenia.</span><span class="sxs-lookup"><span data-stu-id="25b19-107">The Microsoft Identity platform, along with our Microsoft Identity SDKs, does all this hard work for you and gives you the ability to delight your customers with SSO either within your own suite of applications or, as with our broker capability and Authenticator applications, across the entire device.</span></span>

<span data-ttu-id="25b19-108">W tym przewodniku opisano, jak skonfigurować naszego zestawu SDK w celu zapewnienia takich korzyści klientom aplikacji.</span><span class="sxs-lookup"><span data-stu-id="25b19-108">This walkthrough will tell you how to configure our SDK within your application to provide this benefit to your customers.</span></span>

<span data-ttu-id="25b19-109">Ten przewodnik dotyczy:</span><span class="sxs-lookup"><span data-stu-id="25b19-109">This walkthrough applies to:</span></span>

* <span data-ttu-id="25b19-110">Usługa Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="25b19-110">Azure Active Directory</span></span>
* <span data-ttu-id="25b19-111">Azure Active Directory B2C</span><span class="sxs-lookup"><span data-stu-id="25b19-111">Azure Active Directory B2C</span></span>
* <span data-ttu-id="25b19-112">B2B usługi Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="25b19-112">Azure Active Directory B2B</span></span>
* <span data-ttu-id="25b19-113">Dostęp warunkowy usługi Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="25b19-113">Azure Active Directory Conditional Access</span></span>

<span data-ttu-id="25b19-114">Poprzedniego dokumentu zakłada wiesz, jak [udostępnić aplikacje w starszej wersji portalu usługi Azure Active Directory](active-directory-how-to-integrate.md) i zintegrowanych aplikacji z [pakietu Microsoft Identity iOS SDK](https://github.com/AzureAD/azure-activedirectory-library-for-objc).</span><span class="sxs-lookup"><span data-stu-id="25b19-114">The document preceding assumes you know how to [provision applications in the legacy portal for Azure Active Directory](active-directory-how-to-integrate.md) and integrated your application with the [Microsoft Identity iOS SDK](https://github.com/AzureAD/azure-activedirectory-library-for-objc).</span></span>

## <a name="sso-concepts-in-the-microsoft-identity-platform"></a><span data-ttu-id="25b19-115">Pojęcia dotyczące logowania jednokrotnego platformą tożsamości Microsoft</span><span class="sxs-lookup"><span data-stu-id="25b19-115">SSO Concepts in the Microsoft Identity Platform</span></span>
### <a name="microsoft-identity-brokers"></a><span data-ttu-id="25b19-116">Brokerzy tożsamość firmy Microsoft</span><span class="sxs-lookup"><span data-stu-id="25b19-116">Microsoft Identity Brokers</span></span>
<span data-ttu-id="25b19-117">Firma Microsoft udostępnia aplikacji dla każdej platformy przenośne, które umożliwiają łączenie poświadczeń w aplikacjach pochodzących od różnych dostawców i umożliwia specjalne udoskonalone funkcje, które wymagają pojedynczego bezpiecznym miejscu z, w którym można sprawdzić poprawności poświadczeń.</span><span class="sxs-lookup"><span data-stu-id="25b19-117">Microsoft provides applications for every mobile platform that allow for the bridging of credentials across applications from different vendors and allows for special enhanced features that require a single secure place from where to validate credentials.</span></span> <span data-ttu-id="25b19-118">Nazywamy je **brokerzy**.</span><span class="sxs-lookup"><span data-stu-id="25b19-118">We call these **brokers**.</span></span> <span data-ttu-id="25b19-119">W systemach iOS i Android te brokerzy są realizowane za pośrednictwem aplikacji do pobrania, czy klienci zainstalować niezależnie lub może zostać umieszczony na urządzeniu przez użytkowników, którzy zarządzają niektórych lub wszystkich urządzeń dla swoich pracowników firmy.</span><span class="sxs-lookup"><span data-stu-id="25b19-119">On iOS and Android these brokers are provided through downloadable applications that customers either install independently or can be pushed to the device by a company who manages some or all of the device for their employee.</span></span> <span data-ttu-id="25b19-120">Te brokerzy obsługę zarządzania zabezpieczeń tylko niektóre aplikacje lub wszystkich danych z urządzenia oparte na potrzeby administratorzy IT.</span><span class="sxs-lookup"><span data-stu-id="25b19-120">These brokers support managing security just for some applications or the entire device based on what IT Administrators desire.</span></span> <span data-ttu-id="25b19-121">W systemie Windows ta funkcja jest dostarczana przez selektora konta z wbudowanej w system operacyjny, znane pod względem technicznym jako Broker uwierzytelniania sieci Web.</span><span class="sxs-lookup"><span data-stu-id="25b19-121">In Windows, this functionality is provided by an account chooser built in to the operating system, known technically as the Web Authentication Broker.</span></span>

<span data-ttu-id="25b19-122">Aby uzyskać więcej informacji na temat używamy tych brokerów i jak klienci mogą je wyświetlać w ich przepływu logowania na platformy pakietu Microsoft Identity.</span><span class="sxs-lookup"><span data-stu-id="25b19-122">For more information on how we use these brokers and how your customers might see them in their login flow for the Microsoft Identity platform read on.</span></span>

### <a name="patterns-for-logging-in-on-mobile-devices"></a><span data-ttu-id="25b19-123">Wzorce do logowania na urządzeniach przenośnych</span><span class="sxs-lookup"><span data-stu-id="25b19-123">Patterns for logging in on mobile devices</span></span>
<span data-ttu-id="25b19-124">Dostęp do poświadczeń na urządzeniach wykonaj dwa podstawowe wzorce platformy pakietu Microsoft Identity:</span><span class="sxs-lookup"><span data-stu-id="25b19-124">Access to credentials on devices follow two basic patterns for the Microsoft Identity platform:</span></span>

* <span data-ttu-id="25b19-125">Logowania asystowaną bez brokera</span><span class="sxs-lookup"><span data-stu-id="25b19-125">Non-broker assisted logins</span></span>
* <span data-ttu-id="25b19-126">Broker asystowaną logowania</span><span class="sxs-lookup"><span data-stu-id="25b19-126">Broker assisted logins</span></span>

#### <a name="non-broker-assisted-logins"></a><span data-ttu-id="25b19-127">Logowania asystowaną bez brokera</span><span class="sxs-lookup"><span data-stu-id="25b19-127">Non-broker assisted logins</span></span>
<span data-ttu-id="25b19-128">Inne niż brokera asystowaną logowania są środowiska logowania, być wbudowane w aplikacji, które obsługują Magazyn lokalny na urządzeniu dla tej aplikacji.</span><span class="sxs-lookup"><span data-stu-id="25b19-128">Non-broker assisted logins are login experiences that happen inline with the application and use the local storage on the device for that application.</span></span> <span data-ttu-id="25b19-129">Ten magazyn może być współużytkowany przez aplikacje, ale poświadczenia są ściśle powiązane z aplikacji lub pakietu aplikacji przy użyciu tego poświadczenia.</span><span class="sxs-lookup"><span data-stu-id="25b19-129">This storage may be shared across applications but the credentials are tightly bound to the app or suite of apps using that credential.</span></span> <span data-ttu-id="25b19-130">W przypadku najprawdopodobniej wystąpienia to w wielu aplikacjach mobilnych podczas wprowadzania nazwy użytkownika i hasła samej aplikacji.</span><span class="sxs-lookup"><span data-stu-id="25b19-130">You've most likely experienced this in many mobile applications when you enter a username and password within the application itself.</span></span>

<span data-ttu-id="25b19-131">Te nazwy logowania są następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="25b19-131">These logins have the following benefits:</span></span>

* <span data-ttu-id="25b19-132">Środowisko użytkownika istnieje całkowicie w aplikacji.</span><span class="sxs-lookup"><span data-stu-id="25b19-132">User experience exists entirely within the application.</span></span>
* <span data-ttu-id="25b19-133">Poświadczenia mogą być udostępniane między aplikacjami, które są podpisane przez ten sam certyfikat, zapewniając pojedynczego środowisko logowania do pakietu aplikacji.</span><span class="sxs-lookup"><span data-stu-id="25b19-133">Credentials can be shared across applications that are signed by the same certificate, providing a single sign-on experience to your suite of applications.</span></span>
* <span data-ttu-id="25b19-134">Formant wokół środowisko logowania jest dostarczany do aplikacji przed i po zalogowaniu.</span><span class="sxs-lookup"><span data-stu-id="25b19-134">Control around the experience of logging in is provided to the application before and after sign-in.</span></span>

<span data-ttu-id="25b19-135">Te nazwy logowania ma następujące wady:</span><span class="sxs-lookup"><span data-stu-id="25b19-135">These logins have the following drawbacks:</span></span>

* <span data-ttu-id="25b19-136">Użytkownika nie może występować jednokrotnego we wszystkich aplikacji, które używają pakietu Microsoft Identity przez te firmy Microsoft Identities skonfigurowane w aplikacji.</span><span class="sxs-lookup"><span data-stu-id="25b19-136">User cannot experience single-sign on across all apps that use a Microsoft Identity, only across those Microsoft Identities that your application has configured.</span></span>
* <span data-ttu-id="25b19-137">Aplikacji nie można używać z bardziej zaawansowane funkcje biznesowych, takich jak dostęp warunkowy, lub użyj produktów pakietu usługi InTune.</span><span class="sxs-lookup"><span data-stu-id="25b19-137">Your application cannot be used with more advanced business features such as Conditional Access or use the InTune suite of products.</span></span>
* <span data-ttu-id="25b19-138">Używana aplikacja nie obsługuje uwierzytelniania opartego na certyfikatach dla użytkowników biznesowych.</span><span class="sxs-lookup"><span data-stu-id="25b19-138">Your application can't support certificate-based authentication for business users.</span></span>

<span data-ttu-id="25b19-139">Oto reprezentację działanie zestawów SDK tożsamość firmy Microsoft z magazynem udostępnionym aplikacji do włączenia funkcji logowania jednokrotnego:</span><span class="sxs-lookup"><span data-stu-id="25b19-139">Here is a representation of how the Microsoft Identity SDKs work with the shared storage of your applications to enable SSO:</span></span>

```
+------------+ +------------+  +-------------+
|            | |            |  |             |
|   App 1    | |   App 2    |  |   App 3     |
|            | |            |  |             |
|            | |            |  |             |
+------------+ +------------+  +-------------+
| ADAL SDK  |  |  ADAL SDK  |  |  ADAK SDK   |
+------------+-+------------+--+-------------+
|                                            |
|            App Shared Storage              |
+--------------------------------------------+
```

#### <a name="broker-assisted-logins"></a><span data-ttu-id="25b19-140">Broker asystowaną logowania</span><span class="sxs-lookup"><span data-stu-id="25b19-140">Broker assisted logins</span></span>
<span data-ttu-id="25b19-141">Asystowane brokera logowania są funkcji logowania, które występują w aplikacji brokera i korzystania z magazynu i zabezpieczeń brokera udostępnianie poświadczeń we wszystkich aplikacjach na urządzeniu, mające zastosowanie platformy pakietu Microsoft Identity.</span><span class="sxs-lookup"><span data-stu-id="25b19-141">Broker-assisted logins are login experiences that occur within the broker application and use the storage and security of the broker to share credentials across all applications on the device that apply the Microsoft Identity platform.</span></span> <span data-ttu-id="25b19-142">Oznacza to, że aplikacje zależne od brokera do logowania użytkowników.</span><span class="sxs-lookup"><span data-stu-id="25b19-142">This means that your applications rely on the broker to sign users in.</span></span> <span data-ttu-id="25b19-143">W systemach iOS i Android brokerzy te są realizowane za pośrednictwem aplikacji do pobrania, czy klientów zainstalować niezależnie lub może zostać umieszczony na urządzeniu przez firmę, użytkowników, którzy zarządzają urządzenia dla ich użytkownika.</span><span class="sxs-lookup"><span data-stu-id="25b19-143">On iOS and Android these brokers are provided through downloadable applications that customers either install independently or can be pushed to the device by a company who manages the device for their user.</span></span> <span data-ttu-id="25b19-144">Przykładowe aplikacje tego typu jest aplikacja Microsoft Authenticator w systemie iOS.</span><span class="sxs-lookup"><span data-stu-id="25b19-144">An example of this type of application is the Microsoft Authenticator application on iOS.</span></span> <span data-ttu-id="25b19-145">W systemie Windows ta funkcja jest dostarczana przez selektora konta z wbudowanej w system operacyjny, znane pod względem technicznym jako Broker uwierzytelniania sieci Web.</span><span class="sxs-lookup"><span data-stu-id="25b19-145">In Windows this functionality is provided by an account chooser built in to the operating system, known technically as the Web Authentication Broker.</span></span>
<span data-ttu-id="25b19-146">Środowisko jest zależna od platformy i czasami mogą być uciążliwe dla użytkowników w przeciwnym razie zarządzane prawidłowo.</span><span class="sxs-lookup"><span data-stu-id="25b19-146">The experience varies by platform and can sometimes be disruptive to users if not managed correctly.</span></span> <span data-ttu-id="25b19-147">Znasz prawdopodobnie najbardziej tego wzorca Jeśli z zainstalowaną aplikacją Facebook i używać funkcji usługi Facebook połączenie z innej aplikacji.</span><span class="sxs-lookup"><span data-stu-id="25b19-147">You're probably most familiar with this pattern if you have the Facebook application installed and use Facebook Connect from another application.</span></span> <span data-ttu-id="25b19-148">Platforma Microsoft Identity używa tego samego wzorca.</span><span class="sxs-lookup"><span data-stu-id="25b19-148">The Microsoft Identity platform uses the same pattern.</span></span>

<span data-ttu-id="25b19-149">Dla systemu iOS, który prowadzi to do "przejścia" animacji, w którym aplikacji są wysyłane do tła podczas aplikacji Microsoft Authenticator zawiera pierwszego planu dla użytkownika wybrać konto, które chce się zalogować.</span><span class="sxs-lookup"><span data-stu-id="25b19-149">For iOS this leads to a "transition" animation where your application is sent to the background while the Microsoft Authenticator applications comes to the foreground for the user to select which account they would like to sign in with.</span></span>  

<span data-ttu-id="25b19-150">Dla systemów Android i Windows selektora konta jest wyświetlany u góry aplikację, która jest prostszy sposób użytkownika.</span><span class="sxs-lookup"><span data-stu-id="25b19-150">For Android and Windows the account chooser is displayed on top of your application which is less disruptive to the user.</span></span>

#### <a name="how-the-broker-gets-invoked"></a><span data-ttu-id="25b19-151">Sposób wywoływania pobiera brokera</span><span class="sxs-lookup"><span data-stu-id="25b19-151">How the broker gets invoked</span></span>
<span data-ttu-id="25b19-152">Zgodne brokera jest zainstalowany na urządzeniu, takie jak aplikacja Microsoft Authenticator zestawów SDK tożsamości Microsoft będzie automatycznie wykonywać pracy wywoływania brokera automatycznie, gdy użytkownik wskazuje chcą zalogowanie się przy użyciu dowolnego konta z platformy Microsoft Identity.</span><span class="sxs-lookup"><span data-stu-id="25b19-152">If a compatible broker is installed on the device, like the Microsoft Authenticator application, the Microsoft Identity SDKs will automatically do the work of invoking the broker for you when a user indicates they wish to log in using any account from the Microsoft Identity platform.</span></span> <span data-ttu-id="25b19-153">To konto może być Account firmy Microsoft, służbowy lub konta służbowego lub konta, które należy podać i hosta na platformie Azure przy użyciu naszych produktów B2C i B2B.</span><span class="sxs-lookup"><span data-stu-id="25b19-153">This account could be a personal Microsoft Account, a work or school account, or an account that you provide and host in Azure using our B2C and B2B products.</span></span> 

 #### <a name="how-we-ensure-the-application-is-valid"></a><span data-ttu-id="25b19-154">Jak firma Microsoft zapewnia aplikacji jest prawidłowy</span><span class="sxs-lookup"><span data-stu-id="25b19-154">How we ensure the application is valid</span></span>
 
 <span data-ttu-id="25b19-155">Konieczność zapewnienia tożsamości wywołanie aplikacji, które brokera odgrywa kluczową rolę zabezpieczeń, które udostępniamy w brokerze pomocy logowania.</span><span class="sxs-lookup"><span data-stu-id="25b19-155">The need to ensure the identity of an application call the broker is crucial to the security we provide in broker assisted logins.</span></span> <span data-ttu-id="25b19-156">Z systemem iOS ani Android wymusza unikatowych identyfikatorów, które są prawidłowe tylko dla danej aplikacji, więc złośliwego aplikacji może "sfałszować" identyfikator uzasadnionych aplikacji i odbierać tokeny przeznaczone dla aplikacji uzasadnione.</span><span class="sxs-lookup"><span data-stu-id="25b19-156">Neither iOS nor Android enforces unique identifiers that are valid only for a given application, so malicious applications may "spoof" a legitimate application's identifier and receive the tokens meant for the legitimate application.</span></span> <span data-ttu-id="25b19-157">Aby upewnić się, że zawsze komunikują się firma Microsoft z prawej aplikacji w czasie wykonywania, poprosimy developer do niestandardowych redirectURI podczas rejestrowania swoich aplikacji z firmą Microsoft.</span><span class="sxs-lookup"><span data-stu-id="25b19-157">To ensure we are always communicating with the right application at runtime, we ask the developer to provide a custom redirectURI when registering their application with Microsoft.</span></span> <span data-ttu-id="25b19-158">**Jak deweloperzy powinien spreparować identyfikator URI przekierowania omówiono szczegółowo poniżej.**</span><span class="sxs-lookup"><span data-stu-id="25b19-158">**How developers should craft this redirect URI is discussed in detail below.**</span></span> <span data-ttu-id="25b19-159">To niestandardowe redirectURI zawiera identyfikator pakietu aplikacji i zapewniony unikatowa do aplikacji w sklepie Apple App.</span><span class="sxs-lookup"><span data-stu-id="25b19-159">This custom redirectURI contains the Bundle ID of the application and is ensured to be unique to the application by the Apple App Store.</span></span> <span data-ttu-id="25b19-160">Gdy aplikacja wywołuje brokera, broker zapyta, systemu operacyjnego z systemem iOS do tego celu o identyfikatorze pakietu, który wywołał brokera.</span><span class="sxs-lookup"><span data-stu-id="25b19-160">When an application calls the broker, the broker asks the iOS operating system to provide it with the Bundle ID that called the broker.</span></span> <span data-ttu-id="25b19-161">Broker ten identyfikator pakietu do firmy Microsoft w wywołaniu naszym systemie tożsamości.</span><span class="sxs-lookup"><span data-stu-id="25b19-161">The broker provides this Bundle ID to Microsoft in the call to our identity system.</span></span> <span data-ttu-id="25b19-162">Jeśli identyfikator pakietu aplikacji nie odpowiada identyfikator pakietu przekazanego nam przez projektanta podczas rejestracji, firma Microsoft będzie odmawiał żąda dostępu do tokenów dla zasobów aplikacji.</span><span class="sxs-lookup"><span data-stu-id="25b19-162">If the Bundle ID of the application does not match the Bundle ID provided to us by the developer during registration, we will deny access to the tokens for the resource the application is requesting.</span></span> <span data-ttu-id="25b19-163">Tego wyboru gwarantuje, że tylko aplikacja zarejestrowany przez dewelopera otrzyma tokenów.</span><span class="sxs-lookup"><span data-stu-id="25b19-163">This check ensures that only the application registered by the developer receives tokens.</span></span>

<span data-ttu-id="25b19-164">**Deweloper może wybrać opcję Microsoft tożsamość SDK wywołuje brokera lub korzysta z przepływu asystowaną bez brokera.**</span><span class="sxs-lookup"><span data-stu-id="25b19-164">**The developer has the choice of if the Microsoft Identity SDK calls the broker or uses the non-broker assisted flow.**</span></span> <span data-ttu-id="25b19-165">Jednak jeśli wybierze projektanta nie należy używać przepływu wspierana brokera utracą zaletą używania poświadczeń logowania jednokrotnego, czy użytkownik może już dodane na urządzeniu i uniemożliwia ich aplikacji z używane z funkcjami firm, które firma Microsoft udostępnia jej klientów, takie jak dostęp warunkowy, możliwości zarządzania usługi Intune i uwierzytelnianie oparte na certyfikatach.</span><span class="sxs-lookup"><span data-stu-id="25b19-165">However if the developer chooses not to use the broker-assisted flow they lose the benefit of using SSO credentials that the user may have already added on the device and prevents their application from being used with business features Microsoft provides its customers such as Conditional Access, Intune Management capabilities, and certificate-based authentication.</span></span>

<span data-ttu-id="25b19-166">Te nazwy logowania są następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="25b19-166">These logins have the following benefits:</span></span>

* <span data-ttu-id="25b19-167">Użytkownik napotyka logowania jednokrotnego w swoich aplikacjach niezależnie od dostawcy.</span><span class="sxs-lookup"><span data-stu-id="25b19-167">User experiences SSO across all their applications no matter the vendor.</span></span>
* <span data-ttu-id="25b19-168">Aplikacja może użyć bardziej zaawansowane funkcje biznesowych, takich jak dostęp warunkowy lub produktów pakietu usługi InTune.</span><span class="sxs-lookup"><span data-stu-id="25b19-168">Your application can use more advanced business features such as Conditional Access or use the InTune suite of products.</span></span>
* <span data-ttu-id="25b19-169">Aplikacja może obsługiwać uwierzytelnianie oparte na certyfikatach dla użytkowników biznesowych.</span><span class="sxs-lookup"><span data-stu-id="25b19-169">Your application can support certificate-based authentication for business users.</span></span>
* <span data-ttu-id="25b19-170">Bezpieczniejszym logowania jako tożsamość aplikacji i użytkownika są weryfikowane przez aplikację broker z algorytmów zabezpieczeń i szyfrowania.</span><span class="sxs-lookup"><span data-stu-id="25b19-170">Much more secure sign-in experience as the identity of the application and the user are verified by the broker application with additional security algorithms and encryption.</span></span>

<span data-ttu-id="25b19-171">Te nazwy logowania ma następujące wady:</span><span class="sxs-lookup"><span data-stu-id="25b19-171">These logins have the following drawbacks:</span></span>

* <span data-ttu-id="25b19-172">W systemie iOS użytkownika jest są przenoszone poza środowisko aplikacji, a poświadczenia zostały wybrane.</span><span class="sxs-lookup"><span data-stu-id="25b19-172">In iOS the user is transitioned out of your application's experience while credentials are chosen.</span></span>
* <span data-ttu-id="25b19-173">Utrata możliwości zarządzania mogą logować się klienci w aplikacji.</span><span class="sxs-lookup"><span data-stu-id="25b19-173">Loss of the ability to manage the login experience for your customers within your application.</span></span>

<span data-ttu-id="25b19-174">Oto reprezentację działanie zestawów SDK tożsamość firmy Microsoft z aplikacji brokera do włączenia funkcji logowania jednokrotnego:</span><span class="sxs-lookup"><span data-stu-id="25b19-174">Here is a representation of how the Microsoft Identity SDKs work with the broker applications to enable SSO:</span></span>

```
+------------+ +------------+   +-------------+
|            | |            |   |             |
|   App 1    | |   App 2    |   |   Someone   |
|            | |            |   |    Else's   |
|            | |            |   |     App     |
+------------+ +------------+   +-------------+
| Azure SDK  | | Azure SDK  |   | Azure SDK   |
+-----+------+-+-----+------+-  +-------+-----+
      |              |                  |
      |       +------v------+           |
      |       |             |           |
      |       | Microsoft   |           |
      +-------> Broker      |^----------+
              | Application
              |             |
              +-------------+
              |             |
              |   Broker    |
              |   Storage   |
              |             |
              +-------------+
```

<span data-ttu-id="25b19-175">Dzięki tej ogólne informacje, które powinno być możliwe do lepszego zrozumienia i implementowanie logowania jednokrotnego w aplikacji przy użyciu pakietu Microsoft Identity platformy i zestawy SDK.</span><span class="sxs-lookup"><span data-stu-id="25b19-175">Armed with this background information you should be able to better understand and implement SSO within your application using the Microsoft Identity platform and SDKs.</span></span>

## <a name="enabling-cross-app-sso-using-adal"></a><span data-ttu-id="25b19-176">Włączanie logowania jednokrotnego wielu aplikacji za pomocą biblioteki ADAL</span><span class="sxs-lookup"><span data-stu-id="25b19-176">Enabling cross-app SSO using ADAL</span></span>
<span data-ttu-id="25b19-177">W tym miejscu używamy ADAL zestaw SDK dla systemu iOS do:</span><span class="sxs-lookup"><span data-stu-id="25b19-177">Here we use the ADAL iOS SDK to:</span></span>

* <span data-ttu-id="25b19-178">Włącz brokera z systemem innym niż asystowaną pomocą rejestracji Jednokrotnej dla pakietu aplikacji</span><span class="sxs-lookup"><span data-stu-id="25b19-178">Turn on non-broker assisted SSO for your suite of apps</span></span>
* <span data-ttu-id="25b19-179">Włączanie obsługi wspierana brokera logowania jednokrotnego</span><span class="sxs-lookup"><span data-stu-id="25b19-179">Turn on support for broker-assisted SSO</span></span>

### <a name="turning-on-sso-for-non-broker-assisted-sso"></a><span data-ttu-id="25b19-180">Włączanie rejestracji Jednokrotnej z systemem innym niż brokera asystowaną pomocą rejestracji Jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="25b19-180">Turning on SSO for non-broker assisted SSO</span></span>
<span data-ttu-id="25b19-181">Dla bez brokera asystowaną logowania jednokrotnego w aplikacjach zestawów SDK tożsamości Microsoft zarządzać znacznie złożoność logowania jednokrotnego dla Ciebie.</span><span class="sxs-lookup"><span data-stu-id="25b19-181">For non-broker assisted SSO across applications the Microsoft Identity SDKs manage much of the complexity of SSO for you.</span></span> <span data-ttu-id="25b19-182">Obejmuje to wyszukiwanie prawo użytkownika w pamięci podręcznej i przechowywania listy zalogowany użytkowników możesz zbadać.</span><span class="sxs-lookup"><span data-stu-id="25b19-182">This includes finding the right user in the cache and maintaining a list of logged in users for you to query.</span></span>

<span data-ttu-id="25b19-183">Do włączenia funkcji logowania jednokrotnego w aplikacjach jesteś właścicielem, że należy wykonać następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="25b19-183">To enable SSO across applications you own you need to do the following:</span></span>

1. <span data-ttu-id="25b19-184">Upewnij się użytkownika aplikacje tego samego Identyfikatora klienta lub identyfikator aplikacji.</span><span class="sxs-lookup"><span data-stu-id="25b19-184">Ensure all your applications user the same Client ID or Application ID.</span></span>
2. <span data-ttu-id="25b19-185">Upewnij się, dzięki czemu można udostępniać pęki kluczy wszystkie aplikacje współużytkują ten sam certyfikat podpisywania firmy Apple</span><span class="sxs-lookup"><span data-stu-id="25b19-185">Ensure that all of your applications share the same signing certificate from Apple so that you can share keychains</span></span>
3. <span data-ttu-id="25b19-186">Żądanie uprawnienie łańcucha kluczy dla poszczególnych aplikacji.</span><span class="sxs-lookup"><span data-stu-id="25b19-186">Request the same keychain entitlement for each of your applications.</span></span>
4. <span data-ttu-id="25b19-187">Opisz zestawów SDK tożsamości Microsoft udostępnionego łańcucha kluczy, które chcesz nam do użycia.</span><span class="sxs-lookup"><span data-stu-id="25b19-187">Tell the Microsoft Identity SDKs about the shared keychain you want us to use.</span></span>

#### <a name="using-the-same-client-id--application-id-for-all-the-applications-in-your-suite-of-apps"></a><span data-ttu-id="25b19-188">Za pomocą tego samego Identyfikatora klienta / IDENTYFIKATORA aplikacji dla wszystkich aplikacji w pakietu aplikacji</span><span class="sxs-lookup"><span data-stu-id="25b19-188">Using the same Client ID / Application ID for all the applications in your suite of apps</span></span>
<span data-ttu-id="25b19-189">Aby platformy pakietu Microsoft Identity dowiedzieć się, że mogą być udostępnianie tokenów w aplikacji należy poszczególnych aplikacji do udostępniania tego samego Identyfikatora klienta lub identyfikator aplikacji.</span><span class="sxs-lookup"><span data-stu-id="25b19-189">In order for the Microsoft Identity platform to know that it's allowed to share tokens across your applications, each of your applications will need to share the same Client ID or Application ID.</span></span> <span data-ttu-id="25b19-190">Jest to unikatowy identyfikator, który został udostępniony po zarejestrowaniu swoją pierwszą aplikację w portalu.</span><span class="sxs-lookup"><span data-stu-id="25b19-190">This is the unique identifier that was provided to you when you registered your first application in the portal.</span></span>

<span data-ttu-id="25b19-191">Możesz się zastanawiać, jak należy określić różnych aplikacji z usługą Microsoft Identity korzysta z tego samego identyfikatora aplikacji</span><span class="sxs-lookup"><span data-stu-id="25b19-191">You may be wondering how you will identify different apps to the Microsoft Identity service if it uses the same Application ID.</span></span> <span data-ttu-id="25b19-192">Odpowiedź jest z **identyfikator URI przekierowania**.</span><span class="sxs-lookup"><span data-stu-id="25b19-192">The answer is with the **Redirect URIs**.</span></span> <span data-ttu-id="25b19-193">Każda aplikacja może mieć wiele identyfikator URI przekierowania zarejestrowany w portalu przy dołączaniu.</span><span class="sxs-lookup"><span data-stu-id="25b19-193">Each application can have multiple Redirect URIs registered in the onboarding portal.</span></span> <span data-ttu-id="25b19-194">Każdej aplikacji w zestawie ma inny identyfikator URI przekierowania.</span><span class="sxs-lookup"><span data-stu-id="25b19-194">Each app in your suite will have a different redirect URI.</span></span> <span data-ttu-id="25b19-195">Jak wygląda przykład znajduje się poniżej:</span><span class="sxs-lookup"><span data-stu-id="25b19-195">An example of how this looks is below:</span></span>

<span data-ttu-id="25b19-196">Identyfikator URI przekierowania App1`x-msauth-mytestiosapp://com.myapp.mytestapp`</span><span class="sxs-lookup"><span data-stu-id="25b19-196">App1 Redirect URI: `x-msauth-mytestiosapp://com.myapp.mytestapp`</span></span>

<span data-ttu-id="25b19-197">Identyfikator URI przekierowania App2`x-msauth-mytestiosapp://com.myapp.mytestapp2`</span><span class="sxs-lookup"><span data-stu-id="25b19-197">App2 Redirect URI: `x-msauth-mytestiosapp://com.myapp.mytestapp2`</span></span>

<span data-ttu-id="25b19-198">Identyfikator URI przekierowania App3:`x-msauth-mytestiosapp://com.myapp.mytestapp3`</span><span class="sxs-lookup"><span data-stu-id="25b19-198">App3 Redirect URI: `x-msauth-mytestiosapp://com.myapp.mytestapp3`</span></span>

<span data-ttu-id="25b19-199">....</span><span class="sxs-lookup"><span data-stu-id="25b19-199">....</span></span>

<span data-ttu-id="25b19-200">Te są zagnieżdżone w tym samym identyfikatorze klienta / identyfikator aplikacji i wyszukiwać oparte na przekierowanie URI powrócisz do nas w konfiguracji zestawu SDK.</span><span class="sxs-lookup"><span data-stu-id="25b19-200">These are nested under the same client ID / application ID and looked up based on the redirect URI you return to us in your SDK configuration.</span></span>

```
+-------------------+
|                   |
|  Client ID        |
+---------+---------+
          |
          |           +-----------------------------------+
          |           |  App 1 Redirect URI               |
          +----------^+                                   |
          |           +-----------------------------------+
          |
          |           +-----------------------------------+
          +----------^+  App 2 Redirect URI               |
          |           |                                   |
          |           +-----------------------------------+
          |
          +----------^+-----------------------------------+
                      |  App 3 Redirect URI               |
                      |                                   |
                      +-----------------------------------+

```


<span data-ttu-id="25b19-201">*Należy pamiętać, że format tych identyfikator URI przekierowania opisano szczegółowo poniżej. Można użyć identyfikatora URI przekierowania, chyba że chcesz wspierać brokera, w takim przypadku one musi wyglądać powyższych*</span><span class="sxs-lookup"><span data-stu-id="25b19-201">*Note that the format of these Redirect URIs are explained below. You may use any Redirect URI unless you wish to support the broker, in which case they must look something like the above*</span></span>

#### <a name="create-keychain-sharing-between-applications"></a><span data-ttu-id="25b19-202">Tworzenie łańcucha kluczy udostępnianie między aplikacjami</span><span class="sxs-lookup"><span data-stu-id="25b19-202">Create keychain sharing between applications</span></span>
<span data-ttu-id="25b19-203">Włączenie udostępniania łańcucha kluczy wykracza poza zakres tego dokumentu i objęte ich dokumentu przez firmę Apple [Dodawanie możliwości](https://developer.apple.com/library/ios/documentation/IDEs/Conceptual/AppDistributionGuide/AddingCapabilities/AddingCapabilities.html).</span><span class="sxs-lookup"><span data-stu-id="25b19-203">Enabling keychain sharing is beyond the scope of this document and covered by Apple in their document [Adding Capabilities](https://developer.apple.com/library/ios/documentation/IDEs/Conceptual/AppDistributionGuide/AddingCapabilities/AddingCapabilities.html).</span></span> <span data-ttu-id="25b19-204">Ważne jest zdecyduj, jakie chcesz z łańcucha kluczy ma być wywoływana i dodania tej możliwości we wszystkich aplikacjach.</span><span class="sxs-lookup"><span data-stu-id="25b19-204">What is important is that you decide what you want your keychain to be called and add that capability across all your applications.</span></span>

<span data-ttu-id="25b19-205">Jeśli masz plik w katalogu projektu pod tytułem powinna zostać wyświetlona poprawnie można skonfigurować uprawnienia do `entitlements.plist` zawierający element, który wygląda podobnie do następującej:</span><span class="sxs-lookup"><span data-stu-id="25b19-205">When you do have entitlements set up correctly you should see a file in your project directory entitled `entitlements.plist` that contains something that looks like the following:</span></span>

```
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE plist PUBLIC "-//Apple//DTD PLIST 1.0//EN" "http://www.apple.com/DTDs/PropertyList-1.0.dtd">
<plist version="1.0">
<dict>
    <key>keychain-access-groups</key>
    <array>
        <string>$(AppIdentifierPrefix)com.myapp.mytestapp</string>
        <string>$(AppIdentifierPrefix)com.myapp.mycache</string>
    </array>
</dict>
</plist>
```

<span data-ttu-id="25b19-206">Po masz uprawnienie łańcucha kluczy włączone w każdej aplikacji i wszystko jest gotowe do za pomocą logowania jednokrotnego, opisz Microsoft tożsamość SDK z łańcucha kluczy za pomocą następującego ustawienia w Twojej `ADAuthenticationSettings` z następującymi ustawieniami:</span><span class="sxs-lookup"><span data-stu-id="25b19-206">Once you have the keychain entitlement enabled in each of your applications, and you are ready to use SSO, tell the Microsoft Identity SDK about your keychain by using the following setting in your `ADAuthenticationSettings` with the following setting:</span></span>

```
defaultKeychainSharingGroup=@"com.myapp.mycache";
```

> [!WARNING]
> <span data-ttu-id="25b19-207">Jeśli udostępnianie łańcucha kluczy w aplikacji dowolnej aplikacji, można usunąć użytkowników lub gorsze usunąć wszystkie tokeny w aplikacji.</span><span class="sxs-lookup"><span data-stu-id="25b19-207">When you share a keychain across your applications any application can delete users or worse delete all the tokens across your application.</span></span> <span data-ttu-id="25b19-208">Jest to szczególnie Fatalne, jeśli masz aplikacje korzystające z tokenów do pracy w tle.</span><span class="sxs-lookup"><span data-stu-id="25b19-208">This is particularly disastrous if you have applications that rely on the tokens to do background work.</span></span> <span data-ttu-id="25b19-209">Udostępnianie łańcucha kluczy oznacza, że należy zachować ostrożność bardzo w wszystkie Usuń operacji za pomocą zestawów SDK tożsamość firmy Microsoft.</span><span class="sxs-lookup"><span data-stu-id="25b19-209">Sharing a keychain means that you must be very careful in any and all remove operations through the Microsoft Identity SDKs.</span></span>
> 
> 

<span data-ttu-id="25b19-210">Gotowe.</span><span class="sxs-lookup"><span data-stu-id="25b19-210">That's it!</span></span> <span data-ttu-id="25b19-211">Zestaw SDK usługi Microsoft Identity teraz udostępniać poświadczeń we wszystkich aplikacjach.</span><span class="sxs-lookup"><span data-stu-id="25b19-211">The Microsoft Identity SDK will now share credentials across all your applications.</span></span> <span data-ttu-id="25b19-212">Lista użytkowników również będą udostępniane między wystąpieniami aplikacji.</span><span class="sxs-lookup"><span data-stu-id="25b19-212">The user list will also be shared across application instances.</span></span>

### <a name="turning-on-sso-for-broker-assisted-sso"></a><span data-ttu-id="25b19-213">Włączanie logowania jednokrotnego dla brokera asystowaną pomocą rejestracji Jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="25b19-213">Turning on SSO for broker assisted SSO</span></span>
<span data-ttu-id="25b19-214">Dla aplikacji pod kątem wykorzystania brokera, wszelkie zainstalowanego na urządzeniu jest **domyślnie wyłączone**.</span><span class="sxs-lookup"><span data-stu-id="25b19-214">The ability for an application to use any broker that is installed on the device is **turned off by default**.</span></span> <span data-ttu-id="25b19-215">Aby korzystać z aplikacji w brokera muszą nie dodatkowej konfiguracji i dodać kod do aplikacji.</span><span class="sxs-lookup"><span data-stu-id="25b19-215">In order to use your application with the broker you must do some additional configuration and add some code to your application.</span></span>

<span data-ttu-id="25b19-216">Wykonaj kroki są:</span><span class="sxs-lookup"><span data-stu-id="25b19-216">The steps to follow are:</span></span>

1. <span data-ttu-id="25b19-217">Włącz tryb brokera w kodzie aplikacji wywołania MS SDK.</span><span class="sxs-lookup"><span data-stu-id="25b19-217">Enable broker mode in your application code's call to the MS SDK.</span></span>
2. <span data-ttu-id="25b19-218">Ustanów nowy identyfikator URI przekierowania i zapewnić do rejestracji aplikacji i aplikacji.</span><span class="sxs-lookup"><span data-stu-id="25b19-218">Establish a new redirect URI and provide that to both the app and your app registration.</span></span>
3. <span data-ttu-id="25b19-219">Rejestrowanie schemat adresu URL.</span><span class="sxs-lookup"><span data-stu-id="25b19-219">Registering a URL Scheme.</span></span>
4. <span data-ttu-id="25b19-220">Obsługa iOS9: Dodaj uprawnienia do pliku info.plist.</span><span class="sxs-lookup"><span data-stu-id="25b19-220">iOS9 Support: Add a permission to your info.plist file.</span></span>

#### <a name="step-1-enable-broker-mode-in-your-application"></a><span data-ttu-id="25b19-221">Krok 1: Włącz broker tryb w aplikacji</span><span class="sxs-lookup"><span data-stu-id="25b19-221">Step 1: Enable broker mode in your application</span></span>
<span data-ttu-id="25b19-222">Możliwość aplikacji pod kątem wykorzystania brokera jest włączona, podczas tworzenia "context" lub początkowej konfiguracji obiektu uwierzytelniania.</span><span class="sxs-lookup"><span data-stu-id="25b19-222">The ability for your application to use the broker is turned on when you create the "context" or initial setup of your Authentication object.</span></span> <span data-ttu-id="25b19-223">Można to zrobić przez ustawienie danego typu poświadczeń w kodzie:</span><span class="sxs-lookup"><span data-stu-id="25b19-223">You do this by setting your credentials type in your code:</span></span>

```
/*! See the ADCredentialsType enumeration definition for details */
@propertyADCredentialsType credentialsType;
```
<span data-ttu-id="25b19-224">`AD_CREDENTIALS_AUTO` Ustawienie umożliwia SDK tożsamości firmy Microsoft w celu wyróżnienia do brokera, `AD_CREDENTIALS_EMBEDDED` uniemożliwi wywołania do brokera SDK tożsamość firmy Microsoft.</span><span class="sxs-lookup"><span data-stu-id="25b19-224">The `AD_CREDENTIALS_AUTO` setting will allow the Microsoft Identity SDK to try to call out to the broker, `AD_CREDENTIALS_EMBEDDED` will prevent the Microsoft Identity SDK from calling to the broker.</span></span>

#### <a name="step-2-registering-a-url-scheme"></a><span data-ttu-id="25b19-225">Krok 2: Zarejestrowanie schemat adresu URL</span><span class="sxs-lookup"><span data-stu-id="25b19-225">Step 2: Registering a URL Scheme</span></span>
<span data-ttu-id="25b19-226">Platformy pakietu Microsoft Identity używa adresów URL wywołania brokera, a następnie wróć formantu do aplikacji.</span><span class="sxs-lookup"><span data-stu-id="25b19-226">The Microsoft Identity platform uses URLs to invoke the broker and then return control back to your application.</span></span> <span data-ttu-id="25b19-227">Do zakończenia tego obiegu należy zarejestrowane dla aplikacji platformy Microsoft Identity będzie wiedzieć o schemat adresów URL.</span><span class="sxs-lookup"><span data-stu-id="25b19-227">To finish that round trip you need a URL scheme registered for your application that the Microsoft Identity platform will know about.</span></span> <span data-ttu-id="25b19-228">Może to być oprócz innych systemów aplikacji, które może zostały wcześniej zarejestrowane z aplikacją.</span><span class="sxs-lookup"><span data-stu-id="25b19-228">This can be in addition to any other app schemes you may have previously registered with your application.</span></span>

> [!WARNING]
> <span data-ttu-id="25b19-229">Zalecamy utworzenie dość unikatowy, aby zminimalizować prawdopodobieństwo innej aplikacji przy użyciu tego samego schematu URL schemat adresu URL.</span><span class="sxs-lookup"><span data-stu-id="25b19-229">We recommend making the URL scheme fairly unique to minimize the chances of another app using the same URL scheme.</span></span> <span data-ttu-id="25b19-230">Apple nie wymusza unikatowości Schematy adresów URL, które są zarejestrowane w sklepie z aplikacjami.</span><span class="sxs-lookup"><span data-stu-id="25b19-230">Apple does not enforce the uniqueness of URL schemes that are registered in the app store.</span></span>
> 
> 

<span data-ttu-id="25b19-231">Poniżej przedstawiono przykład sposobu wyświetlania w konfiguracji projektu.</span><span class="sxs-lookup"><span data-stu-id="25b19-231">Below is an example of how this appears in your project configuration.</span></span> <span data-ttu-id="25b19-232">Można również wykonać to w środowisku XCode również:</span><span class="sxs-lookup"><span data-stu-id="25b19-232">You may also do this in XCode as well:</span></span>

```
<key>CFBundleURLTypes</key>
<array>
    <dict>
        <key>CFBundleTypeRole</key>
        <string>Editor</string>
        <key>CFBundleURLName</key>
        <string>com.myapp.mytestapp</string>
        <key>CFBundleURLSchemes</key>
        <array>
            <string>x-msauth-mytestiosapp</string>
        </array>
    </dict>
</array>
```

#### <a name="step-3-establish-a-new-redirect-uri-with-your-url-scheme"></a><span data-ttu-id="25b19-233">Krok 3: Ustalanie przekierowania nowy identyfikator URI ze schematem adresu URL</span><span class="sxs-lookup"><span data-stu-id="25b19-233">Step 3: Establish a new redirect URI with your URL Scheme</span></span>
<span data-ttu-id="25b19-234">Aby zapewnić, że firma Microsoft zawsze zwracają tokeny poświadczeń do właściwej aplikacji, musimy upewnij się, że firma Microsoft wywołania zwrotnego dla aplikacji w taki sposób, aby sprawdzić systemu operacyjnego z systemem iOS.</span><span class="sxs-lookup"><span data-stu-id="25b19-234">In order to ensure that we always return the credential tokens to the correct application, we need to make sure we call back to your application in a way that the iOS operating system can verify.</span></span> <span data-ttu-id="25b19-235">System operacyjny iOS raportów do aplikacji firmy Microsoft brokera identyfikator pakietu aplikacji podczas wywoływania go.</span><span class="sxs-lookup"><span data-stu-id="25b19-235">The iOS operating system reports to the Microsoft broker applications the Bundle ID of the application calling it.</span></span> <span data-ttu-id="25b19-236">To nie może być sfałszowane przez nieautoryzowanej aplikacji.</span><span class="sxs-lookup"><span data-stu-id="25b19-236">This cannot be spoofed by a rogue application.</span></span> <span data-ttu-id="25b19-237">W związku z tym możemy wykorzystać to wraz z identyfikatora URI z naszej aplikacji brokera, aby upewnić się, że tokeny są zwracane do odpowiedniej aplikacji.</span><span class="sxs-lookup"><span data-stu-id="25b19-237">Therefore, we leverage this along with the URI of our broker application to ensure that the tokens are returned to the correct application.</span></span> <span data-ttu-id="25b19-238">Wymagane do nawiązania przekierowanie Unikatowy identyfikator URI zarówno w aplikacji i Ustaw jako identyfikator URI przekierowania w portalu deweloperów.</span><span class="sxs-lookup"><span data-stu-id="25b19-238">We require you to establish this unique redirect URI both in your application and set as a Redirect URI in our developer portal.</span></span>

<span data-ttu-id="25b19-239">Identyfikator URI przekierowania musi być w postaci prawidłowego:</span><span class="sxs-lookup"><span data-stu-id="25b19-239">Your redirect URI must be in the proper form of:</span></span>

`<app-scheme>://<your.bundle.id>`

<span data-ttu-id="25b19-240">przykład: *x-msauth-mytestiosapp://com.myapp.mytestapp*</span><span class="sxs-lookup"><span data-stu-id="25b19-240">ex: *x-msauth-mytestiosapp://com.myapp.mytestapp*</span></span>

<span data-ttu-id="25b19-241">Ten identyfikator URI przekierowania trzeba określić za pomocą rejestracji aplikacji [portalu Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="25b19-241">This Redirect URI needs to be specified in your app registration using the [Azure portal](https://portal.azure.com/).</span></span> <span data-ttu-id="25b19-242">Aby uzyskać więcej informacji dotyczących rejestracji aplikacji usługi Azure AD, zobacz [integracji z usługą Azure Active Directory](active-directory-how-to-integrate.md).</span><span class="sxs-lookup"><span data-stu-id="25b19-242">For more information on Azure AD app registration, see [Integrating with Azure Active Directory](active-directory-how-to-integrate.md).</span></span>

##### <a name="step-3a-add-a-redirect-uri-in-your-app-and-dev-portal-to-support-certificate-based-authentication"></a><span data-ttu-id="25b19-243">Krok 3a: Dodaj identyfikator URI przekierowania w portalu i deweloperów aplikacji do obsługi uwierzytelniania opartego na certyfikatach</span><span class="sxs-lookup"><span data-stu-id="25b19-243">Step 3a: Add a redirect URI in your app and dev portal to support certificate based authentication</span></span>
<span data-ttu-id="25b19-244">Obsługa uwierzytelniania certyfikatu na podstawie drugi "msauth" musi zostać zarejestrowany w aplikacji i [portalu Azure](https://portal.azure.com/) do obsługi uwierzytelniania certyfikatów, jeśli chcesz dodać obsługę w aplikacji.</span><span class="sxs-lookup"><span data-stu-id="25b19-244">To support cert based authentication a second "msauth"  needs to be registered in your application and the [Azure portal](https://portal.azure.com/) to handle certificate authentication if you wish to add that support in your application.</span></span>

`msauth://code/<broker-redirect-uri-in-url-encoded-form>`

<span data-ttu-id="25b19-245">przykład: *msauth://code/x-msauth-mytestiosapp%3A%2F%2Fcom.myapp.mytestapp*</span><span class="sxs-lookup"><span data-stu-id="25b19-245">ex: *msauth://code/x-msauth-mytestiosapp%3A%2F%2Fcom.myapp.mytestapp*</span></span>

#### <a name="step-4-ios9-add-a-configuration-parameter-to-your-app"></a><span data-ttu-id="25b19-246">Krok 4: iOS9: Dodawanie parametru konfiguracji do aplikacji</span><span class="sxs-lookup"><span data-stu-id="25b19-246">Step 4: iOS9: Add a configuration parameter to your app</span></span>
<span data-ttu-id="25b19-247">— CanOpenURL używa biblioteki ADAL: Aby sprawdzić, czy broker jest zainstalowane na urządzeniu.</span><span class="sxs-lookup"><span data-stu-id="25b19-247">ADAL uses –canOpenURL: to check if the broker is installed on the device.</span></span> <span data-ttu-id="25b19-248">W systemie iOS 9 Apple zablokowany co można wyszukać schematy aplikacji.</span><span class="sxs-lookup"><span data-stu-id="25b19-248">In iOS 9 Apple locked down what schemes an application can query for.</span></span> <span data-ttu-id="25b19-249">Należy dodać do sekcji LSApplicationQueriesSchemes "msauth" z `info.plist file`.</span><span class="sxs-lookup"><span data-stu-id="25b19-249">You will need to add “msauth” to the LSApplicationQueriesSchemes section of your `info.plist file`.</span></span>

<span data-ttu-id="25b19-250"><key>LSApplicationQueriesSchemes</key></span><span class="sxs-lookup"><span data-stu-id="25b19-250"><key>LSApplicationQueriesSchemes</key></span></span>

<span data-ttu-id="25b19-251"><array><string>msauth</string>
</array></span><span class="sxs-lookup"><span data-stu-id="25b19-251"><array> <string>msauth</string>
</array></span></span>

### <a name="youve-configured-sso"></a><span data-ttu-id="25b19-252">Skonfigurowaniu logowania jednokrotnego!</span><span class="sxs-lookup"><span data-stu-id="25b19-252">You've configured SSO!</span></span>
<span data-ttu-id="25b19-253">Teraz Microsoft tożsamość SDK automatycznie zarówno udostępnianie poświadczeń w aplikacji i wywołać brokera, jeśli jest obecny na urządzeniu.</span><span class="sxs-lookup"><span data-stu-id="25b19-253">Now the Microsoft Identity SDK will automatically both share credentials across your applications and invoke the broker if it's present on their device.</span></span>

