---
title: "Samouczek: Azure Active Directory integrację z klientem Gorilla ziemi | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak tooconfigure logowanie jednokrotne między usługą Azure Active Directory i Gorilla ziemi."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 28acce3e-22a0-4a37-8b66-6e518d777350
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/13/2017
ms.author: jeedes
ms.openlocfilehash: e95a30551e636108fe22a7ab6d1827bc12d7f9a0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-land-gorilla-client"></a><span data-ttu-id="99ae5-103">Samouczek: Integracji Azure Active Directory z ziemi Gorilla klienta</span><span class="sxs-lookup"><span data-stu-id="99ae5-103">Tutorial: Azure Active Directory integration with Land Gorilla Client</span></span>

<span data-ttu-id="99ae5-104">Z tego samouczka, dowiesz się, jak toointegrate ziemi Gorilla klienta z usługą Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="99ae5-104">In this tutorial, you learn how toointegrate Land Gorilla Client with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="99ae5-105">Integrowanie ziemi Gorilla klienta z usługi Azure AD zapewnia hello następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="99ae5-105">Integrating Land Gorilla Client with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="99ae5-106">Można kontrolować w usłudze Azure AD, kto ma dostęp tooLand Gorilla klienta</span><span class="sxs-lookup"><span data-stu-id="99ae5-106">You can control in Azure AD who has access tooLand Gorilla Client</span></span>
- <span data-ttu-id="99ae5-107">Można włączyć użytkownika użytkownicy tooautomatically get zalogowane tooLand Gorilla klienta (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="99ae5-107">You can enable your users tooautomatically get signed-on tooLand Gorilla Client (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="99ae5-108">Możesz zarządzać kont w jednej centralnej lokalizacji - hello portalu zarządzania Azure</span><span class="sxs-lookup"><span data-stu-id="99ae5-108">You can manage your accounts in one central location - hello Azure Management portal</span></span>

<span data-ttu-id="99ae5-109">Jeśli chcesz tooknow więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="99ae5-109">If you want tooknow more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>


## <a name="prerequisites"></a><span data-ttu-id="99ae5-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="99ae5-110">Prerequisites</span></span>

<span data-ttu-id="99ae5-111">tooconfigure integrację usługi Azure AD z klientem Gorilla ziemi, należy hello następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="99ae5-111">tooconfigure Azure AD integration with Land Gorilla Client, you need hello following items:</span></span>

- <span data-ttu-id="99ae5-112">Subskrypcję usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="99ae5-112">An Azure AD subscription</span></span>
- <span data-ttu-id="99ae5-113">Klient Gorilla ziemi jednokrotnego włączone subskrypcji</span><span class="sxs-lookup"><span data-stu-id="99ae5-113">A Land Gorilla Client single-sign on enabled subscription</span></span>


> [!NOTE]
> <span data-ttu-id="99ae5-114">tootest hello kroków w tym samouczku, zaleca się przy użyciu środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="99ae5-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>


<span data-ttu-id="99ae5-115">tootest hello kroki opisane w tym samouczku, należy stosować te zalecenia:</span><span class="sxs-lookup"><span data-stu-id="99ae5-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="99ae5-116">Nie należy używać środowiska produkcyjnego, chyba że jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="99ae5-116">You should not use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="99ae5-117">Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz pobrać miesięczna wersja próbna [tutaj](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="99ae5-117">If you don't have an Azure AD trial environment, you can get an one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>


## <a name="scenario-description"></a><span data-ttu-id="99ae5-118">Opis scenariusza</span><span class="sxs-lookup"><span data-stu-id="99ae5-118">Scenario description</span></span>
<span data-ttu-id="99ae5-119">W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym.</span><span class="sxs-lookup"><span data-stu-id="99ae5-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="99ae5-120">Scenariusz Hello opisane w tym samouczku składa się z dwóch głównych elementów:</span><span class="sxs-lookup"><span data-stu-id="99ae5-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="99ae5-121">Dodawanie klienta Gorilla ziemi z galerii hello</span><span class="sxs-lookup"><span data-stu-id="99ae5-121">Adding Land Gorilla Client from hello gallery</span></span>
2. <span data-ttu-id="99ae5-122">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="99ae5-122">Configuring and testing Azure AD single sign-on</span></span>


## <a name="adding-land-gorilla-client-from-hello-gallery"></a><span data-ttu-id="99ae5-123">Dodawanie klienta Gorilla ziemi z galerii hello</span><span class="sxs-lookup"><span data-stu-id="99ae5-123">Adding Land Gorilla Client from hello gallery</span></span>
<span data-ttu-id="99ae5-124">tooconfigure hello integracji ziemi Gorilla klienta do usługi Azure AD, potrzebujesz ziemi tooadd Gorilla klienta z hello galerii tooyour listę zarządzanych aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="99ae5-124">tooconfigure hello integration of Land Gorilla Client into Azure AD, you need tooadd Land Gorilla Client from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="99ae5-125">**tooadd ziemi Gorilla klienta z galerii hello wykonaj hello następujące kroki:**</span><span class="sxs-lookup"><span data-stu-id="99ae5-125">**tooadd Land Gorilla Client from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="99ae5-126">W hello  **[portalu zarządzania Azure](https://portal.azure.com)**na temat hello panelu nawigacji po lewej stronie, kliknij przycisk **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="99ae5-126">In hello **[Azure Management Portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Usługa Active Directory][1]

2. <span data-ttu-id="99ae5-128">Przejdź za**aplikacje dla przedsiębiorstw**.</span><span class="sxs-lookup"><span data-stu-id="99ae5-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="99ae5-129">Następnie przejdź zbyt**wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="99ae5-129">Then go too**All applications**.</span></span>

    ![Aplikacje][2]
    
3. <span data-ttu-id="99ae5-131">Kliknij przycisk **Dodaj** przycisk u góry hello hello okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="99ae5-131">Click **Add** button on hello top of hello dialog.</span></span>

    ![Aplikacje][3]

4. <span data-ttu-id="99ae5-133">W polu wyszukiwania hello wpisz **klienta Gorilla ziemi**.</span><span class="sxs-lookup"><span data-stu-id="99ae5-133">In hello search box, type **Land Gorilla Client**.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-landgorilla-tutorial/tutorial_landgorilla_search.png)

5. <span data-ttu-id="99ae5-135">W panelu wyników hello, wybierz **klienta Gorilla ziemi**, a następnie kliknij przycisk **Dodaj** przycisk aplikacji hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="99ae5-135">In hello results panel, select **Land Gorilla Client**, and then click **Add** button tooadd hello application.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-landgorilla-tutorial/tutorial_landgorilla_addfromgallery.png)


##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="99ae5-137">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="99ae5-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="99ae5-138">W tej sekcji skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z klientem Gorilla ziemi w oparciu o nazwie "Britta Simona" użytkownika testowego.</span><span class="sxs-lookup"><span data-stu-id="99ae5-138">In this section, you configure and test Azure AD single sign-on with Land Gorilla Client based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="99ae5-139">Dla pojedynczego logowania jednokrotnego toowork usługi Azure AD musi tooknow użytkownika odpowiednikiem powitania klienta Gorilla ziemi jest tooa użytkownika w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="99ae5-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Land Gorilla Client is tooa user in Azure AD.</span></span> <span data-ttu-id="99ae5-140">Innymi słowy relację łącza między użytkownika usługi Azure AD i hello użytkownikowi w kliencie Gorilla ziemi musi toobe ustanowione.</span><span class="sxs-lookup"><span data-stu-id="99ae5-140">In other words, a link relationship between an Azure AD user and hello related user in Land Gorilla Client needs toobe established.</span></span>

<span data-ttu-id="99ae5-141">Ta relacja łącza zostanie nawiązane, przypisując wartość hello hello **nazwy użytkownika** w usłudze Azure AD jako wartość hello hello **Username** w kliencie Gorilla ziemi.</span><span class="sxs-lookup"><span data-stu-id="99ae5-141">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in Land Gorilla Client.</span></span>

<span data-ttu-id="99ae5-142">tooconfigure i testowych usługi Azure AD rejestracji jednokrotnej z klientem Gorilla ziemi, należy po bloków konstrukcyjnych hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="99ae5-142">tooconfigure and test Azure AD single sign-on with Land Gorilla Client, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="99ae5-143">**[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configuring-azure-ad-single-sign-on)**  -tooenable Twojego toouse użytkowników tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="99ae5-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="99ae5-144">**[Tworzenie użytkownika testowego usługi Azure AD](#creating-an-azure-ad-test-user)**  -tootest usługi Azure AD rejestracji jednokrotnej z grupą ograniczone.</span><span class="sxs-lookup"><span data-stu-id="99ae5-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with limited group.</span></span>
3. <span data-ttu-id="99ae5-145">**[Tworzenie użytkownika testowego Gorilla ziemi](#creating-a-land-gorilla-test-user)**  -tootest usługi Azure AD rejestracji jednokrotnej z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="99ae5-145">**[Creating a Land Gorilla test user](#creating-a-land-gorilla-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
4. <span data-ttu-id="99ae5-146">**[Przypisanie użytkownika testowego hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Simona Britta toouse usługi Azure AD rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="99ae5-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="99ae5-147">**[Testowanie rejestracji jednokrotnej](#testing-single-sign-on)**  -tooverify czy hello konfiguracji działania.</span><span class="sxs-lookup"><span data-stu-id="99ae5-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="99ae5-148">Konfigurowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="99ae5-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="99ae5-149">W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w portalu zarządzania Azure hello i skonfigurować logowanie jednokrotne w aplikacji klienta Gorilla ziemi.</span><span class="sxs-lookup"><span data-stu-id="99ae5-149">In this section, you enable Azure AD single sign-on in hello Azure Management portal and configure single sign-on in your Land Gorilla Client application.</span></span>

<span data-ttu-id="99ae5-150">**tooconfigure usługi Azure AD rejestracji jednokrotnej z klientem Gorilla ziemi, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="99ae5-150">**tooconfigure Azure AD single sign-on with Land Gorilla Client, perform hello following steps:**</span></span>

1. <span data-ttu-id="99ae5-151">W portalu zarządzania Azure hello na powitania **klienta Gorilla ziemi** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.</span><span class="sxs-lookup"><span data-stu-id="99ae5-151">In hello Azure Management portal, on hello **Land Gorilla Client** application integration page, click **Single sign-on**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej][4]

2. <span data-ttu-id="99ae5-153">Na powitania **logowanie jednokrotne** okna dialogowego, jako **tryb** wybierz **na języku SAML logowania jednokrotnego** tooenable logowania jednokrotnego.</span><span class="sxs-lookup"><span data-stu-id="99ae5-153">On hello **Single sign-on** dialog, as **Mode** select **SAML-based Sign-on** tooenable single sign on.</span></span>
 
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-landgorilla-tutorial/tutorial_landgorilla_samlbase.png)

3. <span data-ttu-id="99ae5-155">Na powitania **adresy URL i domeny klienta grunt Gorilla** sekcji, wykonaj następujące kroki hello:</span><span class="sxs-lookup"><span data-stu-id="99ae5-155">On hello **Land Gorilla Client Domain and URLs** section, perform hello following steps:</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-landgorilla-tutorial/tutorial_landgorilla_url_02.png)

    <span data-ttu-id="99ae5-157">a.</span><span class="sxs-lookup"><span data-stu-id="99ae5-157">a.</span></span> <span data-ttu-id="99ae5-158">W hello **identyfikator** pole tekstowe, wartość hello typu przy użyciu jednej z hello następującego wzorca:</span><span class="sxs-lookup"><span data-stu-id="99ae5-158">In hello **Identifier** textbox, type hello value using one of hello following pattern:</span></span> 
    
    `https://<customer domain>.landgorilla.com/` 
    
    `https://www.<customer domain>.landgorilla.com`

    <span data-ttu-id="99ae5-159">b.</span><span class="sxs-lookup"><span data-stu-id="99ae5-159">b.</span></span> <span data-ttu-id="99ae5-160">W hello **adres URL odpowiedzi** tekstowym, wpisz adres URL przy użyciu jednej z hello następującego wzorca:</span><span class="sxs-lookup"><span data-stu-id="99ae5-160">In hello **Reply URL** textbox, type a URL using one of hello following pattern:</span></span>

    `https://<customer domain>.landgorilla.com/simplesaml/module.php/core/authenticate.php`

    `https://www.<customer domain>.landgorilla.com/simplesaml/module.php/core/authenticate.php`

    `https://<customer domain>.landgorilla.com/simplesaml/module.php/saml/sp/saml2-acs.php/default-sp`
    
    `https://www.<customer domain>.landgorilla.com/simplesaml/module.php/saml/sp/saml2-acs.php/default-sp`

    > [!NOTE] 
    > <span data-ttu-id="99ae5-161">Należy pamiętać, że nie są one hello wartości rzeczywistych.</span><span class="sxs-lookup"><span data-stu-id="99ae5-161">Please note that these are not hello real values.</span></span> <span data-ttu-id="99ae5-162">Masz tooupdate tych wartości za pomocą hello rzeczywisty identyfikator i odpowiedzi adresu URL.</span><span class="sxs-lookup"><span data-stu-id="99ae5-162">You have tooupdate these values with hello actual Identifier and Reply URL.</span></span> <span data-ttu-id="99ae5-163">W tym miejscu zalecamy możesz toouse hello unikatową wartość ciągu w hello identyfikator.</span><span class="sxs-lookup"><span data-stu-id="99ae5-163">Here we suggest you toouse hello unique value of string in hello Identifier.</span></span> <span data-ttu-id="99ae5-164">Skontaktuj się z [ziemi Gorilla klienta team](https://www.landgorilla.com/support/) tooget tych wartości.</span><span class="sxs-lookup"><span data-stu-id="99ae5-164">Contact [Land Gorilla Client team](https://www.landgorilla.com/support/) tooget these values.</span></span> 

4. <span data-ttu-id="99ae5-165">Na powitania **certyfikat podpisywania SAML** kliknij **XML metadanych** , a następnie zapisz plik XML hello na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="99ae5-165">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello XML file on your computer.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-landgorilla-tutorial/tutorial_landgorilla_certificate.png) 

