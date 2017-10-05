---
title: 'Samouczek: Integracji Azure Active Directory z Jobscience | Dokumentacja firmy Microsoft'
description: "Informacje o sposobie konfigurowania rejestracji jednokrotnej między usługą Azure Active Directory i Jobscience."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 77282dcc-bbe2-4728-953d-adb4ab6a713b
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: jeedes
ms.openlocfilehash: 66bec35a8f17482433dbf02827b90620d1cff378
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-jobscience"></a><span data-ttu-id="0a247-103">Samouczek: Integracji Azure Active Directory z Jobscience</span><span class="sxs-lookup"><span data-stu-id="0a247-103">Tutorial: Azure Active Directory integration with Jobscience</span></span>

<span data-ttu-id="0a247-104">Z tego samouczka dowiesz się integrowanie Jobscience z usługi Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="0a247-104">In this tutorial, you learn how to integrate Jobscience with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="0a247-105">Integracja z usługą Azure AD Jobscience zapewnia następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="0a247-105">Integrating Jobscience with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="0a247-106">Można kontrolować w usłudze Azure AD, który ma dostęp do Jobscience</span><span class="sxs-lookup"><span data-stu-id="0a247-106">You can control in Azure AD who has access to Jobscience</span></span>
- <span data-ttu-id="0a247-107">Umożliwia użytkownikom automatycznie pobrać zalogowane do Jobscience (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="0a247-107">You can enable your users to automatically get signed-on to Jobscience (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="0a247-108">Możesz zarządzać kont w jednej centralnej lokalizacji - portalu Azure</span><span class="sxs-lookup"><span data-stu-id="0a247-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="0a247-109">Jeśli chcesz dowiedzieć się więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="0a247-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="0a247-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="0a247-110">Prerequisites</span></span>

<span data-ttu-id="0a247-111">Aby skonfigurować integrację usługi Azure AD z Jobscience, potrzebne są następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="0a247-111">To configure Azure AD integration with Jobscience, you need the following items:</span></span>

- <span data-ttu-id="0a247-112">Subskrypcję usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="0a247-112">An Azure AD subscription</span></span>
- <span data-ttu-id="0a247-113">Jobscience logowanie jednokrotne włączone subskrypcji</span><span class="sxs-lookup"><span data-stu-id="0a247-113">A Jobscience single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="0a247-114">Aby przetestować kroki opisane w tym samouczku, zaleca się używania środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="0a247-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="0a247-115">Aby przetestować kroki opisane w tym samouczku, należy wykonać te zalecenia:</span><span class="sxs-lookup"><span data-stu-id="0a247-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="0a247-116">Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="0a247-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="0a247-117">Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz pobrać miesięczna wersja próbna tutaj: [oferta wersji próbnej](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="0a247-117">If you don't have an Azure AD trial environment, you can get a one-month trial here: [Trial offer](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="0a247-118">Opis scenariusza</span><span class="sxs-lookup"><span data-stu-id="0a247-118">Scenario description</span></span>
<span data-ttu-id="0a247-119">W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym.</span><span class="sxs-lookup"><span data-stu-id="0a247-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="0a247-120">Scenariusz opisany w tym samouczku składa się z dwóch głównych elementów:</span><span class="sxs-lookup"><span data-stu-id="0a247-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="0a247-121">Dodawanie Jobscience z galerii</span><span class="sxs-lookup"><span data-stu-id="0a247-121">Adding Jobscience from the gallery</span></span>
2. <span data-ttu-id="0a247-122">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="0a247-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-jobscience-from-the-gallery"></a><span data-ttu-id="0a247-123">Dodawanie Jobscience z galerii</span><span class="sxs-lookup"><span data-stu-id="0a247-123">Adding Jobscience from the gallery</span></span>
<span data-ttu-id="0a247-124">Aby skonfigurować integrację usługi Azure AD Jobscience, należy dodać Jobscience z galerii do listy zarządzanych aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="0a247-124">To configure the integration of Jobscience into Azure AD, you need to add Jobscience from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="0a247-125">**Aby dodać Jobscience z galerii, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="0a247-125">**To add Jobscience from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="0a247-126">W  **[portalu Azure](https://portal.azure.com)**, na panelu nawigacyjnym po lewej stronie kliknij **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="0a247-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Usługa Active Directory][1]

2. <span data-ttu-id="0a247-128">Przejdź do **aplikacje dla przedsiębiorstw**.</span><span class="sxs-lookup"><span data-stu-id="0a247-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="0a247-129">Następnie przejdź do **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="0a247-129">Then go to **All applications**.</span></span>

    ![Aplikacje][2]
    
3. <span data-ttu-id="0a247-131">Aby dodać nową aplikację, kliknij przycisk **nowej aplikacji** przycisk w górnej części okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="0a247-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Aplikacje][3]

4. <span data-ttu-id="0a247-133">W polu wyszukiwania wpisz **Jobscience**.</span><span class="sxs-lookup"><span data-stu-id="0a247-133">In the search box, type **Jobscience**.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-jobscience-tutorial/tutorial_jobscience_search.png)

5. <span data-ttu-id="0a247-135">W panelu wyników wybierz **Jobscience**, a następnie kliknij przycisk **Dodaj** przycisk, aby dodać aplikację.</span><span class="sxs-lookup"><span data-stu-id="0a247-135">In the results panel, select **Jobscience**, and then click **Add** button to add the application.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-jobscience-tutorial/tutorial_jobscience_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="0a247-137">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="0a247-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="0a247-138">W tej sekcji możesz skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z Jobscience na podstawie użytkownika testowego, nazywany "Britta Simona".</span><span class="sxs-lookup"><span data-stu-id="0a247-138">In this section, you configure and test Azure AD single sign-on with Jobscience based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="0a247-139">Dla rejestracji jednokrotnej do pracy usługi Azure AD musi wiedzieć, użytkownik odpowiednika w Jobscience jest dla użytkownika, w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="0a247-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Jobscience is to a user in Azure AD.</span></span> <span data-ttu-id="0a247-140">Innymi słowy link relację między użytkownikiem usługi Azure AD i danemu użytkownikowi w Jobscience musi się.</span><span class="sxs-lookup"><span data-stu-id="0a247-140">In other words, a link relationship between an Azure AD user and the related user in Jobscience needs to be established.</span></span>

<span data-ttu-id="0a247-141">W Jobscience, należy przypisać wartość **nazwy użytkownika** w usłudze Azure AD jako wartość **Username** do ustanawiania relacji łącza.</span><span class="sxs-lookup"><span data-stu-id="0a247-141">In Jobscience, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="0a247-142">Aby skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z Jobscience, należy wykonać poniższe bloki konstrukcyjne:</span><span class="sxs-lookup"><span data-stu-id="0a247-142">To configure and test Azure AD single sign-on with Jobscience, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="0a247-143">**[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configuring-azure-ad-single-sign-on)**  — aby umożliwić użytkownikom korzystać z tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="0a247-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="0a247-144">**[Tworzenie użytkownika testowego usługi Azure AD](#creating-an-azure-ad-test-user)**  — do przetestowania usługi Azure AD rejestracji jednokrotnej z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="0a247-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="0a247-145">**[Tworzenie użytkownika testowego Jobscience](#creating-a-jobscience-test-user)**  — w celu zapewnienia odpowiednikiem Simona Britta Jobscience połączonego z usługi Azure AD reprezentację użytkownika.</span><span class="sxs-lookup"><span data-stu-id="0a247-145">**[Creating a Jobscience test user](#creating-a-jobscience-test-user)** - to have a counterpart of Britta Simon in Jobscience that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="0a247-146">**[Przypisanie użytkownika testowego usługi Azure AD](#assigning-the-azure-ad-test-user)**  — aby umożliwić Simona Britta do użycia usługi Azure AD rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="0a247-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="0a247-147">**[Testowanie rejestracji jednokrotnej](#testing-single-sign-on)**  — Aby sprawdzić, czy konfiguracja działa.</span><span class="sxs-lookup"><span data-stu-id="0a247-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="0a247-148">Konfigurowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="0a247-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="0a247-149">W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w portalu Azure i skonfigurować logowanie jednokrotne w aplikacji Jobscience.</span><span class="sxs-lookup"><span data-stu-id="0a247-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Jobscience application.</span></span>

<span data-ttu-id="0a247-150">**Aby skonfigurować usługi Azure AD rejestracji jednokrotnej z Jobscience, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="0a247-150">**To configure Azure AD single sign-on with Jobscience, perform the following steps:**</span></span>

1. <span data-ttu-id="0a247-151">W portalu Azure na **Jobscience** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.</span><span class="sxs-lookup"><span data-stu-id="0a247-151">In the Azure portal, on the **Jobscience** application integration page, click **Single sign-on**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej][4]

2. <span data-ttu-id="0a247-153">Na **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** Aby włączyć logowanie jednokrotne.</span><span class="sxs-lookup"><span data-stu-id="0a247-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-jobscience-tutorial/tutorial_jobscience_samlbase.png)

3. <span data-ttu-id="0a247-155">Na **Jobscience domeny i adres URL** sekcji, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="0a247-155">On the **Jobscience Domain and URLs** section, perform the following steps:</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-jobscience-tutorial/tutorial_jobscience_url.png)

    <span data-ttu-id="0a247-157">W **adres URL logowania** tekstowym, wpisz adres URL, używając następującego wzorca:`http://<company name>.my.salesforce.com`</span><span class="sxs-lookup"><span data-stu-id="0a247-157">In the **Sign-on URL** textbox, type a URL using the following pattern:  `http://<company name>.my.salesforce.com`</span></span>
    
    > [!NOTE] 
    > <span data-ttu-id="0a247-158">Ta wartość nie jest prawdziwe.</span><span class="sxs-lookup"><span data-stu-id="0a247-158">This value is not real.</span></span> <span data-ttu-id="0a247-159">Zaktualizuj tę wartość przy rzeczywisty adres URL logowania.</span><span class="sxs-lookup"><span data-stu-id="0a247-159">Update this value with the actual Sign-On URL.</span></span> <span data-ttu-id="0a247-160">Uzyskać tę wartość za pomocą [zespołem pomocy technicznej klienta Jobscience](https://www.jobscience.com/support) lub w profilu rejestracji Jednokrotnej zostanie utworzona, który znajduje się w dalszej części tego samouczka.</span><span class="sxs-lookup"><span data-stu-id="0a247-160">Get this value by [Jobscience Client support team](https://www.jobscience.com/support) or from the SSO profile you will create which is explained later in the tutorial.</span></span> 
 
4. <span data-ttu-id="0a247-161">Na **certyfikat podpisywania SAML** kliknij **certyfikatu (Base64)** , a następnie zapisz plik certyfikatu na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="0a247-161">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-jobscience-tutorial/tutorial_jobscience_certificate.png) 

5. <span data-ttu-id="0a247-163">Kliknij przycisk **zapisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="0a247-163">Click **Save** button.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-jobscience-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="0a247-165">Na **konfiguracji Jobscience** , kliknij przycisk **skonfigurować Jobscience** otworzyć **Konfigurowanie logowania jednokrotnego** okna.</span><span class="sxs-lookup"><span data-stu-id="0a247-165">On the **Jobscience Configuration** section, click **Configure Jobscience** to open **Configure sign-on** window.</span></span> <span data-ttu-id="0a247-166">Kopiuj **Sign-Out adres URL, identyfikator jednostki SAML i SAML pojedynczy znak na adres URL usługi** z **sekcji krótkimi opisami.**</span><span class="sxs-lookup"><span data-stu-id="0a247-166">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-jobscience-tutorial/tutorial_jobscience_configure.png) 

