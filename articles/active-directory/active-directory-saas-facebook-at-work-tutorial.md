---
title: 'Samouczek: Integracji Azure Active Directory z miejsca pracy przez Facebook | Dokumentacja firmy Microsoft'
description: "Informacje o sposobie konfigurowania rejestracji jednokrotnej między usługą Azure Active Directory i miejsca pracy przez usługi Facebook."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 30f2ee64-95d3-44ef-b832-8a0a27e2967c
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/18/2017
ms.author: jeedes
ms.openlocfilehash: 27e62a00832484667117d8718db9f2fc05e2f4e2
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/29/2017
---
# <a name="tutorial-azure-active-directory-integration-with-workplace-by-facebook"></a><span data-ttu-id="8c1ac-103">Samouczek: Integracji Azure Active Directory z miejsca pracy przez usługi Facebook</span><span class="sxs-lookup"><span data-stu-id="8c1ac-103">Tutorial: Azure Active Directory integration with Workplace by Facebook</span></span>

<span data-ttu-id="8c1ac-104">Z tego samouczka dowiesz się sposobu integracji z usługą Azure Active Directory (Azure AD) miejsca pracy przez usługi Facebook.</span><span class="sxs-lookup"><span data-stu-id="8c1ac-104">In this tutorial, you learn how to integrate Workplace by Facebook with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="8c1ac-105">Integrowanie miejsca pracy przez Facebook z usługą Azure AD zapewnia następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="8c1ac-105">Integrating Workplace by Facebook with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="8c1ac-106">Można kontrolować w usłudze Azure AD, który ma dostęp do miejsca pracy przez usługi Facebook.</span><span class="sxs-lookup"><span data-stu-id="8c1ac-106">You can control in Azure AD who has access to Workplace by Facebook.</span></span>
- <span data-ttu-id="8c1ac-107">Można umożliwić użytkownikom automatycznie pobrać zalogowanego do miejsca pracy przez Facebook (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="8c1ac-107">You can enable your users to automatically get signed on to Workplace by Facebook (single sign-on) with their Azure AD accounts.</span></span>
- <span data-ttu-id="8c1ac-108">Możesz zarządzać kont w jednej centralnej lokalizacji: portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="8c1ac-108">You can manage your accounts in one central location: the Azure portal.</span></span>

<span data-ttu-id="8c1ac-109">Aby uzyskać więcej informacji na temat oprogramowania jako usługa (SaaS) integracji aplikacji z usługą Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="8c1ac-109">For more details about software as a service (SaaS) app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory?](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="8c1ac-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="8c1ac-110">Prerequisites</span></span>

<span data-ttu-id="8c1ac-111">Aby skonfigurować integrację usługi Azure AD z miejsca pracy przez usługi Facebook, potrzebne są następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="8c1ac-111">To configure Azure AD integration with Workplace by Facebook, you need the following items:</span></span>

- <span data-ttu-id="8c1ac-112">Subskrypcję usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="8c1ac-112">An Azure AD subscription</span></span>
- <span data-ttu-id="8c1ac-113">Dołączanie w serwisie Facebook rejestracji jednokrotnej (SSO) włączone subskrypcji</span><span class="sxs-lookup"><span data-stu-id="8c1ac-113">A Workplace by Facebook single sign-on (SSO) enabled subscription</span></span>

<span data-ttu-id="8c1ac-114">Aby przetestować kroki opisane w tym samouczku, wykonaj te zalecenia:</span><span class="sxs-lookup"><span data-stu-id="8c1ac-114">To test the steps in this tutorial, follow these recommendations:</span></span>

- <span data-ttu-id="8c1ac-115">Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="8c1ac-115">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="8c1ac-116">Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz [uzyskać miesięczna wersja próbna](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="8c1ac-116">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="8c1ac-117">Opis scenariusza</span><span class="sxs-lookup"><span data-stu-id="8c1ac-117">Scenario description</span></span>
<span data-ttu-id="8c1ac-118">W tym samouczku można przetestować logowania jednokrotnego programu Azure AD w środowisku testowym.</span><span class="sxs-lookup"><span data-stu-id="8c1ac-118">In this tutorial, you test Azure AD SSO in a test environment.</span></span> <span data-ttu-id="8c1ac-119">Scenariusz opisany w tym samouczku składa się z dwóch głównych elementów:</span><span class="sxs-lookup"><span data-stu-id="8c1ac-119">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="8c1ac-120">Dodaj obszar roboczy w serwisie Facebook w galerii.</span><span class="sxs-lookup"><span data-stu-id="8c1ac-120">Add Workplace by Facebook from the gallery.</span></span>
2. <span data-ttu-id="8c1ac-121">Konfiguracja i testowanie usługi Azure AD rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="8c1ac-121">Configure and test Azure AD single sign-on.</span></span>

## <a name="add-workplace-by-facebook-from-the-gallery"></a><span data-ttu-id="8c1ac-122">Dodawanie miejsca pracy przez Facebook z galerii</span><span class="sxs-lookup"><span data-stu-id="8c1ac-122">Add Workplace by Facebook from the gallery</span></span>
<span data-ttu-id="8c1ac-123">Aby skonfigurować integrację usługi Azure AD miejsca pracy przez usługi Facebook, należy dodać miejsca pracy przez Facebook z galerii do listy zarządzanych aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="8c1ac-123">To configure the integration of Workplace by Facebook into Azure AD, add Workplace by Facebook from the gallery to your list of managed SaaS apps.</span></span>

1. <span data-ttu-id="8c1ac-124">W [portalu Azure](https://portal.azure.com), w okienku po lewej stronie wybierz **usługi Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="8c1ac-124">In the [Azure portal](https://portal.azure.com), in the left pane, select **Azure Active Directory**.</span></span> 

    ![Przycisk usługi Azure Active Directory][1]

2. <span data-ttu-id="8c1ac-126">Przejdź do **aplikacje dla przedsiębiorstw** > **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="8c1ac-126">Browse to **Enterprise applications** > **All applications**.</span></span>

    ![Blok aplikacje przedsiębiorstwa][2]
    
3. <span data-ttu-id="8c1ac-128">Aby dodać nową aplikację, zaznacz **nowej aplikacji** górnej części okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="8c1ac-128">To add the new application, select **New application** on the top of the dialog box.</span></span>

    ![Nowy przycisk aplikacji][3]

4. <span data-ttu-id="8c1ac-130">W polu wyszukiwania wpisz **miejsca pracy przez Facebook**i wybierz **miejsca pracy przez Facebook** z wyników.</span><span class="sxs-lookup"><span data-stu-id="8c1ac-130">In the search box, type **Workplace by Facebook**, and select **Workplace by Facebook** from results.</span></span> <span data-ttu-id="8c1ac-131">Następnie wybierz **Dodaj**, aby dodać aplikację.</span><span class="sxs-lookup"><span data-stu-id="8c1ac-131">Then select **Add**, to add the application.</span></span>

    ![Miejsce pracy przez usługi Facebook na liście wyników](./media/active-directory-saas-facebook-at-work-tutorial/tutorial_workplacebyfacebook_search.png)

##  <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="8c1ac-133">Konfiguracja i testowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="8c1ac-133">Configure and test Azure AD single sign-on</span></span>
<span data-ttu-id="8c1ac-134">W tej sekcji Konfiguracja i testowanie usługi Azure AD SSO z miejsca pracy przez Facebook, na podstawie użytkownika testowego, nazywany "Britta Simona".</span><span class="sxs-lookup"><span data-stu-id="8c1ac-134">In this section, you configure and test Azure AD SSO with Workplace by Facebook, based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="8c1ac-135">Dla logowania jednokrotnego do pracy usługi Azure AD musi wiedzieć, użytkownik odpowiednika w miejscu pracy przez Facebook jest dla użytkownika, w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="8c1ac-135">For SSO to work, Azure AD needs to know what the counterpart user in Workplace by Facebook is to a user in Azure AD.</span></span> <span data-ttu-id="8c1ac-136">Innymi słowy można ustanowić połączonego relacji między użytkownikiem usługi Azure AD i danemu użytkownikowi w miejscu pracy przez usługi Facebook.</span><span class="sxs-lookup"><span data-stu-id="8c1ac-136">In other words, a linked relationship between an Azure AD user and the related user in Workplace by Facebook should be established.</span></span>

<span data-ttu-id="8c1ac-137">Ustanowić tę relację, przypisując wartość **nazwy użytkownika** w usłudze Azure AD jako wartość **Username** w miejscu pracy przez usługi Facebook.</span><span class="sxs-lookup"><span data-stu-id="8c1ac-137">Establish this relationship by assigning the value of the **user name** in Azure AD as the value of the **Username** in Workplace by Facebook.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="8c1ac-138">Konfigurowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="8c1ac-138">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="8c1ac-139">W tej sekcji włączenia funkcji logowania jednokrotnego usługi Azure AD w portalu Azure i skonfigurować logowanie Jednokrotne w miejscu pracy aplikacji usługi Facebook.</span><span class="sxs-lookup"><span data-stu-id="8c1ac-139">In this section, you enable Azure AD SSO in the Azure portal, and you configure SSO in your Workplace by Facebook application.</span></span>

1. <span data-ttu-id="8c1ac-140">W portalu Azure na **miejsca pracy przez Facebook** strona integracji aplikacji, wybierz opcję **logowanie jednokrotne**.</span><span class="sxs-lookup"><span data-stu-id="8c1ac-140">In the Azure portal, on the **Workplace by Facebook** application integration page, select **Single sign-on**.</span></span>

    ![Skonfigurować łącze rejestracji jednokrotnej][4]

2. <span data-ttu-id="8c1ac-142">W **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** do włączenia funkcji logowania jednokrotnego.</span><span class="sxs-lookup"><span data-stu-id="8c1ac-142">In the **Single sign-on** dialog box, select **Mode** as **SAML-based Sign-on** to enable SSO.</span></span>
 
    ![Okno dialogowe rejestracji jednokrotnej](./media/active-directory-saas-facebook-at-work-tutorial/tutorial_workplacebyfacebook_samlbase.png)

3. <span data-ttu-id="8c1ac-144">W **miejsca pracy przez domenę usługi Facebook i adresy URL** sekcji, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="8c1ac-144">In the **Workplace by Facebook Domain and URLs** section, do the following:</span></span>

    <span data-ttu-id="8c1ac-145">a.</span><span class="sxs-lookup"><span data-stu-id="8c1ac-145">a.</span></span> <span data-ttu-id="8c1ac-146">W **adres URL logowania** wpisz adres URL, który korzysta z następującego wzorca:`https://<company subdomain>.facebook.com`</span><span class="sxs-lookup"><span data-stu-id="8c1ac-146">In the **Sign-on URL** text box, type a URL that uses the following pattern: `https://<company subdomain>.facebook.com`</span></span>

    <span data-ttu-id="8c1ac-147">b.</span><span class="sxs-lookup"><span data-stu-id="8c1ac-147">b.</span></span> <span data-ttu-id="8c1ac-148">W **identyfikator** wpisz adres URL, który korzysta z następującego wzorca:`https://www.facebook.com/company/<scim company id>`</span><span class="sxs-lookup"><span data-stu-id="8c1ac-148">In the **Identifier** text box, type a URL that uses the following pattern: `https://www.facebook.com/company/<scim company id>`</span></span>

    > [!NOTE]
    > <span data-ttu-id="8c1ac-149">Te wartości są tylko przykładem.</span><span class="sxs-lookup"><span data-stu-id="8c1ac-149">These values are an example only.</span></span> <span data-ttu-id="8c1ac-150">Rzeczywisty adres URL logowania i identyfikator, należy zaktualizować te wartości.</span><span class="sxs-lookup"><span data-stu-id="8c1ac-150">Update these values with the actual sign-on URL and identifier.</span></span> <span data-ttu-id="8c1ac-151">Skontaktuj się z [miejsca pracy przez zespół obsługi klienta usługi Facebook](https://workplace.fb.com/faq/) uzyskać te wartości.</span><span class="sxs-lookup"><span data-stu-id="8c1ac-151">Contact the [Workplace by Facebook Client support team](https://workplace.fb.com/faq/) to get these values.</span></span> 

4. <span data-ttu-id="8c1ac-152">W **certyfikat podpisywania SAML** wybierz opcję **certyfikatu (Base64)**, a następnie zapisz plik certyfikatu na komputerze.</span><span class="sxs-lookup"><span data-stu-id="8c1ac-152">In the **SAML Signing Certificate** section, select **Certificate (Base64)**, and then save the certificate file on your computer.</span></span>

    ![Łącze pobierania certyfikatu](./media/active-directory-saas-facebook-at-work-tutorial/tutorial_workplacebyfacebook_certificate.png) 

5. <span data-ttu-id="8c1ac-154">Wybierz pozycję **Zapisz**.</span><span class="sxs-lookup"><span data-stu-id="8c1ac-154">Select **Save**.</span></span>

    ![Skonfiguruj przycisk pojedynczego logowania jednokrotnego Zapisz](./media/active-directory-saas-facebook-at-work-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="8c1ac-156">W **miejsca pracy przez konfigurację usługi Facebook** wybierz opcję **skonfigurować miejsca pracy przez Facebook** otworzyć **Konfigurowanie logowania jednokrotnego** okna.</span><span class="sxs-lookup"><span data-stu-id="8c1ac-156">In the **Workplace by Facebook Configuration** section, select **Configure Workplace by Facebook** to open the **Configure sign-on** window.</span></span> <span data-ttu-id="8c1ac-157">Kopiuj **Sign-Out adres URL, identyfikator jednostki SAML i SAML pojedynczy znak na adres URL usługi** z **krótkimi opisami** sekcji.</span><span class="sxs-lookup"><span data-stu-id="8c1ac-157">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference** section.</span></span>

    ![Obszar roboczy w konfiguracji usługi Facebook](./media/active-directory-saas-facebook-at-work-tutorial/config.png) 

7. <span data-ttu-id="8c1ac-159">W oknie przeglądarki innej witryny sieci web należy zalogować się jako administrator do miejsca pracy przez witrynę firmy Facebook.</span><span class="sxs-lookup"><span data-stu-id="8c1ac-159">In a different web browser window, sign in to your Workplace by Facebook company site as an administrator.</span></span>
  
   > [!NOTE] 
   > <span data-ttu-id="8c1ac-160">W ramach procesu uwierzytelniania SAML miejsca pracy można użyć ciągów zapytania do 2,5 kilobajtów rozmiaru w celu przekazania parametrów do usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="8c1ac-160">As part of the SAML authentication process, Workplace can use query strings of up to 2.5 kilobytes in size in order to pass parameters to Azure AD.</span></span>

8. <span data-ttu-id="8c1ac-161">W **pulpitu nawigacyjnego firmy**, przejdź do **uwierzytelniania** kartę.</span><span class="sxs-lookup"><span data-stu-id="8c1ac-161">In the **Company Dashboard**, go to the **Authentication** tab.</span></span>

9. <span data-ttu-id="8c1ac-162">W obszarze **uwierzytelnianie SAML**, wybierz pozycję **logowania jednokrotnego tylko** z listy rozwijanej.</span><span class="sxs-lookup"><span data-stu-id="8c1ac-162">Under **SAML Authentication**, select **SSO Only** from the drop-down list.</span></span>

10. <span data-ttu-id="8c1ac-163">Wprowadź wartości skopiowanych z **miejsca pracy przez konfigurację usługi Facebook** części portalu Azure do odpowiednich pól:</span><span class="sxs-lookup"><span data-stu-id="8c1ac-163">Enter the values copied from the **Workplace by Facebook Configuration** section of the Azure portal into the corresponding fields:</span></span>

    *   <span data-ttu-id="8c1ac-164">W **adres URL SAML** tekst Wklej wartość **pojedynczy znak na adres URL usługi**, które zostały skopiowane z portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="8c1ac-164">In the **SAML URL** text box, paste the value of **Single Sign-On Service URL**, which you have copied from the Azure portal.</span></span>
    *   <span data-ttu-id="8c1ac-165">W **adres URL wystawcy SAML** tekst Wklej wartość **identyfikator jednostki SAML**, które zostały skopiowane z portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="8c1ac-165">In the **SAML Issuer URL** text box, paste the value of **SAML Entity ID**, which you have copied from the Azure portal.</span></span>
    *   <span data-ttu-id="8c1ac-166">W **SAML wylogowania przekierowania (opcjonalnie)**, Wklej wartość **Sign-Out URL**, które zostały skopiowane z portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="8c1ac-166">In **SAML Logout Redirect (optional)**, paste the value of **Sign-Out URL**, which you have copied from the Azure portal.</span></span>
    *   <span data-ttu-id="8c1ac-167">Otwórz z **certyfikatu algorytmem base-64** w Notatniku pobrany z portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="8c1ac-167">Open your **base-64 encoded certificate** in Notepad, downloaded from the Azure portal.</span></span> <span data-ttu-id="8c1ac-168">Skopiuj zawartość go do Schowka, a następnie wklej go do **certyfikatu SAML** pola tekstowego.</span><span class="sxs-lookup"><span data-stu-id="8c1ac-168">Copy the content of it into your clipboard, and then paste it to the **SAML Certificate** text box.</span></span>

11. <span data-ttu-id="8c1ac-169">Może być konieczne wprowadzenie adresu URL odbiorców, odbiorca wyświetlany adres URL i adresu URL ACS (potwierdzenie konsumenta usługa), w obszarze **Konfiguracja SAML** sekcji.</span><span class="sxs-lookup"><span data-stu-id="8c1ac-169">You might need to enter the audience URL, recipient URL, and ACS (Assertion Consumer Service) URL, listed under the **SAML Configuration** section.</span></span>

12. <span data-ttu-id="8c1ac-170">Przewiń w dół do sekcji, a następnie wybierz **Test rejestracji Jednokrotnej**.</span><span class="sxs-lookup"><span data-stu-id="8c1ac-170">Scroll to the bottom of the section, and select **Test SSO**.</span></span> <span data-ttu-id="8c1ac-171">Zostanie wyświetlone okno podręczne z strony logowania usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="8c1ac-171">A pop-up window appears, with the Azure AD sign-in page.</span></span> <span data-ttu-id="8c1ac-172">W celu uwierzytelnienia wprowadź swoje poświadczenia, jak zwykle.</span><span class="sxs-lookup"><span data-stu-id="8c1ac-172">To authenticate, enter your credentials as normal.</span></span> <span data-ttu-id="8c1ac-173">Upewnij się, adres e-mail zwracana z usługi Azure AD jest taka sama jak konto w miejscu pracy, które są rejestrowane przy użyciu.</span><span class="sxs-lookup"><span data-stu-id="8c1ac-173">Ensure the email address returned back from Azure AD is the same as the Workplace account you are logged in with.</span></span>

13. <span data-ttu-id="8c1ac-174">Jeśli test zakończył się pomyślnie, przewiń w dół strony i wybierz **zapisać**.</span><span class="sxs-lookup"><span data-stu-id="8c1ac-174">If the test has finished successfully, scroll to the bottom of the page and select **Save**.</span></span>

14. <span data-ttu-id="8c1ac-175">Teraz przedstawiono wszystkich osób korzystających z miejsca pracy z usługą Azure AD strony logowania dla uwierzytelniania.</span><span class="sxs-lookup"><span data-stu-id="8c1ac-175">Anyone using Workplace is now presented with Azure AD sign-in page for authentication.</span></span>

<span data-ttu-id="8c1ac-176">Można skonfigurować SAML wylogowaniu adresu URL, który może służyć do punktu w wyrejestrowywania usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="8c1ac-176">You can choose to configure a SAML sign out URL, which can be used to point at the Azure AD sign-out page.</span></span> <span data-ttu-id="8c1ac-177">Gdy to ustawienie jest włączone i skonfigurowane, użytkownik nie jest kierowany do strony wylogowania obszar roboczy.</span><span class="sxs-lookup"><span data-stu-id="8c1ac-177">When this setting is enabled and configured, the user is no longer directed to the Workplace sign-out page.</span></span> <span data-ttu-id="8c1ac-178">Użytkownik jest kierowana do adresu URL, który został dodany w ustawieniu przekierowania wylogowania SAML.</span><span class="sxs-lookup"><span data-stu-id="8c1ac-178">Instead, the user is redirected to the URL that was added in the SAML sign-out redirect setting.</span></span>


> [!TIP]
> <span data-ttu-id="8c1ac-179">Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji.</span><span class="sxs-lookup"><span data-stu-id="8c1ac-179">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app.</span></span> <span data-ttu-id="8c1ac-180">Po dodaniu tej aplikacji z **usługi Active Directory** > **aplikacje dla przedsiębiorstw** po prostu zaznacz **rejestracji jednokrotnej** karcie i dostęp do dokumentacji osadzonych za pomocą **konfiguracji** sekcji u dołu.</span><span class="sxs-lookup"><span data-stu-id="8c1ac-180">After adding this app from the **Active Directory** > **Enterprise Applications** section, simply select the **Single Sign-On** tab, and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="8c1ac-181">Więcej o funkcji dokumentacji osadzony w [usługi Azure AD osadzonych dokumentacji]( https://go.microsoft.com/fwlink/?linkid=845985).</span><span class="sxs-lookup"><span data-stu-id="8c1ac-181">You can read more about the embedded documentation feature in the [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985).</span></span>

### <a name="configure-reauthentication-frequency"></a><span data-ttu-id="8c1ac-182">Konfigurowanie częstotliwości ponowne uwierzytelnianie</span><span class="sxs-lookup"><span data-stu-id="8c1ac-182">Configure reauthentication frequency</span></span>

<span data-ttu-id="8c1ac-183">Można skonfigurować miejsca pracy z monitem o wyboru SAML codziennie trzech dni, co tydzień, dwa tygodnie, co miesiąc lub nigdy.</span><span class="sxs-lookup"><span data-stu-id="8c1ac-183">You can configure Workplace to prompt for a SAML check every day, three days, one week, two weeks, one month, or never.</span></span>

> [!NOTE] 
><span data-ttu-id="8c1ac-184">Minimalna wartość wyboru SAML na aplikacje mobilne wynosi tydzień.</span><span class="sxs-lookup"><span data-stu-id="8c1ac-184">The minimum value for the SAML check on mobile applications is set to one week.</span></span>

<span data-ttu-id="8c1ac-185">Możesz też wymusić SAML zresetować dla wszystkich użytkowników.</span><span class="sxs-lookup"><span data-stu-id="8c1ac-185">You can also force a SAML reset for all users.</span></span> <span data-ttu-id="8c1ac-186">Aby to zrobić, użyj **SAML wymagają uwierzytelniania wszystkich użytkowników, którzy teraz** przycisku.</span><span class="sxs-lookup"><span data-stu-id="8c1ac-186">To do this, use the **Require SAML authentication for all users now** button.</span></span>


### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="8c1ac-187">Tworzenie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="8c1ac-187">Create an Azure AD test user</span></span>
<span data-ttu-id="8c1ac-188">Celem tej sekcji jest tworzenie użytkownika testowego w portalu Azure o nazwie Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="8c1ac-188">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Tworzenie użytkowników usługi Azure AD][100]

1. <span data-ttu-id="8c1ac-190">W **portalu Azure**, w okienku po lewej stronie wybierz **usługi Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="8c1ac-190">In the **Azure portal**, in the left pane, select **Azure Active Directory**.</span></span>

    ![Przycisk usługi Azure Active Directory](./media/active-directory-saas-facebook-at-work-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="8c1ac-192">Aby wyświetlić listę użytkowników, przejdź do **użytkowników i grup**i wybierz **wszyscy użytkownicy**.</span><span class="sxs-lookup"><span data-stu-id="8c1ac-192">To display the list of users, go to **Users and groups**, and select **All users**.</span></span>
    
    !["Użytkownicy i grupy" i "Wszyscy użytkownicy" łącza](./media/active-directory-saas-facebook-at-work-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="8c1ac-194">Aby otworzyć **użytkownika** okno dialogowe, wybierz opcję **Dodaj**.</span><span class="sxs-lookup"><span data-stu-id="8c1ac-194">To open the **User** dialog box, select **Add**.</span></span>
 
    ![Przycisk Dodaj](./media/active-directory-saas-facebook-at-work-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="8c1ac-196">W **użytkownika** okno dialogowe, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="8c1ac-196">In the **User** dialog box, do the following:</span></span>
 
    ![Okno dialogowe użytkownika](./media/active-directory-saas-facebook-at-work-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="8c1ac-198">a.</span><span class="sxs-lookup"><span data-stu-id="8c1ac-198">a.</span></span> <span data-ttu-id="8c1ac-199">W **nazwa** polu tekstowym **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="8c1ac-199">In the **Name** text box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="8c1ac-200">b.</span><span class="sxs-lookup"><span data-stu-id="8c1ac-200">b.</span></span> <span data-ttu-id="8c1ac-201">W **nazwy użytkownika** polu tekstowym **adres e-mail** z BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="8c1ac-201">In the **User name** text box, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="8c1ac-202">c.</span><span class="sxs-lookup"><span data-stu-id="8c1ac-202">c.</span></span> <span data-ttu-id="8c1ac-203">Wybierz **Pokaż hasło**i zapisz ją.</span><span class="sxs-lookup"><span data-stu-id="8c1ac-203">Select **Show Password**, and write it down.</span></span>

    <span data-ttu-id="8c1ac-204">d.</span><span class="sxs-lookup"><span data-stu-id="8c1ac-204">d.</span></span> <span data-ttu-id="8c1ac-205">Wybierz pozycję **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="8c1ac-205">Select **Create**.</span></span>
 
### <a name="create-a-workplace-by-facebook-test-user"></a><span data-ttu-id="8c1ac-206">Utwórz pracy przez użytkownika testowego usługi Facebook</span><span class="sxs-lookup"><span data-stu-id="8c1ac-206">Create a Workplace by Facebook test user</span></span>

<span data-ttu-id="8c1ac-207">W tej sekcji o nazwie Simona Britta tworzenia użytkownika w miejscu pracy przez usługi Facebook.</span><span class="sxs-lookup"><span data-stu-id="8c1ac-207">In this section, a user called Britta Simon is created in Workplace by Facebook.</span></span> <span data-ttu-id="8c1ac-208">Obszar roboczy w serwisie Facebook obsługę w czasie, który jest domyślnie włączona.</span><span class="sxs-lookup"><span data-stu-id="8c1ac-208">Workplace by Facebook supports just-in-time provisioning, which is enabled by default.</span></span>

<span data-ttu-id="8c1ac-209">Brak akcji można w tej sekcji.</span><span class="sxs-lookup"><span data-stu-id="8c1ac-209">There is no action for you in this section.</span></span> <span data-ttu-id="8c1ac-210">Jeśli użytkownik nie istnieje w miejscu pracy przez usługi Facebook, nowy jest tworzona przy próbie uzyskania dostępu do miejsca pracy przez usługi Facebook.</span><span class="sxs-lookup"><span data-stu-id="8c1ac-210">If a user doesn't exist in Workplace by Facebook, a new one is created when you attempt to access Workplace by Facebook.</span></span>

>[!Note]
><span data-ttu-id="8c1ac-211">Jeśli trzeba ręcznie utworzyć użytkownika, skontaktuj się z [miejsca pracy przez zespół obsługi klienta usługi Facebook](https://workplace.fb.com/faq/).</span><span class="sxs-lookup"><span data-stu-id="8c1ac-211">If you need to create a user manually, contact the [Workplace by Facebook Client support team](https://workplace.fb.com/faq/).</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="8c1ac-212">Przypisz użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="8c1ac-212">Assign the Azure AD test user</span></span>

<span data-ttu-id="8c1ac-213">W tej sekcji można włączyć Simona Britta do używania Azure logowania jednokrotnego za udzielanie dostępu do miejsca pracy przez usługi Facebook.</span><span class="sxs-lookup"><span data-stu-id="8c1ac-213">In this section, you enable Britta Simon to use Azure SSO by granting access to Workplace by Facebook.</span></span>

![Przypisz użytkownika][200] 

1. <span data-ttu-id="8c1ac-215">W portalu Azure Otwórz widok aplikacji.</span><span class="sxs-lookup"><span data-stu-id="8c1ac-215">In the Azure portal, open the applications view.</span></span> <span data-ttu-id="8c1ac-216">Przejdź do widoku katalogu, przejdź do **aplikacje dla przedsiębiorstw**, a następnie wybierz **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="8c1ac-216">Go to the directory view, go to **Enterprise applications**, and then select **All applications**.</span></span>

    ![Przypisz użytkownika][201] 

2. <span data-ttu-id="8c1ac-218">Na liście aplikacji zaznacz **miejsca pracy przez Facebook**.</span><span class="sxs-lookup"><span data-stu-id="8c1ac-218">In the applications list, select **Workplace by Facebook**.</span></span>

    ![Miejsce pracy za pośrednictwem łącza na liście aplikacji usługi Facebook](./media/active-directory-saas-facebook-at-work-tutorial/tutorial_workplacebyfacebook_app.png) 

3. <span data-ttu-id="8c1ac-220">W menu po lewej stronie wybierz **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="8c1ac-220">In the menu on the left, select **Users and groups**.</span></span>

    ![Łącze "Użytkownicy i grupy"][202] 

4. <span data-ttu-id="8c1ac-222">Wybierz pozycję **Dodaj**.</span><span class="sxs-lookup"><span data-stu-id="8c1ac-222">Select **Add**.</span></span> <span data-ttu-id="8c1ac-223">Następnie w **Dodaj przydziału** okienku wybierz **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="8c1ac-223">Then, in the **Add Assignment** pane, select **Users and groups**.</span></span>

    ![W okienku Dodaj przydziału][203]

5. <span data-ttu-id="8c1ac-225">W **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** na liście Użytkownicy.</span><span class="sxs-lookup"><span data-stu-id="8c1ac-225">In the **Users and groups** dialog box, select **Britta Simon** in the users list.</span></span>

6. <span data-ttu-id="8c1ac-226">W **użytkowników i grup** okno dialogowe, wybierz opcję **wybierz**.</span><span class="sxs-lookup"><span data-stu-id="8c1ac-226">In the **Users and groups** dialog box, select **Select**.</span></span>

7. <span data-ttu-id="8c1ac-227">W **Dodaj przydziału** okno dialogowe, wybierz opcję **przypisać**.</span><span class="sxs-lookup"><span data-stu-id="8c1ac-227">In the **Add Assignment** dialog box, select **Assign**.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="8c1ac-228">Test rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="8c1ac-228">Test single sign-on</span></span>

<span data-ttu-id="8c1ac-229">Jeśli chcesz przetestować ustawienia logowania jednokrotnego, otwórz Panel dostępu.</span><span class="sxs-lookup"><span data-stu-id="8c1ac-229">If you want to test your SSO settings, open the Access Panel.</span></span>
<span data-ttu-id="8c1ac-230">Aby uzyskać więcej informacji, zobacz [Wprowadzenie do panelu dostępu](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="8c1ac-230">For more information, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>


## <a name="next-steps"></a><span data-ttu-id="8c1ac-231">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="8c1ac-231">Next steps</span></span>

* <span data-ttu-id="8c1ac-232">Zobacz [lista samouczków dotyczących sposobów integracji aplikacji SaaS w usłudze Azure Active Directory](active-directory-saas-tutorial-list.md).</span><span class="sxs-lookup"><span data-stu-id="8c1ac-232">See the [list of tutorials on how to integrate SaaS Apps with Azure Active Directory](active-directory-saas-tutorial-list.md).</span></span>
* <span data-ttu-id="8c1ac-233">Odczyt [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="8c1ac-233">Read [What is application access and single sign-on with Azure Active Directory?](active-directory-appssoaccess-whatis.md).</span></span>
* <span data-ttu-id="8c1ac-234">Dowiedz się więcej o sposobie [skonfigurować Inicjowanie obsługi użytkowników](active-directory-saas-facebook-at-work-provisioning-tutorial.md).</span><span class="sxs-lookup"><span data-stu-id="8c1ac-234">Learn more about how to [configure user provisioning](active-directory-saas-facebook-at-work-provisioning-tutorial.md).</span></span>



<!--Image references-->

[1]: ./media/active-directory-saas-facebook-at-work-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-facebook-at-work-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-facebook-at-work-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-facebook-at-work-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-facebook-at-work-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-facebook-at-work-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-facebook-at-work-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-facebook-at-work-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-facebook-at-work-tutorial/tutorial_general_203.png

