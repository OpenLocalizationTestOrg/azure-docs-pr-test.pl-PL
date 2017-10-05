---
title: 'Samouczek: Integracji Azure Active Directory z Syncplicity | Dokumentacja firmy Microsoft'
description: "Informacje o sposobie konfigurowania rejestracji jednokrotnej między usługą Azure Active Directory i Syncplicity."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 896a3211-f368-46d7-95b8-e4768c23be08
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/22/2017
ms.author: jeedes
ms.openlocfilehash: 1321fa71bcd625d6ea754432bfb402d3919e38f3
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-syncplicity"></a><span data-ttu-id="c6c03-103">Samouczek: Integracji Azure Active Directory z Syncplicity</span><span class="sxs-lookup"><span data-stu-id="c6c03-103">Tutorial: Azure Active Directory integration with Syncplicity</span></span>

<span data-ttu-id="c6c03-104">Z tego samouczka dowiesz się integrowanie Syncplicity z usługi Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="c6c03-104">In this tutorial, you learn how to integrate Syncplicity with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="c6c03-105">Integracja z usługą Azure AD Syncplicity zapewnia następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="c6c03-105">Integrating Syncplicity with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="c6c03-106">Można kontrolować w usłudze Azure AD, który ma dostęp do Syncplicity</span><span class="sxs-lookup"><span data-stu-id="c6c03-106">You can control in Azure AD who has access to Syncplicity</span></span>
- <span data-ttu-id="c6c03-107">Umożliwia użytkownikom automatycznie pobrać zalogowane do Syncplicity (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="c6c03-107">You can enable your users to automatically get signed-on to Syncplicity (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="c6c03-108">Możesz zarządzać kont w jednej centralnej lokalizacji - portalu Azure</span><span class="sxs-lookup"><span data-stu-id="c6c03-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="c6c03-109">Jeśli chcesz dowiedzieć się więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="c6c03-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c6c03-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="c6c03-110">Prerequisites</span></span>

<span data-ttu-id="c6c03-111">Aby skonfigurować integrację usługi Azure AD z Syncplicity, potrzebne są następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="c6c03-111">To configure Azure AD integration with Syncplicity, you need the following items:</span></span>

- <span data-ttu-id="c6c03-112">Subskrypcję usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="c6c03-112">An Azure AD subscription</span></span>
- <span data-ttu-id="c6c03-113">Syncplicity logowanie jednokrotne włączone subskrypcji</span><span class="sxs-lookup"><span data-stu-id="c6c03-113">A Syncplicity single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="c6c03-114">Aby przetestować kroki opisane w tym samouczku, zaleca się używania środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="c6c03-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="c6c03-115">Aby przetestować kroki opisane w tym samouczku, należy wykonać te zalecenia:</span><span class="sxs-lookup"><span data-stu-id="c6c03-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="c6c03-116">Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="c6c03-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="c6c03-117">Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz pobrać miesięczna wersja próbna [tutaj](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="c6c03-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="c6c03-118">Opis scenariusza</span><span class="sxs-lookup"><span data-stu-id="c6c03-118">Scenario description</span></span>
<span data-ttu-id="c6c03-119">W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym.</span><span class="sxs-lookup"><span data-stu-id="c6c03-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="c6c03-120">Scenariusz opisany w tym samouczku składa się z dwóch głównych elementów:</span><span class="sxs-lookup"><span data-stu-id="c6c03-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="c6c03-121">Dodawanie Syncplicity z galerii</span><span class="sxs-lookup"><span data-stu-id="c6c03-121">Adding Syncplicity from the gallery</span></span>
2. <span data-ttu-id="c6c03-122">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="c6c03-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-syncplicity-from-the-gallery"></a><span data-ttu-id="c6c03-123">Dodawanie Syncplicity z galerii</span><span class="sxs-lookup"><span data-stu-id="c6c03-123">Adding Syncplicity from the gallery</span></span>
<span data-ttu-id="c6c03-124">Aby skonfigurować integrację usługi Azure AD Syncplicity, należy dodać Syncplicity z galerii do listy zarządzanych aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="c6c03-124">To configure the integration of Syncplicity into Azure AD, you need to add Syncplicity from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="c6c03-125">**Aby dodać Syncplicity z galerii, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="c6c03-125">**To add Syncplicity from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="c6c03-126">W  **[portalu Azure](https://portal.azure.com)**, na panelu nawigacyjnym po lewej stronie kliknij **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="c6c03-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Usługa Active Directory][1]

2. <span data-ttu-id="c6c03-128">Przejdź do **aplikacje dla przedsiębiorstw**.</span><span class="sxs-lookup"><span data-stu-id="c6c03-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="c6c03-129">Następnie przejdź do **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="c6c03-129">Then go to **All applications**.</span></span>

    ![Aplikacje][2]
    
3. <span data-ttu-id="c6c03-131">Aby dodać nową aplikację, kliknij przycisk **nowej aplikacji** przycisk w górnej części okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="c6c03-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Aplikacje][3]

4. <span data-ttu-id="c6c03-133">W polu wyszukiwania wpisz **Syncplicity**.</span><span class="sxs-lookup"><span data-stu-id="c6c03-133">In the search box, type **Syncplicity**.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-syncplicity-tutorial/tutorial_syncplicity_search.png)

5. <span data-ttu-id="c6c03-135">W panelu wyników wybierz **Syncplicity**, a następnie kliknij przycisk **Dodaj** przycisk, aby dodać aplikację.</span><span class="sxs-lookup"><span data-stu-id="c6c03-135">In the results panel, select **Syncplicity**, and then click **Add** button to add the application.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-syncplicity-tutorial/tutorial_syncplicity_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="c6c03-137">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="c6c03-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="c6c03-138">W tej sekcji możesz skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z Syncplicity na podstawie użytkownika testowego, nazywany "Britta Simona".</span><span class="sxs-lookup"><span data-stu-id="c6c03-138">In this section, you configure and test Azure AD single sign-on with Syncplicity based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="c6c03-139">Dla rejestracji jednokrotnej do pracy usługi Azure AD musi wiedzieć, użytkownik odpowiednika w Syncplicity jest dla użytkownika, w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c6c03-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Syncplicity is to a user in Azure AD.</span></span> <span data-ttu-id="c6c03-140">Innymi słowy link relację między użytkownikiem usługi Azure AD i danemu użytkownikowi w Syncplicity musi się.</span><span class="sxs-lookup"><span data-stu-id="c6c03-140">In other words, a link relationship between an Azure AD user and the related user in Syncplicity needs to be established.</span></span>

<span data-ttu-id="c6c03-141">W Syncplicity, należy przypisać wartość **nazwy użytkownika** w usłudze Azure AD jako wartość **Username** do ustanawiania relacji łącza.</span><span class="sxs-lookup"><span data-stu-id="c6c03-141">In Syncplicity, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="c6c03-142">Aby skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z Syncplicity, należy wykonać poniższe bloki konstrukcyjne:</span><span class="sxs-lookup"><span data-stu-id="c6c03-142">To configure and test Azure AD single sign-on with Syncplicity, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="c6c03-143">**[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configuring-azure-ad-single-sign-on)**  — aby umożliwić użytkownikom korzystać z tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="c6c03-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="c6c03-144">**[Tworzenie użytkownika testowego usługi Azure AD](#creating-an-azure-ad-test-user)**  — do przetestowania usługi Azure AD rejestracji jednokrotnej z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="c6c03-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="c6c03-145">**[Tworzenie użytkownika testowego Syncplicity](#creating-a-syncplicity-test-user)**  — w celu zapewnienia odpowiednikiem Simona Britta Syncplicity połączonego z usługi Azure AD reprezentację użytkownika.</span><span class="sxs-lookup"><span data-stu-id="c6c03-145">**[Creating a Syncplicity test user](#creating-a-syncplicity-test-user)** - to have a counterpart of Britta Simon in Syncplicity that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="c6c03-146">**[Przypisanie użytkownika testowego usługi Azure AD](#assigning-the-azure-ad-test-user)**  — aby umożliwić Simona Britta do użycia usługi Azure AD rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="c6c03-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="c6c03-147">**[Testowanie rejestracji jednokrotnej](#testing-single-sign-on)**  — Aby sprawdzić, czy konfiguracja działa.</span><span class="sxs-lookup"><span data-stu-id="c6c03-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="c6c03-148">Konfigurowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="c6c03-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="c6c03-149">W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w portalu Azure i skonfigurować logowanie jednokrotne w aplikacji Syncplicity.</span><span class="sxs-lookup"><span data-stu-id="c6c03-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Syncplicity application.</span></span>

<span data-ttu-id="c6c03-150">**Aby skonfigurować usługi Azure AD rejestracji jednokrotnej z Syncplicity, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="c6c03-150">**To configure Azure AD single sign-on with Syncplicity, perform the following steps:**</span></span>

1. <span data-ttu-id="c6c03-151">W portalu Azure na **Syncplicity** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.</span><span class="sxs-lookup"><span data-stu-id="c6c03-151">In the Azure portal, on the **Syncplicity** application integration page, click **Single sign-on**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej][4]

2. <span data-ttu-id="c6c03-153">Na **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** Aby włączyć logowanie jednokrotne.</span><span class="sxs-lookup"><span data-stu-id="c6c03-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-syncplicity-tutorial/tutorial_syncplicity_samlbase.png)

3. <span data-ttu-id="c6c03-155">Na **Syncplicity domeny i adres URL** sekcji, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="c6c03-155">On the **Syncplicity Domain and URLs** section, perform the following steps:</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-syncplicity-tutorial/tutorial_syncplicity_url.png)

    <span data-ttu-id="c6c03-157">a.</span><span class="sxs-lookup"><span data-stu-id="c6c03-157">a.</span></span> <span data-ttu-id="c6c03-158">W **adres URL logowania** tekstowym, wpisz adres URL, używając następującego wzorca:`https://<companyname>.syncplicity.com`</span><span class="sxs-lookup"><span data-stu-id="c6c03-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<companyname>.syncplicity.com`</span></span>

    <span data-ttu-id="c6c03-159">b.</span><span class="sxs-lookup"><span data-stu-id="c6c03-159">b.</span></span> <span data-ttu-id="c6c03-160">W **identyfikator** tekstowym, wpisz adres URL, używając następującego wzorca:`https://<companyname>.syncplicity.com/sp`</span><span class="sxs-lookup"><span data-stu-id="c6c03-160">In the **Identifier** textbox, type a URL using the following pattern: `https://<companyname>.syncplicity.com/sp`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="c6c03-161">Wartości te nie są prawdziwe.</span><span class="sxs-lookup"><span data-stu-id="c6c03-161">These values are not real.</span></span> <span data-ttu-id="c6c03-162">Rzeczywisty adres URL logowania i identyfikator, należy zaktualizować te wartości.</span><span class="sxs-lookup"><span data-stu-id="c6c03-162">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="c6c03-163">Skontaktuj się z [zespołem pomocy technicznej klienta Syncplicity](https://www.syncplicity.com/contact-us) uzyskać te wartości.</span><span class="sxs-lookup"><span data-stu-id="c6c03-163">Contact [Syncplicity Client support team](https://www.syncplicity.com/contact-us) to get these values.</span></span> 
 

4. <span data-ttu-id="c6c03-164">Na **certyfikat podpisywania SAML** kliknij **certyfikatu (Base64)** , a następnie zapisz plik certyfikatu na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="c6c03-164">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-syncplicity-tutorial/tutorial_syncplicity_certificate.png) 

  
5. <span data-ttu-id="c6c03-166">Kliknij przycisk **zapisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="c6c03-166">Click **Save** button.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-syncplicity-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="c6c03-168">Na **konfiguracji Syncplicity** , kliknij przycisk **skonfigurować Syncplicity** otworzyć **Konfigurowanie logowania jednokrotnego** okna.</span><span class="sxs-lookup"><span data-stu-id="c6c03-168">On the **Syncplicity Configuration** section, click **Configure Syncplicity** to open **Configure sign-on** window.</span></span> <span data-ttu-id="c6c03-169">Kopiuj **Sign-Out adres URL, identyfikator jednostki SAML i SAML pojedynczy znak na adres URL usługi** z **sekcji krótkimi opisami.**</span><span class="sxs-lookup"><span data-stu-id="c6c03-169">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-syncplicity-tutorial/tutorial_syncplicity_configure.png) 