7. <span data-ttu-id="0a247-168">Zaloguj się do witryny firmy Jobscience jako administrator.</span><span class="sxs-lookup"><span data-stu-id="0a247-168">Log in to your Jobscience company site as an administrator.</span></span>

8. <span data-ttu-id="0a247-169">Przejdź do **Instalatora**.</span><span class="sxs-lookup"><span data-stu-id="0a247-169">Go to **Setup**.</span></span>
   
   <span data-ttu-id="0a247-170">![Instalator](./media/active-directory-saas-jobscience-tutorial/IC784358.png "Instalatora")</span><span class="sxs-lookup"><span data-stu-id="0a247-170">![Setup](./media/active-directory-saas-jobscience-tutorial/IC784358.png "Setup")</span></span>

9. <span data-ttu-id="0a247-171">W okienku nawigacji po lewej stronie w **Administruj** , kliknij przycisk **Zarządzanie domenami** rozwiń sekcję powiązane, a następnie kliknij przycisk **Moje domeny** otworzyć **Moje domeny** strony.</span><span class="sxs-lookup"><span data-stu-id="0a247-171">On the left navigation pane, in the **Administer** section, click **Domain Management** to expand the related section, and then click **My Domain** to open the **My Domain** page.</span></span> 
   
   <span data-ttu-id="0a247-172">![Mojej domeny](./media/active-directory-saas-jobscience-tutorial/ic767825.png "mojej domeny")</span><span class="sxs-lookup"><span data-stu-id="0a247-172">![My Domain](./media/active-directory-saas-jobscience-tutorial/ic767825.png "My Domain")</span></span>

