---
title: 'Samouczek: Azure Active Directory integracji z oprogramowaniem Igloo | Dokumentacja firmy Microsoft'
description: "Dowiedz się, jak tooconfigure logowanie jednokrotne między oprogramowaniem Igloo i Azure Active Directory."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 2eb625c1-d3fc-4ae1-a304-6a6733a10e6e
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/23/2017
ms.author: jeedes
ms.openlocfilehash: 406405d4faa6e56f1005a61e69a29ef2ef2eb34b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-igloo-software"></a><span data-ttu-id="50800-103">Samouczek: Azure Active Directory integracji z oprogramowaniem Igloo</span><span class="sxs-lookup"><span data-stu-id="50800-103">Tutorial: Azure Active Directory integration with Igloo Software</span></span>

<span data-ttu-id="50800-104">Z tego samouczka, dowiesz się, jak toointegrate Igloo oprogramowania w usłudze Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="50800-104">In this tutorial, you learn how toointegrate Igloo Software with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="50800-105">Integracja oprogramowania Igloo z usługą Azure AD zapewnia hello następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="50800-105">Integrating Igloo Software with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="50800-106">Można kontrolować w usłudze Azure AD, kto ma dostęp do tooIgloo oprogramowania</span><span class="sxs-lookup"><span data-stu-id="50800-106">You can control in Azure AD who has access tooIgloo Software</span></span>
- <span data-ttu-id="50800-107">Można włączyć użytkownika użytkownicy tooautomatically get zalogowane tooIgloo oprogramowania (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="50800-107">You can enable your users tooautomatically get signed-on tooIgloo Software (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="50800-108">Możesz zarządzać kont w jednej centralnej lokalizacji - hello portalu Azure</span><span class="sxs-lookup"><span data-stu-id="50800-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="50800-109">Jeśli chcesz tooknow więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="50800-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="50800-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="50800-110">Prerequisites</span></span>

<span data-ttu-id="50800-111">tooconfigure integracji usługi Azure AD z oprogramowaniem Igloo należy hello następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="50800-111">tooconfigure Azure AD integration with Igloo Software, you need hello following items:</span></span>

- <span data-ttu-id="50800-112">Subskrypcję usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="50800-112">An Azure AD subscription</span></span>
- <span data-ttu-id="50800-113">Oprogramowanie Igloo logowanie jednokrotne włączone subskrypcji</span><span class="sxs-lookup"><span data-stu-id="50800-113">An Igloo Software single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="50800-114">tootest hello kroków w tym samouczku, zaleca się przy użyciu środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="50800-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="50800-115">tootest hello kroki opisane w tym samouczku, należy stosować te zalecenia:</span><span class="sxs-lookup"><span data-stu-id="50800-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="50800-116">Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="50800-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="50800-117">Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz pobrać miesięczna wersja próbna [tutaj](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="50800-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="50800-118">Opis scenariusza</span><span class="sxs-lookup"><span data-stu-id="50800-118">Scenario description</span></span>
<span data-ttu-id="50800-119">W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym.</span><span class="sxs-lookup"><span data-stu-id="50800-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="50800-120">Scenariusz Hello opisane w tym samouczku składa się z dwóch głównych elementów:</span><span class="sxs-lookup"><span data-stu-id="50800-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="50800-121">Dodawanie oprogramowania Igloo z galerii hello</span><span class="sxs-lookup"><span data-stu-id="50800-121">Adding Igloo Software from hello gallery</span></span>
2. <span data-ttu-id="50800-122">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="50800-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-igloo-software-from-hello-gallery"></a><span data-ttu-id="50800-123">Dodawanie oprogramowania Igloo z galerii hello</span><span class="sxs-lookup"><span data-stu-id="50800-123">Adding Igloo Software from hello gallery</span></span>
<span data-ttu-id="50800-124">tooconfigure hello integracji Igloo oprogramowania do usługi Azure AD, należy tooadd Igloo oprogramowania z listy tooyour galerii hello zarządzanych aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="50800-124">tooconfigure hello integration of Igloo Software into Azure AD, you need tooadd Igloo Software from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="50800-125">**tooadd Igloo oprogramowania z galerii hello wykonaj hello następujące kroki:**</span><span class="sxs-lookup"><span data-stu-id="50800-125">**tooadd Igloo Software from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="50800-126">W hello  **[portalu Azure](https://portal.azure.com)**na temat hello panelu nawigacji po lewej stronie, kliknij przycisk **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="50800-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Usługa Active Directory][1]

2. <span data-ttu-id="50800-128">Przejdź za**aplikacje dla przedsiębiorstw**.</span><span class="sxs-lookup"><span data-stu-id="50800-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="50800-129">Następnie przejdź zbyt**wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="50800-129">Then go too**All applications**.</span></span>

    ![Aplikacje][2]
    
3. <span data-ttu-id="50800-131">tooadd nową aplikację, kliknij przycisk **nowej aplikacji** przycisk u góry hello okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="50800-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplikacje][3]

4. <span data-ttu-id="50800-133">W polu wyszukiwania hello wpisz **oprogramowania Igloo**.</span><span class="sxs-lookup"><span data-stu-id="50800-133">In hello search box, type **Igloo Software**.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-igloo-software-tutorial/tutorial_igloosoftware_search.png)

5. <span data-ttu-id="50800-135">W panelu wyników hello, wybierz **oprogramowania Igloo**, a następnie kliknij przycisk **Dodaj** przycisk aplikacji hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="50800-135">In hello results panel, select **Igloo Software**, and then click **Add** button tooadd hello application.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-igloo-software-tutorial/tutorial_igloosoftware_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="50800-137">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="50800-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="50800-138">W tej sekcji skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z oprogramowaniem Igloo w oparciu o nazwie "Britta Simona" użytkownika testowego.</span><span class="sxs-lookup"><span data-stu-id="50800-138">In this section, you configure and test Azure AD single sign-on with Igloo Software based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="50800-139">Dla pojedynczego logowania jednokrotnego toowork usługi Azure AD musi tooknow użytkownika odpowiednikiem hello w oprogramowaniu Igloo jest tooa użytkownika w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="50800-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Igloo Software is tooa user in Azure AD.</span></span> <span data-ttu-id="50800-140">Innymi słowy relację łącza między użytkownika usługi Azure AD i hello użytkownikowi w oprogramowaniu Igloo musi toobe ustanowione.</span><span class="sxs-lookup"><span data-stu-id="50800-140">In other words, a link relationship between an Azure AD user and hello related user in Igloo Software needs toobe established.</span></span>

<span data-ttu-id="50800-141">W oprogramowaniu Igloo, należy przypisać wartość hello hello **nazwy użytkownika** w usłudze Azure AD jako wartość hello hello **Username** tooestablish hello łącze relacji.</span><span class="sxs-lookup"><span data-stu-id="50800-141">In Igloo Software, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="50800-142">tooconfigure i testowych usługi Azure AD rejestracji jednokrotnej z oprogramowaniem Igloo, należy po bloków konstrukcyjnych hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="50800-142">tooconfigure and test Azure AD single sign-on with Igloo Software, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="50800-143">**[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configuring-azure-ad-single-sign-on)**  -tooenable Twojego toouse użytkowników tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="50800-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="50800-144">**[Tworzenie użytkownika testowego usługi Azure AD](#creating-an-azure-ad-test-user)**  -tootest usługi Azure AD rejestracji jednokrotnej z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="50800-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="50800-145">**[Tworzenie użytkownika testowego oprogramowania Igloo](#creating-an-igloo-software-test-user)**  -toohave odpowiednikiem Simona Britta Igloo oprogramowania, który jest połączony toohello usługi Azure AD reprezentację użytkownika.</span><span class="sxs-lookup"><span data-stu-id="50800-145">**[Creating an Igloo Software test user](#creating-an-igloo-software-test-user)** - toohave a counterpart of Britta Simon in Igloo Software that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="50800-146">**[Przypisanie użytkownika testowego hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Simona Britta toouse usługi Azure AD rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="50800-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="50800-147">**[Testowanie rejestracji jednokrotnej](#testing-single-sign-on)**  -tooverify czy hello konfiguracji działania.</span><span class="sxs-lookup"><span data-stu-id="50800-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="50800-148">Konfigurowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="50800-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="50800-149">W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w hello portalu Azure i skonfigurować rejestracji jednokrotnej w używanej aplikacji Igloo.</span><span class="sxs-lookup"><span data-stu-id="50800-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Igloo Software application.</span></span>

<span data-ttu-id="50800-150">**tooconfigure usługi Azure AD rejestracji jednokrotnej z oprogramowaniem Igloo wykonaj hello następujące kroki:**</span><span class="sxs-lookup"><span data-stu-id="50800-150">**tooconfigure Azure AD single sign-on with Igloo Software, perform hello following steps:**</span></span>

1. <span data-ttu-id="50800-151">W portalu Azure na powitania hello **oprogramowania Igloo** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.</span><span class="sxs-lookup"><span data-stu-id="50800-151">In hello Azure portal, on hello **Igloo Software** application integration page, click **Single sign-on**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej][4]

2. <span data-ttu-id="50800-153">Na powitania **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** tooenable rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="50800-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-igloo-software-tutorial/tutorial_igloosoftware_samlbase.png)

3. <span data-ttu-id="50800-155">Na powitania **Igloo oprogramowania domeny i adres URL** sekcji, wykonaj następujące kroki hello:</span><span class="sxs-lookup"><span data-stu-id="50800-155">On hello **Igloo Software Domain and URLs** section, perform hello following steps:</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-igloo-software-tutorial/tutorial_igloosoftware_url.png)
    
    <span data-ttu-id="50800-157">a.</span><span class="sxs-lookup"><span data-stu-id="50800-157">a.</span></span> <span data-ttu-id="50800-158">W hello **adres URL logowania** tekstowym, wpisz adres URL za pomocą hello następującego wzorca:`https://<company name>.igloocommmunities.com`</span><span class="sxs-lookup"><span data-stu-id="50800-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<company name>.igloocommmunities.com`</span></span>

    <span data-ttu-id="50800-159">b.</span><span class="sxs-lookup"><span data-stu-id="50800-159">b.</span></span> <span data-ttu-id="50800-160">W hello **identyfikator** tekstowym, wpisz adres URL za pomocą hello następującego wzorca:`https://<company name>.igloocommmunities.com/saml.digest`</span><span class="sxs-lookup"><span data-stu-id="50800-160">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<company name>.igloocommmunities.com/saml.digest`</span></span>

    <span data-ttu-id="50800-161">c.</span><span class="sxs-lookup"><span data-stu-id="50800-161">c.</span></span> <span data-ttu-id="50800-162">W hello **adres URL odpowiedzi** tekstowym, wpisz adres URL za pomocą hello następującego wzorca:`https://<company name>.igloocommmunities.com/saml.digest`</span><span class="sxs-lookup"><span data-stu-id="50800-162">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://<company name>.igloocommmunities.com/saml.digest`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="50800-163">Wartości te nie są prawdziwe.</span><span class="sxs-lookup"><span data-stu-id="50800-163">These values are not real.</span></span> <span data-ttu-id="50800-164">Zaktualizować te wartości z hello rzeczywisty identyfikator, adres URL odpowiedzi i adres URL logowania.</span><span class="sxs-lookup"><span data-stu-id="50800-164">Update these values with hello actual Identifier, Reply URL, and Sign-On URL.</span></span> <span data-ttu-id="50800-165">Skontaktuj się z [zespołem pomocy technicznej klienta oprogramowania Igloo](https://www.igloosoftware.com/services/support) tooget tych wartości.</span><span class="sxs-lookup"><span data-stu-id="50800-165">Contact [Igloo Software Client support team](https://www.igloosoftware.com/services/support) tooget these values.</span></span> 

4. <span data-ttu-id="50800-166">Na powitania **certyfikat podpisywania SAML** kliknij **Certificate(Base64)** , a następnie zapisz plik certyfikatu hello na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="50800-166">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-igloo-software-tutorial/tutorial_igloosoftware_certificate.png) 

