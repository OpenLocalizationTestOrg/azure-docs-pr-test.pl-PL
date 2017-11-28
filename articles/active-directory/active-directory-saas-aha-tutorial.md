---
title: 'Samouczek: Integracji Azure Active Directory z Aha! | Microsoft Docs'
description: "Dowiedz się, jak tooconfigure logowanie jednokrotne między usługą Azure Active Directory i Aha!."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: ad955d3d-896a-41bb-800d-68e8cb5ff48d
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/10/2017
ms.author: jeedes
ms.openlocfilehash: d844db3c0a035560e6fb275017215171743fba56
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-aha"></a><span data-ttu-id="bb4d1-104">Samouczek: Integracji Azure Active Directory z Aha!</span><span class="sxs-lookup"><span data-stu-id="bb4d1-104">Tutorial: Azure Active Directory integration with Aha!</span></span>

<span data-ttu-id="bb4d1-105">Z tego samouczka, dowiesz się, jak toointegrate Aha!</span><span class="sxs-lookup"><span data-stu-id="bb4d1-105">In this tutorial, you learn how toointegrate Aha!</span></span> <span data-ttu-id="bb4d1-106">z usługi Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="bb4d1-106">with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="bb4d1-107">Integrowanie Aha!</span><span class="sxs-lookup"><span data-stu-id="bb4d1-107">Integrating Aha!</span></span> <span data-ttu-id="bb4d1-108">z usługą Azure AD zapewnia hello następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="bb4d1-108">with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="bb4d1-109">Można kontrolować w usłudze Azure AD, kto ma dostęp do tooAha!</span><span class="sxs-lookup"><span data-stu-id="bb4d1-109">You can control in Azure AD who has access tooAha!</span></span>
- <span data-ttu-id="bb4d1-110">Można włączyć użytkownika użytkownicy tooautomatically get zalogowane tooAha!</span><span class="sxs-lookup"><span data-stu-id="bb4d1-110">You can enable your users tooautomatically get signed-on tooAha!</span></span> <span data-ttu-id="bb4d1-111">(Logowanie jednokrotne) przy użyciu ich kont usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="bb4d1-111">(Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="bb4d1-112">Możesz zarządzać kont w jednej centralnej lokalizacji - hello portalu Azure</span><span class="sxs-lookup"><span data-stu-id="bb4d1-112">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="bb4d1-113">Jeśli chcesz tooknow więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="bb4d1-113">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="bb4d1-114">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="bb4d1-114">Prerequisites</span></span>

<span data-ttu-id="bb4d1-115">tooconfigure integracji z usługą Azure AD z Aha!, potrzebujesz hello następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="bb4d1-115">tooconfigure Azure AD integration with Aha!, you need hello following items:</span></span>

- <span data-ttu-id="bb4d1-116">Subskrypcję usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="bb4d1-116">An Azure AD subscription</span></span>
- <span data-ttu-id="bb4d1-117">Aha!</span><span class="sxs-lookup"><span data-stu-id="bb4d1-117">An Aha!</span></span> <span data-ttu-id="bb4d1-118">jednokrotnego włączone subskrypcji</span><span class="sxs-lookup"><span data-stu-id="bb4d1-118">single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="bb4d1-119">tootest hello kroków w tym samouczku, zaleca się przy użyciu środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="bb4d1-119">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="bb4d1-120">tootest hello kroki opisane w tym samouczku, należy stosować te zalecenia:</span><span class="sxs-lookup"><span data-stu-id="bb4d1-120">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="bb4d1-121">Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="bb4d1-121">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="bb4d1-122">Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz pobrać miesięczna wersja próbna [tutaj](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="bb4d1-122">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="bb4d1-123">Opis scenariusza</span><span class="sxs-lookup"><span data-stu-id="bb4d1-123">Scenario description</span></span>
<span data-ttu-id="bb4d1-124">W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym.</span><span class="sxs-lookup"><span data-stu-id="bb4d1-124">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="bb4d1-125">Scenariusz Hello opisane w tym samouczku składa się z dwóch głównych elementów:</span><span class="sxs-lookup"><span data-stu-id="bb4d1-125">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="bb4d1-126">Dodawanie Aha!</span><span class="sxs-lookup"><span data-stu-id="bb4d1-126">Adding Aha!</span></span> <span data-ttu-id="bb4d1-127">z galerii hello</span><span class="sxs-lookup"><span data-stu-id="bb4d1-127">from hello gallery</span></span>
2. <span data-ttu-id="bb4d1-128">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="bb4d1-128">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-aha-from-hello-gallery"></a><span data-ttu-id="bb4d1-129">Dodawanie Aha!</span><span class="sxs-lookup"><span data-stu-id="bb4d1-129">Adding Aha!</span></span> <span data-ttu-id="bb4d1-130">z galerii hello</span><span class="sxs-lookup"><span data-stu-id="bb4d1-130">from hello gallery</span></span>
<span data-ttu-id="bb4d1-131">Integracja hello tooconfigure Aha!</span><span class="sxs-lookup"><span data-stu-id="bb4d1-131">tooconfigure hello integration of Aha!</span></span> <span data-ttu-id="bb4d1-132">w usłudze Azure AD należy tooadd Aha!</span><span class="sxs-lookup"><span data-stu-id="bb4d1-132">into Azure AD, you need tooadd Aha!</span></span> <span data-ttu-id="bb4d1-133">z listy tooyour galerii hello zarządzanych aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="bb4d1-133">from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="bb4d1-134">**tooadd Aha! z galerii hello wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="bb4d1-134">**tooadd Aha! from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="bb4d1-135">W hello  **[portalu Azure](https://portal.azure.com)**na temat hello panelu nawigacji po lewej stronie, kliknij przycisk **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="bb4d1-135">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Usługa Active Directory][1]

2. <span data-ttu-id="bb4d1-137">Przejdź za**aplikacje dla przedsiębiorstw**.</span><span class="sxs-lookup"><span data-stu-id="bb4d1-137">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="bb4d1-138">Następnie przejdź zbyt**wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="bb4d1-138">Then go too**All applications**.</span></span>

    ![Aplikacje][2]
    
3. <span data-ttu-id="bb4d1-140">tooadd nową aplikację, kliknij przycisk **nowej aplikacji** przycisk u góry hello okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="bb4d1-140">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplikacje][3]

4. <span data-ttu-id="bb4d1-142">W polu wyszukiwania hello wpisz **Aha!**.</span><span class="sxs-lookup"><span data-stu-id="bb4d1-142">In hello search box, type **Aha!**.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-aha-tutorial/tutorial_aha_search.png)

5. <span data-ttu-id="bb4d1-144">W panelu wyników hello zaznacz **Aha!**, a następnie kliknij przycisk **Dodaj** przycisk aplikacji hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="bb4d1-144">In hello results panel, select **Aha!**, and then click **Add** button tooadd hello application.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-aha-tutorial/tutorial_aha_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="bb4d1-146">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="bb4d1-146">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="bb4d1-147">W tej sekcji możesz skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z Aha!</span><span class="sxs-lookup"><span data-stu-id="bb4d1-147">In this section, you configure and test Azure AD single sign-on with Aha!</span></span> <span data-ttu-id="bb4d1-148">na podstawie użytkownika testowego, nazywany "Britta Simona".</span><span class="sxs-lookup"><span data-stu-id="bb4d1-148">based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="bb4d1-149">Dla pojedynczego logowania jednokrotnego toowork usługi Azure AD wymaga tooknow użytkownika odpowiednikiem hello w Aha!</span><span class="sxs-lookup"><span data-stu-id="bb4d1-149">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Aha!</span></span> <span data-ttu-id="bb4d1-150">jest tooa użytkownika w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="bb4d1-150">is tooa user in Azure AD.</span></span> <span data-ttu-id="bb4d1-151">Innymi słowy link relację między użytkownika usługi Azure AD i hello użytkownikowi w Aha!</span><span class="sxs-lookup"><span data-stu-id="bb4d1-151">In other words, a link relationship between an Azure AD user and hello related user in Aha!</span></span> <span data-ttu-id="bb4d1-152">należy ustanowić toobe.</span><span class="sxs-lookup"><span data-stu-id="bb4d1-152">needs toobe established.</span></span>

<span data-ttu-id="bb4d1-153">W Aha!, przypisz wartość hello hello **nazwy użytkownika** w usłudze Azure AD jako wartość hello hello **Username** tooestablish hello łącze relacji.</span><span class="sxs-lookup"><span data-stu-id="bb4d1-153">In Aha!, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="bb4d1-154">tooconfigure i testowych usługi Azure AD logowanie jednokrotne z Aha!, należy po bloków konstrukcyjnych hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="bb4d1-154">tooconfigure and test Azure AD single sign-on with Aha!, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="bb4d1-155">**[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configuring-azure-ad-single-sign-on)**  -tooenable Twojego toouse użytkowników tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="bb4d1-155">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="bb4d1-156">**[Tworzenie użytkownika testowego usługi Azure AD](#creating-an-azure-ad-test-user)**  -tootest usługi Azure AD rejestracji jednokrotnej z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="bb4d1-156">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="bb4d1-157">**[Tworzenie Aha! Użytkownik testowy](#creating-an-aha-test-user)**  -toohave odpowiednikiem Simona Britta w Aha!</span><span class="sxs-lookup"><span data-stu-id="bb4d1-157">**[Creating an Aha! test user](#creating-an-aha-test-user)** - toohave a counterpart of Britta Simon in Aha!</span></span> <span data-ttu-id="bb4d1-158">to jest połączony toohello reprezentacja użytkownika usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="bb4d1-158">that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="bb4d1-159">**[Przypisanie użytkownika testowego hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Simona Britta toouse usługi Azure AD rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="bb4d1-159">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="bb4d1-160">**[Testowanie rejestracji jednokrotnej](#testing-single-sign-on)**  -tooverify czy hello konfiguracji działania.</span><span class="sxs-lookup"><span data-stu-id="bb4d1-160">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="bb4d1-161">Konfigurowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="bb4d1-161">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="bb4d1-162">W tej sekcji włączyć usługi Azure AD rejestracji jednokrotnej w hello portalu Azure i skonfigurować logowanie jednokrotne w sieci Aha!</span><span class="sxs-lookup"><span data-stu-id="bb4d1-162">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Aha!</span></span> <span data-ttu-id="bb4d1-163">Aplikacja.</span><span class="sxs-lookup"><span data-stu-id="bb4d1-163">application.</span></span>

<span data-ttu-id="bb4d1-164">**tooconfigure usługi Azure AD rejestracji jednokrotnej z Aha!, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="bb4d1-164">**tooconfigure Azure AD single sign-on with Aha!, perform hello following steps:**</span></span>

1. <span data-ttu-id="bb4d1-165">W portalu Azure na powitania hello **Aha!**</span><span class="sxs-lookup"><span data-stu-id="bb4d1-165">In hello Azure portal, on hello **Aha!**</span></span> <span data-ttu-id="bb4d1-166">Strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.</span><span class="sxs-lookup"><span data-stu-id="bb4d1-166">application integration page, click **Single sign-on**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej][4]

2. <span data-ttu-id="bb4d1-168">Na powitania **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** tooenable rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="bb4d1-168">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-aha-tutorial/tutorial_aha_samlbase.png)

