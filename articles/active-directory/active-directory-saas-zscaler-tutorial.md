---
title: 'Samouczek: Integracji Azure Active Directory z Zscaler | Dokumentacja firmy Microsoft'
description: "Dowiedz się, jak tooconfigure logowanie jednokrotne między usługą Azure Active Directory i Zscaler."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 68c453f7-aff1-4614-92d3-9b86f3ad99dc
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/08/2017
ms.author: jeedes
ms.openlocfilehash: e2894534f5d6711fd6af618cd699fa5837b5bf26
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-zscaler"></a><span data-ttu-id="c62a8-103">Samouczek: Integracji Azure Active Directory z Zscaler</span><span class="sxs-lookup"><span data-stu-id="c62a8-103">Tutorial: Azure Active Directory integration with Zscaler</span></span>

<span data-ttu-id="c62a8-104">Z tego samouczka, dowiesz się, jak toointegrate Zscaler w usłudze Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="c62a8-104">In this tutorial, you learn how toointegrate Zscaler with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="c62a8-105">Integracja z usługą Azure AD Zscaler zapewnia hello następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="c62a8-105">Integrating Zscaler with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="c62a8-106">Można kontrolować w usłudze Azure AD, kto ma dostęp do tooZscaler</span><span class="sxs-lookup"><span data-stu-id="c62a8-106">You can control in Azure AD who has access tooZscaler</span></span>
- <span data-ttu-id="c62a8-107">Można włączyć użytkownika użytkownicy tooautomatically get zalogowane tooZscaler (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="c62a8-107">You can enable your users tooautomatically get signed-on tooZscaler (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="c62a8-108">Możesz zarządzać kont w jednej centralnej lokalizacji - hello portalu Azure</span><span class="sxs-lookup"><span data-stu-id="c62a8-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="c62a8-109">Jeśli chcesz tooknow więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="c62a8-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c62a8-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="c62a8-110">Prerequisites</span></span>

<span data-ttu-id="c62a8-111">tooconfigure integracji z usługą Azure AD z Zscaler należy hello następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="c62a8-111">tooconfigure Azure AD integration with Zscaler, you need hello following items:</span></span>

- <span data-ttu-id="c62a8-112">Subskrypcję usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="c62a8-112">An Azure AD subscription</span></span>
- <span data-ttu-id="c62a8-113">Zscaler logowanie jednokrotne włączone subskrypcji</span><span class="sxs-lookup"><span data-stu-id="c62a8-113">A Zscaler single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="c62a8-114">tootest hello kroków w tym samouczku, zaleca się przy użyciu środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="c62a8-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="c62a8-115">tootest hello kroki opisane w tym samouczku, należy stosować te zalecenia:</span><span class="sxs-lookup"><span data-stu-id="c62a8-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="c62a8-116">Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="c62a8-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="c62a8-117">Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz pobrać miesięczna wersja próbna [tutaj](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="c62a8-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="c62a8-118">Opis scenariusza</span><span class="sxs-lookup"><span data-stu-id="c62a8-118">Scenario description</span></span>
<span data-ttu-id="c62a8-119">W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym.</span><span class="sxs-lookup"><span data-stu-id="c62a8-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="c62a8-120">Scenariusz Hello opisane w tym samouczku składa się z dwóch głównych elementów:</span><span class="sxs-lookup"><span data-stu-id="c62a8-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="c62a8-121">Dodawanie Zscaler z galerii hello</span><span class="sxs-lookup"><span data-stu-id="c62a8-121">Adding Zscaler from hello gallery</span></span>
2. <span data-ttu-id="c62a8-122">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="c62a8-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-zscaler-from-hello-gallery"></a><span data-ttu-id="c62a8-123">Dodawanie Zscaler z galerii hello</span><span class="sxs-lookup"><span data-stu-id="c62a8-123">Adding Zscaler from hello gallery</span></span>
<span data-ttu-id="c62a8-124">tooconfigure hello integracji Zscaler do usługi Azure AD, należy tooadd Zscaler z hello galerii tooyour listę zarządzanych aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="c62a8-124">tooconfigure hello integration of Zscaler into Azure AD, you need tooadd Zscaler from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="c62a8-125">**tooadd Zscaler z galerii hello, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="c62a8-125">**tooadd Zscaler from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="c62a8-126">W hello  **[portalu Azure](https://portal.azure.com)**na temat hello panelu nawigacji po lewej stronie, kliknij przycisk **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="c62a8-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Usługa Active Directory][1]

2. <span data-ttu-id="c62a8-128">Przejdź za**aplikacje dla przedsiębiorstw**.</span><span class="sxs-lookup"><span data-stu-id="c62a8-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="c62a8-129">Następnie przejdź zbyt**wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="c62a8-129">Then go too**All applications**.</span></span>

    ![Aplikacje][2]
    
3. <span data-ttu-id="c62a8-131">tooadd nową aplikację, kliknij przycisk **nowej aplikacji** przycisk u góry hello okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="c62a8-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplikacje][3]

4. <span data-ttu-id="c62a8-133">W polu wyszukiwania hello wpisz **Zscaler**.</span><span class="sxs-lookup"><span data-stu-id="c62a8-133">In hello search box, type **Zscaler**.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-zscaler-tutorial/tutorial_zscaler_search.png)

5. <span data-ttu-id="c62a8-135">W panelu wyników hello zaznacz **Zscaler**, a następnie kliknij przycisk **Dodaj** przycisk aplikacji hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="c62a8-135">In hello results panel, select **Zscaler**, and then click **Add** button tooadd hello application.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-zscaler-tutorial/tutorial_zscaler_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="c62a8-137">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="c62a8-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="c62a8-138">W tej sekcji skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z Zscaler w oparciu o nazwie "Britta Simona" użytkownika testowego.</span><span class="sxs-lookup"><span data-stu-id="c62a8-138">In this section, you configure and test Azure AD single sign-on with Zscaler based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="c62a8-139">Dla pojedynczego logowania jednokrotnego toowork usługi Azure AD musi tooknow użytkownika odpowiednikiem hello w Zscaler jest tooa użytkownika w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c62a8-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Zscaler is tooa user in Azure AD.</span></span> <span data-ttu-id="c62a8-140">Innymi słowy relację łącza między użytkownika usługi Azure AD i hello użytkownikowi w Zscaler musi toobe ustanowione.</span><span class="sxs-lookup"><span data-stu-id="c62a8-140">In other words, a link relationship between an Azure AD user and hello related user in Zscaler needs toobe established.</span></span>

<span data-ttu-id="c62a8-141">W Zscaler, należy przypisać wartość hello hello **nazwy użytkownika** w usłudze Azure AD jako wartość hello hello **Username** tooestablish hello łącze relacji.</span><span class="sxs-lookup"><span data-stu-id="c62a8-141">In Zscaler, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="c62a8-142">tooconfigure i testowych usługi Azure AD rejestracji jednokrotnej z Zscaler, należy po bloków konstrukcyjnych hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="c62a8-142">tooconfigure and test Azure AD single sign-on with Zscaler, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="c62a8-143">**[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configuring-azure-ad-single-sign-on)**  -tooenable Twojego toouse użytkowników tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="c62a8-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="c62a8-144">**[Konfigurowanie ustawień serwera proxy](#configuring-proxy-settings)**  — ustawienia serwera proxy hello tooconfigure w programie Internet Explorer</span><span class="sxs-lookup"><span data-stu-id="c62a8-144">**[Configuring proxy settings](#configuring-proxy-settings)** - tooconfigure hello proxy settings in Internet Explorer</span></span>
3. <span data-ttu-id="c62a8-145">**[Tworzenie użytkownika testowego usługi Azure AD](#creating-an-azure-ad-test-user)**  -tootest usługi Azure AD rejestracji jednokrotnej z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="c62a8-145">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
4. <span data-ttu-id="c62a8-146">**[Tworzenie użytkownika testowego Zscaler](#creating-a-zscaler-test-user)**  -toohave odpowiednikiem Simona Britta w Zscaler, który jest połączony toohello usługi Azure AD reprezentację użytkownika.</span><span class="sxs-lookup"><span data-stu-id="c62a8-146">**[Creating a Zscaler test user](#creating-a-zscaler-test-user)** - toohave a counterpart of Britta Simon in Zscaler that is linked toohello Azure AD representation of user.</span></span>
5. <span data-ttu-id="c62a8-147">**[Przypisanie użytkownika testowego hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Simona Britta toouse usługi Azure AD rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="c62a8-147">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
6. <span data-ttu-id="c62a8-148">**[Testowanie rejestracji jednokrotnej](#testing-single-sign-on)**  -tooverify czy hello konfiguracji działania.</span><span class="sxs-lookup"><span data-stu-id="c62a8-148">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="c62a8-149">Konfigurowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="c62a8-149">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="c62a8-150">W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w portalu Azure hello i skonfigurować logowanie jednokrotne w aplikacji Zscaler.</span><span class="sxs-lookup"><span data-stu-id="c62a8-150">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Zscaler application.</span></span>

<span data-ttu-id="c62a8-151">**tooconfigure usługi Azure AD rejestracji jednokrotnej z Zscaler, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="c62a8-151">**tooconfigure Azure AD single sign-on with Zscaler, perform hello following steps:**</span></span>

1. <span data-ttu-id="c62a8-152">W portalu Azure na powitania hello **Zscaler** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.</span><span class="sxs-lookup"><span data-stu-id="c62a8-152">In hello Azure portal, on hello **Zscaler** application integration page, click **Single sign-on**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej][4]

2. <span data-ttu-id="c62a8-154">Na powitania **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** tooenable rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="c62a8-154">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-zscaler-tutorial/tutorial_zscaler_samlbase.png)

3. <span data-ttu-id="c62a8-156">Na powitania **Zscaler domeny i adres URL** sekcji, wykonaj następujące kroki hello:</span><span class="sxs-lookup"><span data-stu-id="c62a8-156">On hello **Zscaler Domain and URLs** section, perform hello following steps:</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-zscaler-tutorial/tutorial_zscaler_url.png)

    <span data-ttu-id="c62a8-158">W hello **adres URL logowania** tekstowym, wpisz adres URL za pomocą hello następującego wzorca:`https://<companyname>.zsclaer.net`</span><span class="sxs-lookup"><span data-stu-id="c62a8-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<companyname>.zsclaer.net`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="c62a8-159">Ta wartość nie jest prawdziwe.</span><span class="sxs-lookup"><span data-stu-id="c62a8-159">This value is not real.</span></span> <span data-ttu-id="c62a8-160">Zaktualizuj tę wartość z hello rzeczywisty adres URL logowania.</span><span class="sxs-lookup"><span data-stu-id="c62a8-160">Update this value with hello actual Sign-On URL.</span></span> <span data-ttu-id="c62a8-161">Skontaktuj się z [zespołem pomocy technicznej klienta Zscaler](https://www.zscaler.com/company/contact) tooget tej wartości.</span><span class="sxs-lookup"><span data-stu-id="c62a8-161">Contact [Zscaler Client support team](https://www.zscaler.com/company/contact) tooget this value.</span></span> 

4. <span data-ttu-id="c62a8-162">Na powitania **certyfikat podpisywania SAML** kliknij **Certificate(Base64)** , a następnie zapisz plik certyfikatu hello na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="c62a8-162">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-zscaler-tutorial/tutorial_zscaler_certificate.png) 

5. <span data-ttu-id="c62a8-164">Kliknij przycisk **zapisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="c62a8-164">Click **Save** button.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-zscaler-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="c62a8-166">Na powitania **konfiguracji Zscaler** kliknij **skonfigurować Zscaler** tooopen **Konfigurowanie logowania jednokrotnego** okna.</span><span class="sxs-lookup"><span data-stu-id="c62a8-166">On hello **Zscaler Configuration** section, click **Configure Zscaler** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="c62a8-167">Kopiuj hello **SAML pojedynczy znak na adres URL usługi** z hello **sekcji krótkimi opisami.**</span><span class="sxs-lookup"><span data-stu-id="c62a8-167">Copy hello **SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-zscaler-tutorial/tutorial_zscaler_configure.png) 

7. <span data-ttu-id="c62a8-169">W oknie przeglądarki innej witryny sieci web Zaloguj się w witrynie firmy ZScaler tooyour jako administrator.</span><span class="sxs-lookup"><span data-stu-id="c62a8-169">In a different web browser window, log in tooyour ZScaler company site as an administrator.</span></span>

8. <span data-ttu-id="c62a8-170">W menu hello na górze hello, kliknij przycisk **administracji**.</span><span class="sxs-lookup"><span data-stu-id="c62a8-170">In hello menu on hello top, click **Administration**.</span></span>
   
    <span data-ttu-id="c62a8-171">![Administracja](./media/active-directory-saas-zscaler-tutorial/ic800206.png "administracji")</span><span class="sxs-lookup"><span data-stu-id="c62a8-171">![Administration](./media/active-directory-saas-zscaler-tutorial/ic800206.png "Administration")</span></span>

9. <span data-ttu-id="c62a8-172">W obszarze **administratorom zarządzanie & role**, kliknij przycisk **Zarządzanie użytkownikami & uwierzytelniania**.</span><span class="sxs-lookup"><span data-stu-id="c62a8-172">Under **Manage Administrators & Roles**, click **Manage Users & Authentication**.</span></span>   
            
    <span data-ttu-id="c62a8-173">![Zarządzaj użytkownikami & uwierzytelniania](./media/active-directory-saas-zscaler-tutorial/ic800207.png "zarządzania użytkownikami i uwierzytelniania")</span><span class="sxs-lookup"><span data-stu-id="c62a8-173">![Manage Users & Authentication](./media/active-directory-saas-zscaler-tutorial/ic800207.png "Manage Users & Authentication")</span></span>

10. <span data-ttu-id="c62a8-174">W hello **wybierz opcje uwierzytelniania dla Twojej organizacji** sekcji, wykonaj następujące kroki hello:</span><span class="sxs-lookup"><span data-stu-id="c62a8-174">In hello **Choose Authentication Options for your Organization** section, perform hello following steps:</span></span>   
                
    <span data-ttu-id="c62a8-175">![Uwierzytelnianie](./media/active-directory-saas-zscaler-tutorial/ic800208.png "uwierzytelniania")</span><span class="sxs-lookup"><span data-stu-id="c62a8-175">![Authentication](./media/active-directory-saas-zscaler-tutorial/ic800208.png "Authentication")</span></span>
   
    <span data-ttu-id="c62a8-176">a.</span><span class="sxs-lookup"><span data-stu-id="c62a8-176">a.</span></span> <span data-ttu-id="c62a8-177">Wybierz **uwierzytelnianie przy użyciu SAML logowania jednokrotnego**.</span><span class="sxs-lookup"><span data-stu-id="c62a8-177">Select **Authenticate using SAML Single Sign-On**.</span></span>

    <span data-ttu-id="c62a8-178">b.</span><span class="sxs-lookup"><span data-stu-id="c62a8-178">b.</span></span> <span data-ttu-id="c62a8-179">Kliknij przycisk **skonfigurować SAML pojedynczego logowania jednokrotnego parametry**.</span><span class="sxs-lookup"><span data-stu-id="c62a8-179">Click **Configure SAML Single Sign-On Parameters**.</span></span>

11. <span data-ttu-id="c62a8-180">Na powitania **skonfigurować SAML pojedynczych logowania jednokrotnego parametrów** strony okna dialogowego, wykonaj następujące kroki hello, a następnie kliknij **gotowe**</span><span class="sxs-lookup"><span data-stu-id="c62a8-180">On hello **Configure SAML Single Sign-On Parameters** dialog page, perform hello following steps, and then click **Done**</span></span>

    <span data-ttu-id="c62a8-181">![Logowanie jednokrotne](./media/active-directory-saas-zscaler-tutorial/ic800209.png "logowanie jednokrotne")</span><span class="sxs-lookup"><span data-stu-id="c62a8-181">![Single Sign-On](./media/active-directory-saas-zscaler-tutorial/ic800209.png "Single Sign-On")</span></span>
    
    <span data-ttu-id="c62a8-182">a.</span><span class="sxs-lookup"><span data-stu-id="c62a8-182">a.</span></span> <span data-ttu-id="c62a8-183">Wklej hello **SAML pojedynczy znak na adres URL usługi** wartość, która została skopiowana z hello portalu Azure do hello **adres URL hello SAML portalu toowhich użytkowników są wysyłane do uwierzytelniania** pola tekstowego.</span><span class="sxs-lookup"><span data-stu-id="c62a8-183">Paste hello **SAML Single Sign-On Service URL** value, which you have copied from hello Azure portal into hello **URL of hello SAML Portal toowhich users are sent for authentication** textbox.</span></span>
    
    <span data-ttu-id="c62a8-184">b.</span><span class="sxs-lookup"><span data-stu-id="c62a8-184">b.</span></span> <span data-ttu-id="c62a8-185">W hello **atrybutu zawierającego nazwę logowania** pole tekstowe, typ **NameID**.</span><span class="sxs-lookup"><span data-stu-id="c62a8-185">In hello **Attribute containing Login Name** textbox, type **NameID**.</span></span>
    
    <span data-ttu-id="c62a8-186">c.</span><span class="sxs-lookup"><span data-stu-id="c62a8-186">c.</span></span> <span data-ttu-id="c62a8-187">tooupload pobranego certyfikatu, kliknij przycisk **Zscaler pem**.</span><span class="sxs-lookup"><span data-stu-id="c62a8-187">tooupload your downloaded certificate, click **Zscaler pem**.</span></span>
    
    <span data-ttu-id="c62a8-188">d.</span><span class="sxs-lookup"><span data-stu-id="c62a8-188">d.</span></span> <span data-ttu-id="c62a8-189">Wybierz **Włącz SAML automatycznego inicjowania obsługi**.</span><span class="sxs-lookup"><span data-stu-id="c62a8-189">Select **Enable SAML Auto-Provisioning**.</span></span>

12. <span data-ttu-id="c62a8-190">Na powitania **skonfigurować uwierzytelnianie użytkownika** okna dialogowego wykonaj hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="c62a8-190">On hello **Configure User Authentication** dialog page, perform hello following steps:</span></span>

    <span data-ttu-id="c62a8-191">![Administracja](./media/active-directory-saas-zscaler-tutorial/ic800210.png "administracji")</span><span class="sxs-lookup"><span data-stu-id="c62a8-191">![Administration](./media/active-directory-saas-zscaler-tutorial/ic800210.png "Administration")</span></span>
    
    <span data-ttu-id="c62a8-192">a.</span><span class="sxs-lookup"><span data-stu-id="c62a8-192">a.</span></span> <span data-ttu-id="c62a8-193">Kliknij pozycję **Zapisz**.</span><span class="sxs-lookup"><span data-stu-id="c62a8-193">Click **Save**.</span></span>

    <span data-ttu-id="c62a8-194">b.</span><span class="sxs-lookup"><span data-stu-id="c62a8-194">b.</span></span> <span data-ttu-id="c62a8-195">Kliknij przycisk **Aktywuj teraz**.</span><span class="sxs-lookup"><span data-stu-id="c62a8-195">Click **Activate Now**.</span></span>

## <a name="configuring-proxy-settings"></a><span data-ttu-id="c62a8-196">Konfigurowanie ustawień serwera proxy</span><span class="sxs-lookup"><span data-stu-id="c62a8-196">Configuring proxy settings</span></span>
### <a name="tooconfigure-hello-proxy-settings-in-internet-explorer"></a><span data-ttu-id="c62a8-197">ustawienia serwera proxy hello tooconfigure w programie Internet Explorer</span><span class="sxs-lookup"><span data-stu-id="c62a8-197">tooconfigure hello proxy settings in Internet Explorer</span></span>

1. <span data-ttu-id="c62a8-198">Uruchom **programu Internet Explorer**.</span><span class="sxs-lookup"><span data-stu-id="c62a8-198">Start **Internet Explorer**.</span></span>

2. <span data-ttu-id="c62a8-199">Wybierz **Opcje internetowe** z hello **narzędzia** menu Otwórz hello **Opcje internetowe** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="c62a8-199">Select **Internet options** from hello **Tools** menu for open hello **Internet Options** dialog.</span></span>   
    
     <span data-ttu-id="c62a8-200">![Opcje internetowe](./media/active-directory-saas-zscaler-tutorial/ic769492.png "Opcje internetowe")</span><span class="sxs-lookup"><span data-stu-id="c62a8-200">![Internet Options](./media/active-directory-saas-zscaler-tutorial/ic769492.png "Internet Options")</span></span>

3. <span data-ttu-id="c62a8-201">Kliknij przycisk hello **połączeń** kartę.</span><span class="sxs-lookup"><span data-stu-id="c62a8-201">Click hello **Connections** tab.</span></span>   
  
     <span data-ttu-id="c62a8-202">![Połączenia](./media/active-directory-saas-zscaler-tutorial/ic769493.png "połączeń")</span><span class="sxs-lookup"><span data-stu-id="c62a8-202">![Connections](./media/active-directory-saas-zscaler-tutorial/ic769493.png "Connections")</span></span>

4. <span data-ttu-id="c62a8-203">Kliknij przycisk **ustawienia sieci LAN** tooopen hello **ustawienia sieci LAN** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="c62a8-203">Click **LAN settings** tooopen hello **LAN Settings** dialog.</span></span>

5. <span data-ttu-id="c62a8-204">W sekcji serwer Proxy hello wykonaj hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="c62a8-204">In hello Proxy server section, perform hello following steps:</span></span>   
   
    <span data-ttu-id="c62a8-205">![Serwer proxy](./media/active-directory-saas-zscaler-tutorial/ic769494.png "serwera Proxy")</span><span class="sxs-lookup"><span data-stu-id="c62a8-205">![Proxy server](./media/active-directory-saas-zscaler-tutorial/ic769494.png "Proxy server")</span></span>

    <span data-ttu-id="c62a8-206">a.</span><span class="sxs-lookup"><span data-stu-id="c62a8-206">a.</span></span> <span data-ttu-id="c62a8-207">Wybierz **Użyj serwera proxy dla sieci LAN**.</span><span class="sxs-lookup"><span data-stu-id="c62a8-207">Select **Use a proxy server for your LAN**.</span></span>

    <span data-ttu-id="c62a8-208">b.</span><span class="sxs-lookup"><span data-stu-id="c62a8-208">b.</span></span> <span data-ttu-id="c62a8-209">W polu tekstowym adres hello, wpisz **gateway.zscaler.net**.</span><span class="sxs-lookup"><span data-stu-id="c62a8-209">In hello Address textbox, type **gateway.zscaler.net**.</span></span>

    <span data-ttu-id="c62a8-210">c.</span><span class="sxs-lookup"><span data-stu-id="c62a8-210">c.</span></span> <span data-ttu-id="c62a8-211">W polu tekstowym portu hello, wpisz **80**.</span><span class="sxs-lookup"><span data-stu-id="c62a8-211">In hello Port textbox, type **80**.</span></span>

    <span data-ttu-id="c62a8-212">d.</span><span class="sxs-lookup"><span data-stu-id="c62a8-212">d.</span></span> <span data-ttu-id="c62a8-213">Wybierz **używaj serwera proxy dla adresów lokalnych**.</span><span class="sxs-lookup"><span data-stu-id="c62a8-213">Select **Bypass proxy server for local addresses**.</span></span>

    <span data-ttu-id="c62a8-214">e.</span><span class="sxs-lookup"><span data-stu-id="c62a8-214">e.</span></span> <span data-ttu-id="c62a8-215">Kliknij przycisk **OK** tooclose hello **ustawienia sieci lokalnej (LAN)** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="c62a8-215">Click **OK** tooclose hello **Local Area Network (LAN) Settings** dialog.</span></span>

6. <span data-ttu-id="c62a8-216">Kliknij przycisk **OK** tooclose hello **Opcje internetowe** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="c62a8-216">Click **OK** tooclose hello **Internet Options** dialog.</span></span>

> [!TIP]
> <span data-ttu-id="c62a8-217">Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz hello [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji hello!</span><span class="sxs-lookup"><span data-stu-id="c62a8-217">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="c62a8-218">Po dodaniu tej aplikacji z hello **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij hello **rejestracji jednokrotnej** hello kartę i dostępu do osadzonych dokumentacji za pośrednictwem hello  **Konfiguracja** sekcji u dołu hello.</span><span class="sxs-lookup"><span data-stu-id="c62a8-218">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="c62a8-219">Więcej o hello osadzonych dokumentacji funkcji w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="c62a8-219">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="c62a8-220">Tworzenie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="c62a8-220">Creating an Azure AD test user</span></span>
<span data-ttu-id="c62a8-221">Celem Hello w tej sekcji jest toocreate użytkownika testowego, w portalu Azure o nazwie Simona Britta hello.</span><span class="sxs-lookup"><span data-stu-id="c62a8-221">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Tworzenie użytkowników usługi Azure AD][100]

<span data-ttu-id="c62a8-223">**toocreate użytkownika testowego w usłudze Azure AD, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="c62a8-223">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="c62a8-224">W hello **portalu Azure**na temat hello w lewym okienku nawigacji, kliknij przycisk **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="c62a8-224">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-zscaler-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="c62a8-226">toodisplay hello listę użytkowników, przejdź zbyt**użytkowników i grup** i kliknij przycisk **wszyscy użytkownicy**.</span><span class="sxs-lookup"><span data-stu-id="c62a8-226">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-zscaler-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="c62a8-228">Witaj tooopen **użytkownika** okna dialogowego, kliknij przycisk **Dodaj** u góry hello hello okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="c62a8-228">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-zscaler-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="c62a8-230">Na powitania **użytkownika** okna dialogowego wykonaj hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="c62a8-230">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-zscaler-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="c62a8-232">a.</span><span class="sxs-lookup"><span data-stu-id="c62a8-232">a.</span></span> <span data-ttu-id="c62a8-233">W hello **nazwa** pole tekstowe, typ **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="c62a8-233">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="c62a8-234">b.</span><span class="sxs-lookup"><span data-stu-id="c62a8-234">b.</span></span> <span data-ttu-id="c62a8-235">W hello **nazwy użytkownika** pole tekstowe, hello typu **adres e-mail** z BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="c62a8-235">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="c62a8-236">c.</span><span class="sxs-lookup"><span data-stu-id="c62a8-236">c.</span></span> <span data-ttu-id="c62a8-237">Wybierz **Pokaż hasło** i zanotuj wartość hello hello **hasło**.</span><span class="sxs-lookup"><span data-stu-id="c62a8-237">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="c62a8-238">d.</span><span class="sxs-lookup"><span data-stu-id="c62a8-238">d.</span></span> <span data-ttu-id="c62a8-239">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="c62a8-239">Click **Create**.</span></span>
 
### <a name="creating-a-zscaler-test-user"></a><span data-ttu-id="c62a8-240">Tworzenie użytkownika testowego Zscaler</span><span class="sxs-lookup"><span data-stu-id="c62a8-240">Creating a Zscaler test user</span></span>

<span data-ttu-id="c62a8-241">tooenable usługi Azure AD użytkownicy toolog tooZScaler, muszą być tooZScaler elastycznie.</span><span class="sxs-lookup"><span data-stu-id="c62a8-241">tooenable Azure AD users toolog in tooZScaler, they must be provisioned tooZScaler.</span></span>  
<span data-ttu-id="c62a8-242">W przypadku hello ZScaler Inicjowanie obsługi to zadanie ręczne.</span><span class="sxs-lookup"><span data-stu-id="c62a8-242">In hello case of ZScaler, provisioning is a manual task.</span></span>

### <a name="tooconfigure-user-provisioning-perform-hello-following-steps"></a><span data-ttu-id="c62a8-243">tooconfigure aprowizacji użytkowników, wykonaj następujące kroki hello:</span><span class="sxs-lookup"><span data-stu-id="c62a8-243">tooconfigure user provisioning, perform hello following steps:</span></span>

1. <span data-ttu-id="c62a8-244">Zaloguj się za tooyour **Zscaler** dzierżawy.</span><span class="sxs-lookup"><span data-stu-id="c62a8-244">Log in tooyour **Zscaler** tenant.</span></span>

2. <span data-ttu-id="c62a8-245">Kliknij przycisk **administracji**.</span><span class="sxs-lookup"><span data-stu-id="c62a8-245">Click **Administration**.</span></span>   
   
    <span data-ttu-id="c62a8-246">![Administracja](./media/active-directory-saas-zscaler-tutorial/ic781035.png "administracji")</span><span class="sxs-lookup"><span data-stu-id="c62a8-246">![Administration](./media/active-directory-saas-zscaler-tutorial/ic781035.png "Administration")</span></span>

3. <span data-ttu-id="c62a8-247">Kliknij przycisk **Zarządzanie użytkownikami**.</span><span class="sxs-lookup"><span data-stu-id="c62a8-247">Click **User Management**.</span></span>   
        
     <span data-ttu-id="c62a8-248">![Dodaj](./media/active-directory-saas-zscaler-tutorial/ic781036.png "Dodaj")</span><span class="sxs-lookup"><span data-stu-id="c62a8-248">![Add](./media/active-directory-saas-zscaler-tutorial/ic781036.png "Add")</span></span>

4. <span data-ttu-id="c62a8-249">W hello **użytkowników** , kliknij pozycję **Dodaj**.</span><span class="sxs-lookup"><span data-stu-id="c62a8-249">In hello **Users** tab, click **Add**.</span></span>
      
    <span data-ttu-id="c62a8-250">![Dodaj](./media/active-directory-saas-zscaler-tutorial/ic781037.png "Dodaj")</span><span class="sxs-lookup"><span data-stu-id="c62a8-250">![Add](./media/active-directory-saas-zscaler-tutorial/ic781037.png "Add")</span></span>

5. <span data-ttu-id="c62a8-251">W sekcji Dodaj użytkownika hello wykonaj hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="c62a8-251">In hello Add User section, perform hello following steps:</span></span>
        
    <span data-ttu-id="c62a8-252">![Dodaj użytkownika](./media/active-directory-saas-zscaler-tutorial/ic781038.png "Dodaj użytkownika")</span><span class="sxs-lookup"><span data-stu-id="c62a8-252">![Add User](./media/active-directory-saas-zscaler-tutorial/ic781038.png "Add User")</span></span>
   
    <span data-ttu-id="c62a8-253">a.</span><span class="sxs-lookup"><span data-stu-id="c62a8-253">a.</span></span> <span data-ttu-id="c62a8-254">Hello typu **UserID**, **Nazwa wyświetlana użytkownika**, **hasło**, **Potwierdź hasło**, a następnie wybierz **grup**i hello **działu** ma tooprovision poprawnego konta usługi AAD.</span><span class="sxs-lookup"><span data-stu-id="c62a8-254">Type hello **UserID**, **User Display Name**, **Password**, **Confirm Password**, and then select **Groups** and hello **Department** of a valid AAD account you want tooprovision.</span></span>

    <span data-ttu-id="c62a8-255">b.</span><span class="sxs-lookup"><span data-stu-id="c62a8-255">b.</span></span> <span data-ttu-id="c62a8-256">Kliknij pozycję **Zapisz**.</span><span class="sxs-lookup"><span data-stu-id="c62a8-256">Click **Save**.</span></span>

> [!NOTE]
> <span data-ttu-id="c62a8-257">Możesz użyć innych ZScaler użytkownika konta tworzenia narzędzi lub interfejsów API dostarczonych przez ZScaler tooprovision kont użytkowników usługi AAD.</span><span class="sxs-lookup"><span data-stu-id="c62a8-257">You can use any other ZScaler user account creation tools or APIs provided by ZScaler tooprovision AAD user accounts.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="c62a8-258">Przypisanie użytkownika testowego hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="c62a8-258">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="c62a8-259">W tej sekcji możesz włączyć toouse Simona Britta Azure logowania jednokrotnego za udzielanie dostępu tooZscaler.</span><span class="sxs-lookup"><span data-stu-id="c62a8-259">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooZscaler.</span></span>

![Przypisz użytkownika][200] 

<span data-ttu-id="c62a8-261">**tooassign tooZscaler Simona Britta wykonaj hello następujące kroki:**</span><span class="sxs-lookup"><span data-stu-id="c62a8-261">**tooassign Britta Simon tooZscaler, perform hello following steps:**</span></span>

1. <span data-ttu-id="c62a8-262">W portalu Azure hello, otwórz widok aplikacji hello, a następnie przejdź do widoku katalogu toohello i przejść za**aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="c62a8-262">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Przypisz użytkownika][201] 

