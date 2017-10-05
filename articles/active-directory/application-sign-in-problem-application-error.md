---
title: "Błąd na stronie aplikacji po zalogowaniu się | Dokumentacja firmy Microsoft"
description: "Jak rozwiązać problemy z logowaniem usługi Azure AD po zgłoszeniu emituje błąd"
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
ms.openlocfilehash: a8cd93256f79ece268ec3411dfbdf590f4b24447
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/03/2017
---
# <a name="error-on-an-applications-page-after-signing-in"></a><span data-ttu-id="1b677-103">Błąd na stronie aplikacji po zalogowaniu</span><span class="sxs-lookup"><span data-stu-id="1b677-103">Error on an application's page after signing in</span></span>

<span data-ttu-id="1b677-104">W tym scenariuszu usługi Azure AD podpisała użytkownika w, ale aplikacja jest wyświetlany błąd nie zezwala na użytkownika do pomyślnego zakończenia logowania w przepływie.</span><span class="sxs-lookup"><span data-stu-id="1b677-104">In this scenario, Azure AD has signed the user in, but the application is displaying an error not allowing the user to successfully finish the sign in flow.</span></span> <span data-ttu-id="1b677-105">W tym scenariuszu aplikacja nie akceptuje problem odpowiedzi przez usługę Azure AD.</span><span class="sxs-lookup"><span data-stu-id="1b677-105">In this scenario, the application is not accepting the response issue by Azure AD.</span></span>

<span data-ttu-id="1b677-106">Istnieje kilka możliwych przyczyn Dlaczego ta aplikacja nie akceptuje odpowiedzi z usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="1b677-106">There are some possible reasons why the application didn’t accept the response from Azure AD.</span></span> <span data-ttu-id="1b677-107">Jeśli ten błąd w aplikacji nie jest jasne, aby dowiedzieć się, czego brakuje w odpowiedzi, następnie:</span><span class="sxs-lookup"><span data-stu-id="1b677-107">If the error in the application is not clear enough to know what is missing in the response, then:</span></span>

