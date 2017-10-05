---
title: 'Samouczek: Integracji Azure Active Directory z Aha! | Microsoft Docs'
description: "Informacje o sposobie konfigurowania rejestracji jednokrotnej między usługą Azure Active Directory i Aha!."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: ad955d3d-896a-41bb-800d-68e8cb5ff48d
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/10/2017
ms.author: jeedes
ms.openlocfilehash: 7723864b2e1ab2d5b69d86f0fa18416b9d3f9aa3
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-aha"></a><span data-ttu-id="e02e7-104">Samouczek: Integracji Azure Active Directory z Aha!</span><span class="sxs-lookup"><span data-stu-id="e02e7-104">Tutorial: Azure Active Directory integration with Aha!</span></span>

<span data-ttu-id="e02e7-105">W tym samouczku opisano sposób integracji Aha!</span><span class="sxs-lookup"><span data-stu-id="e02e7-105">In this tutorial, you learn how to integrate Aha!</span></span> <span data-ttu-id="e02e7-106">z usługi Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="e02e7-106">with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="e02e7-107">Integrowanie Aha!</span><span class="sxs-lookup"><span data-stu-id="e02e7-107">Integrating Aha!</span></span> <span data-ttu-id="e02e7-108">z usługą Azure AD zapewnia następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="e02e7-108">with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="e02e7-109">Można kontrolować w usłudze Azure AD, który ma dostęp do Aha!</span><span class="sxs-lookup"><span data-stu-id="e02e7-109">You can control in Azure AD who has access to Aha!</span></span>
- <span data-ttu-id="e02e7-110">Umożliwia użytkownikom automatycznie pobrać zalogowane do Aha!</span><span class="sxs-lookup"><span data-stu-id="e02e7-110">You can enable your users to automatically get signed-on to Aha!</span></span> <span data-ttu-id="e02e7-111">(Logowanie jednokrotne) przy użyciu ich kont usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="e02e7-111">(Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="e02e7-112">Możesz zarządzać kont w jednej centralnej lokalizacji - portalu Azure</span><span class="sxs-lookup"><span data-stu-id="e02e7-112">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="e02e7-113">Jeśli chcesz dowiedzieć się więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="e02e7-113">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e02e7-114">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="e02e7-114">Prerequisites</span></span>

<span data-ttu-id="e02e7-115">Aby skonfigurować integrację usługi Azure AD z Aha!, potrzebne są następujące zasoby:</span><span class="sxs-lookup"><span data-stu-id="e02e7-115">To configure Azure AD integration with Aha!, you need the following items:</span></span>

- <span data-ttu-id="e02e7-116">Subskrypcję usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="e02e7-116">An Azure AD subscription</span></span>
- <span data-ttu-id="e02e7-117">Aha!</span><span class="sxs-lookup"><span data-stu-id="e02e7-117">An Aha!</span></span> <span data-ttu-id="e02e7-118">jednokrotnego włączone subskrypcji</span><span class="sxs-lookup"><span data-stu-id="e02e7-118">single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="e02e7-119">Aby przetestować kroki opisane w tym samouczku, zaleca się używania środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="e02e7-119">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="e02e7-120">Aby przetestować kroki opisane w tym samouczku, należy wykonać te zalecenia:</span><span class="sxs-lookup"><span data-stu-id="e02e7-120">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="e02e7-121">Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="e02e7-121">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="e02e7-122">Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz pobrać miesięczna wersja próbna [tutaj](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="e02e7-122">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="e02e7-123">Opis scenariusza</span><span class="sxs-lookup"><span data-stu-id="e02e7-123">Scenario description</span></span>
<span data-ttu-id="e02e7-124">W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym.</span><span class="sxs-lookup"><span data-stu-id="e02e7-124">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="e02e7-125">Scenariusz opisany w tym samouczku składa się z dwóch głównych elementów:</span><span class="sxs-lookup"><span data-stu-id="e02e7-125">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="e02e7-126">Dodawanie Aha!</span><span class="sxs-lookup"><span data-stu-id="e02e7-126">Adding Aha!</span></span> <span data-ttu-id="e02e7-127">z galerii</span><span class="sxs-lookup"><span data-stu-id="e02e7-127">from the gallery</span></span>
2. <span data-ttu-id="e02e7-128">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="e02e7-128">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-aha-from-the-gallery"></a><span data-ttu-id="e02e7-129">Dodawanie Aha!</span><span class="sxs-lookup"><span data-stu-id="e02e7-129">Adding Aha!</span></span> <span data-ttu-id="e02e7-130">z galerii</span><span class="sxs-lookup"><span data-stu-id="e02e7-130">from the gallery</span></span>
<span data-ttu-id="e02e7-131">Aby skonfigurować integrację Aha!</span><span class="sxs-lookup"><span data-stu-id="e02e7-131">To configure the integration of Aha!</span></span> <span data-ttu-id="e02e7-132">w usłudze Azure AD należy dodać Aha!</span><span class="sxs-lookup"><span data-stu-id="e02e7-132">into Azure AD, you need to add Aha!</span></span> <span data-ttu-id="e02e7-133">z poziomu galerii do listy zarządzanych aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="e02e7-133">from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="e02e7-134">**Aby dodać Aha! z poziomu galerii wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="e02e7-134">**To add Aha! from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="e02e7-135">W  **[portalu Azure](https://portal.azure.com)**, na panelu nawigacyjnym po lewej stronie kliknij **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="e02e7-135">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Usługa Active Directory][1]

2. <span data-ttu-id="e02e7-137">Przejdź do **aplikacje dla przedsiębiorstw**.</span><span class="sxs-lookup"><span data-stu-id="e02e7-137">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="e02e7-138">Następnie przejdź do **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="e02e7-138">Then go to **All applications**.</span></span>

    ![Aplikacje][2]
    
3. <span data-ttu-id="e02e7-140">Aby dodać nową aplikację, kliknij przycisk **nowej aplikacji** przycisk w górnej części okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="e02e7-140">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Aplikacje][3]

4. <span data-ttu-id="e02e7-142">W polu wyszukiwania wpisz **Aha!**.</span><span class="sxs-lookup"><span data-stu-id="e02e7-142">In the search box, type **Aha!**.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-aha-tutorial/tutorial_aha_search.png)

5. <span data-ttu-id="e02e7-144">W panelu wyników wybierz **Aha!**, a następnie kliknij przycisk **Dodaj** przycisk, aby dodać aplikację.</span><span class="sxs-lookup"><span data-stu-id="e02e7-144">In the results panel, select **Aha!**, and then click **Add** button to add the application.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-aha-tutorial/tutorial_aha_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="e02e7-146">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="e02e7-146">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="e02e7-147">W tej sekcji możesz skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z Aha!</span><span class="sxs-lookup"><span data-stu-id="e02e7-147">In this section, you configure and test Azure AD single sign-on with Aha!</span></span> <span data-ttu-id="e02e7-148">na podstawie użytkownika testowego, nazywany "Britta Simona".</span><span class="sxs-lookup"><span data-stu-id="e02e7-148">based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="e02e7-149">Dla rejestracji jednokrotnej do pracy usługi Azure AD musi wiedzieć, jaki użytkownik odpowiednika w Aha!</span><span class="sxs-lookup"><span data-stu-id="e02e7-149">For single sign-on to work, Azure AD needs to know what the counterpart user in Aha!</span></span> <span data-ttu-id="e02e7-150">jest użytkownikiem w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="e02e7-150">is to a user in Azure AD.</span></span> <span data-ttu-id="e02e7-151">Innymi słowy link relację między użytkownikiem usługi Azure AD i danemu użytkownikowi w Aha!</span><span class="sxs-lookup"><span data-stu-id="e02e7-151">In other words, a link relationship between an Azure AD user and the related user in Aha!</span></span> <span data-ttu-id="e02e7-152">powinien być określony.</span><span class="sxs-lookup"><span data-stu-id="e02e7-152">needs to be established.</span></span>

<span data-ttu-id="e02e7-153">W Aha!, przypisz wartość **nazwy użytkownika** w usłudze Azure AD jako wartość **Username** do ustanawiania relacji łącza.</span><span class="sxs-lookup"><span data-stu-id="e02e7-153">In Aha!, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="e02e7-154">Aby skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z Aha!, należy wykonać poniższe bloki konstrukcyjne:</span><span class="sxs-lookup"><span data-stu-id="e02e7-154">To configure and test Azure AD single sign-on with Aha!, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="e02e7-155">**[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configuring-azure-ad-single-sign-on)**  — aby umożliwić użytkownikom korzystać z tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="e02e7-155">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="e02e7-156">**[Tworzenie użytkownika testowego usługi Azure AD](#creating-an-azure-ad-test-user)**  — do przetestowania usługi Azure AD rejestracji jednokrotnej z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="e02e7-156">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="e02e7-157">**[Tworzenie Aha! Użytkownik testowy](#creating-an-aha-test-user)**  — w celu zapewnienia odpowiednikiem Simona Britta Aha!</span><span class="sxs-lookup"><span data-stu-id="e02e7-157">**[Creating an Aha! test user](#creating-an-aha-test-user)** - to have a counterpart of Britta Simon in Aha!</span></span> <span data-ttu-id="e02e7-158">Reprezentacja usługi Azure AD użytkownik jest połączony.</span><span class="sxs-lookup"><span data-stu-id="e02e7-158">that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="e02e7-159">**[Przypisanie użytkownika testowego usługi Azure AD](#assigning-the-azure-ad-test-user)**  — aby umożliwić Simona Britta do użycia usługi Azure AD rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="e02e7-159">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="e02e7-160">**[Testowanie rejestracji jednokrotnej](#testing-single-sign-on)**  — Aby sprawdzić, czy konfiguracja działa.</span><span class="sxs-lookup"><span data-stu-id="e02e7-160">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="e02e7-161">Konfigurowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="e02e7-161">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="e02e7-162">W tej sekcji włączyć usługi Azure AD rejestracji jednokrotnej w portalu Azure i skonfigurować logowanie jednokrotne w sieci Aha!</span><span class="sxs-lookup"><span data-stu-id="e02e7-162">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Aha!</span></span> <span data-ttu-id="e02e7-163">Aplikacja.</span><span class="sxs-lookup"><span data-stu-id="e02e7-163">application.</span></span>

<span data-ttu-id="e02e7-164">**Aby skonfigurować usługi Azure AD rejestracji jednokrotnej z Aha!, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="e02e7-164">**To configure Azure AD single sign-on with Aha!, perform the following steps:**</span></span>

1. <span data-ttu-id="e02e7-165">W portalu Azure na **Aha!**</span><span class="sxs-lookup"><span data-stu-id="e02e7-165">In the Azure portal, on the **Aha!**</span></span> <span data-ttu-id="e02e7-166">Strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.</span><span class="sxs-lookup"><span data-stu-id="e02e7-166">application integration page, click **Single sign-on**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej][4]

2. <span data-ttu-id="e02e7-168">Na **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** Aby włączyć logowanie jednokrotne.</span><span class="sxs-lookup"><span data-stu-id="e02e7-168">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-aha-tutorial/tutorial_aha_samlbase.png)

