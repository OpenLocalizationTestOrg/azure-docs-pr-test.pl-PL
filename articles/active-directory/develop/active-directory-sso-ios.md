---
title: "aaaHow tooenable logowania jednokrotnego wielu aplikacji w systemie iOS przy użyciu biblioteki ADAL | Dokumentacja firmy Microsoft"
description: 'Jak funkcji hello toouse hello tooenable ADAL SDK rejestracji jednokrotnej w aplikacji. '
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
ms.openlocfilehash: b7b4389a8dcd956211ffa1aaa431aaf21ded8961
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooenable-cross-app-sso-on-ios-using-adal"></a><span data-ttu-id="e4874-103">Jak tooenable logowania jednokrotnego wielu aplikacji w systemie iOS przy użyciu biblioteki ADAL</span><span class="sxs-lookup"><span data-stu-id="e4874-103">How tooenable cross-app SSO on iOS using ADAL</span></span>
<span data-ttu-id="e4874-104">Zapewnianie pojedynczego logowania jednokrotnego (SSO), aby użytkownicy tylko muszą tooenter swoje poświadczenia raz i mieć tych poświadczeń, które są automatycznie pracy w aplikacjach teraz jest oczekiwany przez klientów.</span><span class="sxs-lookup"><span data-stu-id="e4874-104">Providing Single Sign-On (SSO) so that users only need tooenter their credentials once and have those credentials automatically work across applications is now expected by customers.</span></span> <span data-ttu-id="e4874-105">Hello trudności w wprowadzić swoją nazwę użytkownika i hasło na małego ekranu, często razy łączyć się przy użyciu dodatkowego składnika (2FA), takich jak rozmowa telefoniczna lub kod wysłana wiadomość SMS, powoduje niezadowolenie szybki, jeśli użytkownik ma toodo to więcej niż jeden raz na produkt.</span><span class="sxs-lookup"><span data-stu-id="e4874-105">hello difficulty in entering their username and password on a small screen, often times combined with an additional factor (2FA) like a phone call or a texted code, results in quick dissatisfaction if a user has toodo this more than one time for your product.</span></span>

<span data-ttu-id="e4874-106">Ponadto w przypadku zastosowania platformą tożsamości, które inne aplikacje mogą używać takich jak Accounts Microsoft lub konta służbowego z usługi Office 365, klienci oczekują, że te poświadczenia toobe toouse dostępne we wszystkich aplikacjach niezależnie hello dostawcy.</span><span class="sxs-lookup"><span data-stu-id="e4874-106">In addition, if you apply an identity platform that other applications may use such as Microsoft Accounts or a work account from Office365, customers expect that those credentials toobe available toouse across all their applications no matter hello vendor.</span></span>

<span data-ttu-id="e4874-107">Hello platformy pakietu Microsoft Identity, wraz z nasze zestawy SDK tożsamości Microsoft działa wszystkich tego twardym i zapewnia hello toodelight możliwości swoich klientów za pomocą logowania jednokrotnego, albo w ramach własnego pakietu aplikacji, lub jako z możliwości brokera i wystawcy uwierzytelnienia aplikacje na powitania wszystkich danych z urządzenia.</span><span class="sxs-lookup"><span data-stu-id="e4874-107">hello Microsoft Identity platform, along with our Microsoft Identity SDKs, does all this hard work for you and gives you hello ability toodelight your customers with SSO either within your own suite of applications or, as with our broker capability and Authenticator applications, across hello entire device.</span></span>

<span data-ttu-id="e4874-108">W tym przewodniku informuje o sposobie tooconfigure naszego zestawu SDK w ramach Twojej aplikacji tooprovide klientów tooyour tego korzyści.</span><span class="sxs-lookup"><span data-stu-id="e4874-108">This walkthrough will tell you how tooconfigure our SDK within your application tooprovide this benefit tooyour customers.</span></span>

<span data-ttu-id="e4874-109">Ten przewodnik dotyczy:</span><span class="sxs-lookup"><span data-stu-id="e4874-109">This walkthrough applies to:</span></span>

* <span data-ttu-id="e4874-110">Usługa Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="e4874-110">Azure Active Directory</span></span>
* <span data-ttu-id="e4874-111">Azure Active Directory B2C</span><span class="sxs-lookup"><span data-stu-id="e4874-111">Azure Active Directory B2C</span></span>
* <span data-ttu-id="e4874-112">B2B usługi Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="e4874-112">Azure Active Directory B2B</span></span>
* <span data-ttu-id="e4874-113">Dostęp warunkowy usługi Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="e4874-113">Azure Active Directory Conditional Access</span></span>

