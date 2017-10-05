---
title: "Problem podczas instalowania aplikacji dostępu panelu rozszerzenia przeglądarki | Dokumentacja firmy Microsoft"
description: "Jak rozwiązywać typowe błędy podczas instalowania rozszerzenia przeglądarki panelu dostępu"
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
ms.openlocfilehash: 8b7327508633e33917d1fa9c1f35ed1bde5a26e1
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/03/2017
---
# <a name="problem-installing-the-application-access-panel-browser-extension"></a><span data-ttu-id="6ac70-103">Problem podczas instalowania aplikacji dostępu panelu rozszerzenia przeglądarki</span><span class="sxs-lookup"><span data-stu-id="6ac70-103">Problem installing the application access panel browser extension</span></span>

<span data-ttu-id="6ac70-104">Panel dostępu jest widok, a następnie uruchom chmurowych aplikacji, które administrator usługi Azure AD udzielił im dostępu do portalu sieci web, dzięki czemu użytkownik, który ma konto służbowe w usłudze Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="6ac70-104">The Access Panel is a web-based portal which enables a user who has a work or school account in Azure Active Directory (Azure AD) to view and launch cloud-based applications that the Azure AD administrator has granted them access to.</span></span> <span data-ttu-id="6ac70-105">Użytkownik, który ma wersje usługi Azure AD umożliwia także grupami samoobsługi i funkcje zarządzania aplikacjami za pomocą panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="6ac70-105">A user who has Azure AD editions can also use self-service group and app management capabilities through the Access Panel.</span></span> <span data-ttu-id="6ac70-106">Panel dostępu jest oddzielony od portalu Azure i nie wymaga użytkownikom posiadania subskrypcji platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="6ac70-106">The Access Panel is separate from the Azure portal and does not require users to have an Azure subscription.</span></span>

<span data-ttu-id="6ac70-107">Aby użyć opartego na hasłach rejestracji jednokrotnej (SSO) w panelu dostępu, rozszerzenia Panelu dostępu musi być zainstalowany w przeglądarce.</span><span class="sxs-lookup"><span data-stu-id="6ac70-107">To use password-based single sign-on (SSO) in the Access Panel, the Access Panel extension must be installed in the user’s browser.</span></span> <span data-ttu-id="6ac70-108">To rozszerzenie jest pobierany automatycznie, gdy użytkownik wybierze aplikacji, która jest skonfigurowana do opartego na hasłach logowania jednokrotnego.</span><span class="sxs-lookup"><span data-stu-id="6ac70-108">This extension is downloaded automatically when a user selects an application that is configured for password-based SSO.</span></span>

## <a name="meeting-browser-requirements-for-the-access-panel"></a><span data-ttu-id="6ac70-109">Spełniające wymagania przeglądarki do panelu dostępu</span><span class="sxs-lookup"><span data-stu-id="6ac70-109">Meeting browser requirements for the Access Panel</span></span>

<span data-ttu-id="6ac70-110">Panel dostępu wymaga przeglądarki obsługującej JavaScript i włączył CSS.</span><span class="sxs-lookup"><span data-stu-id="6ac70-110">The Access Panel requires a browser that supports JavaScript and has CSS enabled.</span></span> <span data-ttu-id="6ac70-111">Aby użyć opartego na hasłach rejestracji jednokrotnej (SSO) w panelu dostępu, rozszerzenia Panelu dostępu musi być zainstalowany w przeglądarce.</span><span class="sxs-lookup"><span data-stu-id="6ac70-111">To use password-based single sign-on (SSO) in the Access Panel, the Access Panel extension must be installed in the user’s browser.</span></span> <span data-ttu-id="6ac70-112">To rozszerzenie jest pobierany automatycznie, gdy użytkownik wybierze aplikacji, która jest skonfigurowana do opartego na hasłach logowania jednokrotnego.</span><span class="sxs-lookup"><span data-stu-id="6ac70-112">This extension is downloaded automatically when a user selects an application that is configured for password-based SSO.</span></span>

<span data-ttu-id="6ac70-113">Logowanie Jednokrotne opartego na hasłach można przeglądarki przez użytkownika końcowego:</span><span class="sxs-lookup"><span data-stu-id="6ac70-113">For password-based SSO, the end user’s browsers can be:</span></span>

-   <span data-ttu-id="6ac70-114">Internet Explorer 8, 9, 10, 11 — w systemie Windows 7 lub nowszy</span><span class="sxs-lookup"><span data-stu-id="6ac70-114">Internet Explorer 8, 9, 10, 11 -- on Windows 7 or later</span></span>

-   <span data-ttu-id="6ac70-115">Krawędź w systemie Windows 10 Anniversary Edition lub nowszy</span><span class="sxs-lookup"><span data-stu-id="6ac70-115">Edge on Windows 10 Anniversary Edition or later</span></span> 

-   <span data-ttu-id="6ac70-116">Chrome — W systemie Windows 7 lub nowszy oraz System MacOS x lub nowszych</span><span class="sxs-lookup"><span data-stu-id="6ac70-116">Chrome -- on Windows 7 or later, and on MacOS X or later</span></span>

