---
title: 'Samouczek: Integracji Azure Active Directory z kanwy Lms | Dokumentacja firmy Microsoft'
description: "Dowiedz się, jak tooconfigure logowanie jednokrotne między usługą Azure Active Directory i LMS kanwy."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: bfed291c-a33e-410d-b919-5b965a631d45
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/08/2017
ms.author: jeedes
ms.openlocfilehash: 8f4a09266a108e2c92326b0909dd0650b1c84d6a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-canvas-lms"></a><span data-ttu-id="3a92f-103">Samouczek: Integracji Azure Active Directory z LMS kanwy</span><span class="sxs-lookup"><span data-stu-id="3a92f-103">Tutorial: Azure Active Directory integration with Canvas LMS</span></span>

<span data-ttu-id="3a92f-104">Z tego samouczka, dowiesz się, jak toointegrate obszaru roboczego z usługą Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="3a92f-104">In this tutorial, you learn how toointegrate Canvas with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="3a92f-105">Integracja z usługą Azure AD kanwy zapewnia hello następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="3a92f-105">Integrating Canvas with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="3a92f-106">Można kontrolować w usłudze Azure AD, kto ma dostęp do tooCanvas</span><span class="sxs-lookup"><span data-stu-id="3a92f-106">You can control in Azure AD who has access tooCanvas</span></span>
- <span data-ttu-id="3a92f-107">Można włączyć użytkownika użytkownicy tooautomatically get zalogowane tooCanvas (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="3a92f-107">You can enable your users tooautomatically get signed-on tooCanvas (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="3a92f-108">Możesz zarządzać kont w jednej centralnej lokalizacji - hello portalu Azure</span><span class="sxs-lookup"><span data-stu-id="3a92f-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="3a92f-109">Jeśli chcesz tooknow więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="3a92f-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="3a92f-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="3a92f-110">Prerequisites</span></span>

<span data-ttu-id="3a92f-111">tooconfigure integracji z usługą Azure AD kanwy, należy hello następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="3a92f-111">tooconfigure Azure AD integration with Canvas, you need hello following items:</span></span>

- <span data-ttu-id="3a92f-112">Subskrypcję usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="3a92f-112">An Azure AD subscription</span></span>
- <span data-ttu-id="3a92f-113">Kanwy jednokrotnego włączone subskrypcji</span><span class="sxs-lookup"><span data-stu-id="3a92f-113">A Canvas single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="3a92f-114">tootest hello kroków w tym samouczku, zaleca się przy użyciu środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="3a92f-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="3a92f-115">tootest hello kroki opisane w tym samouczku, należy stosować te zalecenia:</span><span class="sxs-lookup"><span data-stu-id="3a92f-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="3a92f-116">Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="3a92f-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="3a92f-117">Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz pobrać miesięczna wersja próbna [tutaj](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="3a92f-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="3a92f-118">Opis scenariusza</span><span class="sxs-lookup"><span data-stu-id="3a92f-118">Scenario description</span></span>
<span data-ttu-id="3a92f-119">W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym.</span><span class="sxs-lookup"><span data-stu-id="3a92f-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="3a92f-120">Scenariusz Hello opisane w tym samouczku składa się z dwóch głównych elementów:</span><span class="sxs-lookup"><span data-stu-id="3a92f-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="3a92f-121">Dodanie obszaru roboczego z galerii hello</span><span class="sxs-lookup"><span data-stu-id="3a92f-121">Adding Canvas from hello gallery</span></span>
2. <span data-ttu-id="3a92f-122">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="3a92f-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-canvas-from-hello-gallery"></a><span data-ttu-id="3a92f-123">Dodanie obszaru roboczego z galerii hello</span><span class="sxs-lookup"><span data-stu-id="3a92f-123">Adding Canvas from hello gallery</span></span>
<span data-ttu-id="3a92f-124">tooconfigure hello integracja kanwy programu Azure AD, należy tooadd obszaru roboczego z hello galerii tooyour listę zarządzanych aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="3a92f-124">tooconfigure hello integration of Canvas into Azure AD, you need tooadd Canvas from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="3a92f-125">**tooadd obszaru roboczego z galerii hello wykonaj hello następujące kroki:**</span><span class="sxs-lookup"><span data-stu-id="3a92f-125">**tooadd Canvas from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="3a92f-126">W hello  **[portalu Azure](https://portal.azure.com)**na temat hello panelu nawigacji po lewej stronie, kliknij przycisk **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="3a92f-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Usługa Active Directory][1]

2. <span data-ttu-id="3a92f-128">Przejdź za**aplikacje dla przedsiębiorstw**.</span><span class="sxs-lookup"><span data-stu-id="3a92f-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="3a92f-129">Następnie przejdź zbyt**wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="3a92f-129">Then go too**All applications**.</span></span>

    ![Aplikacje][2]
    
3. <span data-ttu-id="3a92f-131">tooadd nową aplikację, kliknij przycisk **nowej aplikacji** przycisk u góry hello okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="3a92f-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplikacje][3]

4. <span data-ttu-id="3a92f-133">W polu wyszukiwania hello wpisz **kanwy**.</span><span class="sxs-lookup"><span data-stu-id="3a92f-133">In hello search box, type **Canvas**.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-canvas-lms-tutorial/tutorial_canvaslms_search.png)

5. <span data-ttu-id="3a92f-135">W panelu wyników hello, wybierz **kanwy**, a następnie kliknij przycisk **Dodaj** przycisk tooadd hello aplikacji.</span><span class="sxs-lookup"><span data-stu-id="3a92f-135">In hello results panel, select **Canvas**, and then click **Add** button tooadd hello application.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-canvas-lms-tutorial/tutorial_canvaslms_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="3a92f-137">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="3a92f-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="3a92f-138">W tej sekcji możesz skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej kanwy oparte na koncie użytkownika testu o nazwie "Britta Simona".</span><span class="sxs-lookup"><span data-stu-id="3a92f-138">In this section, you configure and test Azure AD single sign-on with Canvas based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="3a92f-139">Dla pojedynczego logowania jednokrotnego toowork usługi Azure AD musi tooknow użytkownika odpowiednikiem hello kanwie jest tooa użytkownika w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="3a92f-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Canvas is tooa user in Azure AD.</span></span> <span data-ttu-id="3a92f-140">Innymi słowy relację łącza między użytkownika usługi Azure AD i hello użytkownikowi kanwie musi toobe ustanowione.</span><span class="sxs-lookup"><span data-stu-id="3a92f-140">In other words, a link relationship between an Azure AD user and hello related user in Canvas needs toobe established.</span></span>

<span data-ttu-id="3a92f-141">W obszarze roboczym należy przypisać wartość hello hello **nazwy użytkownika** w usłudze Azure AD jako wartość hello hello **Username** tooestablish hello łącze relacji.</span><span class="sxs-lookup"><span data-stu-id="3a92f-141">In Canvas, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="3a92f-142">tooconfigure i testowych usługi Azure AD rejestracji jednokrotnej z kanwy, należy po bloków konstrukcyjnych hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="3a92f-142">tooconfigure and test Azure AD single sign-on with Canvas, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="3a92f-143">**[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configuring-azure-ad-single-sign-on)**  -tooenable Twojego toouse użytkowników tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="3a92f-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="3a92f-144">**[Tworzenie użytkownika testowego usługi Azure AD](#creating-an-azure-ad-test-user)**  -tootest usługi Azure AD rejestracji jednokrotnej z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="3a92f-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="3a92f-145">**[Tworzenie użytkownika testowego kanwy](#creating-a-canvas-test-user)**  -toohave odpowiednikiem Simona Britta w kanwy, która jest odpowiednikiem połączonych toohello usługi Azure AD użytkownika.</span><span class="sxs-lookup"><span data-stu-id="3a92f-145">**[Creating a Canvas test user](#creating-a-canvas-test-user)** - toohave a counterpart of Britta Simon in Canvas that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="3a92f-146">**[Przypisanie użytkownika testowego hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Simona Britta toouse usługi Azure AD rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="3a92f-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="3a92f-147">**[Testowanie rejestracji jednokrotnej](#testing-single-sign-on)**  -tooverify czy hello konfiguracji działania.</span><span class="sxs-lookup"><span data-stu-id="3a92f-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="3a92f-148">Konfigurowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="3a92f-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="3a92f-149">W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w portalu Azure hello i skonfigurować logowanie jednokrotne w aplikacji kanwy.</span><span class="sxs-lookup"><span data-stu-id="3a92f-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Canvas application.</span></span>

<span data-ttu-id="3a92f-150">**tooconfigure usługi Azure AD rejestracji jednokrotnej z kanwy, wykonaj hello następujące kroki:**</span><span class="sxs-lookup"><span data-stu-id="3a92f-150">**tooconfigure Azure AD single sign-on with Canvas, perform hello following steps:**</span></span>

1. <span data-ttu-id="3a92f-151">W portalu Azure na powitania hello **kanwy** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.</span><span class="sxs-lookup"><span data-stu-id="3a92f-151">In hello Azure portal, on hello **Canvas** application integration page, click **Single sign-on**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej][4]

2. <span data-ttu-id="3a92f-153">Na powitania **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** tooenable rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="3a92f-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-canvas-lms-tutorial/tutorial_canvaslms_samlbase.png)

3. <span data-ttu-id="3a92f-155">Na powitania **kanwy domeny i adres URL** sekcji, wykonaj następujące kroki hello:</span><span class="sxs-lookup"><span data-stu-id="3a92f-155">On hello **Canvas Domain and URLs** section, perform hello following steps:</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-canvas-lms-tutorial/tutorial_canvaslms_url.png)

    <span data-ttu-id="3a92f-157">a.</span><span class="sxs-lookup"><span data-stu-id="3a92f-157">a.</span></span> <span data-ttu-id="3a92f-158">W hello **adres URL logowania** tekstowym, wpisz adres URL za pomocą hello następującego wzorca:`https://<tenant-name>.instructure.com`</span><span class="sxs-lookup"><span data-stu-id="3a92f-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<tenant-name>.instructure.com`</span></span>

    <span data-ttu-id="3a92f-159">b.</span><span class="sxs-lookup"><span data-stu-id="3a92f-159">b.</span></span> <span data-ttu-id="3a92f-160">W hello **identyfikator** pole tekstowe, wartość hello typu przy użyciu hello następującego wzorca:`https://<tenant-name>.instructure.com/saml2`</span><span class="sxs-lookup"><span data-stu-id="3a92f-160">In hello **Identifier** textbox, type hello value using hello following pattern: `https://<tenant-name>.instructure.com/saml2`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="3a92f-161">Wartości te nie są prawdziwe.</span><span class="sxs-lookup"><span data-stu-id="3a92f-161">These values are not real.</span></span> <span data-ttu-id="3a92f-162">Zaktualizować te wartości z hello rzeczywisty adres URL logowania i identyfikator.</span><span class="sxs-lookup"><span data-stu-id="3a92f-162">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="3a92f-163">Skontaktuj się z [zespołem pomocy technicznej klienta kanwy](https://community.canvaslms.com/community/help) tooget tych wartości.</span><span class="sxs-lookup"><span data-stu-id="3a92f-163">Contact [Canvas Client support team](https://community.canvaslms.com/community/help) tooget these values.</span></span> 
 
4. <span data-ttu-id="3a92f-164">Na powitania **certyfikat podpisywania SAML** hello kopiowania, sekcji **odcisk PALCA** wartości certyfikatu.</span><span class="sxs-lookup"><span data-stu-id="3a92f-164">On hello **SAML Signing Certificate** section, copy hello **THUMBPRINT** value of certificate.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-canvas-lms-tutorial/tutorial_canvaslms_certificate.png) 

5. <span data-ttu-id="3a92f-166">Kliknij przycisk **zapisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="3a92f-166">Click **Save** button.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-canvas-lms-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="3a92f-168">Na powitania **konfiguracji kanwy** kliknij **skonfigurować kanwy** tooopen **Konfigurowanie logowania jednokrotnego** okna.</span><span class="sxs-lookup"><span data-stu-id="3a92f-168">On hello **Canvas Configuration** section, click **Configure Canvas** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="3a92f-169">Kopiuj hello **Zmień adres URL hasła, adres URL Sign-Out identyfikator jednostki SAML i SAML pojedynczy znak na adres URL usługi** z hello **sekcji krótkimi opisami.**</span><span class="sxs-lookup"><span data-stu-id="3a92f-169">Copy hello **Change Password URL, Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-canvas-lms-tutorial/tutorial_canvaslms_configure.png) 
 
