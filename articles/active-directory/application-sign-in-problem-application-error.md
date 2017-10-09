---
title: "aaaError na stronie aplikacji po zalogowaniu się | Dokumentacja firmy Microsoft"
description: "Jak tooresolve problemy z usługą Azure AD Zaloguj się, gdy sama aplikacja hello emituje błąd"
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
ms.openlocfilehash: 317b6f8e6417520ead80ae4e26c591ba6b134683
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="error-on-an-applications-page-after-signing-in"></a><span data-ttu-id="d5cc0-103">Błąd na stronie aplikacji po zalogowaniu</span><span class="sxs-lookup"><span data-stu-id="d5cc0-103">Error on an application's page after signing in</span></span>

<span data-ttu-id="d5cc0-104">W tym scenariuszu usługi Azure AD podpisała hello użytkownika w, ale aplikacja hello jest wyświetlany błąd nie zezwala hello toosuccessfully Zakończ hello podczas rejestracji w przepływie.</span><span class="sxs-lookup"><span data-stu-id="d5cc0-104">In this scenario, Azure AD has signed hello user in, but hello application is displaying an error not allowing hello user toosuccessfully finish hello sign in flow.</span></span> <span data-ttu-id="d5cc0-105">W tym scenariuszu aplikacja hello nie akceptuje hello problem odpowiedzi przez usługę Azure AD.</span><span class="sxs-lookup"><span data-stu-id="d5cc0-105">In this scenario, hello application is not accepting hello response issue by Azure AD.</span></span>

<span data-ttu-id="d5cc0-106">Istnieje kilka możliwych przyczyn Dlaczego aplikacji hello zaakceptował hello odpowiedzi z usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="d5cc0-106">There are some possible reasons why hello application didn’t accept hello response from Azure AD.</span></span> <span data-ttu-id="d5cc0-107">Jeśli błąd hello w aplikacji hello nie jest wystarczająco wyczyść tooknow co Brak odpowiedzi hello następnie:</span><span class="sxs-lookup"><span data-stu-id="d5cc0-107">If hello error in hello application is not clear enough tooknow what is missing in hello response, then:</span></span>

