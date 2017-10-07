---
title: "Konfigurowanie hasła logowanie jednokrotne dla aplikacji z systemem innym niż galerii aaaProblem | Dokumentacja firmy Microsoft"
description: "Zrozumienie hello typowych problemów osób krój, podczas konfigurowania haseł logowanie jednokrotne dla aplikacji z systemem innym niż galerii niestandardowych, które nie są wymienione w hello galerii aplikacji usługi Azure AD"
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
ms.openlocfilehash: 3aee0a4c525bb3da338da2da0882ec572cf0e5e6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="problem-configuring-password-single-sign-on-for-a-non-gallery-application"></a><span data-ttu-id="dc0e0-103">Problem podczas konfiguracji hasła logowanie jednokrotne dla aplikacji z systemem innym niż galerii</span><span class="sxs-lookup"><span data-stu-id="dc0e0-103">Problem configuring password single sign-on for a non-gallery application</span></span>

<span data-ttu-id="dc0e0-104">W tym artykule pomóc toounderstand hello typowych problemów osób krój podczas konfigurowania **hasło logowania jednokrotnego** z aplikacji innych niż galerii.</span><span class="sxs-lookup"><span data-stu-id="dc0e0-104">This article help you toounderstand hello common problems people face when configuring **Password single sign-on** with a non-gallery application.</span></span>

## <a name="how-toocapture-sign-in-fields-for-an-application"></a><span data-ttu-id="dc0e0-105">Sposób logowania toocapture pól dla aplikacji</span><span class="sxs-lookup"><span data-stu-id="dc0e0-105">How toocapture sign-in fields for an application</span></span>

<span data-ttu-id="dc0e0-106">Przechwytywanie pola logowania jest obsługiwana tylko dla komputerów z obsługą HTML strony logowania i jest **nie jest obsługiwane dla niestandardowych stron logowania**, takich jak implementacje używające Flash i inne technologie włączone HTML.</span><span class="sxs-lookup"><span data-stu-id="dc0e0-106">Sign-in field capture is only supported for HTML-enabled sign-in pages and is **not supported for non-standard sign-in pages**, like those that use Flash, or other non-HTML-enabled technologies.</span></span>

<span data-ttu-id="dc0e0-107">Istnieją dwa sposoby, można przechwytywać logowania pól niestandardowych aplikacji:</span><span class="sxs-lookup"><span data-stu-id="dc0e0-107">There are two ways you can capture sign-in fields for your custom applications:</span></span>

-   <span data-ttu-id="dc0e0-108">Automatyczne logowanie pola przechwytywania</span><span class="sxs-lookup"><span data-stu-id="dc0e0-108">Automatic sign-in field capture</span></span>

-   <span data-ttu-id="dc0e0-109">Ręczne znaku w polu przechwytywania</span><span class="sxs-lookup"><span data-stu-id="dc0e0-109">Manual sign-in field capture</span></span>

<span data-ttu-id="dc0e0-110">**Automatyczne logowanie pola przechwytywania** działa prawidłowo w przypadku większości włączone HTML strony logowania, jeśli używają one **dobrze znane identyfikatory DIV hello nazwy użytkownika i hasła, wprowadź** pola.</span><span class="sxs-lookup"><span data-stu-id="dc0e0-110">**Automatic sign-in field capture** works well with most HTML-enabled sign-in pages, if they use **well-known DIV IDs for hello username and password input** field.</span></span> <span data-ttu-id="dc0e0-111">działa to sposób Hello jest za pomocą oskrobaniu hello HTML na powitania strony toofind identyfikatorów DIV, spełniających określone kryteria i następnie zapisywania tych metadanych dla tej aplikacji, można później odtwarzana tooit hasła.</span><span class="sxs-lookup"><span data-stu-id="dc0e0-111">hello way this works is by scraping hello HTML on hello page toofind DIV IDs that match certain criteria and by then saving that metadata for this application so we can replay passwords tooit later.</span></span>

<span data-ttu-id="dc0e0-112">**Przechwytywanie ręczne znaku w polu** mogą być używane w przypadku hello aplikacji hello **dostawcy nie etykietę** hello wejściowy pola używane w celu logowania się.</span><span class="sxs-lookup"><span data-stu-id="dc0e0-112">**Manual sign-in field capture** can be used in hello case that hello application **vendor does not label** hello input fields used for sign in.</span></span> <span data-ttu-id="dc0e0-113">Ręczne znaku w polu przechwytywania można również w przypadku hello podczas hello **dostawcy renderuje wielu pól** co nie może być wykrywane automatycznie.</span><span class="sxs-lookup"><span data-stu-id="dc0e0-113">Manual sign-in field capture can also be used in hello case when hello **vendor renders multiple fields** which cannot be auto-detected.</span></span> <span data-ttu-id="dc0e0-114">Usługi Azure AD można przechowywać dane jako wiele pól znajdują się na powitania Zaloguj się na stronie tak długo, jak możesz Napisz, których te pola są na stronie powitania.</span><span class="sxs-lookup"><span data-stu-id="dc0e0-114">Azure AD can store data for as many fields as are on hello sign in page, so long as you tell us where those fields are on hello page.</span></span>

<span data-ttu-id="dc0e0-115">Ogólnie rzecz biorąc **Jeśli pole automatycznego logowania przechwytywania nie działa, zawsze zalecamy w trakcie hello opcja ręcznego.**</span><span class="sxs-lookup"><span data-stu-id="dc0e0-115">In general, **if automatic sign-in field capture does not work, we always suggest trying hello manual option.**</span></span>

### <a name="how-tooautomatically-capture-sign-in-fields-for-an-application"></a><span data-ttu-id="dc0e0-116">Jak tooautomatically przechwytywania pola logowania dla aplikacji</span><span class="sxs-lookup"><span data-stu-id="dc0e0-116">How tooautomatically capture sign-in fields for an application</span></span>