7. <span data-ttu-id="c6c03-171">Zaloguj się do Twojego **Syncplicity** dzierżawy.</span><span class="sxs-lookup"><span data-stu-id="c6c03-171">Sign in to your **Syncplicity** tenant.</span></span>

8. <span data-ttu-id="c6c03-172">W menu u góry kliknij **admin**, wybierz pozycję **ustawienia**, a następnie kliknij przycisk **domeny niestandardowe i logowanie jednokrotne**.</span><span class="sxs-lookup"><span data-stu-id="c6c03-172">In the menu on the top, click **admin**, select **settings**, and then click **Custom domain and single sign-on**.</span></span>
   
    <span data-ttu-id="c6c03-173">![Syncplicity](./media/active-directory-saas-syncplicity-tutorial/ic769545.png "Syncplicity")</span><span class="sxs-lookup"><span data-stu-id="c6c03-173">![Syncplicity](./media/active-directory-saas-syncplicity-tutorial/ic769545.png "Syncplicity")</span></span>

9. <span data-ttu-id="c6c03-174">Na **pojedynczego logowania jednokrotnego (SSO)** okna dialogowego strony, należy wykonać następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="c6c03-174">On the **Single Sign-On (SSO)** dialog page, perform the following steps:</span></span>
   
    <span data-ttu-id="c6c03-175">![Logowanie jednokrotne \(logowania jednokrotnego\)](./media/active-directory-saas-syncplicity-tutorial/ic769550.png "Single Sign-On \\\(SSO\\\)")</span><span class="sxs-lookup"><span data-stu-id="c6c03-175">![Single Sign-On \(SSO\)](./media/active-directory-saas-syncplicity-tutorial/ic769550.png "Single Sign-On \\\(SSO\\\)")</span></span>   

    <span data-ttu-id="c6c03-176">a.</span><span class="sxs-lookup"><span data-stu-id="c6c03-176">a.</span></span> <span data-ttu-id="c6c03-177">W **domeny niestandardowe** tekstowym, wpisz nazwę domeny.</span><span class="sxs-lookup"><span data-stu-id="c6c03-177">In the **Custom Domain** textbox, type the name of your domain.</span></span>
  
    <span data-ttu-id="c6c03-178">b.</span><span class="sxs-lookup"><span data-stu-id="c6c03-178">b.</span></span> <span data-ttu-id="c6c03-179">Wybierz **włączone** jako **pojedynczy stan logowania jednokrotnego**.</span><span class="sxs-lookup"><span data-stu-id="c6c03-179">Select **Enabled** as **Single Sign-On Status**.</span></span>

    <span data-ttu-id="c6c03-180">c.</span><span class="sxs-lookup"><span data-stu-id="c6c03-180">c.</span></span> <span data-ttu-id="c6c03-181">W **identyfikator jednostki** pole tekstowe, Wklej wartość **identyfikator jednostki SAML** którego została skopiowana z portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="c6c03-181">In the **Entity Id** textbox, Paste the value of **SAML Entity ID** which you have copied from Azure portal.</span></span>

    <span data-ttu-id="c6c03-182">d.</span><span class="sxs-lookup"><span data-stu-id="c6c03-182">d.</span></span> <span data-ttu-id="c6c03-183">W **adres URL logowania strony** pole tekstowe, Wklej **SAML pojedynczy znak na adres URL usługi** którego została skopiowana z portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="c6c03-183">In the **Sign-in page URL** textbox, Paste the **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span></span>

    <span data-ttu-id="c6c03-184">e.</span><span class="sxs-lookup"><span data-stu-id="c6c03-184">e.</span></span> <span data-ttu-id="c6c03-185">W **adres URL strony wylogowania** pole tekstowe, Wklej **Sign-Out URL** którego została skopiowana z portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="c6c03-185">In the **Logout page URL** textbox, Paste the **Sign-Out URL** which you have copied from Azure portal.</span></span>

    <span data-ttu-id="c6c03-186">f.</span><span class="sxs-lookup"><span data-stu-id="c6c03-186">f.</span></span> <span data-ttu-id="c6c03-187">W **certyfikat dostawcy tożsamości**, kliknij przycisk **wybierz plik**, a następnie przekaż certyfikat, który został pobrany z portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="c6c03-187">In **Identity Provider Certificate**, click **Choose file**, and then upload the certificate which you have downloaded from the Azure portal.</span></span> 

    <span data-ttu-id="c6c03-188">g.</span><span class="sxs-lookup"><span data-stu-id="c6c03-188">g.</span></span> <span data-ttu-id="c6c03-189">Kliknij przycisk **ZAPISAĆ zmiany**.</span><span class="sxs-lookup"><span data-stu-id="c6c03-189">Click **SAVE CHANGES**.</span></span>

