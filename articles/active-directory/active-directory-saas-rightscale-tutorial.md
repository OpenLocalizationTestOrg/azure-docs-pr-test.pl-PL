---
title: 'Samouczek: Integracji Azure Active Directory z Rightscale | Dokumentacja firmy Microsoft'
description: "Dowiedz się, jak tooconfigure logowanie jednokrotne między usługą Azure Active Directory i Rightscale."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 3a8d376d-95fb-4dd7-832a-4fdd4dd7c87c
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/08/2017
ms.author: jeedes
ms.openlocfilehash: 53b927804a1e0f895778a164386459a4ea816f98
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-rightscale"></a><span data-ttu-id="c20c6-103">Samouczek: Integracji Azure Active Directory z Rightscale</span><span class="sxs-lookup"><span data-stu-id="c20c6-103">Tutorial: Azure Active Directory integration with Rightscale</span></span>

<span data-ttu-id="c20c6-104">Z tego samouczka, dowiesz się, jak toointegrate Rightscale w usłudze Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="c20c6-104">In this tutorial, you learn how toointegrate Rightscale with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="c20c6-105">Integracja z usługą Azure AD Rightscale zapewnia hello następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="c20c6-105">Integrating Rightscale with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="c20c6-106">Można kontrolować w usłudze Azure AD, kto ma dostęp do tooRightscale</span><span class="sxs-lookup"><span data-stu-id="c20c6-106">You can control in Azure AD who has access tooRightscale</span></span>
- <span data-ttu-id="c20c6-107">Można włączyć użytkownika użytkownicy tooautomatically get zalogowane tooRightscale (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="c20c6-107">You can enable your users tooautomatically get signed-on tooRightscale (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="c20c6-108">Możesz zarządzać kont w jednej centralnej lokalizacji - hello portalu Azure</span><span class="sxs-lookup"><span data-stu-id="c20c6-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="c20c6-109">Jeśli chcesz tooknow więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="c20c6-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c20c6-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="c20c6-110">Prerequisites</span></span>

<span data-ttu-id="c20c6-111">tooconfigure integracji z usługą Azure AD z Rightscale należy hello następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="c20c6-111">tooconfigure Azure AD integration with Rightscale, you need hello following items:</span></span>

- <span data-ttu-id="c20c6-112">Subskrypcję usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="c20c6-112">An Azure AD subscription</span></span>
- <span data-ttu-id="c20c6-113">Rightscale logowanie jednokrotne włączone subskrypcji</span><span class="sxs-lookup"><span data-stu-id="c20c6-113">A Rightscale single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="c20c6-114">tootest hello kroków w tym samouczku, zaleca się przy użyciu środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="c20c6-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="c20c6-115">tootest hello kroki opisane w tym samouczku, należy stosować te zalecenia:</span><span class="sxs-lookup"><span data-stu-id="c20c6-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="c20c6-116">Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="c20c6-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="c20c6-117">Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz pobrać miesięczna wersja próbna [tutaj](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="c20c6-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="c20c6-118">Opis scenariusza</span><span class="sxs-lookup"><span data-stu-id="c20c6-118">Scenario description</span></span>
<span data-ttu-id="c20c6-119">W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym.</span><span class="sxs-lookup"><span data-stu-id="c20c6-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="c20c6-120">Scenariusz Hello opisane w tym samouczku składa się z dwóch głównych elementów:</span><span class="sxs-lookup"><span data-stu-id="c20c6-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="c20c6-121">Dodawanie Rightscale z galerii hello</span><span class="sxs-lookup"><span data-stu-id="c20c6-121">Adding Rightscale from hello gallery</span></span>
2. <span data-ttu-id="c20c6-122">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="c20c6-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-rightscale-from-hello-gallery"></a><span data-ttu-id="c20c6-123">Dodawanie Rightscale z galerii hello</span><span class="sxs-lookup"><span data-stu-id="c20c6-123">Adding Rightscale from hello gallery</span></span>
<span data-ttu-id="c20c6-124">tooconfigure hello integracji Rightscale do usługi Azure AD, należy tooadd Rightscale z hello galerii tooyour listę zarządzanych aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="c20c6-124">tooconfigure hello integration of Rightscale into Azure AD, you need tooadd Rightscale from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="c20c6-125">**tooadd Rightscale z galerii hello, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="c20c6-125">**tooadd Rightscale from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="c20c6-126">W hello  **[portalu Azure](https://portal.azure.com)**na temat hello panelu nawigacji po lewej stronie, kliknij przycisk **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="c20c6-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Usługa Active Directory][1]

2. <span data-ttu-id="c20c6-128">Przejdź za**aplikacje dla przedsiębiorstw**.</span><span class="sxs-lookup"><span data-stu-id="c20c6-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="c20c6-129">Następnie przejdź zbyt**wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="c20c6-129">Then go too**All applications**.</span></span>

    ![Aplikacje][2]
    
3. <span data-ttu-id="c20c6-131">tooadd nową aplikację, kliknij przycisk **nowej aplikacji** przycisk u góry hello okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="c20c6-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplikacje][3]

4. <span data-ttu-id="c20c6-133">W polu wyszukiwania hello wpisz **Rightscale**.</span><span class="sxs-lookup"><span data-stu-id="c20c6-133">In hello search box, type **Rightscale**.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-rightscale-tutorial/tutorial_rightscale_search.png)

5. <span data-ttu-id="c20c6-135">W panelu wyników hello zaznacz **Rightscale**, a następnie kliknij przycisk **Dodaj** przycisk aplikacji hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="c20c6-135">In hello results panel, select **Rightscale**, and then click **Add** button tooadd hello application.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-rightscale-tutorial/tutorial_rightscale_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="c20c6-137">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="c20c6-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="c20c6-138">W tej sekcji skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z Rightscale w oparciu o nazwie "Britta Simona" użytkownika testowego.</span><span class="sxs-lookup"><span data-stu-id="c20c6-138">In this section, you configure and test Azure AD single sign-on with Rightscale based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="c20c6-139">Dla pojedynczego logowania jednokrotnego toowork usługi Azure AD musi tooknow użytkownika odpowiednikiem hello w Rightscale jest tooa użytkownika w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c20c6-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Rightscale is tooa user in Azure AD.</span></span> <span data-ttu-id="c20c6-140">Innymi słowy relację łącza między użytkownika usługi Azure AD i hello użytkownikowi w Rightscale musi toobe ustanowione.</span><span class="sxs-lookup"><span data-stu-id="c20c6-140">In other words, a link relationship between an Azure AD user and hello related user in Rightscale needs toobe established.</span></span>

<span data-ttu-id="c20c6-141">W Rightscale, należy przypisać wartość hello hello **nazwy użytkownika** w usłudze Azure AD jako wartość hello hello **Username** tooestablish hello łącze relacji.</span><span class="sxs-lookup"><span data-stu-id="c20c6-141">In Rightscale, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="c20c6-142">tooconfigure i testowych usługi Azure AD rejestracji jednokrotnej z Rightscale, należy po bloków konstrukcyjnych hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="c20c6-142">tooconfigure and test Azure AD single sign-on with Rightscale, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="c20c6-143">**[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configuring-azure-ad-single-sign-on)**  -tooenable Twojego toouse użytkowników tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="c20c6-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="c20c6-144">**[Tworzenie użytkownika testowego usługi Azure AD](#creating-an-azure-ad-test-user)**  -tootest usługi Azure AD rejestracji jednokrotnej z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="c20c6-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="c20c6-145">**[Tworzenie użytkownika testowego Rightscale](#creating-a-rightscale-test-user)**  -toohave odpowiednikiem Simona Britta w Rightscale, który jest połączony toohello usługi Azure AD reprezentację użytkownika.</span><span class="sxs-lookup"><span data-stu-id="c20c6-145">**[Creating a Rightscale test user](#creating-a-rightscale-test-user)** - toohave a counterpart of Britta Simon in Rightscale that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="c20c6-146">**[Przypisanie użytkownika testowego hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Simona Britta toouse usługi Azure AD rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="c20c6-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="c20c6-147">**[Testowanie rejestracji jednokrotnej](#testing-single-sign-on)**  -tooverify czy hello konfiguracji działania.</span><span class="sxs-lookup"><span data-stu-id="c20c6-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="c20c6-148">Konfigurowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="c20c6-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="c20c6-149">W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w portalu Azure hello i skonfigurować logowanie jednokrotne w aplikacji Rightscale.</span><span class="sxs-lookup"><span data-stu-id="c20c6-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Rightscale application.</span></span>

<span data-ttu-id="c20c6-150">**tooconfigure usługi Azure AD rejestracji jednokrotnej z Rightscale, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="c20c6-150">**tooconfigure Azure AD single sign-on with Rightscale, perform hello following steps:**</span></span>

1. <span data-ttu-id="c20c6-151">W portalu Azure na powitania hello **Rightscale** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.</span><span class="sxs-lookup"><span data-stu-id="c20c6-151">In hello Azure portal, on hello **Rightscale** application integration page, click **Single sign-on**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej][4]

2. <span data-ttu-id="c20c6-153">Na powitania **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** tooenable rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="c20c6-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-rightscale-tutorial/tutorial_rightscale_samlbase.png)

3. <span data-ttu-id="c20c6-155">Na powitania **domeny Rightscale i adres URL** sekcji, jeśli chcesz, aby aplikacja hello tooconfigure w **IDP zainicjował tryb** nie masz tooperform wszystkie kroki jako aplikacji hello już jest wstępna Integracja z usługą Azure.</span><span class="sxs-lookup"><span data-stu-id="c20c6-155">On hello **Rightscale Domain and URLs** section, if you wish tooconfigure hello application in **IDP initiated mode** you do not have tooperform any steps as hello app is already pre-integrated with Azure.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-rightscale-tutorial/tutorial_rightscale_url.png)

4. <span data-ttu-id="c20c6-157">Na powitania **domeny Rightscale i adres URL** sekcji, jeśli chcesz, aby aplikacja hello tooconfigure w **SP zainicjował tryb**, wykonaj następujące kroki hello:</span><span class="sxs-lookup"><span data-stu-id="c20c6-157">On hello **Rightscale Domain and URLs** section, if you wish tooconfigure hello application in **SP initiated mode**, perform hello following steps:</span></span>
    
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-rightscale-tutorial/tutorial_rightscale_url1.png)

    <span data-ttu-id="c20c6-159">a.</span><span class="sxs-lookup"><span data-stu-id="c20c6-159">a.</span></span> <span data-ttu-id="c20c6-160">Polecenie hello **Pokaż zaawansowane ustawienia adresu URL**.</span><span class="sxs-lookup"><span data-stu-id="c20c6-160">Click on hello **Show advanced URL settings**.</span></span>

    <span data-ttu-id="c20c6-161">b.</span><span class="sxs-lookup"><span data-stu-id="c20c6-161">b.</span></span> <span data-ttu-id="c20c6-162">W hello **na adres URL logowania** pole tekstowe, wprowadź adres URL hello:`https://login.rightscale.com/`</span><span class="sxs-lookup"><span data-stu-id="c20c6-162">In hello **Sign On URL** textbox, type hello URL: `https://login.rightscale.com/`</span></span>

