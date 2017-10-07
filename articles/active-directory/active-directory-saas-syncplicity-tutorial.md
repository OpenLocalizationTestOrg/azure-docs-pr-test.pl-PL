---
title: 'Samouczek: Integracji Azure Active Directory z Syncplicity | Dokumentacja firmy Microsoft'
description: "Dowiedz się, jak tooconfigure logowanie jednokrotne między usługą Azure Active Directory i Syncplicity."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 896a3211-f368-46d7-95b8-e4768c23be08
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/22/2017
ms.author: jeedes
ms.openlocfilehash: 6148112a959232ed24d76d1c7b8773f06568fee7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-syncplicity"></a><span data-ttu-id="97b7f-103">Samouczek: Integracji Azure Active Directory z Syncplicity</span><span class="sxs-lookup"><span data-stu-id="97b7f-103">Tutorial: Azure Active Directory integration with Syncplicity</span></span>

<span data-ttu-id="97b7f-104">Z tego samouczka, dowiesz się, jak toointegrate Syncplicity w usłudze Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="97b7f-104">In this tutorial, you learn how toointegrate Syncplicity with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="97b7f-105">Integracja z usługą Azure AD Syncplicity zapewnia hello następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="97b7f-105">Integrating Syncplicity with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="97b7f-106">Można kontrolować w usłudze Azure AD, kto ma dostęp do tooSyncplicity</span><span class="sxs-lookup"><span data-stu-id="97b7f-106">You can control in Azure AD who has access tooSyncplicity</span></span>
- <span data-ttu-id="97b7f-107">Można włączyć użytkownika użytkownicy tooautomatically get zalogowane tooSyncplicity (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="97b7f-107">You can enable your users tooautomatically get signed-on tooSyncplicity (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="97b7f-108">Możesz zarządzać kont w jednej centralnej lokalizacji - hello portalu Azure</span><span class="sxs-lookup"><span data-stu-id="97b7f-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="97b7f-109">Jeśli chcesz tooknow więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="97b7f-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="97b7f-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="97b7f-110">Prerequisites</span></span>

<span data-ttu-id="97b7f-111">tooconfigure integracji z usługą Azure AD z Syncplicity należy hello następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="97b7f-111">tooconfigure Azure AD integration with Syncplicity, you need hello following items:</span></span>

- <span data-ttu-id="97b7f-112">Subskrypcję usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="97b7f-112">An Azure AD subscription</span></span>
- <span data-ttu-id="97b7f-113">Syncplicity logowanie jednokrotne włączone subskrypcji</span><span class="sxs-lookup"><span data-stu-id="97b7f-113">A Syncplicity single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="97b7f-114">tootest hello kroków w tym samouczku, zaleca się przy użyciu środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="97b7f-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="97b7f-115">tootest hello kroki opisane w tym samouczku, należy stosować te zalecenia:</span><span class="sxs-lookup"><span data-stu-id="97b7f-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="97b7f-116">Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="97b7f-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="97b7f-117">Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz pobrać miesięczna wersja próbna [tutaj](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="97b7f-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="97b7f-118">Opis scenariusza</span><span class="sxs-lookup"><span data-stu-id="97b7f-118">Scenario description</span></span>
<span data-ttu-id="97b7f-119">W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym.</span><span class="sxs-lookup"><span data-stu-id="97b7f-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="97b7f-120">Scenariusz Hello opisane w tym samouczku składa się z dwóch głównych elementów:</span><span class="sxs-lookup"><span data-stu-id="97b7f-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="97b7f-121">Dodawanie Syncplicity z galerii hello</span><span class="sxs-lookup"><span data-stu-id="97b7f-121">Adding Syncplicity from hello gallery</span></span>
2. <span data-ttu-id="97b7f-122">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="97b7f-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-syncplicity-from-hello-gallery"></a><span data-ttu-id="97b7f-123">Dodawanie Syncplicity z galerii hello</span><span class="sxs-lookup"><span data-stu-id="97b7f-123">Adding Syncplicity from hello gallery</span></span>
<span data-ttu-id="97b7f-124">tooconfigure hello integracji Syncplicity do usługi Azure AD, należy tooadd Syncplicity z hello galerii tooyour listę zarządzanych aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="97b7f-124">tooconfigure hello integration of Syncplicity into Azure AD, you need tooadd Syncplicity from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="97b7f-125">**tooadd Syncplicity z galerii hello, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="97b7f-125">**tooadd Syncplicity from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="97b7f-126">W hello  **[portalu Azure](https://portal.azure.com)**na temat hello panelu nawigacji po lewej stronie, kliknij przycisk **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="97b7f-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Usługa Active Directory][1]

2. <span data-ttu-id="97b7f-128">Przejdź za**aplikacje dla przedsiębiorstw**.</span><span class="sxs-lookup"><span data-stu-id="97b7f-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="97b7f-129">Następnie przejdź zbyt**wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="97b7f-129">Then go too**All applications**.</span></span>

    ![Aplikacje][2]
    
3. <span data-ttu-id="97b7f-131">tooadd nową aplikację, kliknij przycisk **nowej aplikacji** przycisk u góry hello okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="97b7f-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplikacje][3]

4. <span data-ttu-id="97b7f-133">W polu wyszukiwania hello wpisz **Syncplicity**.</span><span class="sxs-lookup"><span data-stu-id="97b7f-133">In hello search box, type **Syncplicity**.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-syncplicity-tutorial/tutorial_syncplicity_search.png)

5. <span data-ttu-id="97b7f-135">W panelu wyników hello zaznacz **Syncplicity**, a następnie kliknij przycisk **Dodaj** przycisk aplikacji hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="97b7f-135">In hello results panel, select **Syncplicity**, and then click **Add** button tooadd hello application.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-syncplicity-tutorial/tutorial_syncplicity_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="97b7f-137">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="97b7f-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="97b7f-138">W tej sekcji możesz skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z Syncplicity na podstawie użytkownika testowego, nazywany "Britta Simona".</span><span class="sxs-lookup"><span data-stu-id="97b7f-138">In this section, you configure and test Azure AD single sign-on with Syncplicity based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="97b7f-139">Dla pojedynczego logowania jednokrotnego toowork usługi Azure AD musi tooknow użytkownika odpowiednikiem hello w Syncplicity jest tooa użytkownika w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="97b7f-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Syncplicity is tooa user in Azure AD.</span></span> <span data-ttu-id="97b7f-140">Innymi słowy relację łącza między użytkownika usługi Azure AD i hello użytkownikowi w Syncplicity musi toobe ustanowione.</span><span class="sxs-lookup"><span data-stu-id="97b7f-140">In other words, a link relationship between an Azure AD user and hello related user in Syncplicity needs toobe established.</span></span>

<span data-ttu-id="97b7f-141">W Syncplicity, należy przypisać wartość hello hello **nazwy użytkownika** w usłudze Azure AD jako wartość hello hello **Username** tooestablish hello łącze relacji.</span><span class="sxs-lookup"><span data-stu-id="97b7f-141">In Syncplicity, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="97b7f-142">tooconfigure i testowych usługi Azure AD rejestracji jednokrotnej z Syncplicity, należy po bloków konstrukcyjnych hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="97b7f-142">tooconfigure and test Azure AD single sign-on with Syncplicity, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="97b7f-143">**[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configuring-azure-ad-single-sign-on)**  -tooenable Twojego toouse użytkowników tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="97b7f-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="97b7f-144">**[Tworzenie użytkownika testowego usługi Azure AD](#creating-an-azure-ad-test-user)**  -tootest usługi Azure AD rejestracji jednokrotnej z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="97b7f-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="97b7f-145">**[Tworzenie użytkownika testowego Syncplicity](#creating-a-syncplicity-test-user)**  -toohave odpowiednikiem Simona Britta w Syncplicity, który jest połączony toohello usługi Azure AD reprezentację użytkownika.</span><span class="sxs-lookup"><span data-stu-id="97b7f-145">**[Creating a Syncplicity test user](#creating-a-syncplicity-test-user)** - toohave a counterpart of Britta Simon in Syncplicity that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="97b7f-146">**[Przypisanie użytkownika testowego hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Simona Britta toouse usługi Azure AD rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="97b7f-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="97b7f-147">**[Testowanie rejestracji jednokrotnej](#testing-single-sign-on)**  -tooverify czy hello konfiguracji działania.</span><span class="sxs-lookup"><span data-stu-id="97b7f-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="97b7f-148">Konfigurowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="97b7f-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="97b7f-149">W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w portalu Azure hello i skonfigurować logowanie jednokrotne w aplikacji Syncplicity.</span><span class="sxs-lookup"><span data-stu-id="97b7f-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Syncplicity application.</span></span>

<span data-ttu-id="97b7f-150">**tooconfigure usługi Azure AD rejestracji jednokrotnej z Syncplicity, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="97b7f-150">**tooconfigure Azure AD single sign-on with Syncplicity, perform hello following steps:**</span></span>

1. <span data-ttu-id="97b7f-151">W portalu Azure na powitania hello **Syncplicity** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.</span><span class="sxs-lookup"><span data-stu-id="97b7f-151">In hello Azure portal, on hello **Syncplicity** application integration page, click **Single sign-on**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej][4]

2. <span data-ttu-id="97b7f-153">Na powitania **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** tooenable rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="97b7f-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-syncplicity-tutorial/tutorial_syncplicity_samlbase.png)

3. <span data-ttu-id="97b7f-155">Na powitania **Syncplicity domeny i adres URL** sekcji, wykonaj następujące kroki hello:</span><span class="sxs-lookup"><span data-stu-id="97b7f-155">On hello **Syncplicity Domain and URLs** section, perform hello following steps:</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-syncplicity-tutorial/tutorial_syncplicity_url.png)

    <span data-ttu-id="97b7f-157">a.</span><span class="sxs-lookup"><span data-stu-id="97b7f-157">a.</span></span> <span data-ttu-id="97b7f-158">W hello **adres URL logowania** tekstowym, wpisz adres URL za pomocą hello następującego wzorca:`https://<companyname>.syncplicity.com`</span><span class="sxs-lookup"><span data-stu-id="97b7f-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<companyname>.syncplicity.com`</span></span>

    <span data-ttu-id="97b7f-159">b.</span><span class="sxs-lookup"><span data-stu-id="97b7f-159">b.</span></span> <span data-ttu-id="97b7f-160">W hello **identyfikator** tekstowym, wpisz adres URL za pomocą hello następującego wzorca:`https://<companyname>.syncplicity.com/sp`</span><span class="sxs-lookup"><span data-stu-id="97b7f-160">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<companyname>.syncplicity.com/sp`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="97b7f-161">Wartości te nie są prawdziwe.</span><span class="sxs-lookup"><span data-stu-id="97b7f-161">These values are not real.</span></span> <span data-ttu-id="97b7f-162">Zaktualizować te wartości z hello rzeczywisty adres URL logowania i identyfikator.</span><span class="sxs-lookup"><span data-stu-id="97b7f-162">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="97b7f-163">Skontaktuj się z [zespołem pomocy technicznej klienta Syncplicity](https://www.syncplicity.com/contact-us) tooget tych wartości.</span><span class="sxs-lookup"><span data-stu-id="97b7f-163">Contact [Syncplicity Client support team](https://www.syncplicity.com/contact-us) tooget these values.</span></span> 
 

4. <span data-ttu-id="97b7f-164">Na powitania **certyfikat podpisywania SAML** kliknij **certyfikatu (Base64)** , a następnie zapisz plik certyfikatu hello na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="97b7f-164">On hello **SAML Signing Certificate** section, click **Certificate (Base64)** and then save hello certificate file on your computer.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-syncplicity-tutorial/tutorial_syncplicity_certificate.png) 

  
5. <span data-ttu-id="97b7f-166">Kliknij przycisk **zapisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="97b7f-166">Click **Save** button.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-syncplicity-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="97b7f-168">Na powitania **konfiguracji Syncplicity** kliknij **skonfigurować Syncplicity** tooopen **Konfigurowanie logowania jednokrotnego** okna.</span><span class="sxs-lookup"><span data-stu-id="97b7f-168">On hello **Syncplicity Configuration** section, click **Configure Syncplicity** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="97b7f-169">Kopiuj hello **Sign-Out adres URL, identyfikator jednostki SAML i SAML pojedynczy znak na adres URL usługi** z hello **sekcji krótkimi opisami.**</span><span class="sxs-lookup"><span data-stu-id="97b7f-169">Copy hello **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-syncplicity-tutorial/tutorial_syncplicity_configure.png) 

7. <span data-ttu-id="97b7f-171">Zaloguj się tooyour **Syncplicity** dzierżawy.</span><span class="sxs-lookup"><span data-stu-id="97b7f-171">Sign in tooyour **Syncplicity** tenant.</span></span>

8. <span data-ttu-id="97b7f-172">Hello menu u góry hello, kliknij przycisk **admin**, wybierz pozycję **ustawienia**, a następnie kliknij przycisk **domeny niestandardowe i logowanie jednokrotne**.</span><span class="sxs-lookup"><span data-stu-id="97b7f-172">In hello menu on hello top, click **admin**, select **settings**, and then click **Custom domain and single sign-on**.</span></span>
   
    <span data-ttu-id="97b7f-173">![Syncplicity](./media/active-directory-saas-syncplicity-tutorial/ic769545.png "Syncplicity")</span><span class="sxs-lookup"><span data-stu-id="97b7f-173">![Syncplicity](./media/active-directory-saas-syncplicity-tutorial/ic769545.png "Syncplicity")</span></span>

9. <span data-ttu-id="97b7f-174">Na powitania **pojedynczego logowania jednokrotnego (SSO)** okna dialogowego wykonaj hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="97b7f-174">On hello **Single Sign-On (SSO)** dialog page, perform hello following steps:</span></span>
   
    <span data-ttu-id="97b7f-175">![Logowanie jednokrotne \(logowania jednokrotnego\)](./media/active-directory-saas-syncplicity-tutorial/ic769550.png "Single Sign-On \\\(SSO\\\)")</span><span class="sxs-lookup"><span data-stu-id="97b7f-175">![Single Sign-On \(SSO\)](./media/active-directory-saas-syncplicity-tutorial/ic769550.png "Single Sign-On \\\(SSO\\\)")</span></span>   

    <span data-ttu-id="97b7f-176">a.</span><span class="sxs-lookup"><span data-stu-id="97b7f-176">a.</span></span> <span data-ttu-id="97b7f-177">W hello **domeny niestandardowe** pole tekstowe, typ hello nazwę domeny.</span><span class="sxs-lookup"><span data-stu-id="97b7f-177">In hello **Custom Domain** textbox, type hello name of your domain.</span></span>
  
    <span data-ttu-id="97b7f-178">b.</span><span class="sxs-lookup"><span data-stu-id="97b7f-178">b.</span></span> <span data-ttu-id="97b7f-179">Wybierz **włączone** jako **pojedynczy stan logowania jednokrotnego**.</span><span class="sxs-lookup"><span data-stu-id="97b7f-179">Select **Enabled** as **Single Sign-On Status**.</span></span>

    <span data-ttu-id="97b7f-180">c.</span><span class="sxs-lookup"><span data-stu-id="97b7f-180">c.</span></span> <span data-ttu-id="97b7f-181">W hello **identyfikator jednostki** pole tekstowe, Wklej wartość hello **identyfikator jednostki SAML** którego została skopiowana z portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="97b7f-181">In hello **Entity Id** textbox, Paste hello value of **SAML Entity ID** which you have copied from Azure portal.</span></span>

    <span data-ttu-id="97b7f-182">d.</span><span class="sxs-lookup"><span data-stu-id="97b7f-182">d.</span></span> <span data-ttu-id="97b7f-183">W hello **adres URL logowania strony** pole tekstowe, Wklej hello **SAML pojedynczy znak na adres URL usługi** którego została skopiowana z portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="97b7f-183">In hello **Sign-in page URL** textbox, Paste hello **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span></span>

    <span data-ttu-id="97b7f-184">e.</span><span class="sxs-lookup"><span data-stu-id="97b7f-184">e.</span></span> <span data-ttu-id="97b7f-185">W hello **adres URL strony wylogowania** pole tekstowe, Wklej hello **Sign-Out URL** którego została skopiowana z portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="97b7f-185">In hello **Logout page URL** textbox, Paste hello **Sign-Out URL** which you have copied from Azure portal.</span></span>

    <span data-ttu-id="97b7f-186">f.</span><span class="sxs-lookup"><span data-stu-id="97b7f-186">f.</span></span> <span data-ttu-id="97b7f-187">W **certyfikat dostawcy tożsamości**, kliknij przycisk **wybierz plik**, a następnie przekaż hello certyfikatu, który został pobrany z portalu Azure hello.</span><span class="sxs-lookup"><span data-stu-id="97b7f-187">In **Identity Provider Certificate**, click **Choose file**, and then upload hello certificate which you have downloaded from hello Azure portal.</span></span> 

    <span data-ttu-id="97b7f-188">g.</span><span class="sxs-lookup"><span data-stu-id="97b7f-188">g.</span></span> <span data-ttu-id="97b7f-189">Kliknij przycisk **ZAPISAĆ zmiany**.</span><span class="sxs-lookup"><span data-stu-id="97b7f-189">Click **SAVE CHANGES**.</span></span>

> [!TIP]
> <span data-ttu-id="97b7f-190">Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz hello [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji hello!</span><span class="sxs-lookup"><span data-stu-id="97b7f-190">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="97b7f-191">Po dodaniu tej aplikacji z hello **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij hello **rejestracji jednokrotnej** hello kartę i dostępu do osadzonych dokumentacji za pośrednictwem hello  **Konfiguracja** sekcji u dołu hello.</span><span class="sxs-lookup"><span data-stu-id="97b7f-191">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="97b7f-192">Więcej o hello osadzonych dokumentacji funkcji w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="97b7f-192">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="97b7f-193">Tworzenie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="97b7f-193">Creating an Azure AD test user</span></span>
<span data-ttu-id="97b7f-194">Celem Hello w tej sekcji jest toocreate użytkownika testowego, w portalu Azure o nazwie Simona Britta hello.</span><span class="sxs-lookup"><span data-stu-id="97b7f-194">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Tworzenie użytkowników usługi Azure AD][100]

<span data-ttu-id="97b7f-196">**toocreate użytkownika testowego w usłudze Azure AD, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="97b7f-196">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="97b7f-197">W hello **portalu Azure**na temat hello w lewym okienku nawigacji, kliknij przycisk **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="97b7f-197">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-syncplicity-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="97b7f-199">toodisplay hello listę użytkowników, przejdź zbyt**użytkowników i grup** i kliknij przycisk **wszyscy użytkownicy**.</span><span class="sxs-lookup"><span data-stu-id="97b7f-199">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-syncplicity-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="97b7f-201">Witaj tooopen **użytkownika** okna dialogowego, kliknij przycisk **Dodaj** u góry hello hello okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="97b7f-201">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-syncplicity-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="97b7f-203">Na powitania **użytkownika** okna dialogowego wykonaj hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="97b7f-203">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-syncplicity-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="97b7f-205">a.</span><span class="sxs-lookup"><span data-stu-id="97b7f-205">a.</span></span> <span data-ttu-id="97b7f-206">W hello **nazwa** pole tekstowe, typ **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="97b7f-206">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="97b7f-207">b.</span><span class="sxs-lookup"><span data-stu-id="97b7f-207">b.</span></span> <span data-ttu-id="97b7f-208">W hello **nazwy użytkownika** pole tekstowe, hello typu **adres e-mail** z BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="97b7f-208">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="97b7f-209">c.</span><span class="sxs-lookup"><span data-stu-id="97b7f-209">c.</span></span> <span data-ttu-id="97b7f-210">Wybierz **Pokaż hasło** i zanotuj wartość hello hello **hasło**.</span><span class="sxs-lookup"><span data-stu-id="97b7f-210">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="97b7f-211">d.</span><span class="sxs-lookup"><span data-stu-id="97b7f-211">d.</span></span> <span data-ttu-id="97b7f-212">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="97b7f-212">Click **Create**.</span></span>
 
### <a name="creating-a-syncplicity-test-user"></a><span data-ttu-id="97b7f-213">Tworzenie użytkownika testowego Syncplicity</span><span class="sxs-lookup"><span data-stu-id="97b7f-213">Creating a Syncplicity test user</span></span>
<span data-ttu-id="97b7f-214">AAD użytkowników toobe stanie toosign w muszą być elastycznie tooSyncplicity aplikacji.</span><span class="sxs-lookup"><span data-stu-id="97b7f-214">For AAD users toobe able toosign in, they must be provisioned tooSyncplicity application.</span></span> <span data-ttu-id="97b7f-215">W tej sekcji opisano, jak konta użytkowników usługi AAD toocreate w Syncplicity.</span><span class="sxs-lookup"><span data-stu-id="97b7f-215">This section describes how toocreate AAD user accounts in Syncplicity.</span></span>

<span data-ttu-id="97b7f-216">**tooprovision tooSyncplicity konta użytkownika, należy wykonać hello następujące kroki:**</span><span class="sxs-lookup"><span data-stu-id="97b7f-216">**tooprovision a user account tooSyncplicity, perform hello following steps:**</span></span>

1. <span data-ttu-id="97b7f-217">Zaloguj się za tooyour **Syncplicity** dzierżawy (na przykład: `https://company.Syncplicity.com`).</span><span class="sxs-lookup"><span data-stu-id="97b7f-217">Log in tooyour **Syncplicity** tenant (for example: `https://company.Syncplicity.com`).</span></span>

2. <span data-ttu-id="97b7f-218">Kliknij przycisk **admin** i wybierz **kont użytkowników**.</span><span class="sxs-lookup"><span data-stu-id="97b7f-218">Click **admin** and select **user accounts**.</span></span>

3. <span data-ttu-id="97b7f-219">Kliknij przycisk **dodać użytkownika**.</span><span class="sxs-lookup"><span data-stu-id="97b7f-219">Click **ADD A USER**.</span></span>
   
    <span data-ttu-id="97b7f-220">![Zarządzaj użytkownikami](./media/active-directory-saas-syncplicity-tutorial/ic769764.png "Zarządzanie użytkownikami")</span><span class="sxs-lookup"><span data-stu-id="97b7f-220">![Manage Users](./media/active-directory-saas-syncplicity-tutorial/ic769764.png "Manage Users")</span></span>

4. <span data-ttu-id="97b7f-221">Hello typu **ruch E-mail** konta usługi AAD ma tooprovision, wybierz opcję **użytkownika** jako **roli**, a następnie kliknij przycisk **dalej**.</span><span class="sxs-lookup"><span data-stu-id="97b7f-221">Type hello **Email addressess** of an AAD account you want tooprovision, select **User** as **Role**, and then click **NEXT**.</span></span>
   
    <span data-ttu-id="97b7f-222">![Informacji o koncie](./media/active-directory-saas-syncplicity-tutorial/ic769765.png "informacji o koncie")</span><span class="sxs-lookup"><span data-stu-id="97b7f-222">![Account Information](./media/active-directory-saas-syncplicity-tutorial/ic769765.png "Account Information")</span></span>
   
    >[!NOTE]
    ><span data-ttu-id="97b7f-223">Właściciel konta usługi AAD Hello pobiera wiadomość e-mail, w tym tooconfirm łącza i aktywować hello konta.</span><span class="sxs-lookup"><span data-stu-id="97b7f-223">hello AAD account holder  gets an email including a link tooconfirm and activate hello account.</span></span> 
    > 

5. <span data-ttu-id="97b7f-224">Wybierz grupę w Twojej firmie, nowy użytkownik powinien członkiem, a następnie kliknij przycisk **dalej**.</span><span class="sxs-lookup"><span data-stu-id="97b7f-224">Select a group in your company that your new user should become a member of, and then click **NEXT**.</span></span>
   
    <span data-ttu-id="97b7f-225">![Członkostwa w grupie](./media/active-directory-saas-syncplicity-tutorial/ic769772.png "członkostwa grupy")</span><span class="sxs-lookup"><span data-stu-id="97b7f-225">![Group Membership](./media/active-directory-saas-syncplicity-tutorial/ic769772.png "Group Membership")</span></span>
   
    >[!NOTE]
    ><span data-ttu-id="97b7f-226">Jeśli nie ma żadnych grup, na liście, kliknij przycisk **dalej**.</span><span class="sxs-lookup"><span data-stu-id="97b7f-226">If there are no groups listed, click **NEXT**.</span></span> 
    > 

6. <span data-ttu-id="97b7f-227">Wybierz foldery hello czy tooplace pod kontrolą firmy Syncplicity na komputerze użytkownika hello, takich jak, a następnie kliknij przycisk **dalej**.</span><span class="sxs-lookup"><span data-stu-id="97b7f-227">Select hello folders you would like tooplace under Syncplicity’s control on hello user’s computer, and then click **NEXT**.</span></span>
   
    <span data-ttu-id="97b7f-228">![Foldery Syncplicity](./media/active-directory-saas-syncplicity-tutorial/ic769773.png "Syncplicity folderów")</span><span class="sxs-lookup"><span data-stu-id="97b7f-228">![Syncplicity Folders](./media/active-directory-saas-syncplicity-tutorial/ic769773.png "Syncplicity Folders")</span></span>

>[!NOTE]
><span data-ttu-id="97b7f-229">Możesz użyć innych Syncplicity użytkownika konta tworzenia narzędzi lub interfejsów API dostarczonych przez Syncplicity tooprovision kont użytkowników usługi AAD.</span><span class="sxs-lookup"><span data-stu-id="97b7f-229">You can use any other Syncplicity user account creation tools or APIs provided by Syncplicity tooprovision AAD user accounts.</span></span> 

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="97b7f-230">Przypisanie użytkownika testowego hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="97b7f-230">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="97b7f-231">W tej sekcji możesz włączyć toouse Simona Britta Azure logowania jednokrotnego za udzielanie dostępu tooSyncplicity.</span><span class="sxs-lookup"><span data-stu-id="97b7f-231">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooSyncplicity.</span></span>

![Przypisz użytkownika][200] 

<span data-ttu-id="97b7f-233">**tooassign tooSyncplicity Simona Britta wykonaj hello następujące kroki:**</span><span class="sxs-lookup"><span data-stu-id="97b7f-233">**tooassign Britta Simon tooSyncplicity, perform hello following steps:**</span></span>

1. <span data-ttu-id="97b7f-234">W portalu Azure hello, otwórz widok aplikacji hello, a następnie przejdź do widoku katalogu toohello i przejść za**aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="97b7f-234">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Przypisz użytkownika][201] 

