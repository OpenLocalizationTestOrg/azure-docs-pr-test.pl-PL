---
title: 'Samouczek: Integracji Azure Active Directory z BlueJeans | Dokumentacja firmy Microsoft'
description: "Dowiedz się, jak tooconfigure logowanie jednokrotne między usługą Azure Active Directory i BlueJeans."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: dfc634fd-1b55-4ba8-94a8-b8288429b6a9
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/31/2017
ms.author: jeedes
ms.openlocfilehash: 67613303a9f854afbf4619418cc1607d329caf94
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-bluejeans"></a><span data-ttu-id="790ea-103">Samouczek: Integracji Azure Active Directory z BlueJeans</span><span class="sxs-lookup"><span data-stu-id="790ea-103">Tutorial: Azure Active Directory integration with BlueJeans</span></span>

<span data-ttu-id="790ea-104">Z tego samouczka, dowiesz się, jak toointegrate BlueJeans w usłudze Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="790ea-104">In this tutorial, you learn how toointegrate BlueJeans with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="790ea-105">Integracja z usługą Azure AD BlueJeans zapewnia hello następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="790ea-105">Integrating BlueJeans with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="790ea-106">Można kontrolować w usłudze Azure AD, kto ma dostęp do tooBlueJeans</span><span class="sxs-lookup"><span data-stu-id="790ea-106">You can control in Azure AD who has access tooBlueJeans</span></span>
- <span data-ttu-id="790ea-107">Można włączyć użytkownika użytkownicy tooautomatically get zalogowane tooBlueJeans (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="790ea-107">You can enable your users tooautomatically get signed-on tooBlueJeans (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="790ea-108">Możesz zarządzać kont w jednej centralnej lokalizacji - hello portalu Azure</span><span class="sxs-lookup"><span data-stu-id="790ea-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="790ea-109">Jeśli chcesz tooknow więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="790ea-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="790ea-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="790ea-110">Prerequisites</span></span>

<span data-ttu-id="790ea-111">tooconfigure integracji z usługą Azure AD z BlueJeans należy hello następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="790ea-111">tooconfigure Azure AD integration with BlueJeans, you need hello following items:</span></span>

- <span data-ttu-id="790ea-112">Subskrypcję usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="790ea-112">An Azure AD subscription</span></span>
- <span data-ttu-id="790ea-113">BlueJeans jednokrotnego włączone subskrypcji</span><span class="sxs-lookup"><span data-stu-id="790ea-113">A BlueJeans single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="790ea-114">tootest hello kroków w tym samouczku, zaleca się przy użyciu środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="790ea-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="790ea-115">tootest hello kroki opisane w tym samouczku, należy stosować te zalecenia:</span><span class="sxs-lookup"><span data-stu-id="790ea-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="790ea-116">Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="790ea-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="790ea-117">Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz pobrać miesięczna wersja próbna [tutaj](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="790ea-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="790ea-118">Opis scenariusza</span><span class="sxs-lookup"><span data-stu-id="790ea-118">Scenario description</span></span>
<span data-ttu-id="790ea-119">W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym.</span><span class="sxs-lookup"><span data-stu-id="790ea-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="790ea-120">Scenariusz Hello opisane w tym samouczku składa się z dwóch głównych elementów:</span><span class="sxs-lookup"><span data-stu-id="790ea-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="790ea-121">Dodawanie BlueJeans z galerii hello</span><span class="sxs-lookup"><span data-stu-id="790ea-121">Adding BlueJeans from hello gallery</span></span>
2. <span data-ttu-id="790ea-122">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="790ea-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-bluejeans-from-hello-gallery"></a><span data-ttu-id="790ea-123">Dodawanie BlueJeans z galerii hello</span><span class="sxs-lookup"><span data-stu-id="790ea-123">Adding BlueJeans from hello gallery</span></span>
<span data-ttu-id="790ea-124">tooconfigure hello integracji BlueJeans do usługi Azure AD, należy tooadd BlueJeans z hello galerii tooyour listę zarządzanych aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="790ea-124">tooconfigure hello integration of BlueJeans into Azure AD, you need tooadd BlueJeans from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="790ea-125">**tooadd BlueJeans z galerii hello, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="790ea-125">**tooadd BlueJeans from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="790ea-126">W hello  **[portalu Azure](https://portal.azure.com)**na temat hello panelu nawigacji po lewej stronie, kliknij przycisk **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="790ea-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Usługa Active Directory][1]

2. <span data-ttu-id="790ea-128">Przejdź za**aplikacje dla przedsiębiorstw**.</span><span class="sxs-lookup"><span data-stu-id="790ea-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="790ea-129">Następnie przejdź zbyt**wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="790ea-129">Then go too**All applications**.</span></span>

    ![Aplikacje][2]
    
3. <span data-ttu-id="790ea-131">tooadd nową aplikację, kliknij przycisk **nowej aplikacji** przycisk u góry hello okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="790ea-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplikacje][3]

4. <span data-ttu-id="790ea-133">W polu wyszukiwania hello wpisz **BlueJeans**.</span><span class="sxs-lookup"><span data-stu-id="790ea-133">In hello search box, type **BlueJeans**.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-bluejeans-tutorial/tutorial_bluejeans_search.png)

5. <span data-ttu-id="790ea-135">W panelu wyników hello zaznacz **BlueJeans**, a następnie kliknij przycisk **Dodaj** przycisk aplikacji hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="790ea-135">In hello results panel, select **BlueJeans**, and then click **Add** button tooadd hello application.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-bluejeans-tutorial/tutorial_bluejeans_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="790ea-137">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="790ea-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="790ea-138">W tej sekcji możesz skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z BlueJeans na podstawie użytkownika testowego, nazywany "Britta Simona".</span><span class="sxs-lookup"><span data-stu-id="790ea-138">In this section, you configure and test Azure AD single sign-on with BlueJeans based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="790ea-139">Dla pojedynczego logowania jednokrotnego toowork usługi Azure AD musi tooknow użytkownika odpowiednikiem hello w BlueJeans jest tooa użytkownika w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="790ea-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in BlueJeans is tooa user in Azure AD.</span></span> <span data-ttu-id="790ea-140">Innymi słowy relację łącza między użytkownika usługi Azure AD i hello użytkownikowi w BlueJeans musi toobe ustanowione.</span><span class="sxs-lookup"><span data-stu-id="790ea-140">In other words, a link relationship between an Azure AD user and hello related user in BlueJeans needs toobe established.</span></span>

<span data-ttu-id="790ea-141">W BlueJeans, należy przypisać wartość hello hello **nazwy użytkownika** w usłudze Azure AD jako wartość hello hello **Username** tooestablish hello łącze relacji.</span><span class="sxs-lookup"><span data-stu-id="790ea-141">In BlueJeans, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="790ea-142">tooconfigure i testowych usługi Azure AD rejestracji jednokrotnej z BlueJeans, należy po bloków konstrukcyjnych hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="790ea-142">tooconfigure and test Azure AD single sign-on with BlueJeans, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="790ea-143">**[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configuring-azure-ad-single-sign-on)**  -tooenable Twojego toouse użytkowników tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="790ea-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="790ea-144">**[Tworzenie użytkownika testowego usługi Azure AD](#creating-an-azure-ad-test-user)**  -tootest usługi Azure AD rejestracji jednokrotnej z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="790ea-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="790ea-145">**[Tworzenie użytkownika testowego BlueJeans](#creating-a-bluejeans-test-user)**  -toohave odpowiednikiem Britta Simona w BlueJeans toohello połączonej usługi Azure AD reprezentacja użytkownika.</span><span class="sxs-lookup"><span data-stu-id="790ea-145">**[Creating a BlueJeans test user](#creating-a-bluejeans-test-user)** - toohave a counterpart of Britta Simon in BlueJeans that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="790ea-146">**[Przypisanie użytkownika testowego hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Simona Britta toouse usługi Azure AD rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="790ea-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="790ea-147">**[Testowanie rejestracji jednokrotnej](#testing-single-sign-on)**  -tooverify czy hello konfiguracji działania.</span><span class="sxs-lookup"><span data-stu-id="790ea-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="790ea-148">Konfigurowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="790ea-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="790ea-149">W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w portalu Azure hello i skonfigurować logowanie jednokrotne w aplikacji BlueJeans.</span><span class="sxs-lookup"><span data-stu-id="790ea-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your BlueJeans application.</span></span>

<span data-ttu-id="790ea-150">**tooconfigure usługi Azure AD rejestracji jednokrotnej z BlueJeans, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="790ea-150">**tooconfigure Azure AD single sign-on with BlueJeans, perform hello following steps:**</span></span>

1. <span data-ttu-id="790ea-151">W portalu Azure na powitania hello **BlueJeans** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.</span><span class="sxs-lookup"><span data-stu-id="790ea-151">In hello Azure portal, on hello **BlueJeans** application integration page, click **Single sign-on**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej][4]

2. <span data-ttu-id="790ea-153">Na powitania **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** tooenable rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="790ea-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-bluejeans-tutorial/tutorial_bluejeans_samlbase.png)

3. <span data-ttu-id="790ea-155">Na powitania **BlueJeans domeny i adres URL** sekcji, wykonaj następujące kroki hello:</span><span class="sxs-lookup"><span data-stu-id="790ea-155">On hello **BlueJeans Domain and URLs** section, perform hello following steps:</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-bluejeans-tutorial/tutorial_bluejeans_url.png)

    <span data-ttu-id="790ea-157">a.</span><span class="sxs-lookup"><span data-stu-id="790ea-157">a.</span></span> <span data-ttu-id="790ea-158">W hello **adres URL logowania** tekstowym, wpisz adres URL za pomocą hello następującego wzorca:`https://<companyname>.BlueJeans.com`</span><span class="sxs-lookup"><span data-stu-id="790ea-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<companyname>.BlueJeans.com`</span></span>

    <span data-ttu-id="790ea-159">b.</span><span class="sxs-lookup"><span data-stu-id="790ea-159">b.</span></span> <span data-ttu-id="790ea-160">W hello **identyfikator** tekstowym, wpisz adres URL za pomocą hello następującego wzorca:`https://<companyname>.BlueJeans.com`</span><span class="sxs-lookup"><span data-stu-id="790ea-160">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<companyname>.BlueJeans.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="790ea-161">Wartości te nie są prawdziwe.</span><span class="sxs-lookup"><span data-stu-id="790ea-161">These values are not real.</span></span> <span data-ttu-id="790ea-162">Zaktualizować te wartości z hello rzeczywisty adres URL logowania i identyfikator.</span><span class="sxs-lookup"><span data-stu-id="790ea-162">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="790ea-163">Skontaktuj się z [zespołem pomocy technicznej klienta BlueJeans](https://support.bluejeans.com/contact) tooget tych wartości.</span><span class="sxs-lookup"><span data-stu-id="790ea-163">Contact [BlueJeans Client support team](https://support.bluejeans.com/contact) tooget these values.</span></span> 
 
4. <span data-ttu-id="790ea-164">Na powitania **certyfikat podpisywania SAML** kliknij **Certificate(Base64)** , a następnie zapisz plik certyfikatu hello na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="790ea-164">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-bluejeans-tutorial/tutorial_bluejeans_certificate.png) 

5. <span data-ttu-id="790ea-166">Kliknij przycisk **zapisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="790ea-166">Click **Save** button.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-bluejeans-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="790ea-168">Na powitania **konfiguracji BlueJeans** kliknij **skonfigurować BlueJeans** tooopen **Konfigurowanie logowania jednokrotnego** okna.</span><span class="sxs-lookup"><span data-stu-id="790ea-168">On hello **BlueJeans Configuration** section, click **Configure BlueJeans** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="790ea-169">Kopiuj hello **Sign-Out adres URL, Zmień adres URL hasła i SAML pojedynczy znak na adres URL usługi** z hello **sekcji krótkimi opisami.**</span><span class="sxs-lookup"><span data-stu-id="790ea-169">Copy hello **Sign-Out URL, Change Password URL and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-bluejeans-tutorial/tutorial_bluejeans_configure.png) 