> [!TIP]
> <span data-ttu-id="c6c03-190">Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji!</span><span class="sxs-lookup"><span data-stu-id="c6c03-190">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="c6c03-191">Po dodaniu tej aplikacji z **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij **rejestracji jednokrotnej** karcie i dostęp do dokumentacji osadzonych za pomocą **konfiguracji** sekcji u dołu.</span><span class="sxs-lookup"><span data-stu-id="c6c03-191">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="c6c03-192">Więcej o funkcji dokumentacji osadzonego w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="c6c03-192">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="c6c03-193">Tworzenie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="c6c03-193">Creating an Azure AD test user</span></span>
<span data-ttu-id="c6c03-194">Celem tej sekcji jest tworzenie użytkownika testowego w portalu Azure o nazwie Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="c6c03-194">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Tworzenie użytkowników usługi Azure AD][100]

<span data-ttu-id="c6c03-196">**Aby utworzyć użytkownika testowego w usłudze Azure AD, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="c6c03-196">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="c6c03-197">W **portalu Azure**, w lewym okienku nawigacji, kliknij polecenie **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="c6c03-197">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-syncplicity-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="c6c03-199">Aby wyświetlić listę użytkowników, przejdź do **użytkowników i grup** i kliknij przycisk **wszyscy użytkownicy**.</span><span class="sxs-lookup"><span data-stu-id="c6c03-199">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-syncplicity-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="c6c03-201">Aby otworzyć **użytkownika** okna dialogowego, kliknij przycisk **Dodaj** górnej części okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="c6c03-201">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-syncplicity-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="c6c03-203">Na **użytkownika** okna dialogowego strony, należy wykonać następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="c6c03-203">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-syncplicity-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="c6c03-205">a.</span><span class="sxs-lookup"><span data-stu-id="c6c03-205">a.</span></span> <span data-ttu-id="c6c03-206">W **nazwa** pole tekstowe, typ **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="c6c03-206">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="c6c03-207">b.</span><span class="sxs-lookup"><span data-stu-id="c6c03-207">b.</span></span> <span data-ttu-id="c6c03-208">W **nazwy użytkownika** pole tekstowe, typ **adres e-mail** z BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="c6c03-208">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="c6c03-209">c.</span><span class="sxs-lookup"><span data-stu-id="c6c03-209">c.</span></span> <span data-ttu-id="c6c03-210">Wybierz **Pokaż hasło** i zanotuj wartość **hasło**.</span><span class="sxs-lookup"><span data-stu-id="c6c03-210">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="c6c03-211">d.</span><span class="sxs-lookup"><span data-stu-id="c6c03-211">d.</span></span> <span data-ttu-id="c6c03-212">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="c6c03-212">Click **Create**.</span></span>
 
