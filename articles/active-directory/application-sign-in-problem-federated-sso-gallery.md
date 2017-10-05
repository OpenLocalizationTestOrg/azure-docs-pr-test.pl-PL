---
title: Problemy przy logowaniu do galerii aplikacji skonfigurowana dla federacyjnych logowanie jednokrotne | Dokumentacja firmy Microsoft
description: "Wskazówki dotyczące określonych błędów podczas logowania do aplikacji, które zostały skonfigurowane na podstawie SAML federacyjne logowanie jednokrotne z usługą Azure AD"
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
ms.openlocfilehash: 0fc5a8eb3d033d60bf6082d61bf1698924ab91c6
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/03/2017
---
# <a name="problems-signing-in-to-a-gallery-application-configured-for-federated-single-sign-on"></a><span data-ttu-id="a4663-103">Problemy przy logowaniu do galerii aplikacji skonfigurowana dla federacyjnego logowania jednokrotnego</span><span class="sxs-lookup"><span data-stu-id="a4663-103">Problems signing in to a gallery application configured for federated single sign-on</span></span>

<span data-ttu-id="a4663-104">Aby rozwiązać problem, należy sprawdzić konfigurację aplikacji w usłudze Azure AD jako wykonaj:</span><span class="sxs-lookup"><span data-stu-id="a4663-104">To troubleshoot your problem, you need to verify the application configuration in Azure AD as follow:</span></span>

-   <span data-ttu-id="a4663-105">Zostały wykonane wszystkie kroki konfiguracji w galerii aplikacji usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a4663-105">You have followed all the configuration steps for the Azure AD gallery application.</span></span>

-   <span data-ttu-id="a4663-106">Identyfikator i adres URL odpowiedzi, skonfigurowane w usłudze AAD odpowiadać ich oczekiwanych wartości w aplikacji</span><span class="sxs-lookup"><span data-stu-id="a4663-106">The Identifier and Reply URL configured in AAD match they expected values in the application</span></span>

-   <span data-ttu-id="a4663-107">Przypisano użytkowników do aplikacji</span><span class="sxs-lookup"><span data-stu-id="a4663-107">You have assigned users to the application</span></span>

## <a name="application-not-found-in-directory"></a><span data-ttu-id="a4663-108">Nie można odnaleźć w katalogu aplikacji</span><span class="sxs-lookup"><span data-stu-id="a4663-108">Application not found in directory</span></span>

<span data-ttu-id="a4663-109">*Błąd AADSTS70001: Nie znaleziono aplikacji o identyfikatorze "https://contoso.com" w katalogu*.</span><span class="sxs-lookup"><span data-stu-id="a4663-109">*Error AADSTS70001: Application with Identifier ‘https://contoso.com’ was not found in the directory*.</span></span>

<span data-ttu-id="a4663-110">**Możliwa przyczyna**</span><span class="sxs-lookup"><span data-stu-id="a4663-110">**Possible cause**</span></span>

<span data-ttu-id="a4663-111">Wystawcę, którego atrybut wysyła z aplikacji do usługi Azure AD w żądaniu SAML jest niezgodne z wartością identyfikatora, skonfigurowane w aplikacji usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a4663-111">The Issuer attribute sends from the application to Azure AD in the SAML request doesn’t match the Identifier value configured in the application Azure AD.</span></span>

<span data-ttu-id="a4663-112">**Rozdzielczość**</span><span class="sxs-lookup"><span data-stu-id="a4663-112">**Resolution**</span></span>

<span data-ttu-id="a4663-113">Upewnij się, że atrybut wystawcy w żądaniu SAML jest zgodne identyfikator wartości ustawionej w usłudze Azure AD:</span><span class="sxs-lookup"><span data-stu-id="a4663-113">Ensure that the Issuer attribute in the SAML request it’s matching the Identifier value configured in Azure AD:</span></span>