7. <span data-ttu-id="790ea-171">W oknie przeglądarki innej witryny sieci web, zaloguj się za tooyour **BlueJeans** witryny firmy jako administrator.</span><span class="sxs-lookup"><span data-stu-id="790ea-171">In a different web browser window, log in tooyour **BlueJeans** company site as an administrator.</span></span>

8. <span data-ttu-id="790ea-172">Przejdź za**ADMIN \> ustawienia grupy \> zabezpieczeń**.</span><span class="sxs-lookup"><span data-stu-id="790ea-172">Go too**ADMIN \> Group Settings \> Security**.</span></span>
   
   <span data-ttu-id="790ea-173">![Administrator](./media/active-directory-saas-bluejeans-tutorial/IC785868.png "administratora")</span><span class="sxs-lookup"><span data-stu-id="790ea-173">![Admin](./media/active-directory-saas-bluejeans-tutorial/IC785868.png "Admin")</span></span>

9. <span data-ttu-id="790ea-174">W hello **zabezpieczeń** sekcji, wykonaj następujące kroki hello:</span><span class="sxs-lookup"><span data-stu-id="790ea-174">In hello **Security** section, perform hello following steps:</span></span>
   
   <span data-ttu-id="790ea-175">![SAML logowania jednokrotnego](./media/active-directory-saas-bluejeans-tutorial/IC785869.png "SAML logowania jednokrotnego")</span><span class="sxs-lookup"><span data-stu-id="790ea-175">![SAML Single Sign On](./media/active-directory-saas-bluejeans-tutorial/IC785869.png "SAML Single Sign On")</span></span>   
   
   <span data-ttu-id="790ea-176">a.</span><span class="sxs-lookup"><span data-stu-id="790ea-176">a.</span></span> <span data-ttu-id="790ea-177">Wybierz **SAML logowania jednokrotnego**.</span><span class="sxs-lookup"><span data-stu-id="790ea-177">Select **SAML Single Sign On**.</span></span>
  
   <span data-ttu-id="790ea-178">b.</span><span class="sxs-lookup"><span data-stu-id="790ea-178">b.</span></span> <span data-ttu-id="790ea-179">Wybierz **Włącz automatyczne udostępnianie**.</span><span class="sxs-lookup"><span data-stu-id="790ea-179">Select **Enable automatic provisioning**.</span></span>