7. <span data-ttu-id="3a92f-171">W oknie przeglądarki innej witryny sieci web Zaloguj się w witrynie firmy kanwy tooyour jako administrator.</span><span class="sxs-lookup"><span data-stu-id="3a92f-171">In a different web browser window, log in tooyour Canvas company site as an administrator.</span></span>

8. <span data-ttu-id="3a92f-172">Przejdź za**kursów \> kont zarządzanych \> Microsoft**.</span><span class="sxs-lookup"><span data-stu-id="3a92f-172">Go too**Courses \> Managed Accounts \> Microsoft**.</span></span>
   
    <span data-ttu-id="3a92f-173">![Kanwy](./media/active-directory-saas-canvas-lms-tutorial/IC775990.png "kanwy")</span><span class="sxs-lookup"><span data-stu-id="3a92f-173">![Canvas](./media/active-directory-saas-canvas-lms-tutorial/IC775990.png "Canvas")</span></span>

9. <span data-ttu-id="3a92f-174">W okienku nawigacji hello powitania po lewej stronie wybierz **uwierzytelniania**, a następnie kliknij przycisk **dodać nowej konfiguracji SAML**.</span><span class="sxs-lookup"><span data-stu-id="3a92f-174">In hello navigation pane on hello left, select **Authentication**, and then click **Add New SAML Config**.</span></span>
   
    <span data-ttu-id="3a92f-175">![Uwierzytelnianie](./media/active-directory-saas-canvas-lms-tutorial/IC775991.png "uwierzytelniania")</span><span class="sxs-lookup"><span data-stu-id="3a92f-175">![Authentication](./media/active-directory-saas-canvas-lms-tutorial/IC775991.png "Authentication")</span></span>