### <a name="creating-a-syncplicity-test-user"></a><span data-ttu-id="c6c03-213">Tworzenie użytkownika testowego Syncplicity</span><span class="sxs-lookup"><span data-stu-id="c6c03-213">Creating a Syncplicity test user</span></span>
<span data-ttu-id="c6c03-214">Dla użytkowników usługi AAD można było zarejestrować muszą mieć przydzielone do Syncplicity aplikacji.</span><span class="sxs-lookup"><span data-stu-id="c6c03-214">For AAD users to be able to sign in, they must be provisioned to Syncplicity application.</span></span> <span data-ttu-id="c6c03-215">W tej sekcji opisano sposób tworzenia kont użytkowników usługi AAD w Syncplicity.</span><span class="sxs-lookup"><span data-stu-id="c6c03-215">This section describes how to create AAD user accounts in Syncplicity.</span></span>

<span data-ttu-id="c6c03-216">**Aby udostępnić konta użytkownika do Syncplicity, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="c6c03-216">**To provision a user account to Syncplicity, perform the following steps:**</span></span>

1. <span data-ttu-id="c6c03-217">Zaloguj się do Twojego **Syncplicity** dzierżawy (na przykład: `https://company.Syncplicity.com`).</span><span class="sxs-lookup"><span data-stu-id="c6c03-217">Log in to your **Syncplicity** tenant (for example: `https://company.Syncplicity.com`).</span></span>