3. <span data-ttu-id="bb4d1-170">Na powitania **Aha! Adresy URL i domeny** sekcji, wykonaj następujące kroki hello:</span><span class="sxs-lookup"><span data-stu-id="bb4d1-170">On hello **Aha! Domain and URLs** section, perform hello following steps:</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-aha-tutorial/tutorial_aha_url.png)

    <span data-ttu-id="bb4d1-172">a.</span><span class="sxs-lookup"><span data-stu-id="bb4d1-172">a.</span></span> <span data-ttu-id="bb4d1-173">W hello **adres URL logowania** tekstowym, wpisz adres URL za pomocą hello następującego wzorca:`https://<companyname>.aha.io/session/new`</span><span class="sxs-lookup"><span data-stu-id="bb4d1-173">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<companyname>.aha.io/session/new`</span></span>

    <span data-ttu-id="bb4d1-174">b.</span><span class="sxs-lookup"><span data-stu-id="bb4d1-174">b.</span></span> <span data-ttu-id="bb4d1-175">W hello **identyfikator** tekstowym, wpisz adres URL za pomocą hello następującego wzorca:`https://<companyname>.aha.io`</span><span class="sxs-lookup"><span data-stu-id="bb4d1-175">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<companyname>.aha.io`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="bb4d1-176">Wartości te nie są prawdziwe.</span><span class="sxs-lookup"><span data-stu-id="bb4d1-176">These values are not real.</span></span> <span data-ttu-id="bb4d1-177">Zaktualizować te wartości z hello rzeczywisty adres URL logowania i identyfikator.</span><span class="sxs-lookup"><span data-stu-id="bb4d1-177">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="bb4d1-178">Skontaktuj się z [Aha! Zespół obsługi klienta](https://www.aha.io/company/contact) tooget tych wartości.</span><span class="sxs-lookup"><span data-stu-id="bb4d1-178">Contact [Aha! Client support team](https://www.aha.io/company/contact) tooget these values.</span></span> 
 
