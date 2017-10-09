---
title: "podpisywania aplikacji z systemem innym niż galerii tooa skonfigurowane dla federacyjnych aaaProblems logowanie jednokrotne | Dokumentacja firmy Microsoft"
description: "Wskazówki dotyczące hello określonych problemów, które mogą się spodziewać przy logowaniu się w aplikacji tooan skonfigurowane na podstawie SAML federacyjne logowanie jednokrotne z usługą Azure AD"
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
ms.openlocfilehash: 1243456695c097f404a66fc89893efa2afdaaf22
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="problems-signing-in-tooa-non-gallery-application-configured-for-federated-single-sign-on"></a><span data-ttu-id="1a53c-103">Problemy z zarejestrowaniem w aplikacji innej niż galerii tooa skonfigurowany dla federacyjnego logowania jednokrotnego</span><span class="sxs-lookup"><span data-stu-id="1a53c-103">Problems signing in tooa non-gallery application configured for federated single sign-on</span></span>

<span data-ttu-id="1a53c-104">tootroubleshoot problemu, wymagana konfiguracja aplikacji hello tooverify w usłudze Azure AD następująco:</span><span class="sxs-lookup"><span data-stu-id="1a53c-104">tootroubleshoot your problem, you need tooverify hello application configuration in Azure AD as follow:</span></span>

-   <span data-ttu-id="1a53c-105">Zostały wykonane wszystkie kroki konfiguracji hello hello aplikacji galerii Azure AD.</span><span class="sxs-lookup"><span data-stu-id="1a53c-105">You have followed all hello configuration steps for hello Azure AD gallery application.</span></span>

-   <span data-ttu-id="1a53c-106">Witaj identyfikator i adres URL odpowiedzi, skonfigurowane w usłudze AAD zgodne one oczekiwanych wartości w aplikacji hello</span><span class="sxs-lookup"><span data-stu-id="1a53c-106">hello Identifier and Reply URL configured in AAD match they expected values in hello application</span></span>

-   <span data-ttu-id="1a53c-107">Użytkownicy przypisano toohello aplikacji</span><span class="sxs-lookup"><span data-stu-id="1a53c-107">You have assigned users toohello application</span></span>

## <a name="application-not-found-in-directory"></a><span data-ttu-id="1a53c-108">Nie można odnaleźć w katalogu aplikacji</span><span class="sxs-lookup"><span data-stu-id="1a53c-108">Application not found in directory</span></span>

<span data-ttu-id="1a53c-109">*Błąd AADSTS70001: Nie znaleziono aplikacji o identyfikatorze "https://contoso.com" w katalogu hello*.</span><span class="sxs-lookup"><span data-stu-id="1a53c-109">*Error AADSTS70001: Application with Identifier ‘https://contoso.com’ was not found in hello directory*.</span></span>

<span data-ttu-id="1a53c-110">**Możliwa przyczyna**</span><span class="sxs-lookup"><span data-stu-id="1a53c-110">**Possible cause**</span></span>

<span data-ttu-id="1a53c-111">Witaj wystawca atrybutu wysyła z tooAzure aplikacji hello AD w żądaniu SAML hello jest niezgodny hello identyfikator wartości ustawionej w aplikacji hello Azure AD.</span><span class="sxs-lookup"><span data-stu-id="1a53c-111">hello Issuer attribute sends from hello application tooAzure AD in hello SAML request doesn’t match hello Identifier value configured in hello application Azure AD.</span></span>

<span data-ttu-id="1a53c-112">**Rozdzielczość**</span><span class="sxs-lookup"><span data-stu-id="1a53c-112">**Resolution**</span></span>

<span data-ttu-id="1a53c-113">Upewnij się, ten atrybut wystawcy hello w hello SAML żądanie jest zgodne hello wartość identyfikatora skonfigurowane w usłudze Azure AD:</span><span class="sxs-lookup"><span data-stu-id="1a53c-113">Ensure that hello Issuer attribute in hello SAML request it’s matching hello Identifier value configured in Azure AD:</span></span>

