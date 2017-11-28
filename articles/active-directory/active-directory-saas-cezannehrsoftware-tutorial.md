---
title: 'Samouczek: Azure Active Directory integracji z oprogramowaniem Cezanne HR | Dokumentacja firmy Microsoft'
description: "Dowiedz się, jak tooconfigure logowanie jednokrotne między oprogramowaniem Cezanne HR i Azure Active Directory."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: fb8f95bf-c3c1-4e1f-b2b3-3b67526be72d
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/05/2017
ms.author: jeedes
ms.openlocfilehash: 3675acd8871d62c2277def8074f7aa39ac46e2a3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-integrate-azure-active-directory-with-cezanne-hr-software"></a><span data-ttu-id="13b3e-103">Samouczek: Integrowanie usługi Azure Active Directory z oprogramowaniem Cezanne HR</span><span class="sxs-lookup"><span data-stu-id="13b3e-103">Tutorial: Integrate Azure Active Directory with Cezanne HR software</span></span>

<span data-ttu-id="13b3e-104">Z tego samouczka, dowiesz się, jak toointegrate Cezanne HR oprogramowania w usłudze Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="13b3e-104">In this tutorial, you learn how toointegrate Cezanne HR software with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="13b3e-105">Integracja oprogramowania Cezanne HR z usługą Azure AD zapewnia hello następujące korzyści.</span><span class="sxs-lookup"><span data-stu-id="13b3e-105">Integrating Cezanne HR software with Azure AD provides you with hello following benefits.</span></span> <span data-ttu-id="13b3e-106">Możesz:</span><span class="sxs-lookup"><span data-stu-id="13b3e-106">You can:</span></span>

- <span data-ttu-id="13b3e-107">Kontrolowanie w usłudze Azure AD, kto ma dostęp do tooCezanne HR oprogramowania.</span><span class="sxs-lookup"><span data-stu-id="13b3e-107">Control in Azure AD who has access tooCezanne HR software.</span></span>
- <span data-ttu-id="13b3e-108">Włączanie logowania tooautomatically użytkowników oprogramowania tooCezanne HR rejestracji jednokrotnej (SSO) przy użyciu ich kont usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="13b3e-108">Enable your users tooautomatically sign in tooCezanne HR software with single sign-on (SSO) with their Azure AD accounts.</span></span>
- <span data-ttu-id="13b3e-109">Zarządzanie kont w jednej centralnej lokalizacji: hello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="13b3e-109">Manage your accounts in one central location: hello Azure portal.</span></span>