4. <span data-ttu-id="bb4d1-179">Na powitania **certyfikat podpisywania SAML** kliknij **XML metadanych** , a następnie zapisz plik metadanych hello na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="bb4d1-179">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-aha-tutorial/tutorial_aha_certificate.png) 

5. <span data-ttu-id="bb4d1-181">Kliknij przycisk **zapisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="bb4d1-181">Click **Save** button.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-aha-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="bb4d1-183">W oknie przeglądarki innej witryny sieci web Zaloguj się za tooyour Aha!</span><span class="sxs-lookup"><span data-stu-id="bb4d1-183">In a different web browser window, log in tooyour Aha!</span></span> <span data-ttu-id="bb4d1-184">Witryna firmy jako administrator.</span><span class="sxs-lookup"><span data-stu-id="bb4d1-184">company site as an administrator.</span></span>

7. <span data-ttu-id="bb4d1-185">W menu hello na górze hello, kliknij przycisk **ustawienia**.</span><span class="sxs-lookup"><span data-stu-id="bb4d1-185">In hello menu on hello top, click **Settings**.</span></span>

    <span data-ttu-id="bb4d1-186">![Ustawienia](./media/active-directory-saas-aha-tutorial/IC798950.png "ustawienia")</span><span class="sxs-lookup"><span data-stu-id="bb4d1-186">![Settings](./media/active-directory-saas-aha-tutorial/IC798950.png "Settings")</span></span>

