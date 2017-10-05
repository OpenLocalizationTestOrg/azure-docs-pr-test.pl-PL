---
title: "Jak włączyć logowanie Jednokrotne wielu aplikacji w systemie Android przy użyciu biblioteki ADAL | Dokumentacja firmy Microsoft"
description: "Jak używać funkcji ADAL zestawu SDK do Włącz rejestrację jednokrotną w aplikacji. "
services: active-directory
documentationcenter: 
author: danieldobalian
manager: mbaldwin
editor: 
ms.assetid: 40710225-05ab-40a3-9aec-8b4e96b6b5e7
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: android
ms.devlang: java
ms.topic: article
ms.date: 04/07/2017
ms.author: dadobali
ms.custom: aaddev
ms.openlocfilehash: 9c7e959530a836fe5ddf74708363a636c39b3cc6
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-enable-cross-app-sso-on-android-using-adal"></a><span data-ttu-id="f0ea9-103">Jak włączyć logowanie Jednokrotne wielu aplikacji w systemie Android przy użyciu biblioteki ADAL</span><span class="sxs-lookup"><span data-stu-id="f0ea9-103">How to enable cross-app SSO on Android using ADAL</span></span>
<span data-ttu-id="f0ea9-104">Zapewniające pojedynczego logowania jednokrotnego (SSO), aby użytkownicy potrzebują tylko może wprowadzić swoje poświadczenia raz, a te poświadczenia automatycznie działać przez aplikacje teraz jest oczekiwany przez klientów.</span><span class="sxs-lookup"><span data-stu-id="f0ea9-104">Providing Single Sign-On (SSO) so that users only need to enter their credentials once and have those credentials automatically work across applications is now expected by customers.</span></span> <span data-ttu-id="f0ea9-105">Trudności przy wprowadzaniu swoją nazwę użytkownika i hasło na małego ekranu, często razy łączyć się przy użyciu dodatkowego składnika (2FA), takich jak rozmowa telefoniczna lub kod wysłana wiadomość SMS, powoduje niezadowolenie szybki, jeśli użytkownik ma w tym celu więcej niż jeden raz na produkt.</span><span class="sxs-lookup"><span data-stu-id="f0ea9-105">The difficulty in entering their username and password on a small screen, often times combined with an additional factor (2FA) like a phone call or a texted code, results in quick dissatisfaction if a user has to do this more than one time for your product.</span></span>

<span data-ttu-id="f0ea9-106">Ponadto w przypadku zastosowania platformą tożsamości, które inne aplikacje mogą używać takich jak Accounts Microsoft lub konta służbowego z usługi Office 365, klienci oczekują, że te poświadczenia były dostępne do użycia w swoich aplikacjach niezależnie od dostawcy.</span><span class="sxs-lookup"><span data-stu-id="f0ea9-106">In addition, if you apply an identity platform that other applications may use such as Microsoft Accounts or a work account from Office365, customers expect that those credentials to be available to use across all their applications no matter the vendor.</span></span>

<span data-ttu-id="f0ea9-107">Platformy pakietu Microsoft Identity, wraz z nasze zestawy SDK tożsamości Microsoft robi to twarde pracy i daje możliwość doskonale dopasowanych swoich klientów za pomocą rejestracji Jednokrotnej w pakietu aplikacji lub, w przypadku naszego brokera możliwości i wystawcy uwierzytelnienia aplikacji, we wszystkich danych z urządzenia.</span><span class="sxs-lookup"><span data-stu-id="f0ea9-107">The Microsoft Identity platform, along with our Microsoft Identity SDKs, does all this hard work for you and gives you the ability to delight your customers with SSO either within your own suite of applications or, as with our broker capability and Authenticator applications, across the entire device.</span></span>

<span data-ttu-id="f0ea9-108">W tym przewodniku opisano, jak skonfigurować naszego zestawu SDK w celu zapewnienia takich korzyści klientom aplikacji.</span><span class="sxs-lookup"><span data-stu-id="f0ea9-108">This walkthrough will tell you how to configure our SDK within your application to provide this benefit to your customers.</span></span>

<span data-ttu-id="f0ea9-109">Ten przewodnik dotyczy:</span><span class="sxs-lookup"><span data-stu-id="f0ea9-109">This walkthrough applies to:</span></span>

* <span data-ttu-id="f0ea9-110">Usługa Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="f0ea9-110">Azure Active Directory</span></span>
* <span data-ttu-id="f0ea9-111">Azure Active Directory B2C</span><span class="sxs-lookup"><span data-stu-id="f0ea9-111">Azure Active Directory B2C</span></span>
* <span data-ttu-id="f0ea9-112">B2B usługi Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="f0ea9-112">Azure Active Directory B2B</span></span>
* <span data-ttu-id="f0ea9-113">Dostęp warunkowy usługi Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="f0ea9-113">Azure Active Directory Conditional Access</span></span>