5. <span data-ttu-id="99ae5-167">Kliknij przycisk **zapisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="99ae5-167">Click **Save** button.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-landgorilla-tutorial/tutorial_general_400.png) 

6. <span data-ttu-id="99ae5-169">Kończenie aplikacji na końcu Gorilla ziemi, skontaktuj się z konfiguracji logowania jednokrotnego tooget [zespołem pomocy technicznej klienta Gorilla ziemi](https://www.landgorilla.com/support/) i dostarczać hello pobrane **"XML metadanych** pliku.</span><span class="sxs-lookup"><span data-stu-id="99ae5-169">tooget SSO configuration complete for your application at Land Gorilla end, Contact [Land Gorilla Client support team](https://www.landgorilla.com/support/) and provide them with hello downloaded **“Metadata XML** file.</span></span>


### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="99ae5-170">Tworzenie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="99ae5-170">Creating an Azure AD test user</span></span>
<span data-ttu-id="99ae5-171">Celem Hello w tej sekcji jest toocreate użytkownika testowego, w portalu zarządzania Azure hello o nazwie Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="99ae5-171">hello objective of this section is toocreate a test user in hello Azure Management portal called Britta Simon.</span></span>

![Tworzenie użytkowników usługi Azure AD][100]

<span data-ttu-id="99ae5-173">**toocreate użytkownika testowego w usłudze Azure AD, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="99ae5-173">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="99ae5-174">W hello **portalu zarządzania Azure**na temat hello w lewym okienku nawigacji, kliknij przycisk **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="99ae5-174">In hello **Azure Management portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-landgorilla-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="99ae5-176">Przejdź za**użytkowników i grup** i kliknij przycisk **wszyscy użytkownicy** toodisplay hello listy użytkowników.</span><span class="sxs-lookup"><span data-stu-id="99ae5-176">Go too**Users and groups** and click **All users** toodisplay hello list of users.</span></span>
    
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-landgorilla-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="99ae5-178">U góry okna dialogowego hello powitania kliknij **Dodaj** tooopen hello **użytkownika** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="99ae5-178">At hello top of hello dialog click **Add** tooopen hello **User** dialog.</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-landgorilla-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="99ae5-180">Na powitania **użytkownika** okna dialogowego wykonaj hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="99ae5-180">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-landgorilla-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="99ae5-182">a.</span><span class="sxs-lookup"><span data-stu-id="99ae5-182">a.</span></span> <span data-ttu-id="99ae5-183">W hello **nazwa** pole tekstowe, typ **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="99ae5-183">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="99ae5-184">b.</span><span class="sxs-lookup"><span data-stu-id="99ae5-184">b.</span></span> <span data-ttu-id="99ae5-185">W hello **nazwy użytkownika** pole tekstowe, hello typu **adres e-mail** z BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="99ae5-185">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="99ae5-186">c.</span><span class="sxs-lookup"><span data-stu-id="99ae5-186">c.</span></span> <span data-ttu-id="99ae5-187">Wybierz **Pokaż hasło** i zanotuj wartość hello hello **hasło**.</span><span class="sxs-lookup"><span data-stu-id="99ae5-187">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="99ae5-188">d.</span><span class="sxs-lookup"><span data-stu-id="99ae5-188">d.</span></span> <span data-ttu-id="99ae5-189">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="99ae5-189">Click **Create**.</span></span> 

### <a name="creating-a-land-gorilla-test-user"></a><span data-ttu-id="99ae5-190">Tworzenie użytkownika testowego Gorilla ziemi</span><span class="sxs-lookup"><span data-stu-id="99ae5-190">Creating a Land Gorilla test user</span></span>

<span data-ttu-id="99ae5-191">We współpracy z [zespołem pomocy technicznej Gorilla ziemi](https://www.landgorilla.com/support/) użytkowników hello tooadd hello Gorilla ziemi platformy.</span><span class="sxs-lookup"><span data-stu-id="99ae5-191">Please work with [Land Gorilla support team](https://www.landgorilla.com/support/) tooadd hello users in hello Land Gorilla platform.</span></span>
    
### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="99ae5-192">Przypisanie użytkownika testowego hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="99ae5-192">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="99ae5-193">W tej sekcji można włączyć, przyznając jej tooLand dostępu klienta Gorilla toouse Simona Britta Azure rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="99ae5-193">In this section, you enable Britta Simon toouse Azure single sign-on by granting her access tooLand Gorilla Client.</span></span>

![Przypisz użytkownika][200] 

<span data-ttu-id="99ae5-195">**tooassign tooLand Simona Britta Gorilla klienta, należy wykonać hello następujące kroki:**</span><span class="sxs-lookup"><span data-stu-id="99ae5-195">**tooassign Britta Simon tooLand Gorilla Client, perform hello following steps:**</span></span>

1. <span data-ttu-id="99ae5-196">W portalu zarządzania Azure hello, otwórz widok aplikacji hello, a następnie przejdź widok katalogu toohello i go za**aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="99ae5-196">In hello Azure Management portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Przypisz użytkownika][201] 

2. <span data-ttu-id="99ae5-198">Z listy aplikacji hello wybierz **klienta Gorilla ziemi**.</span><span class="sxs-lookup"><span data-stu-id="99ae5-198">In hello applications list, select **Land Gorilla Client**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-landgorilla-tutorial/tutorial_landgorilla_app.png) 

