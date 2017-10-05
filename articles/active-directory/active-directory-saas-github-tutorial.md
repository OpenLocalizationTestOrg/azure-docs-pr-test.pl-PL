---
title: "Samouczek: Integracji Azure Active Directory z usługi GitHub | Dokumentacja firmy Microsoft"
description: "Informacje o sposobie konfigurowania rejestracji jednokrotnej między usługą Azure Active Directory i usługi GitHub."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 4395bd95-05de-4deb-87a5-dc3bc8ac4d95
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/20/2017
ms.author: jeedes
ms.reviewer: jeedes
ms.openlocfilehash: 9dc12bc2e313bcb2000724d035156c5054d14e1c
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-github"></a><span data-ttu-id="7f944-103">Samouczek: Integracji Azure Active Directory z usługi GitHub</span><span class="sxs-lookup"><span data-stu-id="7f944-103">Tutorial: Azure Active Directory integration with GitHub</span></span>

<span data-ttu-id="7f944-104">Z tego samouczka dowiesz się integrowanie GitHub z usługi Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="7f944-104">In this tutorial, you learn how to integrate GitHub with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="7f944-105">Integrowanie usługi GitHub z usługą Azure AD zapewnia następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="7f944-105">Integrating GitHub with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="7f944-106">Można kontrolować w usłudze Azure AD, który ma dostęp do usługi GitHub</span><span class="sxs-lookup"><span data-stu-id="7f944-106">You can control in Azure AD who has access to GitHub</span></span>
- <span data-ttu-id="7f944-107">Umożliwia użytkownikom automatycznie pobrać zalogowane do usługi GitHub (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="7f944-107">You can enable your users to automatically get signed-on to GitHub (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="7f944-108">Możesz zarządzać kont w jednej centralnej lokalizacji - portalu zarządzania Azure</span><span class="sxs-lookup"><span data-stu-id="7f944-108">You can manage your accounts in one central location - the Azure Management portal</span></span>

<span data-ttu-id="7f944-109">Jeśli chcesz dowiedzieć się więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="7f944-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="7f944-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="7f944-110">Prerequisites</span></span>

<span data-ttu-id="7f944-111">Aby skonfigurować integrację usługi Azure AD z usługi GitHub, potrzebne są następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="7f944-111">To configure Azure AD integration with GitHub, you need the following items:</span></span>

- <span data-ttu-id="7f944-112">Subskrypcję usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="7f944-112">An Azure AD subscription</span></span>
- <span data-ttu-id="7f944-113">GitHub jednokrotnego włączone subskrypcji</span><span class="sxs-lookup"><span data-stu-id="7f944-113">A GitHub single-sign on enabled subscription</span></span>


> [!NOTE]
> <span data-ttu-id="7f944-114">Aby przetestować kroki opisane w tym samouczku, zaleca się używania środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="7f944-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>


<span data-ttu-id="7f944-115">Aby przetestować kroki opisane w tym samouczku, należy wykonać te zalecenia:</span><span class="sxs-lookup"><span data-stu-id="7f944-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="7f944-116">Nie należy używać środowiska produkcyjnego, chyba że jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="7f944-116">You should not use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="7f944-117">Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz pobrać miesięczna wersja próbna [tutaj](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="7f944-117">If you don't have an Azure AD trial environment, you can get an one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>


## <a name="scenario-description"></a><span data-ttu-id="7f944-118">Opis scenariusza</span><span class="sxs-lookup"><span data-stu-id="7f944-118">Scenario description</span></span>
<span data-ttu-id="7f944-119">W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym.</span><span class="sxs-lookup"><span data-stu-id="7f944-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="7f944-120">Scenariusz opisany w tym samouczku składa się z dwóch głównych elementów:</span><span class="sxs-lookup"><span data-stu-id="7f944-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="7f944-121">Dodawanie GitHub z galerii</span><span class="sxs-lookup"><span data-stu-id="7f944-121">Adding GitHub from the gallery</span></span>
2. <span data-ttu-id="7f944-122">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="7f944-122">Configuring and testing Azure AD single sign-on</span></span>


## <a name="adding-github-from-the-gallery"></a><span data-ttu-id="7f944-123">Dodawanie GitHub z galerii</span><span class="sxs-lookup"><span data-stu-id="7f944-123">Adding GitHub from the gallery</span></span>
<span data-ttu-id="7f944-124">Aby skonfigurować integrację usługi Azure AD GitHub, musisz dodać GitHub z galerii do listy zarządzanych aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="7f944-124">To configure the integration of GitHub into Azure AD, you need to add GitHub from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="7f944-125">**Aby dodać GitHub z poziomu galerii, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="7f944-125">**To add GitHub from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="7f944-126">W  **[portalu zarządzania Azure](https://portal.azure.com)**, na panelu nawigacyjnym po lewej stronie kliknij **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="7f944-126">In the **[Azure Management Portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Usługa Active Directory][1]

2. <span data-ttu-id="7f944-128">Przejdź do **aplikacje dla przedsiębiorstw**.</span><span class="sxs-lookup"><span data-stu-id="7f944-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="7f944-129">Następnie przejdź do **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="7f944-129">Then go to **All applications**.</span></span>

    ![Aplikacje][2]
    
3. <span data-ttu-id="7f944-131">Kliknij przycisk **Dodaj** przycisk w górnej części okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="7f944-131">Click **Add** button on the top of the dialog.</span></span>

    ![Aplikacje][3]

4. <span data-ttu-id="7f944-133">W polu wyszukiwania wpisz **witryną GitHub.com**.</span><span class="sxs-lookup"><span data-stu-id="7f944-133">In the search box, type **GitHub.com**.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-github-tutorial/tutorial_github_search02.png)

5. <span data-ttu-id="7f944-135">W panelu wyników wybierz **GitHub**, a następnie kliknij przycisk **Dodaj** przycisk, aby dodać aplikację.</span><span class="sxs-lookup"><span data-stu-id="7f944-135">In the results panel, select **GitHub**, and then click **Add** button to add the application.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-github-tutorial/tutorial_github_search_result02.png)


##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="7f944-137">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="7f944-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="7f944-138">W tej sekcji skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z usługi GitHub w oparciu o nazwie "Britta Simona" użytkownika testowego.</span><span class="sxs-lookup"><span data-stu-id="7f944-138">In this section, you configure and test Azure AD single sign-on with GitHub based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="7f944-139">Dla rejestracji jednokrotnej do pracy usługi Azure AD musi wiedzieć, użytkownik odpowiednika w serwisie GitHub jest dla użytkownika, w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="7f944-139">For single sign-on to work, Azure AD needs to know what the counterpart user in GitHub is to a user in Azure AD.</span></span> <span data-ttu-id="7f944-140">Innymi słowy relację łącza między użytkownika usługi Azure AD i powiązane użytkownika w usłudze GitHub musi określone.</span><span class="sxs-lookup"><span data-stu-id="7f944-140">In other words, a link relationship between an Azure AD user and the related user in GitHub needs to be established.</span></span>

<span data-ttu-id="7f944-141">Ta relacja łącza zostanie nawiązane, przypisując wartość **nazwy użytkownika** w usłudze Azure AD jako wartość **Username** w witrynie GitHub.</span><span class="sxs-lookup"><span data-stu-id="7f944-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in GitHub.</span></span>

<span data-ttu-id="7f944-142">Aby skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z usługi GitHub, należy wykonać poniższe bloki konstrukcyjne:</span><span class="sxs-lookup"><span data-stu-id="7f944-142">To configure and test Azure AD single sign-on with GitHub, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="7f944-143">**[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configuring-azure-ad-single-sign-on)**  — aby umożliwić użytkownikom korzystać z tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="7f944-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="7f944-144">**[Tworzenie użytkownika testowego usługi Azure AD](#creating-an-azure-ad-test-user)**  — do przetestowania usługi Azure AD rejestracji jednokrotnej z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="7f944-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="7f944-145">**[Tworzenie użytkownika testowego GitHub](#creating-a-GitHub-test-user)**  — w celu zapewnienia odpowiednikiem Simona Britta GitHub połączonego z jej reprezentacji usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="7f944-145">**[Creating a GitHub test user](#creating-a-GitHub-test-user)** - to have a counterpart of Britta Simon in GitHub that is linked to the Azure AD representation of her.</span></span>
4. <span data-ttu-id="7f944-146">**[Przypisanie użytkownika testowego usługi Azure AD](#assigning-the-azure-ad-test-user)**  — aby umożliwić Simona Britta do użycia usługi Azure AD rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="7f944-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="7f944-147">**[Testowanie rejestracji jednokrotnej](#testing-single-sign-on)**  — Aby sprawdzić, czy konfiguracja działa.</span><span class="sxs-lookup"><span data-stu-id="7f944-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="7f944-148">Konfigurowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="7f944-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="7f944-149">W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w portalu zarządzania Azure i skonfigurować logowanie jednokrotne w aplikacji GitHub.</span><span class="sxs-lookup"><span data-stu-id="7f944-149">In this section, you enable Azure AD single sign-on in the Azure Management portal and configure single sign-on in your GitHub application.</span></span>

<span data-ttu-id="7f944-150">**Aby skonfigurować usługi Azure AD rejestracji jednokrotnej z usługi GitHub, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="7f944-150">**To configure Azure AD single sign-on with GitHub, perform the following steps:**</span></span>

1. <span data-ttu-id="7f944-151">W portalu zarządzania Azure na **GitHub** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.</span><span class="sxs-lookup"><span data-stu-id="7f944-151">In the Azure Management portal, on the **GitHub** application integration page, click **Single sign-on**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej][4]

2. <span data-ttu-id="7f944-153">Na **logowanie jednokrotne** okna dialogowego, jako **tryb** wybierz **na języku SAML logowania jednokrotnego** Włącz funkcji logowania jednokrotnego.</span><span class="sxs-lookup"><span data-stu-id="7f944-153">On the **Single sign-on** dialog, as **Mode** select **SAML-based Sign-on** to enable single sign on.</span></span>
 
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-github-tutorial/tutorial_github_01.png)

3. <span data-ttu-id="7f944-155">Na **GitHub domeny i adres URL** sekcji, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="7f944-155">On the **GitHub Domain and URLs** section, perform the following steps:</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-github-tutorial/tutorial_github_saml011.png)

    <span data-ttu-id="7f944-157">a.</span><span class="sxs-lookup"><span data-stu-id="7f944-157">a.</span></span> <span data-ttu-id="7f944-158">W **adres URL logowania** tekstowym, wpisz wartość, jak:`https://github.com/orgs/<entity-id>/sso`</span><span class="sxs-lookup"><span data-stu-id="7f944-158">In the **Sign-on URL** textbox, type the value as: `https://github.com/orgs/<entity-id>/sso`</span></span>

    <span data-ttu-id="7f944-159">b.</span><span class="sxs-lookup"><span data-stu-id="7f944-159">b.</span></span> <span data-ttu-id="7f944-160">W **identyfikator** tekstowym, wpisz adres URL, używając następującego wzorca:`https://github.com/orgs/<entity-id>`</span><span class="sxs-lookup"><span data-stu-id="7f944-160">In the **Identifier** textbox, type a URL using the following pattern: `https://github.com/orgs/<entity-id>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="7f944-161">Należy pamiętać, że nie są one rzeczywiste wartości.</span><span class="sxs-lookup"><span data-stu-id="7f944-161">Please note that these are not the real values.</span></span> <span data-ttu-id="7f944-162">Należy zaktualizować te wartości z rzeczywistego uwagi na URL i identyfikator.</span><span class="sxs-lookup"><span data-stu-id="7f944-162">You have to update these values with the actual Sing-on URL and Identifier.</span></span> <span data-ttu-id="7f944-163">W tym miejscu zalecamy można używać unikatowej wartości ciągu w identyfikatorze.</span><span class="sxs-lookup"><span data-stu-id="7f944-163">Here we suggest you to use the unique value of string in the Identifier.</span></span> <span data-ttu-id="7f944-164">Przejdź do sekcji GitHub administratora dotyczące pobierania tych wartości.</span><span class="sxs-lookup"><span data-stu-id="7f944-164">Go to GitHub Admin section to retrieve these values.</span></span> 

4. <span data-ttu-id="7f944-165">Na **atrybuty użytkownika** zaznacz **identyfikator użytkownika** jako user.mail.</span><span class="sxs-lookup"><span data-stu-id="7f944-165">On the **User Attributes** section, select **User Identifier** as user.mail.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-github-tutorial/tutorial_github_attribute_new01.png)
    
5. <span data-ttu-id="7f944-167">Na **certyfikat podpisywania SAML** kliknij **Utwórz nowy certyfikat**.</span><span class="sxs-lookup"><span data-stu-id="7f944-167">On the **SAML Signing Certificate** section, click **Create new certificate**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-github-tutorial/tutorial_github_03.png)

6. <span data-ttu-id="7f944-169">Na **Tworzenie nowego świadectwa** okna dialogowego, kliknij ikonę kalendarza i wybierz **Data wygaśnięcia**.</span><span class="sxs-lookup"><span data-stu-id="7f944-169">On the **Create New Certificate** dialog, click the calendar icon and select an **expiry date**.</span></span> <span data-ttu-id="7f944-170">Następnie kliknij przycisk **zapisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="7f944-170">Then click **Save** button.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-github-tutorial/tutorial_general_300.png)

7. <span data-ttu-id="7f944-172">Na **certyfikat podpisywania SAML** wybierz opcję **uaktywnić nowego świadectwa** i kliknij przycisk **zapisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="7f944-172">On the **SAML Signing Certificate** section, select **Make new certificate active** and click **Save** button.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-github-tutorial/tutorial_github_04.png)

8. <span data-ttu-id="7f944-174">W oknie podręcznym **certyfikat przerzucania** okna, kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="7f944-174">On the pop-up **Rollover certificate** window, click **OK**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-github-tutorial/tutorial_general_400.png)

9. <span data-ttu-id="7f944-176">Na **certyfikat podpisywania SAML** kliknij **certyfikatu (Base64)** , a następnie zapisz plik certyfikatu na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="7f944-176">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-github-tutorial/tutorial_github_05.png) 

10. <span data-ttu-id="7f944-178">Na **konfiguracji GitHub** , kliknij przycisk **skonfigurować GitHub** otworzyć **Konfigurowanie logowania jednokrotnego** okna.</span><span class="sxs-lookup"><span data-stu-id="7f944-178">On the **GitHub Configuration** section, click **Configure GitHub** to open **Configure sign-on** window.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-github-tutorial/tutorial_github_06.png) 

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-github-tutorial/tutorial_github_07.png)

11. <span data-ttu-id="7f944-181">W oknie przeglądarki innej witryny sieci web Zaloguj się do witryny GitHub organizacji jako administrator.</span><span class="sxs-lookup"><span data-stu-id="7f944-181">In a different web browser window, log into your GitHub organization site as an administrator.</span></span>

12. <span data-ttu-id="7f944-182">Przejdź do **ustawienia** i kliknij przycisk **zabezpieczeń**</span><span class="sxs-lookup"><span data-stu-id="7f944-182">Navigate to **Settings** and click **Security**</span></span>

    ![Ustawienia](./media/active-directory-saas-github-tutorial/tutorial_github_config_github_03.png)

13. <span data-ttu-id="7f944-184">Sprawdź **uwierzytelnianie Włącz SAML** pole ujawniania pola konfiguracji logowania jednokrotnego.</span><span class="sxs-lookup"><span data-stu-id="7f944-184">Check the **Enable SAML authentication** box, revealing the Single Sign-on configuration fields.</span></span> <span data-ttu-id="7f944-185">Następnie zaktualizuj pojedynczy adres URL logowania w konfiguracji usługi Azure AD za pomocą pojedynczego logowania jednokrotnego wartość adresu URL.</span><span class="sxs-lookup"><span data-stu-id="7f944-185">Then, use the single sign-on URL value to update the Single sign-on URL on Azure AD configuration.</span></span>

    ![Ustawienia](./media/active-directory-saas-github-tutorial/tutorial_github_config_github_13.png)

14. <span data-ttu-id="7f944-187">Określ następujące pola:</span><span class="sxs-lookup"><span data-stu-id="7f944-187">Configure the following fields:</span></span>

    <span data-ttu-id="7f944-188">a.</span><span class="sxs-lookup"><span data-stu-id="7f944-188">a.</span></span> <span data-ttu-id="7f944-189">**Zaloguj się na adres URL**: wprowadź **SAML rejestracji jednokrotnej adres URL usługi** z **skonfigurować GitHub** sekcję na temat usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="7f944-189">**Sign on URL**: Enter **SAML Single sign-on Service URL** from the **Configure GitHub** section on Azure AD</span></span>

    <span data-ttu-id="7f944-190">b.</span><span class="sxs-lookup"><span data-stu-id="7f944-190">b.</span></span> <span data-ttu-id="7f944-191">**Wystawca**: wprowadź **identyfikator jednostki SAML** z **skonfigurować GitHub** sekcję na temat usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="7f944-191">**Issuer**: Enter **SAML Entity ID** from the **Configure GitHub** section on Azure AD</span></span>

    <span data-ttu-id="7f944-192">c.</span><span class="sxs-lookup"><span data-stu-id="7f944-192">c.</span></span> <span data-ttu-id="7f944-193">**Certyfikat publiczny**: Otwórz pobranego certyfikatu z usługi Azure AD w programie Notatnik i skopiuj zawartość, w tym "Certyfikat BEGIN" i "END CERTIFICATE"</span><span class="sxs-lookup"><span data-stu-id="7f944-193">**Public Certificate**: Open the downloaded certificate from Azure AD in a notepad and copy the content including "BEGIN CERTIFICATE" and "END CERTIFICATE"</span></span>

    ![Ustawienia](./media/active-directory-saas-github-tutorial/tutorial_github_config_github_051.png)

15. <span data-ttu-id="7f944-195">Polecenie **konfiguracji testu SAML** potwierdzić, że nie wystąpiły błędy sprawdzania poprawności lub błędy podczas rejestracji Jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="7f944-195">Click on **Test SAML configuration** to confirm that no validation failures or errors during SSO.</span></span>

    ![Ustawienia](./media/active-directory-saas-github-tutorial/tutorial_github_config_github_06.png)

16. <span data-ttu-id="7f944-197">Kliknij przycisk **Zapisz**</span><span class="sxs-lookup"><span data-stu-id="7f944-197">Click **Save**</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="7f944-198">Tworzenie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="7f944-198">Creating an Azure AD test user</span></span>
<span data-ttu-id="7f944-199">Celem tej sekcji jest tworzenie użytkownika testowego w portalu zarządzania Azure o nazwie Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="7f944-199">The objective of this section is to create a test user in the Azure Management portal called Britta Simon.</span></span>

![Tworzenie użytkowników usługi Azure AD][100]

<span data-ttu-id="7f944-201">**Aby utworzyć użytkownika testowego w usłudze Azure AD, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="7f944-201">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="7f944-202">W **portalu zarządzania Azure**, w lewym okienku nawigacji, kliknij polecenie **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="7f944-202">In the **Azure Management portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-github-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="7f944-204">Przejdź do **użytkowników i grup** i kliknij przycisk **wszyscy użytkownicy** do wyświetlenia na liście Użytkownicy.</span><span class="sxs-lookup"><span data-stu-id="7f944-204">Go to **Users and groups** and click **All users** to display the list of users.</span></span>
    
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-github-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="7f944-206">W górnej części okna dialogowego kliknij **Dodaj** otworzyć **użytkownika** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="7f944-206">At the top of the dialog click **Add** to open the **User** dialog.</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-github-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="7f944-208">Na **użytkownika** okna dialogowego strony, należy wykonać następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="7f944-208">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-github-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="7f944-210">a.</span><span class="sxs-lookup"><span data-stu-id="7f944-210">a.</span></span> <span data-ttu-id="7f944-211">W **nazwa** pole tekstowe, typ **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="7f944-211">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="7f944-212">b.</span><span class="sxs-lookup"><span data-stu-id="7f944-212">b.</span></span> <span data-ttu-id="7f944-213">W **nazwy użytkownika** pole tekstowe, typ **adres e-mail** z BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="7f944-213">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="7f944-214">c.</span><span class="sxs-lookup"><span data-stu-id="7f944-214">c.</span></span> <span data-ttu-id="7f944-215">Wybierz **Pokaż hasło** i zanotuj wartość **hasło**.</span><span class="sxs-lookup"><span data-stu-id="7f944-215">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="7f944-216">d.</span><span class="sxs-lookup"><span data-stu-id="7f944-216">d.</span></span> <span data-ttu-id="7f944-217">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="7f944-217">Click **Create**.</span></span> 


### <a name="creating-a-github-test-user"></a><span data-ttu-id="7f944-218">Tworzenie użytkownika testowego GitHub</span><span class="sxs-lookup"><span data-stu-id="7f944-218">Creating a GitHub test user</span></span>

<span data-ttu-id="7f944-219">Aby włączyć użytkowników usługi Azure AD zalogować się do usługi GitHub, muszą mieć przydzielone w witrynie GitHub.</span><span class="sxs-lookup"><span data-stu-id="7f944-219">In order to enable Azure AD users to log into GitHub, they must be provisioned into GitHub.</span></span>  
<span data-ttu-id="7f944-220">W przypadku GitHub Inicjowanie obsługi to zadanie ręczne.</span><span class="sxs-lookup"><span data-stu-id="7f944-220">In the case of GitHub, provisioning is a manual task.</span></span>

<span data-ttu-id="7f944-221">**Aby udostępnić konta użytkowników, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="7f944-221">**To provision a user accounts, perform the following steps:**</span></span>

1. <span data-ttu-id="7f944-222">Zaloguj się do witryny GitHub firmy jako administrator.</span><span class="sxs-lookup"><span data-stu-id="7f944-222">Log in to your GitHub company site as an administrator.</span></span>

2. <span data-ttu-id="7f944-223">Kliknij przycisk **osób**.</span><span class="sxs-lookup"><span data-stu-id="7f944-223">Click **People**.</span></span>

    <span data-ttu-id="7f944-224">![Osoby](./media/active-directory-saas-github-tutorial/tutorial_github_config_github_08.png "osób")</span><span class="sxs-lookup"><span data-stu-id="7f944-224">![People](./media/active-directory-saas-github-tutorial/tutorial_github_config_github_08.png "People")</span></span>

3. <span data-ttu-id="7f944-225">Kliknij przycisk **Członkowskie zaproszenia**.</span><span class="sxs-lookup"><span data-stu-id="7f944-225">Click **Invite member**.</span></span>

    <span data-ttu-id="7f944-226">![Zaprosić użytkowników](./media/active-directory-saas-github-tutorial/tutorial_github_config_github_09.png "zaprosić użytkowników")</span><span class="sxs-lookup"><span data-stu-id="7f944-226">![Invite Users](./media/active-directory-saas-github-tutorial/tutorial_github_config_github_09.png "Invite Users")</span></span>

4. <span data-ttu-id="7f944-227">Na **Członkowskie zaproszenia** okna dialogowego strony, należy wykonać następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="7f944-227">On the **Invite member** dialog page, perform the following steps:</span></span>

    <span data-ttu-id="7f944-228">a.</span><span class="sxs-lookup"><span data-stu-id="7f944-228">a.</span></span> <span data-ttu-id="7f944-229">W **E-mail** tekstowym, wpisz adres e-mail konta Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="7f944-229">In the **Email** textbox, type the email address of Britta Simon account.</span></span>

    <span data-ttu-id="7f944-230">![Zaproś inne osoby](./media/active-directory-saas-github-tutorial/tutorial_github_config_github_10.png "Zaproś inne osoby")</span><span class="sxs-lookup"><span data-stu-id="7f944-230">![Invite People](./media/active-directory-saas-github-tutorial/tutorial_github_config_github_10.png "Invite People")</span></span>
    
    <span data-ttu-id="7f944-231">b.</span><span class="sxs-lookup"><span data-stu-id="7f944-231">b.</span></span> <span data-ttu-id="7f944-232">Kliknij przycisk **wysłać zaproszenie**.</span><span class="sxs-lookup"><span data-stu-id="7f944-232">Click **Send Invitation**.</span></span>

    <span data-ttu-id="7f944-233">![Zaproś inne osoby](./media/active-directory-saas-github-tutorial/tutorial_github_config_github_11.png "Zaproś inne osoby")</span><span class="sxs-lookup"><span data-stu-id="7f944-233">![Invite People](./media/active-directory-saas-github-tutorial/tutorial_github_config_github_11.png "Invite People")</span></span>

    > [!NOTE]
    > <span data-ttu-id="7f944-234">Właścicielem konta usługi Azure Active Directory otrzymasz wiadomość e-mail, a następnie kliknij łącze, aby potwierdzić swoje konto, zanim staje się aktywny.</span><span class="sxs-lookup"><span data-stu-id="7f944-234">The Azure Active Directory account holder will receive an email and follow a link to confirm their account before it becomes active.</span></span>


### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="7f944-235">Przypisanie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="7f944-235">Assigning the Azure AD test user</span></span>

<span data-ttu-id="7f944-236">W tej sekcji można włączyć Simona Britta do użycia usługi Azure logowania jednokrotnego za udostępnienie jej do usługi GitHub.</span><span class="sxs-lookup"><span data-stu-id="7f944-236">In this section, you enable Britta Simon to use Azure single sign-on by granting her access to GitHub.</span></span>

![Przypisz użytkownika][200] 

<span data-ttu-id="7f944-238">**Aby przypisać Simona Britta GitHub, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="7f944-238">**To assign Britta Simon to GitHub, perform the following steps:**</span></span>

1. <span data-ttu-id="7f944-239">Otwórz widok aplikacji w portalu zarządzania Azure, a następnie przejdź do widoku katalogu i przejdź do **aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="7f944-239">In the Azure Management portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Przypisz użytkownika][201] 

2. <span data-ttu-id="7f944-241">Na liście aplikacji zaznacz **witryną GitHub.com**.</span><span class="sxs-lookup"><span data-stu-id="7f944-241">In the applications list, select **GitHub.com**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-github-tutorial/tutorial_github_search_result021.png) 

3. <span data-ttu-id="7f944-243">W menu po lewej stronie kliknij **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="7f944-243">In the menu on the left, click **Users and groups**.</span></span>

    ![Przypisz użytkownika][202] 

4. <span data-ttu-id="7f944-245">Kliknij przycisk **Dodaj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="7f944-245">Click **Add** button.</span></span> <span data-ttu-id="7f944-246">Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="7f944-246">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Przypisz użytkownika][203]

5. <span data-ttu-id="7f944-248">Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** na liście Użytkownicy.</span><span class="sxs-lookup"><span data-stu-id="7f944-248">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="7f944-249">Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="7f944-249">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="7f944-250">Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="7f944-250">Click **Assign** button on **Add Assignment** dialog.</span></span>
    


### <a name="testing-single-sign-on"></a><span data-ttu-id="7f944-251">Testowanie rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="7f944-251">Testing single sign-on</span></span>

<span data-ttu-id="7f944-252">W tej sekcji można przetestować konfiguracji usługi Azure AD pojedynczego logowania za pomocą panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="7f944-252">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="7f944-253">Po kliknięciu kafelka GitHub w panelu dostępu użytkownik powinien pobrać zalogowane do aplikacji GitHub.</span><span class="sxs-lookup"><span data-stu-id="7f944-253">When you click the GitHub tile in the Access Panel, you should get signed-on to your GitHub application.</span></span> <span data-ttu-id="7f944-254">Można będzie można logować się jako organizacji konta muszą jednak następnie zaloguj się przy użyciu konta osobistego.</span><span class="sxs-lookup"><span data-stu-id="7f944-254">You'll be logging in as an Organization account but then need to log in with your personal account.</span></span>


## <a name="additional-resources"></a><span data-ttu-id="7f944-255">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="7f944-255">Additional resources</span></span>

* [<span data-ttu-id="7f944-256">Lista samouczków dotyczących sposobów integracji aplikacji SaaS przy użyciu usługi Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="7f944-256">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="7f944-257">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="7f944-257">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-github-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-github-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-github-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-github-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-github-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-github-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-github-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-github-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-github-tutorial/tutorial_general_203.png