10. <span data-ttu-id="3a92f-176">Na stronie bieżącego integracji hello wykonaj hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="3a92f-176">On hello Current Integration page, perform hello following steps:</span></span>
   
    <span data-ttu-id="3a92f-177">![Integracja z bieżącym](./media/active-directory-saas-canvas-lms-tutorial/IC775992.png "bieżącego integracji")</span><span class="sxs-lookup"><span data-stu-id="3a92f-177">![Current Integration](./media/active-directory-saas-canvas-lms-tutorial/IC775992.png "Current Integration")</span></span>

    <span data-ttu-id="3a92f-178">a.</span><span class="sxs-lookup"><span data-stu-id="3a92f-178">a.</span></span> <span data-ttu-id="3a92f-179">W **identyfikator jednostki IdP** pole tekstowe, Wklej wartość hello **identyfikator jednostki SAML** którego została skopiowana z portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="3a92f-179">In **IdP Entity ID** textbox, paste hello value of **SAML Entity ID** which you have copied from Azure portal.</span></span>

    <span data-ttu-id="3a92f-180">b.</span><span class="sxs-lookup"><span data-stu-id="3a92f-180">b.</span></span> <span data-ttu-id="3a92f-181">W **dziennika na adres URL** pole tekstowe, Wklej wartość hello **SAML pojedynczy znak na adres URL usługi** którego została skopiowana z portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="3a92f-181">In **Log On URL** textbox, paste hello value of **SAML Single Sign-On Service URL** which you have copied from Azure portal .</span></span>

    <span data-ttu-id="3a92f-182">c.</span><span class="sxs-lookup"><span data-stu-id="3a92f-182">c.</span></span> <span data-ttu-id="3a92f-183">W **adresu URL wylogowania** pole tekstowe, Wklej wartość hello **Sign-Out URL** którego została skopiowana z portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="3a92f-183">In **Log Out URL** textbox, paste hello value of **Sign-Out URL** which you have copied from Azure portal.</span></span>

    <span data-ttu-id="3a92f-184">d.</span><span class="sxs-lookup"><span data-stu-id="3a92f-184">d.</span></span> <span data-ttu-id="3a92f-185">W **łącze Zmień hasło** pole tekstowe, Wklej wartość hello **Zmień adres URL hasła** którego została skopiowana z portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="3a92f-185">In **Change Password Link** textbox, paste hello value of **Change Password URL** which you have copied from Azure portal.</span></span> 

    <span data-ttu-id="3a92f-186">e.</span><span class="sxs-lookup"><span data-stu-id="3a92f-186">e.</span></span> <span data-ttu-id="3a92f-187">W **odcisk palca certyfikatu** pole tekstowe, Wklej hello **odcisk palca** wartość certyfikatów, które zostały skopiowane z portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="3a92f-187">In **Certificate Fingerprint** textbox, paste hello **Thumbprint** value of certificate which you have copied from Azure portal.</span></span>      
        
    <span data-ttu-id="3a92f-188">f.</span><span class="sxs-lookup"><span data-stu-id="3a92f-188">f.</span></span> <span data-ttu-id="3a92f-189">Z hello **atrybutu logowania** listy, wybierz **NameID**.</span><span class="sxs-lookup"><span data-stu-id="3a92f-189">From hello **Login Attribute** list, select **NameID**.</span></span>

    <span data-ttu-id="3a92f-190">g.</span><span class="sxs-lookup"><span data-stu-id="3a92f-190">g.</span></span> <span data-ttu-id="3a92f-191">Z hello **Format identyfikatora** listy, wybierz **emailAddress**.</span><span class="sxs-lookup"><span data-stu-id="3a92f-191">From hello **Identifier Format** list, select **emailAddress**.</span></span>

    <span data-ttu-id="3a92f-192">h.</span><span class="sxs-lookup"><span data-stu-id="3a92f-192">h.</span></span> <span data-ttu-id="3a92f-193">Kliknij przycisk **Zapisz ustawienia uwierzytelniania**.</span><span class="sxs-lookup"><span data-stu-id="3a92f-193">Click **Save Authentication Settings**.</span></span>

