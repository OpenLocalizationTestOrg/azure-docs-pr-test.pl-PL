---
title: 'Samouczek: Integracji Azure Active Directory z Kiteworks | Dokumentacja firmy Microsoft'
description: "Informacje o sposobie konfigurowania rejestracji jednokrotnej między usługą Azure Active Directory i Kiteworks."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: f7984aaf-ab1f-4a85-9646-a9523f5275d9
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/20/2017
ms.author: jeedes
ms.openlocfilehash: 2fd9b346cb6d838069ef94ee9c2a8d113f22779c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-kiteworks"></a><span data-ttu-id="72f0c-103">Samouczek: Integracji Azure Active Directory z Kiteworks</span><span class="sxs-lookup"><span data-stu-id="72f0c-103">Tutorial: Azure Active Directory integration with Kiteworks</span></span>

<span data-ttu-id="72f0c-104">Z tego samouczka dowiesz się integrowanie Kiteworks z usługi Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="72f0c-104">In this tutorial, you learn how to integrate Kiteworks with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="72f0c-105">Integracja z usługą Azure AD Kiteworks zapewnia następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="72f0c-105">Integrating Kiteworks with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="72f0c-106">Można kontrolować w usłudze Azure AD, który ma dostęp do Kiteworks</span><span class="sxs-lookup"><span data-stu-id="72f0c-106">You can control in Azure AD who has access to Kiteworks</span></span>
- <span data-ttu-id="72f0c-107">Umożliwia użytkownikom automatycznie pobrać zalogowane do Kiteworks (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="72f0c-107">You can enable your users to automatically get signed-on to Kiteworks (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="72f0c-108">Możesz zarządzać kont w jednej centralnej lokalizacji - portalu Azure</span><span class="sxs-lookup"><span data-stu-id="72f0c-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="72f0c-109">Jeśli chcesz dowiedzieć się więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="72f0c-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="72f0c-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="72f0c-110">Prerequisites</span></span>

<span data-ttu-id="72f0c-111">Aby skonfigurować integrację usługi Azure AD z Kiteworks, potrzebne są następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="72f0c-111">To configure Azure AD integration with Kiteworks, you need the following items:</span></span>

- <span data-ttu-id="72f0c-112">Subskrypcję usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="72f0c-112">An Azure AD subscription</span></span>
- <span data-ttu-id="72f0c-113">Kiteworks logowanie jednokrotne włączone subskrypcji</span><span class="sxs-lookup"><span data-stu-id="72f0c-113">A Kiteworks single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="72f0c-114">Aby przetestować kroki opisane w tym samouczku, zaleca się używania środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="72f0c-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="72f0c-115">Aby przetestować kroki opisane w tym samouczku, należy wykonać te zalecenia:</span><span class="sxs-lookup"><span data-stu-id="72f0c-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="72f0c-116">Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="72f0c-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="72f0c-117">Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz pobrać miesięczna wersja próbna [tutaj](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="72f0c-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="72f0c-118">Opis scenariusza</span><span class="sxs-lookup"><span data-stu-id="72f0c-118">Scenario description</span></span>
<span data-ttu-id="72f0c-119">W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym.</span><span class="sxs-lookup"><span data-stu-id="72f0c-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="72f0c-120">Scenariusz opisany w tym samouczku składa się z dwóch głównych elementów:</span><span class="sxs-lookup"><span data-stu-id="72f0c-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="72f0c-121">Dodawanie Kiteworks z galerii</span><span class="sxs-lookup"><span data-stu-id="72f0c-121">Adding Kiteworks from the gallery</span></span>
2. <span data-ttu-id="72f0c-122">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="72f0c-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-kiteworks-from-the-gallery"></a><span data-ttu-id="72f0c-123">Dodawanie Kiteworks z galerii</span><span class="sxs-lookup"><span data-stu-id="72f0c-123">Adding Kiteworks from the gallery</span></span>
<span data-ttu-id="72f0c-124">Aby skonfigurować integrację usługi Azure AD Kiteworks, należy dodać Kiteworks z galerii do listy zarządzanych aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="72f0c-124">To configure the integration of Kiteworks into Azure AD, you need to add Kiteworks from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="72f0c-125">**Aby dodać Kiteworks z galerii, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="72f0c-125">**To add Kiteworks from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="72f0c-126">W  **[portalu Azure](https://portal.azure.com)**, na panelu nawigacyjnym po lewej stronie kliknij **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="72f0c-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Usługa Active Directory][1]

2. <span data-ttu-id="72f0c-128">Przejdź do **aplikacje dla przedsiębiorstw**.</span><span class="sxs-lookup"><span data-stu-id="72f0c-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="72f0c-129">Następnie przejdź do **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="72f0c-129">Then go to **All applications**.</span></span>

    ![Aplikacje][2]
    
3. <span data-ttu-id="72f0c-131">Aby dodać nową aplikację, kliknij przycisk **nowej aplikacji** przycisk w górnej części okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="72f0c-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Aplikacje][3]

4. <span data-ttu-id="72f0c-133">W polu wyszukiwania wpisz **Kiteworks**.</span><span class="sxs-lookup"><span data-stu-id="72f0c-133">In the search box, type **Kiteworks**.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-kiteworks-tutorial/tutorial_kiteworks_search.png)

5. <span data-ttu-id="72f0c-135">W panelu wyników wybierz **Kiteworks**, a następnie kliknij przycisk **Dodaj** przycisk, aby dodać aplikację.</span><span class="sxs-lookup"><span data-stu-id="72f0c-135">In the results panel, select **Kiteworks**, and then click **Add** button to add the application.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-kiteworks-tutorial/tutorial_kiteworks_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="72f0c-137">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="72f0c-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="72f0c-138">W tej sekcji skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z Kiteworks w oparciu o nazwie "Britta Simona" użytkownika testowego.</span><span class="sxs-lookup"><span data-stu-id="72f0c-138">In this section, you configure and test Azure AD single sign-on with Kiteworks based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="72f0c-139">Dla rejestracji jednokrotnej do pracy usługi Azure AD musi wiedzieć, użytkownik odpowiednika w Kiteworks jest dla użytkownika, w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="72f0c-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Kiteworks is to a user in Azure AD.</span></span> <span data-ttu-id="72f0c-140">Innymi słowy link relację między użytkownikiem usługi Azure AD i danemu użytkownikowi w Kiteworks musi się.</span><span class="sxs-lookup"><span data-stu-id="72f0c-140">In other words, a link relationship between an Azure AD user and the related user in Kiteworks needs to be established.</span></span>

<span data-ttu-id="72f0c-141">W Kiteworks, należy przypisać wartość **nazwy użytkownika** w usłudze Azure AD jako wartość **Username** do ustanawiania relacji łącza.</span><span class="sxs-lookup"><span data-stu-id="72f0c-141">In Kiteworks, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="72f0c-142">Aby skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z Kiteworks, należy wykonać poniższe bloki konstrukcyjne:</span><span class="sxs-lookup"><span data-stu-id="72f0c-142">To configure and test Azure AD single sign-on with Kiteworks, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="72f0c-143">**[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configuring-azure-ad-single-sign-on)**  — aby umożliwić użytkownikom korzystać z tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="72f0c-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="72f0c-144">**[Tworzenie użytkownika testowego usługi Azure AD](#creating-an-azure-ad-test-user)**  — do przetestowania usługi Azure AD rejestracji jednokrotnej z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="72f0c-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="72f0c-145">**[Tworzenie użytkownika testowego Kiteworks](#creating-a-kiteworks-test-user)**  — w celu zapewnienia odpowiednikiem Simona Britta Kiteworks połączonego z usługi Azure AD reprezentację użytkownika.</span><span class="sxs-lookup"><span data-stu-id="72f0c-145">**[Creating a Kiteworks test user](#creating-a-kiteworks-test-user)** - to have a counterpart of Britta Simon in Kiteworks that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="72f0c-146">**[Przypisanie użytkownika testowego usługi Azure AD](#assigning-the-azure-ad-test-user)**  — aby umożliwić Simona Britta do użycia usługi Azure AD rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="72f0c-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="72f0c-147">**[Testowanie rejestracji jednokrotnej](#testing-single-sign-on)**  — Aby sprawdzić, czy konfiguracja działa.</span><span class="sxs-lookup"><span data-stu-id="72f0c-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="72f0c-148">Konfigurowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="72f0c-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="72f0c-149">W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w portalu Azure i skonfigurować logowanie jednokrotne w aplikacji Kiteworks.</span><span class="sxs-lookup"><span data-stu-id="72f0c-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Kiteworks application.</span></span>

<span data-ttu-id="72f0c-150">**Aby skonfigurować usługi Azure AD rejestracji jednokrotnej z Kiteworks, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="72f0c-150">**To configure Azure AD single sign-on with Kiteworks, perform the following steps:**</span></span>

1. <span data-ttu-id="72f0c-151">W portalu Azure na **Kiteworks** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.</span><span class="sxs-lookup"><span data-stu-id="72f0c-151">In the Azure portal, on the **Kiteworks** application integration page, click **Single sign-on**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej][4]

2. <span data-ttu-id="72f0c-153">Na **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** Aby włączyć logowanie jednokrotne.</span><span class="sxs-lookup"><span data-stu-id="72f0c-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-kiteworks-tutorial/tutorial_kiteworks_samlbase.png)

3. <span data-ttu-id="72f0c-155">Na **Kiteworks domeny i adres URL** sekcji, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="72f0c-155">On the **Kiteworks Domain and URLs** section, perform the following steps:</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-kiteworks-tutorial/tutorial_kiteworks_url.png)

    <span data-ttu-id="72f0c-157">a.</span><span class="sxs-lookup"><span data-stu-id="72f0c-157">a.</span></span> <span data-ttu-id="72f0c-158">W **adres URL logowania** tekstowym, wpisz adres URL, używając następującego wzorca:`https://<subdomain>.kiteworks.com`</span><span class="sxs-lookup"><span data-stu-id="72f0c-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<subdomain>.kiteworks.com`</span></span>

    <span data-ttu-id="72f0c-159">b.</span><span class="sxs-lookup"><span data-stu-id="72f0c-159">b.</span></span> <span data-ttu-id="72f0c-160">W **identyfikator** tekstowym, wpisz adres URL, używając następującego wzorca:`https://<subdomain>.kiteworks.com/sp/module.php/saml/sp/saml2-acs.php/sp-sso`</span><span class="sxs-lookup"><span data-stu-id="72f0c-160">In the **Identifier** textbox, type a URL using the following pattern: `https://<subdomain>.kiteworks.com/sp/module.php/saml/sp/saml2-acs.php/sp-sso`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="72f0c-161">Wartości te nie są prawdziwe.</span><span class="sxs-lookup"><span data-stu-id="72f0c-161">These values are not real.</span></span> <span data-ttu-id="72f0c-162">Rzeczywisty adres URL logowania i identyfikator, należy zaktualizować te wartości.</span><span class="sxs-lookup"><span data-stu-id="72f0c-162">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="72f0c-163">Skontaktuj się z [zespołem pomocy technicznej klienta Kiteworks](http://accellion.com/support) uzyskać te wartości.</span><span class="sxs-lookup"><span data-stu-id="72f0c-163">Contact [Kiteworks Client support team](http://accellion.com/support) to get these values.</span></span> 
 
4. <span data-ttu-id="72f0c-164">Na **certyfikat podpisywania SAML** kliknij **certyfikatu (Base64)** , a następnie zapisz plik certyfikatu na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="72f0c-164">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-kiteworks-tutorial/tutorial_kiteworks_certificate.png) 

5. <span data-ttu-id="72f0c-166">Kliknij przycisk **zapisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="72f0c-166">Click **Save** button.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-kiteworks-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="72f0c-168">Na **konfiguracji Kiteworks** , kliknij przycisk **skonfigurować Kiteworks** otworzyć **Konfigurowanie logowania jednokrotnego** okna.</span><span class="sxs-lookup"><span data-stu-id="72f0c-168">On the **Kiteworks Configuration** section, click **Configure Kiteworks** to open **Configure sign-on** window.</span></span> <span data-ttu-id="72f0c-169">Kopiuj **Sign-Out adres URL, identyfikator jednostki SAML i SAML pojedynczy znak na adres URL usługi** z **sekcji krótkimi opisami.**</span><span class="sxs-lookup"><span data-stu-id="72f0c-169">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-kiteworks-tutorial/tutorial_kiteworks_configure.png) 