5. <span data-ttu-id="50800-168">Kliknij przycisk **zapisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="50800-168">Click **Save** button.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-igloo-software-tutorial/tutorial_general_400.png)
    
6. <span data-ttu-id="50800-170">Na powitania **konfiguracji oprogramowania Igloo** kliknij **Konfigurowanie oprogramowania Igloo** tooopen **Konfigurowanie logowania jednokrotnego** okna.</span><span class="sxs-lookup"><span data-stu-id="50800-170">On hello **Igloo Software Configuration** section, click **Configure Igloo Software** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="50800-171">Kopiuj hello **Sign-Out adresu URL i SAML pojedynczy znak na adres URL usługi** z hello **sekcji krótkimi opisami.**</span><span class="sxs-lookup"><span data-stu-id="50800-171">Copy hello **Sign-Out URL and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-igloo-software-tutorial/tutorial_igloosoftware_configure.png) 

7. <span data-ttu-id="50800-173">W oknie przeglądarki innej witryny sieci web Zaloguj się w witrynie firmy oprogramowania Igloo tooyour jako administrator.</span><span class="sxs-lookup"><span data-stu-id="50800-173">In a different web browser window, log in tooyour Igloo Software company site as an administrator.</span></span>

8. <span data-ttu-id="50800-174">Przejdź toohello **Panelu sterowania**.</span><span class="sxs-lookup"><span data-stu-id="50800-174">Go toohello **Control Panel**.</span></span>
   
     <span data-ttu-id="50800-175">![Panel sterowania](./media/active-directory-saas-igloo-software-tutorial/ic799949.png "Panel sterowania")</span><span class="sxs-lookup"><span data-stu-id="50800-175">![Control Panel](./media/active-directory-saas-igloo-software-tutorial/ic799949.png "Control Panel")</span></span>

