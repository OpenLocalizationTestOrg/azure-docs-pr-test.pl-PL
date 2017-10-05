---
title: "Jak uzyskać AppSource certyfikowane dla usługi Azure Active Directory | Dokumentacja firmy Microsoft"
description: "Więcej informacji na temat aplikacji AppSource certyfikowane dla usługi Azure Active Directory."
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
ms.openlocfilehash: d8e2f8fc19ff879e6a7b632f033fd0ed9d77392a
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/18/2017
---
# <a name="how-to-get-appsource-certified-for-azure-active-directory"></a><span data-ttu-id="95f1f-103">Jak uzyskać AppSource certyfikowane dla usługi Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="95f1f-103">How to get AppSource Certified for Azure Active Directory</span></span>
<span data-ttu-id="95f1f-104">[Microsoft AppSource](https://appsource.microsoft.com/) jest docelowy dla użytkowników biznesowych wykrywanie, spróbuj i zarządzanie nimi z biznesowych aplikacji SaaS (SaaS, jak i dodatku do istniejących produktów Microsoft SaaS).</span><span class="sxs-lookup"><span data-stu-id="95f1f-104">[Microsoft AppSource](https://appsource.microsoft.com/) is a destination for business users to discover, try, and manage line-of-business SaaS applications (standalone SaaS and add-on to existing Microsoft SaaS products).</span></span>

<span data-ttu-id="95f1f-105">Aby wyświetlić listę autonomicznym aplikacji SaaS na AppSource, aplikacja musi akceptować rejestracji jednokrotnej z konta służbowego z firmy lub organizacji, która ma usługę Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="95f1f-105">To list a standalone SaaS application on AppSource, your application must accept single sign-on from work accounts from any company or organization that has Azure Active Directory.</span></span> <span data-ttu-id="95f1f-106">Proces logowania, należy użyć [OpenID Connect](./active-directory-protocols-openid-connect-code.md) lub [OAuth 2.0](./active-directory-protocols-oauth-code.md) protokołów.</span><span class="sxs-lookup"><span data-stu-id="95f1f-106">The sign-in process must use the [OpenID Connect](./active-directory-protocols-openid-connect-code.md) or [OAuth 2.0](./active-directory-protocols-oauth-code.md) protocols.</span></span> <span data-ttu-id="95f1f-107">Integrację SAML nie jest akceptowane AppSource certyfikacji.</span><span class="sxs-lookup"><span data-stu-id="95f1f-107">SAML integration is not accepted for AppSource certification.</span></span>

## <a name="guides-and-code-samples"></a><span data-ttu-id="95f1f-108">Wskazówek i przykładów kodu</span><span class="sxs-lookup"><span data-stu-id="95f1f-108">Guides and code samples</span></span>
<span data-ttu-id="95f1f-109">Jeśli chcesz dowiedzieć się więcej o integracji aplikacji w usłudze Azure Active Directory za pomocą Identyfikatora otwarte połączenie, wykonaj nasze wskazówki i kodu próbek w [przewodnik dewelopera usługi Azure Active Directory](./active-directory-developers-guide.md#get-started "Rozpoczynanie pracy z usługą Azure AD dla deweloperów").</span><span class="sxs-lookup"><span data-stu-id="95f1f-109">If you want to learn about how to integrate your application with Azure Active Directory using Open ID connect, follow our guides and code samples in the [Azure Active Directory developer's guide](./active-directory-developers-guide.md#get-started "Get Started with Azure AD for developers").</span></span>

## <a name="multi-tenant-applications"></a><span data-ttu-id="95f1f-110">Aplikacje wielodostępne</span><span class="sxs-lookup"><span data-stu-id="95f1f-110">Multi-tenant applications</span></span>

<span data-ttu-id="95f1f-111">Aplikacja, która akceptuje logowania użytkowników z firmy lub organizacji mających usługi Azure Active Directory bez konieczności oddzielnego wystąpienia, konfiguracji lub wdrożenia jest znany jako *wielodostępnych aplikacji*.</span><span class="sxs-lookup"><span data-stu-id="95f1f-111">An application that accepts sign-ins from users from any company or organization that have Azure Active Directory without requiring a separate instance, configuration, or deployment is known as a *multi-tenant application*.</span></span> <span data-ttu-id="95f1f-112">AppSource zaleca się, że aplikacje wdrożyć wielodostępność, aby włączyć *jednym kliknięciem* wolne środowisko wersji próbnej.</span><span class="sxs-lookup"><span data-stu-id="95f1f-112">AppSource recommends that applications implement multi-tenancy to enable the *single-click* free trial experience.</span></span>

<span data-ttu-id="95f1f-113">Aby włączyć obsługi wielu dzierżawców w swojej aplikacji:</span><span class="sxs-lookup"><span data-stu-id="95f1f-113">In order to enable multi-tenancy on your application:</span></span>
- <span data-ttu-id="95f1f-114">Ustaw `Multi-Tenanted` właściwości `Yes` na informacje o rejestracji aplikacji w [Azure Portal](https://portal.azure.com/#blade/Microsoft_AAD_IAM/ActiveDirectoryMenuBlade/RegisteredApps) (domyślnie aplikacje utworzone w portalu Azure są skonfigurowane jako *pojedynczej dzierżawy*)</span><span class="sxs-lookup"><span data-stu-id="95f1f-114">Set `Multi-Tenanted` property to `Yes` on your application registration's information in the [Azure Portal](https://portal.azure.com/#blade/Microsoft_AAD_IAM/ActiveDirectoryMenuBlade/RegisteredApps) (by default, applications created in the Azure Portal are configured as *single-tenant*)</span></span>
- <span data-ttu-id="95f1f-115">Zaktualizuj kod do wysyłania żądań do "`common`" punktu końcowego (zaktualizować punktu końcowego z *https://login.microsoftonline.com/ {yourtenant}* do *https://login.microsoftonline.com/common*)</span><span class="sxs-lookup"><span data-stu-id="95f1f-115">Update your code to send requests to the '`common`' endpoint (update the endpoint from *https://login.microsoftonline.com/{yourtenant}* to *https://login.microsoftonline.com/common*)</span></span>
- <span data-ttu-id="95f1f-116">Dla niektórych platform, takich jak ASP.NET należy również zaktualizować swój kod, aby zaakceptować wielu wystawców</span><span class="sxs-lookup"><span data-stu-id="95f1f-116">For some platforms, like ASP.NET, you need also to update your code to accept multiple issuers</span></span>

<span data-ttu-id="95f1f-117">Aby uzyskać więcej informacji na temat obsługi wielu dzierżawców, zobacz: [jak zarejestrować każdy użytkownik usługi Azure Active Directory (AD) przy użyciu wzorca wielodostępnych aplikacji](./active-directory-devhowto-multi-tenant-overview.md).</span><span class="sxs-lookup"><span data-stu-id="95f1f-117">For more information about multi-tenancy, see: [How to sign in any Azure Active Directory (AD) user using the multi-tenant application pattern](./active-directory-devhowto-multi-tenant-overview.md).</span></span>

### <a name="single-tenant-applications"></a><span data-ttu-id="95f1f-118">Aplikacje pojedynczej dzierżawy</span><span class="sxs-lookup"><span data-stu-id="95f1f-118">Single-tenant applications</span></span>
<span data-ttu-id="95f1f-119">Aplikacje, które akceptują tylko logowania użytkowników zdefiniowanych wystąpienia usługi Azure Active Directory są określane jako *aplikacji pojedynczej dzierżawy*.</span><span class="sxs-lookup"><span data-stu-id="95f1f-119">Applications that only accept sign-ins from users of a defined Azure Active Directory instance are known as *single-tenant application*.</span></span> <span data-ttu-id="95f1f-120">Użytkownicy zewnętrzni (łącznie z konta służbowego z innych organizacji lub osobiste konto) można Zaloguj się do aplikacji pojedynczej dzierżawy, po dodaniu każdego użytkownika jako *konta gościa* do wystąpienia usługi Azure Active Directory, że aplikacja jest zarejestrowany.</span><span class="sxs-lookup"><span data-stu-id="95f1f-120">External users (including Work or School accounts from other organizations, or personal account) can sign in to a single-tenant application after adding each user as *guest account* to the Azure Active Directory instance that the application is registered.</span></span> <span data-ttu-id="95f1f-121">Jako konta gościa można dodać użytkowników do usługi Azure Active Directory za pośrednictwem [ *współpracy B2B usługi Azure AD* ](../active-directory-b2b-what-is-azure-ad-b2b.md) - i mogą to robić [programowo](../active-directory-b2b-code-samples.md).</span><span class="sxs-lookup"><span data-stu-id="95f1f-121">You can add users as guest accounts to an Azure Active Directory via the [*Azure AD B2B collaboration*](../active-directory-b2b-what-is-azure-ad-b2b.md) - and it can be done [programatically](../active-directory-b2b-code-samples.md).</span></span> <span data-ttu-id="95f1f-122">Gdy użytkownik zostanie dodany jako konta gościa do usługi Azure Active Directory, wiadomość e-mail z zaproszeniem są wysyłane do użytkownika, który musi zaakceptować zaproszenie, klikając łącze w wiadomości e-mail z zaproszeniem.</span><span class="sxs-lookup"><span data-stu-id="95f1f-122">When you add a user as guest account to an Azure Active Directory, an invitation email is sent to the user, who has to accept the invitation by clicking on the link in the invitation email.</span></span> <span data-ttu-id="95f1f-123">Zaproszenia, które są wysyłane do dodatkowych użytkowników w organizacji zaproszenia, która jest również członkiem organizacji partnerskiej odpowiedzialnej za nie są wymagane, aby zaakceptować zaproszenie do logowania.</span><span class="sxs-lookup"><span data-stu-id="95f1f-123">Invitations that are sent to an additional user in an inviting organization that is also a member of the partner organization are not required to accept an invitation to sign in.</span></span>

<span data-ttu-id="95f1f-124">Aplikacje pojedynczego dzierżawcy można włączyć *kontaktu mnie* środowisko, ale jeśli chcesz włączyć jednym kliknięciem / bezpłatnej wersji próbnej środowisko zalecający AppSource włączenia obsługi wielu dzierżawców w swojej aplikacji zamiast tego.</span><span class="sxs-lookup"><span data-stu-id="95f1f-124">Single-tenant applications can enable the *Contact Me* experience, but if you want to enable the single-click/ free trial experience that AppSource recommends, enable multi-tenancy on your application instead.</span></span>


## <a name="appsource-trial-experiences"></a><span data-ttu-id="95f1f-125">Napotyka AppSource wersji próbnej</span><span class="sxs-lookup"><span data-stu-id="95f1f-125">AppSource trial experiences</span></span>

### <a name="free-trial-customer-led-trial-experience"></a><span data-ttu-id="95f1f-126">Bezpłatna wersja próbna (środowisko wersji próbnej doprowadziły klienta)</span><span class="sxs-lookup"><span data-stu-id="95f1f-126">Free Trial (Customer-led trial experience)</span></span> 
<span data-ttu-id="95f1f-127">*Doprowadziły klienta wersji próbnej* to środowisko, które AppSource zaleca jak oferuje jednym kliknięciem uzyskać dostęp do aplikacji.</span><span class="sxs-lookup"><span data-stu-id="95f1f-127">The *customer-led trial* is the experience that AppSource recommends as it offers a single-click access to your application.</span></span> <span data-ttu-id="95f1f-128">Poniżej w jaki sposób to środowisko wygląda następująco:</span><span class="sxs-lookup"><span data-stu-id="95f1f-128">Below an illustration of how this experience looks like:</span></span><br/><br/>

<table >
<tr>
    <td valign="top" width="33%">1.<br/><img src="media/active-directory-devhowto-appsource-certified/customer-led-trial-step1.png" width="85%"/><ul><li><span data-ttu-id="95f1f-129">Użytkownik wyszukuje aplikacji w witrynie sieci Web AppSource</span><span class="sxs-lookup"><span data-stu-id="95f1f-129">User finds your application in AppSource Web Site</span></span></li><li><span data-ttu-id="95f1f-130">Wybiera opcję "Bezpłatnej wersji próbnej"</span><span class="sxs-lookup"><span data-stu-id="95f1f-130">Selects ‘Free trial’ option</span></span></li></ul></td>
    <td valign="top" width="33%">2.<br/><img src="media/active-directory-devhowto-appsource-certified/customer-led-trial-step2.png" width="85%" /><ul><li><span data-ttu-id="95f1f-131">AppSource przekierowuje użytkownika do adresu URL witryny sieci web</span><span class="sxs-lookup"><span data-stu-id="95f1f-131">AppSource redirects user to a URL in your web site</span></span></li><li><span data-ttu-id="95f1f-132">Z witryny sieci web uruchamia <i>single-sign-on</i> proces automatycznie (ładowania strony)</span><span class="sxs-lookup"><span data-stu-id="95f1f-132">Your web site starts the <i>single-sign-on</i> process automatically (on page load)</span></span></li></ul></td>
    <td valign="top" width="33%">3.<br/><img src="media/active-directory-devhowto-appsource-certified/customer-led-trial-step3.png" width="85%"/><ul><li><span data-ttu-id="95f1f-133">Użytkownik zostanie przekierowany do strony logowania firmy Microsoft</span><span class="sxs-lookup"><span data-stu-id="95f1f-133">User is redirected to Microsoft Sign-in page</span></span></li><li><span data-ttu-id="95f1f-134">Użytkownik podaje poświadczenia do zalogowania</span><span class="sxs-lookup"><span data-stu-id="95f1f-134">User provides credentials to sign in</span></span></li></ul></td>
</tr>
<tr>
    <td valign="top" width="33%">4.<br/><img src="media/active-directory-devhowto-appsource-certified/customer-led-trial-step4.png" width="85%"/><ul><li><span data-ttu-id="95f1f-135">Użytkownik wyrazi zgodę dla aplikacji</span><span class="sxs-lookup"><span data-stu-id="95f1f-135">User gives consent for your application</span></span></li></ul></td>
    <td valign="top" width="33%">5.<br/><img src="media/active-directory-devhowto-appsource-certified/customer-led-trial-step5.png" width="85%"/><ul><li><span data-ttu-id="95f1f-136">Logowanie kończy i użytkownik zostanie przekierowany do witryny sieci web</span><span class="sxs-lookup"><span data-stu-id="95f1f-136">Sign-in completes and user is redirected back to your web site</span></span></li><li><span data-ttu-id="95f1f-137">Użytkownik uruchamia bezpłatnej wersji próbnej</span><span class="sxs-lookup"><span data-stu-id="95f1f-137">User starts the free trial</span></span></li></ul></td>
    <td></td>
</tr>
</table>

### <a name="contact-me-partner-led-trial-experience"></a><span data-ttu-id="95f1f-138">Skontaktować się ze mną (doprowadziły partnera środowisko wersji próbnej)</span><span class="sxs-lookup"><span data-stu-id="95f1f-138">Contact Me (Partner-led trial experience)</span></span>
<span data-ttu-id="95f1f-139">*Partnera środowisko wersji próbnej* można użyć w przypadku ręcznego lub długoterminowej operacja musi zostać przeprowadzona do obsługi administracyjnej użytkownika / firmę: na przykład, aplikacja musi udostępniać maszyn wirtualnych, wystąpień bazy danych lub operacji, które zająć dużo czasu.</span><span class="sxs-lookup"><span data-stu-id="95f1f-139">The *partner trial experience* can be used when a manual or a long-term operation needs to happen to provision the user/ company: for example, your application needs to provision virtual machines, database instances, or operations that take much time to complete.</span></span> <span data-ttu-id="95f1f-140">W takim przypadku po użytkownik wybiera *"Żądania wersji próbnej"* przycisk i wypełnienia formularz AppSource wysyła informacje kontaktowe użytkownika.</span><span class="sxs-lookup"><span data-stu-id="95f1f-140">In this case, after user selects the *'Request Trial'* button and fills out a form, AppSource sends you the user's contact information.</span></span> <span data-ttu-id="95f1f-141">Po otrzymaniu tych informacji, możesz następnie udostępnić środowiska i wysłać instrukcje dla użytkownika na temat sposobu dostępu środowisko wersji próbnej:</span><span class="sxs-lookup"><span data-stu-id="95f1f-141">Upon receiving this information, you then provision the environment and send the instructions to the user on how to access the trial experience:</span></span><br/><br/>

<table valign="top">
<tr>
    <td valign="top" width="33%">1.<br/><img src="media/active-directory-devhowto-appsource-certified/partner-led-trial-step1.png" width="85%"/><ul><li><span data-ttu-id="95f1f-142">Użytkownik wyszukuje aplikacji w witrynie sieci web AppSource</span><span class="sxs-lookup"><span data-stu-id="95f1f-142">User finds your application in AppSource web site</span></span></li><li><span data-ttu-id="95f1f-143">Wybiera opcję "Skontaktuj się z Me"</span><span class="sxs-lookup"><span data-stu-id="95f1f-143">Selects ‘Contact Me’ option</span></span></li></ul></td>
    <td valign="top" width="33%">2.<br/><img src="media/active-directory-devhowto-appsource-certified/partner-led-trial-step2.png" width="85%"/><ul><li><span data-ttu-id="95f1f-144">Wypełnia formularz informacje kontaktowe</span><span class="sxs-lookup"><span data-stu-id="95f1f-144">Fills out a form with contact information</span></span></li></ul></td>
     <td valign="top" width="33%">3.<br/><br/>
        <table bgcolor="#f7f7f7">
        <tr>
            <td><img src="media/active-directory-devhowto-appsource-certified/UserContact.png" width="55%"/></td>
            <td><span data-ttu-id="95f1f-145">Odbieranie informacji o użytkowniku</span><span class="sxs-lookup"><span data-stu-id="95f1f-145">You receive user information</span></span></td>
        </tr>
        <tr>
            <td><img src="media/active-directory-devhowto-appsource-certified/SetupEnv.png" width="55%"/></td>
            <td><span data-ttu-id="95f1f-146">Konfigurowanie środowiska</span><span class="sxs-lookup"><span data-stu-id="95f1f-146">Setup environment</span></span></td>
        </tr>
        <tr>
            <td><img src="media/active-directory-devhowto-appsource-certified/ContactCustomer.png" width="55%"/></td>
            <td><span data-ttu-id="95f1f-147">Skontaktuj się z użytkownikiem z informacjami o wersji próbnej</span><span class="sxs-lookup"><span data-stu-id="95f1f-147">Contact user with trial info</span></span></td>
        </tr>
        </table><br/><br/>
        <ul><li><span data-ttu-id="95f1f-148">Odbieranie informacji i wersji próbnej wystąpienia ustawienia użytkownika</span><span class="sxs-lookup"><span data-stu-id="95f1f-148">You receive user's information and setup trial instance</span></span></li><li><span data-ttu-id="95f1f-149">Wyślij hiperłącze, aby dostęp do aplikacji dla użytkownika</span><span class="sxs-lookup"><span data-stu-id="95f1f-149">You send the hyperlink to access your application to the user</span></span></li></ul>
    </td>
</tr>
<tr>
    <td valign="top" width="33%">4.<br/><img src="media/active-directory-devhowto-appsource-certified/partner-led-trial-step3.png" width="85%"/><ul><li><span data-ttu-id="95f1f-150">Użytkownik uzyskuje dostęp do aplikacji i ukończyć proces single-sign-on</span><span class="sxs-lookup"><span data-stu-id="95f1f-150">User accesses your application and complete the single-sign-on process</span></span></li></ul></td>
    <td valign="top" width="33%">5.<br/><img src="media/active-directory-devhowto-appsource-certified/partner-led-trial-step4.png" width="85%"/><ul><li><span data-ttu-id="95f1f-151">Użytkownik wyrazi zgodę dla aplikacji</span><span class="sxs-lookup"><span data-stu-id="95f1f-151">User gives consent for your application</span></span></li></ul></td>
    <td valign="top" width="33%">6.<br/><img src="media/active-directory-devhowto-appsource-certified/customer-led-trial-step5.png" width="85%"/><ul><li><span data-ttu-id="95f1f-152">Logowanie kończy i użytkownik zostanie przekierowany do witryny sieci web</span><span class="sxs-lookup"><span data-stu-id="95f1f-152">Sign-in completes and user is redirected back to your web site</span></span></li><li><span data-ttu-id="95f1f-153">Użytkownik uruchamia bezpłatnej wersji próbnej</span><span class="sxs-lookup"><span data-stu-id="95f1f-153">User starts the free trial</span></span></li></ul></td>
   
</tr>
</table>

### <a name="more-information"></a><span data-ttu-id="95f1f-154">Więcej informacji</span><span class="sxs-lookup"><span data-stu-id="95f1f-154">More information</span></span>
<span data-ttu-id="95f1f-155">Aby uzyskać więcej informacji na temat środowisko wersji próbnej AppSource, zobacz [ten film](https://aka.ms/trialexperienceforwebapps).</span><span class="sxs-lookup"><span data-stu-id="95f1f-155">For more information about the AppSource trial experience, see [this video](https://aka.ms/trialexperienceforwebapps).</span></span> 
 
## <a name="next-steps"></a><span data-ttu-id="95f1f-156">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="95f1f-156">Next Steps</span></span>

- <span data-ttu-id="95f1f-157">Aby uzyskać więcej informacji dotyczących tworzenia aplikacji, które obsługują usługi Azure Active Directory logowania, zobacz [scenariusze uwierzytelniania dla usługi Azure AD](https://docs.microsoft.com/azure/active-directory/develop/active-directory-authentication-scenarios)</span><span class="sxs-lookup"><span data-stu-id="95f1f-157">For more information on building applications that support Azure Active Directory sign-ins, see [Authentication Scenarios for Azure AD](https://docs.microsoft.com/azure/active-directory/develop/active-directory-authentication-scenarios)</span></span> 

- <span data-ttu-id="95f1f-158">Aby uzyskać informacje dotyczące listy aplikacji SaaS w AppSource, zobacz [informacje o partnerze AppSource](https://appsource.microsoft.com/partners)</span><span class="sxs-lookup"><span data-stu-id="95f1f-158">For information on how to list your SaaS application in AppSource, go see [AppSource Partner Information](https://appsource.microsoft.com/partners)</span></span>


## <a name="get-support"></a><span data-ttu-id="95f1f-159">Uzyskaj pomoc techniczną</span><span class="sxs-lookup"><span data-stu-id="95f1f-159">Get Support</span></span>
<span data-ttu-id="95f1f-160">Integracja usługi Azure Active Directory, używamy [przepełnienie stosu](http://stackoverflow.com/questions/tagged/azure-active-directory) społeczności, aby zapewnić obsługę.</span><span class="sxs-lookup"><span data-stu-id="95f1f-160">For Azure Active Directory integration, we use [Stack Overflow](http://stackoverflow.com/questions/tagged/azure-active-directory) with the community to provide support.</span></span> 

<span data-ttu-id="95f1f-161">Zdecydowanie zaleca się najpierw zadać pytania w witrynie Stack Overflow i Przeglądaj istniejących problemów, aby zobaczyć, jeśli ktoś poprosił pytanie przed.</span><span class="sxs-lookup"><span data-stu-id="95f1f-161">We highly recommend you ask your questions on Stack Overflow first and browse existing issues to see if someone has asked your question before.</span></span> <span data-ttu-id="95f1f-162">Upewnij się, że pytania lub komentarze są oznaczane `[azure-active-directory]`.</span><span class="sxs-lookup"><span data-stu-id="95f1f-162">Make sure that your questions or comments are tagged with `[azure-active-directory]`.</span></span>

<span data-ttu-id="95f1f-163">W poniższej sekcji komentarzy umożliwia wyrazić swoją opinię i pomóc nam dostosować i kształtu zawartość.</span><span class="sxs-lookup"><span data-stu-id="95f1f-163">Use the following comments section to provide feedback and help us refine and shape our content.</span></span>

<!--Reference style links -->
[AAD-Auth-Scenarios]: ./active-directory-authentication-scenarios.md
[AAD-Auth-Scenarios-Browser-To-WebApp]: ./active-directory-authentication-scenarios.md#web-browser-to-web-application
[AAD-Dev-Guide]: ./active-directory-developers-guide.md
[AAD-Howto-Multitenant-Overview]: ./active-directory-devhowto-multi-tenant-overview.md
[AAD-QuickStart-Web-Apps]: ./active-directory-developers-guide.md#get-started


<!--Image references-->