<span data-ttu-id="f0ea9-114">Poprzedniego dokumentu zakłada wiesz, jak [udostępnić aplikacje w starszej wersji portalu usługi Azure Active Directory](active-directory-how-to-integrate.md) i zintegrowanych aplikacji z [zestawu SDK systemu Android tożsamości Microsoft](https://github.com/AzureAD/azure-activedirectory-library-for-android).</span><span class="sxs-lookup"><span data-stu-id="f0ea9-114">The document preceding assumes you know how to [provision applications in the legacy portal for Azure Active Directory](active-directory-how-to-integrate.md) and integrated your application with the [Microsoft Identity Android SDK](https://github.com/AzureAD/azure-activedirectory-library-for-android).</span></span>

## <a name="sso-concepts-in-the-microsoft-identity-platform"></a><span data-ttu-id="f0ea9-115">Pojęcia dotyczące logowania jednokrotnego platformą tożsamości Microsoft</span><span class="sxs-lookup"><span data-stu-id="f0ea9-115">SSO Concepts in the Microsoft Identity Platform</span></span>
### <a name="microsoft-identity-brokers"></a><span data-ttu-id="f0ea9-116">Brokerzy tożsamość firmy Microsoft</span><span class="sxs-lookup"><span data-stu-id="f0ea9-116">Microsoft Identity Brokers</span></span>
<span data-ttu-id="f0ea9-117">Firma Microsoft udostępnia aplikacji dla każdej platformy przenośne, które umożliwiają łączenie poświadczeń w aplikacjach pochodzących od różnych dostawców i umożliwia specjalne udoskonalone funkcje, które wymagają pojedynczego bezpiecznym miejscu z, w którym można sprawdzić poprawności poświadczeń.</span><span class="sxs-lookup"><span data-stu-id="f0ea9-117">Microsoft provides applications for every mobile platform that allow for the bridging of credentials across applications from different vendors and allows for special enhanced features that require a single secure place from where to validate credentials.</span></span> <span data-ttu-id="f0ea9-118">Nazywamy je **brokerzy**.</span><span class="sxs-lookup"><span data-stu-id="f0ea9-118">We call these **brokers**.</span></span> <span data-ttu-id="f0ea9-119">W systemach iOS i Android te są realizowane za pośrednictwem aplikacji do pobrania czy klientów zainstalować niezależnie lub może zostać umieszczony na urządzeniu przez użytkowników, którzy zarządzają niektórych lub wszystkich urządzeń dla swoich pracowników firmy.</span><span class="sxs-lookup"><span data-stu-id="f0ea9-119">On iOS and Android these are provided through downloadable applications that customers either install independently or can be pushed to the device by a company who manages some or all of the device for their employee.</span></span> <span data-ttu-id="f0ea9-120">Te brokerzy obsługę zarządzania zabezpieczeń tylko niektóre aplikacje lub wszystkich danych z urządzenia oparte na potrzeby administratorzy IT.</span><span class="sxs-lookup"><span data-stu-id="f0ea9-120">These brokers support managing security just for some applications or the entire device based on what IT Administrators desire.</span></span> <span data-ttu-id="f0ea9-121">W systemie Windows ta funkcja jest dostarczana przez selektora konta z wbudowanej w system operacyjny, znane pod względem technicznym jako Broker uwierzytelniania sieci Web.</span><span class="sxs-lookup"><span data-stu-id="f0ea9-121">In Windows, this functionality is provided by an account chooser built in to the operating system, known technically as the Web Authentication Broker.</span></span>

<span data-ttu-id="f0ea9-122">Aby uzyskać więcej informacji na temat używamy tych brokerów i jak klienci mogą je wyświetlać w ich przepływu logowania na platformy pakietu Microsoft Identity.</span><span class="sxs-lookup"><span data-stu-id="f0ea9-122">For more information on how we use these brokers and how your customers might see them in their login flow for the Microsoft Identity platform read on.</span></span>

### <a name="patterns-for-logging-in-on-mobile-devices"></a><span data-ttu-id="f0ea9-123">Wzorce do logowania na urządzeniach przenośnych</span><span class="sxs-lookup"><span data-stu-id="f0ea9-123">Patterns for logging in on mobile devices</span></span>
<span data-ttu-id="f0ea9-124">Dostęp do poświadczeń na urządzeniach wykonaj dwa podstawowe wzorce platformy pakietu Microsoft Identity:</span><span class="sxs-lookup"><span data-stu-id="f0ea9-124">Access to credentials on devices follow two basic patterns for the Microsoft Identity platform:</span></span>

* <span data-ttu-id="f0ea9-125">Logowania asystowaną bez brokera</span><span class="sxs-lookup"><span data-stu-id="f0ea9-125">Non-broker assisted logins</span></span>
* <span data-ttu-id="f0ea9-126">Broker asystowaną logowania</span><span class="sxs-lookup"><span data-stu-id="f0ea9-126">Broker assisted logins</span></span>

#### <a name="non-broker-assisted-logins"></a><span data-ttu-id="f0ea9-127">Logowania asystowaną bez brokera</span><span class="sxs-lookup"><span data-stu-id="f0ea9-127">Non-broker assisted logins</span></span>
<span data-ttu-id="f0ea9-128">Inne niż brokera asystowaną logowania są środowiska logowania, być wbudowane w aplikacji, które obsługują Magazyn lokalny na urządzeniu dla tej aplikacji.</span><span class="sxs-lookup"><span data-stu-id="f0ea9-128">Non-broker assisted logins are login experiences that happen inline with the application and use the local storage on the device for that application.</span></span> <span data-ttu-id="f0ea9-129">Ten magazyn może być współużytkowany przez aplikacje, ale poświadczenia są ściśle powiązane z aplikacji lub pakietu aplikacji przy użyciu tego poświadczenia.</span><span class="sxs-lookup"><span data-stu-id="f0ea9-129">This storage may be shared across applications but the credentials are tightly bound to the app or suite of apps using that credential.</span></span> <span data-ttu-id="f0ea9-130">W przypadku najprawdopodobniej wystąpienia to w wielu aplikacjach mobilnych podczas wprowadzania nazwy użytkownika i hasła samej aplikacji.</span><span class="sxs-lookup"><span data-stu-id="f0ea9-130">You've most likely experienced this in many mobile applications when you enter a username and password within the application itself.</span></span>

<span data-ttu-id="f0ea9-131">Te nazwy logowania są następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="f0ea9-131">These logins have the following benefits:</span></span>

* <span data-ttu-id="f0ea9-132">Środowisko użytkownika istnieje całkowicie w aplikacji.</span><span class="sxs-lookup"><span data-stu-id="f0ea9-132">User experience exists entirely within the application.</span></span>
* <span data-ttu-id="f0ea9-133">Poświadczenia mogą być udostępniane między aplikacjami, które są podpisane przez ten sam certyfikat, zapewniając pojedynczego środowisko logowania do pakietu aplikacji.</span><span class="sxs-lookup"><span data-stu-id="f0ea9-133">Credentials can be shared across applications that are signed by the same certificate, providing a single sign-on experience to your suite of applications.</span></span>
* <span data-ttu-id="f0ea9-134">Formant wokół środowisko logowania jest dostarczany do aplikacji przed i po zalogowaniu.</span><span class="sxs-lookup"><span data-stu-id="f0ea9-134">Control around the experience of logging in is provided to the application before and after sign-in.</span></span>

<span data-ttu-id="f0ea9-135">Te nazwy logowania ma następujące wady:</span><span class="sxs-lookup"><span data-stu-id="f0ea9-135">These logins have the following drawbacks:</span></span>

* <span data-ttu-id="f0ea9-136">Użytkownika nie może występować jednokrotnego we wszystkich aplikacji, które używają pakietu Microsoft Identity przez te firmy Microsoft Identities skonfigurowane w aplikacji.</span><span class="sxs-lookup"><span data-stu-id="f0ea9-136">User cannot experience single-sign on across all apps that use a Microsoft Identity, only across those Microsoft Identities that your application has configured.</span></span>
* <span data-ttu-id="f0ea9-137">Aplikacji nie można używać z bardziej zaawansowane funkcje biznesowych, takich jak dostęp warunkowy, lub użyj produktów pakietu usługi InTune.</span><span class="sxs-lookup"><span data-stu-id="f0ea9-137">Your application cannot be used with more advanced business features such as Conditional Access or use the InTune suite of products.</span></span>
* <span data-ttu-id="f0ea9-138">Używana aplikacja nie obsługuje uwierzytelniania opartego na certyfikatach dla użytkowników biznesowych.</span><span class="sxs-lookup"><span data-stu-id="f0ea9-138">Your application can't support certificate-based authentication for business users.</span></span>

<span data-ttu-id="f0ea9-139">Oto reprezentację działanie zestawów SDK tożsamość firmy Microsoft z magazynem udostępnionym aplikacji do włączenia funkcji logowania jednokrotnego:</span><span class="sxs-lookup"><span data-stu-id="f0ea9-139">Here is a representation of how the Microsoft Identity SDKs work with the shared storage of your applications to enable SSO:</span></span>

```
+------------+ +------------+  +-------------+
|            | |            |  |             |
|   App 1    | |   App 2    |  |   App 3     |
|            | |            |  |             |
|            | |            |  |             |
+------------+ +------------+  +-------------+
| Azure SDK  | | Azure SDK  |  | Azure SDK   |
+------------+-+------------+--+-------------+
|                                            |
|            App Shared Storage              |
+--------------------------------------------+
```

#### <a name="broker-assisted-logins"></a><span data-ttu-id="f0ea9-140">Broker asystowaną logowania</span><span class="sxs-lookup"><span data-stu-id="f0ea9-140">Broker assisted logins</span></span>
<span data-ttu-id="f0ea9-141">Asystowane brokera logowania są funkcji logowania, które występują w aplikacji brokera i korzystania z magazynu i zabezpieczeń brokera udostępnianie poświadczeń we wszystkich aplikacjach na urządzeniu, mające zastosowanie platformy pakietu Microsoft Identity.</span><span class="sxs-lookup"><span data-stu-id="f0ea9-141">Broker-assisted logins are login experiences that occur within the broker application and use the storage and security of the broker to share credentials across all applications on the device that apply the Microsoft Identity platform.</span></span> <span data-ttu-id="f0ea9-142">Oznacza to, że aplikacje zależne od brokera do logowania użytkowników.</span><span class="sxs-lookup"><span data-stu-id="f0ea9-142">This means that your applications rely on the broker to sign users in.</span></span> <span data-ttu-id="f0ea9-143">W systemach iOS i Android brokerzy te są realizowane za pośrednictwem aplikacji do pobrania, czy klientów zainstalować niezależnie lub może zostać umieszczony na urządzeniu przez firmę, użytkowników, którzy zarządzają urządzenia dla ich użytkownika.</span><span class="sxs-lookup"><span data-stu-id="f0ea9-143">On iOS and Android these brokers are provided through downloadable applications that customers either install independently or can be pushed to the device by a company who manages the device for their user.</span></span> <span data-ttu-id="f0ea9-144">Przykładowe aplikacje tego typu jest aplikacja Microsoft Authenticator w systemie iOS.</span><span class="sxs-lookup"><span data-stu-id="f0ea9-144">An example of this type of application is the Microsoft Authenticator application on iOS.</span></span> <span data-ttu-id="f0ea9-145">W systemie Windows ta funkcja jest dostarczana przez selektora konta z wbudowanej w system operacyjny, znane pod względem technicznym jako Broker uwierzytelniania sieci Web.</span><span class="sxs-lookup"><span data-stu-id="f0ea9-145">In Windows this functionality is provided by an account chooser built in to the operating system, known technically as the Web Authentication Broker.</span></span>
<span data-ttu-id="f0ea9-146">Środowisko jest zależna od platformy i czasami mogą być uciążliwe dla użytkowników w przeciwnym razie zarządzane prawidłowo.</span><span class="sxs-lookup"><span data-stu-id="f0ea9-146">The experience varies by platform and can sometimes be disruptive to users if not managed correctly.</span></span> <span data-ttu-id="f0ea9-147">Znasz prawdopodobnie najbardziej tego wzorca Jeśli z zainstalowaną aplikacją Facebook i używać funkcji usługi Facebook połączenie z innej aplikacji.</span><span class="sxs-lookup"><span data-stu-id="f0ea9-147">You're probably most familiar with this pattern if you have the Facebook application installed and use Facebook Connect from another application.</span></span> <span data-ttu-id="f0ea9-148">Platforma Microsoft Identity używa tego samego wzorca.</span><span class="sxs-lookup"><span data-stu-id="f0ea9-148">The Microsoft Identity platform uses the same pattern.</span></span>

<span data-ttu-id="f0ea9-149">Dla systemu iOS, który prowadzi to do "przejścia" animacji, w którym aplikacji są wysyłane do tła podczas aplikacji Microsoft Authenticator zawiera pierwszego planu dla użytkownika wybrać konto, które chce się zalogować.</span><span class="sxs-lookup"><span data-stu-id="f0ea9-149">For iOS this leads to a "transition" animation where your application is sent to the background while the Microsoft Authenticator applications comes to the foreground for the user to select which account they would like to sign in with.</span></span>  

<span data-ttu-id="f0ea9-150">Dla systemów Android i Windows selektora konta jest wyświetlany u góry aplikację, która jest prostszy sposób użytkownika.</span><span class="sxs-lookup"><span data-stu-id="f0ea9-150">For Android and Windows the account chooser is displayed on top of your application which is less disruptive to the user.</span></span>

#### <a name="how-the-broker-gets-invoked"></a><span data-ttu-id="f0ea9-151">Sposób wywoływania pobiera brokera</span><span class="sxs-lookup"><span data-stu-id="f0ea9-151">How the broker gets invoked</span></span>
<span data-ttu-id="f0ea9-152">Zgodne brokera jest zainstalowany na urządzeniu, takie jak aplikacja Microsoft Authenticator zestawów SDK tożsamości Microsoft będzie automatycznie wykonywać pracy wywoływania brokera automatycznie, gdy użytkownik wskazuje chcą zalogowanie się przy użyciu dowolnego konta z platformy Microsoft Identity.</span><span class="sxs-lookup"><span data-stu-id="f0ea9-152">If a compatible broker is installed on the device, like the Microsoft Authenticator application, the Microsoft Identity SDKs will automatically do the work of invoking the broker for you when a user indicates they wish to log in using any account from the Microsoft Identity platform.</span></span> <span data-ttu-id="f0ea9-153">To konto może być Account firmy Microsoft, służbowy lub konta służbowego lub konta, które należy podać i hosta na platformie Azure przy użyciu naszych produktów B2C i B2B.</span><span class="sxs-lookup"><span data-stu-id="f0ea9-153">This account could be a personal Microsoft Account, a work or school account, or an account that you provide and host in Azure using our B2C and B2B products.</span></span> 
 
 #### <a name="how-we-ensure-the-application-is-valid"></a><span data-ttu-id="f0ea9-154">Jak firma Microsoft zapewnia aplikacji jest prawidłowy</span><span class="sxs-lookup"><span data-stu-id="f0ea9-154">How we ensure the application is valid</span></span>
 
 <span data-ttu-id="f0ea9-155">Konieczność zapewnienia tożsamości wywołanie aplikacji, które brokera odgrywa kluczową rolę zabezpieczeń, które udostępniamy w brokerze pomocy logowania.</span><span class="sxs-lookup"><span data-stu-id="f0ea9-155">The need to ensure the identity of an application call the broker is crucial to the security we provide in broker assisted logins.</span></span> <span data-ttu-id="f0ea9-156">Z systemem iOS ani Android wymusza unikatowych identyfikatorów, które są prawidłowe tylko dla danej aplikacji, więc złośliwego aplikacji może "sfałszować" identyfikator uzasadnionych aplikacji i odbierać tokeny przeznaczone dla aplikacji uzasadnione.</span><span class="sxs-lookup"><span data-stu-id="f0ea9-156">Neither iOS nor Android enforces unique identifiers that are valid only for a given application, so malicious applications may "spoof" a legitimate application's identifier and receive the tokens meant for the legitimate application.</span></span> <span data-ttu-id="f0ea9-157">Aby upewnić się, że zawsze komunikują się firma Microsoft z prawej aplikacji w czasie wykonywania, poprosimy developer do niestandardowych redirectURI podczas rejestrowania swoich aplikacji z firmą Microsoft.</span><span class="sxs-lookup"><span data-stu-id="f0ea9-157">To ensure we are always communicating with the right application at runtime, we ask the developer to provide a custom redirectURI when registering their application with Microsoft.</span></span> <span data-ttu-id="f0ea9-158">**Jak deweloperzy powinien spreparować identyfikator URI przekierowania omówiono szczegółowo poniżej.**</span><span class="sxs-lookup"><span data-stu-id="f0ea9-158">**How developers should craft this redirect URI is discussed in detail below.**</span></span> <span data-ttu-id="f0ea9-159">To niestandardowe redirectURI zawiera odcisk palca certyfikatu, aplikacji i zapewniony unikatowa do aplikacji w sklepie Google Play.</span><span class="sxs-lookup"><span data-stu-id="f0ea9-159">This custom redirectURI contains the certificate thumbprint of the application and is ensured to be unique to the application by the Google Play Store.</span></span> <span data-ttu-id="f0ea9-160">Gdy aplikacja wywołuje brokera, broker zapyta, systemu operacyjnego Android zapewnienie o odcisk palca certyfikatu, który wywołał brokera.</span><span class="sxs-lookup"><span data-stu-id="f0ea9-160">When an application calls the broker, the broker asks the Android operating system to provide it with the certificate thumbprint that called the broker.</span></span> <span data-ttu-id="f0ea9-161">Broker taki odcisk palca certyfikatu do firmy Microsoft w wywołaniu naszym systemie tożsamości.</span><span class="sxs-lookup"><span data-stu-id="f0ea9-161">The broker provides this certificate thumbprint to Microsoft in the call to our identity system.</span></span> <span data-ttu-id="f0ea9-162">Jeśli odcisk palca certyfikatu aplikacji nie odpowiada odcisk palca certyfikatu przekazanego nam przez projektanta podczas rejestracji, firma Microsoft będzie odmawiał dostępu na tokeny dla zasobu, który żąda aplikacji.</span><span class="sxs-lookup"><span data-stu-id="f0ea9-162">If the certificate thumbprint of the application does not match the certificate thumbprint provided to us by the developer during registration, we will deny access to the tokens for the resource the application is requesting.</span></span> <span data-ttu-id="f0ea9-163">Tego wyboru gwarantuje, że tylko aplikacja zarejestrowany przez dewelopera otrzyma tokenów.</span><span class="sxs-lookup"><span data-stu-id="f0ea9-163">This check ensures that only the application registered by the developer receives tokens.</span></span>

<span data-ttu-id="f0ea9-164">**Deweloper może wybrać opcję Microsoft tożsamość SDK wywołuje brokera lub korzysta z przepływu asystowaną bez brokera.**</span><span class="sxs-lookup"><span data-stu-id="f0ea9-164">**The developer has the choice of if the Microsoft Identity SDK calls the broker or uses the non-broker assisted flow.**</span></span> <span data-ttu-id="f0ea9-165">Jednak jeśli wybierze projektanta nie należy używać przepływu wspierana brokera utracą zaletą używania poświadczeń logowania jednokrotnego, czy użytkownik może już dodane na urządzeniu i uniemożliwia ich aplikacji z używane z funkcjami firm, które firma Microsoft udostępnia jej klientów, takie jak dostęp warunkowy, możliwości zarządzania usługi Intune i uwierzytelnianie oparte na certyfikatach.</span><span class="sxs-lookup"><span data-stu-id="f0ea9-165">However if the developer chooses not to use the broker-assisted flow they lose the benefit of using SSO credentials that the user may have already added on the device and prevents their application from being used with business features Microsoft provides its customers such as Conditional Access, Intune Management capabilities, and certificate-based authentication.</span></span>

<span data-ttu-id="f0ea9-166">Te nazwy logowania są następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="f0ea9-166">These logins have the following benefits:</span></span>

* <span data-ttu-id="f0ea9-167">Użytkownik napotyka logowania jednokrotnego w swoich aplikacjach niezależnie od dostawcy.</span><span class="sxs-lookup"><span data-stu-id="f0ea9-167">User experiences SSO across all their applications no matter the vendor.</span></span>
* <span data-ttu-id="f0ea9-168">Aplikacja może użyć bardziej zaawansowane funkcje biznesowych, takich jak dostęp warunkowy lub produktów pakietu usługi InTune.</span><span class="sxs-lookup"><span data-stu-id="f0ea9-168">Your application can use more advanced business features such as Conditional Access or use the InTune suite of products.</span></span>
* <span data-ttu-id="f0ea9-169">Aplikacja może obsługiwać uwierzytelnianie oparte na certyfikatach dla użytkowników biznesowych.</span><span class="sxs-lookup"><span data-stu-id="f0ea9-169">Your application can support certificate-based authentication for business users.</span></span>
* <span data-ttu-id="f0ea9-170">Bezpieczniejszym logowania jako tożsamość aplikacji i użytkownika są weryfikowane przez aplikację broker z algorytmów zabezpieczeń i szyfrowania.</span><span class="sxs-lookup"><span data-stu-id="f0ea9-170">Much more secure sign-in experience as the identity of the application and the user are verified by the broker application with additional security algorithms and encryption.</span></span>

<span data-ttu-id="f0ea9-171">Te nazwy logowania ma następujące wady:</span><span class="sxs-lookup"><span data-stu-id="f0ea9-171">These logins have the following drawbacks:</span></span>

* <span data-ttu-id="f0ea9-172">W systemie iOS użytkownika jest są przenoszone poza środowisko aplikacji, a poświadczenia zostały wybrane.</span><span class="sxs-lookup"><span data-stu-id="f0ea9-172">In iOS the user is transitioned out of your application's experience while credentials are chosen.</span></span>
* <span data-ttu-id="f0ea9-173">Utrata możliwości zarządzania mogą logować się klienci w aplikacji.</span><span class="sxs-lookup"><span data-stu-id="f0ea9-173">Loss of the ability to manage the login experience for your customers within your application.</span></span>

<span data-ttu-id="f0ea9-174">Oto reprezentację działanie zestawów SDK tożsamość firmy Microsoft z aplikacji brokera do włączenia funkcji logowania jednokrotnego:</span><span class="sxs-lookup"><span data-stu-id="f0ea9-174">Here is a representation of how the Microsoft Identity SDKs work with the broker applications to enable SSO:</span></span>

```
+------------+ +------------+   +-------------+
|            | |            |   |             |
|   App 1    | |   App 2    |   |   Someone   |
|            | |            |   |    Else's   |
|            | |            |   |     App     |
+------------+ +------------+   +-------------+
|  ADAL SDK  | |  ADAL SDK  |   |  ADAL SDK   |
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

<span data-ttu-id="f0ea9-175">Dzięki tej ogólne informacje, które powinno być możliwe do lepszego zrozumienia i implementowanie logowania jednokrotnego w aplikacji przy użyciu pakietu Microsoft Identity platformy i zestawy SDK.</span><span class="sxs-lookup"><span data-stu-id="f0ea9-175">Armed with this background information you should be able to better understand and implement SSO within your application using the Microsoft Identity platform and SDKs.</span></span>

## <a name="enabling-cross-app-sso-using-adal"></a><span data-ttu-id="f0ea9-176">Włączanie logowania jednokrotnego wielu aplikacji za pomocą biblioteki ADAL</span><span class="sxs-lookup"><span data-stu-id="f0ea9-176">Enabling cross-app SSO using ADAL</span></span>
<span data-ttu-id="f0ea9-177">W tym miejscu używamy zestawu SDK systemu Android biblioteki ADAL do:</span><span class="sxs-lookup"><span data-stu-id="f0ea9-177">Here we use the ADAL Android SDK to:</span></span>

* <span data-ttu-id="f0ea9-178">Włącz brokera z systemem innym niż asystowaną pomocą rejestracji Jednokrotnej dla pakietu aplikacji</span><span class="sxs-lookup"><span data-stu-id="f0ea9-178">Turn on non-broker assisted SSO for your suite of apps</span></span>
* <span data-ttu-id="f0ea9-179">Włączanie obsługi wspierana brokera logowania jednokrotnego</span><span class="sxs-lookup"><span data-stu-id="f0ea9-179">Turn on support for broker-assisted SSO</span></span>

### <a name="turning-on-sso-for-non-broker-assisted-sso"></a><span data-ttu-id="f0ea9-180">Włączanie rejestracji Jednokrotnej z systemem innym niż brokera asystowaną pomocą rejestracji Jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="f0ea9-180">Turning on SSO for non-broker assisted SSO</span></span>
<span data-ttu-id="f0ea9-181">Dla bez brokera asystowaną logowania jednokrotnego w aplikacjach zestawów SDK tożsamości Microsoft zarządzać znacznie złożoność logowania jednokrotnego dla Ciebie.</span><span class="sxs-lookup"><span data-stu-id="f0ea9-181">For non-broker assisted SSO across applications the Microsoft Identity SDKs manage much of the complexity of SSO for you.</span></span> <span data-ttu-id="f0ea9-182">Obejmuje to wyszukiwanie prawo użytkownika w pamięci podręcznej i przechowywania listy zalogowany użytkowników możesz zbadać.</span><span class="sxs-lookup"><span data-stu-id="f0ea9-182">This includes finding the right user in the cache and maintaining a list of logged in users for you to query.</span></span>

<span data-ttu-id="f0ea9-183">Do włączenia funkcji logowania jednokrotnego w aplikacjach jesteś właścicielem, że należy wykonać następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="f0ea9-183">To enable SSO across applications you own you need to do the following:</span></span>

1. <span data-ttu-id="f0ea9-184">Upewnij się użytkownika aplikacje tego samego Identyfikatora klienta lub identyfikator aplikacji.</span><span class="sxs-lookup"><span data-stu-id="f0ea9-184">Ensure all your applications user the same Client ID or Application ID.</span></span>
2. <span data-ttu-id="f0ea9-185">Upewnij się, że wszystkie aplikacje mają ten sam zestaw SharedUserID.</span><span class="sxs-lookup"><span data-stu-id="f0ea9-185">Ensure all your applications have the same SharedUserID set.</span></span>
3. <span data-ttu-id="f0ea9-186">Upewnij się, dzięki czemu można udostępniać magazynu wszystkie aplikacje współużytkują ten sam certyfikat podpisywania z magazynu Google Play.</span><span class="sxs-lookup"><span data-stu-id="f0ea9-186">Ensure that all of your applications share the same signing certificate from the Google Play store so that you can share storage.</span></span>

#### <a name="step-1-using-the-same-client-id--application-id-for-all-the-applications-in-your-suite-of-apps"></a><span data-ttu-id="f0ea9-187">Krok 1: Używa tego samego Identyfikatora klienta / IDENTYFIKATORA aplikacji dla wszystkich aplikacji w pakietu aplikacji</span><span class="sxs-lookup"><span data-stu-id="f0ea9-187">Step 1: Using the same Client ID / Application ID for all the applications in your suite of apps</span></span>
<span data-ttu-id="f0ea9-188">Aby platformy pakietu Microsoft Identity dowiedzieć się, że mogą być udostępnianie tokenów w aplikacji należy poszczególnych aplikacji do udostępniania tego samego Identyfikatora klienta lub identyfikator aplikacji.</span><span class="sxs-lookup"><span data-stu-id="f0ea9-188">In order for the Microsoft Identity platform to know that it's allowed to share tokens across your applications, each of your applications will need to share the same Client ID or Application ID.</span></span> <span data-ttu-id="f0ea9-189">Jest to unikatowy identyfikator, który został udostępniony po zarejestrowaniu swoją pierwszą aplikację w portalu.</span><span class="sxs-lookup"><span data-stu-id="f0ea9-189">This is the unique identifier that was provided to you when you registered your first application in the portal.</span></span>

<span data-ttu-id="f0ea9-190">Możesz się zastanawiać, jak należy określić różnych aplikacji z usługą Microsoft Identity korzysta z tego samego identyfikatora aplikacji</span><span class="sxs-lookup"><span data-stu-id="f0ea9-190">You may be wondering how you will identify different apps to the Microsoft Identity service if it uses the same Application ID.</span></span> <span data-ttu-id="f0ea9-191">Odpowiedź jest z **identyfikator URI przekierowania**.</span><span class="sxs-lookup"><span data-stu-id="f0ea9-191">The answer is with the **Redirect URIs**.</span></span> <span data-ttu-id="f0ea9-192">Każda aplikacja może mieć wiele identyfikator URI przekierowania zarejestrowany w portalu przy dołączaniu.</span><span class="sxs-lookup"><span data-stu-id="f0ea9-192">Each application can have multiple Redirect URIs registered in the onboarding portal.</span></span> <span data-ttu-id="f0ea9-193">Każdej aplikacji w zestawie ma inny identyfikator URI przekierowania.</span><span class="sxs-lookup"><span data-stu-id="f0ea9-193">Each app in your suite will have a different redirect URI.</span></span> <span data-ttu-id="f0ea9-194">Jak wygląda przykład znajduje się poniżej:</span><span class="sxs-lookup"><span data-stu-id="f0ea9-194">An example of how this looks is below:</span></span>

<span data-ttu-id="f0ea9-195">Identyfikator URI przekierowania App1`msauth://com.example.userapp/IcB5PxIyvbLkbFVtBI%2FitkW%2Fejk%3D`</span><span class="sxs-lookup"><span data-stu-id="f0ea9-195">App1 Redirect URI: `msauth://com.example.userapp/IcB5PxIyvbLkbFVtBI%2FitkW%2Fejk%3D`</span></span>

<span data-ttu-id="f0ea9-196">Identyfikator URI przekierowania App2`msauth://com.example.userapp1/KmB7PxIytyLkbGHuI%2UitkW%2Fejk%4E`</span><span class="sxs-lookup"><span data-stu-id="f0ea9-196">App2 Redirect URI: `msauth://com.example.userapp1/KmB7PxIytyLkbGHuI%2UitkW%2Fejk%4E`</span></span>

<span data-ttu-id="f0ea9-197">Identyfikator URI przekierowania App3:`msauth://com.example.userapp2/Pt85PxIyvbLkbKUtBI%2SitkW%2Fejk%9F`</span><span class="sxs-lookup"><span data-stu-id="f0ea9-197">App3 Redirect URI: `msauth://com.example.userapp2/Pt85PxIyvbLkbKUtBI%2SitkW%2Fejk%9F`</span></span>

<span data-ttu-id="f0ea9-198">....</span><span class="sxs-lookup"><span data-stu-id="f0ea9-198">....</span></span>

<span data-ttu-id="f0ea9-199">Te są zagnieżdżone w tym samym identyfikatorze klienta / identyfikator aplikacji i wyszukiwać oparte na przekierowanie URI powrócisz do nas w konfiguracji zestawu SDK.</span><span class="sxs-lookup"><span data-stu-id="f0ea9-199">These are nested under the same client ID / application ID and looked up based on the redirect URI you return to us in your SDK configuration.</span></span>

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


<span data-ttu-id="f0ea9-200">*Należy pamiętać, że format tych identyfikator URI przekierowania opisano szczegółowo poniżej. Można użyć identyfikatora URI przekierowania, chyba że chcesz wspierać brokera, w takim przypadku one musi wyglądać powyższych*</span><span class="sxs-lookup"><span data-stu-id="f0ea9-200">*Note that the format of these Redirect URIs are explained below. You may use any Redirect URI unless you wish to support the broker, in which case they must look something like the above*</span></span>

#### <a name="step-2-configuring-shared-storage-in-android"></a><span data-ttu-id="f0ea9-201">Krok 2: Konfigurowanie magazynu udostępnionego w systemie Android</span><span class="sxs-lookup"><span data-stu-id="f0ea9-201">Step 2: Configuring shared storage in Android</span></span>
<span data-ttu-id="f0ea9-202">Ustawienie `SharedUserID` wykracza poza zakres tego dokumentu, ale może być rozpoznawane przez odczytanie w dokumentacji systemu Google Android na [manifestu](http://developer.android.com/guide/topics/manifest/manifest-element.html).</span><span class="sxs-lookup"><span data-stu-id="f0ea9-202">Setting the `SharedUserID` is beyond the scope of this document but can be learned by reading the Google Android documentation on the [Manifest](http://developer.android.com/guide/topics/manifest/manifest-element.html).</span></span> <span data-ttu-id="f0ea9-203">Ważne jest określenie mają sharedUserID Twojego zostanie wywołana i używać go do wszystkich aplikacji sieci.</span><span class="sxs-lookup"><span data-stu-id="f0ea9-203">What is important is that you decide what you want your sharedUserID will be called and use that across all your applications.</span></span>

<span data-ttu-id="f0ea9-204">Po utworzeniu `SharedUserID` w aplikacjach użytkownika można przystąpić do za pomocą logowania jednokrotnego.</span><span class="sxs-lookup"><span data-stu-id="f0ea9-204">Once you have the `SharedUserID` in all your applications you are ready to use SSO.</span></span>

> [!WARNING]
> <span data-ttu-id="f0ea9-205">Po udostępnieniu magazynu przez aplikacje dowolnej aplikacji, można usunąć użytkowników lub gorsze usunąć wszystkie tokeny w aplikacji.</span><span class="sxs-lookup"><span data-stu-id="f0ea9-205">When you share storage across your applications any application can delete users, or worse delete all the tokens across your application.</span></span> <span data-ttu-id="f0ea9-206">Jest to szczególnie Fatalne, jeśli masz aplikacje korzystające z tokenów do pracy w tle.</span><span class="sxs-lookup"><span data-stu-id="f0ea9-206">This is particularly disastrous if you have applications that rely on the tokens to do background work.</span></span> <span data-ttu-id="f0ea9-207">Udostępnianie magazynu oznacza, że należy zachować ostrożność bardzo w operacji Usuń wszystkie za pomocą zestawów SDK tożsamość firmy Microsoft.</span><span class="sxs-lookup"><span data-stu-id="f0ea9-207">Sharing storage means that you must be very careful in any and all remove operations through the Microsoft Identity SDKs.</span></span>
> 
> 

<span data-ttu-id="f0ea9-208">Gotowe.</span><span class="sxs-lookup"><span data-stu-id="f0ea9-208">That's it!</span></span> <span data-ttu-id="f0ea9-209">Zestaw SDK usługi Microsoft Identity teraz udostępniać poświadczeń we wszystkich aplikacjach.</span><span class="sxs-lookup"><span data-stu-id="f0ea9-209">The Microsoft Identity SDK will now share credentials across all your applications.</span></span> <span data-ttu-id="f0ea9-210">Lista użytkowników również będą udostępniane między wystąpieniami aplikacji.</span><span class="sxs-lookup"><span data-stu-id="f0ea9-210">The user list will also be shared across application instances.</span></span>

### <a name="turning-on-sso-for-broker-assisted-sso"></a><span data-ttu-id="f0ea9-211">Włączanie logowania jednokrotnego dla brokera asystowaną pomocą rejestracji Jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="f0ea9-211">Turning on SSO for broker assisted SSO</span></span>
<span data-ttu-id="f0ea9-212">Dla aplikacji pod kątem wykorzystania brokera, wszelkie zainstalowanego na urządzeniu jest **domyślnie wyłączone**.</span><span class="sxs-lookup"><span data-stu-id="f0ea9-212">The ability for an application to use any broker that is installed on the device is **turned off by default**.</span></span> <span data-ttu-id="f0ea9-213">Aby korzystać z aplikacji w brokera muszą nie dodatkowej konfiguracji i dodać kod do aplikacji.</span><span class="sxs-lookup"><span data-stu-id="f0ea9-213">In order to use your application with the broker you must do some additional configuration and add some code to your application.</span></span>

<span data-ttu-id="f0ea9-214">Wykonaj kroki są:</span><span class="sxs-lookup"><span data-stu-id="f0ea9-214">The steps to follow are:</span></span>

1. <span data-ttu-id="f0ea9-215">Włącz tryb brokera w kodzie aplikacji wywołania MS SDK</span><span class="sxs-lookup"><span data-stu-id="f0ea9-215">Enable broker mode in your application code's call to the MS SDK</span></span>
2. <span data-ttu-id="f0ea9-216">Ustanów nowy identyfikator URI przekierowania i zapewnić do rejestracji aplikacji i aplikacji</span><span class="sxs-lookup"><span data-stu-id="f0ea9-216">Establish a new redirect URI and provide that to both the app and your app registration</span></span>
3. <span data-ttu-id="f0ea9-217">Konfigurowanie odpowiednich uprawnień w manifestu systemu Android</span><span class="sxs-lookup"><span data-stu-id="f0ea9-217">Setting up the correct permissions in the Android manifest</span></span>

#### <a name="step-1-enable-broker-mode-in-your-application"></a><span data-ttu-id="f0ea9-218">Krok 1: Włącz broker tryb w aplikacji</span><span class="sxs-lookup"><span data-stu-id="f0ea9-218">Step 1: Enable broker mode in your application</span></span>
<span data-ttu-id="f0ea9-219">Możliwość aplikacji pod kątem wykorzystania brokera jest włączona, podczas tworzenia "ustawienia" lub początkowej konfiguracji wystąpienia uwierzytelniania.</span><span class="sxs-lookup"><span data-stu-id="f0ea9-219">The ability for your application to use the broker is turned on when you create the "settings" or initial setup of your Authentication instance.</span></span> <span data-ttu-id="f0ea9-220">Można to zrobić przez ustawienie danego typu ApplicationSettings w kodzie:</span><span class="sxs-lookup"><span data-stu-id="f0ea9-220">You do this by setting your ApplicationSettings type in your code:</span></span>

```
AuthenticationSettings.Instance.setUseBroker(true);
```


#### <a name="step-2-establish-a-new-redirect-uri-with-your-url-scheme"></a><span data-ttu-id="f0ea9-221">Krok 2: Ustanowić nowe przekierowania identyfikatorem URI ze schematem adresu URL</span><span class="sxs-lookup"><span data-stu-id="f0ea9-221">Step 2: Establish a new redirect URI with your URL Scheme</span></span>
<span data-ttu-id="f0ea9-222">Aby zapewnić, że firma Microsoft zawsze zwracają tokeny poświadczeń do właściwej aplikacji, musimy upewnij się, że firma Microsoft wywołania zwrotnego dla aplikacji w taki sposób, aby sprawdzić, systemu operacyjnego Android.</span><span class="sxs-lookup"><span data-stu-id="f0ea9-222">In order to ensure that we always return the credential tokens to the correct application, we need to make sure we call back to your application in a way that the Android operating system can verify.</span></span> <span data-ttu-id="f0ea9-223">System operacyjny Android używa skrót certyfikatu w sklepie Google Play.</span><span class="sxs-lookup"><span data-stu-id="f0ea9-223">The Android operating system uses the hash of the certificate in the Google Play store.</span></span> <span data-ttu-id="f0ea9-224">To nie może być sfałszowane przez nieautoryzowanej aplikacji.</span><span class="sxs-lookup"><span data-stu-id="f0ea9-224">This cannot be spoofed by a rogue application.</span></span> <span data-ttu-id="f0ea9-225">W związku z tym możemy wykorzystać to wraz z identyfikatora URI z naszej aplikacji brokera, aby upewnić się, że tokeny są zwracane do odpowiedniej aplikacji.</span><span class="sxs-lookup"><span data-stu-id="f0ea9-225">Therefore, we leverage this along with the URI of our broker application to ensure that the tokens are returned to the correct application.</span></span> <span data-ttu-id="f0ea9-226">Wymagane do nawiązania przekierowanie Unikatowy identyfikator URI zarówno w aplikacji i Ustaw jako identyfikator URI przekierowania w portalu deweloperów.</span><span class="sxs-lookup"><span data-stu-id="f0ea9-226">We require you to establish this unique redirect URI both in your application and set as a Redirect URI in our developer portal.</span></span>

<span data-ttu-id="f0ea9-227">Identyfikator URI przekierowania musi być w postaci prawidłowego:</span><span class="sxs-lookup"><span data-stu-id="f0ea9-227">Your redirect URI must be in the proper form of:</span></span>

`msauth://packagename/Base64UrlencodedSignature`

<span data-ttu-id="f0ea9-228">przykład: *msauth://com.example.userapp/IcB5PxIyvbLkbFVtBI%2FitkW%2Fejk%3D*</span><span class="sxs-lookup"><span data-stu-id="f0ea9-228">ex: *msauth://com.example.userapp/IcB5PxIyvbLkbFVtBI%2FitkW%2Fejk%3D*</span></span>

<span data-ttu-id="f0ea9-229">Ten identyfikator URI przekierowania trzeba określić za pomocą rejestracji aplikacji [portalu Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="f0ea9-229">This Redirect URI needs to be specified in your app registration using the [Azure portal](https://portal.azure.com/).</span></span> <span data-ttu-id="f0ea9-230">Aby uzyskać więcej informacji dotyczących rejestracji aplikacji usługi Azure AD, zobacz [integracji z usługą Azure Active Directory](active-directory-how-to-integrate.md).</span><span class="sxs-lookup"><span data-stu-id="f0ea9-230">For more information on Azure AD app registration, see [Integrating with Azure Active Directory](active-directory-how-to-integrate.md).</span></span>

#### <a name="step-3-set-up-the-correct-permissions-in-your-application"></a><span data-ttu-id="f0ea9-231">Krok 3: Konfigurowanie odpowiednich uprawnień w aplikacji</span><span class="sxs-lookup"><span data-stu-id="f0ea9-231">Step 3: Set up the correct permissions in your application</span></span>
<span data-ttu-id="f0ea9-232">Broker aplikacji w systemie Android korzysta z funkcji Menedżera kont systemu operacyjnego Android do zarządzania poświadczeniami w aplikacjach.</span><span class="sxs-lookup"><span data-stu-id="f0ea9-232">Our broker application in Android uses the Accounts Manager feature of the Android OS to manage credentials across applications.</span></span> <span data-ttu-id="f0ea9-233">Aby można było używać brokera w systemie Android manifest aplikacji musi mieć uprawnienia do korzystania z kont elementu AccountManager.</span><span class="sxs-lookup"><span data-stu-id="f0ea9-233">In order to use the broker in Android your app manifest must have permissions to use AccountManager accounts.</span></span> <span data-ttu-id="f0ea9-234">To jest omówiona szczegółowo w [Google dokumentację Menedżera kont w tym miejscu](http://developer.android.com/reference/android/accounts/AccountManager.html)</span><span class="sxs-lookup"><span data-stu-id="f0ea9-234">This is discussed in detail in the [Google documentation for Account Manager here](http://developer.android.com/reference/android/accounts/AccountManager.html)</span></span>

<span data-ttu-id="f0ea9-235">W szczególności te uprawnienia są:</span><span class="sxs-lookup"><span data-stu-id="f0ea9-235">In particular, these permissions are:</span></span>

```
GET_ACCOUNTS
USE_CREDENTIALS
MANAGE_ACCOUNTS
```

### <a name="youve-configured-sso"></a><span data-ttu-id="f0ea9-236">Skonfigurowaniu logowania jednokrotnego!</span><span class="sxs-lookup"><span data-stu-id="f0ea9-236">You've configured SSO!</span></span>
<span data-ttu-id="f0ea9-237">Teraz Microsoft tożsamość SDK automatycznie zarówno udostępnianie poświadczeń w aplikacji i wywołać brokera, jeśli jest obecny na urządzeniu.</span><span class="sxs-lookup"><span data-stu-id="f0ea9-237">Now the Microsoft Identity SDK will automatically both share credentials across your applications and invoke the broker if it's present on their device.</span></span>