9. <span data-ttu-id="50800-176">W hello **członkostwa** , kliknij pozycję **znak ustawień**.</span><span class="sxs-lookup"><span data-stu-id="50800-176">In hello **Membership** tab, click **Sign In Settings**.</span></span>
   
    <span data-ttu-id="50800-177">![Zaloguj się w ustawieniach](./media/active-directory-saas-igloo-software-tutorial/ic783968.png "Zaloguj ustawienia")</span><span class="sxs-lookup"><span data-stu-id="50800-177">![Sign in Settings](./media/active-directory-saas-igloo-software-tutorial/ic783968.png "Sign in Settings")</span></span>

10. <span data-ttu-id="50800-178">W sekcji konfiguracji SAML hello, kliknij przycisk **skonfigurować uwierzytelnianie SAML**.</span><span class="sxs-lookup"><span data-stu-id="50800-178">In hello SAML Configuration section, click **Configure SAML Authentication**.</span></span>
   
    <span data-ttu-id="50800-179">![Konfiguracja SAML](./media/active-directory-saas-igloo-software-tutorial/ic783969.png "Konfiguracja SAML")</span><span class="sxs-lookup"><span data-stu-id="50800-179">![SAML Configuration](./media/active-directory-saas-igloo-software-tutorial/ic783969.png "SAML Configuration")</span></span>
   