-   <span data-ttu-id="1b677-108">Jeśli aplikacja jest w galerii Azure AD, sprawdź zostały wykonane wszystkie kroki opisane w artykule [debugowanie na języku SAML logowanie jednokrotne do aplikacji w usłudze Azure Active Directory](https://azure.microsoft.com/documentation/articles/active-directory-saml-debugging).</span><span class="sxs-lookup"><span data-stu-id="1b677-108">If the application is the Azure AD Gallery, verify you have followed all the steps in the article [How to debug SAML-based single sign-on to applications in Azure Active Directory](https://azure.microsoft.com/documentation/articles/active-directory-saml-debugging).</span></span>

-   <span data-ttu-id="1b677-109">Użyj narzędzia, takiego jak [Fiddler](http://www.telerik.com/fiddler) przechwytywania SAML żądania, odpowiedzi SAML i tokenu SAML.</span><span class="sxs-lookup"><span data-stu-id="1b677-109">Use a tool like [Fiddler](http://www.telerik.com/fiddler) to capture SAML request, SAML response and SAML token.</span></span>

-   <span data-ttu-id="1b677-110">Udostępnianie odpowiedzi SAML z dostawcą aplikacji, aby dowiedzieć się, czego brakuje.</span><span class="sxs-lookup"><span data-stu-id="1b677-110">Share the SAML response with the application vendor to know what is missing.</span></span>

## <a name="missing-attributes-in-the-saml-response"></a><span data-ttu-id="1b677-111">Brak atrybutów w odpowiedzi SAML</span><span class="sxs-lookup"><span data-stu-id="1b677-111">Missing attributes in the SAML response</span></span>

<span data-ttu-id="1b677-112">Aby dodać atrybut w konfiguracji usługi Azure AD do wysłania w odpowiedzi usługi Azure AD, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="1b677-112">To add an attribute in the Azure AD configuration to be sent in the Azure AD response, follow the steps below:</span></span>

1.  <span data-ttu-id="1b677-113">Otwórz [ **Azure Portal** ](https://portal.azure.com/) i zaloguj się jako **administratora globalnego** lub **ko-administratora.**</span><span class="sxs-lookup"><span data-stu-id="1b677-113">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="1b677-114">Otwórz **rozszerzenia usług Azure Active Directory** klikając **więcej usług** u dołu menu nawigacji głównego po lewej stronie.</span><span class="sxs-lookup"><span data-stu-id="1b677-114">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="1b677-115">Wpisz w **"Azure Active Directory**" w polu wyszukiwania filtr a wybierz **usługi Azure Active Directory** elementu.</span><span class="sxs-lookup"><span data-stu-id="1b677-115">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="1b677-116">Kliknij przycisk **aplikacje dla przedsiębiorstw** w menu nawigacji po lewej stronie usługi Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="1b677-116">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="1b677-117">Kliknij przycisk **wszystkie aplikacje** Aby wyświetlić listę wszystkich aplikacji.</span><span class="sxs-lookup"><span data-stu-id="1b677-117">click **All Applications** to view a list of all your applications.</span></span>

   * <span data-ttu-id="1b677-118">Jeśli nie ma aplikacji ma tutaj będą wyświetlane, użyj **filtru** kontroli nad **listę wszystkich aplikacji** i ustaw **Pokaż** opcji w celu **wszystkich aplikacji.**</span><span class="sxs-lookup"><span data-stu-id="1b677-118">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="1b677-119">Wybierz aplikację, aby skonfigurować logowanie jednokrotne.</span><span class="sxs-lookup"><span data-stu-id="1b677-119">Select the application you want to configure single sign-on.</span></span>

7.  <span data-ttu-id="1b677-120">Po załadowaniu aplikacji, kliknij przycisk **logowanie jednokrotne** z menu nawigacji po lewej stronie aplikacji.</span><span class="sxs-lookup"><span data-stu-id="1b677-120">Once the application loads, click the **Single sign-on** from the application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="1b677-121">Kliknij przycisk **wyświetlanie i edytowanie użytkownika wszystkie inne atrybuty w obszarze** **atrybuty użytkownika** sekcji atrybuty przesyłany do aplikacji w tokenie SAML podczas logowania użytkownika.</span><span class="sxs-lookup"><span data-stu-id="1b677-121">click **View and edit all other user attributes under** the **User Attributes** section to edit the attributes to be sent to the application in the SAML token when user sign in.</span></span>

   <span data-ttu-id="1b677-122">Aby dodać atrybutu:</span><span class="sxs-lookup"><span data-stu-id="1b677-122">To add an attribute:</span></span>

   * <span data-ttu-id="1b677-123">Kliknij przycisk **Dodaj atrybut**.</span><span class="sxs-lookup"><span data-stu-id="1b677-123">click **Add attribute**.</span></span> <span data-ttu-id="1b677-124">Wprowadź **nazwa** i wybierz **wartość** z listy rozwijanej.</span><span class="sxs-lookup"><span data-stu-id="1b677-124">Enter the **Name** and the select the **Value** from the dropdown.</span></span>

   * <span data-ttu-id="1b677-125">Kliknij przycisk **zapisać.**</span><span class="sxs-lookup"><span data-stu-id="1b677-125">Click **Save.**</span></span> <span data-ttu-id="1b677-126">Zostanie wyświetlony nowy atrybut w tabeli.</span><span class="sxs-lookup"><span data-stu-id="1b677-126">You see the new attribute in the table.</span></span>

9.  <span data-ttu-id="1b677-127">Zapisz konfigurację.</span><span class="sxs-lookup"><span data-stu-id="1b677-127">Save the configuration.</span></span>

<span data-ttu-id="1b677-128">Następnym razem, gdy użytkownik loguje się do aplikacji usługi Azure AD wysyłanie nowy atrybut w odpowiedzi SAML.</span><span class="sxs-lookup"><span data-stu-id="1b677-128">Next time the user signs in to the application, Azure AD send the new attribute in the SAML response.</span></span>

## <a name="the-application-expects-a-different-user-identifier-value-or-format"></a><span data-ttu-id="1b677-129">Aplikacja oczekuje na format lub inną wartość identyfikatora użytkownika</span><span class="sxs-lookup"><span data-stu-id="1b677-129">The application expects a different User Identifier value or format</span></span>

<span data-ttu-id="1b677-130">Logowanie do aplikacji kończy się niepowodzeniem, ponieważ brak odpowiedzi SAML atrybutów, takich jak role lub aplikacja oczekuje innego formatu dla atrybutu EntityID.</span><span class="sxs-lookup"><span data-stu-id="1b677-130">The sign-in to the application is failing because the SAML response is missing attributes such as roles or because the application is expecting a different format for the EntityID attribute.</span></span>

## <a name="add-an-attribute-in-the-azure-ad-application-configuration"></a><span data-ttu-id="1b677-131">Dodaj atrybut w konfiguracji aplikacji usługi Azure AD:</span><span class="sxs-lookup"><span data-stu-id="1b677-131">Add an attribute in the Azure AD application configuration:</span></span>

<span data-ttu-id="1b677-132">Aby zmienić wartość identyfikatora użytkownika, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="1b677-132">To change the User Identifier value, follow the steps below:</span></span>

1.  <span data-ttu-id="1b677-133">Otwórz [ **Azure Portal** ](https://portal.azure.com/) i zaloguj się jako **administratora globalnego** lub **ko-administratora.**</span><span class="sxs-lookup"><span data-stu-id="1b677-133">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="1b677-134">Otwórz **rozszerzenia usług Azure Active Directory** klikając **więcej usług** u dołu menu nawigacji głównego po lewej stronie.</span><span class="sxs-lookup"><span data-stu-id="1b677-134">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="1b677-135">Wpisz w **"Azure Active Directory**" w polu wyszukiwania filtr a wybierz **usługi Azure Active Directory** elementu.</span><span class="sxs-lookup"><span data-stu-id="1b677-135">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="1b677-136">Kliknij przycisk **aplikacje dla przedsiębiorstw** w menu nawigacji po lewej stronie usługi Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="1b677-136">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="1b677-137">Kliknij przycisk **wszystkie aplikacje** Aby wyświetlić listę wszystkich aplikacji.</span><span class="sxs-lookup"><span data-stu-id="1b677-137">click **All Applications** to view a list of all your applications.</span></span>

   * <span data-ttu-id="1b677-138">Jeśli nie ma aplikacji ma tutaj będą wyświetlane, użyj **filtru** kontroli nad **listę wszystkich aplikacji** i ustaw **Pokaż** opcji w celu **wszystkich aplikacji.**</span><span class="sxs-lookup"><span data-stu-id="1b677-138">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="1b677-139">Wybierz aplikację, aby skonfigurować logowanie jednokrotne.</span><span class="sxs-lookup"><span data-stu-id="1b677-139">Select the application you want to configure single sign-on.</span></span>

7.  <span data-ttu-id="1b677-140">Po załadowaniu aplikacji, kliknij przycisk **logowanie jednokrotne** z menu nawigacji po lewej stronie aplikacji.</span><span class="sxs-lookup"><span data-stu-id="1b677-140">Once the application loads, click the **Single sign-on** from the application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="1b677-141">W obszarze **atrybuty użytkownika**, wybierz Unikatowy identyfikator dla użytkowników w **identyfikator użytkownika** listy rozwijanej.</span><span class="sxs-lookup"><span data-stu-id="1b677-141">Under the **User attributes**, select the unique identifier for your users in the **User Identifier** dropdown.</span></span>

## <a name="change-entityid-user-identifier-format"></a><span data-ttu-id="1b677-142">Zmiana formatu EntityID (identyfikator użytkownika)</span><span class="sxs-lookup"><span data-stu-id="1b677-142">Change EntityID (User Identifier) format</span></span>

<span data-ttu-id="1b677-143">Jeśli aplikacja oczekuje innego formatu dla atrybutu EntityID.</span><span class="sxs-lookup"><span data-stu-id="1b677-143">If the application expects another format for the EntityID attribute.</span></span> <span data-ttu-id="1b677-144">Następnie nie będzie mógł wybrać format EntityID (identyfikator użytkownika), który wysyła usługi Azure AD do aplikacji w odpowiedzi po uwierzytelnieniu użytkownika.</span><span class="sxs-lookup"><span data-stu-id="1b677-144">Then, you won’t be able to select the EntityID (User Identifier) format that Azure AD sends to the application in the response after user authentication.</span></span>

<span data-ttu-id="1b677-145">Wybrano Azure wybierz AD format dla atrybutu NameID (identyfikator użytkownika) na podstawie wartości lub format żądany przez aplikację w SAML AuthRequest.</span><span class="sxs-lookup"><span data-stu-id="1b677-145">Azure AD select the format for the NameID attribute (User Identifier) based on the value selected or the format requested by the application in the SAML AuthRequest.</span></span> <span data-ttu-id="1b677-146">Aby uzyskać więcej informacji można znaleźć w artykule [protokołu SAML rejestracji jednokrotnej](https://docs.microsoft.com/azure/active-directory/develop/active-directory-single-sign-on-protocol-reference#authnrequest) w sekcji NameIDPolicy.</span><span class="sxs-lookup"><span data-stu-id="1b677-146">For more information visit the article [Single Sign-On SAML protocol](https://docs.microsoft.com/azure/active-directory/develop/active-directory-single-sign-on-protocol-reference#authnrequest) under the section NameIDPolicy.</span></span>

## <a name="the-application-expects-a-different-signature-method-for-the-saml-response"></a><span data-ttu-id="1b677-147">Aplikacja oczekuje metody inny podpis dla odpowiedzi SAML</span><span class="sxs-lookup"><span data-stu-id="1b677-147">The application expects a different signature method for the SAML response</span></span>

<span data-ttu-id="1b677-148">Aby zmienić, które części tokenu SAML są podpisane cyfrowo przez usługę Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="1b677-148">To change what parts of the SAML token are digitally signed by Azure Active Directory.</span></span> <span data-ttu-id="1b677-149">Wykonaj poniższe kroki:</span><span class="sxs-lookup"><span data-stu-id="1b677-149">Follow the steps below:</span></span>

1.  <span data-ttu-id="1b677-150">Otwórz [ **Azure Portal** ](https://portal.azure.com/) i zaloguj się jako **administratora globalnego** lub **ko-administratora.**</span><span class="sxs-lookup"><span data-stu-id="1b677-150">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="1b677-151">Otwórz **rozszerzenia usług Azure Active Directory** klikając **więcej usług** u dołu menu nawigacji głównego po lewej stronie.</span><span class="sxs-lookup"><span data-stu-id="1b677-151">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="1b677-152">Wpisz w **"Azure Active Directory**" w polu wyszukiwania filtr a wybierz **usługi Azure Active Directory** elementu.</span><span class="sxs-lookup"><span data-stu-id="1b677-152">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="1b677-153">Kliknij przycisk **aplikacje dla przedsiębiorstw** w menu nawigacji po lewej stronie usługi Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="1b677-153">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="1b677-154">Kliknij przycisk **wszystkie aplikacje** Aby wyświetlić listę wszystkich aplikacji.</span><span class="sxs-lookup"><span data-stu-id="1b677-154">click **All Applications** to view a list of all your applications.</span></span>

  * <span data-ttu-id="1b677-155">Jeśli nie ma aplikacji ma tutaj będą wyświetlane, użyj **filtru** kontroli nad **listę wszystkich aplikacji** i ustaw **Pokaż** opcji w celu **wszystkich aplikacji.**</span><span class="sxs-lookup"><span data-stu-id="1b677-155">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="1b677-156">Wybierz aplikację, aby skonfigurować logowanie jednokrotne.</span><span class="sxs-lookup"><span data-stu-id="1b677-156">Select the application you want to configure single sign-on.</span></span>

7.  <span data-ttu-id="1b677-157">Po załadowaniu aplikacji, kliknij przycisk **logowanie jednokrotne** z menu nawigacji po lewej stronie aplikacji.</span><span class="sxs-lookup"><span data-stu-id="1b677-157">Once the application loads, click the **Single sign-on** from the application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="1b677-158">Kliknij przycisk **Pokaż zaawansowane ustawienia podpisywania certyfikatu** w obszarze **certyfikat podpisywania SAML** sekcji.</span><span class="sxs-lookup"><span data-stu-id="1b677-158">click **Show advanced certificate signing settings** under the **SAML Signing Certificate** section.</span></span>

9.  <span data-ttu-id="1b677-159">Wybierz odpowiednie **opcja podpisywania** oczekiwany przez aplikację:</span><span class="sxs-lookup"><span data-stu-id="1b677-159">Select the appropriate **Signing Option** expected by the application:</span></span>

  * <span data-ttu-id="1b677-160">Odpowiedzi SAML logowania</span><span class="sxs-lookup"><span data-stu-id="1b677-160">Sign SAML response</span></span>

  * <span data-ttu-id="1b677-161">Podpisywanie odpowiedzi SAML i potwierdzenia</span><span class="sxs-lookup"><span data-stu-id="1b677-161">Sign SAML response and assertion</span></span>

  * <span data-ttu-id="1b677-162">Potwierdzenia języka SAML logowania</span><span class="sxs-lookup"><span data-stu-id="1b677-162">Sign SAML assertion</span></span>

<span data-ttu-id="1b677-163">Następnym razem, gdy użytkownik loguje się do aplikacji usługi Azure AD podpisać części odpowiedzi SAML wybrane.</span><span class="sxs-lookup"><span data-stu-id="1b677-163">Next time the user signs in to the application, Azure AD sign the part of the SAML response selected.</span></span>

## <a name="the-application-expects-the-signing-algorithm-to-be-sha-1"></a><span data-ttu-id="1b677-164">Aplikacja oczekuje podpisywania algorytmu SHA-1</span><span class="sxs-lookup"><span data-stu-id="1b677-164">The application expects the signing algorithm to be SHA-1</span></span>

<span data-ttu-id="1b677-165">Domyślnie usługi Azure AD zaloguje się przy użyciu algorytmu większości zabezpieczeń tokenu SAML.</span><span class="sxs-lookup"><span data-stu-id="1b677-165">By default, Azure AD signs the SAML token using the most security algorithm.</span></span> <span data-ttu-id="1b677-166">Zmiana logowania algorytmu SHA-1 nie jest zalecane, chyba że wymagane przez aplikację.</span><span class="sxs-lookup"><span data-stu-id="1b677-166">Changing the sign algorithm to SHA-1 is not recommended unless required by the application.</span></span>

<span data-ttu-id="1b677-167">Aby zmienić algorytm podpisywania, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="1b677-167">To change the signing algorithm, follow the steps below:</span></span>

1.  <span data-ttu-id="1b677-168">Otwórz [ **Azure Portal** ](https://portal.azure.com/) i zaloguj się jako **administratora globalnego** lub **ko-administratora.**</span><span class="sxs-lookup"><span data-stu-id="1b677-168">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="1b677-169">Otwórz **rozszerzenia usług Azure Active Directory** klikając **więcej usług** u dołu menu nawigacji głównego po lewej stronie.</span><span class="sxs-lookup"><span data-stu-id="1b677-169">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="1b677-170">Wpisz w **"Azure Active Directory**" w polu wyszukiwania filtr a wybierz **usługi Azure Active Directory** elementu.</span><span class="sxs-lookup"><span data-stu-id="1b677-170">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="1b677-171">Kliknij przycisk **aplikacje dla przedsiębiorstw** w menu nawigacji po lewej stronie usługi Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="1b677-171">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="1b677-172">Kliknij przycisk **wszystkie aplikacje** Aby wyświetlić listę wszystkich aplikacji.</span><span class="sxs-lookup"><span data-stu-id="1b677-172">click **All Applications** to view a list of all your applications.</span></span>

   * <span data-ttu-id="1b677-173">Jeśli nie ma aplikacji ma tutaj będą wyświetlane, użyj **filtru** kontroli nad **listę wszystkich aplikacji** i ustaw **Pokaż** opcji w celu **wszystkich aplikacji.**</span><span class="sxs-lookup"><span data-stu-id="1b677-173">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="1b677-174">Wybierz aplikację, aby skonfigurować logowanie jednokrotne.</span><span class="sxs-lookup"><span data-stu-id="1b677-174">Select the application you want to configure single sign-on.</span></span>

7.  <span data-ttu-id="1b677-175">Po załadowaniu aplikacji, kliknij przycisk **logowanie jednokrotne** z menu nawigacji po lewej stronie aplikacji.</span><span class="sxs-lookup"><span data-stu-id="1b677-175">Once the application loads, click the **Single sign-on** from the application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="1b677-176">Kliknij przycisk **Pokaż zaawansowane ustawienia podpisywania certyfikatu** w obszarze **certyfikat podpisywania SAML** sekcji.</span><span class="sxs-lookup"><span data-stu-id="1b677-176">click **Show advanced certificate signing settings** under the **SAML Signing Certificate** section.</span></span>

9.  <span data-ttu-id="1b677-177">Wybierz algorytm SHA-1, **algorytm podpisywania**.</span><span class="sxs-lookup"><span data-stu-id="1b677-177">Select SHA-1, in the **Signing Algorithm**.</span></span>

<span data-ttu-id="1b677-178">Następnym razem, gdy użytkownik loguje się do aplikacji usługi Azure AD Zaloguj się przy użyciu algorytmu SHA-1 tokenu SAML.</span><span class="sxs-lookup"><span data-stu-id="1b677-178">Next time the user signs in to the application, Azure AD sign the SAML token using SHA-1 algorithm.</span></span>

## <a name="next-steps"></a><span data-ttu-id="1b677-179">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="1b677-179">Next steps</span></span>
[<span data-ttu-id="1b677-180">Debugowanie na języku SAML logowanie jednokrotne do aplikacji w usłudze Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="1b677-180">How to debug SAML-based single sign-on to applications in Azure Active Directory</span></span>](https://azure.microsoft.com/documentation/articles/active-directory-saml-debugging)