-   <span data-ttu-id="6ac70-117">Firefox 26.0 lub później — w systemie Windows XP z dodatkiem SP2 lub nowszy oraz w systemie Mac OS X 10,6 lub nowszy</span><span class="sxs-lookup"><span data-stu-id="6ac70-117">Firefox 26.0 or later -- on Windows XP SP2 or later, and on Mac OS X 10.6 or later</span></span>

## <a name="how-to-install-the-access-panel-browser-extension"></a><span data-ttu-id="6ac70-118">Jak zainstalować rozszerzenie przeglądarki panelu dostępu</span><span class="sxs-lookup"><span data-stu-id="6ac70-118">How to install the Access Panel Browser extension</span></span>

<span data-ttu-id="6ac70-119">Aby zainstalować rozszerzenie przeglądarki panelu dostępu, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="6ac70-119">To install the Access Panel Browser extension, follow the steps below:</span></span>

1.  <span data-ttu-id="6ac70-120">Otwórz [panelu dostępu](https://myapps.microsoft.com) w jednym z obsługiwanych przeglądarkach i zaloguj się jako **użytkownika** w usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="6ac70-120">Open the [Access Panel](https://myapps.microsoft.com) in one of the supported browsers and sign in as a **user** in your Azure AD.</span></span>

2.  <span data-ttu-id="6ac70-121">Kliknij przycisk **logowania jednokrotnego hasła aplikacji** w panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="6ac70-121">Click a **password-SSO application** in the Access Panel.</span></span>

3.  <span data-ttu-id="6ac70-122">W oknie komunikatu z pytaniem do zainstalowania oprogramowania, zaznaczyć **Zainstaluj teraz**.</span><span class="sxs-lookup"><span data-stu-id="6ac70-122">In the prompt asking to install the software, select **Install Now**.</span></span>

4.  <span data-ttu-id="6ac70-123">Oparte na przeglądarce być kierowane do łącza pobierania.</span><span class="sxs-lookup"><span data-stu-id="6ac70-123">Based on your browser you be directed to the download link.</span></span> <span data-ttu-id="6ac70-124">**Dodaj** rozszerzenia do przeglądarki.</span><span class="sxs-lookup"><span data-stu-id="6ac70-124">**Add** the extension to your browser.</span></span>

5.  <span data-ttu-id="6ac70-125">Jeśli przeglądarka pytanie, wybierz albo **włączyć** lub **Zezwalaj** rozszerzenia.</span><span class="sxs-lookup"><span data-stu-id="6ac70-125">If your browser asks, select to either **Enable** or **Allow** the extension.</span></span>

6.  <span data-ttu-id="6ac70-126">Wcześniej zainstalowano **ponowne uruchomienie** sesji przeglądarki.</span><span class="sxs-lookup"><span data-stu-id="6ac70-126">Once installed, **restart** your browser session.</span></span>

7.  <span data-ttu-id="6ac70-127">Zaloguj się do panelu dostępu i zobacz, czy można **uruchamianie** logowania jednokrotnego hasła aplikacji</span><span class="sxs-lookup"><span data-stu-id="6ac70-127">Sign in into the Access Panel and see if you can **launch** your password-SSO applications</span></span>

<span data-ttu-id="6ac70-128">Może również pobrać rozszerzenia dla programu Chrome i krawędzi z bezpośrednich łączy poniżej:</span><span class="sxs-lookup"><span data-stu-id="6ac70-128">You may also download the extension for Chrome and Edge from the direct links below:</span></span>

-   [<span data-ttu-id="6ac70-129">Rozszerzenie panelu dostępu Chrome</span><span class="sxs-lookup"><span data-stu-id="6ac70-129">Chrome Access Panel Extension</span></span>](https://chrome.google.com/webstore/detail/access-panel-extension/ggjhpefgjjfobnfoldnjipclpcfbgbhl)

-   [<span data-ttu-id="6ac70-130">Rozszerzenie panelu dostępu krawędzi</span><span class="sxs-lookup"><span data-stu-id="6ac70-130">Edge Access Panel Extension</span></span>](https://www.microsoft.com/store/apps/9pc9sckkzk84) 

## <a name="setting-up-a-group-policy-for-internet-explorer"></a><span data-ttu-id="6ac70-131">Konfigurowanie zasad grupy dla programu Internet Explorer</span><span class="sxs-lookup"><span data-stu-id="6ac70-131">Setting up a group policy for Internet Explorer</span></span>

<span data-ttu-id="6ac70-132">Możesz skonfigurować zasady grupy, które umożliwiają zdalnie zainstalować rozszerzenie Panel dostępu dla programu Internet Explorer na komputerach użytkowników.</span><span class="sxs-lookup"><span data-stu-id="6ac70-132">You can setup a group policy that allow you to remotely install the Access Panel extension for Internet Explorer on your users' machines.</span></span>

<span data-ttu-id="6ac70-133">Wymagania wstępne należą:</span><span class="sxs-lookup"><span data-stu-id="6ac70-133">The prerequisites include:</span></span>

-   <span data-ttu-id="6ac70-134">Po skonfigurowaniu [usług domenowych w usłudze Active Directory](https://msdn.microsoft.com/library/aa362244%28v=vs.85%29.aspx), i dołączeniu komputerów użytkowników do domeny.</span><span class="sxs-lookup"><span data-stu-id="6ac70-134">You have set up [Active Directory Domain Services](https://msdn.microsoft.com/library/aa362244%28v=vs.85%29.aspx), and you have joined your users' machines to your domain.</span></span>

-   <span data-ttu-id="6ac70-135">Musi mieć uprawnienie "Edytuj ustawienia" do edycji obiektu zasad grupy (GPO).</span><span class="sxs-lookup"><span data-stu-id="6ac70-135">You must have the "Edit settings" permission to edit the Group Policy Object (GPO).</span></span> <span data-ttu-id="6ac70-136">Domyślnie to uprawnienie mają członków z następujących grup zabezpieczeń: Administratorzy domeny, Administratorzy przedsiębiorstwa oraz Twórcy-właściciele zasad grupy.</span><span class="sxs-lookup"><span data-stu-id="6ac70-136">By default, members of the following security groups have this permission: Domain Administrators, Enterprise Administrators, and Group Policy Creator Owners.</span></span> <span data-ttu-id="6ac70-137">[Dowiedz się więcej](https://technet.microsoft.com/library/cc781991%28v=ws.10%29.aspx).</span><span class="sxs-lookup"><span data-stu-id="6ac70-137">[Learn more](https://technet.microsoft.com/library/cc781991%28v=ws.10%29.aspx).</span></span>

<span data-ttu-id="6ac70-138">Czynności opisane w samouczku [wdrażanie rozszerzenia Panel dostępu dla programu Internet Explorer przy użyciu zasad grupy](active-directory-saas-ie-group-policy.md) instrukcje krok po kroku dotyczące sposobu konfigurowania zasad grupy oraz wdrażanie dla użytkowników.</span><span class="sxs-lookup"><span data-stu-id="6ac70-138">Follow the tutorial [How to Deploy the Access Panel Extension for Internet Explorer using Group Policy](active-directory-saas-ie-group-policy.md) for step by step instructions on how to configure the group policy and deploy it to users.</span></span>

## <a name="troubleshoot-the-access-panel-in-internet-explorer"></a><span data-ttu-id="6ac70-139">Rozwiązywanie problemów z panelu dostępu w programie Internet Explorer</span><span class="sxs-lookup"><span data-stu-id="6ac70-139">Troubleshoot the Access Panel in Internet Explorer</span></span>

<span data-ttu-id="6ac70-140">Postępuj zgodnie z [Rozwiązywanie problemów z rozszerzeniem Panel dostępu dla programu Internet Explorer](active-directory-saas-ie-troubleshooting.md) przewodnik dostępu narzędzia diagnostycznego i instrukcje krok po kroku dotyczące konfigurowania rozszerzenia dla programu Internet Explorer.</span><span class="sxs-lookup"><span data-stu-id="6ac70-140">Follow the [Troubleshoot the Access Panel Extension for Internet Explorer](active-directory-saas-ie-troubleshooting.md) guide for access a diagnostics tool and step by step instructions on configuring the extension for IE.</span></span>

## <a name="if-these-troubleshooting-steps-do-not-resolve-the-issue"></a><span data-ttu-id="6ac70-141">Jeśli te kroki rozwiązywania problemów nie rozwiąże problemu</span><span class="sxs-lookup"><span data-stu-id="6ac70-141">If these troubleshooting steps do not resolve the issue</span></span>

<span data-ttu-id="6ac70-142">Otwórz bilet pomocy technicznej następujące informacje, jeśli są dostępne:</span><span class="sxs-lookup"><span data-stu-id="6ac70-142">open a support ticket with the following information if available:</span></span>

-   <span data-ttu-id="6ac70-143">Identyfikator błędu korelacji</span><span class="sxs-lookup"><span data-stu-id="6ac70-143">Correlation error ID</span></span>

-   <span data-ttu-id="6ac70-144">Nazwa UPN (adres e-mail użytkownika)</span><span class="sxs-lookup"><span data-stu-id="6ac70-144">UPN (user email address)</span></span>

-   <span data-ttu-id="6ac70-145">Dla identyfikatora dzierżawcy</span><span class="sxs-lookup"><span data-stu-id="6ac70-145">TenantID</span></span>

-   <span data-ttu-id="6ac70-146">Typ przeglądarki</span><span class="sxs-lookup"><span data-stu-id="6ac70-146">Browser type</span></span>

-   <span data-ttu-id="6ac70-147">Strefa czasowa i przedziału czasu/czasu podczas błąd występuje</span><span class="sxs-lookup"><span data-stu-id="6ac70-147">Time zone and time/timeframe during error occurs</span></span>

-   <span data-ttu-id="6ac70-148">Ślady fiddler</span><span class="sxs-lookup"><span data-stu-id="6ac70-148">Fiddler traces</span></span>

## <a name="next-steps"></a><span data-ttu-id="6ac70-149">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="6ac70-149">Next steps</span></span>
[<span data-ttu-id="6ac70-150">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="6ac70-150">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)
