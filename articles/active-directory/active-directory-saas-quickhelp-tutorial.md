---
title: 'Samouczek: Integracji Azure Active Directory z QuickHelp | Dokumentacja firmy Microsoft'
description: "Informacje o sposobie konfigurowania rejestracji jednokrotnej między usługą Azure Active Directory i QuickHelp."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 655c9ad3-2076-4e2c-8e47-9ed3bf04be56
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/03/2017
ms.author: jeedes
ms.openlocfilehash: 1c72b0ddee636090129dab7a5c7ec6ffd452434a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-quickhelp"></a><span data-ttu-id="42a43-103">Samouczek: Integracji Azure Active Directory z QuickHelp</span><span class="sxs-lookup"><span data-stu-id="42a43-103">Tutorial: Azure Active Directory integration with QuickHelp</span></span>

<span data-ttu-id="42a43-104">Z tego samouczka dowiesz się integrowanie QuickHelp z usługi Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="42a43-104">In this tutorial, you learn how to integrate QuickHelp with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="42a43-105">Integracja z usługą Azure AD QuickHelp zapewnia następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="42a43-105">Integrating QuickHelp with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="42a43-106">Można kontrolować w usłudze Azure AD, który ma dostęp do QuickHelp</span><span class="sxs-lookup"><span data-stu-id="42a43-106">You can control in Azure AD who has access to QuickHelp</span></span>
- <span data-ttu-id="42a43-107">Umożliwia użytkownikom automatycznie pobrać zalogowane do QuickHelp (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="42a43-107">You can enable your users to automatically get signed-on to QuickHelp (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="42a43-108">Możesz zarządzać kont w jednej centralnej lokalizacji - portalu Azure</span><span class="sxs-lookup"><span data-stu-id="42a43-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="42a43-109">Jeśli chcesz dowiedzieć się więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="42a43-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="42a43-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="42a43-110">Prerequisites</span></span>

<span data-ttu-id="42a43-111">Aby skonfigurować integrację usługi Azure AD z QuickHelp, potrzebne są następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="42a43-111">To configure Azure AD integration with QuickHelp, you need the following items:</span></span>

- <span data-ttu-id="42a43-112">Subskrypcję usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="42a43-112">An Azure AD subscription</span></span>
- <span data-ttu-id="42a43-113">QuickHelp logowanie jednokrotne włączone subskrypcji</span><span class="sxs-lookup"><span data-stu-id="42a43-113">A QuickHelp single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="42a43-114">Aby przetestować kroki opisane w tym samouczku, zaleca się używania środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="42a43-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="42a43-115">Aby przetestować kroki opisane w tym samouczku, należy wykonać te zalecenia:</span><span class="sxs-lookup"><span data-stu-id="42a43-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="42a43-116">Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="42a43-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="42a43-117">Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz pobrać miesięczna wersja próbna [tutaj](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="42a43-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="42a43-118">Opis scenariusza</span><span class="sxs-lookup"><span data-stu-id="42a43-118">Scenario description</span></span>
<span data-ttu-id="42a43-119">W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym.</span><span class="sxs-lookup"><span data-stu-id="42a43-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="42a43-120">Scenariusz opisany w tym samouczku składa się z dwóch głównych elementów:</span><span class="sxs-lookup"><span data-stu-id="42a43-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="42a43-121">Dodawanie QuickHelp z galerii</span><span class="sxs-lookup"><span data-stu-id="42a43-121">Adding QuickHelp from the gallery</span></span>
2. <span data-ttu-id="42a43-122">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="42a43-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-quickhelp-from-the-gallery"></a><span data-ttu-id="42a43-123">Dodawanie QuickHelp z galerii</span><span class="sxs-lookup"><span data-stu-id="42a43-123">Adding QuickHelp from the gallery</span></span>
<span data-ttu-id="42a43-124">Aby skonfigurować integrację usługi Azure AD QuickHelp, należy dodać QuickHelp z galerii do listy zarządzanych aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="42a43-124">To configure the integration of QuickHelp into Azure AD, you need to add QuickHelp from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="42a43-125">**Aby dodać QuickHelp z galerii, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="42a43-125">**To add QuickHelp from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="42a43-126">W  **[portalu Azure](https://portal.azure.com)**, na panelu nawigacyjnym po lewej stronie kliknij **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="42a43-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Usługa Active Directory][1]

2. <span data-ttu-id="42a43-128">Przejdź do **aplikacje dla przedsiębiorstw**.</span><span class="sxs-lookup"><span data-stu-id="42a43-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="42a43-129">Następnie przejdź do **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="42a43-129">Then go to **All applications**.</span></span>

    ![Aplikacje][2]
    
3. <span data-ttu-id="42a43-131">Aby dodać nową aplikację, kliknij przycisk **nowej aplikacji** przycisk w górnej części okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="42a43-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Aplikacje][3]

4. <span data-ttu-id="42a43-133">W polu wyszukiwania wpisz **QuickHelp**.</span><span class="sxs-lookup"><span data-stu-id="42a43-133">In the search box, type **QuickHelp**.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-quickhelp-tutorial/tutorial_quickhelp_search.png)

5. <span data-ttu-id="42a43-135">W panelu wyników wybierz **QuickHelp**, a następnie kliknij przycisk **Dodaj** przycisk, aby dodać aplikację.</span><span class="sxs-lookup"><span data-stu-id="42a43-135">In the results panel, select **QuickHelp**, and then click **Add** button to add the application.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-quickhelp-tutorial/tutorial_quickhelp_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="42a43-137">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="42a43-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="42a43-138">W tej sekcji skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z QuickHelp w oparciu o nazwie "Britta Simona" użytkownika testowego.</span><span class="sxs-lookup"><span data-stu-id="42a43-138">In this section, you configure and test Azure AD single sign-on with QuickHelp based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="42a43-139">Dla rejestracji jednokrotnej do pracy usługi Azure AD musi wiedzieć, użytkownik odpowiednika w QuickHelp jest dla użytkownika, w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="42a43-139">For single sign-on to work, Azure AD needs to know what the counterpart user in QuickHelp is to a user in Azure AD.</span></span> <span data-ttu-id="42a43-140">Innymi słowy link relację między użytkownikiem usługi Azure AD i danemu użytkownikowi w QuickHelp musi się.</span><span class="sxs-lookup"><span data-stu-id="42a43-140">In other words, a link relationship between an Azure AD user and the related user in QuickHelp needs to be established.</span></span>

<span data-ttu-id="42a43-141">W QuickHelp, należy przypisać wartość **nazwy użytkownika** w usłudze Azure AD jako wartość **Username** do ustanawiania relacji łącza.</span><span class="sxs-lookup"><span data-stu-id="42a43-141">In QuickHelp, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="42a43-142">Aby skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z QuickHelp, należy wykonać poniższe bloki konstrukcyjne:</span><span class="sxs-lookup"><span data-stu-id="42a43-142">To configure and test Azure AD single sign-on with QuickHelp, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="42a43-143">**[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configuring-azure-ad-single-sign-on)**  — aby umożliwić użytkownikom korzystać z tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="42a43-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="42a43-144">**[Tworzenie użytkownika testowego usługi Azure AD](#creating-an-azure-ad-test-user)**  — do przetestowania usługi Azure AD rejestracji jednokrotnej z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="42a43-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="42a43-145">**[Tworzenie użytkownika testowego QuickHelp](#creating-a-quickhelp-test-user)**  — w celu zapewnienia odpowiednikiem Simona Britta QuickHelp połączonego z usługi Azure AD reprezentację użytkownika.</span><span class="sxs-lookup"><span data-stu-id="42a43-145">**[Creating a QuickHelp test user](#creating-a-quickhelp-test-user)** - to have a counterpart of Britta Simon in QuickHelp that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="42a43-146">**[Przypisanie użytkownika testowego usługi Azure AD](#assigning-the-azure-ad-test-user)**  — aby umożliwić Simona Britta do użycia usługi Azure AD rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="42a43-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="42a43-147">**[Testowanie rejestracji jednokrotnej](#testing-single-sign-on)**  — Aby sprawdzić, czy konfiguracja działa.</span><span class="sxs-lookup"><span data-stu-id="42a43-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="42a43-148">Konfigurowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="42a43-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="42a43-149">W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w portalu Azure i skonfigurować logowanie jednokrotne w aplikacji QuickHelp.</span><span class="sxs-lookup"><span data-stu-id="42a43-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your QuickHelp application.</span></span>

<span data-ttu-id="42a43-150">**Aby skonfigurować usługi Azure AD rejestracji jednokrotnej z QuickHelp, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="42a43-150">**To configure Azure AD single sign-on with QuickHelp, perform the following steps:**</span></span>

1. <span data-ttu-id="42a43-151">W portalu Azure na **QuickHelp** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.</span><span class="sxs-lookup"><span data-stu-id="42a43-151">In the Azure portal, on the **QuickHelp** application integration page, click **Single sign-on**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej][4]

2. <span data-ttu-id="42a43-153">Na **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** Aby włączyć logowanie jednokrotne.</span><span class="sxs-lookup"><span data-stu-id="42a43-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-quickhelp-tutorial/tutorial_quickhelp_samlbase.png)

3. <span data-ttu-id="42a43-155">Na **QuickHelp domeny i adres URL** sekcji, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="42a43-155">On the **QuickHelp Domain and URLs** section, perform the following steps:</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-quickhelp-tutorial/tutorial_quickhelp_url.png)

    <span data-ttu-id="42a43-157">a.</span><span class="sxs-lookup"><span data-stu-id="42a43-157">a.</span></span> <span data-ttu-id="42a43-158">W **adres URL logowania** tekstowym, wpisz adres URL, używając następującego wzorca:`https://quickhelp.com/<instancename>/#/Login`</span><span class="sxs-lookup"><span data-stu-id="42a43-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://quickhelp.com/<instancename>/#/Login`</span></span>

    <span data-ttu-id="42a43-159">b.</span><span class="sxs-lookup"><span data-stu-id="42a43-159">b.</span></span> <span data-ttu-id="42a43-160">W **identyfikator** tekstowym, wpisz adres URL, używając następującego wzorca:`https://<subdomain>.quickhelp.com`</span><span class="sxs-lookup"><span data-stu-id="42a43-160">In the **Identifier** textbox, type a URL using the following pattern: `https://<subdomain>.quickhelp.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="42a43-161">Wartości te nie są prawdziwe.</span><span class="sxs-lookup"><span data-stu-id="42a43-161">These values are not real.</span></span> <span data-ttu-id="42a43-162">Rzeczywisty adres URL logowania i identyfikator, należy zaktualizować te wartości.</span><span class="sxs-lookup"><span data-stu-id="42a43-162">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="42a43-163">Skontaktuj się z [zespołem pomocy technicznej klienta QuickHelp](https://support.quickhelp.com/) uzyskać te wartości.</span><span class="sxs-lookup"><span data-stu-id="42a43-163">Contact [QuickHelp Client support team](https://support.quickhelp.com/) to get these values.</span></span> 
 
4. <span data-ttu-id="42a43-164">Na **certyfikat podpisywania SAML** kliknij **XML metadanych** , a następnie zapisz plik metadanych na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="42a43-164">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-quickhelp-tutorial/tutorial_quickhelp_certificate.png) 

5. <span data-ttu-id="42a43-166">Kliknij przycisk **zapisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="42a43-166">Click **Save** button.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-quickhelp-tutorial/tutorial_general_400.png) 

6. <span data-ttu-id="42a43-168">Logowanie do witryny firmy QuickHelp jako administrator.</span><span class="sxs-lookup"><span data-stu-id="42a43-168">Sign-on to your QuickHelp company site as administrator.</span></span>

7. <span data-ttu-id="42a43-169">W menu u góry kliknij **Admin**.</span><span class="sxs-lookup"><span data-stu-id="42a43-169">In the menu on the top, click **Admin**.</span></span>
   
    ![Konfigurowanie rejestracji jednokrotnej][21]

8. <span data-ttu-id="42a43-171">W **QuickHelp Admin** menu, kliknij przycisk **ustawienia**.</span><span class="sxs-lookup"><span data-stu-id="42a43-171">In the **QuickHelp Admin** menu, click **Settings**.</span></span>
   
    ![Konfigurowanie rejestracji jednokrotnej][22]

9. <span data-ttu-id="42a43-173">Kliknij przycisk **ustawienia uwierzytelniania**.</span><span class="sxs-lookup"><span data-stu-id="42a43-173">Click **Authentication Settings**.</span></span>

10. <span data-ttu-id="42a43-174">Na **ustawienia uwierzytelniania** wykonaj następujące czynności</span><span class="sxs-lookup"><span data-stu-id="42a43-174">On the **Authentication Settings** page, perform the following steps</span></span>
   
    ![Konfigurowanie rejestracji jednokrotnej][23]
   
    <span data-ttu-id="42a43-176">a.</span><span class="sxs-lookup"><span data-stu-id="42a43-176">a.</span></span> <span data-ttu-id="42a43-177">Jako **typ logowania jednokrotnego**, wybierz pozycję **WSFederation**.</span><span class="sxs-lookup"><span data-stu-id="42a43-177">As **SSO Type**, select **WSFederation**.</span></span>
   
    <span data-ttu-id="42a43-178">b.</span><span class="sxs-lookup"><span data-stu-id="42a43-178">b.</span></span> <span data-ttu-id="42a43-179">Aby przekazać plik pobrany metadanych platformy Azure, kliknij przycisk **Przeglądaj**, przejdź do pliku, następnie kliknij przycisk Zakończ **przekazać metadanych**.</span><span class="sxs-lookup"><span data-stu-id="42a43-179">To upload your downloaded Azure metadata file, click **Browse**, navigate to the file, end then click **Upload Metadata**.</span></span>
   
    <span data-ttu-id="42a43-180">c.</span><span class="sxs-lookup"><span data-stu-id="42a43-180">c.</span></span> <span data-ttu-id="42a43-181">W **E-mail** pole tekstowe, typ `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress`.</span><span class="sxs-lookup"><span data-stu-id="42a43-181">In the **Email** textbox, type `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress`.</span></span>
   
    <span data-ttu-id="42a43-182">d.</span><span class="sxs-lookup"><span data-stu-id="42a43-182">d.</span></span> <span data-ttu-id="42a43-183">W **imię** pole tekstowe, `type http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname`.</span><span class="sxs-lookup"><span data-stu-id="42a43-183">In the **First Name** textbox, `type http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname`.</span></span>
   
    <span data-ttu-id="42a43-184">e.</span><span class="sxs-lookup"><span data-stu-id="42a43-184">e.</span></span> <span data-ttu-id="42a43-185">W **nazwisko** pole tekstowe, `type http://schemas.xmlsoap.org/ws/2005/05/identity/claims/surname`.</span><span class="sxs-lookup"><span data-stu-id="42a43-185">In the **Last Name** textbox, `type http://schemas.xmlsoap.org/ws/2005/05/identity/claims/surname`.</span></span>
   
    <span data-ttu-id="42a43-186">f.</span><span class="sxs-lookup"><span data-stu-id="42a43-186">f.</span></span> <span data-ttu-id="42a43-187">W **pasku akcji**, kliknij przycisk **zapisać**.</span><span class="sxs-lookup"><span data-stu-id="42a43-187">In the **Action Bar**, click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="42a43-188">Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji!</span><span class="sxs-lookup"><span data-stu-id="42a43-188">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="42a43-189">Po dodaniu tej aplikacji z **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij **rejestracji jednokrotnej** karcie i dostęp do dokumentacji osadzonych za pomocą **konfiguracji** sekcji u dołu.</span><span class="sxs-lookup"><span data-stu-id="42a43-189">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="42a43-190">Więcej o funkcji dokumentacji osadzonego w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="42a43-190">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="42a43-191">Tworzenie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="42a43-191">Creating an Azure AD test user</span></span>
<span data-ttu-id="42a43-192">Celem tej sekcji jest tworzenie użytkownika testowego w portalu Azure o nazwie Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="42a43-192">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Tworzenie użytkowników usługi Azure AD][100]