3. <span data-ttu-id="e02e7-170">Na **Aha! Adresy URL i domeny** sekcji, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="e02e7-170">On the **Aha! Domain and URLs** section, perform the following steps:</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-aha-tutorial/tutorial_aha_url.png)

    <span data-ttu-id="e02e7-172">a.</span><span class="sxs-lookup"><span data-stu-id="e02e7-172">a.</span></span> <span data-ttu-id="e02e7-173">W **adres URL logowania** tekstowym, wpisz adres URL, używając następującego wzorca:`https://<companyname>.aha.io/session/new`</span><span class="sxs-lookup"><span data-stu-id="e02e7-173">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<companyname>.aha.io/session/new`</span></span>

    <span data-ttu-id="e02e7-174">b.</span><span class="sxs-lookup"><span data-stu-id="e02e7-174">b.</span></span> <span data-ttu-id="e02e7-175">W **identyfikator** tekstowym, wpisz adres URL, używając następującego wzorca:`https://<companyname>.aha.io`</span><span class="sxs-lookup"><span data-stu-id="e02e7-175">In the **Identifier** textbox, type a URL using the following pattern: `https://<companyname>.aha.io`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="e02e7-176">Wartości te nie są prawdziwe.</span><span class="sxs-lookup"><span data-stu-id="e02e7-176">These values are not real.</span></span> <span data-ttu-id="e02e7-177">Rzeczywisty adres URL logowania i identyfikator, należy zaktualizować te wartości.</span><span class="sxs-lookup"><span data-stu-id="e02e7-177">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="e02e7-178">Skontaktuj się z [Aha! Zespół obsługi klienta](https://www.aha.io/company/contact) uzyskać te wartości.</span><span class="sxs-lookup"><span data-stu-id="e02e7-178">Contact [Aha! Client support team](https://www.aha.io/company/contact) to get these values.</span></span> 
 