10. <span data-ttu-id="0a247-173">Aby sprawdzić, czy domeny nie został skonfigurowany prawidłowo, upewnij się, że jest on "**krok 4 wdrożone dla użytkowników**" i zapoznaj się z "**Moje ustawienia domeny**".</span><span class="sxs-lookup"><span data-stu-id="0a247-173">To verify that your domain has been set up correctly, make sure that it is in “**Step 4 Deployed to Users**” and review your “**My Domain Settings**”.</span></span>

    <span data-ttu-id="0a247-174">![Wdrożonego dla użytkownika domeny](./media/active-directory-saas-jobscience-tutorial/ic784377.png "wdrożonego dla użytkownika domeny")</span><span class="sxs-lookup"><span data-stu-id="0a247-174">![Domain Deployed to User](./media/active-directory-saas-jobscience-tutorial/ic784377.png "Domain Deployed to User")</span></span>

11. <span data-ttu-id="0a247-175">W witrynie firmy Jobscience kliknij przycisk **kontroli bezpieczeństwa**, a następnie kliknij przycisk **ustawień rejestracji jednokrotnej**.</span><span class="sxs-lookup"><span data-stu-id="0a247-175">On the Jobscience company site, click **Security Controls**, and then click **Single Sign-On Settings**.</span></span>
    
    <span data-ttu-id="0a247-176">![Opcje zabezpieczeń](./media/active-directory-saas-jobscience-tutorial/ic784364.png "środki zabezpieczające.")</span><span class="sxs-lookup"><span data-stu-id="0a247-176">![Security Controls](./media/active-directory-saas-jobscience-tutorial/ic784364.png "Security Controls")</span></span>