11. <span data-ttu-id="50800-180">W hello **Konfiguracja ogólna** sekcji, wykonaj następujące kroki hello:</span><span class="sxs-lookup"><span data-stu-id="50800-180">In hello **General Configuration** section, perform hello following steps:</span></span>
   
    <span data-ttu-id="50800-181">![Konfiguracja ogólna](./media/active-directory-saas-igloo-software-tutorial/ic783970.png "konfiguracji ogólnej")</span><span class="sxs-lookup"><span data-stu-id="50800-181">![General Configuration](./media/active-directory-saas-igloo-software-tutorial/ic783970.png "General Configuration")</span></span>

    <span data-ttu-id="50800-182">a.</span><span class="sxs-lookup"><span data-stu-id="50800-182">a.</span></span> <span data-ttu-id="50800-183">W hello **nazwa połączenia** tekstowym, wpisz nazwę niestandardową dla danej konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="50800-183">In hello **Connection Name** textbox, type a custom name for your configuration.</span></span>
   
    <span data-ttu-id="50800-184">b.</span><span class="sxs-lookup"><span data-stu-id="50800-184">b.</span></span> <span data-ttu-id="50800-185">W hello **adres URL logowania IdP** pole tekstowe, Wklej wartość hello **SAML pojedynczy znak na adres URL usługi** którego została skopiowana z portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="50800-185">In hello **IdP Login URL** textbox, paste hello value of **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span></span>
   
    <span data-ttu-id="50800-186">c.</span><span class="sxs-lookup"><span data-stu-id="50800-186">c.</span></span> <span data-ttu-id="50800-187">W hello **adresu URL wylogowania IdP** pole tekstowe, Wklej wartość hello **Sign-Out URL** którego została skopiowana z portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="50800-187">In hello **IdP Logout URL** textbox, paste hello value of **Sign-Out URL** which you have copied from Azure portal.</span></span>
    
    <span data-ttu-id="50800-188">d.</span><span class="sxs-lookup"><span data-stu-id="50800-188">d.</span></span> <span data-ttu-id="50800-189">Wybierz **wylogowania odpowiedzi i żądania HTTP typu** jako **POST**.</span><span class="sxs-lookup"><span data-stu-id="50800-189">Select **Logout Response and Request HTTP Type** as **POST**.</span></span>
   
    <span data-ttu-id="50800-190">e.</span><span class="sxs-lookup"><span data-stu-id="50800-190">e.</span></span> <span data-ttu-id="50800-191">Otwórz z **base-64** zakodowany certyfikat w Notatniku pobrany z portalu Azure, hello kopiowania zawartości go do Schowka, a następnie wklej go toohello **certyfikatu publicznego** pola tekstowego.</span><span class="sxs-lookup"><span data-stu-id="50800-191">Open your **base-64** encoded certificate in notepad downloaded from Azure portal, copy hello content of it into your clipboard, and then paste it toohello **Public Certificate** textbox.</span></span>
    
