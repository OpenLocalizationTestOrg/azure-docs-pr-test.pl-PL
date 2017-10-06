---
title: 'Samouczek: Integracji Azure Active Directory z LCVista | Dokumentacja firmy Microsoft'
description: "Dowiedz się, jak tooconfigure logowanie jednokrotne między usługą Azure Active Directory i LCVista."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 8db80d6e-3275-419f-aa39-6115a7bc9800
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/17/2017
ms.author: jeedes
ms.openlocfilehash: 5a4c7eb7d54b8b68c8241a97b9e516a3f6e55c50
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-lcvista"></a><span data-ttu-id="4be2f-103">Samouczek: Integracji Azure Active Directory z LCVista</span><span class="sxs-lookup"><span data-stu-id="4be2f-103">Tutorial: Azure Active Directory integration with LCVista</span></span>

<span data-ttu-id="4be2f-104">Z tego samouczka, dowiesz się, jak toointegrate LCVista w usłudze Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="4be2f-104">In this tutorial, you learn how toointegrate LCVista with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="4be2f-105">Integracja z usługą Azure AD LCVista zapewnia hello następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="4be2f-105">Integrating LCVista with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="4be2f-106">Można kontrolować w usłudze Azure AD, kto ma dostęp do tooLCVista</span><span class="sxs-lookup"><span data-stu-id="4be2f-106">You can control in Azure AD who has access tooLCVista</span></span>
- <span data-ttu-id="4be2f-107">Można włączyć użytkownika użytkownicy tooautomatically get zalogowane tooLCVista (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="4be2f-107">You can enable your users tooautomatically get signed-on tooLCVista (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="4be2f-108">Możesz zarządzać kont w jednej centralnej lokalizacji - hello portalu Azure</span><span class="sxs-lookup"><span data-stu-id="4be2f-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="4be2f-109">Jeśli chcesz tooknow więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="4be2f-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="4be2f-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="4be2f-110">Prerequisites</span></span>

<span data-ttu-id="4be2f-111">tooconfigure integracji z usługą Azure AD z LCVista należy hello następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="4be2f-111">tooconfigure Azure AD integration with LCVista, you need hello following items:</span></span>

- <span data-ttu-id="4be2f-112">Subskrypcję usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="4be2f-112">An Azure AD subscription</span></span>
- <span data-ttu-id="4be2f-113">LCVista jednokrotnego włączone subskrypcji</span><span class="sxs-lookup"><span data-stu-id="4be2f-113">A LCVista single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="4be2f-114">tootest hello kroków w tym samouczku, zaleca się przy użyciu środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="4be2f-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="4be2f-115">tootest hello kroki opisane w tym samouczku, należy stosować te zalecenia:</span><span class="sxs-lookup"><span data-stu-id="4be2f-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="4be2f-116">Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="4be2f-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="4be2f-117">Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz pobrać miesięczna wersja próbna [tutaj](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="4be2f-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="4be2f-118">Opis scenariusza</span><span class="sxs-lookup"><span data-stu-id="4be2f-118">Scenario description</span></span>
<span data-ttu-id="4be2f-119">W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym.</span><span class="sxs-lookup"><span data-stu-id="4be2f-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="4be2f-120">Scenariusz Hello opisane w tym samouczku składa się z dwóch głównych elementów:</span><span class="sxs-lookup"><span data-stu-id="4be2f-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="4be2f-121">Dodawanie LCVista z galerii hello</span><span class="sxs-lookup"><span data-stu-id="4be2f-121">Adding LCVista from hello gallery</span></span>
2. <span data-ttu-id="4be2f-122">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="4be2f-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-lcvista-from-hello-gallery"></a><span data-ttu-id="4be2f-123">Dodawanie LCVista z galerii hello</span><span class="sxs-lookup"><span data-stu-id="4be2f-123">Adding LCVista from hello gallery</span></span>
<span data-ttu-id="4be2f-124">tooconfigure hello integracji LCVista do usługi Azure AD, należy tooadd LCVista z hello galerii tooyour listę zarządzanych aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="4be2f-124">tooconfigure hello integration of LCVista into Azure AD, you need tooadd LCVista from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="4be2f-125">**tooadd LCVista z galerii hello, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="4be2f-125">**tooadd LCVista from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="4be2f-126">W hello  **[portalu Azure](https://portal.azure.com)**na temat hello panelu nawigacji po lewej stronie, kliknij przycisk **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="4be2f-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Usługa Active Directory][1]

2. <span data-ttu-id="4be2f-128">Przejdź za**aplikacje dla przedsiębiorstw**.</span><span class="sxs-lookup"><span data-stu-id="4be2f-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="4be2f-129">Następnie przejdź zbyt**wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="4be2f-129">Then go too**All applications**.</span></span>

    ![Aplikacje][2]
    
3. <span data-ttu-id="4be2f-131">tooadd nową aplikację, kliknij przycisk **nowej aplikacji** przycisk u góry hello okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="4be2f-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplikacje][3]

4. <span data-ttu-id="4be2f-133">W polu wyszukiwania hello wpisz **LCVista**.</span><span class="sxs-lookup"><span data-stu-id="4be2f-133">In hello search box, type **LCVista**.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-lcvista-tutorial/tutorial_lcvista_search.png)

5. <span data-ttu-id="4be2f-135">W panelu wyników hello zaznacz **LCVista**, a następnie kliknij przycisk **Dodaj** przycisk aplikacji hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="4be2f-135">In hello results panel, select **LCVista**, and then click **Add** button tooadd hello application.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-lcvista-tutorial/tutorial_lcvista_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="4be2f-137">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="4be2f-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="4be2f-138">W tej sekcji możesz skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z LCVista na podstawie użytkownika testowego, nazywany "Britta Simona".</span><span class="sxs-lookup"><span data-stu-id="4be2f-138">In this section, you configure and test Azure AD single sign-on with LCVista based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="4be2f-139">Dla pojedynczego logowania jednokrotnego toowork usługi Azure AD musi tooknow użytkownika odpowiednikiem hello w LCVista jest tooa użytkownika w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="4be2f-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in LCVista is tooa user in Azure AD.</span></span> <span data-ttu-id="4be2f-140">Innymi słowy relację łącza między użytkownika usługi Azure AD i hello użytkownikowi w LCVista musi toobe ustanowione.</span><span class="sxs-lookup"><span data-stu-id="4be2f-140">In other words, a link relationship between an Azure AD user and hello related user in LCVista needs toobe established.</span></span>

<span data-ttu-id="4be2f-141">Ta relacja łącza zostanie nawiązane, przypisując wartość hello hello **nazwy użytkownika** w usłudze Azure AD jako wartość hello hello **Username** w LCVista.</span><span class="sxs-lookup"><span data-stu-id="4be2f-141">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in LCVista.</span></span>

<span data-ttu-id="4be2f-142">tooconfigure i testowych usługi Azure AD rejestracji jednokrotnej z LCVista, należy po bloków konstrukcyjnych hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="4be2f-142">tooconfigure and test Azure AD single sign-on with LCVista, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="4be2f-143">**[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configuring-azure-ad-single-sign-on)**  -tooenable Twojego toouse użytkowników tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="4be2f-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="4be2f-144">**[Tworzenie użytkownika testowego usługi Azure AD](#creating-an-azure-ad-test-user)**  -tootest usługi Azure AD rejestracji jednokrotnej z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="4be2f-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="4be2f-145">**[Tworzenie użytkownika testowego LCVista](#creating-a-lcvista-test-user)**  -toohave odpowiednikiem Simona Britta w LCVista, który jest połączony toohello usługi Azure AD reprezentację użytkownika.</span><span class="sxs-lookup"><span data-stu-id="4be2f-145">**[Creating a LCVista test user](#creating-a-lcvista-test-user)** - toohave a counterpart of Britta Simon in LCVista that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="4be2f-146">**[Przypisanie użytkownika testowego hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Simona Britta toouse usługi Azure AD rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="4be2f-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="4be2f-147">**[Testowanie rejestracji jednokrotnej](#testing-single-sign-on)**  -tooverify czy hello konfiguracji działania.</span><span class="sxs-lookup"><span data-stu-id="4be2f-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="4be2f-148">Konfigurowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="4be2f-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="4be2f-149">W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w portalu Azure hello i skonfigurować logowanie jednokrotne w aplikacji LCVista.</span><span class="sxs-lookup"><span data-stu-id="4be2f-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your LCVista application.</span></span>

<span data-ttu-id="4be2f-150">**tooconfigure usługi Azure AD rejestracji jednokrotnej z LCVista, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="4be2f-150">**tooconfigure Azure AD single sign-on with LCVista, perform hello following steps:**</span></span>

1. <span data-ttu-id="4be2f-151">W portalu Azure na powitania hello **LCVista** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.</span><span class="sxs-lookup"><span data-stu-id="4be2f-151">In hello Azure portal, on hello **LCVista** application integration page, click **Single sign-on**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej][4]

2. <span data-ttu-id="4be2f-153">Na powitania **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** tooenable rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="4be2f-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-lcvista-tutorial/tutorial_lcvista_samlbase.png)

3. <span data-ttu-id="4be2f-155">Na powitania **LCVista domeny i adres URL** sekcji, wykonaj następujące kroki hello:</span><span class="sxs-lookup"><span data-stu-id="4be2f-155">On hello **LCVista Domain and URLs** section, perform hello following steps:</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-lcvista-tutorial/tutorial_lcvista_url.png)

    <span data-ttu-id="4be2f-157">a.</span><span class="sxs-lookup"><span data-stu-id="4be2f-157">a.</span></span> <span data-ttu-id="4be2f-158">W hello **adres URL logowania** tekstowym, wpisz adres URL za pomocą hello następującego wzorca:`https://<subdomain>.lcvista.com/rainier/login`</span><span class="sxs-lookup"><span data-stu-id="4be2f-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<subdomain>.lcvista.com/rainier/login`</span></span>

    <span data-ttu-id="4be2f-159">b.</span><span class="sxs-lookup"><span data-stu-id="4be2f-159">b.</span></span> <span data-ttu-id="4be2f-160">W hello **identyfikator** tekstowym, wpisz adres URL za pomocą hello następującego wzorca:`https://<subdomain>.lcvista.com`</span><span class="sxs-lookup"><span data-stu-id="4be2f-160">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<subdomain>.lcvista.com`</span></span> 
     
    > [!NOTE] 
    > <span data-ttu-id="4be2f-161">Wartości te nie są hello prawdziwe.</span><span class="sxs-lookup"><span data-stu-id="4be2f-161">These values are not hello real.</span></span> <span data-ttu-id="4be2f-162">Zaktualizować te wartości z hello rzeczywisty identyfikator i adres URL logowania.</span><span class="sxs-lookup"><span data-stu-id="4be2f-162">Update these values with hello actual Identifier and Sign-On URL.</span></span> <span data-ttu-id="4be2f-163">Skontaktuj się z [zespołem pomocy technicznej klienta LCVista](https://lcvista.com/contact) tooget tych wartości.</span><span class="sxs-lookup"><span data-stu-id="4be2f-163">Contact [LCVista Client support team](https://lcvista.com/contact) tooget these values.</span></span> 

4. <span data-ttu-id="4be2f-164">Na powitania **certyfikat podpisywania SAML** kliknij **XML metadanych** , a następnie zapisz plik metadanych hello na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="4be2f-164">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-lcvista-tutorial/tutorial_lcvista_certificate.png) 

5. <span data-ttu-id="4be2f-166">Kliknij przycisk **zapisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="4be2f-166">Click **Save** button.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-lcvista-tutorial/tutorial_general_400.png)
    
6. <span data-ttu-id="4be2f-168">Na powitania **konfiguracji LCVista** kliknij **skonfigurować LCVista** tooopen **Konfigurowanie logowania jednokrotnego** okna.</span><span class="sxs-lookup"><span data-stu-id="4be2f-168">On hello **LCVista Configuration** section, click **Configure LCVista** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="4be2f-169">Kopiuj hello **SAML identyfikator jednostki** i **SAML pojedynczy znak na adres URL usługi** z hello **sekcji krótkimi opisami.**</span><span class="sxs-lookup"><span data-stu-id="4be2f-169">Copy hello **SAML Entity ID** and **SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-lcvista-tutorial/tutorial_lcvista_configure.png) 

7.  <span data-ttu-id="4be2f-171">Zaloguj się na tooyour LCVista aplikacji jako administrator.</span><span class="sxs-lookup"><span data-stu-id="4be2f-171">Sign on tooyour LCVista application as an administrator.</span></span>

8. <span data-ttu-id="4be2f-172">W hello **SAML Config** sekcji, sprawdź hello **Włącz SAML logowania** i wprowadź szczegóły hello, jak wspomniano w poniżej obrazu.</span><span class="sxs-lookup"><span data-stu-id="4be2f-172">In hello **SAML Config** section, check hello **Enable SAML login** and enter hello details as mentioned in below image.</span></span> 

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-lcvista-tutorial/tutorial_lcvista_config.png)

    <span data-ttu-id="4be2f-174">a.</span><span class="sxs-lookup"><span data-stu-id="4be2f-174">a.</span></span> <span data-ttu-id="4be2f-175">Wklej hello **adres URL wystawcy** , które zostały skopiowane z usługi Azure AD w hello **identyfikator jednostki** sekcji.</span><span class="sxs-lookup"><span data-stu-id="4be2f-175">Paste hello **Issuer URL** which you have copied from Azure AD in hello **Entity ID** section.</span></span> 

    <span data-ttu-id="4be2f-176">b.</span><span class="sxs-lookup"><span data-stu-id="4be2f-176">b.</span></span> <span data-ttu-id="4be2f-177">Wklej hello **pojedynczy znak na adres URL usługi** , które zostały skopiowane z usługi Azure AD w hello **adres URL** sekcji.</span><span class="sxs-lookup"><span data-stu-id="4be2f-177">Paste hello **Single Sign-On Service URL** which you have copied from Azure AD in hello **URL** section.</span></span>

    <span data-ttu-id="4be2f-178">c.</span><span class="sxs-lookup"><span data-stu-id="4be2f-178">c.</span></span> <span data-ttu-id="4be2f-179">Z metadanych (XML), który został pobrany z portalu Azure, skopiuj wartość hello **X509Certificate** i wklej go w hello **x509 certyfikatu** sekcji.</span><span class="sxs-lookup"><span data-stu-id="4be2f-179">From Metadata (XML) which you have downloaded from Azure portal, copy hello value **X509Certificate** and paste it in hello **x509 Certificate** section.</span></span>

    <span data-ttu-id="4be2f-180">d.</span><span class="sxs-lookup"><span data-stu-id="4be2f-180">d.</span></span> <span data-ttu-id="4be2f-181">W hello **atrybutu imię** pole tekstowe, Wklej hello wartość `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname`.</span><span class="sxs-lookup"><span data-stu-id="4be2f-181">In hello **First name attribute** textbox, paste hello value `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname`.</span></span>

    <span data-ttu-id="4be2f-182">e.</span><span class="sxs-lookup"><span data-stu-id="4be2f-182">e.</span></span> <span data-ttu-id="4be2f-183">W hello **ostatniego atrybutu name** pole tekstowe, Wklej hello wartość `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/surname`.</span><span class="sxs-lookup"><span data-stu-id="4be2f-183">In hello **Last name attribute** textbox, paste hello value `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/surname`.</span></span>

    <span data-ttu-id="4be2f-184">f.</span><span class="sxs-lookup"><span data-stu-id="4be2f-184">f.</span></span> <span data-ttu-id="4be2f-185">W hello **atrybut poczty E-mail** pole tekstowe, Wklej hello wartość `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress`.</span><span class="sxs-lookup"><span data-stu-id="4be2f-185">In hello **Email attribute** textbox, paste hello value `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress`.</span></span>

    <span data-ttu-id="4be2f-186">g.</span><span class="sxs-lookup"><span data-stu-id="4be2f-186">g.</span></span> <span data-ttu-id="4be2f-187">W hello **atrybutu Username** pole tekstowe, Wklej hello wartość `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name`.</span><span class="sxs-lookup"><span data-stu-id="4be2f-187">In hello **Username attribute** textbox, paste hello value `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name`.</span></span>

    <span data-ttu-id="4be2f-188">e.</span><span class="sxs-lookup"><span data-stu-id="4be2f-188">e.</span></span> <span data-ttu-id="4be2f-189">Kliknij przycisk **zapisać** toosave hello ustawienia.</span><span class="sxs-lookup"><span data-stu-id="4be2f-189">Click **Save** toosave hello settings.</span></span>

> [!TIP]
> <span data-ttu-id="4be2f-190">Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz hello [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji hello!</span><span class="sxs-lookup"><span data-stu-id="4be2f-190">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="4be2f-191">Po dodaniu tej aplikacji z hello **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij hello **rejestracji jednokrotnej** hello kartę i dostępu do osadzonych dokumentacji za pośrednictwem hello  **Konfiguracja** sekcji u dołu hello.</span><span class="sxs-lookup"><span data-stu-id="4be2f-191">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="4be2f-192">Więcej o hello osadzonych dokumentacji funkcji w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="4be2f-192">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="4be2f-193">Tworzenie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="4be2f-193">Creating an Azure AD test user</span></span>
<span data-ttu-id="4be2f-194">Celem Hello w tej sekcji jest toocreate użytkownika testowego, w portalu Azure o nazwie Simona Britta hello.</span><span class="sxs-lookup"><span data-stu-id="4be2f-194">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Tworzenie użytkowników usługi Azure AD][100]

<span data-ttu-id="4be2f-196">**toocreate użytkownika testowego w usłudze Azure AD, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="4be2f-196">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="4be2f-197">W hello **portalu Azure**na temat hello w lewym okienku nawigacji, kliknij przycisk **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="4be2f-197">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-lcvista-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="4be2f-199">toodisplay hello listę użytkowników, przejdź zbyt**użytkowników i grup** i kliknij przycisk **wszyscy użytkownicy**.</span><span class="sxs-lookup"><span data-stu-id="4be2f-199">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-lcvista-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="4be2f-201">Witaj tooopen **użytkownika** okna dialogowego, kliknij przycisk **Dodaj** u góry hello hello okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="4be2f-201">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-lcvista-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="4be2f-203">Na powitania **użytkownika** okna dialogowego wykonaj hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="4be2f-203">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-lcvista-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="4be2f-205">a.</span><span class="sxs-lookup"><span data-stu-id="4be2f-205">a.</span></span> <span data-ttu-id="4be2f-206">W hello **nazwa** pole tekstowe, typ **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="4be2f-206">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="4be2f-207">b.</span><span class="sxs-lookup"><span data-stu-id="4be2f-207">b.</span></span> <span data-ttu-id="4be2f-208">W hello **nazwy użytkownika** pole tekstowe, hello typu **adres e-mail** z BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="4be2f-208">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="4be2f-209">c.</span><span class="sxs-lookup"><span data-stu-id="4be2f-209">c.</span></span> <span data-ttu-id="4be2f-210">Wybierz **Pokaż hasło** i zanotuj wartość hello hello **hasło**.</span><span class="sxs-lookup"><span data-stu-id="4be2f-210">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="4be2f-211">d.</span><span class="sxs-lookup"><span data-stu-id="4be2f-211">d.</span></span> <span data-ttu-id="4be2f-212">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="4be2f-212">Click **Create**.</span></span>
 
### <a name="creating-a-lcvista-test-user"></a><span data-ttu-id="4be2f-213">Tworzenie użytkownika testowego LCVista</span><span class="sxs-lookup"><span data-stu-id="4be2f-213">Creating a LCVista test user</span></span>

<span data-ttu-id="4be2f-214">W tej sekcji należy utworzyć użytkownika o nazwie Simona Britta w LCVista.</span><span class="sxs-lookup"><span data-stu-id="4be2f-214">In this section, you create a user called Britta Simon in LCVista.</span></span> <span data-ttu-id="4be2f-215">Należy toocontact [zespołem pomocy technicznej klienta LCVista](https://lcvista.com/contact) tooadd hello użytkowników w hello LCVista aplikacji.</span><span class="sxs-lookup"><span data-stu-id="4be2f-215">You need toocontact [LCVista Client support team](https://lcvista.com/contact) tooadd hello users in hello LCVista application.</span></span> 

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="4be2f-216">Przypisanie użytkownika testowego hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="4be2f-216">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="4be2f-217">W tej sekcji możesz włączyć toouse Simona Britta Azure logowania jednokrotnego za udzielanie dostępu tooLCVista.</span><span class="sxs-lookup"><span data-stu-id="4be2f-217">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooLCVista.</span></span>

![Przypisz użytkownika][200] 

<span data-ttu-id="4be2f-219">**tooassign tooLCVista Simona Britta wykonaj hello następujące kroki:**</span><span class="sxs-lookup"><span data-stu-id="4be2f-219">**tooassign Britta Simon tooLCVista, perform hello following steps:**</span></span>

1. <span data-ttu-id="4be2f-220">W portalu Azure hello, otwórz widok aplikacji hello, a następnie przejdź do widoku katalogu toohello i przejść za**aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="4be2f-220">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Przypisz użytkownika][201] 

2. <span data-ttu-id="4be2f-222">Z listy aplikacji hello wybierz **LCVista**.</span><span class="sxs-lookup"><span data-stu-id="4be2f-222">In hello applications list, select **LCVista**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-lcvista-tutorial/tutorial_lcvista_app.png) 

3. <span data-ttu-id="4be2f-224">W menu powitania po lewej stronie powitania kliknij **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="4be2f-224">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Przypisz użytkownika][202] 

4. <span data-ttu-id="4be2f-226">Kliknij przycisk **Dodaj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="4be2f-226">Click **Add** button.</span></span> <span data-ttu-id="4be2f-227">Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="4be2f-227">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Przypisz użytkownika][203]

5. <span data-ttu-id="4be2f-229">Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** hello listy użytkowników.</span><span class="sxs-lookup"><span data-stu-id="4be2f-229">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="4be2f-230">Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="4be2f-230">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="4be2f-231">Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="4be2f-231">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="4be2f-232">Testowanie rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="4be2f-232">Testing single sign-on</span></span>

<span data-ttu-id="4be2f-233">W tej sekcji można przetestować konfiguracji usługi Azure AD pojedynczego logowania jednokrotnego przy użyciu hello panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="4be2f-233">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span> <span data-ttu-id="4be2f-234">Kliknij Kafelek LCVista hello hello Panel dostępu, będziesz przekierowanie tooOrganization logowania na stronie.</span><span class="sxs-lookup"><span data-stu-id="4be2f-234">Click hello LCVista tile in hello Access Panel, you will be redirected tooOrganization sign on page.</span></span> <span data-ttu-id="4be2f-235">Po pomyślnym logowaniu będzie zalogowane tooyour LCVista aplikacji.</span><span class="sxs-lookup"><span data-stu-id="4be2f-235">After successful login, you will be signed-on tooyour LCVista application.</span></span> <span data-ttu-id="4be2f-236">Aby uzyskać więcej informacji na temat panelu dostępu, zobacz [wprowadzenie do panelu dostępu](https://msdn.microsoft.com/library/dn308586).</span><span class="sxs-lookup"><span data-stu-id="4be2f-236">For more information about the Access Panel, see [Introduction to the Access Panel](https://msdn.microsoft.com/library/dn308586).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="4be2f-237">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="4be2f-237">Additional resources</span></span>

* [<span data-ttu-id="4be2f-238">Lista samouczków dotyczących tooIntegrate aplikacji SaaS w usłudze Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="4be2f-238">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="4be2f-239">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="4be2f-239">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-lcvista-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-lcvista-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-lcvista-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-lcvista-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-lcvista-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-lcvista-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-lcvista-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-lcvista-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-lcvista-tutorial/tutorial_general_203.png