10. <span data-ttu-id="790ea-180">Przejść z hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="790ea-180">Move on with hello following steps:</span></span>

    <span data-ttu-id="790ea-181">![Ścieżka certyfikatu](./media/active-directory-saas-bluejeans-tutorial/IC785870.png "ścieżka certyfikatu")</span><span class="sxs-lookup"><span data-stu-id="790ea-181">![Certificate Path](./media/active-directory-saas-bluejeans-tutorial/IC785870.png "Certificate Path")</span></span>
    
    <span data-ttu-id="790ea-182">a.</span><span class="sxs-lookup"><span data-stu-id="790ea-182">a.</span></span> <span data-ttu-id="790ea-183">Kliknij przycisk **wybierz plik**, a następnie przekaż certyfikat hello pobrane.</span><span class="sxs-lookup"><span data-stu-id="790ea-183">Click **Choose File**, and then upload hello downloaded certificate.</span></span>
   
    <span data-ttu-id="790ea-184">b.</span><span class="sxs-lookup"><span data-stu-id="790ea-184">b.</span></span> <span data-ttu-id="790ea-185">Wklej **SAML pojedynczy znak na adres URL usługi** do hello **adres URL logowania** pola tekstowego.</span><span class="sxs-lookup"><span data-stu-id="790ea-185">Paste **SAML Single Sign-On Service URL** into hello **Login URL** textbox.</span></span>
   
    <span data-ttu-id="790ea-186">c.</span><span class="sxs-lookup"><span data-stu-id="790ea-186">c.</span></span> <span data-ttu-id="790ea-187">Wklej **Zmień adres URL hasła** do hello **hasła, Zmień adres URL** pola tekstowego.</span><span class="sxs-lookup"><span data-stu-id="790ea-187">Paste **Change Password URL** into hello **Password Change URL** textbox.</span></span>
   
    <span data-ttu-id="790ea-188">d.</span><span class="sxs-lookup"><span data-stu-id="790ea-188">d.</span></span> <span data-ttu-id="790ea-189">Wklej **Sign-Out URL** do hello **adresu URL wylogowania** pola tekstowego.</span><span class="sxs-lookup"><span data-stu-id="790ea-189">Paste **Sign-Out URL** into hello **Logout URL** textbox.</span></span>

