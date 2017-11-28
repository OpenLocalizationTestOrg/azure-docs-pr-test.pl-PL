---
title: "Samouczek: Integracji Azure Active Directory z usługi GitHub | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak tooconfigure logowanie jednokrotne między usługą Azure Active Directory i usługi GitHub."
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
ms.openlocfilehash: 688779de4e6627e49c0e3e8a7576f2f8c7a81ab1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-github"></a><span data-ttu-id="34c3e-103">Samouczek: Integracji Azure Active Directory z usługi GitHub</span><span class="sxs-lookup"><span data-stu-id="34c3e-103">Tutorial: Azure Active Directory integration with GitHub</span></span>

<span data-ttu-id="34c3e-104">Z tego samouczka, dowiesz się, jak toointegrate GitHub z usługą Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="34c3e-104">In this tutorial, you learn how toointegrate GitHub with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="34c3e-105">Integracja z usługą Azure AD GitHub udostępnia hello następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="34c3e-105">Integrating GitHub with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="34c3e-106">Można kontrolować w usłudze Azure AD, kto ma dostęp do tooGitHub</span><span class="sxs-lookup"><span data-stu-id="34c3e-106">You can control in Azure AD who has access tooGitHub</span></span>
- <span data-ttu-id="34c3e-107">Można włączyć użytkownika użytkownicy tooautomatically get zalogowane tooGitHub (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="34c3e-107">You can enable your users tooautomatically get signed-on tooGitHub (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="34c3e-108">Możesz zarządzać kont w jednej centralnej lokalizacji - hello portalu zarządzania Azure</span><span class="sxs-lookup"><span data-stu-id="34c3e-108">You can manage your accounts in one central location - hello Azure Management portal</span></span>

<span data-ttu-id="34c3e-109">Jeśli chcesz tooknow więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="34c3e-109">If you want tooknow more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="34c3e-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="34c3e-110">Prerequisites</span></span>

<span data-ttu-id="34c3e-111">tooconfigure integracji z usługą Azure AD z usługi GitHub należy hello następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="34c3e-111">tooconfigure Azure AD integration with GitHub, you need hello following items:</span></span>

- <span data-ttu-id="34c3e-112">Subskrypcję usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="34c3e-112">An Azure AD subscription</span></span>
- <span data-ttu-id="34c3e-113">GitHub jednokrotnego włączone subskrypcji</span><span class="sxs-lookup"><span data-stu-id="34c3e-113">A GitHub single-sign on enabled subscription</span></span>


> [!NOTE]
> <span data-ttu-id="34c3e-114">tootest hello kroków w tym samouczku, zaleca się przy użyciu środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="34c3e-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>


<span data-ttu-id="34c3e-115">tootest hello kroki opisane w tym samouczku, należy stosować te zalecenia:</span><span class="sxs-lookup"><span data-stu-id="34c3e-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="34c3e-116">Nie należy używać środowiska produkcyjnego, chyba że jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="34c3e-116">You should not use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="34c3e-117">Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz pobrać miesięczna wersja próbna [tutaj](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="34c3e-117">If you don't have an Azure AD trial environment, you can get an one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>


## <a name="scenario-description"></a><span data-ttu-id="34c3e-118">Opis scenariusza</span><span class="sxs-lookup"><span data-stu-id="34c3e-118">Scenario description</span></span>
<span data-ttu-id="34c3e-119">W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym.</span><span class="sxs-lookup"><span data-stu-id="34c3e-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="34c3e-120">Scenariusz Hello opisane w tym samouczku składa się z dwóch głównych elementów:</span><span class="sxs-lookup"><span data-stu-id="34c3e-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="34c3e-121">Dodawanie GitHub z galerii hello</span><span class="sxs-lookup"><span data-stu-id="34c3e-121">Adding GitHub from hello gallery</span></span>
2. <span data-ttu-id="34c3e-122">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="34c3e-122">Configuring and testing Azure AD single sign-on</span></span>


## <a name="adding-github-from-hello-gallery"></a><span data-ttu-id="34c3e-123">Dodawanie GitHub z galerii hello</span><span class="sxs-lookup"><span data-stu-id="34c3e-123">Adding GitHub from hello gallery</span></span>
<span data-ttu-id="34c3e-124">tooconfigure hello integracji GitHub z usługą Azure AD, należy tooadd GitHub z hello galerii tooyour listę zarządzanych aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="34c3e-124">tooconfigure hello integration of GitHub into Azure AD, you need tooadd GitHub from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="34c3e-125">**tooadd GitHub z galerii hello, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="34c3e-125">**tooadd GitHub from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="34c3e-126">W hello  **[portalu zarządzania Azure](https://portal.azure.com)**na temat hello panelu nawigacji po lewej stronie, kliknij przycisk **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="34c3e-126">In hello **[Azure Management Portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Usługa Active Directory][1]

2. <span data-ttu-id="34c3e-128">Przejdź za**aplikacje dla przedsiębiorstw**.</span><span class="sxs-lookup"><span data-stu-id="34c3e-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="34c3e-129">Następnie przejdź zbyt**wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="34c3e-129">Then go too**All applications**.</span></span>

    ![Aplikacje][2]
    
3. <span data-ttu-id="34c3e-131">Kliknij przycisk **Dodaj** przycisk u góry hello hello okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="34c3e-131">Click **Add** button on hello top of hello dialog.</span></span>

    ![Aplikacje][3]

4. <span data-ttu-id="34c3e-133">W polu wyszukiwania hello wpisz **witryną GitHub.com**.</span><span class="sxs-lookup"><span data-stu-id="34c3e-133">In hello search box, type **GitHub.com**.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-github-tutorial/tutorial_github_search02.png)

5. <span data-ttu-id="34c3e-135">W panelu wyników hello zaznacz **GitHub**, a następnie kliknij przycisk **Dodaj** przycisk aplikacji hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="34c3e-135">In hello results panel, select **GitHub**, and then click **Add** button tooadd hello application.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-github-tutorial/tutorial_github_search_result02.png)


##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="34c3e-137">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="34c3e-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="34c3e-138">W tej sekcji skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z usługi GitHub w oparciu o nazwie "Britta Simona" użytkownika testowego.</span><span class="sxs-lookup"><span data-stu-id="34c3e-138">In this section, you configure and test Azure AD single sign-on with GitHub based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="34c3e-139">Dla pojedynczego logowania jednokrotnego toowork usługi Azure AD musi tooknow hello odpowiednikiem użytkownika w usłudze GitHub jest tooa użytkownika w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="34c3e-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in GitHub is tooa user in Azure AD.</span></span> <span data-ttu-id="34c3e-140">Innymi słowy relację łącza między użytkownika usługi Azure AD i hello użytkownikowi w serwisie GitHub musi toobe ustanowione.</span><span class="sxs-lookup"><span data-stu-id="34c3e-140">In other words, a link relationship between an Azure AD user and hello related user in GitHub needs toobe established.</span></span>

<span data-ttu-id="34c3e-141">Ta relacja łącza zostanie nawiązane, przypisując wartość hello hello **nazwy użytkownika** w usłudze Azure AD jako wartość hello hello **Username** w serwisie GitHub.</span><span class="sxs-lookup"><span data-stu-id="34c3e-141">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in GitHub.</span></span>

<span data-ttu-id="34c3e-142">tooconfigure i testowych usługi Azure AD rejestracji jednokrotnej z usługi GitHub, należy po bloków konstrukcyjnych hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="34c3e-142">tooconfigure and test Azure AD single sign-on with GitHub, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="34c3e-143">**[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configuring-azure-ad-single-sign-on)**  -tooenable Twojego toouse użytkowników tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="34c3e-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="34c3e-144">**[Tworzenie użytkownika testowego usługi Azure AD](#creating-an-azure-ad-test-user)**  -tootest usługi Azure AD rejestracji jednokrotnej z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="34c3e-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="34c3e-145">**[Tworzenie użytkownika testowego GitHub](#creating-a-GitHub-test-user)**  -toohave odpowiednikiem Simona Britta w usłudze GitHub, że jego reprezentacja toohello połączonej usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="34c3e-145">**[Creating a GitHub test user](#creating-a-GitHub-test-user)** - toohave a counterpart of Britta Simon in GitHub that is linked toohello Azure AD representation of her.</span></span>
4. <span data-ttu-id="34c3e-146">**[Przypisanie użytkownika testowego hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Simona Britta toouse usługi Azure AD rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="34c3e-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="34c3e-147">**[Testowanie rejestracji jednokrotnej](#testing-single-sign-on)**  -tooverify czy hello konfiguracji działania.</span><span class="sxs-lookup"><span data-stu-id="34c3e-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="34c3e-148">Konfigurowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="34c3e-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="34c3e-149">W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w portalu zarządzania Azure hello i skonfigurować logowanie jednokrotne w aplikacji GitHub.</span><span class="sxs-lookup"><span data-stu-id="34c3e-149">In this section, you enable Azure AD single sign-on in hello Azure Management portal and configure single sign-on in your GitHub application.</span></span>

<span data-ttu-id="34c3e-150">**tooconfigure usługi Azure AD rejestracji jednokrotnej z usługi GitHub, wykonaj hello następujące kroki:**</span><span class="sxs-lookup"><span data-stu-id="34c3e-150">**tooconfigure Azure AD single sign-on with GitHub, perform hello following steps:**</span></span>

1. <span data-ttu-id="34c3e-151">W portalu zarządzania Azure hello na powitania **GitHub** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.</span><span class="sxs-lookup"><span data-stu-id="34c3e-151">In hello Azure Management portal, on hello **GitHub** application integration page, click **Single sign-on**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej][4]

2. <span data-ttu-id="34c3e-153">Na powitania **logowanie jednokrotne** okna dialogowego, jako **tryb** wybierz **na języku SAML logowania jednokrotnego** tooenable logowania jednokrotnego.</span><span class="sxs-lookup"><span data-stu-id="34c3e-153">On hello **Single sign-on** dialog, as **Mode** select **SAML-based Sign-on** tooenable single sign on.</span></span>
 
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-github-tutorial/tutorial_github_01.png)

3. <span data-ttu-id="34c3e-155">Na powitania **GitHub domeny i adres URL** sekcji, wykonaj następujące kroki hello:</span><span class="sxs-lookup"><span data-stu-id="34c3e-155">On hello **GitHub Domain and URLs** section, perform hello following steps:</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-github-tutorial/tutorial_github_saml011.png)

    <span data-ttu-id="34c3e-157">a.</span><span class="sxs-lookup"><span data-stu-id="34c3e-157">a.</span></span> <span data-ttu-id="34c3e-158">W hello **adres URL logowania** pole tekstowe, wartość hello typu jako:`https://github.com/orgs/<entity-id>/sso`</span><span class="sxs-lookup"><span data-stu-id="34c3e-158">In hello **Sign-on URL** textbox, type hello value as: `https://github.com/orgs/<entity-id>/sso`</span></span>

    <span data-ttu-id="34c3e-159">b.</span><span class="sxs-lookup"><span data-stu-id="34c3e-159">b.</span></span> <span data-ttu-id="34c3e-160">W hello **identyfikator** tekstowym, wpisz adres URL za pomocą hello następującego wzorca:`https://github.com/orgs/<entity-id>`</span><span class="sxs-lookup"><span data-stu-id="34c3e-160">In hello **Identifier** textbox, type a URL using hello following pattern: `https://github.com/orgs/<entity-id>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="34c3e-161">Należy pamiętać, że nie są one hello wartości rzeczywistych.</span><span class="sxs-lookup"><span data-stu-id="34c3e-161">Please note that these are not hello real values.</span></span> <span data-ttu-id="34c3e-162">Masz tooupdate tych wartości za pomocą hello rzeczywiste uwagi na adres URL i identyfikator.</span><span class="sxs-lookup"><span data-stu-id="34c3e-162">You have tooupdate these values with hello actual Sing-on URL and Identifier.</span></span> <span data-ttu-id="34c3e-163">W tym miejscu zalecamy możesz toouse hello unikatową wartość ciągu w hello identyfikator.</span><span class="sxs-lookup"><span data-stu-id="34c3e-163">Here we suggest you toouse hello unique value of string in hello Identifier.</span></span> <span data-ttu-id="34c3e-164">Przejdź tooretrieve sekcji administracyjnej tooGitHub tych wartości.</span><span class="sxs-lookup"><span data-stu-id="34c3e-164">Go tooGitHub Admin section tooretrieve these values.</span></span> 

4. <span data-ttu-id="34c3e-165">Na powitania **atrybuty użytkownika** zaznacz **identyfikator użytkownika** jako user.mail.</span><span class="sxs-lookup"><span data-stu-id="34c3e-165">On hello **User Attributes** section, select **User Identifier** as user.mail.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-github-tutorial/tutorial_github_attribute_new01.png)
    
5. <span data-ttu-id="34c3e-167">Na powitania **certyfikat podpisywania SAML** kliknij **Utwórz nowy certyfikat**.</span><span class="sxs-lookup"><span data-stu-id="34c3e-167">On hello **SAML Signing Certificate** section, click **Create new certificate**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-github-tutorial/tutorial_github_03.png)

6. <span data-ttu-id="34c3e-169">Na powitania **Tworzenie nowego świadectwa** okna dialogowego, kliknij ikonę kalendarza hello i wybierz **Data wygaśnięcia**.</span><span class="sxs-lookup"><span data-stu-id="34c3e-169">On hello **Create New Certificate** dialog, click hello calendar icon and select an **expiry date**.</span></span> <span data-ttu-id="34c3e-170">Następnie kliknij przycisk **zapisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="34c3e-170">Then click **Save** button.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-github-tutorial/tutorial_general_300.png)

7. <span data-ttu-id="34c3e-172">Na powitania **certyfikat podpisywania SAML** wybierz opcję **uaktywnić nowego świadectwa** i kliknij przycisk **zapisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="34c3e-172">On hello **SAML Signing Certificate** section, select **Make new certificate active** and click **Save** button.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-github-tutorial/tutorial_github_04.png)

8. <span data-ttu-id="34c3e-174">W oknie podręcznym hello **certyfikat przerzucania** okna, kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="34c3e-174">On hello pop-up **Rollover certificate** window, click **OK**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-github-tutorial/tutorial_general_400.png)

9. <span data-ttu-id="34c3e-176">Na powitania **certyfikat podpisywania SAML** kliknij **certyfikatu (Base64)** , a następnie zapisz plik certyfikatu hello na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="34c3e-176">On hello **SAML Signing Certificate** section, click **Certificate (Base64)** and then save hello certificate file on your computer.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-github-tutorial/tutorial_github_05.png) 

10. <span data-ttu-id="34c3e-178">Na powitania **konfiguracji GitHub** kliknij **skonfigurować GitHub** tooopen **Konfigurowanie logowania jednokrotnego** okna.</span><span class="sxs-lookup"><span data-stu-id="34c3e-178">On hello **GitHub Configuration** section, click **Configure GitHub** tooopen **Configure sign-on** window.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-github-tutorial/tutorial_github_06.png) 

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-github-tutorial/tutorial_github_07.png)

11. <span data-ttu-id="34c3e-181">W oknie przeglądarki innej witryny sieci web Zaloguj się do witryny GitHub organizacji jako administrator.</span><span class="sxs-lookup"><span data-stu-id="34c3e-181">In a different web browser window, log into your GitHub organization site as an administrator.</span></span>

12. <span data-ttu-id="34c3e-182">Przejdź za**ustawienia** i kliknij przycisk **zabezpieczeń**</span><span class="sxs-lookup"><span data-stu-id="34c3e-182">Navigate too**Settings** and click **Security**</span></span>

    ![Ustawienia](./media/active-directory-saas-github-tutorial/tutorial_github_config_github_03.png)

13. <span data-ttu-id="34c3e-184">Sprawdź hello **uwierzytelnianie Włącz SAML** pole ujawniania hello rejestracji jednokrotnej pola konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="34c3e-184">Check hello **Enable SAML authentication** box, revealing hello Single Sign-on configuration fields.</span></span> <span data-ttu-id="34c3e-185">Następnie należy użyć hello pojedynczego adresu URL wartość tooupdate hello pojedynczego logowania jednokrotnego adres URL logowania w konfiguracji usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="34c3e-185">Then, use hello single sign-on URL value tooupdate hello Single sign-on URL on Azure AD configuration.</span></span>

    ![Ustawienia](./media/active-directory-saas-github-tutorial/tutorial_github_config_github_13.png)

14. <span data-ttu-id="34c3e-187">Skonfiguruj hello następujące pola:</span><span class="sxs-lookup"><span data-stu-id="34c3e-187">Configure hello following fields:</span></span>

    <span data-ttu-id="34c3e-188">a.</span><span class="sxs-lookup"><span data-stu-id="34c3e-188">a.</span></span> <span data-ttu-id="34c3e-189">**Zaloguj się na adres URL**: wprowadź **SAML rejestracji jednokrotnej adres URL usługi** z hello **skonfigurować GitHub** sekcję na temat usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="34c3e-189">**Sign on URL**: Enter **SAML Single sign-on Service URL** from hello **Configure GitHub** section on Azure AD</span></span>

    <span data-ttu-id="34c3e-190">b.</span><span class="sxs-lookup"><span data-stu-id="34c3e-190">b.</span></span> <span data-ttu-id="34c3e-191">**Wystawca**: wprowadź **identyfikator jednostki SAML** z hello **skonfigurować GitHub** sekcję na temat usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="34c3e-191">**Issuer**: Enter **SAML Entity ID** from hello **Configure GitHub** section on Azure AD</span></span>

    <span data-ttu-id="34c3e-192">c.</span><span class="sxs-lookup"><span data-stu-id="34c3e-192">c.</span></span> <span data-ttu-id="34c3e-193">**Certyfikat publiczny**: Otwórz hello pobrać certyfikatu z usługi Azure AD w programie Notatnik i skopiuj zawartości hello tym "BEGIN certyfikatu" i "END CERTIFICATE"</span><span class="sxs-lookup"><span data-stu-id="34c3e-193">**Public Certificate**: Open hello downloaded certificate from Azure AD in a notepad and copy hello content including "BEGIN CERTIFICATE" and "END CERTIFICATE"</span></span>

    ![Ustawienia](./media/active-directory-saas-github-tutorial/tutorial_github_config_github_051.png)

15. <span data-ttu-id="34c3e-195">Polecenie **konfiguracji testu SAML** tooconfirm że nie wystąpiły błędy sprawdzania poprawności lub błędy podczas rejestracji Jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="34c3e-195">Click on **Test SAML configuration** tooconfirm that no validation failures or errors during SSO.</span></span>

    ![Ustawienia](./media/active-directory-saas-github-tutorial/tutorial_github_config_github_06.png)

16. <span data-ttu-id="34c3e-197">Kliknij przycisk **Zapisz**</span><span class="sxs-lookup"><span data-stu-id="34c3e-197">Click **Save**</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="34c3e-198">Tworzenie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="34c3e-198">Creating an Azure AD test user</span></span>
<span data-ttu-id="34c3e-199">Celem Hello w tej sekcji jest toocreate użytkownika testowego, w portalu zarządzania Azure hello o nazwie Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="34c3e-199">hello objective of this section is toocreate a test user in hello Azure Management portal called Britta Simon.</span></span>

![Tworzenie użytkowników usługi Azure AD][100]

<span data-ttu-id="34c3e-201">**toocreate użytkownika testowego w usłudze Azure AD, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="34c3e-201">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="34c3e-202">W hello **portalu zarządzania Azure**na temat hello w lewym okienku nawigacji, kliknij przycisk **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="34c3e-202">In hello **Azure Management portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-github-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="34c3e-204">Przejdź za**użytkowników i grup** i kliknij przycisk **wszyscy użytkownicy** toodisplay hello listy użytkowników.</span><span class="sxs-lookup"><span data-stu-id="34c3e-204">Go too**Users and groups** and click **All users** toodisplay hello list of users.</span></span>
    
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-github-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="34c3e-206">U góry okna dialogowego hello powitania kliknij **Dodaj** tooopen hello **użytkownika** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="34c3e-206">At hello top of hello dialog click **Add** tooopen hello **User** dialog.</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-github-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="34c3e-208">Na powitania **użytkownika** okna dialogowego wykonaj hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="34c3e-208">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-github-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="34c3e-210">a.</span><span class="sxs-lookup"><span data-stu-id="34c3e-210">a.</span></span> <span data-ttu-id="34c3e-211">W hello **nazwa** pole tekstowe, typ **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="34c3e-211">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="34c3e-212">b.</span><span class="sxs-lookup"><span data-stu-id="34c3e-212">b.</span></span> <span data-ttu-id="34c3e-213">W hello **nazwy użytkownika** pole tekstowe, hello typu **adres e-mail** z BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="34c3e-213">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="34c3e-214">c.</span><span class="sxs-lookup"><span data-stu-id="34c3e-214">c.</span></span> <span data-ttu-id="34c3e-215">Wybierz **Pokaż hasło** i zanotuj wartość hello hello **hasło**.</span><span class="sxs-lookup"><span data-stu-id="34c3e-215">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="34c3e-216">d.</span><span class="sxs-lookup"><span data-stu-id="34c3e-216">d.</span></span> <span data-ttu-id="34c3e-217">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="34c3e-217">Click **Create**.</span></span> 


### <a name="creating-a-github-test-user"></a><span data-ttu-id="34c3e-218">Tworzenie użytkownika testowego GitHub</span><span class="sxs-lookup"><span data-stu-id="34c3e-218">Creating a GitHub test user</span></span>

<span data-ttu-id="34c3e-219">W kolejności tooenable usługi Azure AD użytkownicy toolog w witrynie GitHub muszą mieć przydzielone w witrynie GitHub.</span><span class="sxs-lookup"><span data-stu-id="34c3e-219">In order tooenable Azure AD users toolog into GitHub, they must be provisioned into GitHub.</span></span>  
<span data-ttu-id="34c3e-220">W przypadku hello GitHub Inicjowanie obsługi to zadanie ręczne.</span><span class="sxs-lookup"><span data-stu-id="34c3e-220">In hello case of GitHub, provisioning is a manual task.</span></span>

<span data-ttu-id="34c3e-221">**tooprovision kont użytkowników, wykonaj hello następujące kroki:**</span><span class="sxs-lookup"><span data-stu-id="34c3e-221">**tooprovision a user accounts, perform hello following steps:**</span></span>

1. <span data-ttu-id="34c3e-222">Zaloguj się za tooyour GitHub witryny firmy jako administrator.</span><span class="sxs-lookup"><span data-stu-id="34c3e-222">Log in tooyour GitHub company site as an administrator.</span></span>

2. <span data-ttu-id="34c3e-223">Kliknij przycisk **osób**.</span><span class="sxs-lookup"><span data-stu-id="34c3e-223">Click **People**.</span></span>

    <span data-ttu-id="34c3e-224">![Osoby](./media/active-directory-saas-github-tutorial/tutorial_github_config_github_08.png "osób")</span><span class="sxs-lookup"><span data-stu-id="34c3e-224">![People](./media/active-directory-saas-github-tutorial/tutorial_github_config_github_08.png "People")</span></span>

3. <span data-ttu-id="34c3e-225">Kliknij przycisk **Członkowskie zaproszenia**.</span><span class="sxs-lookup"><span data-stu-id="34c3e-225">Click **Invite member**.</span></span>

    <span data-ttu-id="34c3e-226">![Zaprosić użytkowników](./media/active-directory-saas-github-tutorial/tutorial_github_config_github_09.png "zaprosić użytkowników")</span><span class="sxs-lookup"><span data-stu-id="34c3e-226">![Invite Users](./media/active-directory-saas-github-tutorial/tutorial_github_config_github_09.png "Invite Users")</span></span>

4. <span data-ttu-id="34c3e-227">Na powitania **Członkowskie zaproszenia** okna dialogowego wykonaj hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="34c3e-227">On hello **Invite member** dialog page, perform hello following steps:</span></span>

    <span data-ttu-id="34c3e-228">a.</span><span class="sxs-lookup"><span data-stu-id="34c3e-228">a.</span></span> <span data-ttu-id="34c3e-229">W hello **E-mail** pole tekstowe, adres e-mail hello typu Simona Britta konta.</span><span class="sxs-lookup"><span data-stu-id="34c3e-229">In hello **Email** textbox, type hello email address of Britta Simon account.</span></span>

    <span data-ttu-id="34c3e-230">![Zaproś inne osoby](./media/active-directory-saas-github-tutorial/tutorial_github_config_github_10.png "Zaproś inne osoby")</span><span class="sxs-lookup"><span data-stu-id="34c3e-230">![Invite People](./media/active-directory-saas-github-tutorial/tutorial_github_config_github_10.png "Invite People")</span></span>
    
    <span data-ttu-id="34c3e-231">b.</span><span class="sxs-lookup"><span data-stu-id="34c3e-231">b.</span></span> <span data-ttu-id="34c3e-232">Kliknij przycisk **wysłać zaproszenie**.</span><span class="sxs-lookup"><span data-stu-id="34c3e-232">Click **Send Invitation**.</span></span>

    <span data-ttu-id="34c3e-233">![Zaproś inne osoby](./media/active-directory-saas-github-tutorial/tutorial_github_config_github_11.png "Zaproś inne osoby")</span><span class="sxs-lookup"><span data-stu-id="34c3e-233">![Invite People](./media/active-directory-saas-github-tutorial/tutorial_github_config_github_11.png "Invite People")</span></span>

    > [!NOTE]
    > <span data-ttu-id="34c3e-234">właścicielem konta usługi Azure Active Directory Hello będzie otrzymywać wiadomości e-mail i postępuj zgodnie tooconfirm łącze swojego konta przed staje się aktywny.</span><span class="sxs-lookup"><span data-stu-id="34c3e-234">hello Azure Active Directory account holder will receive an email and follow a link tooconfirm their account before it becomes active.</span></span>


### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="34c3e-235">Przypisanie użytkownika testowego hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="34c3e-235">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="34c3e-236">W tej sekcji możesz włączyć toouse Simona Britta Azure logowania jednokrotnego za udzielanie jej tooGitHub dostępu.</span><span class="sxs-lookup"><span data-stu-id="34c3e-236">In this section, you enable Britta Simon toouse Azure single sign-on by granting her access tooGitHub.</span></span>

![Przypisz użytkownika][200] 

<span data-ttu-id="34c3e-238">**tooassign tooGitHub Simona Britta wykonaj hello następujące kroki:**</span><span class="sxs-lookup"><span data-stu-id="34c3e-238">**tooassign Britta Simon tooGitHub, perform hello following steps:**</span></span>

1. <span data-ttu-id="34c3e-239">W portalu zarządzania Azure hello, otwórz widok aplikacji hello, a następnie przejdź widok katalogu toohello i go za**aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="34c3e-239">In hello Azure Management portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Przypisz użytkownika][201] 

2. <span data-ttu-id="34c3e-241">Z listy aplikacji hello wybierz **witryną GitHub.com**.</span><span class="sxs-lookup"><span data-stu-id="34c3e-241">In hello applications list, select **GitHub.com**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-github-tutorial/tutorial_github_search_result021.png) 

3. <span data-ttu-id="34c3e-243">W menu powitania po lewej stronie powitania kliknij **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="34c3e-243">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Przypisz użytkownika][202] 

4. <span data-ttu-id="34c3e-245">Kliknij przycisk **Dodaj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="34c3e-245">Click **Add** button.</span></span> <span data-ttu-id="34c3e-246">Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="34c3e-246">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Przypisz użytkownika][203]

5. <span data-ttu-id="34c3e-248">Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** hello listy użytkowników.</span><span class="sxs-lookup"><span data-stu-id="34c3e-248">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="34c3e-249">Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="34c3e-249">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="34c3e-250">Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="34c3e-250">Click **Assign** button on **Add Assignment** dialog.</span></span>
    


### <a name="testing-single-sign-on"></a><span data-ttu-id="34c3e-251">Testowanie rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="34c3e-251">Testing single sign-on</span></span>

<span data-ttu-id="34c3e-252">W tej sekcji można przetestować konfiguracji usługi Azure AD pojedynczego logowania jednokrotnego przy użyciu hello panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="34c3e-252">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="34c3e-253">Po kliknięciu kafelka GitHub hello w hello Panel dostępu, należy pobrać zalogowane tooyour GitHub aplikacji.</span><span class="sxs-lookup"><span data-stu-id="34c3e-253">When you click hello GitHub tile in hello Access Panel, you should get signed-on tooyour GitHub application.</span></span> <span data-ttu-id="34c3e-254">Można będzie można logować się jako konta organizacji, ale następnie toolog muszą się przy użyciu konta osobistego.</span><span class="sxs-lookup"><span data-stu-id="34c3e-254">You'll be logging in as an Organization account but then need toolog in with your personal account.</span></span>


## <a name="additional-resources"></a><span data-ttu-id="34c3e-255">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="34c3e-255">Additional resources</span></span>

* [<span data-ttu-id="34c3e-256">Lista samouczków dotyczących tooIntegrate aplikacji SaaS w usłudze Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="34c3e-256">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="34c3e-257">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="34c3e-257">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



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