4. <span data-ttu-id="e02e7-179">Na **certyfikat podpisywania SAML** kliknij **XML metadanych** , a następnie zapisz plik metadanych na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="e02e7-179">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-aha-tutorial/tutorial_aha_certificate.png) 

5. <span data-ttu-id="e02e7-181">Kliknij przycisk **zapisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="e02e7-181">Click **Save** button.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-aha-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="e02e7-183">W oknie przeglądarki innej witryny sieci web należy zalogować się do Twojego Aha!</span><span class="sxs-lookup"><span data-stu-id="e02e7-183">In a different web browser window, log in to your Aha!</span></span> <span data-ttu-id="e02e7-184">Witryna firmy jako administrator.</span><span class="sxs-lookup"><span data-stu-id="e02e7-184">company site as an administrator.</span></span>

7. <span data-ttu-id="e02e7-185">W menu u góry kliknij **ustawienia**.</span><span class="sxs-lookup"><span data-stu-id="e02e7-185">In the menu on the top, click **Settings**.</span></span>

    <span data-ttu-id="e02e7-186">![Ustawienia](./media/active-directory-saas-aha-tutorial/IC798950.png "ustawienia")</span><span class="sxs-lookup"><span data-stu-id="e02e7-186">![Settings](./media/active-directory-saas-aha-tutorial/IC798950.png "Settings")</span></span>