> [!TIP]
> <span data-ttu-id="3a92f-194">Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz hello [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji hello!</span><span class="sxs-lookup"><span data-stu-id="3a92f-194">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="3a92f-195">Po dodaniu tej aplikacji z hello **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij hello **rejestracji jednokrotnej** hello kartę i dostępu do osadzonych dokumentacji za pośrednictwem hello  **Konfiguracja** sekcji u dołu hello.</span><span class="sxs-lookup"><span data-stu-id="3a92f-195">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="3a92f-196">Więcej o hello osadzonych dokumentacji funkcji w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="3a92f-196">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="3a92f-197">Tworzenie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="3a92f-197">Creating an Azure AD test user</span></span>
<span data-ttu-id="3a92f-198">Celem Hello w tej sekcji jest toocreate użytkownika testowego, w portalu Azure o nazwie Simona Britta hello.</span><span class="sxs-lookup"><span data-stu-id="3a92f-198">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Tworzenie użytkowników usługi Azure AD][100]

<span data-ttu-id="3a92f-200">**toocreate użytkownika testowego w usłudze Azure AD, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="3a92f-200">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="3a92f-201">W hello **portalu Azure**na temat hello w lewym okienku nawigacji, kliknij przycisk **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="3a92f-201">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-canvas-lms-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="3a92f-203">toodisplay hello listę użytkowników, przejdź zbyt**użytkowników i grup** i kliknij przycisk **wszyscy użytkownicy**.</span><span class="sxs-lookup"><span data-stu-id="3a92f-203">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-canvas-lms-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="3a92f-205">Witaj tooopen **użytkownika** okna dialogowego, kliknij przycisk **Dodaj** u góry hello hello okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="3a92f-205">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-canvas-lms-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="3a92f-207">Na powitania **użytkownika** okna dialogowego wykonaj hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="3a92f-207">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-canvas-lms-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="3a92f-209">a.</span><span class="sxs-lookup"><span data-stu-id="3a92f-209">a.</span></span> <span data-ttu-id="3a92f-210">W hello **nazwa** pole tekstowe, typ **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="3a92f-210">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="3a92f-211">b.</span><span class="sxs-lookup"><span data-stu-id="3a92f-211">b.</span></span> <span data-ttu-id="3a92f-212">W hello **nazwy użytkownika** pole tekstowe, hello typu **adres e-mail** z BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="3a92f-212">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="3a92f-213">c.</span><span class="sxs-lookup"><span data-stu-id="3a92f-213">c.</span></span> <span data-ttu-id="3a92f-214">Wybierz **Pokaż hasło** i zanotuj wartość hello hello **hasło**.</span><span class="sxs-lookup"><span data-stu-id="3a92f-214">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="3a92f-215">d.</span><span class="sxs-lookup"><span data-stu-id="3a92f-215">d.</span></span> <span data-ttu-id="3a92f-216">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="3a92f-216">Click **Create**.</span></span>
 