12. <span data-ttu-id="50800-192">W hello **odpowiedzi i konfiguracji uwierzytelniania**, wykonaj następujące kroki hello:</span><span class="sxs-lookup"><span data-stu-id="50800-192">In hello **Response and Authentication Configuration**, perform hello following steps:</span></span>
    
    <span data-ttu-id="50800-193">![Odpowiedź i konfiguracji uwierzytelniania](./media/active-directory-saas-igloo-software-tutorial/IC783971.png "odpowiedzi i konfiguracji uwierzytelniania")</span><span class="sxs-lookup"><span data-stu-id="50800-193">![Response and Authentication Configuration](./media/active-directory-saas-igloo-software-tutorial/IC783971.png "Response and Authentication Configuration")</span></span>
  
      <span data-ttu-id="50800-194">a.</span><span class="sxs-lookup"><span data-stu-id="50800-194">a.</span></span> <span data-ttu-id="50800-195">Jako **dostawcy tożsamości**, wybierz pozycję **Microsoft ADFS**.</span><span class="sxs-lookup"><span data-stu-id="50800-195">As **Identity Provider**, select **Microsoft ADFS**.</span></span>
      
      <span data-ttu-id="50800-196">b.</span><span class="sxs-lookup"><span data-stu-id="50800-196">b.</span></span> <span data-ttu-id="50800-197">Jako **typ identyfikatora**, wybierz pozycję **adres E-mail**.</span><span class="sxs-lookup"><span data-stu-id="50800-197">As **Identifier Type**, select **Email Address**.</span></span> 

      <span data-ttu-id="50800-198">c.</span><span class="sxs-lookup"><span data-stu-id="50800-198">c.</span></span> <span data-ttu-id="50800-199">W hello **atrybut poczty E-mail** pole tekstowe, typ **emailaddress**.</span><span class="sxs-lookup"><span data-stu-id="50800-199">In hello **Email Attribute** textbox, type **emailaddress**.</span></span>

      <span data-ttu-id="50800-200">d.</span><span class="sxs-lookup"><span data-stu-id="50800-200">d.</span></span> <span data-ttu-id="50800-201">W hello **atrybutu imię** pole tekstowe, typ **givenname**.</span><span class="sxs-lookup"><span data-stu-id="50800-201">In hello **First Name Attribute** textbox, type **givenname**.</span></span>

      <span data-ttu-id="50800-202">e.</span><span class="sxs-lookup"><span data-stu-id="50800-202">e.</span></span> <span data-ttu-id="50800-203">W hello **ostatniego atrybutu Name** pole tekstowe, typ **nazwisko**.</span><span class="sxs-lookup"><span data-stu-id="50800-203">In hello **Last Name Attribute** textbox, type **surname**.</span></span>