11. <span data-ttu-id="790ea-190">Przejść z hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="790ea-190">Move on with hello following steps:</span></span>
    
    <span data-ttu-id="790ea-191">![Zapisz zmiany](./media/active-directory-saas-bluejeans-tutorial/IC785874.png "zapisać zmiany")</span><span class="sxs-lookup"><span data-stu-id="790ea-191">![Save Changes](./media/active-directory-saas-bluejeans-tutorial/IC785874.png "Save Changes")</span></span>
    
    <span data-ttu-id="790ea-192">a.</span><span class="sxs-lookup"><span data-stu-id="790ea-192">a.</span></span> <span data-ttu-id="790ea-193">W hello **identyfikator użytkownika** pole tekstowe, typ `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name`.</span><span class="sxs-lookup"><span data-stu-id="790ea-193">In hello **User id** textbox, type `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name`.</span></span>
   
    <span data-ttu-id="790ea-194">b.</span><span class="sxs-lookup"><span data-stu-id="790ea-194">b.</span></span> <span data-ttu-id="790ea-195">W hello **E-mail** pole tekstowe, typ `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name`.</span><span class="sxs-lookup"><span data-stu-id="790ea-195">In hello **Email** textbox, type `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name`.</span></span>
   
    <span data-ttu-id="790ea-196">c.</span><span class="sxs-lookup"><span data-stu-id="790ea-196">c.</span></span> <span data-ttu-id="790ea-197">Kliknij przycisk **zapisać zmiany**.</span><span class="sxs-lookup"><span data-stu-id="790ea-197">Click **Save Changes**.</span></span>