12. <span data-ttu-id="0a247-177">W **ustawień rejestracji jednokrotnej** sekcji, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="0a247-177">In the **Single Sign-On Settings** section, perform the following steps:</span></span>
    
    <span data-ttu-id="0a247-178">![Single Sign-On ustawienia](./media/active-directory-saas-jobscience-tutorial/ic781026.png "Single Sign-On ustawienia")</span><span class="sxs-lookup"><span data-stu-id="0a247-178">![Single Sign-On Settings](./media/active-directory-saas-jobscience-tutorial/ic781026.png "Single Sign-On Settings")</span></span>
    
    <span data-ttu-id="0a247-179">a.</span><span class="sxs-lookup"><span data-stu-id="0a247-179">a.</span></span> <span data-ttu-id="0a247-180">Wybierz **SAML włączone**.</span><span class="sxs-lookup"><span data-stu-id="0a247-180">Select **SAML Enabled**.</span></span>

    <span data-ttu-id="0a247-181">b.</span><span class="sxs-lookup"><span data-stu-id="0a247-181">b.</span></span> <span data-ttu-id="0a247-182">Kliknij przycisk **Nowy**.</span><span class="sxs-lookup"><span data-stu-id="0a247-182">Click **New**.</span></span>

13. <span data-ttu-id="0a247-183">Na **SAML pojedynczego logowania jednokrotnego ustawienie Edytuj** okna dialogowego, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="0a247-183">On the **SAML Single Sign-On Setting Edit** dialog, perform the following steps:</span></span>
    
    <span data-ttu-id="0a247-184">![SAML pojedynczy znak na ustawienie](./media/active-directory-saas-jobscience-tutorial/ic784365.png "SAML pojedynczy znak na ustawienie")</span><span class="sxs-lookup"><span data-stu-id="0a247-184">![SAML Single Sign-On Setting](./media/active-directory-saas-jobscience-tutorial/ic784365.png "SAML Single Sign-On Setting")</span></span>
    
    <span data-ttu-id="0a247-185">a.</span><span class="sxs-lookup"><span data-stu-id="0a247-185">a.</span></span> <span data-ttu-id="0a247-186">W **nazwa** tekstowym, wpisz nazwę dla danej konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="0a247-186">In the **Name** textbox, type a name for your configuration.</span></span>

    <span data-ttu-id="0a247-187">b.</span><span class="sxs-lookup"><span data-stu-id="0a247-187">b.</span></span> <span data-ttu-id="0a247-188">W **wystawcy** pole tekstowe, Wklej wartość **identyfikator jednostki SAML**, które zostały skopiowane z portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="0a247-188">In **Issuer** textbox, paste the value of **SAML Entity ID**, which you have copied from Azure portal.</span></span>

    <span data-ttu-id="0a247-189">c.</span><span class="sxs-lookup"><span data-stu-id="0a247-189">c.</span></span> <span data-ttu-id="0a247-190">W **identyfikator jednostki** pole tekstowe, typ`https://salesforce-jobscience.com`</span><span class="sxs-lookup"><span data-stu-id="0a247-190">In the **Entity Id** textbox, type `https://salesforce-jobscience.com`</span></span>

    <span data-ttu-id="0a247-191">d.</span><span class="sxs-lookup"><span data-stu-id="0a247-191">d.</span></span> <span data-ttu-id="0a247-192">Kliknij przycisk **Przeglądaj** można przekazać certyfikatu usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="0a247-192">Click **Browse** to upload your Azure AD certificate.</span></span>

    <span data-ttu-id="0a247-193">e.</span><span class="sxs-lookup"><span data-stu-id="0a247-193">e.</span></span> <span data-ttu-id="0a247-194">Jako **typ tożsamości SAML**, wybierz pozycję **potwierdzenia zawiera identyfikator federacji z obiektu użytkownika**.</span><span class="sxs-lookup"><span data-stu-id="0a247-194">As **SAML Identity Type**, select **Assertion contains the Federation ID from the User object**.</span></span>

    <span data-ttu-id="0a247-195">f.</span><span class="sxs-lookup"><span data-stu-id="0a247-195">f.</span></span> <span data-ttu-id="0a247-196">Jako **lokalizacji tożsamości SAML**, wybierz pozycję **jest tożsamość w elemencie NameIdentfier instrukcji podmiotu**.</span><span class="sxs-lookup"><span data-stu-id="0a247-196">As **SAML Identity Location**, select **Identity is in the NameIdentfier element of the Subject statement**.</span></span>

    <span data-ttu-id="0a247-197">g.</span><span class="sxs-lookup"><span data-stu-id="0a247-197">g.</span></span> <span data-ttu-id="0a247-198">W **adresu URL logowania do dostawcy tożsamości** pole tekstowe, Wklej wartość **SAML pojedynczy znak na adres URL usługi**, które zostały skopiowane z portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="0a247-198">In **Identity Provider Login URL** textbox, paste the value of **SAML Single Sign-On Service URL**, which you have copied from Azure portal.</span></span>

    <span data-ttu-id="0a247-199">h.</span><span class="sxs-lookup"><span data-stu-id="0a247-199">h.</span></span> <span data-ttu-id="0a247-200">W **adres URL wylogowania dostawcy tożsamości** pole tekstowe, Wklej wartość **Sign-Out adres URL**, które zostały skopiowane z portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="0a247-200">In **Identity Provider Logout URL** textbox, paste the value of **Sign-Out URL**, which you have copied from Azure portal.</span></span>

    <span data-ttu-id="0a247-201">i.</span><span class="sxs-lookup"><span data-stu-id="0a247-201">i.</span></span> <span data-ttu-id="0a247-202">Kliknij pozycję **Zapisz**.</span><span class="sxs-lookup"><span data-stu-id="0a247-202">Click **Save**.</span></span>