2. <span data-ttu-id="c62a8-264">Z listy aplikacji hello wybierz **Zscaler**.</span><span class="sxs-lookup"><span data-stu-id="c62a8-264">In hello applications list, select **Zscaler**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-zscaler-tutorial/tutorial_zscaler_app.png) 

3. <span data-ttu-id="c62a8-266">W menu powitania po lewej stronie powitania kliknij **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="c62a8-266">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Przypisz użytkownika][202] 

4. <span data-ttu-id="c62a8-268">Kliknij przycisk **Dodaj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="c62a8-268">Click **Add** button.</span></span> <span data-ttu-id="c62a8-269">Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="c62a8-269">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Przypisz użytkownika][203]

5. <span data-ttu-id="c62a8-271">Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** hello listy użytkowników.</span><span class="sxs-lookup"><span data-stu-id="c62a8-271">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="c62a8-272">Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="c62a8-272">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="c62a8-273">Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="c62a8-273">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="c62a8-274">Testowanie rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="c62a8-274">Testing single sign-on</span></span>

<span data-ttu-id="c62a8-275">W tej sekcji można przetestować konfiguracji usługi Azure AD pojedynczego logowania jednokrotnego przy użyciu hello panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="c62a8-275">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="c62a8-276">Po kliknięciu kafelka Zscaler hello w hello Panel dostępu, należy pobrać automatycznie zalogowane tooyour Zscaler aplikacji.</span><span class="sxs-lookup"><span data-stu-id="c62a8-276">When you click hello Zscaler tile in hello Access Panel, you should get automatically signed-on tooyour Zscaler application.</span></span>
<span data-ttu-id="c62a8-277">Aby uzyskać więcej informacji na temat hello Panel dostępu, zobacz [toohello wprowadzenie panelu dostępu](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="c62a8-277">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="c62a8-278">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="c62a8-278">Additional resources</span></span>

* [<span data-ttu-id="c62a8-279">Lista samouczków dotyczących tooIntegrate aplikacji SaaS w usłudze Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="c62a8-279">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="c62a8-280">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="c62a8-280">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-zscaler-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-zscaler-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-zscaler-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-zscaler-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-zscaler-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-zscaler-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-zscaler-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-zscaler-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-zscaler-tutorial/tutorial_general_203.png

