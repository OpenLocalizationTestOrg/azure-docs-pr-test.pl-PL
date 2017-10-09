---
title: "tooget aaaHow AppSource certyfikowane dla usługi Azure Active Directory | Dokumentacja firmy Microsoft"
description: "Szczegółowe informacje o sposobie tooget aplikacji AppSource certyfikowane dla usługi Azure Active Directory."
services: active-directory
documentationcenter: 
author: andretms
manager: mbaldwin
editor: 
ms.assetid: 21206407-49f8-4c0b-84d1-c25e17cd4183
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 08/03/2017
ms.author: andret
ms.custom: aaddev
ms.openlocfilehash: e9f07e9220afcba1120b987122fe770fe5225eed
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooget-appsource-certified-for-azure-active-directory"></a><span data-ttu-id="f011e-103">W jaki sposób tooget AppSource certyfikowane dla usługi Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="f011e-103">How tooget AppSource Certified for Azure Active Directory</span></span>
<span data-ttu-id="f011e-104">[Microsoft AppSource](https://appsource.microsoft.com/) jest miejsce docelowe dla firm użytkowników toodiscover, spróbuj, aplikacji i zarządzanie nimi z biznesowych SaaS (produktów Microsoft SaaS autonomiczny SaaS i dodatek tooexisting).</span><span class="sxs-lookup"><span data-stu-id="f011e-104">[Microsoft AppSource](https://appsource.microsoft.com/) is a destination for business users toodiscover, try, and manage line-of-business SaaS applications (standalone SaaS and add-on tooexisting Microsoft SaaS products).</span></span>

<span data-ttu-id="f011e-105">toolist autonomicznej aplikacji SaaS na AppSource, aplikacja musi akceptować rejestracji jednokrotnej z konta służbowego z firmy lub organizacji, która ma usługę Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="f011e-105">toolist a standalone SaaS application on AppSource, your application must accept single sign-on from work accounts from any company or organization that has Azure Active Directory.</span></span> <span data-ttu-id="f011e-106">Witaj procesu logowania, należy użyć hello [OpenID Connect](./active-directory-protocols-openid-connect-code.md) lub [OAuth 2.0](./active-directory-protocols-oauth-code.md) protokołów.</span><span class="sxs-lookup"><span data-stu-id="f011e-106">hello sign-in process must use hello [OpenID Connect](./active-directory-protocols-openid-connect-code.md) or [OAuth 2.0](./active-directory-protocols-oauth-code.md) protocols.</span></span> <span data-ttu-id="f011e-107">Integrację SAML nie jest akceptowane AppSource certyfikacji.</span><span class="sxs-lookup"><span data-stu-id="f011e-107">SAML integration is not accepted for AppSource certification.</span></span>

## <a name="guides-and-code-samples"></a><span data-ttu-id="f011e-108">Wskazówek i przykładów kodu</span><span class="sxs-lookup"><span data-stu-id="f011e-108">Guides and code samples</span></span>
<span data-ttu-id="f011e-109">Jeśli chcesz toolearn o jak toointegrate aplikacji w usłudze Azure Active Directory za pomocą Identyfikatora otwarte połączenia, wykonaj nasze wskazówki i przykłady w hello kodu [przewodnik dewelopera usługi Azure Active Directory](./active-directory-developers-guide.md#get-started "wprowadzenie Azure AD dla deweloperów").</span><span class="sxs-lookup"><span data-stu-id="f011e-109">If you want toolearn about how toointegrate your application with Azure Active Directory using Open ID connect, follow our guides and code samples in hello [Azure Active Directory developer's guide](./active-directory-developers-guide.md#get-started "Get Started with Azure AD for developers").</span></span>

## <a name="multi-tenant-applications"></a><span data-ttu-id="f011e-110">Aplikacje wielodostępne</span><span class="sxs-lookup"><span data-stu-id="f011e-110">Multi-tenant applications</span></span>

<span data-ttu-id="f011e-111">Aplikacja, która akceptuje logowania użytkowników z firmy lub organizacji mających usługi Azure Active Directory bez konieczności oddzielnego wystąpienia, konfiguracji lub wdrożenia jest znany jako *wielodostępnych aplikacji*.</span><span class="sxs-lookup"><span data-stu-id="f011e-111">An application that accepts sign-ins from users from any company or organization that have Azure Active Directory without requiring a separate instance, configuration, or deployment is known as a *multi-tenant application*.</span></span> <span data-ttu-id="f011e-112">AppSource zaleca się, że aplikacje wdrożyć hello tooenable wielodostępność *jednym kliknięciem* wolne środowisko wersji próbnej.</span><span class="sxs-lookup"><span data-stu-id="f011e-112">AppSource recommends that applications implement multi-tenancy tooenable hello *single-click* free trial experience.</span></span>

<span data-ttu-id="f011e-113">W kolejności tooenable wielu dzierżawców w swojej aplikacji:</span><span class="sxs-lookup"><span data-stu-id="f011e-113">In order tooenable multi-tenancy on your application:</span></span>
- <span data-ttu-id="f011e-114">Ustaw `Multi-Tenanted` właściwości zbyt`Yes` na informacje o rejestracji aplikacji w hello [Azure Portal](https://portal.azure.com/#blade/Microsoft_AAD_IAM/ActiveDirectoryMenuBlade/RegisteredApps) (domyślnie aplikacje utworzone w portalu Azure hello są skonfigurowane jako *pojedynczego dzierżawcy*)</span><span class="sxs-lookup"><span data-stu-id="f011e-114">Set `Multi-Tenanted` property too`Yes` on your application registration's information in hello [Azure Portal](https://portal.azure.com/#blade/Microsoft_AAD_IAM/ActiveDirectoryMenuBlade/RegisteredApps) (by default, applications created in hello Azure Portal are configured as *single-tenant*)</span></span>
- <span data-ttu-id="f011e-115">Aktualizacja Twojego toohello żądań toosend kodu '`common`"punktu końcowego (zaktualizować punktu końcowego hello z *https://login.microsoftonline.com/ {yourtenant}* za*https://login.microsoftonline.com/common*)</span><span class="sxs-lookup"><span data-stu-id="f011e-115">Update your code toosend requests toohello '`common`' endpoint (update hello endpoint from *https://login.microsoftonline.com/{yourtenant}* too*https://login.microsoftonline.com/common*)</span></span>
- <span data-ttu-id="f011e-116">Dla niektórych platform, takich jak ASP.NET, należy również tooupdate Twojego tooaccept kodu wielu wystawców</span><span class="sxs-lookup"><span data-stu-id="f011e-116">For some platforms, like ASP.NET, you need also tooupdate your code tooaccept multiple issuers</span></span>

<span data-ttu-id="f011e-117">Aby uzyskać więcej informacji na temat obsługi wielu dzierżawców, zobacz: [jak toosign w dowolnej usługi Azure Active Directory (AD) użytkownika za pomocą hello wzorzec wielodostępnych aplikacji](./active-directory-devhowto-multi-tenant-overview.md).</span><span class="sxs-lookup"><span data-stu-id="f011e-117">For more information about multi-tenancy, see: [How toosign in any Azure Active Directory (AD) user using hello multi-tenant application pattern](./active-directory-devhowto-multi-tenant-overview.md).</span></span>

### <a name="single-tenant-applications"></a><span data-ttu-id="f011e-118">Aplikacje pojedynczej dzierżawy</span><span class="sxs-lookup"><span data-stu-id="f011e-118">Single-tenant applications</span></span>
<span data-ttu-id="f011e-119">Aplikacje, które akceptują tylko logowania użytkowników zdefiniowanych wystąpienia usługi Azure Active Directory są określane jako *aplikacji pojedynczej dzierżawy*.</span><span class="sxs-lookup"><span data-stu-id="f011e-119">Applications that only accept sign-ins from users of a defined Azure Active Directory instance are known as *single-tenant application*.</span></span> <span data-ttu-id="f011e-120">Użytkownicy zewnętrzni (łącznie z konta służbowego z innych organizacji lub osobiste konto) można zalogować tooa pojedynczej dzierżawy aplikacji po dodaniu każdego użytkownika jako *konta gościa* wystąpienie toohello usługi Azure Active Directory Aplikacja Hello jest zarejestrowana.</span><span class="sxs-lookup"><span data-stu-id="f011e-120">External users (including Work or School accounts from other organizations, or personal account) can sign in tooa single-tenant application after adding each user as *guest account* toohello Azure Active Directory instance that hello application is registered.</span></span> <span data-ttu-id="f011e-121">Możesz dodać użytkowników jako gość tooan kont usługi Azure Active Directory za pośrednictwem hello [ *współpracy B2B usługi Azure AD* ](../active-directory-b2b-what-is-azure-ad-b2b.md) - i mogą to robić [programowo](../active-directory-b2b-code-samples.md).</span><span class="sxs-lookup"><span data-stu-id="f011e-121">You can add users as guest accounts tooan Azure Active Directory via hello [*Azure AD B2B collaboration*](../active-directory-b2b-what-is-azure-ad-b2b.md) - and it can be done [programatically](../active-directory-b2b-code-samples.md).</span></span> <span data-ttu-id="f011e-122">Gdy użytkownik zostanie dodany jako gość tooan konta usługi Azure Active Directory, wiadomość e-mail z zaproszeniem są wysyłane toohello użytkownik, który ma tooaccept hello zaproszenia, klikając łącze hello w hello wiadomość e-mail z zaproszeniem.</span><span class="sxs-lookup"><span data-stu-id="f011e-122">When you add a user as guest account tooan Azure Active Directory, an invitation email is sent toohello user, who has tooaccept hello invitation by clicking on hello link in hello invitation email.</span></span> <span data-ttu-id="f011e-123">Zaproszeń do skorzystania z wysyłanych użytkownika dodatkowe tooan zaproszenia organizacji, która jest również członkiem organizacji partnerskiej hello są tooaccept nie jest wymagane toosign zaproszenia w.</span><span class="sxs-lookup"><span data-stu-id="f011e-123">Invitations that are sent tooan additional user in an inviting organization that is also a member of hello partner organization are not required tooaccept an invitation toosign in.</span></span>

<span data-ttu-id="f011e-124">Aplikacje pojedynczego dzierżawcy można włączyć hello *kontaktu mnie* środowisko, ale tooenable hello jednym kliknięciem / bezpłatnej wersji próbnej środowisko, które zaleca AppSource, należy włączyć wielodostępność na aplikacji zamiast tego.</span><span class="sxs-lookup"><span data-stu-id="f011e-124">Single-tenant applications can enable hello *Contact Me* experience, but if you want tooenable hello single-click/ free trial experience that AppSource recommends, enable multi-tenancy on your application instead.</span></span>


## <a name="appsource-trial-experiences"></a><span data-ttu-id="f011e-125">Napotyka AppSource wersji próbnej</span><span class="sxs-lookup"><span data-stu-id="f011e-125">AppSource trial experiences</span></span>

### <a name="free-trial-customer-led-trial-experience"></a><span data-ttu-id="f011e-126">Bezpłatna wersja próbna (środowisko wersji próbnej doprowadziły klienta)</span><span class="sxs-lookup"><span data-stu-id="f011e-126">Free Trial (Customer-led trial experience)</span></span> 
<span data-ttu-id="f011e-127">Witaj *doprowadziły klienta wersji próbnej* to środowisko hello, które AppSource zaleca jak oferuje aplikacji tooyour dostępu jednym kliknięciem.</span><span class="sxs-lookup"><span data-stu-id="f011e-127">hello *customer-led trial* is hello experience that AppSource recommends as it offers a single-click access tooyour application.</span></span> <span data-ttu-id="f011e-128">Poniżej w jaki sposób to środowisko wygląda następująco:</span><span class="sxs-lookup"><span data-stu-id="f011e-128">Below an illustration of how this experience looks like:</span></span><br/><br/>

<table >
<tr>
    <td valign="top" width="33%">1.<br/><img src="media/active-directory-devhowto-appsource-certified/customer-led-trial-step1.png" width="85%"/><ul><li><span data-ttu-id="f011e-129">Użytkownik wyszukuje aplikacji w witrynie sieci Web AppSource</span><span class="sxs-lookup"><span data-stu-id="f011e-129">User finds your application in AppSource Web Site</span></span></li><li><span data-ttu-id="f011e-130">Wybiera opcję "Bezpłatnej wersji próbnej"</span><span class="sxs-lookup"><span data-stu-id="f011e-130">Selects ‘Free trial’ option</span></span></li></ul></td>
    <td valign="top" width="33%">2.<br/><img src="media/active-directory-devhowto-appsource-certified/customer-led-trial-step2.png" width="85%" /><ul><li><span data-ttu-id="f011e-131">AppSource przekierowuje użytkownika tooa adres URL witryny sieci web</span><span class="sxs-lookup"><span data-stu-id="f011e-131">AppSource redirects user tooa URL in your web site</span></span></li><li><span data-ttu-id="f011e-132">Witryny sieci web uruchamia hello <i>single-sign-on</i> proces automatycznie (ładowania strony)</span><span class="sxs-lookup"><span data-stu-id="f011e-132">Your web site starts hello <i>single-sign-on</i> process automatically (on page load)</span></span></li></ul></td>
    <td valign="top" width="33%">3.<br/><img src="media/active-directory-devhowto-appsource-certified/customer-led-trial-step3.png" width="85%"/><ul><li><span data-ttu-id="f011e-133">Użytkownik jest strona przekierowywania tooMicrosoft logowania</span><span class="sxs-lookup"><span data-stu-id="f011e-133">User is redirected tooMicrosoft Sign-in page</span></span></li><li><span data-ttu-id="f011e-134">Użytkownik podaje toosign poświadczeń w</span><span class="sxs-lookup"><span data-stu-id="f011e-134">User provides credentials toosign in</span></span></li></ul></td>
</tr>
<tr>
    <td valign="top" width="33%">4.<br/><img src="media/active-directory-devhowto-appsource-certified/customer-led-trial-step4.png" width="85%"/><ul><li><span data-ttu-id="f011e-135">Użytkownik wyrazi zgodę dla aplikacji</span><span class="sxs-lookup"><span data-stu-id="f011e-135">User gives consent for your application</span></span></li></ul></td>
    <td valign="top" width="33%">5.<br/><img src="media/active-directory-devhowto-appsource-certified/customer-led-trial-step5.png" width="85%"/><ul><li><span data-ttu-id="f011e-136">Logowanie kończy i użytkownik jest przekierowane tooyour wstecz witryny sieci web</span><span class="sxs-lookup"><span data-stu-id="f011e-136">Sign-in completes and user is redirected back tooyour web site</span></span></li><li><span data-ttu-id="f011e-137">Użytkownik uruchamia hello bezpłatnej wersji próbnej</span><span class="sxs-lookup"><span data-stu-id="f011e-137">User starts hello free trial</span></span></li></ul></td>
    <td></td>
</tr>
</table>

### <a name="contact-me-partner-led-trial-experience"></a><span data-ttu-id="f011e-138">Skontaktować się ze mną (doprowadziły partnera środowisko wersji próbnej)</span><span class="sxs-lookup"><span data-stu-id="f011e-138">Contact Me (Partner-led trial experience)</span></span>
<span data-ttu-id="f011e-139">Witaj *partnera środowisko wersji próbnej* można użyć w przypadku ręcznego lub długoterminowej operacja wymaga toohappen tooprovision hello użytkownika / firmę: na przykład, aplikacja musi tooprovision maszyn wirtualnych, wystąpień bazy danych lub operacje, które przyjmują toocomplete dużo czasu.</span><span class="sxs-lookup"><span data-stu-id="f011e-139">hello *partner trial experience* can be used when a manual or a long-term operation needs toohappen tooprovision hello user/ company: for example, your application needs tooprovision virtual machines, database instances, or operations that take much time toocomplete.</span></span> <span data-ttu-id="f011e-140">W takim przypadku po użytkownik wybiera hello *"Żądania wersji próbnej"* przycisk i wypełnia formularz, AppSource wysyła hello informacje kontaktowe użytkownika.</span><span class="sxs-lookup"><span data-stu-id="f011e-140">In this case, after user selects hello *'Request Trial'* button and fills out a form, AppSource sends you hello user's contact information.</span></span> <span data-ttu-id="f011e-141">Po otrzymaniu tych informacji, następnie udostępnić hello środowiska i wysłać hello instrukcje toohello użytkownika, w jaki sposób tooaccess hello środowisko wersji próbnej:</span><span class="sxs-lookup"><span data-stu-id="f011e-141">Upon receiving this information, you then provision hello environment and send hello instructions toohello user on how tooaccess hello trial experience:</span></span><br/><br/>

<table valign="top">
<tr>
    <td valign="top" width="33%">1.<br/><img src="media/active-directory-devhowto-appsource-certified/partner-led-trial-step1.png" width="85%"/><ul><li><span data-ttu-id="f011e-142">Użytkownik wyszukuje aplikacji w witrynie sieci web AppSource</span><span class="sxs-lookup"><span data-stu-id="f011e-142">User finds your application in AppSource web site</span></span></li><li><span data-ttu-id="f011e-143">Wybiera opcję "Skontaktuj się z Me"</span><span class="sxs-lookup"><span data-stu-id="f011e-143">Selects ‘Contact Me’ option</span></span></li></ul></td>
    <td valign="top" width="33%">2.<br/><img src="media/active-directory-devhowto-appsource-certified/partner-led-trial-step2.png" width="85%"/><ul><li><span data-ttu-id="f011e-144">Wypełnia formularz informacje kontaktowe</span><span class="sxs-lookup"><span data-stu-id="f011e-144">Fills out a form with contact information</span></span></li></ul></td>
     <td valign="top" width="33%">3.<br/><br/>
        <table bgcolor="#f7f7f7">
        <tr>
            <td><img src="media/active-directory-devhowto-appsource-certified/UserContact.png" width="55%"/></td>
            <td><span data-ttu-id="f011e-145">Odbieranie informacji o użytkowniku</span><span class="sxs-lookup"><span data-stu-id="f011e-145">You receive user information</span></span></td>
        </tr>
        <tr>
            <td><img src="media/active-directory-devhowto-appsource-certified/SetupEnv.png" width="55%"/></td>
            <td><span data-ttu-id="f011e-146">Konfigurowanie środowiska</span><span class="sxs-lookup"><span data-stu-id="f011e-146">Setup environment</span></span></td>
        </tr>
        <tr>
            <td><img src="media/active-directory-devhowto-appsource-certified/ContactCustomer.png" width="55%"/></td>
            <td><span data-ttu-id="f011e-147">Skontaktuj się z użytkownikiem z informacjami o wersji próbnej</span><span class="sxs-lookup"><span data-stu-id="f011e-147">Contact user with trial info</span></span></td>
        </tr>
        </table><br/><br/>
        <ul><li><span data-ttu-id="f011e-148">Odbieranie informacji i wersji próbnej wystąpienia ustawienia użytkownika</span><span class="sxs-lookup"><span data-stu-id="f011e-148">You receive user's information and setup trial instance</span></span></li><li><span data-ttu-id="f011e-149">Wyślij hello hyperlink tooaccess użytkownika toohello aplikacji</span><span class="sxs-lookup"><span data-stu-id="f011e-149">You send hello hyperlink tooaccess your application toohello user</span></span></li></ul>
    </td>
</tr>
<tr>
    <td valign="top" width="33%">4.<br/><img src="media/active-directory-devhowto-appsource-certified/partner-led-trial-step3.png" width="85%"/><ul><li><span data-ttu-id="f011e-150">Użytkownik uzyskuje dostęp do aplikacji i pełne hello single-sign-on procesu</span><span class="sxs-lookup"><span data-stu-id="f011e-150">User accesses your application and complete hello single-sign-on process</span></span></li></ul></td>
    <td valign="top" width="33%">5.<br/><img src="media/active-directory-devhowto-appsource-certified/partner-led-trial-step4.png" width="85%"/><ul><li><span data-ttu-id="f011e-151">Użytkownik wyrazi zgodę dla aplikacji</span><span class="sxs-lookup"><span data-stu-id="f011e-151">User gives consent for your application</span></span></li></ul></td>
    <td valign="top" width="33%">6.<br/><img src="media/active-directory-devhowto-appsource-certified/customer-led-trial-step5.png" width="85%"/><ul><li><span data-ttu-id="f011e-152">Logowanie kończy i użytkownik jest przekierowane tooyour wstecz witryny sieci web</span><span class="sxs-lookup"><span data-stu-id="f011e-152">Sign-in completes and user is redirected back tooyour web site</span></span></li><li><span data-ttu-id="f011e-153">Użytkownik uruchamia hello bezpłatnej wersji próbnej</span><span class="sxs-lookup"><span data-stu-id="f011e-153">User starts hello free trial</span></span></li></ul></td>
   
</tr>
</table>

### <a name="more-information"></a><span data-ttu-id="f011e-154">Więcej informacji</span><span class="sxs-lookup"><span data-stu-id="f011e-154">More information</span></span>
<span data-ttu-id="f011e-155">Aby uzyskać więcej informacji na temat środowisko wersji próbnej AppSource hello zobacz [ten film](https://aka.ms/trialexperienceforwebapps).</span><span class="sxs-lookup"><span data-stu-id="f011e-155">For more information about hello AppSource trial experience, see [this video](https://aka.ms/trialexperienceforwebapps).</span></span> 
 
## <a name="next-steps"></a><span data-ttu-id="f011e-156">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="f011e-156">Next Steps</span></span>

- <span data-ttu-id="f011e-157">Aby uzyskać więcej informacji dotyczących tworzenia aplikacji, które obsługują usługi Azure Active Directory logowania, zobacz [scenariusze uwierzytelniania dla usługi Azure AD](https://docs.microsoft.com/azure/active-directory/develop/active-directory-authentication-scenarios)</span><span class="sxs-lookup"><span data-stu-id="f011e-157">For more information on building applications that support Azure Active Directory sign-ins, see [Authentication Scenarios for Azure AD](https://docs.microsoft.com/azure/active-directory/develop/active-directory-authentication-scenarios)</span></span> 

- <span data-ttu-id="f011e-158">Aby uzyskać informacje dotyczące sposobu toolist aplikacji SaaS w AppSource, zobacz [informacje o partnerze AppSource](https://appsource.microsoft.com/partners)</span><span class="sxs-lookup"><span data-stu-id="f011e-158">For information on how toolist your SaaS application in AppSource, go see [AppSource Partner Information](https://appsource.microsoft.com/partners)</span></span>


## <a name="get-support"></a><span data-ttu-id="f011e-159">Uzyskaj pomoc techniczną</span><span class="sxs-lookup"><span data-stu-id="f011e-159">Get Support</span></span>
<span data-ttu-id="f011e-160">Integracja usługi Azure Active Directory, używamy [przepełnienie stosu](http://stackoverflow.com/questions/tagged/azure-active-directory) z obsługą tooprovide społeczności hello.</span><span class="sxs-lookup"><span data-stu-id="f011e-160">For Azure Active Directory integration, we use [Stack Overflow](http://stackoverflow.com/questions/tagged/azure-active-directory) with hello community tooprovide support.</span></span> 

<span data-ttu-id="f011e-161">Zdecydowanie zaleca się najpierw zadać pytania w witrynie Stack Overflow i Przeglądaj istniejących toosee problemów, jeśli ktoś poprosił pytanie przed.</span><span class="sxs-lookup"><span data-stu-id="f011e-161">We highly recommend you ask your questions on Stack Overflow first and browse existing issues toosee if someone has asked your question before.</span></span> <span data-ttu-id="f011e-162">Upewnij się, że pytania lub komentarze są oznaczane `[azure-active-directory]`.</span><span class="sxs-lookup"><span data-stu-id="f011e-162">Make sure that your questions or comments are tagged with `[azure-active-directory]`.</span></span>

<span data-ttu-id="f011e-163">Użyj powitania po opinii tooprovide sekcji komentarzy i pomóc nam dostosować i kształtu zawartość.</span><span class="sxs-lookup"><span data-stu-id="f011e-163">Use hello following comments section tooprovide feedback and help us refine and shape our content.</span></span>

<!--Reference style links -->
[AAD-Auth-Scenarios]: ./active-directory-authentication-scenarios.md
[AAD-Auth-Scenarios-Browser-To-WebApp]: ./active-directory-authentication-scenarios.md#web-browser-to-web-application
[AAD-Dev-Guide]: ./active-directory-developers-guide.md
[AAD-Howto-Multitenant-Overview]: ./active-directory-devhowto-multi-tenant-overview.md
[AAD-QuickStart-Web-Apps]: ./active-directory-developers-guide.md#get-started


<!--Image references-->