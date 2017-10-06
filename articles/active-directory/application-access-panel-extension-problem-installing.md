---
title: "Instalowanie rozszerzenia przeglądarki panelu dostępu do aplikacji hello aaaProblem | Dokumentacja firmy Microsoft"
description: "Jak toofix typowych błędów napotkanych podczas instalowania rozszerzenia przeglądarki panelu dostępu hello"
services: active-directory
documentationcenter: 
author: ajamess
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: asteen
ms.reviewer: japere
ms.openlocfilehash: 5f750d12c5f9b405ec4f81596d5cc5e0a48f9a62
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="problem-installing-hello-application-access-panel-browser-extension"></a><span data-ttu-id="1bc42-103">Problem podczas instalowania rozszerzenia przeglądarki panelu dostępu do aplikacji hello</span><span class="sxs-lookup"><span data-stu-id="1bc42-103">Problem installing hello application access panel browser extension</span></span>

<span data-ttu-id="1bc42-104">Witaj Panel dostępu jest oparte na sieci web portalu, co pozwoli na użytkownika mającego służbowe konto w usłudze Azure Active Directory (Azure AD) tooview, a następnie uruchom aplikacje oparte na chmurze administrator hello Azure AD udzielił im dostępu do.</span><span class="sxs-lookup"><span data-stu-id="1bc42-104">hello Access Panel is a web-based portal which enables a user who has a work or school account in Azure Active Directory (Azure AD) tooview and launch cloud-based applications that hello Azure AD administrator has granted them access to.</span></span> <span data-ttu-id="1bc42-105">Użytkownik, który ma wersje usługi Azure AD umożliwia także grupami samoobsługi i funkcje zarządzania aplikacjami za pośrednictwem hello panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="1bc42-105">A user who has Azure AD editions can also use self-service group and app management capabilities through hello Access Panel.</span></span> <span data-ttu-id="1bc42-106">Witaj Panel dostępu jest oddzielony od hello portalu Azure i nie wymaga toohave użytkownicy subskrypcji platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="1bc42-106">hello Access Panel is separate from hello Azure portal and does not require users toohave an Azure subscription.</span></span>

<span data-ttu-id="1bc42-107">toouse opartego na hasłach rejestracji jednokrotnej (SSO) w hello Panel dostępu, hello rozszerzenia Panelu dostępu należy zainstalować w przeglądarce użytkownika hello.</span><span class="sxs-lookup"><span data-stu-id="1bc42-107">toouse password-based single sign-on (SSO) in hello Access Panel, hello Access Panel extension must be installed in hello user’s browser.</span></span> <span data-ttu-id="1bc42-108">To rozszerzenie jest pobierany automatycznie, gdy użytkownik wybierze aplikacji, która jest skonfigurowana do opartego na hasłach logowania jednokrotnego.</span><span class="sxs-lookup"><span data-stu-id="1bc42-108">This extension is downloaded automatically when a user selects an application that is configured for password-based SSO.</span></span>

## <a name="meeting-browser-requirements-for-hello-access-panel"></a><span data-ttu-id="1bc42-109">Spełnia wymagania dotyczące przeglądarki dla hello panelu dostępu</span><span class="sxs-lookup"><span data-stu-id="1bc42-109">Meeting browser requirements for hello Access Panel</span></span>

<span data-ttu-id="1bc42-110">Witaj panelu dostępu wymaga przeglądarki obsługującej JavaScript i włączył CSS.</span><span class="sxs-lookup"><span data-stu-id="1bc42-110">hello Access Panel requires a browser that supports JavaScript and has CSS enabled.</span></span> <span data-ttu-id="1bc42-111">toouse opartego na hasłach rejestracji jednokrotnej (SSO) w hello Panel dostępu, hello rozszerzenia Panelu dostępu należy zainstalować w przeglądarce użytkownika hello.</span><span class="sxs-lookup"><span data-stu-id="1bc42-111">toouse password-based single sign-on (SSO) in hello Access Panel, hello Access Panel extension must be installed in hello user’s browser.</span></span> <span data-ttu-id="1bc42-112">To rozszerzenie jest pobierany automatycznie, gdy użytkownik wybierze aplikacji, która jest skonfigurowana do opartego na hasłach logowania jednokrotnego.</span><span class="sxs-lookup"><span data-stu-id="1bc42-112">This extension is downloaded automatically when a user selects an application that is configured for password-based SSO.</span></span>