7. <span data-ttu-id="72f0c-171">Zalogować się do witryny firmy Kiteworks jako administrator.</span><span class="sxs-lookup"><span data-stu-id="72f0c-171">Sign on to your Kiteworks company site as an administrator.</span></span>

8. <span data-ttu-id="72f0c-172">Na pasku narzędzi u góry kliknij **ustawienia**.</span><span class="sxs-lookup"><span data-stu-id="72f0c-172">In the toolbar on the top, click **Settings**.</span></span>
   
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-kiteworks-tutorial/tutorial_kiteworks_06.png) 

9. <span data-ttu-id="72f0c-174">W **uwierzytelniania i autoryzacji** kliknij **ustawienia logowania jednokrotnego**.</span><span class="sxs-lookup"><span data-stu-id="72f0c-174">In the **Authentication and Authorization** section, click **SSO Setup**.</span></span> 
   
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-kiteworks-tutorial/tutorial_kiteworks_07.png)
 
10. <span data-ttu-id="72f0c-176">Na stronie Ustawienia logowania jednokrotnego wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="72f0c-176">On the SSO Setup page, perform the following steps:</span></span>
   
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-kiteworks-tutorial/tutorial_kiteworks_09.png)   

    <span data-ttu-id="72f0c-178">a.</span><span class="sxs-lookup"><span data-stu-id="72f0c-178">a.</span></span> <span data-ttu-id="72f0c-179">Wybierz **uwierzytelniania za pomocą logowania jednokrotnego**.</span><span class="sxs-lookup"><span data-stu-id="72f0c-179">Select **Authenticate via SSO**.</span></span>

    <span data-ttu-id="72f0c-180">b.</span><span class="sxs-lookup"><span data-stu-id="72f0c-180">b.</span></span> <span data-ttu-id="72f0c-181">Wybierz **zainicjować AuthnRequest**.</span><span class="sxs-lookup"><span data-stu-id="72f0c-181">Select **Initiate AuthnRequest**.</span></span>

    <span data-ttu-id="72f0c-182">c.</span><span class="sxs-lookup"><span data-stu-id="72f0c-182">c.</span></span> <span data-ttu-id="72f0c-183">W **identyfikator jednostki IDP** pole tekstowe, Wklej wartość **SAML identyfikator jednostki**, które zostały skopiowane z portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="72f0c-183">In the **IDP Entity ID** textbox, paste the value of **SAML Entity ID**, which you have copied from Azure portal.</span></span> 

    <span data-ttu-id="72f0c-184">d.</span><span class="sxs-lookup"><span data-stu-id="72f0c-184">d.</span></span> <span data-ttu-id="72f0c-185">W **pojedynczy znak na adres URL usługi** pole tekstowe, Wklej wartość **SAML pojedynczy znak na adres URL usługi**, które zostały skopiowane z portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="72f0c-185">In the **Single Sign-On Service URL** textbox, paste the value of **SAML Single Sign-On Service URL**, which you have copied from Azure portal.</span></span>

    <span data-ttu-id="72f0c-186">e.</span><span class="sxs-lookup"><span data-stu-id="72f0c-186">e.</span></span> <span data-ttu-id="72f0c-187">W **pojedynczy adres URL usługi wylogowania** pole tekstowe, Wklej wartość **Sign-Out URL**, które zostały skopiowane z portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="72f0c-187">In the **Single Logout Service URL** textbox, paste the value of **Sign-Out URL**, which you have copied from Azure portal.</span></span>

    <span data-ttu-id="72f0c-188">f.</span><span class="sxs-lookup"><span data-stu-id="72f0c-188">f.</span></span> <span data-ttu-id="72f0c-189">Otwórz w Notatniku pobranego certyfikatu, skopiuj zawartość, a następnie wklej go do **certyfikatu klucza publicznego RSA** pola tekstowego.</span><span class="sxs-lookup"><span data-stu-id="72f0c-189">Open your downloaded certificate in Notepad, copy the content, and then paste it into the **RSA Public Key Certificate** textbox.</span></span>
 
    <span data-ttu-id="72f0c-190">g.</span><span class="sxs-lookup"><span data-stu-id="72f0c-190">g.</span></span> <span data-ttu-id="72f0c-191">Kliknij pozycję **Zapisz**.</span><span class="sxs-lookup"><span data-stu-id="72f0c-191">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="72f0c-192">Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji!</span><span class="sxs-lookup"><span data-stu-id="72f0c-192">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="72f0c-193">Po dodaniu tej aplikacji z **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij **rejestracji jednokrotnej** karcie i dostęp do dokumentacji osadzonych za pomocą **konfiguracji** sekcji u dołu.</span><span class="sxs-lookup"><span data-stu-id="72f0c-193">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="72f0c-194">Więcej o funkcji dokumentacji osadzonego w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="72f0c-194">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="72f0c-195">Tworzenie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="72f0c-195">Creating an Azure AD test user</span></span>