5. <span data-ttu-id="c20c6-163">Na powitania **certyfikat podpisywania SAML** kliknij **certyfikatu (Base64)** , a następnie zapisz plik certyfikatu hello na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="c20c6-163">On hello **SAML Signing Certificate** section, click **Certificate (Base64)** and then save hello certificate file on your computer.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-rightscale-tutorial/tutorial_rightscale_certificate.png) 

6. <span data-ttu-id="c20c6-165">Kliknij przycisk **zapisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="c20c6-165">Click **Save** button.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-rightscale-tutorial/tutorial_general_400.png)

7. <span data-ttu-id="c20c6-167">Na powitania **konfiguracji Rightscale** kliknij **skonfigurować Rightscale** tooopen **Konfigurowanie logowania jednokrotnego** okna.</span><span class="sxs-lookup"><span data-stu-id="c20c6-167">On hello **Rightscale Configuration** section, click **Configure Rightscale** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="c20c6-168">Kopiuj hello **identyfikator jednostki SAML i SAML pojedynczy znak na adres URL usługi** z hello **sekcji krótkimi opisami.**</span><span class="sxs-lookup"><span data-stu-id="c20c6-168">Copy hello **SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    <span data-ttu-id="c20c6-169">![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-rightscale-tutorial/tutorial_rightscale_configure.png) 
<CS></span><span class="sxs-lookup"><span data-stu-id="c20c6-169">![Configure Single Sign-On](./media/active-directory-saas-rightscale-tutorial/tutorial_rightscale_configure.png) 
<CS></span></span>
8. <span data-ttu-id="c20c6-170">tooget logowania jednokrotnego skonfigurowane dla aplikacji, należy na toosign tooyour RightScale dzierżawy z uprawnieniami administratora.</span><span class="sxs-lookup"><span data-stu-id="c20c6-170">tooget SSO configured for your application, you need toosign-on tooyour RightScale tenant as an administrator.</span></span>

    <span data-ttu-id="c20c6-171">a.</span><span class="sxs-lookup"><span data-stu-id="c20c6-171">a.</span></span> <span data-ttu-id="c20c6-172">W menu hello na górze powitania kliknij hello **ustawienia** i wybierz **rejestracji jednokrotnej**.</span><span class="sxs-lookup"><span data-stu-id="c20c6-172">In hello menu on hello top, click hello **Settings** tab and select **Single Sign-On**.</span></span>
   
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-rightscale-tutorial/tutorial_rightscale_001.png) 

    <span data-ttu-id="c20c6-174">b.</span><span class="sxs-lookup"><span data-stu-id="c20c6-174">b.</span></span> <span data-ttu-id="c20c6-175">Kliknij przycisk hello "**nowe**" tooadd przycisk **Your dostawców tożsamości SAML**.</span><span class="sxs-lookup"><span data-stu-id="c20c6-175">Click hello "**new**" button tooadd **Your SAML Identity Providers**.</span></span>
   
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-rightscale-tutorial/tutorial_rightscale_002.png) 
 
    <span data-ttu-id="c20c6-177">c.</span><span class="sxs-lookup"><span data-stu-id="c20c6-177">c.</span></span> <span data-ttu-id="c20c6-178">W polu tekstowym hello z **Nazwa wyświetlana**, wprowadź nazwę swojej firmy.</span><span class="sxs-lookup"><span data-stu-id="c20c6-178">In hello textbox of **Display Name**, input your company name.</span></span>
   
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-rightscale-tutorial/tutorial_rightscale_003.png)
 
    <span data-ttu-id="c20c6-180">d.</span><span class="sxs-lookup"><span data-stu-id="c20c6-180">d.</span></span> <span data-ttu-id="c20c6-181">Wybierz **inicjowane Zezwalaj RightScale logowania jednokrotnego, używając wskazówki odnajdywania** i wejściowego z **nazwy domeny** w hello poniżej pola tekstowego.</span><span class="sxs-lookup"><span data-stu-id="c20c6-181">Select **Allow RightScale-initiated SSO using a discovery hint** and input your **domain name** in hello below textbox.</span></span>
   
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-rightscale-tutorial/tutorial_rightscale_004.png)

    <span data-ttu-id="c20c6-183">e.</span><span class="sxs-lookup"><span data-stu-id="c20c6-183">e.</span></span> <span data-ttu-id="c20c6-184">Wklej wartość hello **SAML pojedynczy znak na adres URL usługi** , które zostały skopiowane z portalu Azure do **punktu końcowego logowania jednokrotnego SAML** w RightScale.</span><span class="sxs-lookup"><span data-stu-id="c20c6-184">Paste hello value of **SAML Single Sign-On Service URL** which you have copied from Azure portal into **SAML SSO Endpoint** in RightScale.</span></span>
   
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-rightscale-tutorial/tutorial_rightscale_006.png)

    <span data-ttu-id="c20c6-186">f.</span><span class="sxs-lookup"><span data-stu-id="c20c6-186">f.</span></span> <span data-ttu-id="c20c6-187">Wklej wartość hello **identyfikator jednostki SAML** , które zostały skopiowane z portalu Azure do **SAML EntityID** w RightScale.</span><span class="sxs-lookup"><span data-stu-id="c20c6-187">Paste hello value of **SAML Entity ID** which you have copied from Azure portal into **SAML EntityID** in RightScale.</span></span>
   
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-rightscale-tutorial/tutorial_rightscale_008.png)

    <span data-ttu-id="c20c6-189">g.</span><span class="sxs-lookup"><span data-stu-id="c20c6-189">g.</span></span> <span data-ttu-id="c20c6-190">Kliknij przycisk **przeglądarki** przycisk tooupload hello certyfikatu, który został pobrany z portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="c20c6-190">Click **Browser** button tooupload hello certificate which you downloaded from Azure portal.</span></span>
   
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-rightscale-tutorial/tutorial_rightscale_009.png)

    <span data-ttu-id="c20c6-192">h.</span><span class="sxs-lookup"><span data-stu-id="c20c6-192">h.</span></span> <span data-ttu-id="c20c6-193">Kliknij pozycję **Zapisz**.</span><span class="sxs-lookup"><span data-stu-id="c20c6-193">Click **Save**.</span></span>