> [!TIP]
> <span data-ttu-id="790ea-198">Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz hello [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji hello!</span><span class="sxs-lookup"><span data-stu-id="790ea-198">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="790ea-199">Po dodaniu tej aplikacji z hello **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij hello **rejestracji jednokrotnej** hello kartę i dostępu do osadzonych dokumentacji za pośrednictwem hello  **Konfiguracja** sekcji u dołu hello.</span><span class="sxs-lookup"><span data-stu-id="790ea-199">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="790ea-200">Więcej o hello osadzonych dokumentacji funkcji w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="790ea-200">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="790ea-201">Tworzenie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="790ea-201">Creating an Azure AD test user</span></span>
<span data-ttu-id="790ea-202">Celem Hello w tej sekcji jest toocreate użytkownika testowego, w portalu Azure o nazwie Simona Britta hello.</span><span class="sxs-lookup"><span data-stu-id="790ea-202">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Tworzenie użytkowników usługi Azure AD][100]

<span data-ttu-id="790ea-204">**toocreate użytkownika testowego w usłudze Azure AD, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="790ea-204">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="790ea-205">W hello **portalu Azure**na temat hello w lewym okienku nawigacji, kliknij przycisk **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="790ea-205">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-bluejeans-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="790ea-207">toodisplay hello listę użytkowników, przejdź zbyt**użytkowników i grup** i kliknij przycisk **wszyscy użytkownicy**.</span><span class="sxs-lookup"><span data-stu-id="790ea-207">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-bluejeans-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="790ea-209">Witaj tooopen **użytkownika** okna dialogowego, kliknij przycisk **Dodaj** u góry hello hello okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="790ea-209">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-bluejeans-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="790ea-211">Na powitania **użytkownika** okna dialogowego wykonaj hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="790ea-211">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-bluejeans-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="790ea-213">a.</span><span class="sxs-lookup"><span data-stu-id="790ea-213">a.</span></span> <span data-ttu-id="790ea-214">W hello **nazwa** pole tekstowe, typ **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="790ea-214">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="790ea-215">b.</span><span class="sxs-lookup"><span data-stu-id="790ea-215">b.</span></span> <span data-ttu-id="790ea-216">W hello **nazwy użytkownika** pole tekstowe, hello typu **adres e-mail** z BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="790ea-216">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="790ea-217">c.</span><span class="sxs-lookup"><span data-stu-id="790ea-217">c.</span></span> <span data-ttu-id="790ea-218">Wybierz **Pokaż hasło** i zanotuj wartość hello hello **hasło**.</span><span class="sxs-lookup"><span data-stu-id="790ea-218">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="790ea-219">d.</span><span class="sxs-lookup"><span data-stu-id="790ea-219">d.</span></span> <span data-ttu-id="790ea-220">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="790ea-220">Click **Create**.</span></span>
 