<span data-ttu-id="72f0c-196">Celem tej sekcji jest tworzenie użytkownika testowego w portalu Azure o nazwie Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="72f0c-196">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Tworzenie użytkowników usługi Azure AD][100]

<span data-ttu-id="72f0c-198">**Aby utworzyć użytkownika testowego w usłudze Azure AD, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="72f0c-198">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="72f0c-199">W **portalu Azure**, w lewym okienku nawigacji, kliknij polecenie **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="72f0c-199">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-kiteworks-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="72f0c-201">Aby wyświetlić listę użytkowników, przejdź do **użytkowników i grup** i kliknij przycisk **wszyscy użytkownicy**.</span><span class="sxs-lookup"><span data-stu-id="72f0c-201">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-kiteworks-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="72f0c-203">Aby otworzyć **użytkownika** okna dialogowego, kliknij przycisk **Dodaj** górnej części okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="72f0c-203">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-kiteworks-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="72f0c-205">Na **użytkownika** okna dialogowego strony, należy wykonać następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="72f0c-205">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-kiteworks-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="72f0c-207">a.</span><span class="sxs-lookup"><span data-stu-id="72f0c-207">a.</span></span> <span data-ttu-id="72f0c-208">W **nazwa** pole tekstowe, typ **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="72f0c-208">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="72f0c-209">b.</span><span class="sxs-lookup"><span data-stu-id="72f0c-209">b.</span></span> <span data-ttu-id="72f0c-210">W **nazwy użytkownika** pole tekstowe, typ **adres e-mail** z BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="72f0c-210">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="72f0c-211">c.</span><span class="sxs-lookup"><span data-stu-id="72f0c-211">c.</span></span> <span data-ttu-id="72f0c-212">Wybierz **Pokaż hasło** i zanotuj wartość **hasło**.</span><span class="sxs-lookup"><span data-stu-id="72f0c-212">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="72f0c-213">d.</span><span class="sxs-lookup"><span data-stu-id="72f0c-213">d.</span></span> <span data-ttu-id="72f0c-214">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="72f0c-214">Click **Create**.</span></span>
 