<CE>
> [!TIP]
> <span data-ttu-id="c20c6-194">Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz hello [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji hello!</span><span class="sxs-lookup"><span data-stu-id="c20c6-194">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="c20c6-195">Po dodaniu tej aplikacji z hello **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij hello **rejestracji jednokrotnej** hello kartę i dostępu do osadzonych dokumentacji za pośrednictwem hello  **Konfiguracja** sekcji u dołu hello.</span><span class="sxs-lookup"><span data-stu-id="c20c6-195">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="c20c6-196">Więcej o hello osadzonych dokumentacji funkcji w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="c20c6-196">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="c20c6-197">Tworzenie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="c20c6-197">Creating an Azure AD test user</span></span>
<span data-ttu-id="c20c6-198">Celem Hello w tej sekcji jest toocreate użytkownika testowego, w portalu Azure o nazwie Simona Britta hello.</span><span class="sxs-lookup"><span data-stu-id="c20c6-198">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Tworzenie użytkowników usługi Azure AD][100]

<span data-ttu-id="c20c6-200">**toocreate użytkownika testowego w usłudze Azure AD, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="c20c6-200">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="c20c6-201">W hello **portalu Azure**na temat hello w lewym okienku nawigacji, kliknij przycisk **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="c20c6-201">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-rightscale-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="c20c6-203">toodisplay hello listę użytkowników, przejdź zbyt**użytkowników i grup** i kliknij przycisk **wszyscy użytkownicy**.</span><span class="sxs-lookup"><span data-stu-id="c20c6-203">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-rightscale-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="c20c6-205">Witaj tooopen **użytkownika** okna dialogowego, kliknij przycisk **Dodaj** u góry hello hello okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="c20c6-205">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-rightscale-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="c20c6-207">Na powitania **użytkownika** okna dialogowego wykonaj hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="c20c6-207">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-rightscale-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="c20c6-209">a.</span><span class="sxs-lookup"><span data-stu-id="c20c6-209">a.</span></span> <span data-ttu-id="c20c6-210">W hello **nazwa** pole tekstowe, typ **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="c20c6-210">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="c20c6-211">b.</span><span class="sxs-lookup"><span data-stu-id="c20c6-211">b.</span></span> <span data-ttu-id="c20c6-212">W hello **nazwy użytkownika** pole tekstowe, hello typu **adres e-mail** z BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="c20c6-212">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="c20c6-213">c.</span><span class="sxs-lookup"><span data-stu-id="c20c6-213">c.</span></span> <span data-ttu-id="c20c6-214">Wybierz **Pokaż hasło** i zanotuj wartość hello hello **hasło**.</span><span class="sxs-lookup"><span data-stu-id="c20c6-214">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="c20c6-215">d.</span><span class="sxs-lookup"><span data-stu-id="c20c6-215">d.</span></span> <span data-ttu-id="c20c6-216">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="c20c6-216">Click **Create**.</span></span>
 