### <a name="creating-a-bluejeans-test-user"></a><span data-ttu-id="790ea-221">Tworzenie użytkownika testowego BlueJeans</span><span class="sxs-lookup"><span data-stu-id="790ea-221">Creating a BlueJeans test user</span></span>

<span data-ttu-id="790ea-222">toolog użytkowników tooenable usługi Azure AD w tooBlueJeans, muszą mieć przydzielone do BlueJeans.</span><span class="sxs-lookup"><span data-stu-id="790ea-222">tooenable Azure AD users toolog in tooBlueJeans, they must be provisioned into BlueJeans.</span></span>  

<span data-ttu-id="790ea-223">W przypadku BlueJeans Inicjowanie obsługi to zadanie ręczne.</span><span class="sxs-lookup"><span data-stu-id="790ea-223">In case of BlueJeans, provisioning is a manual task.</span></span>

<span data-ttu-id="790ea-224">**tooprovision kont użytkowników, wykonaj hello następujące kroki:**</span><span class="sxs-lookup"><span data-stu-id="790ea-224">**tooprovision a user accounts, perform hello following steps:**</span></span>

1. <span data-ttu-id="790ea-225">Zaloguj się za tooyour **BlueJeans** witryny firmy jako administrator.</span><span class="sxs-lookup"><span data-stu-id="790ea-225">Log in tooyour **BlueJeans** company site as an administrator.</span></span>

2. <span data-ttu-id="790ea-226">Przejdź za**ADMIN \> Zarządzanie użytkownikami \> Dodaj użytkownika**.</span><span class="sxs-lookup"><span data-stu-id="790ea-226">Go too**ADMIN \> Manage Users \> Add User**.</span></span>
   
   <span data-ttu-id="790ea-227">![Administrator](./media/active-directory-saas-bluejeans-tutorial/IC785877.png "administratora")</span><span class="sxs-lookup"><span data-stu-id="790ea-227">![Admin](./media/active-directory-saas-bluejeans-tutorial/IC785877.png "Admin")</span></span>
   
   >[!IMPORTANT]
   ><span data-ttu-id="790ea-228">Witaj **Dodaj użytkownika** karta jest dostępna tylko, gdy w hello **kartę Zabezpieczenia**, **Włącz automatyczne udostępnianie** nie jest zaznaczone.</span><span class="sxs-lookup"><span data-stu-id="790ea-228">hello **Add User** tab is only available if, in hello **Security tab**, **Enable automatic provisioning** is unchecked.</span></span> 
   
3. <span data-ttu-id="790ea-229">W hello **Dodaj użytkownika** sekcji, wykonaj następujące kroki hello:</span><span class="sxs-lookup"><span data-stu-id="790ea-229">In hello **Add User** section, perform hello following steps:</span></span>

    <span data-ttu-id="790ea-230">![Dodaj użytkownika](./media/active-directory-saas-bluejeans-tutorial/IC785886.png "Dodaj użytkownika")</span><span class="sxs-lookup"><span data-stu-id="790ea-230">![Add User](./media/active-directory-saas-bluejeans-tutorial/IC785886.png "Add User")</span></span>
    
    <span data-ttu-id="790ea-231">a.</span><span class="sxs-lookup"><span data-stu-id="790ea-231">a.</span></span> <span data-ttu-id="790ea-232">Wpisz **BlueJeans Username**, **adres E-mail**, **identyfikator spotkania BlueJeans**, **moderatora kod dostępu**, **imię i nazwisko** , hello **firmy** z prawidłowego konta usługi AAD mają tooprovision w hello związane z pól tekstowych.</span><span class="sxs-lookup"><span data-stu-id="790ea-232">Type a **BlueJeans Username**, an **Email address**, a **BlueJeans Meeting ID**, a **Moderator Passcode**, a **Full Name**, hello **Company** of a valid AAD account you want tooprovision into hello related textboxes.</span></span>
    
    <span data-ttu-id="790ea-233">b.</span><span class="sxs-lookup"><span data-stu-id="790ea-233">b.</span></span> <span data-ttu-id="790ea-234">Kliknij przycisk **dodać użytkownika**.</span><span class="sxs-lookup"><span data-stu-id="790ea-234">Click **Add User**.</span></span>

