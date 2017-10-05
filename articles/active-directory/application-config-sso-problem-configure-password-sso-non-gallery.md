---
title: "Problem podczas konfiguracji hasła logowanie jednokrotne dla aplikacji z systemem innym niż galerii | Dokumentacja firmy Microsoft"
description: "Zrozumienie kroju osób typowe problemy podczas konfigurowania haseł logowanie jednokrotne dla aplikacji z systemem innym niż galerii niestandardowych, które nie są wymienione w galerii aplikacji usługi Azure AD"
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
ms.openlocfilehash: 9c76b6f3495e2dd759a156fcef97b57aece8d632
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/03/2017
---
# <a name="problem-configuring-password-single-sign-on-for-a-non-gallery-application"></a><span data-ttu-id="a7795-103">Problem podczas konfiguracji hasła logowanie jednokrotne dla aplikacji z systemem innym niż galerii</span><span class="sxs-lookup"><span data-stu-id="a7795-103">Problem configuring password single sign-on for a non-gallery application</span></span>

<span data-ttu-id="a7795-104">Ten artykuł ułatwia zrozumienie kroju osób typowe problemy podczas konfigurowania **hasło logowania jednokrotnego** z aplikacji innych niż galerii.</span><span class="sxs-lookup"><span data-stu-id="a7795-104">This article help you to understand the common problems people face when configuring **Password single sign-on** with a non-gallery application.</span></span>

## <a name="how-to-capture-sign-in-fields-for-an-application"></a><span data-ttu-id="a7795-105">Jak przechwycić pola logowania dla aplikacji</span><span class="sxs-lookup"><span data-stu-id="a7795-105">How to capture sign-in fields for an application</span></span>

<span data-ttu-id="a7795-106">Przechwytywanie pola logowania jest obsługiwana tylko dla komputerów z obsługą HTML strony logowania i jest **nie jest obsługiwane dla niestandardowych stron logowania**, takich jak implementacje używające Flash i inne technologie włączone HTML.</span><span class="sxs-lookup"><span data-stu-id="a7795-106">Sign-in field capture is only supported for HTML-enabled sign-in pages and is **not supported for non-standard sign-in pages**, like those that use Flash, or other non-HTML-enabled technologies.</span></span>

<span data-ttu-id="a7795-107">Istnieją dwa sposoby, można przechwytywać logowania pól niestandardowych aplikacji:</span><span class="sxs-lookup"><span data-stu-id="a7795-107">There are two ways you can capture sign-in fields for your custom applications:</span></span>

-   <span data-ttu-id="a7795-108">Automatyczne logowanie pola przechwytywania</span><span class="sxs-lookup"><span data-stu-id="a7795-108">Automatic sign-in field capture</span></span>

-   <span data-ttu-id="a7795-109">Ręczne znaku w polu przechwytywania</span><span class="sxs-lookup"><span data-stu-id="a7795-109">Manual sign-in field capture</span></span>

<span data-ttu-id="a7795-110">**Automatyczne logowanie pola przechwytywania** działa prawidłowo w przypadku większości włączone HTML strony logowania, jeśli używają one **dobrze znane identyfikatory DIV o nazwę użytkownika i hasło, wprowadź** pola.</span><span class="sxs-lookup"><span data-stu-id="a7795-110">**Automatic sign-in field capture** works well with most HTML-enabled sign-in pages, if they use **well-known DIV IDs for the username and password input** field.</span></span> <span data-ttu-id="a7795-111">To działania jest oskrobaniu HTML na stronie, aby znaleźć identyfikatory DIV, spełniających określone kryteria, a następnie zapisywania tych metadanych dla tej aplikacji, można odtwarzana hasła do niego później.</span><span class="sxs-lookup"><span data-stu-id="a7795-111">The way this works is by scraping the HTML on the page to find DIV IDs that match certain criteria and by then saving that metadata for this application so we can replay passwords to it later.</span></span>

<span data-ttu-id="a7795-112">**Ręczne znaku w polu przechwytywania** mogą być używane w przypadku który aplikacji **dostawcy nie etykietę** pole wejściowe, używane w celu logowania się.</span><span class="sxs-lookup"><span data-stu-id="a7795-112">**Manual sign-in field capture** can be used in the case that the application **vendor does not label** the input fields used for sign in.</span></span> <span data-ttu-id="a7795-113">Ręczne znaku w polu przechwytywania można również w przypadku gdy **dostawcy renderuje wielu pól** co nie może być wykrywane automatycznie.</span><span class="sxs-lookup"><span data-stu-id="a7795-113">Manual sign-in field capture can also be used in the case when the **vendor renders multiple fields** which cannot be auto-detected.</span></span> <span data-ttu-id="a7795-114">Usługi Azure AD można przechowywać dane jako wiele pól znajdują się na stronie logowania, tak długo, jak możesz Napisz, których te pola są na stronie.</span><span class="sxs-lookup"><span data-stu-id="a7795-114">Azure AD can store data for as many fields as are on the sign in page, so long as you tell us where those fields are on the page.</span></span>

<span data-ttu-id="a7795-115">Ogólnie rzecz biorąc **Jeśli pole automatycznego logowania przechwytywania nie działa, zawsze zalecamy opcja ręcznego w trakcie.**</span><span class="sxs-lookup"><span data-stu-id="a7795-115">In general, **if automatic sign-in field capture does not work, we always suggest trying the manual option.**</span></span>

### <a name="how-to-automatically-capture-sign-in-fields-for-an-application"></a><span data-ttu-id="a7795-116">Automatycznie Przechwytywanie pola logowania dla aplikacji</span><span class="sxs-lookup"><span data-stu-id="a7795-116">How to automatically capture sign-in fields for an application</span></span>