8. <span data-ttu-id="bb4d1-187">Kliknij przycisk **konta**.</span><span class="sxs-lookup"><span data-stu-id="bb4d1-187">Click **Account**.</span></span>
   
    <span data-ttu-id="bb4d1-188">![Profil](./media/active-directory-saas-aha-tutorial/IC798951.png "profilu")</span><span class="sxs-lookup"><span data-stu-id="bb4d1-188">![Profile](./media/active-directory-saas-aha-tutorial/IC798951.png "Profile")</span></span>

9. <span data-ttu-id="bb4d1-189">Kliknij przycisk **zabezpieczeń i logowanie jednokrotne**.</span><span class="sxs-lookup"><span data-stu-id="bb4d1-189">Click **Security and single sign-on**.</span></span>
   
    <span data-ttu-id="bb4d1-190">![Bezpieczeństwo i logowanie jednokrotne](./media/active-directory-saas-aha-tutorial/IC798952.png "zabezpieczeń i logowanie jednokrotne")</span><span class="sxs-lookup"><span data-stu-id="bb4d1-190">![Security and single sign-on](./media/active-directory-saas-aha-tutorial/IC798952.png "Security and single sign-on")</span></span>

10. <span data-ttu-id="bb4d1-191">W **rejestracji jednokrotnej** sekcji jako **dostawcy tożsamości**, wybierz pozycję **SAML2.0**.</span><span class="sxs-lookup"><span data-stu-id="bb4d1-191">In **Single Sign-On** section, as **Identity Provider**, select **SAML2.0**.</span></span>
   
    <span data-ttu-id="bb4d1-192">![Bezpieczeństwo i logowanie jednokrotne](./media/active-directory-saas-aha-tutorial/IC798953.png "zabezpieczeń i logowanie jednokrotne")</span><span class="sxs-lookup"><span data-stu-id="bb4d1-192">![Security and single sign-on](./media/active-directory-saas-aha-tutorial/IC798953.png "Security and single sign-on")</span></span>