<span data-ttu-id="dc0e0-117">tooconfigure **opartego na hasłach rejestracji jednokrotnej** dla aplikacji przy użyciu **przechwytywania automatycznego logowania pola**, wykonaj poniższe kroki hello:</span><span class="sxs-lookup"><span data-stu-id="dc0e0-117">tooconfigure **Password-based Single Sign-on** for an application using **automatic sign-in field capture**, follow hello steps below:</span></span>

1.  <span data-ttu-id="dc0e0-118">Otwórz hello [ **Azure Portal** ](https://portal.azure.com/) i zaloguj się jako **administratora globalnego** lub **ko-administratora.**</span><span class="sxs-lookup"><span data-stu-id="dc0e0-118">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="dc0e0-119">Otwórz hello **rozszerzenia usług Azure Active Directory** klikając **więcej usług** u dołu menu nawigacji głównego po lewej stronie powitania hello.</span><span class="sxs-lookup"><span data-stu-id="dc0e0-119">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="dc0e0-120">Wpisz w **"Azure Active Directory**" w polu wyszukiwania filtr hello a wybierz hello **usługi Azure Active Directory** elementu.</span><span class="sxs-lookup"><span data-stu-id="dc0e0-120">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="dc0e0-121">Kliknij przycisk **aplikacje dla przedsiębiorstw** z menu nawigacji po lewej stronie powitania w usłudze Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="dc0e0-121">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="dc0e0-122">Kliknij przycisk **wszystkie aplikacje** tooview listę wszystkich aplikacji.</span><span class="sxs-lookup"><span data-stu-id="dc0e0-122">click **All Applications** tooview a list of all your applications.</span></span>

  * <span data-ttu-id="dc0e0-123">Jeśli nie ma aplikacji hello mają być wyświetlane tutaj, użyj hello **filtru** kontroli u góry hello hello **listę wszystkich aplikacji** i zestaw hello **Pokaż** opcję zbyt **Wszystkie aplikacje.**</span><span class="sxs-lookup"><span data-stu-id="dc0e0-123">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="dc0e0-124">Wybierz aplikację hello ma tooconfigure rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="dc0e0-124">Select hello application you want tooconfigure single sign-on.</span></span>

7.  <span data-ttu-id="dc0e0-125">Po załadowaniu aplikacji hello, kliknij przycisk hello **logowanie jednokrotne** z menu nawigacji po lewej stronie powitania aplikacji.</span><span class="sxs-lookup"><span data-stu-id="dc0e0-125">Once hello application loads, click hello **Single sign-on** from hello application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="dc0e0-126">Tryb wybierz hello **opartego na hasłach logowania jednokrotnego.**</span><span class="sxs-lookup"><span data-stu-id="dc0e0-126">Select hello mode **Password-based Sign-on.**</span></span>

9.  <span data-ttu-id="dc0e0-127">Wprowadź hello **adres URL logowania**.</span><span class="sxs-lookup"><span data-stu-id="dc0e0-127">Enter hello **Sign-on URL**.</span></span> <span data-ttu-id="dc0e0-128">Jest to adres URL hello, gdzie użytkownicy wprowadzać ich nazwy użytkownika i hasła toosign w w celu.</span><span class="sxs-lookup"><span data-stu-id="dc0e0-128">This is hello URL where users enter their username and password toosign in to.</span></span> <span data-ttu-id="dc0e0-129">**Upewnij się, hello logowania pola są widoczne pod adresem URL hello, musisz podać**.</span><span class="sxs-lookup"><span data-stu-id="dc0e0-129">**Ensure hello sign in fields are visible at hello URL you provide**.</span></span>

10. <span data-ttu-id="dc0e0-130">Kliknij przycisk hello **zapisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="dc0e0-130">Click hello **Save** button.</span></span>

11. <span data-ttu-id="dc0e0-131">Po można to zrobić, firma Microsoft będzie automatycznie scrape tego adresu URL dla nazwy użytkownika i hasła pole wprowadzania i umożliwić toosecurely usługi Azure AD toouse przekazuje hasła toothat aplikacji przy użyciu rozszerzenia przeglądarki panelu dostępu hello.</span><span class="sxs-lookup"><span data-stu-id="dc0e0-131">Once you do that, we’ll automatically scrape that URL for a username and password input box and allow you toouse Azure AD toosecurely transmit passwords toothat application using hello access panel browser extension.</span></span>

## <a name="how-toomanually-capture-sign-in-fields-for-an-application"></a><span data-ttu-id="dc0e0-132">Jak toomanually przechwytywania pola logowania dla aplikacji</span><span class="sxs-lookup"><span data-stu-id="dc0e0-132">How toomanually capture sign-in fields for an application</span></span>

<span data-ttu-id="dc0e0-133">toomanually przechwytywania logowania pól, trzeba rozszerzenia przeglądarki panelu dostępu hello zainstalowany i **nie jest uruchomiona w trybie inPrivate, incognito lub prywatnej.**</span><span class="sxs-lookup"><span data-stu-id="dc0e0-133">toomanually capture sign in fields, you must first have hello Access Panel Browser extension installed and **not be running in inPrivate, incognito, or private mode.**</span></span> <span data-ttu-id="dc0e0-134">Rozszerzenie przeglądarki hello tooinstall, wykonaj kroki hello hello [jak tooinstall hello rozszerzenia przeglądarki panelu dostępu](#i-cannot-manually-detect-sign-in-fields-for-my-application) sekcji.</span><span class="sxs-lookup"><span data-stu-id="dc0e0-134">tooinstall hello browser extension, follow hello steps in hello [How tooinstall hello Access Panel Browser extension](#i-cannot-manually-detect-sign-in-fields-for-my-application) section.</span></span>

<span data-ttu-id="dc0e0-135">tooconfigure **opartego na hasłach rejestracji jednokrotnej** dla aplikacji przy użyciu **przechwytywania ręczne znaku w polu**, wykonaj poniższe kroki hello:</span><span class="sxs-lookup"><span data-stu-id="dc0e0-135">tooconfigure **Password-based Single Sign-on** for an application using **manual sign-in field capture**, follow hello steps below:</span></span>

1.  <span data-ttu-id="dc0e0-136">Otwórz hello [ **Azure Portal** ](https://portal.azure.com/) i zaloguj się jako **administratora globalnego** lub **ko-administratora.**</span><span class="sxs-lookup"><span data-stu-id="dc0e0-136">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="dc0e0-137">Otwórz hello **rozszerzenia usług Azure Active Directory** klikając **więcej usług** u dołu menu nawigacji głównego po lewej stronie powitania hello.</span><span class="sxs-lookup"><span data-stu-id="dc0e0-137">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="dc0e0-138">Wpisz w **"Azure Active Directory**" w polu wyszukiwania filtr hello a wybierz hello **usługi Azure Active Directory** elementu.</span><span class="sxs-lookup"><span data-stu-id="dc0e0-138">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="dc0e0-139">Kliknij przycisk **aplikacje dla przedsiębiorstw** z menu nawigacji po lewej stronie powitania w usłudze Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="dc0e0-139">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="dc0e0-140">Kliknij przycisk **wszystkie aplikacje** tooview listę wszystkich aplikacji.</span><span class="sxs-lookup"><span data-stu-id="dc0e0-140">click **All Applications** tooview a list of all your applications.</span></span>

   * <span data-ttu-id="dc0e0-141">Jeśli nie ma aplikacji hello mają być wyświetlane tutaj, użyj hello **filtru** kontroli u góry hello hello **listę wszystkich aplikacji** i zestaw hello **Pokaż** opcję zbyt **Wszystkie aplikacje.**</span><span class="sxs-lookup"><span data-stu-id="dc0e0-141">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="dc0e0-142">Wybierz aplikację hello ma tooconfigure rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="dc0e0-142">Select hello application you want tooconfigure single sign-on.</span></span>

7.  <span data-ttu-id="dc0e0-143">Po załadowaniu aplikacji hello, kliknij przycisk hello **logowanie jednokrotne** z menu nawigacji po lewej stronie powitania aplikacji.</span><span class="sxs-lookup"><span data-stu-id="dc0e0-143">Once hello application loads, click hello **Single sign-on** from hello application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="dc0e0-144">Tryb wybierz hello **opartego na hasłach logowania jednokrotnego.**</span><span class="sxs-lookup"><span data-stu-id="dc0e0-144">Select hello mode **Password-based Sign-on.**</span></span>

9.  <span data-ttu-id="dc0e0-145">Wprowadź hello **adres URL logowania**.</span><span class="sxs-lookup"><span data-stu-id="dc0e0-145">Enter hello **Sign-on URL**.</span></span> <span data-ttu-id="dc0e0-146">Jest to adres URL hello, gdzie użytkownicy wprowadzać ich nazwy użytkownika i hasła toosign w w celu.</span><span class="sxs-lookup"><span data-stu-id="dc0e0-146">This is hello URL where users enter their username and password toosign in to.</span></span> <span data-ttu-id="dc0e0-147">**Upewnij się, hello logowania pola są widoczne pod adresem URL hello, musisz podać**.</span><span class="sxs-lookup"><span data-stu-id="dc0e0-147">**Ensure hello sign in fields are visible at hello URL you provide**.</span></span>

10. <span data-ttu-id="dc0e0-148">Kliknij przycisk hello **zapisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="dc0e0-148">Click hello **Save** button.</span></span>

11. <span data-ttu-id="dc0e0-149">Po można to zrobić, firma Microsoft będzie automatycznie scrape tego adresu URL dla nazwy użytkownika i hasła pole wprowadzania i umożliwić toosecurely usługi Azure AD toouse przekazuje hasła toothat aplikacji przy użyciu rozszerzenia przeglądarki panelu dostępu hello.</span><span class="sxs-lookup"><span data-stu-id="dc0e0-149">Once you do that, we’ll automatically scrape that URL for a username and password input box and allow you toouse Azure AD toosecurely transmit passwords toothat application using hello access panel browser extension.</span></span> <span data-ttu-id="dc0e0-150">W przypadku hello, że to się nie powiedzie, może **zmienić hello logowania w trybie toouse ręczne znaku w polu przechwytywania** kontynuując toostep 12.</span><span class="sxs-lookup"><span data-stu-id="dc0e0-150">In hello case that this fails, you can **change hello sign-in mode toouse manual sign-in field capture** by continuing toostep 12.</span></span>

12. <span data-ttu-id="dc0e0-151">Kliknij przycisk **Konfiguruj &lt;appname&gt; ustawienia jednego hasła logowania jednokrotnego**.</span><span class="sxs-lookup"><span data-stu-id="dc0e0-151">click **Configure &lt;appname&gt; Password Single Sign-on Settings**.</span></span>

13. <span data-ttu-id="dc0e0-152">Wybierz hello **ręcznie wykryć pola logowania** opcji konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="dc0e0-152">Select hello **Manually detect sign-in fields** configuration option.</span></span>

14. <span data-ttu-id="dc0e0-153">Kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="dc0e0-153">Click **Ok**.</span></span>

15. <span data-ttu-id="dc0e0-154">Kliknij pozycję **Zapisz**.</span><span class="sxs-lookup"><span data-stu-id="dc0e0-154">Click **Save**.</span></span>

16. <span data-ttu-id="dc0e0-155">Wykonaj hello na ekranie instrukcjami toouse hello panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="dc0e0-155">Follow hello on screen instructions toouse hello Access Panel.</span></span>

## <a name="i-see-a-we-couldnt-find-any-sign-in-fields-at-that-url-error"></a><span data-ttu-id="dc0e0-156">Wyświetlany jest komunikat Błąd "Nie można odnaleźć żadnych pól logowania pod tym adresem URL"</span><span class="sxs-lookup"><span data-stu-id="dc0e0-156">I see a “We couldn’t find any sign-in fields at that URL” error</span></span>

<span data-ttu-id="dc0e0-157">Zostanie wyświetlony ten błąd, gdy automatyczne wykrywanie pól logowanie nie powiodło się.</span><span class="sxs-lookup"><span data-stu-id="dc0e0-157">You see this error when automatic detection of sign-in fields fails.</span></span> <span data-ttu-id="dc0e0-158">Ten problem, spróbuj ręcznie znaku w polu wykrywania przez następujące hello etapami hello tooresolve [jak toomanually przechwytywania pola logowania dla aplikacji](#how-to-manually-capture-sign-in-fields-for-an-application) sekcji.</span><span class="sxs-lookup"><span data-stu-id="dc0e0-158">tooresolve this issue, try manual sign-in field detection by following hello steps in hello [How toomanually capture sign-in fields for an application](#how-to-manually-capture-sign-in-fields-for-an-application) section.</span></span>

## <a name="i-see-an-unable-toosave-single-sign-on-configuration-error"></a><span data-ttu-id="dc0e0-159">Komunikat "toosave rejestracji jednokrotnej konfiguracji"</span><span class="sxs-lookup"><span data-stu-id="dc0e0-159">I see an “Unable toosave Single Sign-on configuration” error</span></span>

<span data-ttu-id="dc0e0-160">W niektórych rzadkich przypadkach aktualizacja hello pojedynczego logowania jednokrotnego konfiguracji może zakończyć się niepowodzeniem.</span><span class="sxs-lookup"><span data-stu-id="dc0e0-160">In certain rare cases, updating hello single sign-on configuration can fail.</span></span> <span data-ttu-id="dc0e0-161">tooresolve to spróbuj zapisać hello pojedynczego logowania jednokrotnego ponownie konfigurację.</span><span class="sxs-lookup"><span data-stu-id="dc0e0-161">tooresolve this try saving hello single sign-on configuration again.</span></span>

<span data-ttu-id="dc0e0-162">Jeśli ten proces jest kontynuowany toofail spójnie, otwieranie sprawy pomocy technicznej i podaj hello informacje zebrane w hello [jak toosee szczegóły hello powiadomieniu portalu](#i-cannot-manually-detect-sign-in-fields-for-my-application) i [jak tooget pomóc, wysyłając powiadomienia szczegóły tooa inżynier pomocy technicznej](#how-to-get-help-by-sending-notification-details-to-a-support-engineer) sekcje.</span><span class="sxs-lookup"><span data-stu-id="dc0e0-162">If this continues toofail consistently, open a support case and provide hello information gathered in hello [How toosee hello details of a portal notification](#i-cannot-manually-detect-sign-in-fields-for-my-application) and [How tooget help by sending notification details tooa support engineer](#how-to-get-help-by-sending-notification-details-to-a-support-engineer) sections.</span></span>

## <a name="i-cannot-manually-detect-sign-in-fields-for-my-application"></a><span data-ttu-id="dc0e0-163">I nie można ręcznie wykrywania logowania w polach Moja aplikacja</span><span class="sxs-lookup"><span data-stu-id="dc0e0-163">I cannot manually detect sign in fields for my application</span></span>

<span data-ttu-id="dc0e0-164">Witaj zachowania, które można napotkać podczas ręcznego wykrywania nie działa, należą:</span><span class="sxs-lookup"><span data-stu-id="dc0e0-164">Some of hello behaviors you might see when manual detection is not working include:</span></span>

-   <span data-ttu-id="dc0e0-165">Proces przechwytywania ręczne Hello pojawił się toowork, ale pola hello przechwytywane nie była prawidłowa</span><span class="sxs-lookup"><span data-stu-id="dc0e0-165">hello manual capture process appeared toowork, but hello fields captured were not correct</span></span>

-   <span data-ttu-id="dc0e0-166">Witaj prawej strony pola nie pobrać wyróżniony podczas wykonywania procesu przechwytywania hello</span><span class="sxs-lookup"><span data-stu-id="dc0e0-166">hello right fields don’t get highlighted when performing hello capture process</span></span>

-   <span data-ttu-id="dc0e0-167">Proces przechwytywania Hello przejście strony logowania toohello aplikacji zgodnie z oczekiwaniami, ale nic się nie dzieje</span><span class="sxs-lookup"><span data-stu-id="dc0e0-167">hello capture process takes me toohello application’s login page as expected, but nothing happens</span></span>

-   <span data-ttu-id="dc0e0-168">Ręczne przechwytywania jest wyświetlany toowork, ale nie jest realizowane logowania jednokrotnego gdy Moi użytkownicy przejdą toohello aplikacji hello panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="dc0e0-168">Manual capture appears toowork, but SSO doesn’t happen when my users navigate toohello application from hello Access Panel.</span></span>

<span data-ttu-id="dc0e0-169">Jeśli którekolwiek z tych problemów, sprawdź następujące hello:</span><span class="sxs-lookup"><span data-stu-id="dc0e0-169">check hello following if you encounter any of these issues:</span></span>

-   <span data-ttu-id="dc0e0-170">Upewnij się, że masz najnowszej wersji rozszerzenia przeglądarki panelu dostępu hello hello **zainstalowane** i **włączone** wykonując kroki hello w hello [jak tooinstall hello przeglądarki panelu dostępu rozszerzenie](#how-to-install-the-access-panel-browser-extension) sekcji.</span><span class="sxs-lookup"><span data-stu-id="dc0e0-170">Ensure that you have hello latest version of hello access panel browser extension **installed** and **enabled** by following hello steps in hello [How tooinstall hello Access Panel Browser extension](#how-to-install-the-access-panel-browser-extension) section.</span></span>

-   <span data-ttu-id="dc0e0-171">Upewnij się, że nie próbujesz proces przechwytywania hello podczas do przeglądarki, **incognito, przeglądanie inPrivate lub prywatnej tryb**.</span><span class="sxs-lookup"><span data-stu-id="dc0e0-171">Ensure that you are not attempting hello capture process while your browser in **incognito, inPrivate, or Private mode**.</span></span> <span data-ttu-id="dc0e0-172">rozszerzenie panelu dostępu Hello nie jest obsługiwana w tych trybach.</span><span class="sxs-lookup"><span data-stu-id="dc0e0-172">hello access panel extension is not supported in these modes.</span></span>

-   <span data-ttu-id="dc0e0-173">Upewnij się, że użytkownicy nie próbujesz toosign w toohello aplikacji hello panelu dostępu podczas w **incognito, przeglądanie inPrivate lub prywatnej tryb**.</span><span class="sxs-lookup"><span data-stu-id="dc0e0-173">Ensure that your users are not trying toosign in toohello application from hello access panel while in **incognito, inPrivate, or Private mode**.</span></span> <span data-ttu-id="dc0e0-174">rozszerzenie panelu dostępu Hello nie jest obsługiwana w tych trybach.</span><span class="sxs-lookup"><span data-stu-id="dc0e0-174">hello access panel extension is not supported in these modes.</span></span>

-   <span data-ttu-id="dc0e0-175">Spróbuj ponownie proces przechwytywania ręczne hello, zapewnienie znaczników hello red za pośrednictwem hello odpowiednich pól.</span><span class="sxs-lookup"><span data-stu-id="dc0e0-175">Try hello manual capture process again, ensuring hello red markers are over hello correct fields.</span></span>

-   <span data-ttu-id="dc0e0-176">Jeśli proces przechwytywania ręczne hello prawdopodobnie toohang lub strona logowania hello nie niczego (przypadku 3 powyżej), spróbuj proces przechwytywania ręczne hello ponownie.</span><span class="sxs-lookup"><span data-stu-id="dc0e0-176">If hello manual capture process seems toohang, or hello sign in page doesn’t do anything (case 3 above), try hello manual capture process again.</span></span> <span data-ttu-id="dc0e0-177">Jednak to czas, po zakończeniu procesu hello, naciśnij klawisz hello **F12** przycisk tooopen konsoli dla deweloperów w przeglądarce.</span><span class="sxs-lookup"><span data-stu-id="dc0e0-177">But, this time after completing hello process, press hello **F12** button tooopen your browser’s developer console.</span></span> <span data-ttu-id="dc0e0-178">Raz, otwórz hello **konsoli** i typ **window.location= "&lt;wprowadź hello znaku w adresie url zostało określone podczas konfigurowania aplikacji hello&gt;"** , a następnie naciśnij klawisz  **Wprowadź**.</span><span class="sxs-lookup"><span data-stu-id="dc0e0-178">Once there, open hello **console** and type **window.location=”&lt;enter hello sign in url you specified when configuring hello app&gt;”** and then press **Enter**.</span></span> <span data-ttu-id="dc0e0-179">Siła ta strona przekierowywania co zakończyć proces przechwytywania hello i przechowywać hello pola, które została przechwycona.</span><span class="sxs-lookup"><span data-stu-id="dc0e0-179">This force a page redirect which end hello capture process and store hello fields that have been captured.</span></span>

<span data-ttu-id="dc0e0-180">Jeśli z tych metod nie działają dla Ciebie, możemy pomóc.</span><span class="sxs-lookup"><span data-stu-id="dc0e0-180">If none of these approaches work for you, we can help.</span></span> <span data-ttu-id="dc0e0-181">Otwieranie sprawy pomocy technicznej z hello szczegółowe informacje, które miały, a także hello informacje zebrane w hello [jak toosee szczegóły hello powiadomieniu portalu](#i-cannot-manually-detect-sign-in-fields-for-my-application) i [jak tooget pomóc, wysyłając powiadomienia szczegóły tooa pomocy technicznej inżynier](#how-to-get-help-by-sending-notification-details-to-a-support-engineer) sekcje (jeśli dotyczy).</span><span class="sxs-lookup"><span data-stu-id="dc0e0-181">Open a support case with hello details of what you tried, as well as hello information gathered in hello [How toosee hello details of a portal notification](#i-cannot-manually-detect-sign-in-fields-for-my-application) and [How tooget help by sending notification details tooa support engineer](#how-to-get-help-by-sending-notification-details-to-a-support-engineer) sections (if applicable).</span></span>

## <a name="how-tooinstall-hello-access-panel-browser-extension"></a><span data-ttu-id="dc0e0-182">Jak tooinstall hello rozszerzenia przeglądarki panelu dostępu</span><span class="sxs-lookup"><span data-stu-id="dc0e0-182">How tooinstall hello Access Panel Browser extension</span></span>

<span data-ttu-id="dc0e0-183">hello tooinstall rozszerzenia przeglądarki panelu dostępu, wykonaj poniższe kroki hello:</span><span class="sxs-lookup"><span data-stu-id="dc0e0-183">tooinstall hello Access Panel Browser extension, follow hello steps below:</span></span>

1.  <span data-ttu-id="dc0e0-184">Otwórz hello [panelu dostępu](https://myapps.microsoft.com) w jednym z hello obsługiwane przeglądarki i zaloguj się jako **użytkownika** w usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="dc0e0-184">Open hello [Access Panel](https://myapps.microsoft.com) in one of hello supported browsers and sign in as a **user** in your Azure AD.</span></span>

2.  <span data-ttu-id="dc0e0-185">Kliknij przycisk **logowania jednokrotnego hasła aplikacji** w hello panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="dc0e0-185">click a **password-SSO application** in hello Access Panel.</span></span>

3.  <span data-ttu-id="dc0e0-186">Hello monitu pytaniem tooinstall hello oprogramowania, zaznaczyć **Zainstaluj teraz**.</span><span class="sxs-lookup"><span data-stu-id="dc0e0-186">In hello prompt asking tooinstall hello software, select **Install Now**.</span></span>

4.  <span data-ttu-id="dc0e0-187">Oparte na przeglądarce można ukierunkowanej toohello łącze.</span><span class="sxs-lookup"><span data-stu-id="dc0e0-187">Based on your browser you be directed toohello download link.</span></span> <span data-ttu-id="dc0e0-188">**Dodaj** hello rozszerzenia tooyour przeglądarki.</span><span class="sxs-lookup"><span data-stu-id="dc0e0-188">**Add** hello extension tooyour browser.</span></span>

5.  <span data-ttu-id="dc0e0-189">Jeśli przeglądarka pytanie, wybierz tooeither **włączyć** lub **Zezwalaj** hello rozszerzenia.</span><span class="sxs-lookup"><span data-stu-id="dc0e0-189">If your browser asks, select tooeither **Enable** or **Allow** hello extension.</span></span>

6.  <span data-ttu-id="dc0e0-190">Wcześniej zainstalowano **ponowne uruchomienie** sesji przeglądarki.</span><span class="sxs-lookup"><span data-stu-id="dc0e0-190">Once installed, **restart** your browser session.</span></span>

7.  <span data-ttu-id="dc0e0-191">Zaloguj się do hello panelu dostępu i zobacz, czy można **uruchamianie** logowania jednokrotnego hasła aplikacji.</span><span class="sxs-lookup"><span data-stu-id="dc0e0-191">Sign in into hello Access Panel and see if you can **launch** your password-SSO applications.</span></span>

<span data-ttu-id="dc0e0-192">Może również pobrać hello rozszerzenia dla programu Chrome, a program Firefox z poniższych linków bezpośrednich hello:</span><span class="sxs-lookup"><span data-stu-id="dc0e0-192">You may also download hello extension for Chrome and Firefox from hello direct links below:</span></span>

-   [<span data-ttu-id="dc0e0-193">Rozszerzenie panelu dostępu Chrome</span><span class="sxs-lookup"><span data-stu-id="dc0e0-193">Chrome Access Panel Extension</span></span>](https://chrome.google.com/webstore/detail/access-panel-extension/ggjhpefgjjfobnfoldnjipclpcfbgbhl)

-   [<span data-ttu-id="dc0e0-194">Rozszerzenie panelu dostępu Firefox</span><span class="sxs-lookup"><span data-stu-id="dc0e0-194">Firefox Access Panel Extension</span></span>](https://addons.mozilla.org/firefox/addon/access-panel-extension/)

## <a name="how-toosee-hello-details-of-a-portal-notification"></a><span data-ttu-id="dc0e0-195">Jak toosee szczegóły hello powiadomieniu portalu</span><span class="sxs-lookup"><span data-stu-id="dc0e0-195">How toosee hello details of a portal notification</span></span>

<span data-ttu-id="dc0e0-196">Szczegóły hello powiadomienia portalu można wyświetlić, wykonując poniższe kroki hello:</span><span class="sxs-lookup"><span data-stu-id="dc0e0-196">You can see hello details of any portal notification by following hello steps below:</span></span>

1.  <span data-ttu-id="dc0e0-197">Kliknij przycisk hello **powiadomienia** ikonę (hello dzwonka) w prawym górnym rogu portalu Azure hello hello</span><span class="sxs-lookup"><span data-stu-id="dc0e0-197">click hello **Notifications** icon (hello bell) in hello upper right of hello Azure Portal</span></span>

2.  <span data-ttu-id="dc0e0-198">Wybierz wszystkich powiadomień w **błąd** stanu (te z toothem dalej czerwony (!)).</span><span class="sxs-lookup"><span data-stu-id="dc0e0-198">Select any notification in an **Error** state (those with a red (!) next toothem).</span></span>

  ><span data-ttu-id="dc0e0-199">! Należy zwrócić uwagę] możesz nie kliknij powiadomienia w **Powodzenie** lub **w toku** stanu.</span><span class="sxs-lookup"><span data-stu-id="dc0e0-199">!NOTE] You cannot click notifications in a **Successful** or **In Progress** state.</span></span>
  >
  >

3.  <span data-ttu-id="dc0e0-200">Ta Otwórz hello **szczegóły powiadomienia** bloku.</span><span class="sxs-lookup"><span data-stu-id="dc0e0-200">This open hello **Notification Details** blade.</span></span>

4.  <span data-ttu-id="dc0e0-201">Dzięki tym informacjom samodzielnie toounderstand więcej szczegółowych informacji o hello problem.</span><span class="sxs-lookup"><span data-stu-id="dc0e0-201">Use this information yourself toounderstand more details about hello problem.</span></span>

5.  <span data-ttu-id="dc0e0-202">Jeśli nadal potrzebujesz pomocy, można również udostępniać te informacje pomocy technicznej odtwarzania lub hello grupy tooget Pomoc produktu o problemie.</span><span class="sxs-lookup"><span data-stu-id="dc0e0-202">If you still need help, you can also share this information with a support engineer or hello product group tooget help with your problem.</span></span>

6.  <span data-ttu-id="dc0e0-203">Kliknij hello **kopiowania** **ikona** toohello rogu hello **błąd kopiowania** toocopy pole tekstowe wszystkich hello tooshare szczegóły powiadomienia o z pracownikiem pomocy technicznej lub produkt grupy.</span><span class="sxs-lookup"><span data-stu-id="dc0e0-203">Click hello **copy** **icon** toohello right of hello **Copy error** textbox toocopy all hello notification details tooshare with a support or product group engineer.</span></span>

## <a name="how-tooget-help-by-sending-notification-details-tooa-support-engineer"></a><span data-ttu-id="dc0e0-204">Jak tooget pomóc, wysyłając powiadomienia szczegóły tooa specjaliście pomocy technicznej</span><span class="sxs-lookup"><span data-stu-id="dc0e0-204">How tooget help by sending notification details tooa support engineer</span></span>

<span data-ttu-id="dc0e0-205">Jest bardzo ważne, aby udostępniać **hello wszystkie dane przedstawione poniżej** z pracownikiem pomocy technicznej, jeśli potrzebujesz pomocy, dzięki czemu mogą one ułatwić szybkie.</span><span class="sxs-lookup"><span data-stu-id="dc0e0-205">It is very important that you share **all hello details listed below** with a support engineer if you need help, so that they can help you quickly.</span></span> <span data-ttu-id="dc0e0-206">Możesz to zrobić w prosty sposób przez **zrobieniem zrzutu ekranu,** lub przez kliknięcie przycisku hello **ikony błędu kopiowania**, znaleziono prawej toohello hello **błąd kopiowania** pola tekstowego.</span><span class="sxs-lookup"><span data-stu-id="dc0e0-206">You can do this easily by **taking a screenshot,** or by clicking hello **Copy error icon**, found toohello right of hello **Copy error** textbox.</span></span>

## <a name="notification-details-explained"></a><span data-ttu-id="dc0e0-207">Szczegóły powiadomienia wyjaśniono</span><span class="sxs-lookup"><span data-stu-id="dc0e0-207">Notification Details Explained</span></span>

<span data-ttu-id="dc0e0-208">Hello poniżej opisano bardziej jakie poszczególnych elementów powiadomień hello oznacza oraz przykłady zapewnia każdego z nich.</span><span class="sxs-lookup"><span data-stu-id="dc0e0-208">hello below explains more what each of hello notification items means, and gives examples of each of them.</span></span>

### <a name="essential-notification-items"></a><span data-ttu-id="dc0e0-209">Elementy podstawowych powiadomień</span><span class="sxs-lookup"><span data-stu-id="dc0e0-209">Essential Notification Items</span></span>

-   <span data-ttu-id="dc0e0-210">**Tytuł** — Witaj opisowy tytuł hello powiadomień</span><span class="sxs-lookup"><span data-stu-id="dc0e0-210">**Title** – hello descriptive title of hello notification</span></span>

    -   <span data-ttu-id="dc0e0-211">Przykład — **ustawienia serwera proxy aplikacji**</span><span class="sxs-lookup"><span data-stu-id="dc0e0-211">Example – **Application proxy settings**</span></span>

-   <span data-ttu-id="dc0e0-212">**Opis elementu** — Witaj opis co nastąpiło w wyniku operacji hello</span><span class="sxs-lookup"><span data-stu-id="dc0e0-212">**Description** – hello description of what occurred as a result of hello operation</span></span>

    -   <span data-ttu-id="dc0e0-213">Przykład — **wewnętrzny wprowadzony adres url jest już używana przez inną aplikację**</span><span class="sxs-lookup"><span data-stu-id="dc0e0-213">Example – **Internal url entered is already being used by another application**</span></span>

-   <span data-ttu-id="dc0e0-214">**Identyfikator powiadomień** — Unikatowy identyfikator hello hello powiadomienia</span><span class="sxs-lookup"><span data-stu-id="dc0e0-214">**Notification Id** – hello unique id of hello notification</span></span>

    -   <span data-ttu-id="dc0e0-215">Przykład — **clientNotification-2adbfc06-2073-4678-a69f-7eb78d96b068**</span><span class="sxs-lookup"><span data-stu-id="dc0e0-215">Example – **clientNotification-2adbfc06-2073-4678-a69f-7eb78d96b068**</span></span>

-   <span data-ttu-id="dc0e0-216">**Identyfikator żądania klienta** — identyfikator określonego żądania hello wprowadzone przez przeglądarkę</span><span class="sxs-lookup"><span data-stu-id="dc0e0-216">**Client Request Id** – hello specific request id made by your browser</span></span>

    -   <span data-ttu-id="dc0e0-217">Przykład — **302fd775-3329-4670-a9f3-bea37004f0bc**</span><span class="sxs-lookup"><span data-stu-id="dc0e0-217">Example – **302fd775-3329-4670-a9f3-bea37004f0bc**</span></span>

-   <span data-ttu-id="dc0e0-218">**Czas UTC sygnatury** — Witaj znaczników czasu, w którym wystąpił hello powiadomień, w formacie UTC</span><span class="sxs-lookup"><span data-stu-id="dc0e0-218">**Time Stamp UTC** – hello timestamp during which hello notification occurred, in UTC</span></span>

    -   <span data-ttu-id="dc0e0-219">Przykład — **2017-03-23T19:50:43.7583681Z**</span><span class="sxs-lookup"><span data-stu-id="dc0e0-219">Example – **2017-03-23T19:50:43.7583681Z**</span></span>

-   <span data-ttu-id="dc0e0-220">**Wewnętrzny identyfikator transakcji** — Witaj wewnętrzny identyfikator możemy użyć błąd hello toolook w naszych systemów</span><span class="sxs-lookup"><span data-stu-id="dc0e0-220">**Internal Transaction Id** – hello internal ID we can use toolook hello error up in our systems</span></span>

    -   <span data-ttu-id="dc0e0-221">Przykład — **71a2f329-ca29-402f-aa72-bc00a7aca603**</span><span class="sxs-lookup"><span data-stu-id="dc0e0-221">Example – **71a2f329-ca29-402f-aa72-bc00a7aca603**</span></span>

-   <span data-ttu-id="dc0e0-222">**Nazwa UPN** — Witaj użytkownika, który wykonał operację hello</span><span class="sxs-lookup"><span data-stu-id="dc0e0-222">**UPN** – hello user who performed hello operation</span></span>

    -   <span data-ttu-id="dc0e0-223">Przykład —**tperkins@f128.info**</span><span class="sxs-lookup"><span data-stu-id="dc0e0-223">Example – **tperkins@f128.info**</span></span>

-   <span data-ttu-id="dc0e0-224">**Identyfikator dzierżawy** — Unikatowy identyfikator dzierżawy hello, która hello użytkownika wykonującego operację hello hello był członkiem</span><span class="sxs-lookup"><span data-stu-id="dc0e0-224">**Tenant Id** – hello unique ID of hello tenant that hello user who performed hello operation was a member of</span></span>

    -   <span data-ttu-id="dc0e0-225">Przykład — **7918d4b5-0442-4a97-be2d-36f9f9962ece**</span><span class="sxs-lookup"><span data-stu-id="dc0e0-225">Example – **7918d4b5-0442-4a97-be2d-36f9f9962ece**</span></span>

-   <span data-ttu-id="dc0e0-226">**Identyfikator obiektu użytkownika** — Witaj Unikatowy identyfikator hello użytkownika, który wykonał operację hello</span><span class="sxs-lookup"><span data-stu-id="dc0e0-226">**User object Id** – hello unique ID of hello user who performed hello operation</span></span>

    -   <span data-ttu-id="dc0e0-227">Przykład — **17f84be4-51f8-483a-b533-383791227a99**</span><span class="sxs-lookup"><span data-stu-id="dc0e0-227">Example – **17f84be4-51f8-483a-b533-383791227a99**</span></span>

### <a name="detailed-notification-items"></a><span data-ttu-id="dc0e0-228">Elementy szczegółowe powiadomienia</span><span class="sxs-lookup"><span data-stu-id="dc0e0-228">Detailed Notification Items</span></span>

-   <span data-ttu-id="dc0e0-229">**Nazwa wyświetlana** — **(może być pusta)** nazwę wyświetlaną bardziej szczegółowy błąd hello</span><span class="sxs-lookup"><span data-stu-id="dc0e0-229">**Display Name** – **(can be empty)** a more detailed display name for hello error</span></span>

    -   <span data-ttu-id="dc0e0-230">Przykład * — **ustawienia serwera proxy aplikacji**</span><span class="sxs-lookup"><span data-stu-id="dc0e0-230">Example *– **Application proxy settings**</span></span>

-   <span data-ttu-id="dc0e0-231">**Stan** — Witaj określonego stanu hello powiadomień</span><span class="sxs-lookup"><span data-stu-id="dc0e0-231">**Status** – hello specific status of hello notification</span></span>

    -   <span data-ttu-id="dc0e0-232">Przykład * — **nie powiodło się**</span><span class="sxs-lookup"><span data-stu-id="dc0e0-232">Example *– **Failed**</span></span>

-   <span data-ttu-id="dc0e0-233">**Obiekt o identyfikatorze** — **(może być pusta)** hello Identyfikatora obiektu, względem których hello wykonano operację</span><span class="sxs-lookup"><span data-stu-id="dc0e0-233">**Object Id** – **(can be empty)** hello object ID against which hello operation was performed</span></span>

    -   <span data-ttu-id="dc0e0-234">Przykład — **8e08161d-f2fd-40ad-a34a-a9632d6bb599**</span><span class="sxs-lookup"><span data-stu-id="dc0e0-234">Example – **8e08161d-f2fd-40ad-a34a-a9632d6bb599**</span></span>

-   <span data-ttu-id="dc0e0-235">**Szczegóły** — Witaj szczegółowy opis co nastąpiło w wyniku operacji hello</span><span class="sxs-lookup"><span data-stu-id="dc0e0-235">**Details** – hello detailed description of what occurred as a result of hello operation</span></span>

    -   <span data-ttu-id="dc0e0-236">Przykład — **wewnętrznego adresu url "http://bing.com/" jest nieprawidłowy, ponieważ jest już używana**</span><span class="sxs-lookup"><span data-stu-id="dc0e0-236">Example – **Internal url 'http://bing.com/' is invalid since it is already in use**</span></span>

-   <span data-ttu-id="dc0e0-237">**Błąd kopiowania** — kliknij hello **ikonę kopiowania** toohello rogu hello **błąd kopiowania** toocopy pole tekstowe wszystkich hello tooshare szczegóły powiadomienia o inżyniera grupa pomocy technicznej lub produktu</span><span class="sxs-lookup"><span data-stu-id="dc0e0-237">**Copy error** – Click hello **copy icon** toohello right of hello **Copy error** textbox toocopy all hello notification details tooshare with a support or product group engineer</span></span>

    -   <span data-ttu-id="dc0e0-238">Przykład —```{"errorCode":"InternalUrl\_Duplicate","localizedErrorDetails":{"errorDetail":"Internal url 'http://google.com/' is invalid since it is already in use"},"operationResults":\[{"objectId":null,"displayName":null,"status":0,"details":"Internal url 'http://bing.com/' is invalid since it is already in use"}\],"timeStampUtc":"2017-03-23T19:50:26.465743Z","clientRequestId":"302fd775-3329-4670-a9f3-bea37004f0bb","internalTransactionId":"ea5b5475-03b9-4f08-8e95-bbb11289ab65","upn":"tperkins@f128.info","tenantId":"7918d4b5-0442-4a97-be2d-36f9f9962ece","userObjectId":"17f84be4-51f8-483a-b533-383791227a99"}```</span><span class="sxs-lookup"><span data-stu-id="dc0e0-238">Example – ```{"errorCode":"InternalUrl\_Duplicate","localizedErrorDetails":{"errorDetail":"Internal url 'http://google.com/' is invalid since it is already in use"},"operationResults":\[{"objectId":null,"displayName":null,"status":0,"details":"Internal url 'http://bing.com/' is invalid since it is already in use"}\],"timeStampUtc":"2017-03-23T19:50:26.465743Z","clientRequestId":"302fd775-3329-4670-a9f3-bea37004f0bb","internalTransactionId":"ea5b5475-03b9-4f08-8e95-bbb11289ab65","upn":"tperkins@f128.info","tenantId":"7918d4b5-0442-4a97-be2d-36f9f9962ece","userObjectId":"17f84be4-51f8-483a-b533-383791227a99"}```</span></span>

## <a name="next-steps"></a><span data-ttu-id="dc0e0-239">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="dc0e0-239">Next steps</span></span>
[<span data-ttu-id="dc0e0-240">Podaj aplikacji tooyour rejestracji jednokrotnej z serwerem Proxy aplikacji</span><span class="sxs-lookup"><span data-stu-id="dc0e0-240">Provide single sign-on tooyour apps with Application Proxy</span></span>](active-directory-application-proxy-sso-using-kcd.md)