### <a name="creating-a-canvas-test-user"></a><span data-ttu-id="3a92f-217">Tworzenie użytkownika testowego kanwy</span><span class="sxs-lookup"><span data-stu-id="3a92f-217">Creating a Canvas test user</span></span>

<span data-ttu-id="3a92f-218">toolog użytkowników tooenable usługi Azure AD w tooCanvas, muszą mieć przydzielone do kanwy.</span><span class="sxs-lookup"><span data-stu-id="3a92f-218">tooenable Azure AD users toolog in tooCanvas, they must be provisioned into Canvas.</span></span>

<span data-ttu-id="3a92f-219">W przypadku kanwy Inicjowanie obsługi użytkowników jest zadanie ręczne.</span><span class="sxs-lookup"><span data-stu-id="3a92f-219">In case of Canvas, user provisioning is a manual task.</span></span>

<span data-ttu-id="3a92f-220">**tooprovision konta użytkownika, należy wykonać hello następujące kroki:**</span><span class="sxs-lookup"><span data-stu-id="3a92f-220">**tooprovision a user account, perform hello following steps:**</span></span>

1. <span data-ttu-id="3a92f-221">Zaloguj się za tooyour **kanwy** dzierżawy.</span><span class="sxs-lookup"><span data-stu-id="3a92f-221">Log in tooyour **Canvas** tenant.</span></span>