### <a name="creating-a-kiteworks-test-user"></a><span data-ttu-id="72f0c-215">Tworzenie użytkownika testowego Kiteworks</span><span class="sxs-lookup"><span data-stu-id="72f0c-215">Creating a Kiteworks test user</span></span>

<span data-ttu-id="72f0c-216">Celem tej sekcji jest utworzenie użytkownika o nazwie Simona Britta w Kiteworks.</span><span class="sxs-lookup"><span data-stu-id="72f0c-216">The objective of this section is to create a user called Britta Simon in Kiteworks.</span></span>

<span data-ttu-id="72f0c-217">Kiteworks obsługę w czasie, który jest domyślnie włączone.</span><span class="sxs-lookup"><span data-stu-id="72f0c-217">Kiteworks supports just-in-time provisioning, which is by default enabled.</span></span> <span data-ttu-id="72f0c-218">Nie ma elementu akcji można w tej sekcji.</span><span class="sxs-lookup"><span data-stu-id="72f0c-218">There is no action item for you in this section.</span></span> <span data-ttu-id="72f0c-219">Nowy użytkownik został utworzony podczas próby dostępu Kitewors, jeśli go jeszcze nie istnieje.</span><span class="sxs-lookup"><span data-stu-id="72f0c-219">A new user is created during an attempt to access Kitewors if it doesn't exist yet.</span></span>