1.  <span data-ttu-id="a4663-114">Otwórz [ **Azure Portal** ](https://portal.azure.com/) i zaloguj się jako **administratora globalnego** lub **ko-administratora.**</span><span class="sxs-lookup"><span data-stu-id="a4663-114">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="a4663-115">Otwórz **rozszerzenia usług Azure Active Directory** klikając **więcej usług** u dołu menu nawigacji głównego po lewej stronie.</span><span class="sxs-lookup"><span data-stu-id="a4663-115">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="a4663-116">Wpisz w **"Azure Active Directory**" w polu wyszukiwania filtr a wybierz **usługi Azure Active Directory** elementu.</span><span class="sxs-lookup"><span data-stu-id="a4663-116">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="a4663-117">Kliknij przycisk **aplikacje dla przedsiębiorstw** w menu nawigacji po lewej stronie usługi Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="a4663-117">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="a4663-118">Kliknij przycisk **wszystkie aplikacje** Aby wyświetlić listę wszystkich aplikacji.</span><span class="sxs-lookup"><span data-stu-id="a4663-118">click **All Applications** to view a list of all your applications.</span></span>

  * <span data-ttu-id="a4663-119">Jeśli nie ma aplikacji ma tutaj będą wyświetlane, użyj **filtru** kontroli nad **listę wszystkich aplikacji** i ustaw **Pokaż** opcji w celu **wszystkich aplikacji.**</span><span class="sxs-lookup"><span data-stu-id="a4663-119">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="a4663-120">Wybierz aplikację, aby skonfigurować logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="a4663-120">Select the application you want to configure single sign-on</span></span>

7.  <span data-ttu-id="a4663-121">Po załadowaniu aplikacji, kliknij przycisk **logowanie jednokrotne** z menu nawigacji po lewej stronie aplikacji.</span><span class="sxs-lookup"><span data-stu-id="a4663-121">Once the application loads, click the **Single sign-on** from the application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="a4663-122">Przejdź do **domeny i adres URL** sekcji.</span><span class="sxs-lookup"><span data-stu-id="a4663-122">Go to **Domain and URLs** section.</span></span> <span data-ttu-id="a4663-123">Upewnij się, że wartość w polu tekstowym identyfikatora jest zgodne z wartość identyfikatora wyświetlony w dzienniku błędów.</span><span class="sxs-lookup"><span data-stu-id="a4663-123">Verify that the value in the Identifier textbox is matching the value for the identifier value displayed in the error.</span></span>

<span data-ttu-id="a4663-124">Po jego jest dopasowanie wysyła wartości przez aplikację w żądaniu SAML i wartość identyfikatora zostały zaktualizowane w usłudze Azure AD, należy zalogować się do aplikacji.</span><span class="sxs-lookup"><span data-stu-id="a4663-124">After you have updated the Identifier value in Azure AD and it’s matching the value sends by the application in the SAML request, you should be able to sign in to the application.</span></span>

## <a name="the-reply-address-does-not-match-the-reply-addresses-configured-for-the-application"></a><span data-ttu-id="a4663-125">Adres, który jest niezgodny z adresów odpowiedzi skonfigurowanych dla aplikacji.</span><span class="sxs-lookup"><span data-stu-id="a4663-125">The reply address does not match the reply addresses configured for the application.</span></span>

<span data-ttu-id="a4663-126">*Błąd AADSTS50011: Adres zwrotny "https://contoso.com" pasują do adresów odpowiedzi, skonfigurowana dla aplikacji.*</span><span class="sxs-lookup"><span data-stu-id="a4663-126">*Error AADSTS50011: The reply address ‘https://contoso.com’ does not match the reply addresses configured for the application*</span></span>

<span data-ttu-id="a4663-127">**Możliwa przyczyna**</span><span class="sxs-lookup"><span data-stu-id="a4663-127">**Possible cause**</span></span>

<span data-ttu-id="a4663-128">Wartość AssertionConsumerServiceURL w żądaniu SAML nie jest zgodna wartość adresu URL odpowiedzi lub wzorca skonfigurowane w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a4663-128">The AssertionConsumerServiceURL value in the SAML request doesn't match the Reply URL value or pattern configured in Azure AD.</span></span> <span data-ttu-id="a4663-129">Wartość AssertionConsumerServiceURL w żądaniu SAML jest adres URL, zostanie wyświetlony w dzienniku błędów.</span><span class="sxs-lookup"><span data-stu-id="a4663-129">The AssertionConsumerServiceURL value in the SAML request is the URL you see in the error.</span></span>

<span data-ttu-id="a4663-130">**Rozdzielczość**</span><span class="sxs-lookup"><span data-stu-id="a4663-130">**Resolution**</span></span>

<span data-ttu-id="a4663-131">Upewnij się, że wartość AssertionConsumerServiceURL w żądaniu SAML jest dopasowywania adresu URL odpowiedzi wartości ustawionej w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a4663-131">Ensure that the AssertionConsumerServiceURL value in the SAML request it's matching the Reply URL value configured in Azure AD.</span></span>

1.  <span data-ttu-id="a4663-132">Otwórz [ **Azure Portal** ](https://portal.azure.com/) i zaloguj się jako **administratora globalnego** lub **ko-administratora.**</span><span class="sxs-lookup"><span data-stu-id="a4663-132">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="a4663-133">Otwórz **rozszerzenia usług Azure Active Directory** klikając **więcej usług** u dołu menu nawigacji głównego po lewej stronie.</span><span class="sxs-lookup"><span data-stu-id="a4663-133">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="a4663-134">Wpisz w **"Azure Active Directory**" w polu wyszukiwania filtr a wybierz **usługi Azure Active Directory** elementu.</span><span class="sxs-lookup"><span data-stu-id="a4663-134">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="a4663-135">Kliknij przycisk **aplikacje dla przedsiębiorstw** w menu nawigacji po lewej stronie usługi Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="a4663-135">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="a4663-136">Kliknij przycisk **wszystkie aplikacje** Aby wyświetlić listę wszystkich aplikacji.</span><span class="sxs-lookup"><span data-stu-id="a4663-136">click **All Applications** to view a list of all your applications.</span></span>

  * <span data-ttu-id="a4663-137">Jeśli nie ma aplikacji ma tutaj będą wyświetlane, użyj **filtru** kontroli nad **listę wszystkich aplikacji** i ustaw **Pokaż** opcji w celu **wszystkich aplikacji.**</span><span class="sxs-lookup"><span data-stu-id="a4663-137">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="a4663-138">Wybierz aplikację, aby skonfigurować logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="a4663-138">Select the application you want to configure single sign-on</span></span>

7.  <span data-ttu-id="a4663-139">Po załadowaniu aplikacji, kliknij przycisk **logowanie jednokrotne** z menu nawigacji po lewej stronie aplikacji.</span><span class="sxs-lookup"><span data-stu-id="a4663-139">Once the application loads, click the **Single sign-on** from the application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="a4663-140">Przejdź do **domeny i adres URL** sekcji.</span><span class="sxs-lookup"><span data-stu-id="a4663-140">Go to **Domain and URLs** section.</span></span> <span data-ttu-id="a4663-141">Sprawdź lub zaktualizuj tę wartość w polu tekstowym adres URL odpowiedzi służący do dopasowania wartości AssertionConsumerServiceURL w żądaniu SAML.</span><span class="sxs-lookup"><span data-stu-id="a4663-141">Verify or update the value in the Reply URL textbox to match the AssertionConsumerServiceURL value in the SAML request.</span></span>  
    * <span data-ttu-id="a4663-142">Jeśli nie widzisz pole tekstowe adresu URL odpowiedzi, wybierz **Pokaż zaawansowane ustawienia adresu URL** wyboru.</span><span class="sxs-lookup"><span data-stu-id="a4663-142">If you don't see the Reply URL textbox, select the **Show advanced URL settings** checkbox.</span></span>

<span data-ttu-id="a4663-143">Po jego jest dopasowanie wysyła wartości przez aplikację w żądaniu SAML i wartość adresu URL odpowiedzi zostały zaktualizowane w usłudze Azure AD, należy zalogować się do aplikacji.</span><span class="sxs-lookup"><span data-stu-id="a4663-143">After you have updated the Reply URL value in Azure AD and it’s matching the value sends by the application in the SAML request, you should be able to sign in to the application.</span></span>

## <a name="user-not-assigned-a-role"></a><span data-ttu-id="a4663-144">Nie przypisaną rolę użytkownika</span><span class="sxs-lookup"><span data-stu-id="a4663-144">User not assigned a role</span></span>

<span data-ttu-id="a4663-145">*Błąd AADSTS50105: Zalogowanemu użytkownikowi "brian@contoso.com" nie jest przypisany do roli aplikacji*.</span><span class="sxs-lookup"><span data-stu-id="a4663-145">*Error AADSTS50105: The signed in user 'brian@contoso.com' is not assigned to a role for the application*.</span></span>

<span data-ttu-id="a4663-146">**Możliwa przyczyna**</span><span class="sxs-lookup"><span data-stu-id="a4663-146">**Possible cause**</span></span>

<span data-ttu-id="a4663-147">Użytkownikowi nie udzielono dostępu do aplikacji w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a4663-147">The user has not been granted access to the application in Azure AD.</span></span>

<span data-ttu-id="a4663-148">**Rozdzielczość**</span><span class="sxs-lookup"><span data-stu-id="a4663-148">**Resolution**</span></span>

<span data-ttu-id="a4663-149">Aby przypisać bezpośrednio co najmniej jednego użytkownika do aplikacji, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="a4663-149">To assign one or more users to an application directly, follow the steps below:</span></span>

1.  <span data-ttu-id="a4663-150">Otwórz [ **Azure Portal** ](https://portal.azure.com/) i zaloguj się jako **administratora globalnego.**</span><span class="sxs-lookup"><span data-stu-id="a4663-150">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="a4663-151">Otwórz **rozszerzenia usług Azure Active Directory** klikając **więcej usług** u dołu menu nawigacji głównego po lewej stronie.</span><span class="sxs-lookup"><span data-stu-id="a4663-151">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="a4663-152">Wpisz w **"Azure Active Directory**" w polu wyszukiwania filtr a wybierz **usługi Azure Active Directory** elementu.</span><span class="sxs-lookup"><span data-stu-id="a4663-152">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="a4663-153">Kliknij przycisk **aplikacje dla przedsiębiorstw** w menu nawigacji po lewej stronie usługi Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="a4663-153">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="a4663-154">Kliknij przycisk **wszystkie aplikacje** Aby wyświetlić listę wszystkich aplikacji.</span><span class="sxs-lookup"><span data-stu-id="a4663-154">click **All Applications** to view a list of all your applications.</span></span>

  * <span data-ttu-id="a4663-155">Jeśli nie ma aplikacji ma tutaj będą wyświetlane, użyj **filtru** kontroli nad **listę wszystkich aplikacji** i ustaw **Pokaż** opcji w celu **wszystkich aplikacji.**</span><span class="sxs-lookup"><span data-stu-id="a4663-155">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="a4663-156">Wybierz aplikacji, którą chcesz przypisać do użytkownika z listy.</span><span class="sxs-lookup"><span data-stu-id="a4663-156">Select the application you want to assign a user to from the list.</span></span>

7.  <span data-ttu-id="a4663-157">Po załadowaniu aplikacji, kliknij przycisk **użytkowników i grup** z menu nawigacji po lewej stronie aplikacji.</span><span class="sxs-lookup"><span data-stu-id="a4663-157">Once the application loads, click **Users and Groups** from the application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="a4663-158">Kliknij przycisk **Dodaj** przycisk nad **użytkowników i grup** listy, aby otworzyć **Dodaj przydziału** bloku.</span><span class="sxs-lookup"><span data-stu-id="a4663-158">Click the **Add** button on top of the **Users and Groups** list to open the **Add Assignment** blade.</span></span>

9.  <span data-ttu-id="a4663-159">Kliknij przycisk **użytkowników i grup** selektora z **Dodaj przydziału** bloku.</span><span class="sxs-lookup"><span data-stu-id="a4663-159">click the **Users and groups** selector from the **Add Assignment** blade.</span></span>

10. <span data-ttu-id="a4663-160">Wpisz w **Pełna nazwa** lub **adres e-mail** użytkownika planuje się przypisanie do **wyszukiwanie według nazwy lub adresu e-mail** pola wyszukiwania.</span><span class="sxs-lookup"><span data-stu-id="a4663-160">Type in the **full name** or **email address** of the user you are interested in assigning into the **Search by name or email address** search box.</span></span>

11. <span data-ttu-id="a4663-161">Umieść kursor nad **użytkownika** na liście, aby wyświetlić **wyboru**.</span><span class="sxs-lookup"><span data-stu-id="a4663-161">Hover over the **user** in the list to reveal a **checkbox**.</span></span> <span data-ttu-id="a4663-162">Zaznacz pole wyboru obok zdjęcia profilu użytkownika lub logo, aby dodać użytkownika do **wybrane** listy.</span><span class="sxs-lookup"><span data-stu-id="a4663-162">Click the checkbox next to the user’s profile photo or logo to add your user to the **Selected** list.</span></span>

12. <span data-ttu-id="a4663-163">**Opcjonalnie:** Jeśli chcesz **dodać więcej niż jednego użytkownika**, typu w innym **Pełna nazwa** lub **adres e-mail** do **wyszukiwanie według nazwy lub adresu e-mail** polu wyszukiwania, a następnie kliknij przycisk wyboru, aby dodać użytkownika do **wybrane** listy.</span><span class="sxs-lookup"><span data-stu-id="a4663-163">**Optional:** If you would like to **add more than one user**, type in another **full name** or **email address** into the **Search by name or email address** search box, and click the checkbox to add this user to the **Selected** list.</span></span>

13. <span data-ttu-id="a4663-164">Po zakończeniu wybierania użytkowników, kliknij przycisk **wybierz** przycisk, aby dodać je do listy użytkowników i grup, które ma być przypisany do aplikacji.</span><span class="sxs-lookup"><span data-stu-id="a4663-164">When you are finished selecting users, click the **Select** button to add them to the list of users and groups to be assigned to the application.</span></span>

14. <span data-ttu-id="a4663-165">**Opcjonalnie:** kliknij **wybierz rolę** selektora w **Dodaj przydziału** bloku, aby wybrać rolę można przypisać do użytkowników po wybraniu.</span><span class="sxs-lookup"><span data-stu-id="a4663-165">**Optional:** click the **Select Role** selector in the **Add Assignment** blade to select a role to assign to the users you have selected.</span></span>

15. <span data-ttu-id="a4663-166">Kliknij przycisk **przypisać** przycisk, aby przypisać aplikację do wybranych użytkowników.</span><span class="sxs-lookup"><span data-stu-id="a4663-166">Click the **Assign** button to assign the application to the selected users.</span></span>

<span data-ttu-id="a4663-167">Po krótkim czasie użytkowników, dla których wybrano mieć możliwość uruchamiania tych aplikacji za pomocą metod opisanych w sekcji Opis rozwiązania.</span><span class="sxs-lookup"><span data-stu-id="a4663-167">After a short period of time, the users you have selected be able to launch these applications using the methods described in the solution description section.</span></span>

## <a name="not-a-valid-saml-request"></a><span data-ttu-id="a4663-168">Nie prawidłowy SAML żądanie</span><span class="sxs-lookup"><span data-stu-id="a4663-168">Not a valid SAML Request</span></span>

<span data-ttu-id="a4663-169">*Błąd AADSTS75005: Żądanie nie jest prawidłowy komunikat protokołu Saml2.*</span><span class="sxs-lookup"><span data-stu-id="a4663-169">*Error AADSTS75005: The request is not a valid Saml2 protocol message.*</span></span>

<span data-ttu-id="a4663-170">**Możliwa przyczyna**</span><span class="sxs-lookup"><span data-stu-id="a4663-170">**Possible cause**</span></span>

<span data-ttu-id="a4663-171">Usługi Azure AD nie obsługuje SAML żądania wysyłane przez aplikację do logowania jednokrotnego.</span><span class="sxs-lookup"><span data-stu-id="a4663-171">Azure AD doesn’t support the SAML Request sent by the application for Single Sign-on.</span></span> <span data-ttu-id="a4663-172">Dostępne są następujące typowe problemy:</span><span class="sxs-lookup"><span data-stu-id="a4663-172">Some common issues are:</span></span>

-   <span data-ttu-id="a4663-173">Brak wymaganego pola w żądaniu SAML</span><span class="sxs-lookup"><span data-stu-id="a4663-173">Missing required fields in the SAML request</span></span>

-   <span data-ttu-id="a4663-174">Metoda żądania zakodowane SAML</span><span class="sxs-lookup"><span data-stu-id="a4663-174">SAML request encoded method</span></span>

<span data-ttu-id="a4663-175">**Rozdzielczość**</span><span class="sxs-lookup"><span data-stu-id="a4663-175">**Resolution**</span></span>

1.  <span data-ttu-id="a4663-176">Przechwycenie żądania SAML.</span><span class="sxs-lookup"><span data-stu-id="a4663-176">Capture SAML request.</span></span> <span data-ttu-id="a4663-177">czynności opisane w samouczku [debugowanie na języku SAML logowanie jednokrotne do aplikacji w usłudze Azure AD](https://docs.microsoft.com/azure/active-directory/develop/active-directory-saml-debugging) informacje na temat przechwytywania żądania SAML.</span><span class="sxs-lookup"><span data-stu-id="a4663-177">follow the tutorial [How to debug SAML-based single sign-on to applications in Azure AD](https://docs.microsoft.com/azure/active-directory/develop/active-directory-saml-debugging) to learn how to capture the SAML request.</span></span>

2.  <span data-ttu-id="a4663-178">Skontaktuj się z dostawcą aplikacji i udziału:</span><span class="sxs-lookup"><span data-stu-id="a4663-178">Contact the application vendor and share:</span></span>

   -   <span data-ttu-id="a4663-179">Żądanie SAML</span><span class="sxs-lookup"><span data-stu-id="a4663-179">SAML request</span></span>

   -   [<span data-ttu-id="a4663-180">Wymagania dotyczące protokołu usługi AD pojedynczego logowania jednokrotnego SAML Azure</span><span class="sxs-lookup"><span data-stu-id="a4663-180">Azure AD Single Sign-on SAML protocol requirements</span></span>](https://docs.microsoft.com/azure/active-directory/develop/active-directory-single-sign-on-protocol-reference)

<span data-ttu-id="a4663-181">Należy sprawdzić poprawność ich obsługę wdrożenia usługi Azure AD SAML logowania jednokrotnego.</span><span class="sxs-lookup"><span data-stu-id="a4663-181">They should validate they support the Azure AD SAML implementation for Single Sign-on.</span></span>

## <a name="no-resource-in-requiredresourceaccess-list"></a><span data-ttu-id="a4663-182">Żaden z zasobów na liście requiredResourceAccess</span><span class="sxs-lookup"><span data-stu-id="a4663-182">No resource in requiredResourceAccess list</span></span>

<span data-ttu-id="a4663-183">*Błąd AADSTS65005: aplikacja kliencka żąda dostępu do zasobu "00000002-0000-0000-c000-000000000000'. To żądanie nie powiodło się, ponieważ klient nie określił tego zasobu na swojej liście requiredResourceAccess*.</span><span class="sxs-lookup"><span data-stu-id="a4663-183">*Error AADSTS65005:The client application has requested access to resource '00000002-0000-0000-c000-000000000000'. This request has failed because the client has not specified this resource in its requiredResourceAccess list*.</span></span>

<span data-ttu-id="a4663-184">**Możliwa przyczyna**</span><span class="sxs-lookup"><span data-stu-id="a4663-184">**Possible cause**</span></span>

<span data-ttu-id="a4663-185">Obiekt application jest uszkodzony.</span><span class="sxs-lookup"><span data-stu-id="a4663-185">The application object is corrupted.</span></span>

<span data-ttu-id="a4663-186">**Rozwiązanie: opcja 1**</span><span class="sxs-lookup"><span data-stu-id="a4663-186">**Resolution: option 1**</span></span>

<span data-ttu-id="a4663-187">Aby rozwiązać ten problem, należy dodać wartość Unikatowy identyfikator w konfiguracji usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a4663-187">To solve the problem, add the unique Identifier value in the Azure AD configuration.</span></span> <span data-ttu-id="a4663-188">Aby dodać wartości identyfikatora, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="a4663-188">To add a Identifier value, follow the steps below:</span></span>

1.  <span data-ttu-id="a4663-189">Otwórz [ **Azure Portal** ](https://portal.azure.com/) i zaloguj się jako **administratora globalnego** lub **ko-administratora.**</span><span class="sxs-lookup"><span data-stu-id="a4663-189">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="a4663-190">Otwórz **rozszerzenia usług Azure Active Directory** klikając **więcej usług** u dołu menu nawigacji głównego po lewej stronie.</span><span class="sxs-lookup"><span data-stu-id="a4663-190">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="a4663-191">Wpisz w **"Azure Active Directory**" w polu wyszukiwania filtr a wybierz **usługi Azure Active Directory** elementu.</span><span class="sxs-lookup"><span data-stu-id="a4663-191">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="a4663-192">Kliknij przycisk **aplikacje dla przedsiębiorstw** w menu nawigacji po lewej stronie usługi Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="a4663-192">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="a4663-193">Kliknij przycisk **wszystkie aplikacje** Aby wyświetlić listę wszystkich aplikacji.</span><span class="sxs-lookup"><span data-stu-id="a4663-193">click **All Applications** to view a list of all your applications.</span></span>

  * <span data-ttu-id="a4663-194">Jeśli nie ma aplikacji ma tutaj będą wyświetlane, użyj **filtru** kontroli nad **listę wszystkich aplikacji** i ustaw **Pokaż** opcji w celu **wszystkich aplikacji.**</span><span class="sxs-lookup"><span data-stu-id="a4663-194">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="a4663-195">Wybierz aplikację, skonfigurowaniu logowania jednokrotnego.</span><span class="sxs-lookup"><span data-stu-id="a4663-195">Select the application you have configured single sign-on.</span></span>

7.  <span data-ttu-id="a4663-196">Po załadowaniu aplikacji, kliknij **logowanie jednokrotne** z menu nawigacji po lewej stronie aplikacji</span><span class="sxs-lookup"><span data-stu-id="a4663-196">Once the application loads, click on the **Single sign-on** from the application’s left hand navigation menu</span></span>

8.  <span data-ttu-id="a4663-197">W obszarze **domeny i adres URL** sekcji, sprawdź na **Pokaż zaawansowane ustawienia adresu URL**.</span><span class="sxs-lookup"><span data-stu-id="a4663-197">Under the **Domain and URL** section, check on the **Show advanced URL settings**.</span></span>

9.  <span data-ttu-id="a4663-198">w **identyfikator** pole tekstowe wpisz unikatowy identyfikator dla aplikacji.</span><span class="sxs-lookup"><span data-stu-id="a4663-198">in the **Identifier** textbox type a unique identifier for the application.</span></span>

10. <span data-ttu-id="a4663-199">**Zapisz** konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="a4663-199">**Save** the configuration.</span></span>


<span data-ttu-id="a4663-200">**Opcja rozpoznawania 2**</span><span class="sxs-lookup"><span data-stu-id="a4663-200">**Resolution option 2**</span></span>

<span data-ttu-id="a4663-201">Jeśli opcja 1 powyżej zakończyło się niepowodzeniem dla Ciebie, spróbuj, usunięcie aplikacji z katalogu.</span><span class="sxs-lookup"><span data-stu-id="a4663-201">If option 1 above did not work for you, try removing the application from the directory.</span></span> <span data-ttu-id="a4663-202">Następnie należy dodać i zmiany konfiguracji aplikacji, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="a4663-202">Then, add and reconfigure the application, follow the steps below:</span></span>

1.  <span data-ttu-id="a4663-203">Otwórz [ **Azure Portal** ](https://portal.azure.com/) i zaloguj się jako **administratora globalnego** lub **ko-administratora.**</span><span class="sxs-lookup"><span data-stu-id="a4663-203">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="a4663-204">Otwórz **rozszerzenia usług Azure Active Directory** klikając **więcej usług** u dołu menu nawigacji głównego po lewej stronie.</span><span class="sxs-lookup"><span data-stu-id="a4663-204">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="a4663-205">Wpisz w **"Azure Active Directory**" w polu wyszukiwania filtr a wybierz **usługi Azure Active Directory** elementu.</span><span class="sxs-lookup"><span data-stu-id="a4663-205">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="a4663-206">Kliknij przycisk **aplikacje dla przedsiębiorstw** w menu nawigacji po lewej stronie usługi Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="a4663-206">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="a4663-207">Kliknij przycisk **wszystkie aplikacje** Aby wyświetlić listę wszystkich aplikacji.</span><span class="sxs-lookup"><span data-stu-id="a4663-207">click **All Applications** to view a list of all your applications.</span></span>

  * <span data-ttu-id="a4663-208">Jeśli nie ma aplikacji ma tutaj będą wyświetlane, użyj **filtru** kontroli nad **listę wszystkich aplikacji** i ustaw **Pokaż** opcji w celu **wszystkich aplikacji.**</span><span class="sxs-lookup"><span data-stu-id="a4663-208">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="a4663-209">Wybierz aplikację, aby skonfigurować logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="a4663-209">Select the application you want to configure single sign-on</span></span>

7.  <span data-ttu-id="a4663-210">Kliknij przycisk **usunąć** w lewym górnym aplikacji **omówienie** bloku.</span><span class="sxs-lookup"><span data-stu-id="a4663-210">Click **Delete** at the top-left of the application **Overview** blade.</span></span>

8.  <span data-ttu-id="a4663-211">Odśwież usługi Azure AD i dodaj aplikację z galerii Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a4663-211">Refresh Azure AD and Add the application from the Azure AD gallery.</span></span> <span data-ttu-id="a4663-212">Następnie należy skonfigurować aplikację</span><span class="sxs-lookup"><span data-stu-id="a4663-212">Then, Configure the application</span></span>

<span data-ttu-id="a4663-213"><span id="_Hlk477190176" class="anchor"></span>Po ponownej konfiguracji aplikacji, można logować się do aplikacji.</span><span class="sxs-lookup"><span data-stu-id="a4663-213"><span id="_Hlk477190176" class="anchor"></span>After reconfiguring the application, you should be able to sign in to the application.</span></span>

## <a name="certificate-or-key-not-configured"></a><span data-ttu-id="a4663-214">Certyfikat lub klucz nie jest skonfigurowany</span><span class="sxs-lookup"><span data-stu-id="a4663-214">Certificate or key not configured</span></span>

<span data-ttu-id="a4663-215">*Błąd AADSTS50003: Nie klucza podpisywania skonfigurowane.*</span><span class="sxs-lookup"><span data-stu-id="a4663-215">*Error AADSTS50003: No signing key configured.*</span></span>

<span data-ttu-id="a4663-216">**Możliwa przyczyna**</span><span class="sxs-lookup"><span data-stu-id="a4663-216">**Possible cause**</span></span>

<span data-ttu-id="a4663-217">Obiekt application jest uszkodzony i usługi Azure AD nie rozpoznaje certyfikatu skonfigurowane dla aplikacji.</span><span class="sxs-lookup"><span data-stu-id="a4663-217">The application object is corrupted and Azure AD doesn’t recognize the certificate configured for the application.</span></span>

<span data-ttu-id="a4663-218">**Rozdzielczość**</span><span class="sxs-lookup"><span data-stu-id="a4663-218">**Resolution**</span></span>

<span data-ttu-id="a4663-219">Aby usunąć i utworzyć nowy certyfikat, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="a4663-219">To delete and create a new certificate, follow the steps below:</span></span>

1.  <span data-ttu-id="a4663-220">Otwórz [ **Azure Portal** ](https://portal.azure.com/) i zaloguj się jako **administratora globalnego** lub **ko-administratora.**</span><span class="sxs-lookup"><span data-stu-id="a4663-220">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="a4663-221">Otwórz **rozszerzenia usług Azure Active Directory** klikając **więcej usług** u dołu menu nawigacji głównego po lewej stronie.</span><span class="sxs-lookup"><span data-stu-id="a4663-221">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="a4663-222">Wpisz w **"Azure Active Directory**" w polu wyszukiwania filtr a wybierz **usługi Azure Active Directory** elementu.</span><span class="sxs-lookup"><span data-stu-id="a4663-222">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="a4663-223">Kliknij przycisk **aplikacje dla przedsiębiorstw** w menu nawigacji po lewej stronie usługi Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="a4663-223">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="a4663-224">Kliknij przycisk **wszystkie aplikacje** Aby wyświetlić listę wszystkich aplikacji.</span><span class="sxs-lookup"><span data-stu-id="a4663-224">click **All Applications** to view a list of all your applications.</span></span>

 * <span data-ttu-id="a4663-225">Jeśli nie ma aplikacji ma tutaj będą wyświetlane, użyj **filtru** kontroli nad **listę wszystkich aplikacji** i ustaw **Pokaż** opcji w celu **wszystkich aplikacji.**</span><span class="sxs-lookup"><span data-stu-id="a4663-225">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="a4663-226">Wybierz aplikację, aby skonfigurować logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="a4663-226">Select the application you want to configure single sign-on</span></span>

7.  <span data-ttu-id="a4663-227">Po załadowaniu aplikacji, kliknij przycisk **logowanie jednokrotne** z menu nawigacji po lewej stronie aplikacji.</span><span class="sxs-lookup"><span data-stu-id="a4663-227">Once the application loads, click the **Single sign-on** from the application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="a4663-228">Kliknij przycisk **Utwórz nowy certyfikat** w obszarze **SAML certyfikatu podpisywania** sekcji.</span><span class="sxs-lookup"><span data-stu-id="a4663-228">click **Create new certificate** under the **SAML signing Certificate** section.</span></span>

9.  <span data-ttu-id="a4663-229">Wybierz datę wygaśnięcia.</span><span class="sxs-lookup"><span data-stu-id="a4663-229">Select Expiration date.</span></span> <span data-ttu-id="a4663-230">Następnie kliknij przycisk **zapisać.**</span><span class="sxs-lookup"><span data-stu-id="a4663-230">Then, click **Save.**</span></span>

10. <span data-ttu-id="a4663-231">Sprawdź **uaktywnić nowego świadectwa** do przesłonięcia aktywnego certyfikatu.</span><span class="sxs-lookup"><span data-stu-id="a4663-231">Check **Make new certificate active** to override the active certificate.</span></span> <span data-ttu-id="a4663-232">Następnie kliknij przycisk **zapisać** w górnej części bloku i zaakceptować certyfikat przerzucania aktywować.</span><span class="sxs-lookup"><span data-stu-id="a4663-232">Then, click **Save** at the top of the blade and accept to activate the rollover certificate.</span></span>

11. <span data-ttu-id="a4663-233">W obszarze **certyfikat podpisywania SAML** kliknij **Usuń** do usunięcia **nieużywane** certyfikatu.</span><span class="sxs-lookup"><span data-stu-id="a4663-233">Under the **SAML Signing Certificate** section, click **remove** to remove the **Unused** certificate.</span></span>

## <a name="problem-when-customizing-the-saml-claims-sent-to-an-application"></a><span data-ttu-id="a4663-234">Problem w przypadku dostosowywania SAML oświadczenia wysyłane do aplikacji</span><span class="sxs-lookup"><span data-stu-id="a4663-234">Problem when customizing the SAML claims sent to an application</span></span>

<span data-ttu-id="a4663-235">Aby dowiedzieć się, jak dostosować oświadczeń atrybutów SAML wysyłanych do aplikacji, zobacz [oświadczeń mapowanie w usłudze Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-claims-mapping) Aby uzyskać więcej informacji.</span><span class="sxs-lookup"><span data-stu-id="a4663-235">To learn how to customize the SAML attribute claims sent to your application, see [Claims mapping in Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-claims-mapping) for more information.</span></span>

## <a name="next-steps"></a><span data-ttu-id="a4663-236">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="a4663-236">Next steps</span></span>
[<span data-ttu-id="a4663-237">Debugowanie na języku SAML logowanie jednokrotne do aplikacji w usłudze Azure AD</span><span class="sxs-lookup"><span data-stu-id="a4663-237">How to debug SAML-based single sign-on to applications in Azure AD</span></span>](https://docs.microsoft.com/azure/active-directory/develop/active-directory-saml-debugging)