<span data-ttu-id="42a43-194">**Aby utworzyć użytkownika testowego w usłudze Azure AD, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="42a43-194">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="42a43-195">W **portalu Azure**, w lewym okienku nawigacji, kliknij polecenie **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="42a43-195">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-quickhelp-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="42a43-197">Aby wyświetlić listę użytkowników, przejdź do **użytkowników i grup** i kliknij przycisk **wszyscy użytkownicy**.</span><span class="sxs-lookup"><span data-stu-id="42a43-197">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-quickhelp-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="42a43-199">Aby otworzyć **użytkownika** okna dialogowego, kliknij przycisk **Dodaj** górnej części okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="42a43-199">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-quickhelp-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="42a43-201">Na **użytkownika** okna dialogowego strony, należy wykonać następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="42a43-201">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-quickhelp-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="42a43-203">a.</span><span class="sxs-lookup"><span data-stu-id="42a43-203">a.</span></span> <span data-ttu-id="42a43-204">W **nazwa** pole tekstowe, typ **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="42a43-204">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="42a43-205">b.</span><span class="sxs-lookup"><span data-stu-id="42a43-205">b.</span></span> <span data-ttu-id="42a43-206">W **nazwy użytkownika** pole tekstowe, typ **adres e-mail** z BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="42a43-206">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="42a43-207">c.</span><span class="sxs-lookup"><span data-stu-id="42a43-207">c.</span></span> <span data-ttu-id="42a43-208">Wybierz **Pokaż hasło** i zanotuj wartość **hasło**.</span><span class="sxs-lookup"><span data-stu-id="42a43-208">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="42a43-209">d.</span><span class="sxs-lookup"><span data-stu-id="42a43-209">d.</span></span> <span data-ttu-id="42a43-210">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="42a43-210">Click **Create**.</span></span>
 