1.  <span data-ttu-id="1a53c-114">Otwórz hello [ **Azure Portal** ](https://portal.azure.com/) i zaloguj się jako **administratora globalnego** lub **ko-administratora.**</span><span class="sxs-lookup"><span data-stu-id="1a53c-114">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="1a53c-115">Otwórz hello **rozszerzenia usług Azure Active Directory** klikając **więcej usług** u dołu menu nawigacji głównego po lewej stronie powitania hello.</span><span class="sxs-lookup"><span data-stu-id="1a53c-115">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="1a53c-116">Wpisz w **"Azure Active Directory**" w polu wyszukiwania filtr hello a wybierz hello **usługi Azure Active Directory** elementu.</span><span class="sxs-lookup"><span data-stu-id="1a53c-116">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="1a53c-117">Kliknij przycisk **aplikacje dla przedsiębiorstw** z menu nawigacji po lewej stronie powitania w usłudze Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="1a53c-117">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="1a53c-118">Kliknij przycisk **wszystkie aplikacje** tooview listę wszystkich aplikacji.</span><span class="sxs-lookup"><span data-stu-id="1a53c-118">click **All Applications** tooview a list of all your applications.</span></span>

   * <span data-ttu-id="1a53c-119">Jeśli nie ma aplikacji hello mają być wyświetlane tutaj, użyj hello **filtru** kontroli u góry hello hello **listę wszystkich aplikacji** i zestaw hello **Pokaż** opcję zbyt **Wszystkie aplikacje.**</span><span class="sxs-lookup"><span data-stu-id="1a53c-119">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="1a53c-120">Wybierz aplikację hello ma tooconfigure rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="1a53c-120">Select hello application you want tooconfigure single sign-on.</span></span>

7.  <span data-ttu-id="1a53c-121">Po załadowaniu aplikacji hello, kliknij przycisk hello **logowanie jednokrotne** z menu nawigacji po lewej stronie powitania aplikacji.</span><span class="sxs-lookup"><span data-stu-id="1a53c-121">Once hello application loads, click hello **Single sign-on** from hello application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="1a53c-122"><span id="_Hlk477190042" class="anchor"></span>Przejdź za**domeny i adres URL** sekcji.</span><span class="sxs-lookup"><span data-stu-id="1a53c-122"><span id="_Hlk477190042" class="anchor"></span>Go too**Domain and URLs** section.</span></span> <span data-ttu-id="1a53c-123">Sprawdź, czy hello w hello identyfikator hello wartość hello identyfikator wyświetlany omyłkowo hello jest zgodne z pola tekstowego.</span><span class="sxs-lookup"><span data-stu-id="1a53c-123">Verify that hello value in hello Identifier textbox is matching hello value for hello identifier value displayed in hello error.</span></span>

<span data-ttu-id="1a53c-124">Po wartości identyfikatora hello zostały zaktualizowane w usłudze Azure AD i jej pasującego hello wartości wysyła aplikacja hello w żądaniu SAML hello, powinno być możliwe toosign w toohello aplikacji.</span><span class="sxs-lookup"><span data-stu-id="1a53c-124">After you have updated hello Identifier value in Azure AD and it’s matching hello value sends by hello application in hello SAML request, you should be able toosign in toohello application.</span></span>

## <a name="hello-reply-address-does-not-match-hello-reply-addresses-configured-for-hello-application"></a><span data-ttu-id="1a53c-125">adres zwrotny Hello jest niezgodna z adresów odpowiedzi hello skonfigurowanych dla aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="1a53c-125">hello reply address does not match hello reply addresses configured for hello application.</span></span> 

<span data-ttu-id="1a53c-126">*Błąd AADSTS50011: hello odpowiedzi adres "https://contoso.com" jest niezgodny adresy odpowiedzi hello skonfigurowane dla aplikacji hello*</span><span class="sxs-lookup"><span data-stu-id="1a53c-126">*Error AADSTS50011: hello reply address ‘https://contoso.com’ does not match hello reply addresses configured for hello application*</span></span> 

<span data-ttu-id="1a53c-127">**Możliwa przyczyna**</span><span class="sxs-lookup"><span data-stu-id="1a53c-127">**Possible cause**</span></span> 

<span data-ttu-id="1a53c-128">wartość adresu URL odpowiedzi hello lub wzorca skonfigurowane w usłudze Azure AD Hello AssertionConsumerServiceURL wartość w żądaniu SAML hello nie jest zgodny.</span><span class="sxs-lookup"><span data-stu-id="1a53c-128">hello AssertionConsumerServiceURL value in hello SAML request doesn't match hello Reply URL value or pattern configured in Azure AD.</span></span> <span data-ttu-id="1a53c-129">Witaj AssertionConsumerServiceURL wartość w żądaniu SAML hello jest hello adresu URL, zobacz błąd hello.</span><span class="sxs-lookup"><span data-stu-id="1a53c-129">hello AssertionConsumerServiceURL value in hello SAML request is hello URL you see in hello error.</span></span> 

<span data-ttu-id="1a53c-130">**Rozdzielczość**</span><span class="sxs-lookup"><span data-stu-id="1a53c-130">**Resolution**</span></span> 

<span data-ttu-id="1a53c-131">Upewnij się, ta wartość AssertionConsumerServiceURL hello w żądaniu SAML hello jego pasującego hello wartość adresu URL odpowiedzi skonfigurowane w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="1a53c-131">Ensure that hello AssertionConsumerServiceURL value in hello SAML request it's matching hello Reply URL value configured in Azure AD.</span></span> 
 
1.  <span data-ttu-id="1a53c-132">Otwórz hello [ **Azure Portal** ](https://portal.azure.com/) i zaloguj się jako **administratora globalnego** lub **ko-administratora.**</span><span class="sxs-lookup"><span data-stu-id="1a53c-132">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span> 

2.  <span data-ttu-id="1a53c-133">Otwórz hello **rozszerzenia usług Azure Active Directory** klikając **więcej usług** u dołu menu nawigacji głównego po lewej stronie powitania hello.</span><span class="sxs-lookup"><span data-stu-id="1a53c-133">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span> 

3.  <span data-ttu-id="1a53c-134">Wpisz w **"Azure Active Directory**" w polu wyszukiwania filtr hello a wybierz hello **usługi Azure Active Directory** elementu.</span><span class="sxs-lookup"><span data-stu-id="1a53c-134">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span> 

4.  <span data-ttu-id="1a53c-135">Kliknij przycisk **aplikacje dla przedsiębiorstw** z menu nawigacji po lewej stronie powitania w usłudze Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="1a53c-135">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span> 

5.  <span data-ttu-id="1a53c-136">Kliknij przycisk **wszystkie aplikacje** tooview listę wszystkich aplikacji.</span><span class="sxs-lookup"><span data-stu-id="1a53c-136">click **All Applications** tooview a list of all your applications.</span></span> 

  * <span data-ttu-id="1a53c-137">Jeśli nie ma aplikacji hello mają być wyświetlane tutaj, użyj hello **filtru** kontroli u góry hello hello **listę wszystkich aplikacji** i zestaw hello **Pokaż** opcję zbyt **Wszystkie aplikacje.**</span><span class="sxs-lookup"><span data-stu-id="1a53c-137">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and       set hello **Show** option too**All Applications.**</span></span>
  
6.  <span data-ttu-id="1a53c-138">Wybierz hello aplikację tooconfigure rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="1a53c-138">Select hello application you want tooconfigure single sign-on</span></span>

7.  <span data-ttu-id="1a53c-139">Po załadowaniu aplikacji hello, kliknij przycisk hello **logowanie jednokrotne** z menu nawigacji po lewej stronie powitania aplikacji.</span><span class="sxs-lookup"><span data-stu-id="1a53c-139">Once hello application loads, click hello **Single sign-on** from hello application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="1a53c-140">Przejdź za**domeny i adres URL** sekcji.</span><span class="sxs-lookup"><span data-stu-id="1a53c-140">Go too**Domain and URLs** section.</span></span> <span data-ttu-id="1a53c-141">Sprawdź lub zaktualizować wartości hello hello adres URL odpowiedzi pole tekstowe toomatch hello AssertionConsumerServiceURL wartość w żądaniu SAML hello.</span><span class="sxs-lookup"><span data-stu-id="1a53c-141">Verify or update hello value in hello Reply URL textbox toomatch hello AssertionConsumerServiceURL value in hello SAML request.</span></span>

  * <span data-ttu-id="1a53c-142">Jeśli nie widzisz pole tekstowe adresu URL odpowiedzi hello wybierz hello **Pokaż zaawansowane ustawienia adresu URL** wyboru.</span><span class="sxs-lookup"><span data-stu-id="1a53c-142">If you don't see hello Reply URL textbox, select hello **Show advanced URL settings** checkbox.</span></span> 

<span data-ttu-id="1a53c-143">Po zaktualizowaniu wartość adresu URL odpowiedzi hello w usłudze Azure AD i ma dopasowania wartości hello wysyła aplikacja hello w hello żądanie SAML, powinno być możliwe toosign w toohello aplikacji.</span><span class="sxs-lookup"><span data-stu-id="1a53c-143">After you have updated hello Reply URL value in Azure AD and it’s matching hello value sends by hello application in hello SAML request, you should be able toosign in toohello application.</span></span>

## <a name="user-not-assigned-a-role"></a><span data-ttu-id="1a53c-144">Nie przypisaną rolę użytkownika</span><span class="sxs-lookup"><span data-stu-id="1a53c-144">User not assigned a role</span></span>

<span data-ttu-id="1a53c-145">*Błąd AADSTS50105: hello zalogowany użytkownik "brian@contoso.com" nie jest przypisana rola tooa dla aplikacji hello*</span><span class="sxs-lookup"><span data-stu-id="1a53c-145">*Error AADSTS50105: hello signed in user 'brian@contoso.com' is not assigned tooa role for hello application*</span></span>

<span data-ttu-id="1a53c-146">**Możliwa przyczyna**</span><span class="sxs-lookup"><span data-stu-id="1a53c-146">**Possible cause**</span></span>

<span data-ttu-id="1a53c-147">Hello użytkownikowi nie udzielono dostępu toohello aplikacji w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="1a53c-147">hello user has not been granted access toohello application in Azure AD.</span></span>

<span data-ttu-id="1a53c-148">**Rozdzielczość**</span><span class="sxs-lookup"><span data-stu-id="1a53c-148">**Resolution**</span></span>

<span data-ttu-id="1a53c-149">tooassign jednej lub kilku użytkowników aplikacji tooan bezpośrednio, wykonaj poniższe kroki hello:</span><span class="sxs-lookup"><span data-stu-id="1a53c-149">tooassign one or more users tooan application directly, follow hello steps below:</span></span>

1.  <span data-ttu-id="1a53c-150">Otwórz hello [ **Azure Portal** ](https://portal.azure.com/) i zaloguj się jako **administratora globalnego.**</span><span class="sxs-lookup"><span data-stu-id="1a53c-150">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="1a53c-151">Otwórz hello **rozszerzenia usług Azure Active Directory** klikając **więcej usług** u dołu menu nawigacji głównego po lewej stronie powitania hello.</span><span class="sxs-lookup"><span data-stu-id="1a53c-151">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="1a53c-152">Wpisz w **"Azure Active Directory**" w polu wyszukiwania filtr hello a wybierz hello **usługi Azure Active Directory** elementu.</span><span class="sxs-lookup"><span data-stu-id="1a53c-152">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="1a53c-153">Kliknij przycisk **aplikacje dla przedsiębiorstw** z menu nawigacji po lewej stronie powitania w usłudze Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="1a53c-153">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="1a53c-154">Kliknij przycisk **wszystkie aplikacje** tooview listę wszystkich aplikacji.</span><span class="sxs-lookup"><span data-stu-id="1a53c-154">click **All Applications** tooview a list of all your applications.</span></span>

  * <span data-ttu-id="1a53c-155">Jeśli nie ma aplikacji hello mają być wyświetlane tutaj, użyj hello **filtru** kontroli u góry hello hello **listę wszystkich aplikacji** i zestaw hello **Pokaż** opcję zbyt **Wszystkie aplikacje.**</span><span class="sxs-lookup"><span data-stu-id="1a53c-155">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="1a53c-156">Wybierz aplikację hello ma tooassign listy hello toofrom użytkownika.</span><span class="sxs-lookup"><span data-stu-id="1a53c-156">Select hello application you want tooassign a user toofrom hello list.</span></span>

7.  <span data-ttu-id="1a53c-157">Po załadowaniu aplikacji hello, kliknij przycisk **użytkowników i grup** z menu nawigacji po lewej stronie powitania aplikacji.</span><span class="sxs-lookup"><span data-stu-id="1a53c-157">Once hello application loads, click **Users and Groups** from hello application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="1a53c-158">Kliknij przycisk hello **Dodaj** przycisk na powitania **użytkowników i grup** hello tooopen listy **Dodaj przydziału** bloku.</span><span class="sxs-lookup"><span data-stu-id="1a53c-158">Click hello **Add** button on top of hello **Users and Groups** list tooopen hello **Add Assignment** blade.</span></span>

9.  <span data-ttu-id="1a53c-159">Kliknij przycisk hello **użytkowników i grup** selektora z hello **Dodaj przydziału** bloku.</span><span class="sxs-lookup"><span data-stu-id="1a53c-159">click hello **Users and groups** selector from hello **Add Assignment** blade.</span></span>

10. <span data-ttu-id="1a53c-160">Typ w hello **Pełna nazwa** lub **adres e-mail** użytkownika hello planuje się przypisanie do hello **wyszukiwanie według nazwy lub adresu e-mail** pola wyszukiwania.</span><span class="sxs-lookup"><span data-stu-id="1a53c-160">Type in hello **full name** or **email address** of hello user you are interested in assigning into hello **Search by name or email address** search box.</span></span>

11. <span data-ttu-id="1a53c-161">Umieść kursor nad hello **użytkownika** w tooreveal listy hello **wyboru**.</span><span class="sxs-lookup"><span data-stu-id="1a53c-161">Hover over hello **user** in hello list tooreveal a **checkbox**.</span></span> <span data-ttu-id="1a53c-162">Kliknij przycisk hello wyboru dalej toohello użytkownika profilu zdjęcie lub logo tooadd Twojego toohello użytkownika **wybrane** listy.</span><span class="sxs-lookup"><span data-stu-id="1a53c-162">Click hello checkbox next toohello user’s profile photo or logo tooadd your user toohello **Selected** list.</span></span>

12. <span data-ttu-id="1a53c-163">**Opcjonalnie:** Jeśli chcesz zbyt**dodać więcej niż jednego użytkownika**, typu w innym **Pełna nazwa** lub **adres e-mail** do hello **wyszukiwania według nazwy lub adresu e-mail** polu wyszukiwania, a następnie kliknij przycisk tooadd wyboru hello toohello tego użytkownika **wybrane** listy.</span><span class="sxs-lookup"><span data-stu-id="1a53c-163">**Optional:** If you would like too**add more than one user**, type in another **full name** or **email address** into hello **Search by name or email address** search box, and click hello checkbox tooadd this user toohello **Selected** list.</span></span>

13. <span data-ttu-id="1a53c-164">Po wybraniu użytkowników, kliknij przycisk hello **wybierz** tooadd przycisk ich toohello listę użytkowników i grup toobe przypisane toohello aplikacji.</span><span class="sxs-lookup"><span data-stu-id="1a53c-164">When you are finished selecting users, click hello **Select** button tooadd them toohello list of users and groups toobe assigned toohello application.</span></span>

14. <span data-ttu-id="1a53c-165">**Opcjonalnie:** kliknij hello **wybierz rolę** selektora w hello **Dodaj przydziału** tooselect bloku roli użytkowników toohello tooassign wybrano.</span><span class="sxs-lookup"><span data-stu-id="1a53c-165">**Optional:** click hello **Select Role** selector in hello **Add Assignment** blade tooselect a role tooassign toohello users you have selected.</span></span>

15. <span data-ttu-id="1a53c-166">Kliknij przycisk hello **przypisać** toohello aplikacji hello tooassign przycisk wybranych użytkowników.</span><span class="sxs-lookup"><span data-stu-id="1a53c-166">Click hello **Assign** button tooassign hello application toohello selected users.</span></span>

<span data-ttu-id="1a53c-167">Po krótkim czasie użytkownicy hello, wybranych będą mogli toolaunch te aplikacje przy użyciu hello metod opisanych w sekcji Opis rozwiązania hello.</span><span class="sxs-lookup"><span data-stu-id="1a53c-167">After a short period of time, hello users you have selected be able toolaunch these applications using hello methods described in hello solution description section.</span></span>

## <a name="not-a-valid-saml-request"></a><span data-ttu-id="1a53c-168">Nie prawidłowy SAML żądanie</span><span class="sxs-lookup"><span data-stu-id="1a53c-168">Not a valid SAML Request</span></span>

<span data-ttu-id="1a53c-169">*Błąd AADSTS75005: hello żądanie nie jest prawidłowy komunikat protokołu Saml2.*</span><span class="sxs-lookup"><span data-stu-id="1a53c-169">*Error AADSTS75005: hello request is not a valid Saml2 protocol message.*</span></span>

<span data-ttu-id="1a53c-170">**Możliwa przyczyna**</span><span class="sxs-lookup"><span data-stu-id="1a53c-170">**Possible cause**</span></span>

<span data-ttu-id="1a53c-171">Usługi Azure AD nie obsługuje hello SAML żądania wysyłane przez aplikację powitania dla logowania jednokrotnego.</span><span class="sxs-lookup"><span data-stu-id="1a53c-171">Azure AD doesn’t support hello SAML Request sent by hello application for Single Sign-on.</span></span> <span data-ttu-id="1a53c-172">Dostępne są następujące typowe problemy:</span><span class="sxs-lookup"><span data-stu-id="1a53c-172">Some common issues are:</span></span>

-   <span data-ttu-id="1a53c-173">Brak wymaganego pola w żądaniu SAML hello</span><span class="sxs-lookup"><span data-stu-id="1a53c-173">Missing required fields in hello SAML request</span></span>

-   <span data-ttu-id="1a53c-174">Metoda żądania zakodowane SAML</span><span class="sxs-lookup"><span data-stu-id="1a53c-174">SAML request encoded method</span></span>

<span data-ttu-id="1a53c-175">**Rozdzielczość**</span><span class="sxs-lookup"><span data-stu-id="1a53c-175">**Resolution**</span></span>

1.  <span data-ttu-id="1a53c-176">Przechwycenie żądania SAML.</span><span class="sxs-lookup"><span data-stu-id="1a53c-176">Capture SAML request.</span></span> <span data-ttu-id="1a53c-177">Postępuj zgodnie z samouczkiem hello [jak toodebug SAML na podstawie pojedynczego logowania jednokrotnego tooapplications w usłudze Azure AD](https://docs.microsoft.com/azure/active-directory/develop/active-directory-saml-debugging) toolearn jak toocapture hello SAML żądania.</span><span class="sxs-lookup"><span data-stu-id="1a53c-177">follow hello tutorial on [how toodebug SAML-based single sign-on tooapplications in Azure AD](https://docs.microsoft.com/azure/active-directory/develop/active-directory-saml-debugging) toolearn how toocapture hello SAML request.</span></span>

2.  <span data-ttu-id="1a53c-178">Skontaktuj się z dostawcą aplikacji hello i udziału:</span><span class="sxs-lookup"><span data-stu-id="1a53c-178">Contact hello application vendor and share:</span></span>

    -   <span data-ttu-id="1a53c-179">Żądanie SAML</span><span class="sxs-lookup"><span data-stu-id="1a53c-179">SAML request</span></span>

    -   [<span data-ttu-id="1a53c-180">Wymagania dotyczące protokołu usługi AD pojedynczego logowania jednokrotnego SAML Azure</span><span class="sxs-lookup"><span data-stu-id="1a53c-180">Azure AD Single Sign-on SAML protocol requirements</span></span>](https://docs.microsoft.com/azure/active-directory/develop/active-directory-single-sign-on-protocol-reference)

<span data-ttu-id="1a53c-181">Należy sprawdzić poprawność obsługują hello Azure AD SAML implementacji dla logowania jednokrotnego.</span><span class="sxs-lookup"><span data-stu-id="1a53c-181">They should validate they support hello Azure AD SAML implementation for Single Sign-on.</span></span>

## <a name="no-resource-in-requiredresourceaccess-list"></a><span data-ttu-id="1a53c-182">Żaden z zasobów na liście requiredResourceAccess</span><span class="sxs-lookup"><span data-stu-id="1a53c-182">No resource in requiredResourceAccess list</span></span>

<span data-ttu-id="1a53c-183">*Błąd AADSTS65005: aplikacja kliencka hello zażądał tooresource dostępu "00000002-0000-0000-c000-000000000000'. To żądanie nie powiodło się, ponieważ powitania klienta nie określono tego zasobu na swojej liście requiredResourceAccess*.</span><span class="sxs-lookup"><span data-stu-id="1a53c-183">*Error AADSTS65005: hello client application has requested access tooresource '00000002-0000-0000-c000-000000000000'. This request has failed because hello client has not specified this resource in its requiredResourceAccess list*.</span></span>

<span data-ttu-id="1a53c-184">**Możliwa przyczyna**</span><span class="sxs-lookup"><span data-stu-id="1a53c-184">**Possible cause**</span></span>

<span data-ttu-id="1a53c-185">obiekt aplikacji Hello jest uszkodzony.</span><span class="sxs-lookup"><span data-stu-id="1a53c-185">hello application object is corrupted.</span></span>

<span data-ttu-id="1a53c-186">**Rozdzielczość**</span><span class="sxs-lookup"><span data-stu-id="1a53c-186">**Resolution**</span></span>

<span data-ttu-id="1a53c-187">toosolve hello problem, Usuń hello aplikacji z katalogu hello.</span><span class="sxs-lookup"><span data-stu-id="1a53c-187">toosolve hello problem, remove hello application from hello directory.</span></span> <span data-ttu-id="1a53c-188">Następnie należy dodać i skonfigurować aplikacji hello, wykonaj poniższe kroki hello:</span><span class="sxs-lookup"><span data-stu-id="1a53c-188">Then, add and reconfigure hello application, follow hello steps below:</span></span>

1.  <span data-ttu-id="1a53c-189">Otwórz hello [ **Azure Portal** ](https://portal.azure.com/) i zaloguj się jako **administratora globalnego** lub **ko-administratora.**</span><span class="sxs-lookup"><span data-stu-id="1a53c-189">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="1a53c-190">Otwórz hello **rozszerzenia usług Azure Active Directory** klikając **więcej usług** u dołu menu nawigacji głównego po lewej stronie powitania hello.</span><span class="sxs-lookup"><span data-stu-id="1a53c-190">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="1a53c-191">Wpisz w **"Azure Active Directory**" w polu wyszukiwania filtr hello a wybierz hello **usługi Azure Active Directory** elementu.</span><span class="sxs-lookup"><span data-stu-id="1a53c-191">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="1a53c-192">Kliknij przycisk **aplikacje dla przedsiębiorstw** z menu nawigacji po lewej stronie powitania w usłudze Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="1a53c-192">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="1a53c-193">Kliknij przycisk **wszystkie aplikacje** tooview listę wszystkich aplikacji.</span><span class="sxs-lookup"><span data-stu-id="1a53c-193">click **All Applications** tooview a list of all your applications.</span></span>

  * <span data-ttu-id="1a53c-194">Jeśli nie ma aplikacji hello mają być wyświetlane tutaj, użyj hello **filtru** kontroli u góry hello hello **listę wszystkich aplikacji** i zestaw hello **Pokaż** opcję zbyt **Wszystkie aplikacje.**</span><span class="sxs-lookup"><span data-stu-id="1a53c-194">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="1a53c-195">Wybierz aplikację hello ma tooconfigure rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="1a53c-195">Select hello application you want tooconfigure single sign-on.</span></span>

7.  <span data-ttu-id="1a53c-196">Kliknij przycisk **usunąć** w lewym górnym hello aplikacji hello **omówienie** bloku.</span><span class="sxs-lookup"><span data-stu-id="1a53c-196">Click **Delete** at hello top-left of hello application **Overview** blade.</span></span>

8.  <span data-ttu-id="1a53c-197">Odśwież usługi Azure AD i dodawanie aplikacji hello z galerii Azure AD hello.</span><span class="sxs-lookup"><span data-stu-id="1a53c-197">Refresh Azure AD and Add hello application from hello Azure AD gallery.</span></span> <span data-ttu-id="1a53c-198">Skonfiguruj ponownie aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="1a53c-198">Then, Configure hello application again.</span></span>

<span data-ttu-id="1a53c-199">Po ponownej konfiguracji aplikacji hello, powinno być możliwe toosign w toohello aplikacji.</span><span class="sxs-lookup"><span data-stu-id="1a53c-199">After reconfiguring hello application, you should be able toosign in toohello application.</span></span>

## <a name="certificate-or-key-not-configured"></a><span data-ttu-id="1a53c-200">Certyfikat lub klucz nie jest skonfigurowany</span><span class="sxs-lookup"><span data-stu-id="1a53c-200">Certificate or key not configured</span></span>

<span data-ttu-id="1a53c-201">Błąd AADSTS50003: Nie klucza podpisywania skonfigurowane.</span><span class="sxs-lookup"><span data-stu-id="1a53c-201">Error AADSTS50003: No signing key configured.</span></span>

<span data-ttu-id="1a53c-202">**Możliwa przyczyna**</span><span class="sxs-lookup"><span data-stu-id="1a53c-202">**Possible cause**</span></span>

<span data-ttu-id="1a53c-203">obiekt aplikacji Hello jest uszkodzony i usługi Azure AD nie rozpoznaje certyfikatu hello skonfigurowanego dla aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="1a53c-203">hello application object is corrupted and Azure AD doesn’t recognize hello certificate configured for hello application.</span></span>

<span data-ttu-id="1a53c-204">**Rozdzielczość**</span><span class="sxs-lookup"><span data-stu-id="1a53c-204">**Resolution**</span></span>

<span data-ttu-id="1a53c-205">toodelete i utworzyć nowy certyfikat, wykonaj poniższe kroki hello:</span><span class="sxs-lookup"><span data-stu-id="1a53c-205">toodelete and create a new certificate, follow hello steps below:</span></span>

1.  <span data-ttu-id="1a53c-206">Otwórz hello [ **Azure Portal** ](https://portal.azure.com/) i zaloguj się jako **administratora globalnego** lub **ko-administratora.**</span><span class="sxs-lookup"><span data-stu-id="1a53c-206">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="1a53c-207">Otwórz hello **rozszerzenia usług Azure Active Directory** klikając **więcej usług** u dołu menu nawigacji głównego po lewej stronie powitania hello.</span><span class="sxs-lookup"><span data-stu-id="1a53c-207">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="1a53c-208">Wpisz w **"Azure Active Directory**" w polu wyszukiwania filtr hello a wybierz hello **usługi Azure Active Directory** elementu.</span><span class="sxs-lookup"><span data-stu-id="1a53c-208">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="1a53c-209">Kliknij przycisk **aplikacje dla przedsiębiorstw** z menu nawigacji po lewej stronie powitania w usłudze Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="1a53c-209">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="1a53c-210">Kliknij przycisk **wszystkie aplikacje** tooview listę wszystkich aplikacji.</span><span class="sxs-lookup"><span data-stu-id="1a53c-210">click **All Applications** tooview a list of all your applications.</span></span>

  * <span data-ttu-id="1a53c-211">Jeśli nie ma aplikacji hello mają być wyświetlane tutaj, użyj hello **filtru** kontroli u góry hello hello **listę wszystkich aplikacji** i zestaw hello **Pokaż** opcję zbyt **Wszystkie aplikacje.**</span><span class="sxs-lookup"><span data-stu-id="1a53c-211">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="1a53c-212">Wybierz aplikację hello ma tooconfigure rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="1a53c-212">Select hello application you want tooconfigure single sign-on.</span></span>

7.  <span data-ttu-id="1a53c-213">Po załadowaniu aplikacji hello, kliknij przycisk hello **logowanie jednokrotne** z menu nawigacji po lewej stronie powitania aplikacji.</span><span class="sxs-lookup"><span data-stu-id="1a53c-213">Once hello application loads, click hello **Single sign-on** from hello application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="1a53c-214">Kliknij przycisk **Utwórz nowy certyfikat** w obszarze hello **SAML certyfikatu podpisywania** sekcji.</span><span class="sxs-lookup"><span data-stu-id="1a53c-214">click **Create new certificate** under hello **SAML signing Certificate** section.</span></span>

9.  <span data-ttu-id="1a53c-215">Wybierz datę wygaśnięcia.</span><span class="sxs-lookup"><span data-stu-id="1a53c-215">Select Expiration date.</span></span> <span data-ttu-id="1a53c-216">Następnie kliknij przycisk **zapisać.**</span><span class="sxs-lookup"><span data-stu-id="1a53c-216">Then, click **Save.**</span></span>

10. <span data-ttu-id="1a53c-217">Sprawdź **uaktywnić nowego świadectwa** toooverride hello active certyfikatu.</span><span class="sxs-lookup"><span data-stu-id="1a53c-217">Check **Make new certificate active** toooverride hello active certificate.</span></span> <span data-ttu-id="1a53c-218">Następnie kliknij przycisk **zapisać** u góry bloku hello hello i zaakceptować certyfikat przerzucania hello tooactivate.</span><span class="sxs-lookup"><span data-stu-id="1a53c-218">Then, click **Save** at hello top of hello blade and accept tooactivate hello rollover certificate.</span></span>

11. <span data-ttu-id="1a53c-219">W obszarze hello **certyfikat podpisywania SAML** , kliknij przycisk **Usuń** tooremove hello **nieużywane** certyfikatu.</span><span class="sxs-lookup"><span data-stu-id="1a53c-219">Under hello **SAML Signing Certificate** section, click **remove** tooremove hello **Unused** certificate.</span></span>

## <a name="problem-when-customizing-hello-saml-claims-sent-tooan-application"></a><span data-ttu-id="1a53c-220">Problem w przypadku dostosowywania hello SAML oświadczenia wysyłane tooan aplikacji</span><span class="sxs-lookup"><span data-stu-id="1a53c-220">Problem when customizing hello SAML claims sent tooan application</span></span>

<span data-ttu-id="1a53c-221">toolearn toocustomize hello SAML atrybutu oświadczenia wysyłane tooyour aplikacji, zobacz [oświadczeń mapowanie w usłudze Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-claims-mapping) Aby uzyskać więcej informacji.</span><span class="sxs-lookup"><span data-stu-id="1a53c-221">toolearn how toocustomize hello SAML attribute claims sent tooyour application, see [Claims mapping in Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-claims-mapping) for more information.</span></span>

## <a name="next-steps"></a><span data-ttu-id="1a53c-222">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="1a53c-222">Next steps</span></span>
[<span data-ttu-id="1a53c-223">Wymagania dotyczące protokołu usługi AD pojedynczego logowania jednokrotnego SAML Azure</span><span class="sxs-lookup"><span data-stu-id="1a53c-223">Azure AD Single Sign-on SAML protocol requirements</span></span>](https://docs.microsoft.com/azure/active-directory/develop/active-directory-single-sign-on-protocol-reference)