2. <span data-ttu-id="c6c03-218">Kliknij przycisk **admin** i wybierz **kont użytkowników**.</span><span class="sxs-lookup"><span data-stu-id="c6c03-218">Click **admin** and select **user accounts**.</span></span>

3. <span data-ttu-id="c6c03-219">Kliknij przycisk **dodać użytkownika**.</span><span class="sxs-lookup"><span data-stu-id="c6c03-219">Click **ADD A USER**.</span></span>
   
    <span data-ttu-id="c6c03-220">![Zarządzaj użytkownikami](./media/active-directory-saas-syncplicity-tutorial/ic769764.png "Zarządzanie użytkownikami")</span><span class="sxs-lookup"><span data-stu-id="c6c03-220">![Manage Users](./media/active-directory-saas-syncplicity-tutorial/ic769764.png "Manage Users")</span></span>

4. <span data-ttu-id="c6c03-221">Typ **ruch poczty E-mail** konta usługi AAD chcesz udostępnić, wybierz **użytkownika** jako **roli**, a następnie kliknij przycisk **dalej**.</span><span class="sxs-lookup"><span data-stu-id="c6c03-221">Type the **Email addressess** of an AAD account you want to provision, select **User** as **Role**, and then click **NEXT**.</span></span>
   
    <span data-ttu-id="c6c03-222">![Informacji o koncie](./media/active-directory-saas-syncplicity-tutorial/ic769765.png "informacji o koncie")</span><span class="sxs-lookup"><span data-stu-id="c6c03-222">![Account Information](./media/active-directory-saas-syncplicity-tutorial/ic769765.png "Account Information")</span></span>
   
    >[!NOTE]
    ><span data-ttu-id="c6c03-223">Właściciel konta usługi AAD pobiera adres e-mail, łącznie z łączem do potwierdzenia i Aktywuj konta.</span><span class="sxs-lookup"><span data-stu-id="c6c03-223">The AAD account holder  gets an email including a link to confirm and activate the account.</span></span> 
    > 