### <a name="creating-a-quickhelp-test-user"></a><span data-ttu-id="42a43-211">Tworzenie użytkownika testowego QuickHelp</span><span class="sxs-lookup"><span data-stu-id="42a43-211">Creating a QuickHelp test user</span></span>

<span data-ttu-id="42a43-212">Celem tej sekcji jest utworzenie użytkownika o nazwie Simona Britta w QuickHelp.</span><span class="sxs-lookup"><span data-stu-id="42a43-212">The objective of this section is to create a user called Britta Simon in QuickHelp.</span></span>
<span data-ttu-id="42a43-213">Dla rejestracji jednokrotnej do pracy usługi Azure AD musi wiedzieć, co to jest odpowiednikiem użytkownikowi w QuickHelp użytkownika w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="42a43-213">For single sign-on to work, Azure AD needs to know what the counterpart user in QuickHelp to a user in Azure AD is.</span></span> <span data-ttu-id="42a43-214">Innymi słowy link relację między użytkownikiem usługi Azure AD i danemu użytkownikowi w QuickHelp musi się.</span><span class="sxs-lookup"><span data-stu-id="42a43-214">In other words, a link relationship between an Azure AD user and the related user in QuickHelp needs to be established.</span></span>

<span data-ttu-id="42a43-215">QuickHelp obsługę w czasie.</span><span class="sxs-lookup"><span data-stu-id="42a43-215">QuickHelp supports just-in-time provisioning.</span></span> <span data-ttu-id="42a43-216">Oznacza to, jeśli to konieczne, konto użytkownika jest automatycznie tworzony w QuickHelp i konto jest połączony z kontem usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="42a43-216">This means, if necessary, a user account is automatically created in QuickHelp and the account is linked to the Azure AD account.</span></span>