11. <span data-ttu-id="bb4d1-193">Na powitania **rejestracji jednokrotnej** konfiguracji wykonaj hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="bb4d1-193">On hello **Single Sign-On** configuration page, perform hello following steps:</span></span>
    
    <span data-ttu-id="bb4d1-194">![Logowanie jednokrotne](./media/active-directory-saas-aha-tutorial/IC798954.png "logowanie jednokrotne")</span><span class="sxs-lookup"><span data-stu-id="bb4d1-194">![Single Sign-On](./media/active-directory-saas-aha-tutorial/IC798954.png "Single Sign-On")</span></span>
    
       <span data-ttu-id="bb4d1-195">a.</span><span class="sxs-lookup"><span data-stu-id="bb4d1-195">a.</span></span> <span data-ttu-id="bb4d1-196">W hello **nazwa** tekstowym, wpisz nazwę dla danej konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="bb4d1-196">In hello **Name** textbox, type a name for your configuration.</span></span>

       <span data-ttu-id="bb4d1-197">b.</span><span class="sxs-lookup"><span data-stu-id="bb4d1-197">b.</span></span> <span data-ttu-id="bb4d1-198">Aby uzyskać **skonfigurować za pomocą**, wybierz pozycję **pliku metadanych**.</span><span class="sxs-lookup"><span data-stu-id="bb4d1-198">For **Configure using**, select **Metadata File**.</span></span>
   
       <span data-ttu-id="bb4d1-199">c.</span><span class="sxs-lookup"><span data-stu-id="bb4d1-199">c.</span></span> <span data-ttu-id="bb4d1-200">tooupload pliku metadanych pobranych, kliknij przycisk **Przeglądaj**.</span><span class="sxs-lookup"><span data-stu-id="bb4d1-200">tooupload your downloaded metadata file, click **Browse**.</span></span>
   
       <span data-ttu-id="bb4d1-201">d.</span><span class="sxs-lookup"><span data-stu-id="bb4d1-201">d.</span></span> <span data-ttu-id="bb4d1-202">Kliknij przycisk **aktualizacji**.</span><span class="sxs-lookup"><span data-stu-id="bb4d1-202">Click **Update**.</span></span>