2. <span data-ttu-id="3a92f-222">Przejdź za**kursów \> kont zarządzanych \> Microsoft**.</span><span class="sxs-lookup"><span data-stu-id="3a92f-222">Go too**Courses \> Managed Accounts \> Microsoft**.</span></span>
   
   <span data-ttu-id="3a92f-223">![Kanwy](./media/active-directory-saas-canvas-lms-tutorial/IC775990.png "kanwy")</span><span class="sxs-lookup"><span data-stu-id="3a92f-223">![Canvas](./media/active-directory-saas-canvas-lms-tutorial/IC775990.png "Canvas")</span></span>

3. <span data-ttu-id="3a92f-224">Kliknij przycisk **użytkowników**.</span><span class="sxs-lookup"><span data-stu-id="3a92f-224">Click **Users**.</span></span>
   
   <span data-ttu-id="3a92f-225">![Użytkownicy](./media/active-directory-saas-canvas-lms-tutorial/IC775995.png "użytkowników")</span><span class="sxs-lookup"><span data-stu-id="3a92f-225">![Users](./media/active-directory-saas-canvas-lms-tutorial/IC775995.png "Users")</span></span>

4. <span data-ttu-id="3a92f-226">Kliknij przycisk **Dodaj nowego użytkownika**.</span><span class="sxs-lookup"><span data-stu-id="3a92f-226">Click **Add New User**.</span></span>
   
   <span data-ttu-id="3a92f-227">![Użytkownicy](./media/active-directory-saas-canvas-lms-tutorial/IC775996.png "użytkowników")</span><span class="sxs-lookup"><span data-stu-id="3a92f-227">![Users](./media/active-directory-saas-canvas-lms-tutorial/IC775996.png "Users")</span></span>