<span data-ttu-id="42a43-217">Nie ma elementu akcji można w tej sekcji.</span><span class="sxs-lookup"><span data-stu-id="42a43-217">There is no action item for you in this section.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="42a43-218">Przypisanie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="42a43-218">Assigning the Azure AD test user</span></span>

<span data-ttu-id="42a43-219">W tej sekcji można włączyć Simona Britta do używania Azure logowania jednokrotnego za udzielanie dostępu QuickHelp.</span><span class="sxs-lookup"><span data-stu-id="42a43-219">In this section, you enable Britta Simon to use Azure single sign-on by granting access to QuickHelp.</span></span>

![Przypisz użytkownika][200] 

<span data-ttu-id="42a43-221">**Aby przypisać Simona Britta QuickHelp, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="42a43-221">**To assign Britta Simon to QuickHelp, perform the following steps:**</span></span>

1. <span data-ttu-id="42a43-222">W portalu Azure Otwórz widok aplikacji, a następnie przejdź do widoku katalogu i przejdź do **aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="42a43-222">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Przypisz użytkownika][201] 

2. <span data-ttu-id="42a43-224">Na liście aplikacji zaznacz **QuickHelp**.</span><span class="sxs-lookup"><span data-stu-id="42a43-224">In the applications list, select **QuickHelp**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-quickhelp-tutorial/tutorial_quickhelp_app.png) 