8. <span data-ttu-id="e02e7-187">Kliknij przycisk **konta**.</span><span class="sxs-lookup"><span data-stu-id="e02e7-187">Click **Account**.</span></span>
   
    <span data-ttu-id="e02e7-188">![Profil](./media/active-directory-saas-aha-tutorial/IC798951.png "profilu")</span><span class="sxs-lookup"><span data-stu-id="e02e7-188">![Profile](./media/active-directory-saas-aha-tutorial/IC798951.png "Profile")</span></span>

9. <span data-ttu-id="e02e7-189">Kliknij przycisk **zabezpieczeń i logowanie jednokrotne**.</span><span class="sxs-lookup"><span data-stu-id="e02e7-189">Click **Security and single sign-on**.</span></span>
   
    <span data-ttu-id="e02e7-190">![Bezpieczeństwo i logowanie jednokrotne](./media/active-directory-saas-aha-tutorial/IC798952.png "zabezpieczeń i logowanie jednokrotne")</span><span class="sxs-lookup"><span data-stu-id="e02e7-190">![Security and single sign-on](./media/active-directory-saas-aha-tutorial/IC798952.png "Security and single sign-on")</span></span>

10. <span data-ttu-id="e02e7-191">W **rejestracji jednokrotnej** sekcji jako **dostawcy tożsamości**, wybierz pozycję **SAML2.0**.</span><span class="sxs-lookup"><span data-stu-id="e02e7-191">In **Single Sign-On** section, as **Identity Provider**, select **SAML2.0**.</span></span>
   
    <span data-ttu-id="e02e7-192">![Bezpieczeństwo i logowanie jednokrotne](./media/active-directory-saas-aha-tutorial/IC798953.png "zabezpieczeń i logowanie jednokrotne")</span><span class="sxs-lookup"><span data-stu-id="e02e7-192">![Security and single sign-on](./media/active-directory-saas-aha-tutorial/IC798953.png "Security and single sign-on")</span></span>