<span data-ttu-id="1bc42-113">Logowanie Jednokrotne opartego na hasłach można przeglądarki hello przez użytkownika końcowego:</span><span class="sxs-lookup"><span data-stu-id="1bc42-113">For password-based SSO, hello end user’s browsers can be:</span></span>

-   <span data-ttu-id="1bc42-114">Internet Explorer 8, 9, 10, 11 — w systemie Windows 7 lub nowszy</span><span class="sxs-lookup"><span data-stu-id="1bc42-114">Internet Explorer 8, 9, 10, 11 -- on Windows 7 or later</span></span>

-   <span data-ttu-id="1bc42-115">Krawędź w systemie Windows 10 Anniversary Edition lub nowszy</span><span class="sxs-lookup"><span data-stu-id="1bc42-115">Edge on Windows 10 Anniversary Edition or later</span></span> 

-   <span data-ttu-id="1bc42-116">Chrome — W systemie Windows 7 lub nowszy oraz System MacOS x lub nowszych</span><span class="sxs-lookup"><span data-stu-id="1bc42-116">Chrome -- on Windows 7 or later, and on MacOS X or later</span></span>

-   <span data-ttu-id="1bc42-117">Firefox 26.0 lub później — w systemie Windows XP z dodatkiem SP2 lub nowszy oraz w systemie Mac OS X 10,6 lub nowszy</span><span class="sxs-lookup"><span data-stu-id="1bc42-117">Firefox 26.0 or later -- on Windows XP SP2 or later, and on Mac OS X 10.6 or later</span></span>

## <a name="how-tooinstall-hello-access-panel-browser-extension"></a><span data-ttu-id="1bc42-118">Jak tooinstall hello rozszerzenia przeglądarki panelu dostępu</span><span class="sxs-lookup"><span data-stu-id="1bc42-118">How tooinstall hello Access Panel Browser extension</span></span>

<span data-ttu-id="1bc42-119">hello tooinstall rozszerzenia przeglądarki panelu dostępu, wykonaj poniższe kroki hello:</span><span class="sxs-lookup"><span data-stu-id="1bc42-119">tooinstall hello Access Panel Browser extension, follow hello steps below:</span></span>