5. <span data-ttu-id="3a92f-228">Dodaj nowego użytkownika strony okna dialogowego hello wykonywanie hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="3a92f-228">On hello Add a New User dialog page, perform hello following steps:</span></span>
   
   <span data-ttu-id="3a92f-229">![Dodaj użytkownika](./media/active-directory-saas-canvas-lms-tutorial/IC775997.png "Dodaj użytkownika")</span><span class="sxs-lookup"><span data-stu-id="3a92f-229">![Add User](./media/active-directory-saas-canvas-lms-tutorial/IC775997.png "Add User")</span></span>
   
   <span data-ttu-id="3a92f-230">a.</span><span class="sxs-lookup"><span data-stu-id="3a92f-230">a.</span></span> <span data-ttu-id="3a92f-231">W hello **imię i nazwisko** pole tekstowe, wprowadź nazwę użytkownika, takie jak hello **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="3a92f-231">In hello **Full Name** textbox, enter hello name of user like **BrittaSimon**.</span></span>

   <span data-ttu-id="3a92f-232">b.</span><span class="sxs-lookup"><span data-stu-id="3a92f-232">b.</span></span> <span data-ttu-id="3a92f-233">W hello **E-mail** pole tekstowe, wprowadź adres e-mail użytkownika, takie jak hello  **brittasimon@contoso.com** .</span><span class="sxs-lookup"><span data-stu-id="3a92f-233">In hello **Email** textbox, enter hello email of user like **brittasimon@contoso.com**.</span></span>

   <span data-ttu-id="3a92f-234">c.</span><span class="sxs-lookup"><span data-stu-id="3a92f-234">c.</span></span> <span data-ttu-id="3a92f-235">W hello **logowania** pole tekstowe, wprowadź adres e-mail usługi Azure AD hello użytkownika, takich jak  **brittasimon@contoso.com** .</span><span class="sxs-lookup"><span data-stu-id="3a92f-235">In hello **Login** textbox, enter hello user’s Azure AD email address like **brittasimon@contoso.com**.</span></span>

   <span data-ttu-id="3a92f-236">d.</span><span class="sxs-lookup"><span data-stu-id="3a92f-236">d.</span></span> <span data-ttu-id="3a92f-237">Wybierz **E-mail hello użytkownika o tworzeniu tego konta**.</span><span class="sxs-lookup"><span data-stu-id="3a92f-237">Select **Email hello user about this account creation**.</span></span>

   <span data-ttu-id="3a92f-238">e.</span><span class="sxs-lookup"><span data-stu-id="3a92f-238">e.</span></span> <span data-ttu-id="3a92f-239">Kliknij przycisk **dodać użytkownika**.</span><span class="sxs-lookup"><span data-stu-id="3a92f-239">Click **Add User**.</span></span>