5. <span data-ttu-id="c6c03-224">Wybierz grupę w Twojej firmie, nowy użytkownik powinien członkiem, a następnie kliknij przycisk **dalej**.</span><span class="sxs-lookup"><span data-stu-id="c6c03-224">Select a group in your company that your new user should become a member of, and then click **NEXT**.</span></span>
   
    <span data-ttu-id="c6c03-225">![Członkostwa w grupie](./media/active-directory-saas-syncplicity-tutorial/ic769772.png "członkostwa grupy")</span><span class="sxs-lookup"><span data-stu-id="c6c03-225">![Group Membership](./media/active-directory-saas-syncplicity-tutorial/ic769772.png "Group Membership")</span></span>
   
    >[!NOTE]
    ><span data-ttu-id="c6c03-226">Jeśli nie ma żadnych grup, na liście, kliknij przycisk **dalej**.</span><span class="sxs-lookup"><span data-stu-id="c6c03-226">If there are no groups listed, click **NEXT**.</span></span> 
    > 

6. <span data-ttu-id="c6c03-227">Wybierz foldery, które chcesz umieścić pod kontrolą firmy Syncplicity na komputerze użytkownika, a następnie kliknij przycisk **dalej**.</span><span class="sxs-lookup"><span data-stu-id="c6c03-227">Select the folders you would like to place under Syncplicity’s control on the user’s computer, and then click **NEXT**.</span></span>
   
    <span data-ttu-id="c6c03-228">![Foldery Syncplicity](./media/active-directory-saas-syncplicity-tutorial/ic769773.png "Syncplicity folderów")</span><span class="sxs-lookup"><span data-stu-id="c6c03-228">![Syncplicity Folders](./media/active-directory-saas-syncplicity-tutorial/ic769773.png "Syncplicity Folders")</span></span>