1.  <span data-ttu-id="1bc42-120">Otwórz hello [panelu dostępu](https://myapps.microsoft.com) w jednym z hello obsługiwane przeglądarki i zaloguj się jako **użytkownika** w usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="1bc42-120">Open hello [Access Panel](https://myapps.microsoft.com) in one of hello supported browsers and sign in as a **user** in your Azure AD.</span></span>

2.  <span data-ttu-id="1bc42-121">Kliknij przycisk **logowania jednokrotnego hasła aplikacji** w hello panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="1bc42-121">Click a **password-SSO application** in hello Access Panel.</span></span>

3.  <span data-ttu-id="1bc42-122">Hello monitu pytaniem tooinstall hello oprogramowania, zaznaczyć **Zainstaluj teraz**.</span><span class="sxs-lookup"><span data-stu-id="1bc42-122">In hello prompt asking tooinstall hello software, select **Install Now**.</span></span>

4.  <span data-ttu-id="1bc42-123">Oparte na przeglądarce można ukierunkowanej toohello łącze.</span><span class="sxs-lookup"><span data-stu-id="1bc42-123">Based on your browser you be directed toohello download link.</span></span> <span data-ttu-id="1bc42-124">**Dodaj** hello rozszerzenia tooyour przeglądarki.</span><span class="sxs-lookup"><span data-stu-id="1bc42-124">**Add** hello extension tooyour browser.</span></span>

5.  <span data-ttu-id="1bc42-125">Jeśli przeglądarka pytanie, wybierz tooeither **włączyć** lub **Zezwalaj** hello rozszerzenia.</span><span class="sxs-lookup"><span data-stu-id="1bc42-125">If your browser asks, select tooeither **Enable** or **Allow** hello extension.</span></span>

6.  <span data-ttu-id="1bc42-126">Wcześniej zainstalowano **ponowne uruchomienie** sesji przeglądarki.</span><span class="sxs-lookup"><span data-stu-id="1bc42-126">Once installed, **restart** your browser session.</span></span>

7.  <span data-ttu-id="1bc42-127">Zaloguj się do hello panelu dostępu i zobacz, czy można **uruchamianie** logowania jednokrotnego hasła aplikacji</span><span class="sxs-lookup"><span data-stu-id="1bc42-127">Sign in into hello Access Panel and see if you can **launch** your password-SSO applications</span></span>

<span data-ttu-id="1bc42-128">Może również pobrać hello rozszerzenia dla programu Chrome i krawędzi, z poniższe linki bezpośrednie hello:</span><span class="sxs-lookup"><span data-stu-id="1bc42-128">You may also download hello extension for Chrome and Edge from hello direct links below:</span></span>

-   [<span data-ttu-id="1bc42-129">Rozszerzenie panelu dostępu Chrome</span><span class="sxs-lookup"><span data-stu-id="1bc42-129">Chrome Access Panel Extension</span></span>](https://chrome.google.com/webstore/detail/access-panel-extension/ggjhpefgjjfobnfoldnjipclpcfbgbhl)

-   [<span data-ttu-id="1bc42-130">Rozszerzenie panelu dostępu krawędzi</span><span class="sxs-lookup"><span data-stu-id="1bc42-130">Edge Access Panel Extension</span></span>](https://www.microsoft.com/store/apps/9pc9sckkzk84) 

## <a name="setting-up-a-group-policy-for-internet-explorer"></a><span data-ttu-id="1bc42-131">Konfigurowanie zasad grupy dla programu Internet Explorer</span><span class="sxs-lookup"><span data-stu-id="1bc42-131">Setting up a group policy for Internet Explorer</span></span>

<span data-ttu-id="1bc42-132">Możesz skonfigurować zasady grupy, które pozwalają tooremotely instalacji hello panelu dostępu rozszerzenie programu Internet Explorer na komputerach użytkowników.</span><span class="sxs-lookup"><span data-stu-id="1bc42-132">You can setup a group policy that allow you tooremotely install hello Access Panel extension for Internet Explorer on your users' machines.</span></span>

<span data-ttu-id="1bc42-133">wymagania wstępne Hello obejmują:</span><span class="sxs-lookup"><span data-stu-id="1bc42-133">hello prerequisites include:</span></span>

-   <span data-ttu-id="1bc42-134">Po skonfigurowaniu [usług domenowych w usłudze Active Directory](https://msdn.microsoft.com/library/aa362244%28v=vs.85%29.aspx), i mieć przyłączone do domeny tooyour maszyny użytkowników.</span><span class="sxs-lookup"><span data-stu-id="1bc42-134">You have set up [Active Directory Domain Services](https://msdn.microsoft.com/library/aa362244%28v=vs.85%29.aspx), and you have joined your users' machines tooyour domain.</span></span>

-   <span data-ttu-id="1bc42-135">Musi mieć hello "Edytuj ustawienia" uprawnień tooedit hello obiektu zasad grupy (GPO).</span><span class="sxs-lookup"><span data-stu-id="1bc42-135">You must have hello "Edit settings" permission tooedit hello Group Policy Object (GPO).</span></span> <span data-ttu-id="1bc42-136">Domyślnie to uprawnienie mają członkowie hello następujących grup zabezpieczeń: Administratorzy domeny, Administratorzy przedsiębiorstwa oraz Twórcy-właściciele zasad grupy.</span><span class="sxs-lookup"><span data-stu-id="1bc42-136">By default, members of hello following security groups have this permission: Domain Administrators, Enterprise Administrators, and Group Policy Creator Owners.</span></span> <span data-ttu-id="1bc42-137">[Dowiedz się więcej](https://technet.microsoft.com/library/cc781991%28v=ws.10%29.aspx).</span><span class="sxs-lookup"><span data-stu-id="1bc42-137">[Learn more](https://technet.microsoft.com/library/cc781991%28v=ws.10%29.aspx).</span></span>

<span data-ttu-id="1bc42-138">Czynności opisane w samouczku hello [jak tooDeploy hello rozszerzenia Panel dostępu dla programu Internet Explorer przy użyciu zasad grupy](active-directory-saas-ie-group-policy.md) instrukcje krok po kroku dotyczące sposobu tooconfigure hello zasad grupy i wdróż je toousers.</span><span class="sxs-lookup"><span data-stu-id="1bc42-138">Follow hello tutorial [How tooDeploy hello Access Panel Extension for Internet Explorer using Group Policy](active-directory-saas-ie-group-policy.md) for step by step instructions on how tooconfigure hello group policy and deploy it toousers.</span></span>

## <a name="troubleshoot-hello-access-panel-in-internet-explorer"></a><span data-ttu-id="1bc42-139">Rozwiązywanie problemów z hello panelu dostępu w programie Internet Explorer</span><span class="sxs-lookup"><span data-stu-id="1bc42-139">Troubleshoot hello Access Panel in Internet Explorer</span></span>

<span data-ttu-id="1bc42-140">Wykonaj hello [rozwiązywanie hello rozszerzenia Panel dostępu dla programu Internet Explorer](active-directory-saas-ie-troubleshooting.md) przewodnik dostępu narzędzia diagnostycznego i instrukcje krok po kroku dotyczące konfigurowania hello rozszerzenia dla programu Internet Explorer.</span><span class="sxs-lookup"><span data-stu-id="1bc42-140">Follow hello [Troubleshoot hello Access Panel Extension for Internet Explorer](active-directory-saas-ie-troubleshooting.md) guide for access a diagnostics tool and step by step instructions on configuring hello extension for IE.</span></span>

## <a name="if-these-troubleshooting-steps-do-not-resolve-hello-issue"></a><span data-ttu-id="1bc42-141">Jeśli te kroki rozwiązywania problemów nie rozwiąże problemu hello</span><span class="sxs-lookup"><span data-stu-id="1bc42-141">If these troubleshooting steps do not resolve hello issue</span></span>

<span data-ttu-id="1bc42-142">Otwórz bilet pomocy technicznej z następujących informacji, jeśli jest dostępna hello:</span><span class="sxs-lookup"><span data-stu-id="1bc42-142">open a support ticket with hello following information if available:</span></span>

-   <span data-ttu-id="1bc42-143">Identyfikator błędu korelacji</span><span class="sxs-lookup"><span data-stu-id="1bc42-143">Correlation error ID</span></span>

-   <span data-ttu-id="1bc42-144">Nazwa UPN (adres e-mail użytkownika)</span><span class="sxs-lookup"><span data-stu-id="1bc42-144">UPN (user email address)</span></span>

-   <span data-ttu-id="1bc42-145">Dla identyfikatora dzierżawcy</span><span class="sxs-lookup"><span data-stu-id="1bc42-145">TenantID</span></span>

-   <span data-ttu-id="1bc42-146">Typ przeglądarki</span><span class="sxs-lookup"><span data-stu-id="1bc42-146">Browser type</span></span>

-   <span data-ttu-id="1bc42-147">Strefa czasowa i przedziału czasu/czasu podczas błąd występuje</span><span class="sxs-lookup"><span data-stu-id="1bc42-147">Time zone and time/timeframe during error occurs</span></span>

-   <span data-ttu-id="1bc42-148">Ślady fiddler</span><span class="sxs-lookup"><span data-stu-id="1bc42-148">Fiddler traces</span></span>

## <a name="next-steps"></a><span data-ttu-id="1bc42-149">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="1bc42-149">Next steps</span></span>
[<span data-ttu-id="1bc42-150">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="1bc42-150">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)