> [!TIP]
> <span data-ttu-id="bb4d1-203">Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz hello [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji hello!</span><span class="sxs-lookup"><span data-stu-id="bb4d1-203">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="bb4d1-204">Po dodaniu tej aplikacji z hello **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij hello **rejestracji jednokrotnej** hello kartę i dostępu do osadzonych dokumentacji za pośrednictwem hello  **Konfiguracja** sekcji u dołu hello.</span><span class="sxs-lookup"><span data-stu-id="bb4d1-204">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="bb4d1-205">Więcej o hello osadzonych dokumentacji funkcji w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="bb4d1-205">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="bb4d1-206">Tworzenie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="bb4d1-206">Creating an Azure AD test user</span></span>
<span data-ttu-id="bb4d1-207">Celem Hello w tej sekcji jest toocreate użytkownika testowego, w portalu Azure o nazwie Simona Britta hello.</span><span class="sxs-lookup"><span data-stu-id="bb4d1-207">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Tworzenie użytkowników usługi Azure AD][100]

<span data-ttu-id="bb4d1-209">**toocreate użytkownika testowego w usłudze Azure AD, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="bb4d1-209">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="bb4d1-210">W hello **portalu Azure**na temat hello w lewym okienku nawigacji, kliknij przycisk **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="bb4d1-210">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-aha-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="bb4d1-212">toodisplay hello listę użytkowników, przejdź zbyt**użytkowników i grup** i kliknij przycisk **wszyscy użytkownicy**.</span><span class="sxs-lookup"><span data-stu-id="bb4d1-212">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-aha-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="bb4d1-214">Witaj tooopen **użytkownika** okna dialogowego, kliknij przycisk **Dodaj** u góry hello hello okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="bb4d1-214">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-aha-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="bb4d1-216">Na powitania **użytkownika** okna dialogowego wykonaj hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="bb4d1-216">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-aha-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="bb4d1-218">a.</span><span class="sxs-lookup"><span data-stu-id="bb4d1-218">a.</span></span> <span data-ttu-id="bb4d1-219">W hello **nazwa** pole tekstowe, typ **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="bb4d1-219">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="bb4d1-220">b.</span><span class="sxs-lookup"><span data-stu-id="bb4d1-220">b.</span></span> <span data-ttu-id="bb4d1-221">W hello **nazwy użytkownika** pole tekstowe, hello typu **adres e-mail** z BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="bb4d1-221">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="bb4d1-222">c.</span><span class="sxs-lookup"><span data-stu-id="bb4d1-222">c.</span></span> <span data-ttu-id="bb4d1-223">Wybierz **Pokaż hasło** i zanotuj wartość hello hello **hasło**.</span><span class="sxs-lookup"><span data-stu-id="bb4d1-223">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="bb4d1-224">d.</span><span class="sxs-lookup"><span data-stu-id="bb4d1-224">d.</span></span> <span data-ttu-id="bb4d1-225">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="bb4d1-225">Click **Create**.</span></span>
 
### <a name="creating-an-aha-test-user"></a><span data-ttu-id="bb4d1-226">Tworzenie Aha!</span><span class="sxs-lookup"><span data-stu-id="bb4d1-226">Creating an Aha!</span></span> <span data-ttu-id="bb4d1-227">Użytkownik testowy</span><span class="sxs-lookup"><span data-stu-id="bb4d1-227">test user</span></span>

<span data-ttu-id="bb4d1-228">toolog użytkowników tooenable usługi Azure AD w tooAha!, muszą mieć przydzielone do Aha!.</span><span class="sxs-lookup"><span data-stu-id="bb4d1-228">tooenable Azure AD users toolog in tooAha!, they must be provisioned into Aha!.</span></span>  

<span data-ttu-id="bb4d1-229">W przypadku hello Aha!, inicjowanie obsługi administracyjnej jest zautomatyzowanego zadania.</span><span class="sxs-lookup"><span data-stu-id="bb4d1-229">In hello case of Aha!, provisioning is an automated task.</span></span> <span data-ttu-id="bb4d1-230">Nie ma elementu akcji dla Ciebie.</span><span class="sxs-lookup"><span data-stu-id="bb4d1-230">There is no action item for you.</span></span>