-   <span data-ttu-id="d5cc0-108">Jeśli aplikacja hello jest galerii hello Azure AD, sprawdź zostały wykonane wszystkie kroki hello w artykule hello [jak toodebug SAML na podstawie pojedynczego logowania jednokrotnego tooapplications w usłudze Azure Active Directory](https://azure.microsoft.com/documentation/articles/active-directory-saml-debugging).</span><span class="sxs-lookup"><span data-stu-id="d5cc0-108">If hello application is hello Azure AD Gallery, verify you have followed all hello steps in hello article [How toodebug SAML-based single sign-on tooapplications in Azure Active Directory](https://azure.microsoft.com/documentation/articles/active-directory-saml-debugging).</span></span>

-   <span data-ttu-id="d5cc0-109">Użyj narzędzia, takiego jak [Fiddler](http://www.telerik.com/fiddler) toocapture SAML żądania, odpowiedzi SAML i tokenu SAML.</span><span class="sxs-lookup"><span data-stu-id="d5cc0-109">Use a tool like [Fiddler](http://www.telerik.com/fiddler) toocapture SAML request, SAML response and SAML token.</span></span>

-   <span data-ttu-id="d5cc0-110">Udostępnij odpowiedzi SAML hello tooknow dostawcy aplikacji hello brakujących.</span><span class="sxs-lookup"><span data-stu-id="d5cc0-110">Share hello SAML response with hello application vendor tooknow what is missing.</span></span>

## <a name="missing-attributes-in-hello-saml-response"></a><span data-ttu-id="d5cc0-111">Brak atrybutów w hello odpowiedzi SAML</span><span class="sxs-lookup"><span data-stu-id="d5cc0-111">Missing attributes in hello SAML response</span></span>

<span data-ttu-id="d5cc0-112">tooadd atrybutu w toobe konfiguracji usługi Azure AD hello wysyłany w odpowiedzi hello Azure AD, wykonaj poniższe kroki hello:</span><span class="sxs-lookup"><span data-stu-id="d5cc0-112">tooadd an attribute in hello Azure AD configuration toobe sent in hello Azure AD response, follow hello steps below:</span></span>

1.  <span data-ttu-id="d5cc0-113">Otwórz hello [ **Azure Portal** ](https://portal.azure.com/) i zaloguj się jako **administratora globalnego** lub **ko-administratora.**</span><span class="sxs-lookup"><span data-stu-id="d5cc0-113">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="d5cc0-114">Otwórz hello **rozszerzenia usług Azure Active Directory** klikając **więcej usług** u dołu menu nawigacji głównego po lewej stronie powitania hello.</span><span class="sxs-lookup"><span data-stu-id="d5cc0-114">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="d5cc0-115">Wpisz w **"Azure Active Directory**" w polu wyszukiwania filtr hello a wybierz hello **usługi Azure Active Directory** elementu.</span><span class="sxs-lookup"><span data-stu-id="d5cc0-115">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="d5cc0-116">Kliknij przycisk **aplikacje dla przedsiębiorstw** z menu nawigacji po lewej stronie powitania w usłudze Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="d5cc0-116">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="d5cc0-117">Kliknij przycisk **wszystkie aplikacje** tooview listę wszystkich aplikacji.</span><span class="sxs-lookup"><span data-stu-id="d5cc0-117">click **All Applications** tooview a list of all your applications.</span></span>

   * <span data-ttu-id="d5cc0-118">Jeśli nie ma aplikacji hello mają być wyświetlane tutaj, użyj hello **filtru** kontroli u góry hello hello **listę wszystkich aplikacji** i zestaw hello **Pokaż** opcję zbyt **Wszystkie aplikacje.**</span><span class="sxs-lookup"><span data-stu-id="d5cc0-118">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="d5cc0-119">Wybierz aplikację hello ma tooconfigure rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="d5cc0-119">Select hello application you want tooconfigure single sign-on.</span></span>

7.  <span data-ttu-id="d5cc0-120">Po załadowaniu aplikacji hello, kliknij przycisk hello **logowanie jednokrotne** z menu nawigacji po lewej stronie powitania aplikacji.</span><span class="sxs-lookup"><span data-stu-id="d5cc0-120">Once hello application loads, click hello **Single sign-on** from hello application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="d5cc0-121">Kliknij przycisk **wyświetlanie i edytowanie użytkownika wszystkie inne atrybuty w obszarze** hello **atrybuty użytkownika** hello tooedit sekcji atrybutów aplikacji toohello toobe wysyłane w tokenie SAML powitania po zalogowaniu się użytkownika.</span><span class="sxs-lookup"><span data-stu-id="d5cc0-121">click **View and edit all other user attributes under** hello **User Attributes** section tooedit hello attributes toobe sent toohello application in hello SAML token when user sign in.</span></span>

   <span data-ttu-id="d5cc0-122">tooadd atrybutu:</span><span class="sxs-lookup"><span data-stu-id="d5cc0-122">tooadd an attribute:</span></span>

   * <span data-ttu-id="d5cc0-123">Kliknij przycisk **Dodaj atrybut**.</span><span class="sxs-lookup"><span data-stu-id="d5cc0-123">click **Add attribute**.</span></span> <span data-ttu-id="d5cc0-124">Wprowadź hello **nazwa** i wybierz hello hello **wartość** z listy rozwijanej hello.</span><span class="sxs-lookup"><span data-stu-id="d5cc0-124">Enter hello **Name** and hello select hello **Value** from hello dropdown.</span></span>

   * <span data-ttu-id="d5cc0-125">Kliknij przycisk **zapisać.**</span><span class="sxs-lookup"><span data-stu-id="d5cc0-125">Click **Save.**</span></span> <span data-ttu-id="d5cc0-126">Zostanie wyświetlony nowy atrybut hello hello tabeli.</span><span class="sxs-lookup"><span data-stu-id="d5cc0-126">You see hello new attribute in hello table.</span></span>

9.  <span data-ttu-id="d5cc0-127">Zapisz konfigurację hello.</span><span class="sxs-lookup"><span data-stu-id="d5cc0-127">Save hello configuration.</span></span>

<span data-ttu-id="d5cc0-128">Następnym zalogowaniu użytkownika hello toohello aplikacji, usługi Azure AD Wyślij nowy atrybut hello w hello odpowiedzi SAML.</span><span class="sxs-lookup"><span data-stu-id="d5cc0-128">Next time hello user signs in toohello application, Azure AD send hello new attribute in hello SAML response.</span></span>

## <a name="hello-application-expects-a-different-user-identifier-value-or-format"></a><span data-ttu-id="d5cc0-129">Aplikacja Hello oczekuje na format lub inną wartość identyfikatora użytkownika</span><span class="sxs-lookup"><span data-stu-id="d5cc0-129">hello application expects a different User Identifier value or format</span></span>

<span data-ttu-id="d5cc0-130">Witaj toohello logowania aplikacji kończy się niepowodzeniem ponieważ hello odpowiedzi SAML nie ma atrybutów, takich jak role lub aplikacji hello oczekuje inny format hello EntityID atrybutu.</span><span class="sxs-lookup"><span data-stu-id="d5cc0-130">hello sign-in toohello application is failing because hello SAML response is missing attributes such as roles or because hello application is expecting a different format for hello EntityID attribute.</span></span>

## <a name="add-an-attribute-in-hello-azure-ad-application-configuration"></a><span data-ttu-id="d5cc0-131">Dodaj atrybut w konfiguracji aplikacji hello Azure AD:</span><span class="sxs-lookup"><span data-stu-id="d5cc0-131">Add an attribute in hello Azure AD application configuration:</span></span>

<span data-ttu-id="d5cc0-132">hello toochange wartość identyfikatora użytkownika, wykonaj poniższe kroki hello:</span><span class="sxs-lookup"><span data-stu-id="d5cc0-132">toochange hello User Identifier value, follow hello steps below:</span></span>

1.  <span data-ttu-id="d5cc0-133">Otwórz hello [ **Azure Portal** ](https://portal.azure.com/) i zaloguj się jako **administratora globalnego** lub **ko-administratora.**</span><span class="sxs-lookup"><span data-stu-id="d5cc0-133">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="d5cc0-134">Otwórz hello **rozszerzenia usług Azure Active Directory** klikając **więcej usług** u dołu menu nawigacji głównego po lewej stronie powitania hello.</span><span class="sxs-lookup"><span data-stu-id="d5cc0-134">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="d5cc0-135">Wpisz w **"Azure Active Directory**" w polu wyszukiwania filtr hello a wybierz hello **usługi Azure Active Directory** elementu.</span><span class="sxs-lookup"><span data-stu-id="d5cc0-135">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="d5cc0-136">Kliknij przycisk **aplikacje dla przedsiębiorstw** z menu nawigacji po lewej stronie powitania w usłudze Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="d5cc0-136">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="d5cc0-137">Kliknij przycisk **wszystkie aplikacje** tooview listę wszystkich aplikacji.</span><span class="sxs-lookup"><span data-stu-id="d5cc0-137">click **All Applications** tooview a list of all your applications.</span></span>

   * <span data-ttu-id="d5cc0-138">Jeśli nie ma aplikacji hello mają być wyświetlane tutaj, użyj hello **filtru** kontroli u góry hello hello **listę wszystkich aplikacji** i zestaw hello **Pokaż** opcję zbyt **Wszystkie aplikacje.**</span><span class="sxs-lookup"><span data-stu-id="d5cc0-138">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="d5cc0-139">Wybierz aplikację hello ma tooconfigure rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="d5cc0-139">Select hello application you want tooconfigure single sign-on.</span></span>

7.  <span data-ttu-id="d5cc0-140">Po załadowaniu aplikacji hello, kliknij przycisk hello **logowanie jednokrotne** z menu nawigacji po lewej stronie powitania aplikacji.</span><span class="sxs-lookup"><span data-stu-id="d5cc0-140">Once hello application loads, click hello **Single sign-on** from hello application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="d5cc0-141">W obszarze hello **atrybuty użytkownika**, wybierz hello Unikatowy identyfikator dla użytkowników w hello **identyfikator użytkownika** listy rozwijanej.</span><span class="sxs-lookup"><span data-stu-id="d5cc0-141">Under hello **User attributes**, select hello unique identifier for your users in hello **User Identifier** dropdown.</span></span>

## <a name="change-entityid-user-identifier-format"></a><span data-ttu-id="d5cc0-142">Zmiana formatu EntityID (identyfikator użytkownika)</span><span class="sxs-lookup"><span data-stu-id="d5cc0-142">Change EntityID (User Identifier) format</span></span>

<span data-ttu-id="d5cc0-143">Jeśli aplikacja hello oczekuje innego formatu hello EntityID atrybutu.</span><span class="sxs-lookup"><span data-stu-id="d5cc0-143">If hello application expects another format for hello EntityID attribute.</span></span> <span data-ttu-id="d5cc0-144">Następnie będzie format EntityID (identyfikator użytkownika) hello stanie tooselect usługi Azure AD wysyła toohello aplikacji hello odpowiedzi po uwierzytelnieniu użytkownika.</span><span class="sxs-lookup"><span data-stu-id="d5cc0-144">Then, you won’t be able tooselect hello EntityID (User Identifier) format that Azure AD sends toohello application in hello response after user authentication.</span></span>

<span data-ttu-id="d5cc0-145">Azure AD hello wybierz format dla atrybutu NameID hello (identyfikator użytkownika) oparte na wybranej wartości hello lub hello żądany przez aplikację hello w hello SAML AuthRequest format.</span><span class="sxs-lookup"><span data-stu-id="d5cc0-145">Azure AD select hello format for hello NameID attribute (User Identifier) based on hello value selected or hello format requested by hello application in hello SAML AuthRequest.</span></span> <span data-ttu-id="d5cc0-146">Aby uzyskać więcej informacji można znaleźć w artykule hello [protokołu SAML rejestracji jednokrotnej](https://docs.microsoft.com/azure/active-directory/develop/active-directory-single-sign-on-protocol-reference#authnrequest) w hello sekcja NameIDPolicy.</span><span class="sxs-lookup"><span data-stu-id="d5cc0-146">For more information visit hello article [Single Sign-On SAML protocol](https://docs.microsoft.com/azure/active-directory/develop/active-directory-single-sign-on-protocol-reference#authnrequest) under hello section NameIDPolicy.</span></span>

## <a name="hello-application-expects-a-different-signature-method-for-hello-saml-response"></a><span data-ttu-id="d5cc0-147">Aplikacja Hello oczekuje inny podpis metody hello odpowiedzi SAML</span><span class="sxs-lookup"><span data-stu-id="d5cc0-147">hello application expects a different signature method for hello SAML response</span></span>

<span data-ttu-id="d5cc0-148">toochange, które części tokenu SAML hello są podpisane cyfrowo przez usługę Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="d5cc0-148">toochange what parts of hello SAML token are digitally signed by Azure Active Directory.</span></span> <span data-ttu-id="d5cc0-149">Wykonaj poniższe kroki hello:</span><span class="sxs-lookup"><span data-stu-id="d5cc0-149">Follow hello steps below:</span></span>

1.  <span data-ttu-id="d5cc0-150">Otwórz hello [ **Azure Portal** ](https://portal.azure.com/) i zaloguj się jako **administratora globalnego** lub **ko-administratora.**</span><span class="sxs-lookup"><span data-stu-id="d5cc0-150">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="d5cc0-151">Otwórz hello **rozszerzenia usług Azure Active Directory** klikając **więcej usług** u dołu menu nawigacji głównego po lewej stronie powitania hello.</span><span class="sxs-lookup"><span data-stu-id="d5cc0-151">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="d5cc0-152">Wpisz w **"Azure Active Directory**" w polu wyszukiwania filtr hello a wybierz hello **usługi Azure Active Directory** elementu.</span><span class="sxs-lookup"><span data-stu-id="d5cc0-152">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="d5cc0-153">Kliknij przycisk **aplikacje dla przedsiębiorstw** z menu nawigacji po lewej stronie powitania w usłudze Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="d5cc0-153">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="d5cc0-154">Kliknij przycisk **wszystkie aplikacje** tooview listę wszystkich aplikacji.</span><span class="sxs-lookup"><span data-stu-id="d5cc0-154">click **All Applications** tooview a list of all your applications.</span></span>

  * <span data-ttu-id="d5cc0-155">Jeśli nie ma aplikacji hello mają być wyświetlane tutaj, użyj hello **filtru** kontroli u góry hello hello **listę wszystkich aplikacji** i zestaw hello **Pokaż** opcję zbyt **Wszystkie aplikacje.**</span><span class="sxs-lookup"><span data-stu-id="d5cc0-155">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="d5cc0-156">Wybierz aplikację hello ma tooconfigure rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="d5cc0-156">Select hello application you want tooconfigure single sign-on.</span></span>

7.  <span data-ttu-id="d5cc0-157">Po załadowaniu aplikacji hello, kliknij przycisk hello **logowanie jednokrotne** z menu nawigacji po lewej stronie powitania aplikacji.</span><span class="sxs-lookup"><span data-stu-id="d5cc0-157">Once hello application loads, click hello **Single sign-on** from hello application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="d5cc0-158">Kliknij przycisk **Pokaż zaawansowane ustawienia podpisywania certyfikatu** w obszarze hello **certyfikat podpisywania SAML** sekcji.</span><span class="sxs-lookup"><span data-stu-id="d5cc0-158">click **Show advanced certificate signing settings** under hello **SAML Signing Certificate** section.</span></span>

9.  <span data-ttu-id="d5cc0-159">Wybierz odpowiednie hello **opcja podpisywania** oczekiwany przez aplikacji hello:</span><span class="sxs-lookup"><span data-stu-id="d5cc0-159">Select hello appropriate **Signing Option** expected by hello application:</span></span>

  * <span data-ttu-id="d5cc0-160">Odpowiedzi SAML logowania</span><span class="sxs-lookup"><span data-stu-id="d5cc0-160">Sign SAML response</span></span>

  * <span data-ttu-id="d5cc0-161">Podpisywanie odpowiedzi SAML i potwierdzenia</span><span class="sxs-lookup"><span data-stu-id="d5cc0-161">Sign SAML response and assertion</span></span>

  * <span data-ttu-id="d5cc0-162">Potwierdzenia języka SAML logowania</span><span class="sxs-lookup"><span data-stu-id="d5cc0-162">Sign SAML assertion</span></span>

<span data-ttu-id="d5cc0-163">Następnym zalogowaniu użytkownika hello toohello aplikacji, rejestrowania usługi Azure AD hello część odpowiedzi SAML hello wybrane.</span><span class="sxs-lookup"><span data-stu-id="d5cc0-163">Next time hello user signs in toohello application, Azure AD sign hello part of hello SAML response selected.</span></span>

## <a name="hello-application-expects-hello-signing-algorithm-toobe-sha-1"></a><span data-ttu-id="d5cc0-164">Aplikacja Hello oczekuje hello podpisywania toobe algorytmu SHA-1</span><span class="sxs-lookup"><span data-stu-id="d5cc0-164">hello application expects hello signing algorithm toobe SHA-1</span></span>

<span data-ttu-id="d5cc0-165">Domyślnie program Azure AD podpisuje token SAML hello przy użyciu hello większości algorytmu zabezpieczeń.</span><span class="sxs-lookup"><span data-stu-id="d5cc0-165">By default, Azure AD signs hello SAML token using hello most security algorithm.</span></span> <span data-ttu-id="d5cc0-166">Zmiana algorytmu znak hello tooSHA-1 nie jest zalecane, chyba że wymagane przez aplikację hello.</span><span class="sxs-lookup"><span data-stu-id="d5cc0-166">Changing hello sign algorithm tooSHA-1 is not recommended unless required by hello application.</span></span>

<span data-ttu-id="d5cc0-167">toochange hello algorytm podpisywania, wykonaj poniższe kroki hello:</span><span class="sxs-lookup"><span data-stu-id="d5cc0-167">toochange hello signing algorithm, follow hello steps below:</span></span>

1.  <span data-ttu-id="d5cc0-168">Otwórz hello [ **Azure Portal** ](https://portal.azure.com/) i zaloguj się jako **administratora globalnego** lub **ko-administratora.**</span><span class="sxs-lookup"><span data-stu-id="d5cc0-168">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="d5cc0-169">Otwórz hello **rozszerzenia usług Azure Active Directory** klikając **więcej usług** u dołu menu nawigacji głównego po lewej stronie powitania hello.</span><span class="sxs-lookup"><span data-stu-id="d5cc0-169">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="d5cc0-170">Wpisz w **"Azure Active Directory**" w polu wyszukiwania filtr hello a wybierz hello **usługi Azure Active Directory** elementu.</span><span class="sxs-lookup"><span data-stu-id="d5cc0-170">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="d5cc0-171">Kliknij przycisk **aplikacje dla przedsiębiorstw** z menu nawigacji po lewej stronie powitania w usłudze Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="d5cc0-171">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="d5cc0-172">Kliknij przycisk **wszystkie aplikacje** tooview listę wszystkich aplikacji.</span><span class="sxs-lookup"><span data-stu-id="d5cc0-172">click **All Applications** tooview a list of all your applications.</span></span>

   * <span data-ttu-id="d5cc0-173">Jeśli nie ma aplikacji hello mają być wyświetlane tutaj, użyj hello **filtru** kontroli u góry hello hello **listę wszystkich aplikacji** i zestaw hello **Pokaż** opcję zbyt **Wszystkie aplikacje.**</span><span class="sxs-lookup"><span data-stu-id="d5cc0-173">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="d5cc0-174">Wybierz aplikację hello ma tooconfigure rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="d5cc0-174">Select hello application you want tooconfigure single sign-on.</span></span>

7.  <span data-ttu-id="d5cc0-175">Po załadowaniu aplikacji hello, kliknij przycisk hello **logowanie jednokrotne** z menu nawigacji po lewej stronie powitania aplikacji.</span><span class="sxs-lookup"><span data-stu-id="d5cc0-175">Once hello application loads, click hello **Single sign-on** from hello application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="d5cc0-176">Kliknij przycisk **Pokaż zaawansowane ustawienia podpisywania certyfikatu** w obszarze hello **certyfikat podpisywania SAML** sekcji.</span><span class="sxs-lookup"><span data-stu-id="d5cc0-176">click **Show advanced certificate signing settings** under hello **SAML Signing Certificate** section.</span></span>

9.  <span data-ttu-id="d5cc0-177">Wybierz algorytm SHA-1, hello **algorytm podpisywania**.</span><span class="sxs-lookup"><span data-stu-id="d5cc0-177">Select SHA-1, in hello **Signing Algorithm**.</span></span>

<span data-ttu-id="d5cc0-178">Loguje użytkownika toohello aplikacji hello następnym, rejestrowania usługi Azure AD hello tokenu SAML przy użyciu algorytmu SHA-1.</span><span class="sxs-lookup"><span data-stu-id="d5cc0-178">Next time hello user signs in toohello application, Azure AD sign hello SAML token using SHA-1 algorithm.</span></span>

## <a name="next-steps"></a><span data-ttu-id="d5cc0-179">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="d5cc0-179">Next steps</span></span>
[<span data-ttu-id="d5cc0-180">Jak toodebug SAML na podstawie pojedynczego logowania jednokrotnego tooapplications w usłudze Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="d5cc0-180">How toodebug SAML-based single sign-on tooapplications in Azure Active Directory</span></span>](https://azure.microsoft.com/documentation/articles/active-directory-saml-debugging)