>[!NOTE]
><span data-ttu-id="790ea-235">Możesz użyć innych BlueJeans użytkownika konta tworzenia narzędzi lub interfejsów API dostarczonych przez BlueJeans tooprovision kont użytkowników usługi AAD.</span><span class="sxs-lookup"><span data-stu-id="790ea-235">You can use any other BlueJeans user account creation tools or APIs provided by BlueJeans tooprovision AAD user accounts.</span></span> 
> 

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="790ea-236">Przypisanie użytkownika testowego hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="790ea-236">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="790ea-237">W tej sekcji możesz włączyć toouse Simona Britta Azure logowania jednokrotnego za udzielanie dostępu tooBlueJeans.</span><span class="sxs-lookup"><span data-stu-id="790ea-237">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooBlueJeans.</span></span>

![Przypisz użytkownika][200] 

<span data-ttu-id="790ea-239">**tooassign tooBlueJeans Simona Britta wykonaj hello następujące kroki:**</span><span class="sxs-lookup"><span data-stu-id="790ea-239">**tooassign Britta Simon tooBlueJeans, perform hello following steps:**</span></span>

1. <span data-ttu-id="790ea-240">W portalu Azure hello, otwórz widok aplikacji hello, a następnie przejdź do widoku katalogu toohello i przejść za**aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="790ea-240">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Przypisz użytkownika][201] 

2. <span data-ttu-id="790ea-242">Z listy aplikacji hello wybierz **BlueJeans**.</span><span class="sxs-lookup"><span data-stu-id="790ea-242">In hello applications list, select **BlueJeans**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-bluejeans-tutorial/tutorial_bluejeans_app.png) 

3. <span data-ttu-id="790ea-244">W menu powitania po lewej stronie powitania kliknij **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="790ea-244">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Przypisz użytkownika][202] 

4. <span data-ttu-id="790ea-246">Kliknij przycisk **Dodaj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="790ea-246">Click **Add** button.</span></span> <span data-ttu-id="790ea-247">Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="790ea-247">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Przypisz użytkownika][203]

5. <span data-ttu-id="790ea-249">Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** hello listy użytkowników.</span><span class="sxs-lookup"><span data-stu-id="790ea-249">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="790ea-250">Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="790ea-250">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="790ea-251">Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="790ea-251">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="790ea-252">Testowanie rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="790ea-252">Testing single sign-on</span></span>

<span data-ttu-id="790ea-253">W tej sekcji można przetestować konfiguracji usługi Azure AD pojedynczego logowania jednokrotnego przy użyciu hello panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="790ea-253">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="790ea-254">Po kliknięciu powitalne BlueJeans kafelka w hello Panel dostępu, należy pobrać strony logowania BlueJeans aplikacji.</span><span class="sxs-lookup"><span data-stu-id="790ea-254">When you click hello BlueJeans tile in hello Access Panel, you should get login page of BlueJeans application.</span></span>
<span data-ttu-id="790ea-255">Aby uzyskać więcej informacji na temat hello Panel dostępu, zobacz [toohello wprowadzenie panelu dostępu](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="790ea-255">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="790ea-256">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="790ea-256">Additional resources</span></span>

* [<span data-ttu-id="790ea-257">Lista samouczków dotyczących tooIntegrate aplikacji SaaS w usłudze Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="790ea-257">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="790ea-258">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="790ea-258">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-bluejeans-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-bluejeans-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-bluejeans-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-bluejeans-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-bluejeans-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-bluejeans-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-bluejeans-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-bluejeans-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-bluejeans-tutorial/tutorial_general_203.png