3. <span data-ttu-id="99ae5-200">W menu powitania po lewej stronie powitania kliknij **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="99ae5-200">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Przypisz użytkownika][202] 

4. <span data-ttu-id="99ae5-202">Kliknij przycisk **Dodaj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="99ae5-202">Click **Add** button.</span></span> <span data-ttu-id="99ae5-203">Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="99ae5-203">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Przypisz użytkownika][203]

5. <span data-ttu-id="99ae5-205">Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** hello listy użytkowników.</span><span class="sxs-lookup"><span data-stu-id="99ae5-205">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="99ae5-206">Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="99ae5-206">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="99ae5-207">Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="99ae5-207">Click **Assign** button on **Add Assignment** dialog.</span></span>
    


### <a name="testing-single-sign-on"></a><span data-ttu-id="99ae5-208">Testowanie rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="99ae5-208">Testing single sign-on</span></span>

<span data-ttu-id="99ae5-209">W tej sekcji można przetestować konfiguracji usługi Azure AD pojedynczego logowania jednokrotnego przy użyciu hello panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="99ae5-209">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="99ae5-210">Po kliknięciu kafelka klienta Gorilla ziemi hello w hello Panel dostępu, należy pobrać automatycznie zalogowane tooyour aplikacji klienckiej Gorilla ziemi.</span><span class="sxs-lookup"><span data-stu-id="99ae5-210">When you click hello Land Gorilla Client tile in hello Access Panel, you should get automatically signed-on tooyour Land Gorilla Client application.</span></span>


## <a name="additional-resources"></a><span data-ttu-id="99ae5-211">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="99ae5-211">Additional resources</span></span>

* [<span data-ttu-id="99ae5-212">Lista samouczków dotyczących tooIntegrate aplikacji SaaS w usłudze Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="99ae5-212">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="99ae5-213">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="99ae5-213">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-landgorilla-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-landgorilla-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-landgorilla-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-landgorilla-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-landgorilla-tutorial/tutorial_general_100.png
[200]: ./media/active-directory-saas-landgorilla-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-landgorilla-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-landgorilla-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-landgorilla-tutorial/tutorial_general_203.png