### <a name="creating-a-rightscale-test-user"></a><span data-ttu-id="c20c6-217">Tworzenie użytkownika testowego Rightscale</span><span class="sxs-lookup"><span data-stu-id="c20c6-217">Creating a Rightscale test user</span></span>

<span data-ttu-id="c20c6-218">W tej sekcji należy utworzyć użytkownika o nazwie Simona Britta w RightScale.</span><span class="sxs-lookup"><span data-stu-id="c20c6-218">In this section, you create a user called Britta Simon in RightScale.</span></span> <span data-ttu-id="c20c6-219">Praca z [zespołem pomocy technicznej klienta Rightscale](mailto:support@rightscale.com) tooadd hello użytkowników hello RightScale platformy.</span><span class="sxs-lookup"><span data-stu-id="c20c6-219">Work with [Rightscale Client support team](mailto:support@rightscale.com) tooadd hello users in hello RightScale platform.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="c20c6-220">Przypisanie użytkownika testowego hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="c20c6-220">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="c20c6-221">W tej sekcji możesz włączyć toouse Simona Britta Azure logowania jednokrotnego za udzielanie dostępu tooRightscale.</span><span class="sxs-lookup"><span data-stu-id="c20c6-221">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooRightscale.</span></span>

![Przypisz użytkownika][200] 