2. <span data-ttu-id="97b7f-236">Z listy aplikacji hello wybierz **Syncplicity**.</span><span class="sxs-lookup"><span data-stu-id="97b7f-236">In hello applications list, select **Syncplicity**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-syncplicity-tutorial/tutorial_syncplicity_app.png) 

3. <span data-ttu-id="97b7f-238">W menu powitania po lewej stronie powitania kliknij **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="97b7f-238">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Przypisz użytkownika][202] 

4. <span data-ttu-id="97b7f-240">Kliknij przycisk **Dodaj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="97b7f-240">Click **Add** button.</span></span> <span data-ttu-id="97b7f-241">Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="97b7f-241">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Przypisz użytkownika][203]

5. <span data-ttu-id="97b7f-243">Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** hello listy użytkowników.</span><span class="sxs-lookup"><span data-stu-id="97b7f-243">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="97b7f-244">Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="97b7f-244">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="97b7f-245">Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="97b7f-245">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="97b7f-246">Testowanie rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="97b7f-246">Testing single sign-on</span></span>

<span data-ttu-id="97b7f-247">Celem Hello w tej sekcji jest tootest użyciu usługi Azure AD konfiguracji rejestracji jednokrotnej hello panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="97b7f-247">hello objective of this section is tootest your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="97b7f-248">Po kliknięciu kafelka Syncplicity hello w hello Panel dostępu, należy pobrać automatycznie zalogowane tooyour Syncplicity aplikacji.</span><span class="sxs-lookup"><span data-stu-id="97b7f-248">When you click hello Syncplicity tile in hello Access Panel, you should get automatically signed-on tooyour Syncplicity application.</span></span>
## <a name="additional-resources"></a><span data-ttu-id="97b7f-249">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="97b7f-249">Additional resources</span></span>

* [<span data-ttu-id="97b7f-250">Lista samouczków dotyczących tooIntegrate aplikacji SaaS w usłudze Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="97b7f-250">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="97b7f-251">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="97b7f-251">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-syncplicity-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-syncplicity-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-syncplicity-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-syncplicity-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-syncplicity-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-syncplicity-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-syncplicity-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-syncplicity-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-syncplicity-tutorial/tutorial_general_203.png