14. <span data-ttu-id="0a247-203">W okienku nawigacji po lewej stronie w **Administruj** , kliknij przycisk **Zarządzanie domenami** rozwiń sekcję powiązane, a następnie kliknij przycisk **Moje domeny** otworzyć **Moje domeny** strony.</span><span class="sxs-lookup"><span data-stu-id="0a247-203">On the left navigation pane, in the **Administer** section, click **Domain Management** to expand the related section, and then click **My Domain** to open the **My Domain** page.</span></span> 
    
    <span data-ttu-id="0a247-204">![Mojej domeny](./media/active-directory-saas-jobscience-tutorial/ic767825.png "mojej domeny")</span><span class="sxs-lookup"><span data-stu-id="0a247-204">![My Domain](./media/active-directory-saas-jobscience-tutorial/ic767825.png "My Domain")</span></span>

15. <span data-ttu-id="0a247-205">Na **Moje domeny** strony w **znakowanie strony logowania** kliknij **Edytuj**.</span><span class="sxs-lookup"><span data-stu-id="0a247-205">On the **My Domain** page, in the **Login Page Branding** section, click **Edit**.</span></span>
    
    <span data-ttu-id="0a247-206">![Znakowanie strony logowania](./media/active-directory-saas-jobscience-tutorial/ic767826.png "znakowanie strony logowania")</span><span class="sxs-lookup"><span data-stu-id="0a247-206">![Login Page Branding](./media/active-directory-saas-jobscience-tutorial/ic767826.png "Login Page Branding")</span></span>

16. <span data-ttu-id="0a247-207">Na **znakowanie strony logowania** strony w **usługi uwierzytelniania** sekcji Nazwa Twojej **ustawienia logowania jednokrotnego SAML** jest wyświetlany.</span><span class="sxs-lookup"><span data-stu-id="0a247-207">On the **Login Page Branding** page, in the **Authentication Service** section, the name of your **SAML SSO Settings** is displayed.</span></span> <span data-ttu-id="0a247-208">Wybierz go, a następnie kliknij przycisk **zapisać**.</span><span class="sxs-lookup"><span data-stu-id="0a247-208">Select it, and then click **Save**.</span></span>
    
    <span data-ttu-id="0a247-209">![Znakowanie strony logowania](./media/active-directory-saas-jobscience-tutorial/ic784366.png "znakowanie strony logowania")</span><span class="sxs-lookup"><span data-stu-id="0a247-209">![Login Page Branding](./media/active-directory-saas-jobscience-tutorial/ic784366.png "Login Page Branding")</span></span>