<span data-ttu-id="13b3e-110">toolearn więcej informacji na temat oprogramowania jako usługa (SaaS) integracji aplikacji z usługą Azure AD, zobacz [co to jest dostęp do aplikacji i logowania jednokrotnego w usłudze Azure Active Directory?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="13b3e-110">toolearn more about software as a service (SaaS) app integration with Azure AD, see [What is application access and SSO with Azure Active Directory?](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="13b3e-111">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="13b3e-111">Prerequisites</span></span>

<span data-ttu-id="13b3e-112">tooconfigure integracji usługi Azure AD z oprogramowaniem Cezanne HR należy hello następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="13b3e-112">tooconfigure Azure AD integration with Cezanne HR software, you need hello following items:</span></span>

- <span data-ttu-id="13b3e-113">Subskrypcję usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="13b3e-113">An Azure AD subscription</span></span>
- <span data-ttu-id="13b3e-114">Logowanie Jednokrotne włączone subskrypcji oprogramowania Cezanne HR</span><span class="sxs-lookup"><span data-stu-id="13b3e-114">A Cezanne HR software SSO-enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="13b3e-115">Zalecamy tootest hello kroki opisane w tym samouczku, nie używaj do środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="13b3e-115">tootest hello steps in this tutorial, we recommend that you do not use a production environment.</span></span>

<span data-ttu-id="13b3e-116">kroki hello tootest w tym samouczku, wykonaj te zalecenia:</span><span class="sxs-lookup"><span data-stu-id="13b3e-116">tootest hello steps in this tutorial, follow these recommendations:</span></span>

- <span data-ttu-id="13b3e-117">Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="13b3e-117">Don't use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="13b3e-118">Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz [uzyskać miesięczna wersja próbna](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="13b3e-118">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="13b3e-119">Opis scenariusza</span><span class="sxs-lookup"><span data-stu-id="13b3e-119">Scenario description</span></span>
<span data-ttu-id="13b3e-120">W tym samouczku można przetestować logowania jednokrotnego programu Azure AD w środowisku testowym.</span><span class="sxs-lookup"><span data-stu-id="13b3e-120">In this tutorial, you test Azure AD SSO in a test environment.</span></span> 

<span data-ttu-id="13b3e-121">Scenariusz Hello opisane w tym samouczku składa się z dwóch głównych elementów:</span><span class="sxs-lookup"><span data-stu-id="13b3e-121">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

* <span data-ttu-id="13b3e-122">Dodawanie oprogramowania Cezanne HR z galerii hello</span><span class="sxs-lookup"><span data-stu-id="13b3e-122">Adding Cezanne HR software from hello gallery</span></span>
* <span data-ttu-id="13b3e-123">Konfigurowanie i testowania logowania jednokrotnego programu Azure AD</span><span class="sxs-lookup"><span data-stu-id="13b3e-123">Configuring and testing Azure AD SSO</span></span>

## <a name="add-cezanne-hr-software-from-hello-gallery"></a><span data-ttu-id="13b3e-124">Dodawanie oprogramowania Cezanne HR z galerii hello</span><span class="sxs-lookup"><span data-stu-id="13b3e-124">Add Cezanne HR software from hello gallery</span></span>
<span data-ttu-id="13b3e-125">Integracja hello tooconfigure Cezanne HR oprogramowania do usługi Azure AD, Dodaj oprogramowania Cezanne HR hello galerii tooyour listy zarządzanych aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="13b3e-125">tooconfigure hello integration of Cezanne HR software into Azure AD, add Cezanne HR software from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="13b3e-126">tooadd Cezanne HR oprogramowania z galerii hello hello następujące:</span><span class="sxs-lookup"><span data-stu-id="13b3e-126">tooadd Cezanne HR software from hello gallery, do hello following:</span></span>

1. <span data-ttu-id="13b3e-127">W hello  **[portalu Azure](https://portal.azure.com)**, w lewym okienku hello, wybierz hello **usługi Azure Active Directory** przycisku.</span><span class="sxs-lookup"><span data-stu-id="13b3e-127">In hello **[Azure portal](https://portal.azure.com)**, in hello left pane, select hello **Azure Active Directory** button.</span></span> 

    ![przycisk "Azure Active Directory" Hello][1]

2. <span data-ttu-id="13b3e-129">Wybierz **aplikacje dla przedsiębiorstw** > **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="13b3e-129">Select **Enterprise applications** > **All applications**.</span></span>

    ![Witaj link "Wszystkie aplikacje"][2]
    
3. <span data-ttu-id="13b3e-131">tooadd nową aplikację, u góry hello hello **wszystkie aplikacje** okno dialogowe, wybierz opcję **nowej aplikacji**.</span><span class="sxs-lookup"><span data-stu-id="13b3e-131">tooadd a new application, at hello top of hello **All applications** dialog box, select **New application**.</span></span>

    ![Witaj "Nowej aplikacji" przycisku][3]

4. <span data-ttu-id="13b3e-133">W polu wyszukiwania hello wpisz **Cezanne HR oprogramowania**.</span><span class="sxs-lookup"><span data-stu-id="13b3e-133">In hello search box, type **Cezanne HR Software**.</span></span>

    ![pole wyszukiwania Hello](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_search.png)

5. <span data-ttu-id="13b3e-135">Na liście wyników hello, wybierz **Cezanne HR oprogramowania** , a następnie wybierz hello **Dodaj** przycisk tooadd hello aplikacji.</span><span class="sxs-lookup"><span data-stu-id="13b3e-135">In hello results list, select **Cezanne HR Software** and then select hello **Add** button tooadd hello application.</span></span>

    ![Lista wyników Hello](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="13b3e-137">Konfiguracja i testowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="13b3e-137">Configure and test Azure AD single sign-on</span></span>
<span data-ttu-id="13b3e-138">W tej sekcji możesz skonfigurować i przetestować logowania jednokrotnego programu Azure AD z oprogramowaniem Cezanne HR oparte na koncie użytkownika testu o nazwie "Britta Simona".</span><span class="sxs-lookup"><span data-stu-id="13b3e-138">In this section, you configure and test Azure AD SSO with Cezanne HR software based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="13b3e-139">Aby toowork logowania jednokrotnego usługi Azure AD musi użytkownika usługi Azure AD toohello odpowiednikiem oprogramowania tooknow hello Cezanne HR.</span><span class="sxs-lookup"><span data-stu-id="13b3e-139">For SSO toowork, Azure AD needs tooknow hello Cezanne HR software counterpart toohello Azure AD user.</span></span> <span data-ttu-id="13b3e-140">Innymi słowy musi ustanowić relację łącza między użytkownika usługi Azure AD i hello użytkownikowi, w hello Cezanne HR oprogramowania.</span><span class="sxs-lookup"><span data-stu-id="13b3e-140">In other words, you must establish a link relationship between an Azure AD user and hello related user in hello Cezanne HR software.</span></span>

<span data-ttu-id="13b3e-141">Relacja linku hello tooestablish, przypisz hello oprogramowania Cezanne HR **nazwy użytkownika** wartość jako hello Azure AD **Username** wartość.</span><span class="sxs-lookup"><span data-stu-id="13b3e-141">tooestablish hello link relationship, assign hello Cezanne HR software **user name** value as hello Azure AD **Username** value.</span></span>

<span data-ttu-id="13b3e-142">tooconfigure i testowania Azure AD logowania jednokrotnego za pomocą oprogramowania Cezanne HR, pełną powitania po bloków konstrukcyjnych.</span><span class="sxs-lookup"><span data-stu-id="13b3e-142">tooconfigure and test Azure AD SSO by using Cezanne HR software, complete hello following building blocks.</span></span>

### <a name="configure-azure-ad-sso"></a><span data-ttu-id="13b3e-143">Konfigurowanie usługi Azure AD logowania jednokrotnego.</span><span class="sxs-lookup"><span data-stu-id="13b3e-143">Configure Azure AD SSO</span></span>

<span data-ttu-id="13b3e-144">W tej sekcji możesz włączenia funkcji logowania jednokrotnego usługi Azure AD w portalu Azure hello i konfigurowanie logowania jednokrotnego w używanej aplikacji Cezanne HR hello następujący:</span><span class="sxs-lookup"><span data-stu-id="13b3e-144">In this section, you can enable Azure AD SSO in hello Azure portal and configure SSO in your Cezanne HR software application by doing hello following:</span></span>

1. <span data-ttu-id="13b3e-145">W portalu Azure na powitania hello **oprogramowania HR Cezanne** strona integracji aplikacji, wybierz opcję **logowanie jednokrotne**.</span><span class="sxs-lookup"><span data-stu-id="13b3e-145">In hello Azure portal, on hello **Cezanne HR Software** application integration page, select **Single sign-on**.</span></span>

    ![Witaj "Logowanie jednokrotne" polecenia][4]

2. <span data-ttu-id="13b3e-147">tooenable logowanie Jednokrotne, w hello **logowanie jednokrotne** okno dialogowe, wybierz opcję hello **tryb** jako **na języku SAML logowania jednokrotnego**.</span><span class="sxs-lookup"><span data-stu-id="13b3e-147">tooenable SSO, in hello **Single sign-on** dialog box, select hello **Mode** as **SAML-based Sign-on**.</span></span>
 
    ![pole "Tryb" Hello](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_samlbase.png)

3. <span data-ttu-id="13b3e-149">W obszarze **Cezanne HR oprogramowania domeny i adres URL**, hello następujące:</span><span class="sxs-lookup"><span data-stu-id="13b3e-149">Under **Cezanne HR Software Domain and URLs**, do hello following:</span></span>

    ![Witaj w sekcji "Cezanne HR oprogramowania domeny i adresy URL"](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_url.png)

    <span data-ttu-id="13b3e-151">a.</span><span class="sxs-lookup"><span data-stu-id="13b3e-151">a.</span></span> <span data-ttu-id="13b3e-152">W hello **adres URL logowania** wpisz adres URL, który ma hello następującej składni:`https://w3.cezanneondemand.com/cezannehr/-/<tenant id>`</span><span class="sxs-lookup"><span data-stu-id="13b3e-152">In hello **Sign-on URL** box, type a URL that has hello following syntax: `https://w3.cezanneondemand.com/cezannehr/-/<tenant id>`</span></span>

    <span data-ttu-id="13b3e-153">b.</span><span class="sxs-lookup"><span data-stu-id="13b3e-153">b.</span></span> <span data-ttu-id="13b3e-154">W hello **adres URL odpowiedzi** wpisz adres URL, który ma hello następującej składni:`https://w3.cezanneondemand.com:443/<tenantid>`</span><span class="sxs-lookup"><span data-stu-id="13b3e-154">In hello **Reply URL** box, type a URL that has hello following syntax: `https://w3.cezanneondemand.com:443/<tenantid>`</span></span>    
     
    > [!NOTE] 
    > <span data-ttu-id="13b3e-155">Witaj poprzedniej wartości nie są prawdziwe.</span><span class="sxs-lookup"><span data-stu-id="13b3e-155">hello preceding values are not real.</span></span> <span data-ttu-id="13b3e-156">Zaktualizuj je z adresu URL odpowiedzi rzeczywiste hello i hello adres URL logowania.</span><span class="sxs-lookup"><span data-stu-id="13b3e-156">Update them with hello actual reply URL and hello sign-on URL.</span></span> <span data-ttu-id="13b3e-157">wartości hello tooobtain, skontaktuj się z pomocą hello [Cezanne HR oprogramowanie klienta z pomocą techniczną](mailto:info@cezannehr.com).</span><span class="sxs-lookup"><span data-stu-id="13b3e-157">tooobtain hello values, contact hello [Cezanne HR software client support team](mailto:info@cezannehr.com).</span></span>

4. <span data-ttu-id="13b3e-158">W obszarze **SAML certyfikat podpisywania**, wybierz pozycję **certyfikatu (Base64)**, a następnie zapisz plik certyfikatu hello na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="13b3e-158">Under **SAML Signing Certificate**, select **Certificate (Base64)**, and then save hello certificate file on your computer.</span></span>

    ![Witaj sekcji "Certyfikat podpisywania SAML"](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_certificate.png) 

5. <span data-ttu-id="13b3e-160">Wybierz pozycję **Zapisz**.</span><span class="sxs-lookup"><span data-stu-id="13b3e-160">Select **Save**.</span></span>

    ![przycisk "Zapisz" Hello](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_general_400.png)
    
6. <span data-ttu-id="13b3e-162">W obszarze **konfiguracji oprogramowania HR Cezanne**, wybierz pozycję **Konfigurowanie oprogramowania HR Cezanne** tooopen hello **Konfigurowanie logowania jednokrotnego** okna.</span><span class="sxs-lookup"><span data-stu-id="13b3e-162">Under **Cezanne HR Software Configuration**, select **Configure Cezanne HR Software** tooopen hello **Configure sign-on** window.</span></span> <span data-ttu-id="13b3e-163">Hello kopiowania **identyfikator jednostki SAML** i **SAML logowania jednokrotnego usługi pojedynczej** adresu URL z hello **krótkimi opisami** sekcji.</span><span class="sxs-lookup"><span data-stu-id="13b3e-163">Copy hello **SAML Entity ID** and **SAML Single Sign-On Service** URL from hello **Quick Reference** section.</span></span>

    ![Witaj w sekcji "Konfiguracja oprogramowania HR Cezanne"](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_configure.png) 

7. <span data-ttu-id="13b3e-165">W oknie przeglądarki sieci web inną logowania tooyour Cezanne HR oprogramowania dzierżawy z uprawnieniami administratora.</span><span class="sxs-lookup"><span data-stu-id="13b3e-165">In a different web browser window, sign on tooyour Cezanne HR software tenant as an administrator.</span></span>

8. <span data-ttu-id="13b3e-166">Wybierz w okienku po lewej stronie powitania **konfiguracji systemu**.</span><span class="sxs-lookup"><span data-stu-id="13b3e-166">In hello left pane, select **System Setup**.</span></span> <span data-ttu-id="13b3e-167">Wybierz **ustawienia zabezpieczeń** > **pojedynczy konfiguracji logowania jednokrotnego**.</span><span class="sxs-lookup"><span data-stu-id="13b3e-167">Select **Security Settings** > **Single Sign-On Configuration**.</span></span>

    ![łącze "Pojedynczego logowania jednokrotnego konfiguracji" Hello](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_000.png)

9. <span data-ttu-id="13b3e-169">W hello **Zezwalaj toolog użytkowników za pomocą powitania po jednym logowania jednokrotnego (SSO) usług** okienku, wybierz hello **SAML 2.0** pole wyboru i wybierz hello **Advanced Configuration** Opcja.</span><span class="sxs-lookup"><span data-stu-id="13b3e-169">In hello **Allow users toolog in using hello following Single Sign-On (SSO) services** pane, select hello **SAML 2.0** check box and select hello **Advanced Configuration** option.</span></span>

    ![Opcje logowania jednokrotnego usług](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_001.png)

10. <span data-ttu-id="13b3e-171">Wybierz **Dodawanie nowych**.</span><span class="sxs-lookup"><span data-stu-id="13b3e-171">Select **Add New**.</span></span>

    ![przycisk "Dodaj nowy" Hello](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_002.png)

11. <span data-ttu-id="13b3e-173">W obszarze **dostawców tożsamości SAML 2.0**, hello następujące:</span><span class="sxs-lookup"><span data-stu-id="13b3e-173">Under **SAML 2.0 Identity Providers**, do hello following:</span></span>

    ![Witaj sekcji "Dostawców tożsamości SAML 2.0"](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_003.png)
    
    <span data-ttu-id="13b3e-175">a.</span><span class="sxs-lookup"><span data-stu-id="13b3e-175">a.</span></span> <span data-ttu-id="13b3e-176">W hello **Nazwa wyświetlana** wprowadź nazwę hello dostawcy tożsamości.</span><span class="sxs-lookup"><span data-stu-id="13b3e-176">In hello **Display Name** box, enter hello name of your identity provider.</span></span>

    <span data-ttu-id="13b3e-177">b.</span><span class="sxs-lookup"><span data-stu-id="13b3e-177">b.</span></span> <span data-ttu-id="13b3e-178">W hello **identyfikator** Wklej hello **identyfikator jednostki SAML** skopiowany z hello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="13b3e-178">In hello **Entity Identifier** box, paste hello **SAML Entity ID** that you copied from hello Azure portal.</span></span> 

    <span data-ttu-id="13b3e-179">c.</span><span class="sxs-lookup"><span data-stu-id="13b3e-179">c.</span></span> <span data-ttu-id="13b3e-180">W hello **powiązanie SAML** pola listy, wybierz opcję **POST**.</span><span class="sxs-lookup"><span data-stu-id="13b3e-180">In hello **SAML Binding** list box, select **POST**.</span></span>

    <span data-ttu-id="13b3e-181">d.</span><span class="sxs-lookup"><span data-stu-id="13b3e-181">d.</span></span> <span data-ttu-id="13b3e-182">W hello **punktu końcowego usługi tokenu zabezpieczającego** Wklej hello **SAML logowania jednokrotnego usługi pojedynczej** adresu URL skopiowanego z hello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="13b3e-182">In hello **Security Token Service Endpoint** box, paste hello **SAML Single Sign-On Service** URL that you copied from hello Azure portal.</span></span> 
    
    <span data-ttu-id="13b3e-183">e.</span><span class="sxs-lookup"><span data-stu-id="13b3e-183">e.</span></span> <span data-ttu-id="13b3e-184">W hello **nazwa atrybutu ID użytkownika** wprowadź `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name`.</span><span class="sxs-lookup"><span data-stu-id="13b3e-184">In hello **User ID Attribute Name** box, enter `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name`.</span></span>
    
    <span data-ttu-id="13b3e-185">f.</span><span class="sxs-lookup"><span data-stu-id="13b3e-185">f.</span></span> <span data-ttu-id="13b3e-186">tooupload hello pobrać certyfikatu z usługi Azure AD, wybierz hello **przekazać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="13b3e-186">tooupload hello downloaded certificate from Azure AD, select hello **Upload** button.</span></span>
    
    <span data-ttu-id="13b3e-187">g.</span><span class="sxs-lookup"><span data-stu-id="13b3e-187">g.</span></span> <span data-ttu-id="13b3e-188">Kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="13b3e-188">Select **OK**.</span></span> 

12. <span data-ttu-id="13b3e-189">Wybierz pozycję **Zapisz**.</span><span class="sxs-lookup"><span data-stu-id="13b3e-189">Select **Save**.</span></span>

    ![przycisk "Zapisz" Hello](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_004.png)

> [!TIP]
> <span data-ttu-id="13b3e-191">Po skonfigurowaniu aplikacji hello może odczytywać zwięzły wersji hello poprzedzających instrukcji w hello [portalu Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="13b3e-191">As you set up hello app, you can read a concise version of hello preceding instructions in hello [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="13b3e-192">Po dodaniu aplikacji hello z hello **usługi Active Directory** > **aplikacje dla przedsiębiorstw** sekcji, wybierz hello **logowanie jednokrotne** kartę. Hello dostęp osadzone dokumentacji z hello **konfiguracji** sekcji.</span><span class="sxs-lookup"><span data-stu-id="13b3e-192">After you add hello app from hello **Active Directory** > **Enterprise applications** section, select hello **Single sign-on** tab. Then access hello embedded documentation from hello **Configuration** section.</span></span> 

<span data-ttu-id="13b3e-193">toolearn więcej informacji na temat hello osadzonych dokumentacji funkcji, zobacz [usługi Azure AD osadzonych dokumentacji]( https://go.microsoft.com/fwlink/?linkid=845985).</span><span class="sxs-lookup"><span data-stu-id="13b3e-193">toolearn more about hello embedded documentation feature, see [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985).</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="13b3e-194">Tworzenie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="13b3e-194">Create an Azure AD test user</span></span>
<span data-ttu-id="13b3e-195">W tej sekcji utworzysz użytkownika testowego Simona Britta w hello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="13b3e-195">In this section, you create test user Britta Simon in hello Azure portal.</span></span>

![użytkownika testowego Hello Simona Britta][100]

<span data-ttu-id="13b3e-197">toocreate użytkownika testowego w usłudze Azure AD, hello następujące:</span><span class="sxs-lookup"><span data-stu-id="13b3e-197">toocreate a test user in Azure AD, do hello following:</span></span>

1. <span data-ttu-id="13b3e-198">W hello **portalu Azure**, w lewym okienku hello, wybierz hello **usługi Azure Active Directory** przycisku.</span><span class="sxs-lookup"><span data-stu-id="13b3e-198">In hello **Azure portal**, in hello left pane, select hello **Azure Active Directory** button.</span></span>

    ![przycisk "Azure Active Directory" Hello](./media/active-directory-saas-cezannehrsoftware-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="13b3e-200">toodisplay hello listę użytkowników, wybierz opcję **użytkowników i grup** > **wszyscy użytkownicy**.</span><span class="sxs-lookup"><span data-stu-id="13b3e-200">toodisplay hello list of users, select **Users and groups** > **All users**.</span></span>
    
    ![Witaj link "Wszyscy użytkownicy"](./media/active-directory-saas-cezannehrsoftware-tutorial/create_aaduser_02.png) 
    
    <span data-ttu-id="13b3e-202">Witaj **wszyscy użytkownicy** zostanie otwarte okno dialogowe.</span><span class="sxs-lookup"><span data-stu-id="13b3e-202">hello **All users** dialog box opens.</span></span>

3. <span data-ttu-id="13b3e-203">Witaj tooopen **użytkownika** okno dialogowe, wybierz opcję **Dodaj**.</span><span class="sxs-lookup"><span data-stu-id="13b3e-203">tooopen hello **User** dialog box, select **Add**.</span></span>
 
    ![przycisk "Dodaj" Hello](./media/active-directory-saas-cezannehrsoftware-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="13b3e-205">W hello **użytkownika** okna dialogowego pozycję hello następujące:</span><span class="sxs-lookup"><span data-stu-id="13b3e-205">In hello **User** dialog box, do hello following:</span></span>
 
    ![okno dialogowe "Użytkownika" Hello](./media/active-directory-saas-cezannehrsoftware-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="13b3e-207">a.</span><span class="sxs-lookup"><span data-stu-id="13b3e-207">a.</span></span> <span data-ttu-id="13b3e-208">W hello **nazwa** wpisz **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="13b3e-208">In hello **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="13b3e-209">b.</span><span class="sxs-lookup"><span data-stu-id="13b3e-209">b.</span></span> <span data-ttu-id="13b3e-210">W hello **nazwy użytkownika** wpisz użytkownika Britta Simona **adres e-mail**.</span><span class="sxs-lookup"><span data-stu-id="13b3e-210">In hello **User name** box, type user Britta Simon's **email address**.</span></span>

    <span data-ttu-id="13b3e-211">c.</span><span class="sxs-lookup"><span data-stu-id="13b3e-211">c.</span></span> <span data-ttu-id="13b3e-212">Wybierz hello **Pokaż hasło** pole wyboru, a następnie wartość hello Uwaga, który został wygenerowany w hello **hasło** pole.</span><span class="sxs-lookup"><span data-stu-id="13b3e-212">Select hello **Show Password** check box, and then note hello value that was generated in hello **Password** box.</span></span>

    <span data-ttu-id="13b3e-213">d.</span><span class="sxs-lookup"><span data-stu-id="13b3e-213">d.</span></span> <span data-ttu-id="13b3e-214">Wybierz pozycję **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="13b3e-214">Select **Create**.</span></span>
 
### <a name="create-a-cezanne-hr-software-test-user"></a><span data-ttu-id="13b3e-215">Tworzenie użytkownika testowego Cezanne HR oprogramowania</span><span class="sxs-lookup"><span data-stu-id="13b3e-215">Create a Cezanne HR software test user</span></span>

<span data-ttu-id="13b3e-216">tooenable usługi Azure AD użytkownicy toosign tooCezanne HR oprogramowania, muszą mieć przydzielone do Cezanne HR oprogramowania.</span><span class="sxs-lookup"><span data-stu-id="13b3e-216">tooenable Azure AD users toosign in tooCezanne HR software, they must be provisioned into Cezanne HR software.</span></span> <span data-ttu-id="13b3e-217">W przypadku hello Cezanne HR oprogramowania Inicjowanie obsługi to zadanie ręczne.</span><span class="sxs-lookup"><span data-stu-id="13b3e-217">In hello case of Cezanne HR software, provisioning is a manual task.</span></span>

<span data-ttu-id="13b3e-218">Ustanowienie konta użytkownika, wykonując następujące hello:</span><span class="sxs-lookup"><span data-stu-id="13b3e-218">Provision a user account by doing hello following:</span></span>

1.  <span data-ttu-id="13b3e-219">Zaloguj się tooyour Cezanne HR witrynę firmy jako administrator.</span><span class="sxs-lookup"><span data-stu-id="13b3e-219">Sign in tooyour Cezanne HR software company site as an administrator.</span></span>

2.  <span data-ttu-id="13b3e-220">Wybierz w okienku po lewej stronie powitania **konfiguracji systemu** > **Zarządzanie użytkownikami** > **Dodaj nowego użytkownika**.</span><span class="sxs-lookup"><span data-stu-id="13b3e-220">In hello left pane, select **System Setup** > **Manage Users** > **Add New User**.</span></span>

    <span data-ttu-id="13b3e-221">![łącze "Dodaj nowego użytkownika" Hello](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_005.png "nowego użytkownika")</span><span class="sxs-lookup"><span data-stu-id="13b3e-221">![hello "Add New User" link](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_005.png "New User")</span></span>

3.  <span data-ttu-id="13b3e-222">W obszarze **dane osobowe**, hello następujące:</span><span class="sxs-lookup"><span data-stu-id="13b3e-222">Under **Person Details**, do hello following:</span></span>

    <span data-ttu-id="13b3e-223">![sekcja "Dane osobowe" Hello](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_006.png "nowego użytkownika")</span><span class="sxs-lookup"><span data-stu-id="13b3e-223">![hello "Person Details" section](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_006.png "New User")</span></span>
    
    <span data-ttu-id="13b3e-224">a.</span><span class="sxs-lookup"><span data-stu-id="13b3e-224">a.</span></span> <span data-ttu-id="13b3e-225">Ustaw **wewnętrznego użytkownika** jako **OFF**.</span><span class="sxs-lookup"><span data-stu-id="13b3e-225">Set **Internal User** as **OFF**.</span></span>
    
    <span data-ttu-id="13b3e-226">b.</span><span class="sxs-lookup"><span data-stu-id="13b3e-226">b.</span></span> <span data-ttu-id="13b3e-227">W hello **imię** okno, typ hello imię użytkownika, na przykład **Britta**.</span><span class="sxs-lookup"><span data-stu-id="13b3e-227">In hello **First Name** box, type hello user's first name, for example, **Britta**.</span></span>  
 
    <span data-ttu-id="13b3e-228">c.</span><span class="sxs-lookup"><span data-stu-id="13b3e-228">c.</span></span> <span data-ttu-id="13b3e-229">W hello **nazwisko** okno, typ hello nazwisko użytkownika, na przykład **Simona**.</span><span class="sxs-lookup"><span data-stu-id="13b3e-229">In hello **Last Name** box, type hello user's last name, for example, **Simon**.</span></span>
    
    <span data-ttu-id="13b3e-230">d.</span><span class="sxs-lookup"><span data-stu-id="13b3e-230">d.</span></span> <span data-ttu-id="13b3e-231">W hello **E-mail** wpisz adres e-mail użytkownika hello, na przykład Brittasimon@contoso.com.</span><span class="sxs-lookup"><span data-stu-id="13b3e-231">In hello **E-mail** box, type hello user's email address, for example, Brittasimon@contoso.com.</span></span>

4.  <span data-ttu-id="13b3e-232">W obszarze **informacje o koncie**, hello następujące:</span><span class="sxs-lookup"><span data-stu-id="13b3e-232">Under **Account Information**, do hello following:</span></span>

    <span data-ttu-id="13b3e-233">![sekcja "Informacje o koncie" Hello](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_007.png "nowego użytkownika")</span><span class="sxs-lookup"><span data-stu-id="13b3e-233">![hello "Account Information" section](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_007.png "New User")</span></span>
    
    <span data-ttu-id="13b3e-234">a.</span><span class="sxs-lookup"><span data-stu-id="13b3e-234">a.</span></span> <span data-ttu-id="13b3e-235">W hello **Username** wpisz adres e-mail użytkownika hello, na przykład Brittasimon@contoso.com.</span><span class="sxs-lookup"><span data-stu-id="13b3e-235">In hello **Username** box, type hello user's email address, for example, Brittasimon@contoso.com.</span></span>
    
    <span data-ttu-id="13b3e-236">b.</span><span class="sxs-lookup"><span data-stu-id="13b3e-236">b.</span></span> <span data-ttu-id="13b3e-237">W hello **hasło** wpisz hasło użytkownika hello.</span><span class="sxs-lookup"><span data-stu-id="13b3e-237">In hello **Password** box, type hello user's password.</span></span>
    
    <span data-ttu-id="13b3e-238">c.</span><span class="sxs-lookup"><span data-stu-id="13b3e-238">c.</span></span> <span data-ttu-id="13b3e-239">W hello **roli zabezpieczeń** wybierz opcję **HR Professional**.</span><span class="sxs-lookup"><span data-stu-id="13b3e-239">In hello **Security Role** box, select **HR Professional**.</span></span>
    
    <span data-ttu-id="13b3e-240">d.</span><span class="sxs-lookup"><span data-stu-id="13b3e-240">d.</span></span> <span data-ttu-id="13b3e-241">Kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="13b3e-241">Select **OK**.</span></span>

5. <span data-ttu-id="13b3e-242">Na powitania **logowanie jednokrotne** na karcie hello **SAML 2.0 identyfikatory** zaznacz **Dodaj nowy**.</span><span class="sxs-lookup"><span data-stu-id="13b3e-242">On hello **Single sign-on** tab, in hello **SAML 2.0 Identifiers** section, select **Add New**.</span></span>

    <span data-ttu-id="13b3e-243">![przycisk "Dodaj nowy" Hello](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_008.png "użytkownika")</span><span class="sxs-lookup"><span data-stu-id="13b3e-243">![hello "Add New" button](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_008.png "User")</span></span>

6. <span data-ttu-id="13b3e-244">W hello **dostawcy tożsamości** pola listy, wybierz dostawcy tożsamości.</span><span class="sxs-lookup"><span data-stu-id="13b3e-244">In hello **Identity Provider** list box, select your identity provider.</span></span> <span data-ttu-id="13b3e-245">W hello **identyfikator użytkownika** wprowadź adres e-mail hello Simona testu użytkownika Britta konta.</span><span class="sxs-lookup"><span data-stu-id="13b3e-245">In hello **User Identifier** box, enter hello email address for test user Britta Simon's account.</span></span>

    <span data-ttu-id="13b3e-246">![Witaj pola "Dostawcy tożsamości" i "Identyfikator użytkownika"](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_009.png "użytkownika")</span><span class="sxs-lookup"><span data-stu-id="13b3e-246">![hello "Identity Provider" and "User Identifier" boxes](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_009.png "User")</span></span>
    
7. <span data-ttu-id="13b3e-247">Wybierz pozycję **Zapisz**.</span><span class="sxs-lookup"><span data-stu-id="13b3e-247">Select **Save**.</span></span>

    <span data-ttu-id="13b3e-248">![przycisk "Zapisz" Hello](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_010.png "użytkownika")</span><span class="sxs-lookup"><span data-stu-id="13b3e-248">![hello "Save" button](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_010.png "User")</span></span>

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="13b3e-249">Przypisz użytkownika testowego hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="13b3e-249">Assign hello Azure AD test user</span></span>

<span data-ttu-id="13b3e-250">W tej sekcji możesz włączyć użytkownika testowego toouse Simona Britta Azure logowania jednokrotnego za udzielanie dostępu tooCezanne HR oprogramowania.</span><span class="sxs-lookup"><span data-stu-id="13b3e-250">In this section, you enable test user Britta Simon toouse Azure SSO by granting access tooCezanne HR software.</span></span>

![Dostęp użytkownika testowego][200] 

1. <span data-ttu-id="13b3e-252">W portalu Azure hello Otwórz widok aplikacji hello, a następnie przejdź toohello widok katalogu.</span><span class="sxs-lookup"><span data-stu-id="13b3e-252">In hello Azure portal, open hello applications view and then go toohello directory view.</span></span> <span data-ttu-id="13b3e-253">Wybierz **aplikacje dla przedsiębiorstw** > **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="13b3e-253">Select **Enterprise applications** > **All applications**.</span></span>

    ![Witaj link "Wszystkie aplikacje"][201] 

2. <span data-ttu-id="13b3e-255">Z listy aplikacji hello wybierz **Cezanne HR oprogramowania**.</span><span class="sxs-lookup"><span data-stu-id="13b3e-255">In hello applications list, select **Cezanne HR Software**.</span></span>

    ![listę "Aplikacji" Hello](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_app.png) 

3. <span data-ttu-id="13b3e-257">W menu hello powitania po lewej stronie wybierz **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="13b3e-257">In hello menu on hello left, select **Users and groups**.</span></span>

    ![Przypisz użytkownika][202] 

4. <span data-ttu-id="13b3e-259">Wybierz pozycję **Dodaj**.</span><span class="sxs-lookup"><span data-stu-id="13b3e-259">Select **Add**.</span></span> <span data-ttu-id="13b3e-260">Następnie w hello **Dodaj przydziału** okno dialogowe, wybierz opcję **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="13b3e-260">Then in hello **Add Assignment** dialog box, select **Users and groups**.</span></span>

    ![Łącze "Użytkownicy i grupy"][203]

5. <span data-ttu-id="13b3e-262">W hello **użytkowników i grup** okno dialogowe, w hello **użytkowników** listy, wybierz **Simona Britta**.</span><span class="sxs-lookup"><span data-stu-id="13b3e-262">In hello **Users and groups** dialog box, in hello **Users** list, select **Britta Simon**.</span></span>

6. <span data-ttu-id="13b3e-263">W hello **użytkowników i grup** okno dialogowe, wybierz opcję **wybierz**.</span><span class="sxs-lookup"><span data-stu-id="13b3e-263">In hello **Users and groups** dialog box, select **Select**.</span></span>

7. <span data-ttu-id="13b3e-264">W hello **Dodaj przydziału** okno dialogowe, wybierz opcję **przypisać**.</span><span class="sxs-lookup"><span data-stu-id="13b3e-264">In hello **Add Assignment** dialog box, select **Assign**.</span></span>
    
### <a name="test-sso"></a><span data-ttu-id="13b3e-265">Test rejestracji Jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="13b3e-265">Test SSO</span></span>

<span data-ttu-id="13b3e-266">W tej sekcji możesz przetestować konfigurację programu Azure AD z logowania jednokrotnego przy użyciu hello panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="13b3e-266">In this section, you test your Azure AD SSO configuration by using hello Access Panel.</span></span>

<span data-ttu-id="13b3e-267">Po wybraniu kafelka oprogramowania Cezanne HR hello w hello panelu dostępu logowania jest automatycznie tooyour Cezanne HR aplikacji.</span><span class="sxs-lookup"><span data-stu-id="13b3e-267">When you select hello Cezanne HR software tile in hello Access Panel, you sign on automatically tooyour Cezanne HR software application.</span></span>

## <a name="next-steps"></a><span data-ttu-id="13b3e-268">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="13b3e-268">Next steps</span></span>

* [<span data-ttu-id="13b3e-269">Lista samouczków dotyczących toointegrate aplikacji SaaS w usłudze Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="13b3e-269">List of tutorials on how toointegrate SaaS apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="13b3e-270">Co to jest dostęp do aplikacji i logowania jednokrotnego w usłudze Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="13b3e-270">What is application access and SSO with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_general_203.png