13. <span data-ttu-id="50800-204">Wykonaj następujące kroki toocomplete hello konfiguracji hello:</span><span class="sxs-lookup"><span data-stu-id="50800-204">Perform hello following steps toocomplete hello configuration:</span></span>
    
    <span data-ttu-id="50800-205">![Tworzenie użytkownika na logowania](./media/active-directory-saas-igloo-software-tutorial/IC783972.png "Tworzenie użytkownika na logowania")</span><span class="sxs-lookup"><span data-stu-id="50800-205">![User creation on Sign in](./media/active-directory-saas-igloo-software-tutorial/IC783972.png "User creation on Sign in")</span></span> 

     <span data-ttu-id="50800-206">a.</span><span class="sxs-lookup"><span data-stu-id="50800-206">a.</span></span> <span data-ttu-id="50800-207">Jako **Tworzenie użytkownika na logowania**, wybierz pozycję **utworzenie nowego użytkownika w swojej witrynie, po zalogowaniu**.</span><span class="sxs-lookup"><span data-stu-id="50800-207">As **User creation on Sign in**, select **Create a new user in your site when they sign in**.</span></span>

     <span data-ttu-id="50800-208">b.</span><span class="sxs-lookup"><span data-stu-id="50800-208">b.</span></span> <span data-ttu-id="50800-209">Jako **Zaloguj ustawienia**, wybierz pozycję **SAML użyj przycisku na ekranie "Zaloguj"**.</span><span class="sxs-lookup"><span data-stu-id="50800-209">As **Sign in Settings**, select **Use SAML button on “Sign in” screen**.</span></span>

     <span data-ttu-id="50800-210">c.</span><span class="sxs-lookup"><span data-stu-id="50800-210">c.</span></span> <span data-ttu-id="50800-211">Kliknij pozycję **Zapisz**.</span><span class="sxs-lookup"><span data-stu-id="50800-211">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="50800-212">Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz hello [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji hello!</span><span class="sxs-lookup"><span data-stu-id="50800-212">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="50800-213">Po dodaniu tej aplikacji z hello **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij hello **rejestracji jednokrotnej** hello kartę i dostępu do osadzonych dokumentacji za pośrednictwem hello  **Konfiguracja** sekcji u dołu hello.</span><span class="sxs-lookup"><span data-stu-id="50800-213">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="50800-214">Więcej o hello osadzonych dokumentacji funkcji w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="50800-214">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="50800-215">Tworzenie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="50800-215">Creating an Azure AD test user</span></span>
<span data-ttu-id="50800-216">Celem Hello w tej sekcji jest toocreate użytkownika testowego, w portalu Azure o nazwie Simona Britta hello.</span><span class="sxs-lookup"><span data-stu-id="50800-216">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Tworzenie użytkowników usługi Azure AD][100]

<span data-ttu-id="50800-218">**toocreate użytkownika testowego w usłudze Azure AD, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="50800-218">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="50800-219">W hello **portalu Azure**na temat hello w lewym okienku nawigacji, kliknij przycisk **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="50800-219">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-igloo-software-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="50800-221">toodisplay hello listę użytkowników, przejdź zbyt**użytkowników i grup** i kliknij przycisk **wszyscy użytkownicy**.</span><span class="sxs-lookup"><span data-stu-id="50800-221">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-igloo-software-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="50800-223">Witaj tooopen **użytkownika** okna dialogowego, kliknij przycisk **Dodaj** u góry hello hello okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="50800-223">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-igloo-software-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="50800-225">Na powitania **użytkownika** okna dialogowego wykonaj hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="50800-225">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-igloo-software-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="50800-227">a.</span><span class="sxs-lookup"><span data-stu-id="50800-227">a.</span></span> <span data-ttu-id="50800-228">W hello **nazwa** pole tekstowe, typ **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="50800-228">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="50800-229">b.</span><span class="sxs-lookup"><span data-stu-id="50800-229">b.</span></span> <span data-ttu-id="50800-230">W hello **nazwy użytkownika** pole tekstowe, hello typu **adres e-mail** z BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="50800-230">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="50800-231">c.</span><span class="sxs-lookup"><span data-stu-id="50800-231">c.</span></span> <span data-ttu-id="50800-232">Wybierz **Pokaż hasło** i zanotuj wartość hello hello **hasło**.</span><span class="sxs-lookup"><span data-stu-id="50800-232">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="50800-233">d.</span><span class="sxs-lookup"><span data-stu-id="50800-233">d.</span></span> <span data-ttu-id="50800-234">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="50800-234">Click **Create**.</span></span>
 