17. <span data-ttu-id="0a247-210">Aby uzyskać PS zainicjować funkcji logowania jednokrotnego kliknij adres URL logowania na **ustawień rejestracji jednokrotnej** w **kontroli bezpieczeństwa** części menu.</span><span class="sxs-lookup"><span data-stu-id="0a247-210">To get the SP initiated Single Sign on Login URL click on the **Single Sign On settings** in the **Security Controls** menu section.</span></span>

    <span data-ttu-id="0a247-211">![Opcje zabezpieczeń](./media/active-directory-saas-jobscience-tutorial/ic784368.png "środki zabezpieczające.")</span><span class="sxs-lookup"><span data-stu-id="0a247-211">![Security Controls](./media/active-directory-saas-jobscience-tutorial/ic784368.png "Security Controls")</span></span>
    
    <span data-ttu-id="0a247-212">Kliknij profil rejestracji Jednokrotnej, utworzony w poprzednim kroku.</span><span class="sxs-lookup"><span data-stu-id="0a247-212">Click the SSO profile you have created in the step above.</span></span> <span data-ttu-id="0a247-213">Ta strona zawiera rejestracji jednokrotnej na adres URL dla Twojej firmy (na przykład [https://companyname.my.salesforce.com?so=companyid](https://companyname.my.salesforce.com?so=companyid).</span><span class="sxs-lookup"><span data-stu-id="0a247-213">This page shows the Single Sign on URL for your company (for example, [https://companyname.my.salesforce.com?so=companyid](https://companyname.my.salesforce.com?so=companyid).</span></span>    

> [!TIP]
> <span data-ttu-id="0a247-214">Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji!</span><span class="sxs-lookup"><span data-stu-id="0a247-214">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="0a247-215">Po dodaniu tej aplikacji z **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij **rejestracji jednokrotnej** karcie i dostęp do dokumentacji osadzonych za pomocą **konfiguracji** sekcji u dołu.</span><span class="sxs-lookup"><span data-stu-id="0a247-215">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="0a247-216">Więcej o funkcji dokumentacji osadzonego w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="0a247-216">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="0a247-217">Tworzenie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="0a247-217">Creating an Azure AD test user</span></span>
<span data-ttu-id="0a247-218">Celem tej sekcji jest tworzenie użytkownika testowego w portalu Azure o nazwie Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="0a247-218">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Tworzenie użytkowników usługi Azure AD][100]

<span data-ttu-id="0a247-220">**Aby utworzyć użytkownika testowego w usłudze Azure AD, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="0a247-220">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="0a247-221">W **portalu Azure**, w lewym okienku nawigacji, kliknij polecenie **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="0a247-221">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-jobscience-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="0a247-223">Aby wyświetlić listę użytkowników, przejdź do **użytkowników i grup** i kliknij przycisk **wszyscy użytkownicy**.</span><span class="sxs-lookup"><span data-stu-id="0a247-223">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-jobscience-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="0a247-225">Aby otworzyć **użytkownika** okna dialogowego, kliknij przycisk **Dodaj** górnej części okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="0a247-225">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-jobscience-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="0a247-227">Na **użytkownika** okna dialogowego strony, należy wykonać następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="0a247-227">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-jobscience-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="0a247-229">a.</span><span class="sxs-lookup"><span data-stu-id="0a247-229">a.</span></span> <span data-ttu-id="0a247-230">W **nazwa** pole tekstowe, typ **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="0a247-230">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="0a247-231">b.</span><span class="sxs-lookup"><span data-stu-id="0a247-231">b.</span></span> <span data-ttu-id="0a247-232">W **nazwy użytkownika** pole tekstowe, typ **adres e-mail** z BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="0a247-232">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="0a247-233">c.</span><span class="sxs-lookup"><span data-stu-id="0a247-233">c.</span></span> <span data-ttu-id="0a247-234">Wybierz **Pokaż hasło** i zanotuj wartość **hasło**.</span><span class="sxs-lookup"><span data-stu-id="0a247-234">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="0a247-235">d.</span><span class="sxs-lookup"><span data-stu-id="0a247-235">d.</span></span> <span data-ttu-id="0a247-236">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="0a247-236">Click **Create**.</span></span>
 
### <a name="creating-a-jobscience-test-user"></a><span data-ttu-id="0a247-237">Tworzenie użytkownika testowego Jobscience</span><span class="sxs-lookup"><span data-stu-id="0a247-237">Creating a Jobscience test user</span></span>

<span data-ttu-id="0a247-238">Aby umożliwić użytkownikom zalogować się do Jobscience usługi Azure AD, musi być przygotowana do Jobscience.</span><span class="sxs-lookup"><span data-stu-id="0a247-238">In order to enable Azure AD users to log in to Jobscience, they must be provisioned into Jobscience.</span></span> <span data-ttu-id="0a247-239">W przypadku Jobscience Inicjowanie obsługi to zadanie ręczne.</span><span class="sxs-lookup"><span data-stu-id="0a247-239">In the case of Jobscience, provisioning is a manual task.</span></span>

>[!NOTE]
><span data-ttu-id="0a247-240">Możesz użyć innych Jobscience użytkownika konta tworzenia narzędzi lub interfejsów API dostarczonych przez Jobscience do świadczenia usługi Azure Active Directory kont użytkowników.</span><span class="sxs-lookup"><span data-stu-id="0a247-240">You can use any other Jobscience user account creation tools or APIs provided by Jobscience to provision Azure Active Directory user accounts.</span></span>
>  
        
<span data-ttu-id="0a247-241">**Aby skonfigurować, inicjowanie obsługi użytkowników, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="0a247-241">**To configure user provisioning, perform the following steps:**</span></span>

1. <span data-ttu-id="0a247-242">Zaloguj się do Twojego **Jobscience** witryny firmy jako administrator.</span><span class="sxs-lookup"><span data-stu-id="0a247-242">Log in to your **Jobscience** company site as administrator.</span></span>

2. <span data-ttu-id="0a247-243">Przejdź do instalacji.</span><span class="sxs-lookup"><span data-stu-id="0a247-243">Go to Setup.</span></span>
   
   <span data-ttu-id="0a247-244">![Instalator](./media/active-directory-saas-jobscience-tutorial/ic784358.png "Instalatora")</span><span class="sxs-lookup"><span data-stu-id="0a247-244">![Setup](./media/active-directory-saas-jobscience-tutorial/ic784358.png "Setup")</span></span>
3. <span data-ttu-id="0a247-245">Przejdź do **Zarządzanie użytkownikami \> użytkowników**.</span><span class="sxs-lookup"><span data-stu-id="0a247-245">Go to **Manage Users \> Users**.</span></span>
   
   <span data-ttu-id="0a247-246">![Użytkownicy](./media/active-directory-saas-jobscience-tutorial/ic784369.png "użytkowników")</span><span class="sxs-lookup"><span data-stu-id="0a247-246">![Users](./media/active-directory-saas-jobscience-tutorial/ic784369.png "Users")</span></span>
4. <span data-ttu-id="0a247-247">Kliknij przycisk **nowego użytkownika**.</span><span class="sxs-lookup"><span data-stu-id="0a247-247">Click **New User**.</span></span>
   
   <span data-ttu-id="0a247-248">![Wszyscy użytkownicy](./media/active-directory-saas-jobscience-tutorial/ic784370.png "wszyscy użytkownicy")</span><span class="sxs-lookup"><span data-stu-id="0a247-248">![All Users](./media/active-directory-saas-jobscience-tutorial/ic784370.png "All Users")</span></span>
5. <span data-ttu-id="0a247-249">Na **Edytowanie użytkownika** okna dialogowego, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="0a247-249">On the **Edit User** dialog, perform the following steps:</span></span>
   
   <span data-ttu-id="0a247-250">![Edycja użytkownika](./media/active-directory-saas-jobscience-tutorial/ic784371.png "Edycja użytkownika")</span><span class="sxs-lookup"><span data-stu-id="0a247-250">![User Edit](./media/active-directory-saas-jobscience-tutorial/ic784371.png "User Edit")</span></span>
   
   <span data-ttu-id="0a247-251">a.</span><span class="sxs-lookup"><span data-stu-id="0a247-251">a.</span></span> <span data-ttu-id="0a247-252">W **imię** tekstowym, wpisz imię użytkownika, takich jak Britta.</span><span class="sxs-lookup"><span data-stu-id="0a247-252">In the **First Name** textbox, type a first name of the user like Britta.</span></span>
   
   <span data-ttu-id="0a247-253">b.</span><span class="sxs-lookup"><span data-stu-id="0a247-253">b.</span></span> <span data-ttu-id="0a247-254">W **nazwisko** tekstowym, wpisz nazwisko użytkownika, takich jak Simona.</span><span class="sxs-lookup"><span data-stu-id="0a247-254">In the **Last Name** textbox, type a last name of the user like Simon.</span></span>
   
   <span data-ttu-id="0a247-255">c.</span><span class="sxs-lookup"><span data-stu-id="0a247-255">c.</span></span> <span data-ttu-id="0a247-256">W **Alias** tekstowym, wpisz nazwę użytkownika, takich jak brittas aliasu.</span><span class="sxs-lookup"><span data-stu-id="0a247-256">In the **Alias** textbox, type an alias name of the user like brittas.</span></span>

   <span data-ttu-id="0a247-257">d.</span><span class="sxs-lookup"><span data-stu-id="0a247-257">d.</span></span> <span data-ttu-id="0a247-258">W **E-mail** tekstowym, wpisz adres e-mail użytkownika, takich jak Brittasimon@contoso.com.</span><span class="sxs-lookup"><span data-stu-id="0a247-258">In the **Email** textbox, type the email address of user like Brittasimon@contoso.com.</span></span>

   <span data-ttu-id="0a247-259">e.</span><span class="sxs-lookup"><span data-stu-id="0a247-259">e.</span></span> <span data-ttu-id="0a247-260">W **nazwy użytkownika** tekstowym, wpisz nazwę użytkownika użytkownika, takich jak Brittasimon@contoso.com.</span><span class="sxs-lookup"><span data-stu-id="0a247-260">In the **User Name** textbox, type a user name of user like Brittasimon@contoso.com.</span></span>

   <span data-ttu-id="0a247-261">f.</span><span class="sxs-lookup"><span data-stu-id="0a247-261">f.</span></span> <span data-ttu-id="0a247-262">W **pseudonim** tekstowym, wpisz nazwę użytkownika, takich jak Simona nick.</span><span class="sxs-lookup"><span data-stu-id="0a247-262">In the **Nick Name** textbox, type a nick name of user like Simon.</span></span>

   <span data-ttu-id="0a247-263">g.</span><span class="sxs-lookup"><span data-stu-id="0a247-263">g.</span></span> <span data-ttu-id="0a247-264">Kliknij pozycję **Zapisz**.</span><span class="sxs-lookup"><span data-stu-id="0a247-264">Click **Save**.</span></span>

    
> [!NOTE]
> <span data-ttu-id="0a247-265">Właściciel konta usługi Azure Active Directory otrzymuje wiadomość e-mail i następuje łącze, aby potwierdzić swoje konto, zanim staje się aktywny.</span><span class="sxs-lookup"><span data-stu-id="0a247-265">The Azure Active Directory account holder receives an email and follows a link to confirm their account before it becomes active.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="0a247-266">Przypisanie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="0a247-266">Assigning the Azure AD test user</span></span>

<span data-ttu-id="0a247-267">W tej sekcji można włączyć Simona Britta do używania Azure logowania jednokrotnego za udzielanie dostępu Jobscience.</span><span class="sxs-lookup"><span data-stu-id="0a247-267">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Jobscience.</span></span>

![Przypisz użytkownika][200] 

<span data-ttu-id="0a247-269">**Aby przypisać Simona Britta Jobscience, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="0a247-269">**To assign Britta Simon to Jobscience, perform the following steps:**</span></span>

1. <span data-ttu-id="0a247-270">W portalu Azure Otwórz widok aplikacji, a następnie przejdź do widoku katalogu i przejdź do **aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="0a247-270">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Przypisz użytkownika][201] 