3. <span data-ttu-id="42a43-226">W menu po lewej stronie kliknij **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="42a43-226">In the menu on the left, click **Users and groups**.</span></span>

    ![Przypisz użytkownika][202] 

4. <span data-ttu-id="42a43-228">Kliknij przycisk **Dodaj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="42a43-228">Click **Add** button.</span></span> <span data-ttu-id="42a43-229">Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="42a43-229">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Przypisz użytkownika][203]

5. <span data-ttu-id="42a43-231">Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** na liście Użytkownicy.</span><span class="sxs-lookup"><span data-stu-id="42a43-231">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="42a43-232">Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="42a43-232">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="42a43-233">Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="42a43-233">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="42a43-234">Testowanie rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="42a43-234">Testing single sign-on</span></span>

<span data-ttu-id="42a43-235">Celem tej sekcji służy do testowania konfiguracji usługi Azure AD pojedynczego logowania za pomocą panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="42a43-235">The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.</span></span>  

<span data-ttu-id="42a43-236">Po kliknięciu kafelka QuickHelp w panelu dostępu użytkownik powinien pobrać automatycznie zalogowane do aplikacji QuickHelp.</span><span class="sxs-lookup"><span data-stu-id="42a43-236">When you click the QuickHelp tile in the Access Panel, you should get automatically signed-on to your QuickHelp application.</span></span>


## <a name="additional-resources"></a><span data-ttu-id="42a43-237">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="42a43-237">Additional resources</span></span>

* [<span data-ttu-id="42a43-238">Lista samouczków dotyczących sposobów integracji aplikacji SaaS przy użyciu usługi Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="42a43-238">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="42a43-239">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="42a43-239">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-quickhelp-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-quickhelp-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-quickhelp-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-quickhelp-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-quickhelp-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-quickhelp-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-quickhelp-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-quickhelp-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-quickhelp-tutorial/tutorial_general_203.png
[21]: ./media/active-directory-saas-quickhelp-tutorial/tutorial_quickhelp_05.png
[22]: ./media/active-directory-saas-quickhelp-tutorial/tutorial_quickhelp_06.png
[23]: ./media/active-directory-saas-quickhelp-tutorial/tutorial_quickhelp_07.png