>[!NOTE]
><span data-ttu-id="3a92f-240">Możesz użyć innych kanwy użytkownika konta tworzenia narzędzi lub interfejsów API dostarczonych przez tooprovision kanwy kont użytkowników usługi AAD.</span><span class="sxs-lookup"><span data-stu-id="3a92f-240">You can use any other Canvas user account creation tools or APIs provided by Canvas tooprovision AAD user accounts.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="3a92f-241">Przypisanie użytkownika testowego hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="3a92f-241">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="3a92f-242">W tej sekcji możesz włączyć toouse Simona Britta Azure logowania jednokrotnego za udzielanie dostępu tooCanvas.</span><span class="sxs-lookup"><span data-stu-id="3a92f-242">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooCanvas.</span></span>

![Przypisz użytkownika][200] 

<span data-ttu-id="3a92f-244">**tooassign tooCanvas Simona Britta wykonaj hello następujące kroki:**</span><span class="sxs-lookup"><span data-stu-id="3a92f-244">**tooassign Britta Simon tooCanvas, perform hello following steps:**</span></span>

1. <span data-ttu-id="3a92f-245">W portalu Azure hello, otwórz widok aplikacji hello, a następnie przejdź do widoku katalogu toohello i przejść za**aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="3a92f-245">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Przypisz użytkownika][201] 

2. <span data-ttu-id="3a92f-247">Z listy aplikacji hello wybierz **kanwy**.</span><span class="sxs-lookup"><span data-stu-id="3a92f-247">In hello applications list, select **Canvas**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-canvas-lms-tutorial/tutorial_canvaslms_app.png) 

3. <span data-ttu-id="3a92f-249">W menu powitania po lewej stronie powitania kliknij **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="3a92f-249">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Przypisz użytkownika][202] 

4. <span data-ttu-id="3a92f-251">Kliknij przycisk **Dodaj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="3a92f-251">Click **Add** button.</span></span> <span data-ttu-id="3a92f-252">Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="3a92f-252">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Przypisz użytkownika][203]

5. <span data-ttu-id="3a92f-254">Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** hello listy użytkowników.</span><span class="sxs-lookup"><span data-stu-id="3a92f-254">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="3a92f-255">Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="3a92f-255">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="3a92f-256">Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="3a92f-256">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="3a92f-257">Testowanie rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="3a92f-257">Testing single sign-on</span></span>

<span data-ttu-id="3a92f-258">W tej sekcji można przetestować konfiguracji usługi Azure AD pojedynczego logowania jednokrotnego przy użyciu hello panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="3a92f-258">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="3a92f-259">Po kliknięciu kafelka kanwy hello w hello Panel dostępu, należy pobrać automatycznie zalogowane tooyour obszaru roboczego aplikacji.</span><span class="sxs-lookup"><span data-stu-id="3a92f-259">When you click hello Canvas tile in hello Access Panel, you should get automatically signed-on tooyour Canvas application.</span></span>
<span data-ttu-id="3a92f-260">Aby uzyskać więcej informacji na temat hello Panel dostępu, zobacz [toohello wprowadzenie panelu dostępu](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="3a92f-260">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="3a92f-261">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="3a92f-261">Additional resources</span></span>

* [<span data-ttu-id="3a92f-262">Lista samouczków dotyczących tooIntegrate aplikacji SaaS w usłudze Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="3a92f-262">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="3a92f-263">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="3a92f-263">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-canvas-lms-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-canvas-lms-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-canvas-lms-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-canvas-lms-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-canvas-lms-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-canvas-lms-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-canvas-lms-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-canvas-lms-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-canvas-lms-tutorial/tutorial_general_203.png