11. <span data-ttu-id="e02e7-193">Na **rejestracji jednokrotnej** konfiguracji wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="e02e7-193">On the **Single Sign-On** configuration page, perform the following steps:</span></span>
    
    <span data-ttu-id="e02e7-194">![Logowanie jednokrotne](./media/active-directory-saas-aha-tutorial/IC798954.png "logowanie jednokrotne")</span><span class="sxs-lookup"><span data-stu-id="e02e7-194">![Single Sign-On](./media/active-directory-saas-aha-tutorial/IC798954.png "Single Sign-On")</span></span>
    
       <span data-ttu-id="e02e7-195">a.</span><span class="sxs-lookup"><span data-stu-id="e02e7-195">a.</span></span> <span data-ttu-id="e02e7-196">W **nazwa** tekstowym, wpisz nazwę dla danej konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="e02e7-196">In the **Name** textbox, type a name for your configuration.</span></span>

       <span data-ttu-id="e02e7-197">b.</span><span class="sxs-lookup"><span data-stu-id="e02e7-197">b.</span></span> <span data-ttu-id="e02e7-198">Aby uzyskać **skonfigurować za pomocą**, wybierz pozycję **pliku metadanych**.</span><span class="sxs-lookup"><span data-stu-id="e02e7-198">For **Configure using**, select **Metadata File**.</span></span>
   
       <span data-ttu-id="e02e7-199">c.</span><span class="sxs-lookup"><span data-stu-id="e02e7-199">c.</span></span> <span data-ttu-id="e02e7-200">Aby przekazać plik metadanych pobranych, kliknij przycisk **Przeglądaj**.</span><span class="sxs-lookup"><span data-stu-id="e02e7-200">To upload your downloaded metadata file, click **Browse**.</span></span>
   
       <span data-ttu-id="e02e7-201">d.</span><span class="sxs-lookup"><span data-stu-id="e02e7-201">d.</span></span> <span data-ttu-id="e02e7-202">Kliknij przycisk **aktualizacji**.</span><span class="sxs-lookup"><span data-stu-id="e02e7-202">Click **Update**.</span></span>

> [!TIP]
> <span data-ttu-id="e02e7-203">Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji!</span><span class="sxs-lookup"><span data-stu-id="e02e7-203">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="e02e7-204">Po dodaniu tej aplikacji z **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij **rejestracji jednokrotnej** karcie i dostęp do dokumentacji osadzonych za pomocą **konfiguracji** sekcji u dołu.</span><span class="sxs-lookup"><span data-stu-id="e02e7-204">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="e02e7-205">Więcej o funkcji dokumentacji osadzonego w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="e02e7-205">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="e02e7-206">Tworzenie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="e02e7-206">Creating an Azure AD test user</span></span>
<span data-ttu-id="e02e7-207">Celem tej sekcji jest tworzenie użytkownika testowego w portalu Azure o nazwie Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="e02e7-207">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Tworzenie użytkowników usługi Azure AD][100]

<span data-ttu-id="e02e7-209">**Aby utworzyć użytkownika testowego w usłudze Azure AD, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="e02e7-209">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="e02e7-210">W **portalu Azure**, w lewym okienku nawigacji, kliknij polecenie **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="e02e7-210">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-aha-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="e02e7-212">Aby wyświetlić listę użytkowników, przejdź do **użytkowników i grup** i kliknij przycisk **wszyscy użytkownicy**.</span><span class="sxs-lookup"><span data-stu-id="e02e7-212">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-aha-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="e02e7-214">Aby otworzyć **użytkownika** okna dialogowego, kliknij przycisk **Dodaj** górnej części okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="e02e7-214">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-aha-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="e02e7-216">Na **użytkownika** okna dialogowego strony, należy wykonać następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="e02e7-216">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-aha-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="e02e7-218">a.</span><span class="sxs-lookup"><span data-stu-id="e02e7-218">a.</span></span> <span data-ttu-id="e02e7-219">W **nazwa** pole tekstowe, typ **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="e02e7-219">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="e02e7-220">b.</span><span class="sxs-lookup"><span data-stu-id="e02e7-220">b.</span></span> <span data-ttu-id="e02e7-221">W **nazwy użytkownika** pole tekstowe, typ **adres e-mail** z BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="e02e7-221">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="e02e7-222">c.</span><span class="sxs-lookup"><span data-stu-id="e02e7-222">c.</span></span> <span data-ttu-id="e02e7-223">Wybierz **Pokaż hasło** i zanotuj wartość **hasło**.</span><span class="sxs-lookup"><span data-stu-id="e02e7-223">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="e02e7-224">d.</span><span class="sxs-lookup"><span data-stu-id="e02e7-224">d.</span></span> <span data-ttu-id="e02e7-225">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="e02e7-225">Click **Create**.</span></span>
 
### <a name="creating-an-aha-test-user"></a><span data-ttu-id="e02e7-226">Tworzenie Aha!</span><span class="sxs-lookup"><span data-stu-id="e02e7-226">Creating an Aha!</span></span> <span data-ttu-id="e02e7-227">Użytkownik testowy</span><span class="sxs-lookup"><span data-stu-id="e02e7-227">test user</span></span>

<span data-ttu-id="e02e7-228">Aby umożliwić użytkownikom usługi Azure AD zalogować się do Aha!, muszą mieć przydzielone do Aha!.</span><span class="sxs-lookup"><span data-stu-id="e02e7-228">To enable Azure AD users to log in to Aha!, they must be provisioned into Aha!.</span></span>  