>[!NOTE]
><span data-ttu-id="72f0c-220">Jeśli trzeba ręcznie utworzyć użytkownika, należy skontaktować się [Kiteworks obsługuje zespołu](http://accellion.com/support).</span><span class="sxs-lookup"><span data-stu-id="72f0c-220">If you need to create a user manually, you need to contact the [Kiteworks support team](http://accellion.com/support).</span></span>
 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="72f0c-221">Przypisanie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="72f0c-221">Assigning the Azure AD test user</span></span>

<span data-ttu-id="72f0c-222">W tej sekcji można włączyć Simona Britta do używania Azure logowania jednokrotnego za udzielanie dostępu Kiteworks.</span><span class="sxs-lookup"><span data-stu-id="72f0c-222">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Kiteworks.</span></span>

![Przypisz użytkownika][200] 

<span data-ttu-id="72f0c-224">**Aby przypisać Simona Britta Kiteworks, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="72f0c-224">**To assign Britta Simon to Kiteworks, perform the following steps:**</span></span>

1. <span data-ttu-id="72f0c-225">W portalu Azure Otwórz widok aplikacji, a następnie przejdź do widoku katalogu i przejdź do **aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="72f0c-225">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Przypisz użytkownika][201] 

2. <span data-ttu-id="72f0c-227">Na liście aplikacji zaznacz **Kiteworks**.</span><span class="sxs-lookup"><span data-stu-id="72f0c-227">In the applications list, select **Kiteworks**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-kiteworks-tutorial/tutorial_kiteworks_app.png) 