>[!NOTE]
><span data-ttu-id="c6c03-229">Możesz użyć innych Syncplicity użytkownika konta tworzenia narzędzi lub interfejsów API dostarczonych przez Syncplicity do kont użytkowników usługi AAD.</span><span class="sxs-lookup"><span data-stu-id="c6c03-229">You can use any other Syncplicity user account creation tools or APIs provided by Syncplicity to provision AAD user accounts.</span></span> 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="c6c03-230">Przypisanie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="c6c03-230">Assigning the Azure AD test user</span></span>

<span data-ttu-id="c6c03-231">W tej sekcji można włączyć Simona Britta do używania Azure logowania jednokrotnego za udzielanie dostępu Syncplicity.</span><span class="sxs-lookup"><span data-stu-id="c6c03-231">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Syncplicity.</span></span>

![Przypisz użytkownika][200] 

<span data-ttu-id="c6c03-233">**Aby przypisać Simona Britta Syncplicity, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="c6c03-233">**To assign Britta Simon to Syncplicity, perform the following steps:**</span></span>

1. <span data-ttu-id="c6c03-234">W portalu Azure Otwórz widok aplikacji, a następnie przejdź do widoku katalogu i przejdź do **aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="c6c03-234">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Przypisz użytkownika][201] 

2. <span data-ttu-id="c6c03-236">Na liście aplikacji zaznacz **Syncplicity**.</span><span class="sxs-lookup"><span data-stu-id="c6c03-236">In the applications list, select **Syncplicity**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-syncplicity-tutorial/tutorial_syncplicity_app.png) 

3. <span data-ttu-id="c6c03-238">W menu po lewej stronie kliknij **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="c6c03-238">In the menu on the left, click **Users and groups**.</span></span>

    ![Przypisz użytkownika][202] 

4. <span data-ttu-id="c6c03-240">Kliknij przycisk **Dodaj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="c6c03-240">Click **Add** button.</span></span> <span data-ttu-id="c6c03-241">Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="c6c03-241">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Przypisz użytkownika][203]

5. <span data-ttu-id="c6c03-243">Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** na liście Użytkownicy.</span><span class="sxs-lookup"><span data-stu-id="c6c03-243">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="c6c03-244">Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="c6c03-244">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="c6c03-245">Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="c6c03-245">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="c6c03-246">Testowanie rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="c6c03-246">Testing single sign-on</span></span>

<span data-ttu-id="c6c03-247">Celem tej sekcji służy do testowania konfiguracji usługi Azure AD pojedynczego logowania za pomocą panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="c6c03-247">The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="c6c03-248">Po kliknięciu kafelka Syncplicity w panelu dostępu użytkownik powinien pobrać automatycznie zalogowane do aplikacji Syncplicity.</span><span class="sxs-lookup"><span data-stu-id="c6c03-248">When you click the Syncplicity tile in the Access Panel, you should get automatically signed-on to your Syncplicity application.</span></span>
## <a name="additional-resources"></a><span data-ttu-id="c6c03-249">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="c6c03-249">Additional resources</span></span>

* [<span data-ttu-id="c6c03-250">Lista samouczków dotyczących sposobów integracji aplikacji SaaS przy użyciu usługi Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="c6c03-250">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="c6c03-251">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="c6c03-251">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-syncplicity-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-syncplicity-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-syncplicity-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-syncplicity-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-syncplicity-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-syncplicity-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-syncplicity-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-syncplicity-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-syncplicity-tutorial/tutorial_general_203.png