<span data-ttu-id="e02e7-229">W przypadku Aha!, inicjowanie obsługi administracyjnej jest zautomatyzowanego zadania.</span><span class="sxs-lookup"><span data-stu-id="e02e7-229">In the case of Aha!, provisioning is an automated task.</span></span> <span data-ttu-id="e02e7-230">Nie ma elementu akcji dla Ciebie.</span><span class="sxs-lookup"><span data-stu-id="e02e7-230">There is no action item for you.</span></span>

<span data-ttu-id="e02e7-231">Użytkownicy są tworzone automatycznie w razie potrzeby podczas pierwszej pojedynczego logowania jednokrotnego próby.</span><span class="sxs-lookup"><span data-stu-id="e02e7-231">Users are automatically created if necessary during the first single sign-on attempt.</span></span>

>[!NOTE]
><span data-ttu-id="e02e7-232">Można użyć innych Aha!</span><span class="sxs-lookup"><span data-stu-id="e02e7-232">You can use any other Aha!</span></span> <span data-ttu-id="e02e7-233">narzędzia do tworzenia konta użytkownika lub interfejsów API dostarczonych przez Aha!</span><span class="sxs-lookup"><span data-stu-id="e02e7-233">user account creation tools or APIs provided by Aha!</span></span> <span data-ttu-id="e02e7-234">Aby udostępnić konta użytkownika usługi AAD.</span><span class="sxs-lookup"><span data-stu-id="e02e7-234">to provision AAD user accounts.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="e02e7-235">Przypisanie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="e02e7-235">Assigning the Azure AD test user</span></span>

<span data-ttu-id="e02e7-236">W tej sekcji można włączyć Simona Britta do używania Azure logowania jednokrotnego za udzielanie dostępu Aha!.</span><span class="sxs-lookup"><span data-stu-id="e02e7-236">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Aha!.</span></span>

![Przypisz użytkownika][200] 

<span data-ttu-id="e02e7-238">**Aby przypisać Simona Britta Aha!, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="e02e7-238">**To assign Britta Simon to Aha!, perform the following steps:**</span></span>

1. <span data-ttu-id="e02e7-239">W portalu Azure Otwórz widok aplikacji, a następnie przejdź do widoku katalogu i przejdź do **aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="e02e7-239">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Przypisz użytkownika][201] 

2. <span data-ttu-id="e02e7-241">Na liście aplikacji zaznacz **Aha!**.</span><span class="sxs-lookup"><span data-stu-id="e02e7-241">In the applications list, select **Aha!**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-aha-tutorial/tutorial_aha_app.png) 

3. <span data-ttu-id="e02e7-243">W menu po lewej stronie kliknij **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="e02e7-243">In the menu on the left, click **Users and groups**.</span></span>

    ![Przypisz użytkownika][202] 

4. <span data-ttu-id="e02e7-245">Kliknij przycisk **Dodaj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="e02e7-245">Click **Add** button.</span></span> <span data-ttu-id="e02e7-246">Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="e02e7-246">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Przypisz użytkownika][203]

5. <span data-ttu-id="e02e7-248">Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** na liście Użytkownicy.</span><span class="sxs-lookup"><span data-stu-id="e02e7-248">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="e02e7-249">Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="e02e7-249">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="e02e7-250">Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="e02e7-250">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="e02e7-251">Testowanie rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="e02e7-251">Testing single sign-on</span></span>

<span data-ttu-id="e02e7-252">Jeśli chcesz przetestować jednego ustawienia logowania jednokrotnego, otwórz Panel dostępu.</span><span class="sxs-lookup"><span data-stu-id="e02e7-252">If you want to test your single sign-on settings, open the Access Panel.</span></span> <span data-ttu-id="e02e7-253">Aby uzyskać więcej informacji na temat panelu dostępu, zobacz [wprowadzenie do panelu dostępu](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="e02e7-253">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="e02e7-254">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="e02e7-254">Additional resources</span></span>

* [<span data-ttu-id="e02e7-255">Lista samouczków dotyczących sposobów integracji aplikacji SaaS przy użyciu usługi Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="e02e7-255">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="e02e7-256">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="e02e7-256">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-aha-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-aha-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-aha-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-aha-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-aha-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-aha-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-aha-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-aha-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-aha-tutorial/tutorial_general_203.png

