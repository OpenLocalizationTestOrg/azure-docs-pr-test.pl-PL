---
title: "Aplikacje, uprawnienia i zgody w usłudze Azure Active Directory. | Microsoft Docs"
description: "Program Azure AD Connect umożliwia integrowanie katalogów lokalnych z usługą Azure Active Directory. Dzięki temu tooprovide wspólną tożsamością dla usługi Office 365, Azure i aplikacji SaaS zintegrowanych z usługą Azure AD."
keywords: "wprowadzenie tooAzure AD, aplikacji, co to jest usługa Azure AD Connect, instalowania usługi active directory"
services: active-directory
documentationcenter: 
author: billmath
manager: femila
editor: 
ms.assetid: 25897cc4-7687-49b6-b0d5-71f51302b6b1
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/31/2017
ms.author: billmath
ms.reviewer: jesakowi
ms.custom: oldportal;it-pro;
ms.openlocfilehash: af0c2669199736fdb41e85876a7e3a7064e80770
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="apps-permissions-and-consent-in-azure-active-directory"></a><span data-ttu-id="0a7a5-105">Aplikacje, uprawnienia i zgody w usłudze Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="0a7a5-105">Apps, permissions, and consent in Azure Active Directory</span></span>
<span data-ttu-id="0a7a5-106">W usłudze Azure Active Directory możesz dodać katalog tooyour aplikacji.</span><span class="sxs-lookup"><span data-stu-id="0a7a5-106">Within Azure Active Directory, you can add applications tooyour directory.</span></span>  <span data-ttu-id="0a7a5-107">aplikacji Hello może się różnić w zależności od typu aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="0a7a5-107">hello applications can vary depending on hello type of application.</span></span>  <span data-ttu-id="0a7a5-108">aplikacje tooview w portalu klasycznym hello, wybierz katalog i wybierz aplikacje.</span><span class="sxs-lookup"><span data-stu-id="0a7a5-108">tooview applications in hello classic portal, select a directory and choose applications.</span></span>

![](media/active-directory-apps-permissions-consent/apps1.png)