<span data-ttu-id="c20c6-223">**tooassign tooRightscale Simona Britta wykonaj hello następujące kroki:**</span><span class="sxs-lookup"><span data-stu-id="c20c6-223">**tooassign Britta Simon tooRightscale, perform hello following steps:**</span></span>

1. <span data-ttu-id="c20c6-224">W portalu Azure hello, otwórz widok aplikacji hello, a następnie przejdź do widoku katalogu toohello i przejść za**aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="c20c6-224">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Przypisz użytkownika][201] 

2. <span data-ttu-id="c20c6-226">Z listy aplikacji hello wybierz **Rightscale**.</span><span class="sxs-lookup"><span data-stu-id="c20c6-226">In hello applications list, select **Rightscale**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-rightscale-tutorial/tutorial_rightscale_app.png) 

3. <span data-ttu-id="c20c6-228">W menu powitania po lewej stronie powitania kliknij **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="c20c6-228">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Przypisz użytkownika][202] 

4. <span data-ttu-id="c20c6-230">Kliknij przycisk **Dodaj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="c20c6-230">Click **Add** button.</span></span> <span data-ttu-id="c20c6-231">Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="c20c6-231">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Przypisz użytkownika][203]

5. <span data-ttu-id="c20c6-233">Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** hello listy użytkowników.</span><span class="sxs-lookup"><span data-stu-id="c20c6-233">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="c20c6-234">Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="c20c6-234">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="c20c6-235">Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="c20c6-235">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="c20c6-236">Testowanie rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="c20c6-236">Testing single sign-on</span></span>

<span data-ttu-id="c20c6-237">Celem Hello w tej sekcji jest tootest programu Azure AD SSO konfiguracji przy użyciu hello panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="c20c6-237">hello objective of this section is tootest your Azure AD SSO configuration using hello Access Panel.</span></span>  

<span data-ttu-id="c20c6-238">Po kliknięciu kafelka RightScale hello w hello Panel dostępu, należy pobrać automatycznie zalogowane tooyour RightScale aplikacji.</span><span class="sxs-lookup"><span data-stu-id="c20c6-238">When you click hello RightScale tile in hello Access Panel, you should get automatically signed-on tooyour RightScale application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="c20c6-239">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="c20c6-239">Additional resources</span></span>

* [<span data-ttu-id="c20c6-240">Lista samouczków dotyczących tooIntegrate aplikacji SaaS w usłudze Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="c20c6-240">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="c20c6-241">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="c20c6-241">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-rightscale-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-rightscale-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-rightscale-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-rightscale-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-rightscale-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-rightscale-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-rightscale-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-rightscale-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-rightscale-tutorial/tutorial_general_203.png