### <a name="creating-an-igloo-software-test-user"></a><span data-ttu-id="50800-235">Tworzenie użytkownika testowego Igloo oprogramowania</span><span class="sxs-lookup"><span data-stu-id="50800-235">Creating an Igloo Software test user</span></span>

<span data-ttu-id="50800-236">Nie ma elementu akcji można tooconfigure użytkownika inicjowania obsługi administracyjnej tooIgloo oprogramowania.</span><span class="sxs-lookup"><span data-stu-id="50800-236">There is no action item for you tooconfigure user provisioning tooIgloo Software.</span></span>  

<span data-ttu-id="50800-237">Gdy toolog prób przypisany użytkownik za pomocą oprogramowania tooIgloo hello panel dostępu, Igloo oprogramowania sprawdza, czy użytkownik hello istnieje.</span><span class="sxs-lookup"><span data-stu-id="50800-237">When an assigned user tries toolog in tooIgloo Software using hello access panel, Igloo Software checks whether hello user exists.</span></span>  <span data-ttu-id="50800-238">Jeśli nie jest Brak konta użytkownika dostępny jeszcze, są tworzone przez oprogramowanie Igloo.</span><span class="sxs-lookup"><span data-stu-id="50800-238">If there is no user account available yet, it is automatically created by Igloo Software.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="50800-239">Przypisanie użytkownika testowego hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="50800-239">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="50800-240">W tej sekcji możesz włączyć toouse Simona Britta Azure logowania jednokrotnego za udzielanie dostępu tooIgloo oprogramowania.</span><span class="sxs-lookup"><span data-stu-id="50800-240">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooIgloo Software.</span></span>

![Przypisz użytkownika][200] 

<span data-ttu-id="50800-242">**tooassign tooIgloo Simona Britta oprogramowania, wykonaj hello następujące kroki:**</span><span class="sxs-lookup"><span data-stu-id="50800-242">**tooassign Britta Simon tooIgloo Software, perform hello following steps:**</span></span>

1. <span data-ttu-id="50800-243">W portalu Azure hello, otwórz widok aplikacji hello, a następnie przejdź do widoku katalogu toohello i przejść za**aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="50800-243">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Przypisz użytkownika][201] 

2. <span data-ttu-id="50800-245">Z listy aplikacji hello wybierz **oprogramowania Igloo**.</span><span class="sxs-lookup"><span data-stu-id="50800-245">In hello applications list, select **Igloo Software**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-igloo-software-tutorial/tutorial_igloosoftware_app.png) 

3. <span data-ttu-id="50800-247">W menu powitania po lewej stronie powitania kliknij **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="50800-247">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Przypisz użytkownika][202] 

4. <span data-ttu-id="50800-249">Kliknij przycisk **Dodaj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="50800-249">Click **Add** button.</span></span> <span data-ttu-id="50800-250">Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="50800-250">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Przypisz użytkownika][203]

5. <span data-ttu-id="50800-252">Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** hello listy użytkowników.</span><span class="sxs-lookup"><span data-stu-id="50800-252">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="50800-253">Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="50800-253">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="50800-254">Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="50800-254">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="50800-255">Testowanie rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="50800-255">Testing single sign-on</span></span>

<span data-ttu-id="50800-256">W tej sekcji można przetestować konfiguracji usługi Azure AD pojedynczego logowania jednokrotnego przy użyciu hello panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="50800-256">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="50800-257">Po kliknięciu kafelka oprogramowania Igloo hello w hello Panel dostępu, należy pobrać automatycznie zalogowane tooyour Igloo aplikacji.</span><span class="sxs-lookup"><span data-stu-id="50800-257">When you click hello Igloo Software tile in hello Access Panel, you should get automatically signed-on tooyour Igloo Software application.</span></span>
<span data-ttu-id="50800-258">Aby uzyskać więcej informacji na temat panelu dostępu, zobacz [toohello wprowadzenie panelu dostępu](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="50800-258">For more information about the Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="50800-259">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="50800-259">Additional resources</span></span>

* [<span data-ttu-id="50800-260">Lista samouczków dotyczących tooIntegrate aplikacji SaaS w usłudze Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="50800-260">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="50800-261">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="50800-261">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-igloo-software-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-igloo-software-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-igloo-software-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-igloo-software-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-igloo-software-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-igloo-software-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-igloo-software-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-igloo-software-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-igloo-software-tutorial/tutorial_general_203.png