> [!IMPORTANT]
> <span data-ttu-id="0a7a5-109">Firma Microsoft zaleca się, że zarządzania usługi Azure AD przy użyciu hello [Centrum administracyjnego usługi Azure AD](https://aad.portal.azure.com) w hello portalu Azure zamiast hello klasycznego portalu Azure, do którego odwołuje się w tym artykule.</span><span class="sxs-lookup"><span data-stu-id="0a7a5-109">Microsoft recommends that you manage Azure AD using hello [Azure AD admin center](https://aad.portal.azure.com) in hello Azure portal instead of using hello Azure classic portal referenced in this article.</span></span>

## <a name="types-of-apps"></a><span data-ttu-id="0a7a5-110">Typy aplikacji</span><span class="sxs-lookup"><span data-stu-id="0a7a5-110">Types of apps</span></span>

1. <span data-ttu-id="0a7a5-111">**Aplikacje z jedną dzierżawą**</span><span class="sxs-lookup"><span data-stu-id="0a7a5-111">**Single-tenant apps**</span></span> </br>
    - <span data-ttu-id="0a7a5-112">**Aplikacje pojedynczej dzierżawy** -często określany tooas aplikacji — biznesowych (LOB).</span><span class="sxs-lookup"><span data-stu-id="0a7a5-112">**Single-tenant apps** - Often referred tooas line-of-business (LOB) apps.</span></span> <span data-ttu-id="0a7a5-113">Jest to hello wtedy, gdy ktoś z organizacji rozwija własnej aplikacji i chcesz użytkowników w stanie toosign toobe hello organizacji w toohello aplikacji.</span><span class="sxs-lookup"><span data-stu-id="0a7a5-113">This is hello case where someone within your organization develops their own app, and would like users in hello organization toobe able toosign in toohello app.</span></span>
    ![](media/active-directory-apps-permissions-consent/apps2.png)
    - <span data-ttu-id="0a7a5-114">**Aplikacje serwera Proxy aplikacji** — udostępnianie aplikacji lokalnych przy użyciu serwera Proxy aplikacji usługi AD platformy Azure, aplikacji pojedynczej dzierżawy jest zarejestrowany w dzierżawie (w toohello dodanie usługi serwera Proxy aplikacji).</span><span class="sxs-lookup"><span data-stu-id="0a7a5-114">**App Proxy apps** - When you expose an on-prem application with Azure AD App Proxy, a single-tenant app is registered in your tenant (in addition toohello App Proxy service).</span></span> <span data-ttu-id="0a7a5-115">Ta aplikacja reprezentuje Twoją aplikację lokalną dla wszystkich interakcji w chmurze (na przykład na potrzeby uwierzytelniania).</span><span class="sxs-lookup"><span data-stu-id="0a7a5-115">This app is what represents your on-prem application for all cloud interactions (for example, authentication).</span></span> <span data-ttu-id="0a7a5-116">(Usługa Serwer proxy aplikacji wymaga usługi Azure AD w wersji Podstawowa lub wyższej).</span><span class="sxs-lookup"><span data-stu-id="0a7a5-116">(App Proxy requires Azure AD Basic or higher.)</span></span>


2. <span data-ttu-id="0a7a5-117">**Aplikacje z wieloma dzierżawami**</span><span class="sxs-lookup"><span data-stu-id="0a7a5-117">**Multi-tenant apps**</span></span>
    - <span data-ttu-id="0a7a5-118">**Wielodostępne aplikacji, które inne osoby mogą wyrazić zgodę na** — podobne zbyt "pojedynczej dzierżawy aplikacji, które organizacja rozwija".</span><span class="sxs-lookup"><span data-stu-id="0a7a5-118">**Multi-tenant apps which others can consent to** - similar too“single-tenant apps that your organization develops”.</span></span> <span data-ttu-id="0a7a5-119">Podstawowa różnica Hello (oprócz hello logikę w samej aplikacji hello) polega na tym, że użytkownicy od pozostałych dzierżawców można również zgody tooand logowania aplikacji toohello.</span><span class="sxs-lookup"><span data-stu-id="0a7a5-119">hello main difference (besides hello logic in hello app itself) is that users from other tenants can also consent tooand sign in toohello app.</span></span></br>
    ![](media/active-directory-apps-permissions-consent/apps4.png)
    - <span data-ttu-id="0a7a5-120">**Opracowane przez strony trzecie aplikacje z wieloma dzierżawami, na które może się zgodzić firma Contoso**.</span><span class="sxs-lookup"><span data-stu-id="0a7a5-120">**Multi-tenant apps others develop, which Contoso can consent to**.</span></span> <span data-ttu-id="0a7a5-121">(W skrócie: „aplikacje, na które wyrażono zgodę”). Jest to po stronie Przerzucanie hello "wielodostępnych aplikacji, które rozwija organizacji".</span><span class="sxs-lookup"><span data-stu-id="0a7a5-121">(Or “consented apps”, for short.) This is hello flip side of “multi-tenant apps your organization develops”.</span></span> <span data-ttu-id="0a7a5-122">Gdy aplikacja wielodostępne innej organizacji, które zostały zaakceptowane, użytkownicy w organizacji można zgody toohello aplikacji i zaloguj tooit.</span><span class="sxs-lookup"><span data-stu-id="0a7a5-122">When another organization develops a multi-tenant app, users of your organization can consent toohello app and sign in tooit.</span></span>
    - <span data-ttu-id="0a7a5-123">**Aplikacje firmy Microsoft** — aplikacje, które reprezentują usługi firmy Microsoft.</span><span class="sxs-lookup"><span data-stu-id="0a7a5-123">**Microsoft first-party apps** - Apps that represent Microsoft services.</span></span> <span data-ttu-id="0a7a5-124">Zgoda jest wymuszany przez fakt hello utworzysz hello usługi.</span><span class="sxs-lookup"><span data-stu-id="0a7a5-124">Consent is driven by hello fact that you sign up for hello service.</span></span> <span data-ttu-id="0a7a5-125">Brak czasami specjalne UX i logiki dla niektórych aplikacji firmy, która jest często używana podczas ustanawiania zasady wokół aplikacji toohello dostępu.</span><span class="sxs-lookup"><span data-stu-id="0a7a5-125">There is sometimes special UX and logic for certain first-party apps that is often used when establishing policies around access toohello app.</span></span></br>
    ![](media/active-directory-apps-permissions-consent/apps3.png)
    - <span data-ttu-id="0a7a5-126">**Wstępnie zintegrowanych aplikacji** -aplikacji dostępnych w hello AD galerii aplikacji Azure, które można dodać tooyour katalogu tooprovide pojedynczego logowania jednokrotnego (i w niektórych przypadkach inicjowania obsługi administracyjnej) toopopular aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="0a7a5-126">**Pre-integrated apps** - Apps available in hello Azure AD App Gallery, which you can add tooyour directory tooprovide single sign-on (and in some cases, provisioning) toopopular SaaS apps.</span></span>
    - <span data-ttu-id="0a7a5-127">**Logowanie jednokrotne w usłudze Azure AD**: „rzeczywiste” logowanie jednokrotne w aplikacjach, które można zintegrować z usługą Azure AD przy użyciu obsługiwanego protokołu logowania, takiego jak SAML 2.0 lub OpenID Connect.</span><span class="sxs-lookup"><span data-stu-id="0a7a5-127">**Azure AD single sign-on**: “Real” SSO, for apps that can be integrated with Azure AD, through a supported sign-in protocol such as SAML 2.0 or OpenID Connect.</span></span> <span data-ttu-id="0a7a5-128">Kreator Hello przeprowadzi Cię przez proces konfigurowania go.</span><span class="sxs-lookup"><span data-stu-id="0a7a5-128">hello wizard walks you through setting it up.</span></span>
    - <span data-ttu-id="0a7a5-129">**Hasło logowania jednokrotnego**: usługi Azure AD bezpiecznie przechowuje poświadczenia użytkownika hello aplikacji hello, a poświadczenia hello są "wstrzykuje" hello logowania w formularzu przez hello rozszerzenia przeglądarki dostępu aplikacji usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="0a7a5-129">**Password single sign-on**: Azure AD securely stores hello user’s credentials for hello app, and hello credentials are “injected” into hello sign-in form by hello Azure AD App Access browser extension.</span></span> <span data-ttu-id="0a7a5-130">To działanie jest znane również jako „magazynowanie haseł”.</span><span class="sxs-lookup"><span data-stu-id="0a7a5-130">Also known as “password vaulting”.</span></span>

## <a name="permissions"></a><span data-ttu-id="0a7a5-131">Uprawnienia</span><span class="sxs-lookup"><span data-stu-id="0a7a5-131">Permissions</span></span>

<span data-ttu-id="0a7a5-132">Podczas rejestrowania aplikacji hello użytkownika wykonującego hello rejestracji aplikacji (czyli hello developer) definiuje uprawnienia aplikacji hello musi mieć dostęp do i zasoby.</span><span class="sxs-lookup"><span data-stu-id="0a7a5-132">When an app is registered, hello user performing hello app registration (that is, hello developer) defines which permissions hello app needs access to, and which resources.</span></span> <span data-ttu-id="0a7a5-133">(hello zasoby są, same zdefiniowany jako innych aplikacji). Ktoś tworzeniem aplikacji czytnika poczty, będzie na przykład stan czy aplikacji musi mieć uprawnienie "Dostęp do skrzynek pocztowych jako hello zalogowanego użytkownika" hello w hello "Office 365 usługi Exchange Online" zasobów:</span><span class="sxs-lookup"><span data-stu-id="0a7a5-133">(hello resources are, themselves, defined as other apps.) For example, someone building a mail reader app, would state that their app requires hello “Access mailboxes as hello signed-in user” permission in hello “Office 365 Exchange Online” resource:</span></span>
    
![](media/active-directory-apps-permissions-consent/apps6.png)

<span data-ttu-id="0a7a5-134">Aby dla jednej aplikacji (powitania klienta) toorequest niektóre uprawnienia z innej aplikacji (hello zasobów) deweloperów hello hello zasobów aplikacji definiuje hello uprawnienia, które istnieją.</span><span class="sxs-lookup"><span data-stu-id="0a7a5-134">In order for one app (hello client) toorequest a certain permission from another app (hello resource), hello developer of hello resource app defines hello permissions that exist.</span></span> <span data-ttu-id="0a7a5-135">W naszym przykładzie firmy Microsoft, właściciela hello hello "Office 365 usługi Exchange Online" zasobów aplikacji zdefiniowano uprawnień o nazwie "Dostęp do skrzynek pocztowych jako hello zalogowanego użytkownika".</span><span class="sxs-lookup"><span data-stu-id="0a7a5-135">In our example, Microsoft, hello owner of hello “Office 365 Exchange Online” resource app, have defined a permission named “Access mailboxes as hello signed-in user”.</span></span>

<span data-ttu-id="0a7a5-136">Podczas definiowania uprawnień, hello Deweloper aplikacji musi definiować czy hello uprawnienia można zgodę na, czy wymaga zgody administratora.</span><span class="sxs-lookup"><span data-stu-id="0a7a5-136">When defining permissions, hello app developer must define if hello permission can be consented to, or if it requires admin consent.</span></span> <span data-ttu-id="0a7a5-137">Dzięki temu deweloperzy tooallow tooconsent użytkowników na własnych tooapps żądanie tylko małej czułości uprawnień, ale wymagają administratorom tooconsent toomore poufnych uprawnienia.</span><span class="sxs-lookup"><span data-stu-id="0a7a5-137">This allows developers tooallow users tooconsent on their own tooapps requesting only low-sensitivity permissions, but require admins tooconsent toomore sensitive permissions.</span></span> <span data-ttu-id="0a7a5-138">Na przykład Witaj aplikacji zasobu "Azure Active Directory", została zdefiniowana, dlatego użytkownicy mogą wyrazić zgodę tooapps, żądania z ograniczonymi uprawnieniami tylko do odczytu.</span><span class="sxs-lookup"><span data-stu-id="0a7a5-138">For example, hello “Azure Active Directory” resource app, has been defined, so users can consent tooapps, requesting limited read-only permissions.</span></span>  <span data-ttu-id="0a7a5-139">Jednak w przypadku pełnych uprawnień do odczytu i wszystkich uprawnień do zapisu jest wymagana zgoda administratora.</span><span class="sxs-lookup"><span data-stu-id="0a7a5-139">However, admin consent is required for full read permissions, and all write permissions.</span></span>

<span data-ttu-id="0a7a5-140">Ponieważ klienci natywni nie są uwierzytelniani, aplikacja zdefiniowana jako klient natywny może żądać jedynie uprawnień delegowanych.</span><span class="sxs-lookup"><span data-stu-id="0a7a5-140">Because native clients are not authenticated, an app defined as a native client app can only request delegated permissions.</span></span> <span data-ttu-id="0a7a5-141">To znaczy, że w uzyskiwanie tokenu zawsze musi być zaangażowany rzeczywisty użytkownik.</span><span class="sxs-lookup"><span data-stu-id="0a7a5-141">This means that there must always be an actual user involved when obtaining a token.</span></span> <span data-ttu-id="0a7a5-142">Podczas uzyskiwania tokenu dostępu aplikacje sieci Web i interfejsy API sieci Web (klienci poufni) zawsze muszą dokonywać uwierzytelniania za pomocą usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="0a7a5-142">Web apps and web APIs (confidential clients), must always authenticate with Azure AD when getting an access token.</span></span> <span data-ttu-id="0a7a5-143">Co oznacza mają również możliwość hello żąda uprawnienia tylko do aplikacji.</span><span class="sxs-lookup"><span data-stu-id="0a7a5-143">Meaning they also have hello possibility of requesting app-only permissions.</span></span> <span data-ttu-id="0a7a5-144">Jeśli na przykład usługi zaplecza tooanother tooauthenticate wymaga jednej usługi zaplecza.</span><span class="sxs-lookup"><span data-stu-id="0a7a5-144">For example, if one back-end service needs tooauthenticate tooanother back-end service.</span></span> <span data-ttu-id="0a7a5-145">Aplikacje żądające uprawnień dotyczących tylko aplikacji zawsze wymagają zgody administratora.</span><span class="sxs-lookup"><span data-stu-id="0a7a5-145">Applications requesting app-only permissions always require administrator consent.</span></span>

<span data-ttu-id="0a7a5-146">Podsumowując:</span><span class="sxs-lookup"><span data-stu-id="0a7a5-146">Summarizing:</span></span>



- <span data-ttu-id="0a7a5-147">Aplikacji (klienta) określają uprawnienia hello, które są niezbędne do innych aplikacji (zasoby).</span><span class="sxs-lookup"><span data-stu-id="0a7a5-147">An app (client) states hello permissions it needs for other apps (resources).</span></span>
- <span data-ttu-id="0a7a5-148">Aplikacja (zasobów) określają, jakie uprawnienia są uwidocznione tooother aplikacji (klienci).</span><span class="sxs-lookup"><span data-stu-id="0a7a5-148">An app (resource) states what permissions are exposed tooother apps (clients).</span></span>
- <span data-ttu-id="0a7a5-149">Uprawnienia mogą dotyczyć tylko aplikacji lub być uprawnieniami delegowanymi.</span><span class="sxs-lookup"><span data-stu-id="0a7a5-149">A permission can be an app-only permission, or a delegated permission.</span></span>
- <span data-ttu-id="0a7a5-150">Uprawnienia delegowane mogą być oznaczona jako wymagające zgody użytkownika lub wymagające zgody administratora.</span><span class="sxs-lookup"><span data-stu-id="0a7a5-150">A delegated permission can be marked as “allows user consent”, or “requires admin consent”.</span></span>
- <span data-ttu-id="0a7a5-151">Aplikacja może zachowywać się jako klient (przez zadeklarowanie wymaga uprawnień tooa zasobów), jako zasób (przez zadeklarowanie uprawnienia, które udostępnia ona) lub obie.</span><span class="sxs-lookup"><span data-stu-id="0a7a5-151">An app can behave as a client (by declaring that it needs permissions tooa resource), as a resource (by declaring which permissions it exposes), or as both.</span></span>

## <a name="controls"></a><span data-ttu-id="0a7a5-152">Kontrolki</span><span class="sxs-lookup"><span data-stu-id="0a7a5-152">Controls</span></span>

<span data-ttu-id="0a7a5-153">Witaj poniżej znajduje się lista formantów inny administrator hello dostępne dla tego zachowania.</span><span class="sxs-lookup"><span data-stu-id="0a7a5-153">hello following is a list of hello different admin controls available for all this behavior.</span></span> <span data-ttu-id="0a7a5-154">Witaj, Administratorze przez formanty można uzyskać w portalu klasycznym hello na konfigurowanie hello katalogu.</span><span class="sxs-lookup"><span data-stu-id="0a7a5-154">hello admin controls can be accessed in hello classic portal from configure under hello directory.</span></span>

![](media/active-directory-apps-permissions-consent/apps7.png)

<span data-ttu-id="0a7a5-155">W hello Azure portalu, w obszarze **zarządzanie**, **ustawienia użytkownika**.</span><span class="sxs-lookup"><span data-stu-id="0a7a5-155">In hello Azure portal, under **manage**, **user settings**.</span></span>

![](media/active-directory-apps-permissions-consent/apps11.png)



- <span data-ttu-id="0a7a5-156">Można kontrolować, czy użytkownicy mogą wyrazić zgodę tooapps:</span><span class="sxs-lookup"><span data-stu-id="0a7a5-156">You can control whether users can consent tooapps:</span></span>

<span data-ttu-id="0a7a5-157">W portalu klasycznym hello, wybierz **użytkownicy mogą spowodować tooaccess uprawnienia aplikacji swoje dane.**
![](media/active-directory-apps-permissions-consent/apps8.png)</span><span class="sxs-lookup"><span data-stu-id="0a7a5-157">In hello classic portal, select **Users may give applications permissions tooaccess their data.**
![](media/active-directory-apps-permissions-consent/apps8.png)</span></span>

<span data-ttu-id="0a7a5-158">Hello portalu Azure, wybierz **użytkownicy mogą zezwolić aplikacji tooaccess swoje dane**.</span><span class="sxs-lookup"><span data-stu-id="0a7a5-158">In hello Azure portal, select **users can allow apps tooaccess their data**.</span></span>
![](media/active-directory-apps-permissions-consent/apps12.png)



- <span data-ttu-id="0a7a5-159">Można kontrolować, czy użytkownicy mogą zarejestrować swoje własne aplikacje BIZNESOWE pojedynczej dzierżawy: W klasycznym portalu wybierz hello **użytkownicy mogą dodawać zintegrowanych aplikacji.**
![](media/active-directory-apps-permissions-consent/apps9.png)</span><span class="sxs-lookup"><span data-stu-id="0a7a5-159">You can control whether users can register their own single-tenant LOB apps: In hello classic portal select **Users may add integrated applications.**
![](media/active-directory-apps-permissions-consent/apps9.png)</span></span>

<span data-ttu-id="0a7a5-160">Hello portalu Azure, wybierz **użytkownicy mogą zezwolić aplikacji tooaccess swoje dane**.</span><span class="sxs-lookup"><span data-stu-id="0a7a5-160">In hello Azure portal, select **users can allow apps tooaccess their data**.</span></span>
![](media/active-directory-apps-permissions-consent/apps13.png)

>[!NOTE]
><span data-ttu-id="0a7a5-161">Nawet jeśli użytkownicy aplikacji biznesowych tooregister pojedynczej dzierżawy, istnieją limity toowhat mogą być rejestrowane.</span><span class="sxs-lookup"><span data-stu-id="0a7a5-161">Even if you do allow users tooregister single-tenant LOB apps, there are limits toowhat can be registered.</span></span>  
><span data-ttu-id="0a7a5-162">Dotyczy to na przykład deweloperów, którzy nie są administratorami katalogów.</span><span class="sxs-lookup"><span data-stu-id="0a7a5-162">For example, developers who are not directory admins.</span></span>
>
>- <span data-ttu-id="0a7a5-163">Z aplikacji z jedną dzierżawą użytkownicy nie mogą zrobić aplikacji z wieloma dzierżawami.</span><span class="sxs-lookup"><span data-stu-id="0a7a5-163">Users cannot make a single-tenant app a multi-tenant app.</span></span>
>- <span data-ttu-id="0a7a5-164">Podczas rejestrowania aplikacji biznesowych pojedynczej dzierżawy, użytkownicy nie może zażądać aplikacji tooother uprawnienia tylko do aplikacji.</span><span class="sxs-lookup"><span data-stu-id="0a7a5-164">When registering single-tenant LOB apps, users cannot request app-only permissions tooother apps.</span></span>
>- <span data-ttu-id="0a7a5-165">Podczas rejestrowania aplikacji biznesowych pojedynczej dzierżawy, użytkownicy nie może zażądać aplikacji tooother delegowane uprawnienia, jeśli te uprawnienia Wymagaj zgody administratora.</span><span class="sxs-lookup"><span data-stu-id="0a7a5-165">When registering single-tenant LOB apps, users cannot request delegated permissions tooother apps if those permissions require admin consent.</span></span>
>- <span data-ttu-id="0a7a5-166">Użytkownicy nie mogą podjąć tooapps zmiany, które nie są właścicielami.</span><span class="sxs-lookup"><span data-stu-id="0a7a5-166">Users cannot make changes tooapps that they are not owners of.</span></span>



- <span data-ttu-id="0a7a5-167">Można zdecydować, czy użytkownicy mogą samodzielnie dodawać wstępnie zintegrowane aplikacje korzystające z logowania jednokrotnego z użyciem hasła („magazynowania haseł”). ![](media/active-directory-apps-permissions-consent/apps10.png)</span><span class="sxs-lookup"><span data-stu-id="0a7a5-167">You can control whether users can themselves add pre-integrated apps that use password SSO (aka “password vaulting”) ![](media/active-directory-apps-permissions-consent/apps10.png)</span></span>



- <span data-ttu-id="0a7a5-168">Można zdecydować, w jakich warunkach jest możliwe uzyskanie dostępu do aplikacji (dostęp warunkowy).</span><span class="sxs-lookup"><span data-stu-id="0a7a5-168">You can control under which conditions applications can be accessed (that is, conditional access).</span></span> <span data-ttu-id="0a7a5-169">Należy pamiętać, że dotyczy to zarówno aplikacja klienta toohello i toohello zasobów aplikacji.</span><span class="sxs-lookup"><span data-stu-id="0a7a5-169">Be aware this applies both toohello client app and toohello resource app.</span></span> <span data-ttu-id="0a7a5-170">Tak Załóżmy, że w ustawieniu zasad dostępu warunkowego, stwierdzający, że tej aplikacji "Office 365 usługi Exchange Online" hello jest możliwy tylko z komputerów, które są zgodne.</span><span class="sxs-lookup"><span data-stu-id="0a7a5-170">So, say you set a conditional access policy that says that hello “Office 365 Exchange Online” app can only be accessed from machines, which are compliant.</span></span>  <span data-ttu-id="0a7a5-171">Ta zasada będzie również zaczną działać, gdy użytkownik próbuje toouse aplikacji klienckiej, która żąda uprawnienia tooExchange w trybie Online.</span><span class="sxs-lookup"><span data-stu-id="0a7a5-171">This policy will also kick in when a user attempts toouse a client app which requests permissions tooExchange Online.</span></span>



- <span data-ttu-id="0a7a5-172">Masz widoczność, w którym aplikacje zostały przyzwolenie tooand te, które są używane.</span><span class="sxs-lookup"><span data-stu-id="0a7a5-172">You have visibility into which apps have been consented tooand which ones are being used.</span></span>

1.  <span data-ttu-id="0a7a5-173">Gdy użytkownik wyraża zgodę tooan aplikacji, tworzony jest obiekt ServicePrincipal w dzierżawie powitalnych.</span><span class="sxs-lookup"><span data-stu-id="0a7a5-173">When a user consents tooan app, a ServicePrincipal object is created in hello tenant.</span></span> <span data-ttu-id="0a7a5-174">Tworzenie ServicePrincipal jest uwzględniona w raporcie inspekcji hello.</span><span class="sxs-lookup"><span data-stu-id="0a7a5-174">ServicePrincipal creation is included in hello audit report.</span></span>
2.  <span data-ttu-id="0a7a5-175">Raporty dotyczące działań logowania użytkownika informujące użytkownika hello aplikacji, który loguje się do.</span><span class="sxs-lookup"><span data-stu-id="0a7a5-175">User sign-in activity reports tell you which app hello user is signing in to.</span></span> 

## <a name="example"></a><span data-ttu-id="0a7a5-176">Przykład</span><span class="sxs-lookup"><span data-stu-id="0a7a5-176">Example</span></span>

<span data-ttu-id="0a7a5-177">Na przykład Przyjrzyjmy aplikacji "FabrikamMail dla usługi Office 365" hello, która zaobserwowany się, że użytkownicy w Twojej dzierżawie się rejestruje.</span><span class="sxs-lookup"><span data-stu-id="0a7a5-177">As an example, let’s take hello “FabrikamMail for Office 365” app, which you’ve noticed users in your tenant are signing in to.</span></span> <span data-ttu-id="0a7a5-178">Aplikacja „FabrikamMail” to czytnik poczty e-mail dla systemu Android opublikowany przez firmę „Fabrikam, Inc.”.</span><span class="sxs-lookup"><span data-stu-id="0a7a5-178">“FabrikamMail” is a mail reader app for Android, published by “Fabrikam, Inc.”.</span></span> <span data-ttu-id="0a7a5-179">Znajduje się na powitania "aplikacje wielodostępne innych opracowanie, który Contoso można wyrazić zgodę na".</span><span class="sxs-lookup"><span data-stu-id="0a7a5-179">This falls into hello “multi-tenant apps other develop, which Contoso can consent to”.</span></span>

<span data-ttu-id="0a7a5-180">Jeśli użytkownicy mogą tooconsent, otrzymują zgody hello monitu o zalogowaniu po raz pierwszy:![](media/active-directory-apps-permissions-consent/apps14.png)</span><span class="sxs-lookup"><span data-stu-id="0a7a5-180">If users are allowed tooconsent, they get a consent prompt hello first time they sign in: ![](media/active-directory-apps-permissions-consent/apps14.png)</span></span>

<span data-ttu-id="0a7a5-181">"Dostęp do skrzynek pocztowych" jest hello uwzględniającym działania użytkownika zgody ciąg uprawnienia "Dostęp do skrzynek pocztowych jako hello zalogowanego użytkownika" hello udostępnianych przez "Office 365 usługi Exchange Online" (czyli Exchange).</span><span class="sxs-lookup"><span data-stu-id="0a7a5-181">“Access your mailboxes” is hello user-facing consent string for hello “Access mailboxes as hello signed-in user” permission exposed by “Office 365 Exchange Online” (that is, Exchange).</span></span>

<span data-ttu-id="0a7a5-182">Widać uprawnienia hello wyszukując hello ServicePrincipal obiektu dla programu Exchange (hello zasobów), który zostało dodane po utworzeniu konta w usłudze Office 365.</span><span class="sxs-lookup"><span data-stu-id="0a7a5-182">You can see hello permissions by looking up hello ServicePrincipal object for Exchange (hello resource), which was added when you signed up for Office 365.</span></span> <span data-ttu-id="0a7a5-183">Obiekt ServicePrincipal hello "wystąpienia" hello aplikacji można traktować w dzierżawie, który służy do rejestrowania różnych opcjach i konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="0a7a5-183">You can think of hello ServicePrincipal object of an “instance” of hello app in your tenant, which is used for recording different options and configurations.</span></span>  <span data-ttu-id="0a7a5-184">Zobacz ten przy użyciu hello `Get-AzureADServicePrincipal` w programie PowerShell.</span><span class="sxs-lookup"><span data-stu-id="0a7a5-184">You can see this by using hello `Get-AzureADServicePrincipal` in PowerShell.</span></span>

    PS C:\> Get-AzureADServicePrincipal -ObjectId 383f7b97-6754-4d3d-9474-3908ebcba1c6 | fl *
    
    DeletionTimeStamp         : 
    ObjectId                  : 383f7b97-6754-4d3d-9474-3908ebcba1c6
    ObjectType                : ServicePrincipal
    AccountEnabled            : True
    AppDisplayName            : Office 365 Exchange Online
    AppId                     : 00000002-0000-0ff1-ce00-000000000000
    AppOwnerTenantId          : 
    AppRoleAssignmentRequired : False
    AppRoles                  : {...}
    DisplayName               : Microsoft.Exchange
    ErrorUrl                  : 
    Homepage                  : 
    KeyCredentials            : {}
    LogoutUrl                 : 
    Oauth2Permissions         : {...
                                , class OAuth2Permission {
                                  AdminConsentDescription : Allows hello app toohave hello same access toomailboxes as hello signed-in user via Exchange Web Services.
                                  AdminConsentDisplayName : Access mailboxes as hello signed-in user via Exchange Web Services
                                  Id                      : 3b5f3d61-589b-4a3c-a359-5dd4b5ee5bd5
                                  IsEnabled               : True
                                  Type                    : User
                                  UserConsentDescription  : Allows hello app full access tooyour mailboxes on your behalf.
                                  UserConsentDisplayName  : Access your mailboxes
                                  Value                   : full_access_as_user
                                },
                                ...}
    PasswordCredentials       : {}
    PublisherName             : 
    ReplyUrl                  : 
    SamlMetadataUrl           : 
    ServicePrincipalNames     : {00000002-0000-0ff1-ce00-000000000000/outlook.office365.com, 00000002-0000-0ff1-ce00-000000000000/mail.office365.com, 00000002-0000-0ff1-ce00-000000000000/outlook.com, 
                                00000002-0000-0ff1-ce00-000000000000/*.outlook.com...}
    Tags                      : {}

<span data-ttu-id="0a7a5-185">Zgoda jest inicjowane, gdy hello użytkownik kliknie przycisk "Akceptuj".</span><span class="sxs-lookup"><span data-stu-id="0a7a5-185">Consent is initiated when hello user clicks “Accept”.</span></span> <span data-ttu-id="0a7a5-186">Najpierw tworzony jest obiekt ServicePrincipal dla "FabrikamMail dla usługi Office 365" w dzierżawie powitalnych.</span><span class="sxs-lookup"><span data-stu-id="0a7a5-186">First, a ServicePrincipal object for “FabrikamMail for Office 365” is created in hello tenant.</span></span> <span data-ttu-id="0a7a5-187">Witaj ServicePrincipal wygląda następująco:</span><span class="sxs-lookup"><span data-stu-id="0a7a5-187">hello ServicePrincipal looks something like this:</span></span>

    PS C:\> Get-AzureADServicePrincipal -SearchString "FabrikamMail for Office 365" | fl *
    
    DeletionTimeStamp         : 
    ObjectId                  : a8b16333-851d-42e8-acd2-eac155849b37
    ObjectType                : ServicePrincipal
    AccountEnabled            : True
    AppDisplayName            : FabrikamMail for Office 365
    AppId                     : aba7c072-2267-4031-8960-e7a2db6e0590
    AppOwnerTenantId          : 4a4076e0-a70f-41c6-b819-6f9c4a86df89
    AppRoleAssignmentRequired : False
    AppRoles                  : {}
    DisplayName               : FabrikamMail for Office 365
    ErrorUrl                  : 
    Homepage                  : 
    KeyCredentials            : {}
    LogoutUrl                 : 
    Oauth2Permissions         : {}
    PasswordCredentials       : {}
    PublisherName             : Fabrikam, Inc.
    ReplyUrl                  : 
    SamlMetadataUrl           : 
    ServicePrincipalNames     : {aba7c072-2267-4031-8960-e7a2db6e0590}
    Tags                      : {WindowsAzureActiveDirectoryIntegratedApp}

<span data-ttu-id="0a7a5-188">Zgodę aplikacji tooan tworzy łącze Oauth2PermissionGrant hello następującego zakresu:</span><span class="sxs-lookup"><span data-stu-id="0a7a5-188">Consenting tooan app creates an Oauth2PermissionGrant link between hello following:</span></span>
  
- <span data-ttu-id="0a7a5-189">Witaj obiektu użytkownika</span><span class="sxs-lookup"><span data-stu-id="0a7a5-189">hello user object</span></span>
- <span data-ttu-id="0a7a5-190">aplikacje klienta Hello ServicePrincipalName (SPN)</span><span class="sxs-lookup"><span data-stu-id="0a7a5-190">hello client apps ServicePrincipalName (SPN)</span></span>
- <span data-ttu-id="0a7a5-191">aplikacje zasobów Hello ServicePrincipalName (SPN)</span><span class="sxs-lookup"><span data-stu-id="0a7a5-191">hello resource apps ServicePrincipalName (SPN)</span></span>
- <span data-ttu-id="0a7a5-192">uprawnienia w hello zasobów aplikacji.</span><span class="sxs-lookup"><span data-stu-id="0a7a5-192">permissions in hello resource app.</span></span>  

<span data-ttu-id="0a7a5-193">W przypadku hello FabrikamMail wygląda mniej więcej tak:</span><span class="sxs-lookup"><span data-stu-id="0a7a5-193">In hello case of FabrikamMail, it looks something like this:</span></span>

    PS C:\> Get-AzureADUserOAuth2PermissionGrant -ObjectId ddiggle@aadpremiumlab.onmicrosoft.com | fl *
    
    ClientId    : a8b16333-851d-42e8-acd2-eac155849b37
    ConsentType : Principal
    ExpiryTime  : 05/15/2017 07:02:39 AM
    ObjectId    : M2OxqB2F6EKs0urBVYSbN5d7PzhUZz1NlH25COvLocbJjoxkUFfRQauryBKwBWet
    PrincipalId : 648c8ec9-5750-41d1-abab-c812b00567ad
    ResourceId  : 383f7b97-6754-4d3d-9474-3908ebcba1c6
    Scope       : full_access_as_user
    StartTime   : 01/01/0001 12:00:00 AM

<span data-ttu-id="0a7a5-194">(**ClientId** jest identyfikator obiekt główny usługi przez FabrikamMail (hello, które utworzono właśnie), **PrincipalId** jest hello obiektu identyfikator użytkownika (hello użytkownika, który zgodę), **ResourceId**to usługa programu Exchange dla obiekt główny identyfikator zakresu jest hello uprawnień w programie Exchange, która została zgodę na).</span><span class="sxs-lookup"><span data-stu-id="0a7a5-194">(**ClientId** is FabrikamMail’s service principal object ID (hello one that just got created), **PrincipalId** is hello user object ID (of hello user who consented), **ResourceId** is Exchange’s service principal object ID, Scope is hello permission in Exchange that was consented to).</span></span>

<span data-ttu-id="0a7a5-195">Jeśli użytkownicy nie mogą tooconsent, zostanie wyświetlony ekran z informacją, że uprawnienie jest wymagane.</span><span class="sxs-lookup"><span data-stu-id="0a7a5-195">If users are not allowed tooconsent, they will see a screen that says that permission is required.</span></span>