3. <span data-ttu-id="72f0c-229">W menu po lewej stronie kliknij **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="72f0c-229">In the menu on the left, click **Users and groups**.</span></span>

    ![Przypisz użytkownika][202] 

4. <span data-ttu-id="72f0c-231">Kliknij przycisk **Dodaj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="72f0c-231">Click **Add** button.</span></span> <span data-ttu-id="72f0c-232">Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="72f0c-232">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Przypisz użytkownika][203]

5. <span data-ttu-id="72f0c-234">Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** na liście Użytkownicy.</span><span class="sxs-lookup"><span data-stu-id="72f0c-234">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="72f0c-235">Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="72f0c-235">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="72f0c-236">Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="72f0c-236">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="72f0c-237">Testowanie rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="72f0c-237">Testing single sign-on</span></span>

<span data-ttu-id="72f0c-238">Celem tej sekcji służy do testowania konfigurację usługi Azure AD z logowania jednokrotnego za pomocą panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="72f0c-238">The objective of this section is to test your Azure AD SSO configuration using the Access Panel.</span></span>  

<span data-ttu-id="72f0c-239">Po kliknięciu kafelka Kiteworks w panelu dostępu użytkownik powinien pobrać automatycznie zalogowane do aplikacji Kiteworks.</span><span class="sxs-lookup"><span data-stu-id="72f0c-239">When you click the Kiteworks tile in the Access Panel, you should get automatically signed-on to your Kiteworks application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="72f0c-240">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="72f0c-240">Additional resources</span></span>

* [<span data-ttu-id="72f0c-241">Lista samouczków dotyczących sposobów integracji aplikacji SaaS przy użyciu usługi Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="72f0c-241">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="72f0c-242">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="72f0c-242">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-kiteworks-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-kiteworks-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-kiteworks-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-kiteworks-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-kiteworks-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-kiteworks-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-kiteworks-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-kiteworks-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-kiteworks-tutorial/tutorial_general_203.png