<span data-ttu-id="a7795-117">Aby skonfigurować **opartego na hasłach rejestracji jednokrotnej** dla aplikacji przy użyciu **przechwytywania automatycznego logowania pola**, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="a7795-117">To configure **Password-based Single Sign-on** for an application using **automatic sign-in field capture**, follow the steps below:</span></span>

1.  <span data-ttu-id="a7795-118">Otwórz [ **Azure Portal** ](https://portal.azure.com/) i zaloguj się jako **administratora globalnego** lub **ko-administratora.**</span><span class="sxs-lookup"><span data-stu-id="a7795-118">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="a7795-119">Otwórz **rozszerzenia usług Azure Active Directory** klikając **więcej usług** u dołu menu nawigacji głównego po lewej stronie.</span><span class="sxs-lookup"><span data-stu-id="a7795-119">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="a7795-120">Wpisz w **"Azure Active Directory**" w polu wyszukiwania filtr a wybierz **usługi Azure Active Directory** elementu.</span><span class="sxs-lookup"><span data-stu-id="a7795-120">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="a7795-121">Kliknij przycisk **aplikacje dla przedsiębiorstw** w menu nawigacji po lewej stronie usługi Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="a7795-121">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="a7795-122">Kliknij przycisk **wszystkie aplikacje** Aby wyświetlić listę wszystkich aplikacji.</span><span class="sxs-lookup"><span data-stu-id="a7795-122">click **All Applications** to view a list of all your applications.</span></span>

  * <span data-ttu-id="a7795-123">Jeśli nie ma aplikacji ma tutaj będą wyświetlane, użyj **filtru** kontroli nad **listę wszystkich aplikacji** i ustaw **Pokaż** opcji w celu **wszystkich aplikacji.**</span><span class="sxs-lookup"><span data-stu-id="a7795-123">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="a7795-124">Wybierz aplikację, aby skonfigurować logowanie jednokrotne.</span><span class="sxs-lookup"><span data-stu-id="a7795-124">Select the application you want to configure single sign-on.</span></span>

7.  <span data-ttu-id="a7795-125">Po załadowaniu aplikacji, kliknij przycisk **logowanie jednokrotne** z menu nawigacji po lewej stronie aplikacji.</span><span class="sxs-lookup"><span data-stu-id="a7795-125">Once the application loads, click the **Single sign-on** from the application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="a7795-126">Wybierz tryb **opartego na hasłach logowania jednokrotnego.**</span><span class="sxs-lookup"><span data-stu-id="a7795-126">Select the mode **Password-based Sign-on.**</span></span>

9.  <span data-ttu-id="a7795-127">Wprowadź **adres URL logowania**.</span><span class="sxs-lookup"><span data-stu-id="a7795-127">Enter the **Sign-on URL**.</span></span> <span data-ttu-id="a7795-128">Jest to adres URL, których użytkownicy wprowadzić swoją nazwę i hasło do logowania się na.</span><span class="sxs-lookup"><span data-stu-id="a7795-128">This is the URL where users enter their username and password to sign in to.</span></span> <span data-ttu-id="a7795-129">**Upewnij się, logowania pola są widoczne w adresie URL, musisz podać**.</span><span class="sxs-lookup"><span data-stu-id="a7795-129">**Ensure the sign in fields are visible at the URL you provide**.</span></span>

10. <span data-ttu-id="a7795-130">Kliknij przycisk **Zapisz**.</span><span class="sxs-lookup"><span data-stu-id="a7795-130">Click the **Save** button.</span></span>

11. <span data-ttu-id="a7795-131">Po wykonaniu tej czynności, firma Microsoft będzie automatycznie scrape tego adresu URL dla nazwy użytkownika i hasło pole wprowadzania i umożliwiają używanie usługi Azure AD do bezpiecznego przesyłania hasła do tej aplikacji przy użyciu rozszerzenia przeglądarki panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="a7795-131">Once you do that, we’ll automatically scrape that URL for a username and password input box and allow you to use Azure AD to securely transmit passwords to that application using the access panel browser extension.</span></span>

## <a name="how-to-manually-capture-sign-in-fields-for-an-application"></a><span data-ttu-id="a7795-132">Ręcznie Przechwytywanie pola logowania dla aplikacji</span><span class="sxs-lookup"><span data-stu-id="a7795-132">How to manually capture sign-in fields for an application</span></span>

<span data-ttu-id="a7795-133">Ręcznie przechwytywania logowania pól, najpierw musi mieć zainstalowane rozszerzenia przeglądarki panelu dostępu i **nie jest uruchomiona w trybie inPrivate, incognito lub prywatnej.**</span><span class="sxs-lookup"><span data-stu-id="a7795-133">To manually capture sign in fields, you must first have the Access Panel Browser extension installed and **not be running in inPrivate, incognito, or private mode.**</span></span> <span data-ttu-id="a7795-134">Aby zainstalować rozszerzenie przeglądarki, postępuj zgodnie z instrukcjami [jak zainstalować rozszerzenie przeglądarki panelu dostępu](#i-cannot-manually-detect-sign-in-fields-for-my-application) sekcji.</span><span class="sxs-lookup"><span data-stu-id="a7795-134">To install the browser extension, follow the steps in the [How to install the Access Panel Browser extension](#i-cannot-manually-detect-sign-in-fields-for-my-application) section.</span></span>

<span data-ttu-id="a7795-135">Aby skonfigurować **opartego na hasłach rejestracji jednokrotnej** dla aplikacji przy użyciu **przechwytywania ręczne znaku w polu**, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="a7795-135">To configure **Password-based Single Sign-on** for an application using **manual sign-in field capture**, follow the steps below:</span></span>

1.  <span data-ttu-id="a7795-136">Otwórz [ **Azure Portal** ](https://portal.azure.com/) i zaloguj się jako **administratora globalnego** lub **ko-administratora.**</span><span class="sxs-lookup"><span data-stu-id="a7795-136">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="a7795-137">Otwórz **rozszerzenia usług Azure Active Directory** klikając **więcej usług** u dołu menu nawigacji głównego po lewej stronie.</span><span class="sxs-lookup"><span data-stu-id="a7795-137">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="a7795-138">Wpisz w **"Azure Active Directory**" w polu wyszukiwania filtr a wybierz **usługi Azure Active Directory** elementu.</span><span class="sxs-lookup"><span data-stu-id="a7795-138">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="a7795-139">Kliknij przycisk **aplikacje dla przedsiębiorstw** w menu nawigacji po lewej stronie usługi Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="a7795-139">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="a7795-140">Kliknij przycisk **wszystkie aplikacje** Aby wyświetlić listę wszystkich aplikacji.</span><span class="sxs-lookup"><span data-stu-id="a7795-140">click **All Applications** to view a list of all your applications.</span></span>

   * <span data-ttu-id="a7795-141">Jeśli nie ma aplikacji ma tutaj będą wyświetlane, użyj **filtru** kontroli nad **listę wszystkich aplikacji** i ustaw **Pokaż** opcji w celu **wszystkich aplikacji.**</span><span class="sxs-lookup"><span data-stu-id="a7795-141">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="a7795-142">Wybierz aplikację, aby skonfigurować logowanie jednokrotne.</span><span class="sxs-lookup"><span data-stu-id="a7795-142">Select the application you want to configure single sign-on.</span></span>

7.  <span data-ttu-id="a7795-143">Po załadowaniu aplikacji, kliknij przycisk **logowanie jednokrotne** z menu nawigacji po lewej stronie aplikacji.</span><span class="sxs-lookup"><span data-stu-id="a7795-143">Once the application loads, click the **Single sign-on** from the application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="a7795-144">Wybierz tryb **opartego na hasłach logowania jednokrotnego.**</span><span class="sxs-lookup"><span data-stu-id="a7795-144">Select the mode **Password-based Sign-on.**</span></span>

9.  <span data-ttu-id="a7795-145">Wprowadź **adres URL logowania**.</span><span class="sxs-lookup"><span data-stu-id="a7795-145">Enter the **Sign-on URL**.</span></span> <span data-ttu-id="a7795-146">Jest to adres URL, których użytkownicy wprowadzić swoją nazwę i hasło do logowania się na.</span><span class="sxs-lookup"><span data-stu-id="a7795-146">This is the URL where users enter their username and password to sign in to.</span></span> <span data-ttu-id="a7795-147">**Upewnij się, logowania pola są widoczne w adresie URL, musisz podać**.</span><span class="sxs-lookup"><span data-stu-id="a7795-147">**Ensure the sign in fields are visible at the URL you provide**.</span></span>

10. <span data-ttu-id="a7795-148">Kliknij przycisk **Zapisz**.</span><span class="sxs-lookup"><span data-stu-id="a7795-148">Click the **Save** button.</span></span>

11. <span data-ttu-id="a7795-149">Po wykonaniu tej czynności, firma Microsoft będzie automatycznie scrape tego adresu URL dla nazwy użytkownika i hasło pole wprowadzania i umożliwiają używanie usługi Azure AD do bezpiecznego przesyłania hasła do tej aplikacji przy użyciu rozszerzenia przeglądarki panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="a7795-149">Once you do that, we’ll automatically scrape that URL for a username and password input box and allow you to use Azure AD to securely transmit passwords to that application using the access panel browser extension.</span></span> <span data-ttu-id="a7795-150">W przypadku, gdy to się nie powiedzie, może **zmienić tryb logowania, aby używać przechwytywania ręczne znaku w polu** kontynuując krok 12.</span><span class="sxs-lookup"><span data-stu-id="a7795-150">In the case that this fails, you can **change the sign-in mode to use manual sign-in field capture** by continuing to step 12.</span></span>

12. <span data-ttu-id="a7795-151">Kliknij przycisk **Konfiguruj &lt;appname&gt; ustawienia jednego hasła logowania jednokrotnego**.</span><span class="sxs-lookup"><span data-stu-id="a7795-151">click **Configure &lt;appname&gt; Password Single Sign-on Settings**.</span></span>

13. <span data-ttu-id="a7795-152">Wybierz **ręcznie wykryć pola logowania** opcji konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="a7795-152">Select the **Manually detect sign-in fields** configuration option.</span></span>

14. <span data-ttu-id="a7795-153">Kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="a7795-153">Click **Ok**.</span></span>

15. <span data-ttu-id="a7795-154">Kliknij pozycję **Zapisz**.</span><span class="sxs-lookup"><span data-stu-id="a7795-154">Click **Save**.</span></span>

16. <span data-ttu-id="a7795-155">Postępuj zgodnie z instrukcjami wyświetlanymi na ekranie do panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="a7795-155">Follow the on screen instructions to use the Access Panel.</span></span>

## <a name="i-see-a-we-couldnt-find-any-sign-in-fields-at-that-url-error"></a><span data-ttu-id="a7795-156">Wyświetlany jest komunikat Błąd "Nie można odnaleźć żadnych pól logowania pod tym adresem URL"</span><span class="sxs-lookup"><span data-stu-id="a7795-156">I see a “We couldn’t find any sign-in fields at that URL” error</span></span>

<span data-ttu-id="a7795-157">Zostanie wyświetlony ten błąd, gdy automatyczne wykrywanie pól logowanie nie powiodło się.</span><span class="sxs-lookup"><span data-stu-id="a7795-157">You see this error when automatic detection of sign-in fields fails.</span></span> <span data-ttu-id="a7795-158">Aby rozwiązać ten problem, spróbuj wykrywania ręczne pola logowania, wykonując kroki opisane w [ręcznie Przechwytywanie pola logowania dla aplikacji](#how-to-manually-capture-sign-in-fields-for-an-application) sekcji.</span><span class="sxs-lookup"><span data-stu-id="a7795-158">To resolve this issue, try manual sign-in field detection by following the steps in the [How to manually capture sign-in fields for an application](#how-to-manually-capture-sign-in-fields-for-an-application) section.</span></span>

## <a name="i-see-an-unable-to-save-single-sign-on-configuration-error"></a><span data-ttu-id="a7795-159">Widać "Nie można zapisać konfiguracji logowania jednokrotnego" Błąd</span><span class="sxs-lookup"><span data-stu-id="a7795-159">I see an “Unable to save Single Sign-on configuration” error</span></span>

<span data-ttu-id="a7795-160">W niektórych rzadkich przypadkach aktualizacja jednej konfiguracji logowania jednokrotnego może zakończyć się niepowodzeniem.</span><span class="sxs-lookup"><span data-stu-id="a7795-160">In certain rare cases, updating the single sign-on configuration can fail.</span></span> <span data-ttu-id="a7795-161">Aby rozwiązać ten spróbuj zapisać pojedynczego logowania jednokrotnego ponownie konfigurację.</span><span class="sxs-lookup"><span data-stu-id="a7795-161">TO resolve this try saving the single sign-on configuration again.</span></span>

<span data-ttu-id="a7795-162">Jeśli to się stale zwracają błąd, otwieranie sprawy pomocy technicznej i podaj informacje zebrane w [sposób wyświetlić szczegóły powiadomieniu portalu](#i-cannot-manually-detect-sign-in-fields-for-my-application) i [jak uzyskać pomoc, wysyłając szczegóły powiadomienia do pomocy technicznej inżynier](#how-to-get-help-by-sending-notification-details-to-a-support-engineer) sekcje.</span><span class="sxs-lookup"><span data-stu-id="a7795-162">If this continues to fail consistently, open a support case and provide the information gathered in the [How to see the details of a portal notification](#i-cannot-manually-detect-sign-in-fields-for-my-application) and [How to get help by sending notification details to a support engineer](#how-to-get-help-by-sending-notification-details-to-a-support-engineer) sections.</span></span>

## <a name="i-cannot-manually-detect-sign-in-fields-for-my-application"></a><span data-ttu-id="a7795-163">I nie można ręcznie wykrywania logowania w polach Moja aplikacja</span><span class="sxs-lookup"><span data-stu-id="a7795-163">I cannot manually detect sign in fields for my application</span></span>

<span data-ttu-id="a7795-164">Zachowania, które można napotkać podczas ręcznego wykrywania nie działa, należą:</span><span class="sxs-lookup"><span data-stu-id="a7795-164">Some of the behaviors you might see when manual detection is not working include:</span></span>

-   <span data-ttu-id="a7795-165">Proces przechwytywania ręczne pojawił się do pracy, ale pola przechwytywane nie była prawidłowa</span><span class="sxs-lookup"><span data-stu-id="a7795-165">The manual capture process appeared to work, but the fields captured were not correct</span></span>

-   <span data-ttu-id="a7795-166">Pola prawo nie pobrać wyróżniony podczas wykonywania procesu przechwytywania</span><span class="sxs-lookup"><span data-stu-id="a7795-166">The right fields don’t get highlighted when performing the capture process</span></span>

-   <span data-ttu-id="a7795-167">Przechwytywanie powoduje przejście do strony logowania aplikacji zgodnie z oczekiwaniami, ale nic się nie dzieje</span><span class="sxs-lookup"><span data-stu-id="a7795-167">The capture process takes me to the application’s login page as expected, but nothing happens</span></span>

-   <span data-ttu-id="a7795-168">Ręczne przechwytywania wydaje się działać, ale logowania jednokrotnego nie się zdarzyć, gdy Moi użytkownicy przejdź do aplikacji, z panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="a7795-168">Manual capture appears to work, but SSO doesn’t happen when my users navigate to the application from the Access Panel.</span></span>

<span data-ttu-id="a7795-169">Jeśli którekolwiek z tych problemów sprawdź następujące kwestie:</span><span class="sxs-lookup"><span data-stu-id="a7795-169">check the following if you encounter any of these issues:</span></span>

-   <span data-ttu-id="a7795-170">Upewnij się, że masz najnowszej wersji rozszerzenia przeglądarki panelu dostępu **zainstalowane** i **włączone** wykonując kroki opisane w [sposób instalowania rozszerzenia przeglądarki panelu dostępu](#how-to-install-the-access-panel-browser-extension) sekcji.</span><span class="sxs-lookup"><span data-stu-id="a7795-170">Ensure that you have the latest version of the access panel browser extension **installed** and **enabled** by following the steps in the [How to install the Access Panel Browser extension](#how-to-install-the-access-panel-browser-extension) section.</span></span>

-   <span data-ttu-id="a7795-171">Upewnij się, że nie próbujesz proces przechwytywania podczas do przeglądarki, **incognito, przeglądanie inPrivate lub prywatnej tryb**.</span><span class="sxs-lookup"><span data-stu-id="a7795-171">Ensure that you are not attempting the capture process while your browser in **incognito, inPrivate, or Private mode**.</span></span> <span data-ttu-id="a7795-172">Rozszerzenie panelu dostępu nie jest obsługiwana w tych trybach.</span><span class="sxs-lookup"><span data-stu-id="a7795-172">The access panel extension is not supported in these modes.</span></span>

-   <span data-ttu-id="a7795-173">Upewnij się, że użytkownicy nie próbuje zalogować się do aplikacji w panelu dostępu podczas w **incognito, przeglądanie inPrivate lub prywatnej tryb**.</span><span class="sxs-lookup"><span data-stu-id="a7795-173">Ensure that your users are not trying to sign in to the application from the access panel while in **incognito, inPrivate, or Private mode**.</span></span> <span data-ttu-id="a7795-174">Rozszerzenie panelu dostępu nie jest obsługiwana w tych trybach.</span><span class="sxs-lookup"><span data-stu-id="a7795-174">The access panel extension is not supported in these modes.</span></span>

-   <span data-ttu-id="a7795-175">Spróbuj ręcznie proces przechwytywania ponownie, zapewnienie, że czerwonych znaczników przekroczyli odpowiednich pól.</span><span class="sxs-lookup"><span data-stu-id="a7795-175">Try the manual capture process again, ensuring the red markers are over the correct fields.</span></span>

-   <span data-ttu-id="a7795-176">Proces przechwytywania ręczne wydaje się zawieszenie, czy strona logowania nie wszystko (przypadku 3 powyżej), spróbuj proces przechwytywania ręczne ponownie.</span><span class="sxs-lookup"><span data-stu-id="a7795-176">If the manual capture process seems to hang, or the sign in page doesn’t do anything (case 3 above), try the manual capture process again.</span></span> <span data-ttu-id="a7795-177">Jednak to czas, po zakończeniu procesu, naciśnij klawisz **F12** przycisk, aby otworzyć konsoli dla deweloperów w przeglądarce.</span><span class="sxs-lookup"><span data-stu-id="a7795-177">But, this time after completing the process, press the **F12** button to open your browser’s developer console.</span></span> <span data-ttu-id="a7795-178">Raz, otwórz **konsoli** i typ **window.location= "&lt;wprowadzać znaku w adresie url zostało określone podczas konfigurowania aplikacji&gt;"** , a następnie naciśnij klawisz **Enter**.</span><span class="sxs-lookup"><span data-stu-id="a7795-178">Once there, open the **console** and type **window.location=”&lt;enter the sign in url you specified when configuring the app&gt;”** and then press **Enter**.</span></span> <span data-ttu-id="a7795-179">Siła ta Strona przekierowania, który kończy proces przechwytywania i przechowywać pola, które została przechwycona.</span><span class="sxs-lookup"><span data-stu-id="a7795-179">This force a page redirect which end the capture process and store the fields that have been captured.</span></span>

<span data-ttu-id="a7795-180">Jeśli z tych metod nie działają dla Ciebie, możemy pomóc.</span><span class="sxs-lookup"><span data-stu-id="a7795-180">If none of these approaches work for you, we can help.</span></span> <span data-ttu-id="a7795-181">Otwieranie sprawy pomocy technicznej Szczegóły co próbujesz, a także informacje zebrane w [sposób wyświetlić szczegóły powiadomieniu portalu](#i-cannot-manually-detect-sign-in-fields-for-my-application) i [jak uzyskać pomoc, wysyłając szczegóły powiadomienia do pracownika pomocy technicznej ](#how-to-get-help-by-sending-notification-details-to-a-support-engineer) sekcje (jeśli dotyczy).</span><span class="sxs-lookup"><span data-stu-id="a7795-181">Open a support case with the details of what you tried, as well as the information gathered in the [How to see the details of a portal notification](#i-cannot-manually-detect-sign-in-fields-for-my-application) and [How to get help by sending notification details to a support engineer](#how-to-get-help-by-sending-notification-details-to-a-support-engineer) sections (if applicable).</span></span>

## <a name="how-to-install-the-access-panel-browser-extension"></a><span data-ttu-id="a7795-182">Jak zainstalować rozszerzenie przeglądarki panelu dostępu</span><span class="sxs-lookup"><span data-stu-id="a7795-182">How to install the Access Panel Browser extension</span></span>

<span data-ttu-id="a7795-183">Aby zainstalować rozszerzenie przeglądarki panelu dostępu, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="a7795-183">To install the Access Panel Browser extension, follow the steps below:</span></span>

1.  <span data-ttu-id="a7795-184">Otwórz [panelu dostępu](https://myapps.microsoft.com) w jednym z obsługiwanych przeglądarkach i zaloguj się jako **użytkownika** w usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a7795-184">Open the [Access Panel](https://myapps.microsoft.com) in one of the supported browsers and sign in as a **user** in your Azure AD.</span></span>

2.  <span data-ttu-id="a7795-185">Kliknij przycisk **logowania jednokrotnego hasła aplikacji** w panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="a7795-185">click a **password-SSO application** in the Access Panel.</span></span>

3.  <span data-ttu-id="a7795-186">W oknie komunikatu z pytaniem do zainstalowania oprogramowania, zaznaczyć **Zainstaluj teraz**.</span><span class="sxs-lookup"><span data-stu-id="a7795-186">In the prompt asking to install the software, select **Install Now**.</span></span>

4.  <span data-ttu-id="a7795-187">Oparte na przeglądarce być kierowane do łącza pobierania.</span><span class="sxs-lookup"><span data-stu-id="a7795-187">Based on your browser you be directed to the download link.</span></span> <span data-ttu-id="a7795-188">**Dodaj** rozszerzenia do przeglądarki.</span><span class="sxs-lookup"><span data-stu-id="a7795-188">**Add** the extension to your browser.</span></span>

5.  <span data-ttu-id="a7795-189">Jeśli przeglądarka pytanie, wybierz albo **włączyć** lub **Zezwalaj** rozszerzenia.</span><span class="sxs-lookup"><span data-stu-id="a7795-189">If your browser asks, select to either **Enable** or **Allow** the extension.</span></span>

6.  <span data-ttu-id="a7795-190">Wcześniej zainstalowano **ponowne uruchomienie** sesji przeglądarki.</span><span class="sxs-lookup"><span data-stu-id="a7795-190">Once installed, **restart** your browser session.</span></span>

7.  <span data-ttu-id="a7795-191">Zaloguj się do panelu dostępu i zobacz, czy można **uruchamianie** logowania jednokrotnego hasła aplikacji.</span><span class="sxs-lookup"><span data-stu-id="a7795-191">Sign in into the Access Panel and see if you can **launch** your password-SSO applications.</span></span>

<span data-ttu-id="a7795-192">Może również pobrać rozszerzenia dla programu Chrome, a program Firefox z bezpośrednich łączy poniżej:</span><span class="sxs-lookup"><span data-stu-id="a7795-192">You may also download the extension for Chrome and Firefox from the direct links below:</span></span>

-   [<span data-ttu-id="a7795-193">Rozszerzenie panelu dostępu Chrome</span><span class="sxs-lookup"><span data-stu-id="a7795-193">Chrome Access Panel Extension</span></span>](https://chrome.google.com/webstore/detail/access-panel-extension/ggjhpefgjjfobnfoldnjipclpcfbgbhl)

-   [<span data-ttu-id="a7795-194">Rozszerzenie panelu dostępu Firefox</span><span class="sxs-lookup"><span data-stu-id="a7795-194">Firefox Access Panel Extension</span></span>](https://addons.mozilla.org/firefox/addon/access-panel-extension/)

## <a name="how-to-see-the-details-of-a-portal-notification"></a><span data-ttu-id="a7795-195">Jak wyświetlić szczegóły powiadomieniu portalu</span><span class="sxs-lookup"><span data-stu-id="a7795-195">How to see the details of a portal notification</span></span>

<span data-ttu-id="a7795-196">Szczegółowe informacje o każdym powiadomieniu portalu można wyświetlić, wykonując poniższe kroki:</span><span class="sxs-lookup"><span data-stu-id="a7795-196">You can see the details of any portal notification by following the steps below:</span></span>

1.  <span data-ttu-id="a7795-197">Kliknij przycisk **powiadomienia** ikonę (dzwonka) w prawym górnym rogu portalu Azure</span><span class="sxs-lookup"><span data-stu-id="a7795-197">click the **Notifications** icon (the bell) in the upper right of the Azure Portal</span></span>

2.  <span data-ttu-id="a7795-198">Wybierz wszystkich powiadomień w **błąd** stanu (te z czerwonym znakiem (!) obok nich).</span><span class="sxs-lookup"><span data-stu-id="a7795-198">Select any notification in an **Error** state (those with a red (!) next to them).</span></span>

  ><span data-ttu-id="a7795-199">! Należy zwrócić uwagę] możesz nie kliknij powiadomienia w **Powodzenie** lub **w toku** stanu.</span><span class="sxs-lookup"><span data-stu-id="a7795-199">!NOTE] You cannot click notifications in a **Successful** or **In Progress** state.</span></span>
  >
  >

3.  <span data-ttu-id="a7795-200">Otwórz ten **szczegóły powiadomienia** bloku.</span><span class="sxs-lookup"><span data-stu-id="a7795-200">This open the **Notification Details** blade.</span></span>

4.  <span data-ttu-id="a7795-201">Dzięki tym informacjom samodzielnie, aby poznać więcej szczegółów o problemie.</span><span class="sxs-lookup"><span data-stu-id="a7795-201">Use this information yourself to understand more details about the problem.</span></span>

5.  <span data-ttu-id="a7795-202">Jeśli nadal potrzebujesz pomocy, te informacje mogą również współużytkować z pracownikiem pomocy technicznej lub grupa produktów, aby uzyskać pomoc dotyczącą tego problemu.</span><span class="sxs-lookup"><span data-stu-id="a7795-202">If you still need help, you can also share this information with a support engineer or the product group to get help with your problem.</span></span>

6.  <span data-ttu-id="a7795-203">Kliknij przycisk **kopiowania** **ikona** z prawej strony **błąd kopiowania** skopiuj wszystkie szczegóły powiadomienia na udostępnianie z pracownikiem pomocy technicznej lub produkt grupy w polu tekstowym.</span><span class="sxs-lookup"><span data-stu-id="a7795-203">Click the **copy** **icon** to the right of the **Copy error** textbox to copy all the notification details to share with a support or product group engineer.</span></span>

## <a name="how-to-get-help-by-sending-notification-details-to-a-support-engineer"></a><span data-ttu-id="a7795-204">Jak uzyskać pomoc, wysyłając szczegóły powiadomienia do pracownika pomocy technicznej</span><span class="sxs-lookup"><span data-stu-id="a7795-204">How to get help by sending notification details to a support engineer</span></span>

<span data-ttu-id="a7795-205">Jest bardzo ważne, aby udostępniać **poniższymi szczegółami** z pracownikiem pomocy technicznej, jeśli potrzebujesz pomocy, dzięki czemu mogą one ułatwić szybkie.</span><span class="sxs-lookup"><span data-stu-id="a7795-205">It is very important that you share **all the details listed below** with a support engineer if you need help, so that they can help you quickly.</span></span> <span data-ttu-id="a7795-206">Możesz to zrobić w prosty sposób przez **zrobieniem zrzutu ekranu,** lub przez kliknięcie przycisku **ikony błędu kopiowania**, liczba znalezionych na prawo od **błąd kopiowania** pola tekstowego.</span><span class="sxs-lookup"><span data-stu-id="a7795-206">You can do this easily by **taking a screenshot,** or by clicking the **Copy error icon**, found to the right of the **Copy error** textbox.</span></span>

## <a name="notification-details-explained"></a><span data-ttu-id="a7795-207">Szczegóły powiadomienia wyjaśniono</span><span class="sxs-lookup"><span data-stu-id="a7795-207">Notification Details Explained</span></span>

<span data-ttu-id="a7795-208">Poniżej przedstawiono więcej funkcji każdego, powiadomienia elementów oznacza i zawiera przykłady każdego z nich.</span><span class="sxs-lookup"><span data-stu-id="a7795-208">The below explains more what each of the notification items means, and gives examples of each of them.</span></span>

### <a name="essential-notification-items"></a><span data-ttu-id="a7795-209">Elementy podstawowych powiadomień</span><span class="sxs-lookup"><span data-stu-id="a7795-209">Essential Notification Items</span></span>

-   <span data-ttu-id="a7795-210">**Tytuł** — opisowy tytuł powiadomienia</span><span class="sxs-lookup"><span data-stu-id="a7795-210">**Title** – the descriptive title of the notification</span></span>

    -   <span data-ttu-id="a7795-211">Przykład — **ustawienia serwera proxy aplikacji**</span><span class="sxs-lookup"><span data-stu-id="a7795-211">Example – **Application proxy settings**</span></span>

-   <span data-ttu-id="a7795-212">**Opis elementu** — opis co nastąpiło w wyniku operacji</span><span class="sxs-lookup"><span data-stu-id="a7795-212">**Description** – the description of what occurred as a result of the operation</span></span>

    -   <span data-ttu-id="a7795-213">Przykład — **wewnętrzny wprowadzony adres url jest już używana przez inną aplikację**</span><span class="sxs-lookup"><span data-stu-id="a7795-213">Example – **Internal url entered is already being used by another application**</span></span>

-   <span data-ttu-id="a7795-214">**Identyfikator powiadomień** — Unikatowy identyfikator powiadomienia.</span><span class="sxs-lookup"><span data-stu-id="a7795-214">**Notification Id** – the unique id of the notification</span></span>

    -   <span data-ttu-id="a7795-215">Przykład — **clientNotification-2adbfc06-2073-4678-a69f-7eb78d96b068**</span><span class="sxs-lookup"><span data-stu-id="a7795-215">Example – **clientNotification-2adbfc06-2073-4678-a69f-7eb78d96b068**</span></span>

-   <span data-ttu-id="a7795-216">**Identyfikator żądania klienta** — identyfikator określonego żądania przez przeglądarkę</span><span class="sxs-lookup"><span data-stu-id="a7795-216">**Client Request Id** – the specific request id made by your browser</span></span>

    -   <span data-ttu-id="a7795-217">Przykład — **302fd775-3329-4670-a9f3-bea37004f0bc**</span><span class="sxs-lookup"><span data-stu-id="a7795-217">Example – **302fd775-3329-4670-a9f3-bea37004f0bc**</span></span>

-   <span data-ttu-id="a7795-218">**Czas UTC sygnatury** — znacznik czasu, w którym wystąpił powiadomienia, w formacie UTC</span><span class="sxs-lookup"><span data-stu-id="a7795-218">**Time Stamp UTC** – the timestamp during which the notification occurred, in UTC</span></span>

    -   <span data-ttu-id="a7795-219">Przykład — **2017-03-23T19:50:43.7583681Z**</span><span class="sxs-lookup"><span data-stu-id="a7795-219">Example – **2017-03-23T19:50:43.7583681Z**</span></span>

-   <span data-ttu-id="a7795-220">**Wewnętrzny identyfikator transakcji** — wewnętrzny identyfikator możemy użyć do wyszukiwania błąd w naszym systemie</span><span class="sxs-lookup"><span data-stu-id="a7795-220">**Internal Transaction Id** – the internal ID we can use to look the error up in our systems</span></span>

    -   <span data-ttu-id="a7795-221">Przykład — **71a2f329-ca29-402f-aa72-bc00a7aca603**</span><span class="sxs-lookup"><span data-stu-id="a7795-221">Example – **71a2f329-ca29-402f-aa72-bc00a7aca603**</span></span>

-   <span data-ttu-id="a7795-222">**Nazwa UPN** — użytkownik, który wykonał działanie</span><span class="sxs-lookup"><span data-stu-id="a7795-222">**UPN** – the user who performed the operation</span></span>

    -   <span data-ttu-id="a7795-223">Przykład —**tperkins@f128.info**</span><span class="sxs-lookup"><span data-stu-id="a7795-223">Example – **tperkins@f128.info**</span></span>

-   <span data-ttu-id="a7795-224">**Identyfikator dzierżawy** — Unikatowy identyfikator dzierżawy, który użytkownik, który wykonał działanie był członkiem</span><span class="sxs-lookup"><span data-stu-id="a7795-224">**Tenant Id** – the unique ID of the tenant that the user who performed the operation was a member of</span></span>

    -   <span data-ttu-id="a7795-225">Przykład — **7918d4b5-0442-4a97-be2d-36f9f9962ece**</span><span class="sxs-lookup"><span data-stu-id="a7795-225">Example – **7918d4b5-0442-4a97-be2d-36f9f9962ece**</span></span>

-   <span data-ttu-id="a7795-226">**Identyfikator obiektu użytkownika** — Unikatowy identyfikator użytkownika, który wykonał działanie</span><span class="sxs-lookup"><span data-stu-id="a7795-226">**User object Id** – the unique ID of the user who performed the operation</span></span>

    -   <span data-ttu-id="a7795-227">Przykład — **17f84be4-51f8-483a-b533-383791227a99**</span><span class="sxs-lookup"><span data-stu-id="a7795-227">Example – **17f84be4-51f8-483a-b533-383791227a99**</span></span>

### <a name="detailed-notification-items"></a><span data-ttu-id="a7795-228">Elementy szczegółowe powiadomienia</span><span class="sxs-lookup"><span data-stu-id="a7795-228">Detailed Notification Items</span></span>

-   <span data-ttu-id="a7795-229">**Nazwa wyświetlana** — **(może być pusta)** nazwę wyświetlaną bardziej szczegółowy kod błędu</span><span class="sxs-lookup"><span data-stu-id="a7795-229">**Display Name** – **(can be empty)** a more detailed display name for the error</span></span>

    -   <span data-ttu-id="a7795-230">Przykład * — **ustawienia serwera proxy aplikacji**</span><span class="sxs-lookup"><span data-stu-id="a7795-230">Example *– **Application proxy settings**</span></span>

-   <span data-ttu-id="a7795-231">**Stan** — stan określonego powiadomienia</span><span class="sxs-lookup"><span data-stu-id="a7795-231">**Status** – the specific status of the notification</span></span>

    -   <span data-ttu-id="a7795-232">Przykład * — **nie powiodło się**</span><span class="sxs-lookup"><span data-stu-id="a7795-232">Example *– **Failed**</span></span>

-   <span data-ttu-id="a7795-233">**Obiekt o identyfikatorze** — **(może być pusta)** Identyfikatora obiektu, względem którego wykonano operację</span><span class="sxs-lookup"><span data-stu-id="a7795-233">**Object Id** – **(can be empty)** the object ID against which the operation was performed</span></span>

    -   <span data-ttu-id="a7795-234">Przykład — **8e08161d-f2fd-40ad-a34a-a9632d6bb599**</span><span class="sxs-lookup"><span data-stu-id="a7795-234">Example – **8e08161d-f2fd-40ad-a34a-a9632d6bb599**</span></span>

-   <span data-ttu-id="a7795-235">**Szczegóły** — szczegółowy opis co nastąpiło w wyniku operacji</span><span class="sxs-lookup"><span data-stu-id="a7795-235">**Details** – the detailed description of what occurred as a result of the operation</span></span>

    -   <span data-ttu-id="a7795-236">Przykład — **wewnętrznego adresu url "http://bing.com/" jest nieprawidłowy, ponieważ jest już używana**</span><span class="sxs-lookup"><span data-stu-id="a7795-236">Example – **Internal url 'http://bing.com/' is invalid since it is already in use**</span></span>

-   <span data-ttu-id="a7795-237">**Błąd kopiowania** — kliknij przycisk **ikonę kopiowania** z prawej strony **błąd kopiowania** pole tekstowe, aby skopiować wszystkie szczegóły powiadomienia na udostępnianie z pracownikiem pomocy technicznej lub produkt grupy</span><span class="sxs-lookup"><span data-stu-id="a7795-237">**Copy error** – Click the **copy icon** to the right of the **Copy error** textbox to copy all the notification details to share with a support or product group engineer</span></span>

    -   <span data-ttu-id="a7795-238">Przykład —```{"errorCode":"InternalUrl\_Duplicate","localizedErrorDetails":{"errorDetail":"Internal url 'http://google.com/' is invalid since it is already in use"},"operationResults":\[{"objectId":null,"displayName":null,"status":0,"details":"Internal url 'http://bing.com/' is invalid since it is already in use"}\],"timeStampUtc":"2017-03-23T19:50:26.465743Z","clientRequestId":"302fd775-3329-4670-a9f3-bea37004f0bb","internalTransactionId":"ea5b5475-03b9-4f08-8e95-bbb11289ab65","upn":"tperkins@f128.info","tenantId":"7918d4b5-0442-4a97-be2d-36f9f9962ece","userObjectId":"17f84be4-51f8-483a-b533-383791227a99"}```</span><span class="sxs-lookup"><span data-stu-id="a7795-238">Example – ```{"errorCode":"InternalUrl\_Duplicate","localizedErrorDetails":{"errorDetail":"Internal url 'http://google.com/' is invalid since it is already in use"},"operationResults":\[{"objectId":null,"displayName":null,"status":0,"details":"Internal url 'http://bing.com/' is invalid since it is already in use"}\],"timeStampUtc":"2017-03-23T19:50:26.465743Z","clientRequestId":"302fd775-3329-4670-a9f3-bea37004f0bb","internalTransactionId":"ea5b5475-03b9-4f08-8e95-bbb11289ab65","upn":"tperkins@f128.info","tenantId":"7918d4b5-0442-4a97-be2d-36f9f9962ece","userObjectId":"17f84be4-51f8-483a-b533-383791227a99"}```</span></span>

## <a name="next-steps"></a><span data-ttu-id="a7795-239">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="a7795-239">Next steps</span></span>
[<span data-ttu-id="a7795-240">Podaj logowanie jednokrotne do aplikacji przy użyciu serwera Proxy aplikacji</span><span class="sxs-lookup"><span data-stu-id="a7795-240">Provide single sign-on to your apps with Application Proxy</span></span>](active-directory-application-proxy-sso-using-kcd.md)