<span data-ttu-id="bb4d1-231">Użytkownicy są tworzone automatycznie w razie potrzeby podczas hello pierwszej pojedynczego logowania jednokrotnego próby.</span><span class="sxs-lookup"><span data-stu-id="bb4d1-231">Users are automatically created if necessary during hello first single sign-on attempt.</span></span>

>[!NOTE]
><span data-ttu-id="bb4d1-232">Można użyć innych Aha!</span><span class="sxs-lookup"><span data-stu-id="bb4d1-232">You can use any other Aha!</span></span> <span data-ttu-id="bb4d1-233">narzędzia do tworzenia konta użytkownika lub interfejsów API dostarczonych przez Aha!</span><span class="sxs-lookup"><span data-stu-id="bb4d1-233">user account creation tools or APIs provided by Aha!</span></span> <span data-ttu-id="bb4d1-234">tooprovision kont użytkowników usługi AAD.</span><span class="sxs-lookup"><span data-stu-id="bb4d1-234">tooprovision AAD user accounts.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="bb4d1-235">Przypisanie użytkownika testowego hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="bb4d1-235">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="bb4d1-236">W tej sekcji możesz włączyć toouse Simona Britta Azure logowania jednokrotnego za udzielanie dostępu tooAha!.</span><span class="sxs-lookup"><span data-stu-id="bb4d1-236">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooAha!.</span></span>

![Przypisz użytkownika][200] 

<span data-ttu-id="bb4d1-238">**tooassign tooAha Simona Britta!, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="bb4d1-238">**tooassign Britta Simon tooAha!, perform hello following steps:**</span></span>

1. <span data-ttu-id="bb4d1-239">W portalu Azure hello, otwórz widok aplikacji hello, a następnie przejdź do widoku katalogu toohello i przejść za**aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="bb4d1-239">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Przypisz użytkownika][201] 

2. <span data-ttu-id="bb4d1-241">Z listy aplikacji hello wybierz **Aha!**.</span><span class="sxs-lookup"><span data-stu-id="bb4d1-241">In hello applications list, select **Aha!**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-aha-tutorial/tutorial_aha_app.png) 

3. <span data-ttu-id="bb4d1-243">W menu powitania po lewej stronie powitania kliknij **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="bb4d1-243">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Przypisz użytkownika][202] 

4. <span data-ttu-id="bb4d1-245">Kliknij przycisk **Dodaj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="bb4d1-245">Click **Add** button.</span></span> <span data-ttu-id="bb4d1-246">Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="bb4d1-246">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Przypisz użytkownika][203]

5. <span data-ttu-id="bb4d1-248">Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** hello listy użytkowników.</span><span class="sxs-lookup"><span data-stu-id="bb4d1-248">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="bb4d1-249">Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="bb4d1-249">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="bb4d1-250">Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="bb4d1-250">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="bb4d1-251">Testowanie rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="bb4d1-251">Testing single sign-on</span></span>

<span data-ttu-id="bb4d1-252">Jeśli chcesz tootest jednego ustawienia logowania jednokrotnego, otwórz hello panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="bb4d1-252">If you want tootest your single sign-on settings, open hello Access Panel.</span></span> <span data-ttu-id="bb4d1-253">Aby uzyskać więcej informacji na temat hello Panel dostępu, zobacz [toohello wprowadzenie panelu dostępu](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="bb4d1-253">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="bb4d1-254">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="bb4d1-254">Additional resources</span></span>

* [<span data-ttu-id="bb4d1-255">Lista samouczków dotyczących tooIntegrate aplikacji SaaS w usłudze Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="bb4d1-255">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="bb4d1-256">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="bb4d1-256">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-aha-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-aha-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-aha-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-aha-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-aha-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-aha-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-aha-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-aha-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-aha-tutorial/tutorial_general_203.png