2. <span data-ttu-id="0a247-272">Na liście aplikacji zaznacz **Jobscience**.</span><span class="sxs-lookup"><span data-stu-id="0a247-272">In the applications list, select **Jobscience**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-jobscience-tutorial/tutorial_jobscience_app.png) 

3. <span data-ttu-id="0a247-274">W menu po lewej stronie kliknij **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="0a247-274">In the menu on the left, click **Users and groups**.</span></span>

    ![Przypisz użytkownika][202] 

4. <span data-ttu-id="0a247-276">Kliknij przycisk **Dodaj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="0a247-276">Click **Add** button.</span></span> <span data-ttu-id="0a247-277">Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="0a247-277">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Przypisz użytkownika][203]

5. <span data-ttu-id="0a247-279">Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** na liście Użytkownicy.</span><span class="sxs-lookup"><span data-stu-id="0a247-279">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="0a247-280">Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="0a247-280">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="0a247-281">Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="0a247-281">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="0a247-282">Testowanie rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="0a247-282">Testing single sign-on</span></span>

<span data-ttu-id="0a247-283">W tej sekcji można przetestować konfiguracji usługi Azure AD pojedynczego logowania za pomocą panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="0a247-283">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="0a247-284">Po kliknięciu kafelka Jobscience w panelu dostępu użytkownik powinien pobrać automatycznie zalogowane do aplikacji Jobscience.</span><span class="sxs-lookup"><span data-stu-id="0a247-284">When you click the Jobscience tile in the Access Panel, you should get automatically signed-on to your Jobscience application.</span></span>
<span data-ttu-id="0a247-285">Aby uzyskać więcej informacji na temat panelu dostępu, zobacz [wprowadzenie do panelu dostępu](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="0a247-285">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="0a247-286">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="0a247-286">Additional resources</span></span>

* [<span data-ttu-id="0a247-287">Lista samouczków dotyczących sposobów integracji aplikacji SaaS przy użyciu usługi Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="0a247-287">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="0a247-288">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="0a247-288">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-jobscience-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-jobscience-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-jobscience-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-jobscience-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-jobscience-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-jobscience-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-jobscience-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-jobscience-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-jobscience-tutorial/tutorial_general_203.png