<span data-ttu-id="e4874-114">dokument Hello poprzedniego przyjęto założenie, wiesz, jak za[udostępnić aplikacje w portalu starszych hello usługi Azure Active Directory](active-directory-how-to-integrate.md) i zintegrowane aplikacji z hello [pakietu Microsoft Identity iOS SDK](https://github.com/AzureAD/azure-activedirectory-library-for-objc).</span><span class="sxs-lookup"><span data-stu-id="e4874-114">hello document preceding assumes you know how too[provision applications in hello legacy portal for Azure Active Directory](active-directory-how-to-integrate.md) and integrated your application with hello [Microsoft Identity iOS SDK](https://github.com/AzureAD/azure-activedirectory-library-for-objc).</span></span>

## <a name="sso-concepts-in-hello-microsoft-identity-platform"></a><span data-ttu-id="e4874-115">Pojęcia dotyczące logowania jednokrotnego hello platformą tożsamości Microsoft</span><span class="sxs-lookup"><span data-stu-id="e4874-115">SSO Concepts in hello Microsoft Identity Platform</span></span>
### <a name="microsoft-identity-brokers"></a><span data-ttu-id="e4874-116">Brokerzy tożsamość firmy Microsoft</span><span class="sxs-lookup"><span data-stu-id="e4874-116">Microsoft Identity Brokers</span></span>
<span data-ttu-id="e4874-117">Firma Microsoft udostępnia aplikacji dla każdej platformy przenośne, które umożliwiają mostkowania hello poświadczeń w aplikacjach pochodzących od różnych dostawców i umożliwia specjalne udoskonalone funkcje, które wymagają pojedynczego bezpiecznym miejscu w przypadku toovalidate poświadczeń.</span><span class="sxs-lookup"><span data-stu-id="e4874-117">Microsoft provides applications for every mobile platform that allow for hello bridging of credentials across applications from different vendors and allows for special enhanced features that require a single secure place from where toovalidate credentials.</span></span> <span data-ttu-id="e4874-118">Nazywamy je **brokerzy**.</span><span class="sxs-lookup"><span data-stu-id="e4874-118">We call these **brokers**.</span></span> <span data-ttu-id="e4874-119">W systemach iOS i Android te brokerzy są realizowane za pośrednictwem aplikacji do pobrania, że klienci zainstalować niezależnie lub można je przesłać toohello urządzeń przez użytkowników, którzy zarządzają niektórych lub wszystkich urządzeń hello dla swoich pracowników firmy.</span><span class="sxs-lookup"><span data-stu-id="e4874-119">On iOS and Android these brokers are provided through downloadable applications that customers either install independently or can be pushed toohello device by a company who manages some or all of hello device for their employee.</span></span> <span data-ttu-id="e4874-120">Te brokerzy obsługuje zarządzanie zabezpieczeń tylko dla niektórych aplikacji lub hello wszystkich danych z urządzenia oparte na potrzeby administratorzy IT.</span><span class="sxs-lookup"><span data-stu-id="e4874-120">These brokers support managing security just for some applications or hello entire device based on what IT Administrators desire.</span></span> <span data-ttu-id="e4874-121">W systemie Windows ta funkcja jest dostarczana przez selektora konta wbudowane w system operacyjny toohello technicznie nazywane hello brokera uwierzytelniania sieci Web.</span><span class="sxs-lookup"><span data-stu-id="e4874-121">In Windows, this functionality is provided by an account chooser built in toohello operating system, known technically as hello Web Authentication Broker.</span></span>

<span data-ttu-id="e4874-122">Aby uzyskać więcej informacji na temat używamy tych brokerów i jak klienci mogą je wyświetlać w ich przepływu logowania dla platformy pakietu Microsoft Identity hello na.</span><span class="sxs-lookup"><span data-stu-id="e4874-122">For more information on how we use these brokers and how your customers might see them in their login flow for hello Microsoft Identity platform read on.</span></span>

### <a name="patterns-for-logging-in-on-mobile-devices"></a><span data-ttu-id="e4874-123">Wzorce do logowania na urządzeniach przenośnych</span><span class="sxs-lookup"><span data-stu-id="e4874-123">Patterns for logging in on mobile devices</span></span>
<span data-ttu-id="e4874-124">Toocredentials dostępu na urządzeniach wykonaj dwa podstawowe wzorce platformy pakietu Microsoft Identity hello:</span><span class="sxs-lookup"><span data-stu-id="e4874-124">Access toocredentials on devices follow two basic patterns for hello Microsoft Identity platform:</span></span>

* <span data-ttu-id="e4874-125">Logowania asystowaną bez brokera</span><span class="sxs-lookup"><span data-stu-id="e4874-125">Non-broker assisted logins</span></span>
* <span data-ttu-id="e4874-126">Broker asystowaną logowania</span><span class="sxs-lookup"><span data-stu-id="e4874-126">Broker assisted logins</span></span>

#### <a name="non-broker-assisted-logins"></a><span data-ttu-id="e4874-127">Logowania asystowaną bez brokera</span><span class="sxs-lookup"><span data-stu-id="e4874-127">Non-broker assisted logins</span></span>
<span data-ttu-id="e4874-128">Inne niż brokera asystowaną logowania są funkcji logowania, które wykonana wbudowany z aplikacji hello i Użyj magazynu lokalnego hello hello urządzenia dla tej aplikacji.</span><span class="sxs-lookup"><span data-stu-id="e4874-128">Non-broker assisted logins are login experiences that happen inline with hello application and use hello local storage on hello device for that application.</span></span> <span data-ttu-id="e4874-129">Ten magazyn może być współużytkowany przez aplikacje, ale poświadczenia hello są ściśle powiązane toohello aplikacji lub pakietu aplikacji przy użyciu to poświadczenie.</span><span class="sxs-lookup"><span data-stu-id="e4874-129">This storage may be shared across applications but hello credentials are tightly bound toohello app or suite of apps using that credential.</span></span> <span data-ttu-id="e4874-130">W przypadku najprawdopodobniej wystąpienia to w wielu aplikacjach mobilnych podczas wprowadzania nazwy użytkownika i hasła w samej aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="e4874-130">You've most likely experienced this in many mobile applications when you enter a username and password within hello application itself.</span></span>

<span data-ttu-id="e4874-131">Te nazwy logowania ma hello następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="e4874-131">These logins have hello following benefits:</span></span>

* <span data-ttu-id="e4874-132">Środowisko użytkownika istnieje w całości w aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="e4874-132">User experience exists entirely within hello application.</span></span>
* <span data-ttu-id="e4874-133">Poświadczenia mogą być współużytkowane przez aplikacje, które są podpisane przez hello tego samego certyfikatu, podając mechanizm obsługi rejestracji jednokrotnej tooyour aplikacji.</span><span class="sxs-lookup"><span data-stu-id="e4874-133">Credentials can be shared across applications that are signed by hello same certificate, providing a single sign-on experience tooyour suite of applications.</span></span>
* <span data-ttu-id="e4874-134">Formant wokół hello środowisko logowania jest dostarczany aplikacji toohello przed i po zalogowaniu.</span><span class="sxs-lookup"><span data-stu-id="e4874-134">Control around hello experience of logging in is provided toohello application before and after sign-in.</span></span>

<span data-ttu-id="e4874-135">Te nazwy logowania ma następujące wady hello:</span><span class="sxs-lookup"><span data-stu-id="e4874-135">These logins have hello following drawbacks:</span></span>

* <span data-ttu-id="e4874-136">Użytkownika nie może występować jednokrotnego we wszystkich aplikacji, które używają pakietu Microsoft Identity przez te firmy Microsoft Identities skonfigurowane w aplikacji.</span><span class="sxs-lookup"><span data-stu-id="e4874-136">User cannot experience single-sign on across all apps that use a Microsoft Identity, only across those Microsoft Identities that your application has configured.</span></span>
* <span data-ttu-id="e4874-137">Nie można używać aplikacji z bardziej zaawansowane funkcje biznesowych, takich jak dostęp warunkowy lub zestawu InTune hello Użyj produktów.</span><span class="sxs-lookup"><span data-stu-id="e4874-137">Your application cannot be used with more advanced business features such as Conditional Access or use hello InTune suite of products.</span></span>
* <span data-ttu-id="e4874-138">Używana aplikacja nie obsługuje uwierzytelniania opartego na certyfikatach dla użytkowników biznesowych.</span><span class="sxs-lookup"><span data-stu-id="e4874-138">Your application can't support certificate-based authentication for business users.</span></span>

<span data-ttu-id="e4874-139">Oto reprezentację jak zestawy SDK tożsamości Microsoft hello pracować z hello udostępniony magazyn tooenable Twojej aplikacji rejestracji Jednokrotnej:</span><span class="sxs-lookup"><span data-stu-id="e4874-139">Here is a representation of how hello Microsoft Identity SDKs work with hello shared storage of your applications tooenable SSO:</span></span>

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

#### <a name="broker-assisted-logins"></a><span data-ttu-id="e4874-140">Broker asystowaną logowania</span><span class="sxs-lookup"><span data-stu-id="e4874-140">Broker assisted logins</span></span>
<span data-ttu-id="e4874-141">Asystowane brokera logowania są środowiska logowania, przeprowadzone w ciągu hello brokera aplikacji, które obsługują hello magazynu i zabezpieczeń hello brokera tooshare poświadczeń we wszystkich aplikacjach na urządzeniu hello stosowane hello pakietu Microsoft Identity platformy.</span><span class="sxs-lookup"><span data-stu-id="e4874-141">Broker-assisted logins are login experiences that occur within hello broker application and use hello storage and security of hello broker tooshare credentials across all applications on hello device that apply hello Microsoft Identity platform.</span></span> <span data-ttu-id="e4874-142">Oznacza to, że aplikacje zależne od hello brokera toosign użytkowników w.</span><span class="sxs-lookup"><span data-stu-id="e4874-142">This means that your applications rely on hello broker toosign users in.</span></span> <span data-ttu-id="e4874-143">W systemach iOS i Android brokerzy te są realizowane za pośrednictwem aplikacji do pobrania, czy klientów zainstalować niezależnie lub można je przesłać toohello urządzenia przez firmę, użytkowników, którzy zarządzają hello urządzenie ich użytkownika.</span><span class="sxs-lookup"><span data-stu-id="e4874-143">On iOS and Android these brokers are provided through downloadable applications that customers either install independently or can be pushed toohello device by a company who manages hello device for their user.</span></span> <span data-ttu-id="e4874-144">Przykładem tego typu aplikacji jest aplikacją Microsoft Authenticator hello w systemie iOS.</span><span class="sxs-lookup"><span data-stu-id="e4874-144">An example of this type of application is hello Microsoft Authenticator application on iOS.</span></span> <span data-ttu-id="e4874-145">W systemie Windows ta funkcja jest dostarczana przez selektora konta wbudowane w system operacyjny toohello technicznie nazywane hello brokera uwierzytelniania sieci Web.</span><span class="sxs-lookup"><span data-stu-id="e4874-145">In Windows this functionality is provided by an account chooser built in toohello operating system, known technically as hello Web Authentication Broker.</span></span>
<span data-ttu-id="e4874-146">środowisko Hello jest zależna od platformy i czasami mogą być destrukcyjne toousers Jeśli nie poprawnie zarządzane.</span><span class="sxs-lookup"><span data-stu-id="e4874-146">hello experience varies by platform and can sometimes be disruptive toousers if not managed correctly.</span></span> <span data-ttu-id="e4874-147">Znasz prawdopodobnie najbardziej tego wzorca Jeśli masz zainstalowaną aplikację usługi Facebook hello i używać funkcji usługi Facebook połączenie z innej aplikacji.</span><span class="sxs-lookup"><span data-stu-id="e4874-147">You're probably most familiar with this pattern if you have hello Facebook application installed and use Facebook Connect from another application.</span></span> <span data-ttu-id="e4874-148">Witaj używa platformy pakietu Microsoft Identity hello tego samego wzorca.</span><span class="sxs-lookup"><span data-stu-id="e4874-148">hello Microsoft Identity platform uses hello same pattern.</span></span>

<span data-ttu-id="e4874-149">Dla systemu iOS prowadzi to animacji "przejścia" tooa aplikacji wysyłania tła toohello podczas aplikacji Microsoft Authenticator hello pochodzi pierwszego planu toohello dla tooselect użytkownika hello konto, które chciałby toosign przy użyciu.</span><span class="sxs-lookup"><span data-stu-id="e4874-149">For iOS this leads tooa "transition" animation where your application is sent toohello background while hello Microsoft Authenticator applications comes toohello foreground for hello user tooselect which account they would like toosign in with.</span></span>  

<span data-ttu-id="e4874-150">Dla systemów Android i Windows hello konta selektora jest wyświetlany u góry aplikację, która jest prostszy toohello użytkownika.</span><span class="sxs-lookup"><span data-stu-id="e4874-150">For Android and Windows hello account chooser is displayed on top of your application which is less disruptive toohello user.</span></span>

#### <a name="how-hello-broker-gets-invoked"></a><span data-ttu-id="e4874-151">Sposób wywoływania pobiera hello brokera</span><span class="sxs-lookup"><span data-stu-id="e4874-151">How hello broker gets invoked</span></span>
<span data-ttu-id="e4874-152">Jeśli zgodny brokera jest zainstalowany na urządzeniu hello, takich jak hello Microsoft Authenticator aplikacji hello zestawów SDK programu Microsoft Identity będzie automatycznie hello pracy wywoływania brokera hello automatycznie, gdy użytkownik wskazuje życzą toolog przy użyciu dowolnego konta z Platforma Microsoft Identity Hello.</span><span class="sxs-lookup"><span data-stu-id="e4874-152">If a compatible broker is installed on hello device, like hello Microsoft Authenticator application, hello Microsoft Identity SDKs will automatically do hello work of invoking hello broker for you when a user indicates they wish toolog in using any account from hello Microsoft Identity platform.</span></span> <span data-ttu-id="e4874-153">To konto może być Account firmy Microsoft, służbowy lub konta służbowego lub konta, które należy podać i hosta na platformie Azure przy użyciu naszych produktów B2C i B2B.</span><span class="sxs-lookup"><span data-stu-id="e4874-153">This account could be a personal Microsoft Account, a work or school account, or an account that you provide and host in Azure using our B2C and B2B products.</span></span> 

 #### <a name="how-we-ensure-hello-application-is-valid"></a><span data-ttu-id="e4874-154">Jak firma Microsoft zapewnia aplikacji hello jest prawidłowy</span><span class="sxs-lookup"><span data-stu-id="e4874-154">How we ensure hello application is valid</span></span>
 
 <span data-ttu-id="e4874-155">Hello potrzeby tooensure hello tożsamość aplikacji wywołania hello brokera jest toohello kluczową rolę zabezpieczeń, dostarczamy w danych logowania brokera wspierana.</span><span class="sxs-lookup"><span data-stu-id="e4874-155">hello need tooensure hello identity of an application call hello broker is crucial toohello security we provide in broker assisted logins.</span></span> <span data-ttu-id="e4874-156">Z systemem iOS ani Android wymusza unikatowych identyfikatorów, które są prawidłowe tylko dla danej aplikacji, więc złośliwego aplikacji może "sfałszować" identyfikator uzasadnionych aplikacji i odbierać tokeny hello przeznaczone dla aplikacji uzasadnionych hello.</span><span class="sxs-lookup"><span data-stu-id="e4874-156">Neither iOS nor Android enforces unique identifiers that are valid only for a given application, so malicious applications may "spoof" a legitimate application's identifier and receive hello tokens meant for hello legitimate application.</span></span> <span data-ttu-id="e4874-157">tooensure, który zawsze komunikują się firma Microsoft z prawej aplikacji hello w czasie wykonywania, poprosimy hello developer tooprovide redirectURI niestandardowych podczas rejestrowania aplikacji z firmą Microsoft.</span><span class="sxs-lookup"><span data-stu-id="e4874-157">tooensure we are always communicating with hello right application at runtime, we ask hello developer tooprovide a custom redirectURI when registering their application with Microsoft.</span></span> <span data-ttu-id="e4874-158">**Jak deweloperzy powinien spreparować identyfikator URI przekierowania omówiono szczegółowo poniżej.**</span><span class="sxs-lookup"><span data-stu-id="e4874-158">**How developers should craft this redirect URI is discussed in detail below.**</span></span> <span data-ttu-id="e4874-159">To niestandardowe redirectURI zawiera hello identyfikator pakietu aplikacji hello i jest zapewniana toobe unikatowy toohello aplikacji przez hello sklepu Apple App Store.</span><span class="sxs-lookup"><span data-stu-id="e4874-159">This custom redirectURI contains hello Bundle ID of hello application and is ensured toobe unique toohello application by hello Apple App Store.</span></span> <span data-ttu-id="e4874-160">Po wyświetleniu monitu brokera hello hello brokera połączeń aplikacji hello iOS tooprovide systemu operacyjnego za pomocą hello identyfikator pakietu, który wywołał hello brokera.</span><span class="sxs-lookup"><span data-stu-id="e4874-160">When an application calls hello broker, hello broker asks hello iOS operating system tooprovide it with hello Bundle ID that called hello broker.</span></span> <span data-ttu-id="e4874-161">Hello broker zawiera tooMicrosoft ten identyfikator pakietu w hello wywołania tooour tożsamości systemu.</span><span class="sxs-lookup"><span data-stu-id="e4874-161">hello broker provides this Bundle ID tooMicrosoft in hello call tooour identity system.</span></span> <span data-ttu-id="e4874-162">Identyfikator pakietu aplikacji hello hello niezgodna hello, podać identyfikator pakietu toous przez dewelopera hello podczas rejestracji, firma Microsoft będzie odmawiał dostępu toohello tokenów dla aplikacji hello zasobów hello żąda.</span><span class="sxs-lookup"><span data-stu-id="e4874-162">If hello Bundle ID of hello application does not match hello Bundle ID provided toous by hello developer during registration, we will deny access toohello tokens for hello resource hello application is requesting.</span></span> <span data-ttu-id="e4874-163">Tego wyboru gwarantuje, że tylko aplikacja hello zarejestrowany przez dewelopera hello odbiera tokenów.</span><span class="sxs-lookup"><span data-stu-id="e4874-163">This check ensures that only hello application registered by hello developer receives tokens.</span></span>

<span data-ttu-id="e4874-164">**Deweloper Hello ma wybór hello hello zestaw SDK programu Microsoft Identity wywołuje brokera hello lub korzysta z przepływu asystowaną hello bez brokera.**</span><span class="sxs-lookup"><span data-stu-id="e4874-164">**hello developer has hello choice of if hello Microsoft Identity SDK calls hello broker or uses hello non-broker assisted flow.**</span></span> <span data-ttu-id="e4874-165">Jednak jeśli hello developer wybierze nie toouse hello wspierana brokera przepływu utracą zaletą hello przy użyciu poświadczeń logowania jednokrotnego użytkownika hello zostało już dodane na urządzeniu hello i uniemożliwia ich aplikacji z użycia przy użyciu funkcji biznesowych firmy Microsoft Umożliwia klientom, takich jak dostęp warunkowy, możliwości zarządzania usługi Intune i uwierzytelnianie oparte na certyfikatach.</span><span class="sxs-lookup"><span data-stu-id="e4874-165">However if hello developer chooses not toouse hello broker-assisted flow they lose hello benefit of using SSO credentials that hello user may have already added on hello device and prevents their application from being used with business features Microsoft provides its customers such as Conditional Access, Intune Management capabilities, and certificate-based authentication.</span></span>

<span data-ttu-id="e4874-166">Te nazwy logowania ma hello następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="e4874-166">These logins have hello following benefits:</span></span>

* <span data-ttu-id="e4874-167">Użytkownik napotyka logowania jednokrotnego w swoich aplikacjach bez względu na powitania dostawcy.</span><span class="sxs-lookup"><span data-stu-id="e4874-167">User experiences SSO across all their applications no matter hello vendor.</span></span>
* <span data-ttu-id="e4874-168">Aplikacji można użyć bardziej zaawansowane funkcje biznesowych, takich jak dostęp warunkowy lub zestawu InTune hello produktów.</span><span class="sxs-lookup"><span data-stu-id="e4874-168">Your application can use more advanced business features such as Conditional Access or use hello InTune suite of products.</span></span>
* <span data-ttu-id="e4874-169">Aplikacja może obsługiwać uwierzytelnianie oparte na certyfikatach dla użytkowników biznesowych.</span><span class="sxs-lookup"><span data-stu-id="e4874-169">Your application can support certificate-based authentication for business users.</span></span>
* <span data-ttu-id="e4874-170">Bardziej bezpieczne logowanie występować jako hello tożsamości aplikacji hello i użytkownika hello są weryfikowane przez aplikację brokera hello z algorytmów zabezpieczeń i szyfrowania.</span><span class="sxs-lookup"><span data-stu-id="e4874-170">Much more secure sign-in experience as hello identity of hello application and hello user are verified by hello broker application with additional security algorithms and encryption.</span></span>

<span data-ttu-id="e4874-171">Te nazwy logowania ma następujące wady hello:</span><span class="sxs-lookup"><span data-stu-id="e4874-171">These logins have hello following drawbacks:</span></span>

* <span data-ttu-id="e4874-172">W systemie iOS hello użytkownika jest są przenoszone poza środowisko aplikacji, a poświadczenia zostały wybrane.</span><span class="sxs-lookup"><span data-stu-id="e4874-172">In iOS hello user is transitioned out of your application's experience while credentials are chosen.</span></span>
* <span data-ttu-id="e4874-173">Wystąpić utrata hello możliwości toomanage hello logowania dla klientów w aplikacji.</span><span class="sxs-lookup"><span data-stu-id="e4874-173">Loss of hello ability toomanage hello login experience for your customers within your application.</span></span>

<span data-ttu-id="e4874-174">Oto reprezentację jak hello zestawów SDK programu Microsoft Identity współpracują z hello broker tooenable aplikacji rejestracji Jednokrotnej:</span><span class="sxs-lookup"><span data-stu-id="e4874-174">Here is a representation of how hello Microsoft Identity SDKs work with hello broker applications tooenable SSO:</span></span>

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

<span data-ttu-id="e4874-175">Dzięki tym informacje powinno być możliwe toobetter poznanie i wdrożenie logowania jednokrotnego w aplikacji przy użyciu platformy pakietu Microsoft Identity hello i zestawy SDK.</span><span class="sxs-lookup"><span data-stu-id="e4874-175">Armed with this background information you should be able toobetter understand and implement SSO within your application using hello Microsoft Identity platform and SDKs.</span></span>

## <a name="enabling-cross-app-sso-using-adal"></a><span data-ttu-id="e4874-176">Włączanie logowania jednokrotnego wielu aplikacji za pomocą biblioteki ADAL</span><span class="sxs-lookup"><span data-stu-id="e4874-176">Enabling cross-app SSO using ADAL</span></span>
<span data-ttu-id="e4874-177">W tym miejscu używamy hello ADAL dla systemu iOS SDK do:</span><span class="sxs-lookup"><span data-stu-id="e4874-177">Here we use hello ADAL iOS SDK to:</span></span>

* <span data-ttu-id="e4874-178">Włącz brokera z systemem innym niż asystowaną pomocą rejestracji Jednokrotnej dla pakietu aplikacji</span><span class="sxs-lookup"><span data-stu-id="e4874-178">Turn on non-broker assisted SSO for your suite of apps</span></span>
* <span data-ttu-id="e4874-179">Włączanie obsługi wspierana brokera logowania jednokrotnego</span><span class="sxs-lookup"><span data-stu-id="e4874-179">Turn on support for broker-assisted SSO</span></span>

### <a name="turning-on-sso-for-non-broker-assisted-sso"></a><span data-ttu-id="e4874-180">Włączanie rejestracji Jednokrotnej z systemem innym niż brokera asystowaną pomocą rejestracji Jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="e4874-180">Turning on SSO for non-broker assisted SSO</span></span>
<span data-ttu-id="e4874-181">Dla innych niż brokera asystowaną logowania jednokrotnego w aplikacjach hello zestawów SDK programu Microsoft Identity Zarządzanie znacznie hello złożoność logowania jednokrotnego dla Ciebie.</span><span class="sxs-lookup"><span data-stu-id="e4874-181">For non-broker assisted SSO across applications hello Microsoft Identity SDKs manage much of hello complexity of SSO for you.</span></span> <span data-ttu-id="e4874-182">W tym znajdowanie hello prawo użytkownika w pamięci podręcznej hello i utrzymywanie lista zalogowany użytkowników możesz tooquery.</span><span class="sxs-lookup"><span data-stu-id="e4874-182">This includes finding hello right user in hello cache and maintaining a list of logged in users for you tooquery.</span></span>

<span data-ttu-id="e4874-183">tooenable logowania jednokrotnego w aplikacjach własnej potrzebne hello toodo następujące:</span><span class="sxs-lookup"><span data-stu-id="e4874-183">tooenable SSO across applications you own you need toodo hello following:</span></span>

1. <span data-ttu-id="e4874-184">Upewnij się, wszystkie Twoje aplikacje użytkownika hello tego samego Identyfikatora klienta lub identyfikator aplikacji.</span><span class="sxs-lookup"><span data-stu-id="e4874-184">Ensure all your applications user hello same Client ID or Application ID.</span></span>
2. <span data-ttu-id="e4874-185">Upewnij się, że wszystkie Twoje hello udziału aplikacji podpisywania tego samego certyfikatu firmy Apple, dzięki czemu można udostępniać pęki kluczy</span><span class="sxs-lookup"><span data-stu-id="e4874-185">Ensure that all of your applications share hello same signing certificate from Apple so that you can share keychains</span></span>
3. <span data-ttu-id="e4874-186">Żądanie hello uprawnienie łańcucha kluczy dla poszczególnych aplikacji.</span><span class="sxs-lookup"><span data-stu-id="e4874-186">Request hello same keychain entitlement for each of your applications.</span></span>
4. <span data-ttu-id="e4874-187">Opisz zestawów SDK tożsamości Microsoft hello hello udostępnionego łańcucha kluczy, które chcesz nam toouse.</span><span class="sxs-lookup"><span data-stu-id="e4874-187">Tell hello Microsoft Identity SDKs about hello shared keychain you want us toouse.</span></span>

#### <a name="using-hello-same-client-id--application-id-for-all-hello-applications-in-your-suite-of-apps"></a><span data-ttu-id="e4874-188">Przy użyciu hello na tym samym identyfikatorze klienta / IDENTYFIKATORA aplikacji dla wszystkich hello aplikacji w pakietu aplikacji</span><span class="sxs-lookup"><span data-stu-id="e4874-188">Using hello same Client ID / Application ID for all hello applications in your suite of apps</span></span>
<span data-ttu-id="e4874-189">Aby tooknow platformy pakietu Microsoft Identity hello, że tokeny tooshare jest dozwolony w aplikacji należy poszczególnych aplikacji hello tooshare tego samego Identyfikatora klienta lub identyfikator aplikacji.</span><span class="sxs-lookup"><span data-stu-id="e4874-189">In order for hello Microsoft Identity platform tooknow that it's allowed tooshare tokens across your applications, each of your applications will need tooshare hello same Client ID or Application ID.</span></span> <span data-ttu-id="e4874-190">Jest to hello Unikatowy identyfikator, który podano tooyou podczas rejestrowania swoją pierwszą aplikację w portalu hello.</span><span class="sxs-lookup"><span data-stu-id="e4874-190">This is hello unique identifier that was provided tooyou when you registered your first application in hello portal.</span></span>

<span data-ttu-id="e4874-191">Możesz się zastanawiać, jak należy określić różnych aplikacji hello toohello pakietu Microsoft Identity usługa korzysta z tego samego identyfikatora aplikacji.</span><span class="sxs-lookup"><span data-stu-id="e4874-191">You may be wondering how you will identify different apps toohello Microsoft Identity service if it uses hello same Application ID.</span></span> <span data-ttu-id="e4874-192">Witaj odpowiedzi jest z hello **identyfikator URI przekierowania**.</span><span class="sxs-lookup"><span data-stu-id="e4874-192">hello answer is with hello **Redirect URIs**.</span></span> <span data-ttu-id="e4874-193">Każda aplikacja może mieć wiele identyfikator URI przekierowania zarejestrowany w hello przechodzenia do portalu.</span><span class="sxs-lookup"><span data-stu-id="e4874-193">Each application can have multiple Redirect URIs registered in hello onboarding portal.</span></span> <span data-ttu-id="e4874-194">Każdej aplikacji w zestawie ma inny identyfikator URI przekierowania.</span><span class="sxs-lookup"><span data-stu-id="e4874-194">Each app in your suite will have a different redirect URI.</span></span> <span data-ttu-id="e4874-195">Jak wygląda przykład znajduje się poniżej:</span><span class="sxs-lookup"><span data-stu-id="e4874-195">An example of how this looks is below:</span></span>

<span data-ttu-id="e4874-196">Identyfikator URI przekierowania App1`x-msauth-mytestiosapp://com.myapp.mytestapp`</span><span class="sxs-lookup"><span data-stu-id="e4874-196">App1 Redirect URI: `x-msauth-mytestiosapp://com.myapp.mytestapp`</span></span>

<span data-ttu-id="e4874-197">Identyfikator URI przekierowania App2`x-msauth-mytestiosapp://com.myapp.mytestapp2`</span><span class="sxs-lookup"><span data-stu-id="e4874-197">App2 Redirect URI: `x-msauth-mytestiosapp://com.myapp.mytestapp2`</span></span>

<span data-ttu-id="e4874-198">Identyfikator URI przekierowania App3:`x-msauth-mytestiosapp://com.myapp.mytestapp3`</span><span class="sxs-lookup"><span data-stu-id="e4874-198">App3 Redirect URI: `x-msauth-mytestiosapp://com.myapp.mytestapp3`</span></span>

<span data-ttu-id="e4874-199">....</span><span class="sxs-lookup"><span data-stu-id="e4874-199">....</span></span>

<span data-ttu-id="e4874-200">Te są zagnieżdżone w ramach tego samego Identyfikatora klienta hello / identyfikator aplikacji i wyszukiwać na podstawie hello przekierowania URI powrocie toous w konfiguracji zestawu SDK.</span><span class="sxs-lookup"><span data-stu-id="e4874-200">These are nested under hello same client ID / application ID and looked up based on hello redirect URI you return toous in your SDK configuration.</span></span>

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


<span data-ttu-id="e4874-201">*Należy pamiętać, że format tych identyfikatorów przekierowania hello opisano poniżej. Identyfikator URI przekierowania może używać, chyba że chcesz toosupport hello brokera, w tym przypadku one musi wyglądać hello powyżej*</span><span class="sxs-lookup"><span data-stu-id="e4874-201">*Note that hello format of these Redirect URIs are explained below. You may use any Redirect URI unless you wish toosupport hello broker, in which case they must look something like hello above*</span></span>

#### <a name="create-keychain-sharing-between-applications"></a><span data-ttu-id="e4874-202">Tworzenie łańcucha kluczy udostępnianie między aplikacjami</span><span class="sxs-lookup"><span data-stu-id="e4874-202">Create keychain sharing between applications</span></span>
<span data-ttu-id="e4874-203">Włączenie udostępniania łańcucha kluczy wykracza poza zakres tego dokumentu hello i objęte ich dokumentu przez firmę Apple [Dodawanie możliwości](https://developer.apple.com/library/ios/documentation/IDEs/Conceptual/AppDistributionGuide/AddingCapabilities/AddingCapabilities.html).</span><span class="sxs-lookup"><span data-stu-id="e4874-203">Enabling keychain sharing is beyond hello scope of this document and covered by Apple in their document [Adding Capabilities](https://developer.apple.com/library/ios/documentation/IDEs/Conceptual/AppDistributionGuide/AddingCapabilities/AddingCapabilities.html).</span></span> <span data-ttu-id="e4874-204">Ważne jest zdecydować, co Twoje toobe łańcucha kluczy o nazwie, a następnie dodać tę możliwość we wszystkich aplikacjach.</span><span class="sxs-lookup"><span data-stu-id="e4874-204">What is important is that you decide what you want your keychain toobe called and add that capability across all your applications.</span></span>

<span data-ttu-id="e4874-205">Jeśli masz plik w katalogu projektu pod tytułem powinna zostać wyświetlona poprawnie można skonfigurować uprawnienia do `entitlements.plist` coś, która wygląda hello zawiera:</span><span class="sxs-lookup"><span data-stu-id="e4874-205">When you do have entitlements set up correctly you should see a file in your project directory entitled `entitlements.plist` that contains something that looks like hello following:</span></span>

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

<span data-ttu-id="e4874-206">Po masz uprawnienie łańcucha kluczy hello włączone w każdej aplikacji i są gotowe toouse logowania jednokrotnego, opisz hello zestaw SDK programu Microsoft Identity z łańcucha kluczy za pomocą hello następujące ustawienie w Twojej `ADAuthenticationSettings` z hello następujące ustawienia:</span><span class="sxs-lookup"><span data-stu-id="e4874-206">Once you have hello keychain entitlement enabled in each of your applications, and you are ready toouse SSO, tell hello Microsoft Identity SDK about your keychain by using hello following setting in your `ADAuthenticationSettings` with hello following setting:</span></span>

```
defaultKeychainSharingGroup=@"com.myapp.mycache";
```

> [!WARNING]
> <span data-ttu-id="e4874-207">Jeśli udostępnianie łańcucha kluczy w aplikacji dowolnej aplikacji, można usunąć użytkowników lub gorsze usunąć wszystkie tokeny hello w aplikacji.</span><span class="sxs-lookup"><span data-stu-id="e4874-207">When you share a keychain across your applications any application can delete users or worse delete all hello tokens across your application.</span></span> <span data-ttu-id="e4874-208">Jest to szczególnie Fatalne, jeśli masz aplikacje, które opierają się na powitania Praca w tle toodo tokenów.</span><span class="sxs-lookup"><span data-stu-id="e4874-208">This is particularly disastrous if you have applications that rely on hello tokens toodo background work.</span></span> <span data-ttu-id="e4874-209">Udostępnianie łańcucha kluczy oznacza, że należy zachować ostrożność bardzo w wszystkie Usuń operacji za pomocą zestawów SDK tożsamości Microsoft hello.</span><span class="sxs-lookup"><span data-stu-id="e4874-209">Sharing a keychain means that you must be very careful in any and all remove operations through hello Microsoft Identity SDKs.</span></span>
> 
> 

<span data-ttu-id="e4874-210">Gotowe.</span><span class="sxs-lookup"><span data-stu-id="e4874-210">That's it!</span></span> <span data-ttu-id="e4874-211">we wszystkich aplikacji Hello zestaw SDK programu Microsoft Identity teraz udostępniać poświadczeń.</span><span class="sxs-lookup"><span data-stu-id="e4874-211">hello Microsoft Identity SDK will now share credentials across all your applications.</span></span> <span data-ttu-id="e4874-212">Lista użytkowników Hello również zostaną udostępnione w wystąpieniach aplikacji.</span><span class="sxs-lookup"><span data-stu-id="e4874-212">hello user list will also be shared across application instances.</span></span>

### <a name="turning-on-sso-for-broker-assisted-sso"></a><span data-ttu-id="e4874-213">Włączanie logowania jednokrotnego dla brokera asystowaną pomocą rejestracji Jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="e4874-213">Turning on SSO for broker assisted SSO</span></span>
<span data-ttu-id="e4874-214">Witaj możliwość toouse aplikacji żadnych broker jest zainstalowana na urządzeniu hello jest **domyślnie wyłączone**.</span><span class="sxs-lookup"><span data-stu-id="e4874-214">hello ability for an application toouse any broker that is installed on hello device is **turned off by default**.</span></span> <span data-ttu-id="e4874-215">W celu toouse aplikacji z brokera hello należy wykonać pewne dodatkowe czynności konfiguracyjne i dodać niektórych aplikacji tooyour kodu.</span><span class="sxs-lookup"><span data-stu-id="e4874-215">In order toouse your application with hello broker you must do some additional configuration and add some code tooyour application.</span></span>

<span data-ttu-id="e4874-216">Witaj toofollow kroki są następujące:</span><span class="sxs-lookup"><span data-stu-id="e4874-216">hello steps toofollow are:</span></span>

1. <span data-ttu-id="e4874-217">Włącz tryb brokera w kodzie aplikacji toohello wywołania MS SDK.</span><span class="sxs-lookup"><span data-stu-id="e4874-217">Enable broker mode in your application code's call toohello MS SDK.</span></span>
2. <span data-ttu-id="e4874-218">Ustanów nowy identyfikator URI przekierowania i podaj, aplikacja hello tooboth i rejestracji aplikacji.</span><span class="sxs-lookup"><span data-stu-id="e4874-218">Establish a new redirect URI and provide that tooboth hello app and your app registration.</span></span>
3. <span data-ttu-id="e4874-219">Rejestrowanie schemat adresu URL.</span><span class="sxs-lookup"><span data-stu-id="e4874-219">Registering a URL Scheme.</span></span>
4. <span data-ttu-id="e4874-220">Obsługa iOS9: Dodaj plik info.plist tooyour uprawnienia.</span><span class="sxs-lookup"><span data-stu-id="e4874-220">iOS9 Support: Add a permission tooyour info.plist file.</span></span>

#### <a name="step-1-enable-broker-mode-in-your-application"></a><span data-ttu-id="e4874-221">Krok 1: Włącz broker tryb w aplikacji</span><span class="sxs-lookup"><span data-stu-id="e4874-221">Step 1: Enable broker mode in your application</span></span>
<span data-ttu-id="e4874-222">Hello możliwości dla twojej aplikacji toouse hello broker jest włączona, podczas tworzenia kontekstu"hello" lub początkowej konfiguracji obiektu uwierzytelniania.</span><span class="sxs-lookup"><span data-stu-id="e4874-222">hello ability for your application toouse hello broker is turned on when you create hello "context" or initial setup of your Authentication object.</span></span> <span data-ttu-id="e4874-223">Można to zrobić przez ustawienie danego typu poświadczeń w kodzie:</span><span class="sxs-lookup"><span data-stu-id="e4874-223">You do this by setting your credentials type in your code:</span></span>

```
/*! See hello ADCredentialsType enumeration definition for details */
@propertyADCredentialsType credentialsType;
```
<span data-ttu-id="e4874-224">Witaj `AD_CREDENTIALS_AUTO` ustawienie umożliwia toocall tootry tożsamości zestawu SDK usługi Microsoft hello limit brokera toohello `AD_CREDENTIALS_EMBEDDED` uniemożliwi wywoływania brokera toohello hello zestaw SDK programu Microsoft Identity.</span><span class="sxs-lookup"><span data-stu-id="e4874-224">hello `AD_CREDENTIALS_AUTO` setting will allow hello Microsoft Identity SDK tootry toocall out toohello broker, `AD_CREDENTIALS_EMBEDDED` will prevent hello Microsoft Identity SDK from calling toohello broker.</span></span>

#### <a name="step-2-registering-a-url-scheme"></a><span data-ttu-id="e4874-225">Krok 2: Zarejestrowanie schemat adresu URL</span><span class="sxs-lookup"><span data-stu-id="e4874-225">Step 2: Registering a URL Scheme</span></span>
<span data-ttu-id="e4874-226">Hello platformy pakietu Microsoft Identity używa brokera hello tooinvoke adresy URL i następnie zwracany sterowania tooyour Wstecz.</span><span class="sxs-lookup"><span data-stu-id="e4874-226">hello Microsoft Identity platform uses URLs tooinvoke hello broker and then return control back tooyour application.</span></span> <span data-ttu-id="e4874-227">toofinish tego obiegu należy schemat adresu URL zarejestrowane dla aplikacji tego pakietu Microsoft Identity platformy będzie wiedzieć o hello.</span><span class="sxs-lookup"><span data-stu-id="e4874-227">toofinish that round trip you need a URL scheme registered for your application that hello Microsoft Identity platform will know about.</span></span> <span data-ttu-id="e4874-228">To może być także tooany innych systemów aplikacji może zostały wcześniej zarejestrowane z aplikacją.</span><span class="sxs-lookup"><span data-stu-id="e4874-228">This can be in addition tooany other app schemes you may have previously registered with your application.</span></span>

> [!WARNING]
> <span data-ttu-id="e4874-229">Zalecamy utworzenie hello adresu URL schemat dość unikatowy toominimize hello szanse innej aplikacji przy użyciu hello sam schemat adresu URL.</span><span class="sxs-lookup"><span data-stu-id="e4874-229">We recommend making hello URL scheme fairly unique toominimize hello chances of another app using hello same URL scheme.</span></span> <span data-ttu-id="e4874-230">Apple wymuszać unikatowość hello Schematy adresów URL, które są zarejestrowane w magazynie aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="e4874-230">Apple does not enforce hello uniqueness of URL schemes that are registered in hello app store.</span></span>
> 
> 

<span data-ttu-id="e4874-231">Poniżej przedstawiono przykład sposobu wyświetlania w konfiguracji projektu.</span><span class="sxs-lookup"><span data-stu-id="e4874-231">Below is an example of how this appears in your project configuration.</span></span> <span data-ttu-id="e4874-232">Można również wykonać to w środowisku XCode również:</span><span class="sxs-lookup"><span data-stu-id="e4874-232">You may also do this in XCode as well:</span></span>

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

#### <a name="step-3-establish-a-new-redirect-uri-with-your-url-scheme"></a><span data-ttu-id="e4874-233">Krok 3: Ustalanie przekierowania nowy identyfikator URI ze schematem adresu URL</span><span class="sxs-lookup"><span data-stu-id="e4874-233">Step 3: Establish a new redirect URI with your URL Scheme</span></span>
<span data-ttu-id="e4874-234">W kolejności tooensure, że firma Microsoft zawsze zwracać poświadczeń hello tokeny toohello właściwej aplikacji potrzebujemy toomake się, że firma Microsoft wywołania zwrotnego, że tooyour aplikacji w taki sposób, aby hello wersja systemu operacyjnego można sprawdzić.</span><span class="sxs-lookup"><span data-stu-id="e4874-234">In order tooensure that we always return hello credential tokens toohello correct application, we need toomake sure we call back tooyour application in a way that hello iOS operating system can verify.</span></span> <span data-ttu-id="e4874-235">aplikacje brokera Microsoft Hello iOS systemu operacyjnego raporty toohello hello identyfikator pakietu aplikacji hello wywoływania go.</span><span class="sxs-lookup"><span data-stu-id="e4874-235">hello iOS operating system reports toohello Microsoft broker applications hello Bundle ID of hello application calling it.</span></span> <span data-ttu-id="e4874-236">To nie może być sfałszowane przez nieautoryzowanej aplikacji.</span><span class="sxs-lookup"><span data-stu-id="e4874-236">This cannot be spoofed by a rogue application.</span></span> <span data-ttu-id="e4874-237">W związku z tym możemy wykorzystać to wraz z hello URI naszych tooensure aplikacji brokera, że tokeny hello są zwracane toohello właściwej aplikacji.</span><span class="sxs-lookup"><span data-stu-id="e4874-237">Therefore, we leverage this along with hello URI of our broker application tooensure that hello tokens are returned toohello correct application.</span></span> <span data-ttu-id="e4874-238">Wymagamy możesz tooestablish przekierowanie Unikatowy identyfikator URI, zarówno w aplikacji i Ustaw jako identyfikator URI przekierowania w portalu deweloperów.</span><span class="sxs-lookup"><span data-stu-id="e4874-238">We require you tooestablish this unique redirect URI both in your application and set as a Redirect URI in our developer portal.</span></span>

<span data-ttu-id="e4874-239">Identyfikator URI przekierowania musi być w formie prawidłowego hello:</span><span class="sxs-lookup"><span data-stu-id="e4874-239">Your redirect URI must be in hello proper form of:</span></span>

`<app-scheme>://<your.bundle.id>`

<span data-ttu-id="e4874-240">przykład: *x-msauth-mytestiosapp://com.myapp.mytestapp*</span><span class="sxs-lookup"><span data-stu-id="e4874-240">ex: *x-msauth-mytestiosapp://com.myapp.mytestapp*</span></span>

<span data-ttu-id="e4874-241">Ten identyfikator URI przekierowania musi toobe określone w Twojej rejestracji aplikacji przy użyciu hello [portalu Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="e4874-241">This Redirect URI needs toobe specified in your app registration using hello [Azure portal](https://portal.azure.com/).</span></span> <span data-ttu-id="e4874-242">Aby uzyskać więcej informacji dotyczących rejestracji aplikacji usługi Azure AD, zobacz [integracji z usługą Azure Active Directory](active-directory-how-to-integrate.md).</span><span class="sxs-lookup"><span data-stu-id="e4874-242">For more information on Azure AD app registration, see [Integrating with Azure Active Directory](active-directory-how-to-integrate.md).</span></span>

##### <a name="step-3a-add-a-redirect-uri-in-your-app-and-dev-portal-toosupport-certificate-based-authentication"></a><span data-ttu-id="e4874-243">Krok 3a: Dodaj identyfikator URI przekierowania w przypadku uwierzytelniania opartego na certyfikatach toosupport portalu deweloperów i aplikacji</span><span class="sxs-lookup"><span data-stu-id="e4874-243">Step 3a: Add a redirect URI in your app and dev portal toosupport certificate based authentication</span></span>
<span data-ttu-id="e4874-244">uwierzytelnianie certyfikatu na podstawie toosupport drugi "msauth" wymaga toobe zarejestrowany w aplikacji i hello [portalu Azure](https://portal.azure.com/) toohandle uwierzytelnianie certyfikatu, jeśli chcesz, aby tooadd, które obsługują w aplikacji.</span><span class="sxs-lookup"><span data-stu-id="e4874-244">toosupport cert based authentication a second "msauth"  needs toobe registered in your application and hello [Azure portal](https://portal.azure.com/) toohandle certificate authentication if you wish tooadd that support in your application.</span></span>

`msauth://code/<broker-redirect-uri-in-url-encoded-form>`

<span data-ttu-id="e4874-245">przykład: *msauth://code/x-msauth-mytestiosapp%3A%2F%2Fcom.myapp.mytestapp*</span><span class="sxs-lookup"><span data-stu-id="e4874-245">ex: *msauth://code/x-msauth-mytestiosapp%3A%2F%2Fcom.myapp.mytestapp*</span></span>

#### <a name="step-4-ios9-add-a-configuration-parameter-tooyour-app"></a><span data-ttu-id="e4874-246">Krok 4: iOS9: Dodaj aplikację tooyour parametru konfiguracji</span><span class="sxs-lookup"><span data-stu-id="e4874-246">Step 4: iOS9: Add a configuration parameter tooyour app</span></span>
<span data-ttu-id="e4874-247">— CanOpenURL używa biblioteki ADAL: toocheck Jeśli brokera hello jest zainstalowany na urządzeniu hello.</span><span class="sxs-lookup"><span data-stu-id="e4874-247">ADAL uses –canOpenURL: toocheck if hello broker is installed on hello device.</span></span> <span data-ttu-id="e4874-248">W systemie iOS 9 Apple zablokowany co można wyszukać schematy aplikacji.</span><span class="sxs-lookup"><span data-stu-id="e4874-248">In iOS 9 Apple locked down what schemes an application can query for.</span></span> <span data-ttu-id="e4874-249">Konieczne będzie tooadd "msauth" toohello LSApplicationQueriesSchemes części Twojego `info.plist file`.</span><span class="sxs-lookup"><span data-stu-id="e4874-249">You will need tooadd “msauth” toohello LSApplicationQueriesSchemes section of your `info.plist file`.</span></span>

<span data-ttu-id="e4874-250"><key>LSApplicationQueriesSchemes</key></span><span class="sxs-lookup"><span data-stu-id="e4874-250"><key>LSApplicationQueriesSchemes</key></span></span>

<span data-ttu-id="e4874-251"><array><string>msauth</string>
</array></span><span class="sxs-lookup"><span data-stu-id="e4874-251"><array> <string>msauth</string>
</array></span></span>

### <a name="youve-configured-sso"></a><span data-ttu-id="e4874-252">Skonfigurowaniu logowania jednokrotnego!</span><span class="sxs-lookup"><span data-stu-id="e4874-252">You've configured SSO!</span></span>
<span data-ttu-id="e4874-253">Teraz hello zestaw SDK programu Microsoft Identity automatycznie zarówno udostępnianie poświadczeń w aplikacji i wywołać hello brokera, jeśli jest obecny na urządzeniu.</span><span class="sxs-lookup"><span data-stu-id="e4874-253">Now hello Microsoft Identity SDK will automatically both share credentials across your applications and invoke hello broker if it's present on their device.</span></span>

