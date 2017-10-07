---
title: 'Samouczek: Integracji Azure Active Directory z Jobscience | Dokumentacja firmy Microsoft'
description: "Dowiedz się, jak tooconfigure logowanie jednokrotne między usługą Azure Active Directory i Jobscience."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 77282dcc-bbe2-4728-953d-adb4ab6a713b
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: jeedes
ms.openlocfilehash: 4a4c78aad6d324795a15a9569542afc23b4716d1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-jobscience"></a><span data-ttu-id="4b293-103">Samouczek: Integracji Azure Active Directory z Jobscience</span><span class="sxs-lookup"><span data-stu-id="4b293-103">Tutorial: Azure Active Directory integration with Jobscience</span></span>

<span data-ttu-id="4b293-104">Z tego samouczka, dowiesz się, jak toointegrate Jobscience w usłudze Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="4b293-104">In this tutorial, you learn how toointegrate Jobscience with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="4b293-105">Integracja z usługą Azure AD Jobscience zapewnia hello następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="4b293-105">Integrating Jobscience with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="4b293-106">Można kontrolować w usłudze Azure AD, kto ma dostęp do tooJobscience</span><span class="sxs-lookup"><span data-stu-id="4b293-106">You can control in Azure AD who has access tooJobscience</span></span>
- <span data-ttu-id="4b293-107">Można włączyć użytkownika użytkownicy tooautomatically get zalogowane tooJobscience (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="4b293-107">You can enable your users tooautomatically get signed-on tooJobscience (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="4b293-108">Możesz zarządzać kont w jednej centralnej lokalizacji - hello portalu Azure</span><span class="sxs-lookup"><span data-stu-id="4b293-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="4b293-109">Jeśli chcesz tooknow więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="4b293-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="4b293-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="4b293-110">Prerequisites</span></span>

<span data-ttu-id="4b293-111">tooconfigure integracji z usługą Azure AD z Jobscience należy hello następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="4b293-111">tooconfigure Azure AD integration with Jobscience, you need hello following items:</span></span>

- <span data-ttu-id="4b293-112">Subskrypcję usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="4b293-112">An Azure AD subscription</span></span>
- <span data-ttu-id="4b293-113">Jobscience logowanie jednokrotne włączone subskrypcji</span><span class="sxs-lookup"><span data-stu-id="4b293-113">A Jobscience single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="4b293-114">tootest hello kroków w tym samouczku, zaleca się przy użyciu środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="4b293-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="4b293-115">tootest hello kroki opisane w tym samouczku, należy stosować te zalecenia:</span><span class="sxs-lookup"><span data-stu-id="4b293-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="4b293-116">Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="4b293-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="4b293-117">Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz pobrać miesięczna wersja próbna tutaj: [oferta wersji próbnej](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="4b293-117">If you don't have an Azure AD trial environment, you can get a one-month trial here: [Trial offer](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="4b293-118">Opis scenariusza</span><span class="sxs-lookup"><span data-stu-id="4b293-118">Scenario description</span></span>
<span data-ttu-id="4b293-119">W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym.</span><span class="sxs-lookup"><span data-stu-id="4b293-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="4b293-120">Scenariusz Hello opisane w tym samouczku składa się z dwóch głównych elementów:</span><span class="sxs-lookup"><span data-stu-id="4b293-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="4b293-121">Dodawanie Jobscience z galerii hello</span><span class="sxs-lookup"><span data-stu-id="4b293-121">Adding Jobscience from hello gallery</span></span>
2. <span data-ttu-id="4b293-122">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="4b293-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-jobscience-from-hello-gallery"></a><span data-ttu-id="4b293-123">Dodawanie Jobscience z galerii hello</span><span class="sxs-lookup"><span data-stu-id="4b293-123">Adding Jobscience from hello gallery</span></span>
<span data-ttu-id="4b293-124">tooconfigure hello integracji Jobscience do usługi Azure AD, należy tooadd Jobscience z hello galerii tooyour listę zarządzanych aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="4b293-124">tooconfigure hello integration of Jobscience into Azure AD, you need tooadd Jobscience from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="4b293-125">**tooadd Jobscience z galerii hello, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="4b293-125">**tooadd Jobscience from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="4b293-126">W hello  **[portalu Azure](https://portal.azure.com)**na temat hello panelu nawigacji po lewej stronie, kliknij przycisk **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="4b293-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Usługa Active Directory][1]

2. <span data-ttu-id="4b293-128">Przejdź za**aplikacje dla przedsiębiorstw**.</span><span class="sxs-lookup"><span data-stu-id="4b293-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="4b293-129">Następnie przejdź zbyt**wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="4b293-129">Then go too**All applications**.</span></span>

    ![Aplikacje][2]
    
3. <span data-ttu-id="4b293-131">tooadd nową aplikację, kliknij przycisk **nowej aplikacji** przycisk u góry hello okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="4b293-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplikacje][3]

4. <span data-ttu-id="4b293-133">W polu wyszukiwania hello wpisz **Jobscience**.</span><span class="sxs-lookup"><span data-stu-id="4b293-133">In hello search box, type **Jobscience**.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-jobscience-tutorial/tutorial_jobscience_search.png)

5. <span data-ttu-id="4b293-135">W panelu wyników hello zaznacz **Jobscience**, a następnie kliknij przycisk **Dodaj** przycisk aplikacji hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="4b293-135">In hello results panel, select **Jobscience**, and then click **Add** button tooadd hello application.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-jobscience-tutorial/tutorial_jobscience_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="4b293-137">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="4b293-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="4b293-138">W tej sekcji możesz skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z Jobscience na podstawie użytkownika testowego, nazywany "Britta Simona".</span><span class="sxs-lookup"><span data-stu-id="4b293-138">In this section, you configure and test Azure AD single sign-on with Jobscience based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="4b293-139">Dla pojedynczego logowania jednokrotnego toowork usługi Azure AD musi tooknow użytkownika odpowiednikiem hello w Jobscience jest tooa użytkownika w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="4b293-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Jobscience is tooa user in Azure AD.</span></span> <span data-ttu-id="4b293-140">Innymi słowy relację łącza między użytkownika usługi Azure AD i hello użytkownikowi w Jobscience musi toobe ustanowione.</span><span class="sxs-lookup"><span data-stu-id="4b293-140">In other words, a link relationship between an Azure AD user and hello related user in Jobscience needs toobe established.</span></span>

<span data-ttu-id="4b293-141">W Jobscience, należy przypisać wartość hello hello **nazwy użytkownika** w usłudze Azure AD jako wartość hello hello **Username** tooestablish hello łącze relacji.</span><span class="sxs-lookup"><span data-stu-id="4b293-141">In Jobscience, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="4b293-142">tooconfigure i testowych usługi Azure AD rejestracji jednokrotnej z Jobscience, należy po bloków konstrukcyjnych hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="4b293-142">tooconfigure and test Azure AD single sign-on with Jobscience, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="4b293-143">**[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configuring-azure-ad-single-sign-on)**  -tooenable Twojego toouse użytkowników tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="4b293-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="4b293-144">**[Tworzenie użytkownika testowego usługi Azure AD](#creating-an-azure-ad-test-user)**  -tootest usługi Azure AD rejestracji jednokrotnej z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="4b293-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="4b293-145">**[Tworzenie użytkownika testowego Jobscience](#creating-a-jobscience-test-user)**  -toohave odpowiednikiem Simona Britta w Jobscience, który jest połączony toohello usługi Azure AD reprezentację użytkownika.</span><span class="sxs-lookup"><span data-stu-id="4b293-145">**[Creating a Jobscience test user](#creating-a-jobscience-test-user)** - toohave a counterpart of Britta Simon in Jobscience that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="4b293-146">**[Przypisanie użytkownika testowego hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Simona Britta toouse usługi Azure AD rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="4b293-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="4b293-147">**[Testowanie rejestracji jednokrotnej](#testing-single-sign-on)**  -tooverify czy hello konfiguracji działania.</span><span class="sxs-lookup"><span data-stu-id="4b293-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="4b293-148">Konfigurowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="4b293-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="4b293-149">W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w portalu Azure hello i skonfigurować logowanie jednokrotne w aplikacji Jobscience.</span><span class="sxs-lookup"><span data-stu-id="4b293-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Jobscience application.</span></span>

<span data-ttu-id="4b293-150">**tooconfigure usługi Azure AD rejestracji jednokrotnej z Jobscience, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="4b293-150">**tooconfigure Azure AD single sign-on with Jobscience, perform hello following steps:**</span></span>

1. <span data-ttu-id="4b293-151">W portalu Azure na powitania hello **Jobscience** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.</span><span class="sxs-lookup"><span data-stu-id="4b293-151">In hello Azure portal, on hello **Jobscience** application integration page, click **Single sign-on**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej][4]

2. <span data-ttu-id="4b293-153">Na powitania **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** tooenable rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="4b293-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-jobscience-tutorial/tutorial_jobscience_samlbase.png)

3. <span data-ttu-id="4b293-155">Na powitania **Jobscience domeny i adres URL** sekcji, wykonaj następujące kroki hello:</span><span class="sxs-lookup"><span data-stu-id="4b293-155">On hello **Jobscience Domain and URLs** section, perform hello following steps:</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-jobscience-tutorial/tutorial_jobscience_url.png)

    <span data-ttu-id="4b293-157">W hello **adres URL logowania** tekstowym, wpisz adres URL za pomocą hello następującego wzorca:`http://<company name>.my.salesforce.com`</span><span class="sxs-lookup"><span data-stu-id="4b293-157">In hello **Sign-on URL** textbox, type a URL using hello following pattern:  `http://<company name>.my.salesforce.com`</span></span>
    
    > [!NOTE] 
    > <span data-ttu-id="4b293-158">Ta wartość nie jest prawdziwe.</span><span class="sxs-lookup"><span data-stu-id="4b293-158">This value is not real.</span></span> <span data-ttu-id="4b293-159">Zaktualizuj tę wartość z hello rzeczywisty adres URL logowania.</span><span class="sxs-lookup"><span data-stu-id="4b293-159">Update this value with hello actual Sign-On URL.</span></span> <span data-ttu-id="4b293-160">Uzyskać tę wartość za pomocą [zespołem pomocy technicznej klienta Jobscience](https://www.jobscience.com/support) lub z profilu rejestracji Jednokrotnej hello zostanie utworzona, który znajduje się w dalszej części samouczka hello.</span><span class="sxs-lookup"><span data-stu-id="4b293-160">Get this value by [Jobscience Client support team](https://www.jobscience.com/support) or from hello SSO profile you will create which is explained later in hello tutorial.</span></span> 
 
4. <span data-ttu-id="4b293-161">Na powitania **certyfikat podpisywania SAML** kliknij **certyfikatu (Base64)** , a następnie zapisz plik certyfikatu hello na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="4b293-161">On hello **SAML Signing Certificate** section, click **Certificate (Base64)** and then save hello certificate file on your computer.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-jobscience-tutorial/tutorial_jobscience_certificate.png) 

5. <span data-ttu-id="4b293-163">Kliknij przycisk **zapisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="4b293-163">Click **Save** button.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-jobscience-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="4b293-165">Na powitania **konfiguracji Jobscience** kliknij **skonfigurować Jobscience** tooopen **Konfigurowanie logowania jednokrotnego** okna.</span><span class="sxs-lookup"><span data-stu-id="4b293-165">On hello **Jobscience Configuration** section, click **Configure Jobscience** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="4b293-166">Kopiuj hello **Sign-Out adres URL, identyfikator jednostki SAML i SAML pojedynczy znak na adres URL usługi** z hello **sekcji krótkimi opisami.**</span><span class="sxs-lookup"><span data-stu-id="4b293-166">Copy hello **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-jobscience-tutorial/tutorial_jobscience_configure.png) 

7. <span data-ttu-id="4b293-168">Zaloguj się za tooyour Jobscience witryny firmy jako administrator.</span><span class="sxs-lookup"><span data-stu-id="4b293-168">Log in tooyour Jobscience company site as an administrator.</span></span>

8. <span data-ttu-id="4b293-169">Przejdź za**Instalatora**.</span><span class="sxs-lookup"><span data-stu-id="4b293-169">Go too**Setup**.</span></span>
   
   <span data-ttu-id="4b293-170">![Instalator](./media/active-directory-saas-jobscience-tutorial/IC784358.png "Instalatora")</span><span class="sxs-lookup"><span data-stu-id="4b293-170">![Setup](./media/active-directory-saas-jobscience-tutorial/IC784358.png "Setup")</span></span>

9. <span data-ttu-id="4b293-171">W okienku nawigacji po lewej stronie powitania w hello **Administruj** , kliknij przycisk **Zarządzanie domenami** tooexpand hello powiązanych sekcji, a następnie kliknij przycisk **Moje domeny** tooopen hello  **Mojej domeny** strony.</span><span class="sxs-lookup"><span data-stu-id="4b293-171">On hello left navigation pane, in hello **Administer** section, click **Domain Management** tooexpand hello related section, and then click **My Domain** tooopen hello **My Domain** page.</span></span> 
   
   <span data-ttu-id="4b293-172">![Mojej domeny](./media/active-directory-saas-jobscience-tutorial/ic767825.png "mojej domeny")</span><span class="sxs-lookup"><span data-stu-id="4b293-172">![My Domain](./media/active-directory-saas-jobscience-tutorial/ic767825.png "My Domain")</span></span>

10. <span data-ttu-id="4b293-173">tooverify, który domeny nie został skonfigurowany prawidłowo, upewnij się, że jest on "**krok 4 wdrożone tooUsers**" i zapoznaj się z "**Moje ustawienia domeny**".</span><span class="sxs-lookup"><span data-stu-id="4b293-173">tooverify that your domain has been set up correctly, make sure that it is in “**Step 4 Deployed tooUsers**” and review your “**My Domain Settings**”.</span></span>

    <span data-ttu-id="4b293-174">![Domeny wdrożono tooUser](./media/active-directory-saas-jobscience-tutorial/ic784377.png "tooUser wdrożone domeny")</span><span class="sxs-lookup"><span data-stu-id="4b293-174">![Domain Deployed tooUser](./media/active-directory-saas-jobscience-tutorial/ic784377.png "Domain Deployed tooUser")</span></span>

11. <span data-ttu-id="4b293-175">W witrynie hello Jobscience firmy, kliknij przycisk **kontroli bezpieczeństwa**, a następnie kliknij przycisk **ustawień rejestracji jednokrotnej**.</span><span class="sxs-lookup"><span data-stu-id="4b293-175">On hello Jobscience company site, click **Security Controls**, and then click **Single Sign-On Settings**.</span></span>
    
    <span data-ttu-id="4b293-176">![Opcje zabezpieczeń](./media/active-directory-saas-jobscience-tutorial/ic784364.png "środki zabezpieczające.")</span><span class="sxs-lookup"><span data-stu-id="4b293-176">![Security Controls](./media/active-directory-saas-jobscience-tutorial/ic784364.png "Security Controls")</span></span>

12. <span data-ttu-id="4b293-177">W hello **ustawień rejestracji jednokrotnej** sekcji, wykonaj następujące kroki hello:</span><span class="sxs-lookup"><span data-stu-id="4b293-177">In hello **Single Sign-On Settings** section, perform hello following steps:</span></span>
    
    <span data-ttu-id="4b293-178">![Single Sign-On ustawienia](./media/active-directory-saas-jobscience-tutorial/ic781026.png "Single Sign-On ustawienia")</span><span class="sxs-lookup"><span data-stu-id="4b293-178">![Single Sign-On Settings](./media/active-directory-saas-jobscience-tutorial/ic781026.png "Single Sign-On Settings")</span></span>
    
    <span data-ttu-id="4b293-179">a.</span><span class="sxs-lookup"><span data-stu-id="4b293-179">a.</span></span> <span data-ttu-id="4b293-180">Wybierz **SAML włączone**.</span><span class="sxs-lookup"><span data-stu-id="4b293-180">Select **SAML Enabled**.</span></span>

    <span data-ttu-id="4b293-181">b.</span><span class="sxs-lookup"><span data-stu-id="4b293-181">b.</span></span> <span data-ttu-id="4b293-182">Kliknij przycisk **Nowy**.</span><span class="sxs-lookup"><span data-stu-id="4b293-182">Click **New**.</span></span>

13. <span data-ttu-id="4b293-183">Na powitania **SAML pojedynczego logowania jednokrotnego ustawienie Edytuj** okna dialogowego, wykonaj następujące kroki hello:</span><span class="sxs-lookup"><span data-stu-id="4b293-183">On hello **SAML Single Sign-On Setting Edit** dialog, perform hello following steps:</span></span>
    
    <span data-ttu-id="4b293-184">![SAML pojedynczy znak na ustawienie](./media/active-directory-saas-jobscience-tutorial/ic784365.png "SAML pojedynczy znak na ustawienie")</span><span class="sxs-lookup"><span data-stu-id="4b293-184">![SAML Single Sign-On Setting](./media/active-directory-saas-jobscience-tutorial/ic784365.png "SAML Single Sign-On Setting")</span></span>
    
    <span data-ttu-id="4b293-185">a.</span><span class="sxs-lookup"><span data-stu-id="4b293-185">a.</span></span> <span data-ttu-id="4b293-186">W hello **nazwa** tekstowym, wpisz nazwę dla danej konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="4b293-186">In hello **Name** textbox, type a name for your configuration.</span></span>

    <span data-ttu-id="4b293-187">b.</span><span class="sxs-lookup"><span data-stu-id="4b293-187">b.</span></span> <span data-ttu-id="4b293-188">W **wystawcy** pole tekstowe, Wklej wartość hello **identyfikator jednostki SAML**, które zostały skopiowane z portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="4b293-188">In **Issuer** textbox, paste hello value of **SAML Entity ID**, which you have copied from Azure portal.</span></span>

    <span data-ttu-id="4b293-189">c.</span><span class="sxs-lookup"><span data-stu-id="4b293-189">c.</span></span> <span data-ttu-id="4b293-190">W hello **identyfikator jednostki** pole tekstowe, typ`https://salesforce-jobscience.com`</span><span class="sxs-lookup"><span data-stu-id="4b293-190">In hello **Entity Id** textbox, type `https://salesforce-jobscience.com`</span></span>

    <span data-ttu-id="4b293-191">d.</span><span class="sxs-lookup"><span data-stu-id="4b293-191">d.</span></span> <span data-ttu-id="4b293-192">Kliknij przycisk **Przeglądaj** tooupload certyfikat usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="4b293-192">Click **Browse** tooupload your Azure AD certificate.</span></span>

    <span data-ttu-id="4b293-193">e.</span><span class="sxs-lookup"><span data-stu-id="4b293-193">e.</span></span> <span data-ttu-id="4b293-194">Jako **typ tożsamości SAML**, wybierz pozycję **potwierdzenia zawiera hello identyfikator federacyjnej z obiektu użytkownika hello**.</span><span class="sxs-lookup"><span data-stu-id="4b293-194">As **SAML Identity Type**, select **Assertion contains hello Federation ID from hello User object**.</span></span>

    <span data-ttu-id="4b293-195">f.</span><span class="sxs-lookup"><span data-stu-id="4b293-195">f.</span></span> <span data-ttu-id="4b293-196">Jako **lokalizacji tożsamości SAML**, wybierz pozycję **jest tożsamość w elemencie NameIdentfier hello hello instrukcji podmiotu**.</span><span class="sxs-lookup"><span data-stu-id="4b293-196">As **SAML Identity Location**, select **Identity is in hello NameIdentfier element of hello Subject statement**.</span></span>

    <span data-ttu-id="4b293-197">g.</span><span class="sxs-lookup"><span data-stu-id="4b293-197">g.</span></span> <span data-ttu-id="4b293-198">W **adresu URL logowania do dostawcy tożsamości** pole tekstowe, Wklej wartość hello **SAML pojedynczy znak na adres URL usługi**, które zostały skopiowane z portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="4b293-198">In **Identity Provider Login URL** textbox, paste hello value of **SAML Single Sign-On Service URL**, which you have copied from Azure portal.</span></span>

    <span data-ttu-id="4b293-199">h.</span><span class="sxs-lookup"><span data-stu-id="4b293-199">h.</span></span> <span data-ttu-id="4b293-200">W **adres URL wylogowania dostawcy tożsamości** pole tekstowe, Wklej wartość hello **Sign-Out adres URL**, które zostały skopiowane z portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="4b293-200">In **Identity Provider Logout URL** textbox, paste hello value of **Sign-Out URL**, which you have copied from Azure portal.</span></span>

    <span data-ttu-id="4b293-201">i.</span><span class="sxs-lookup"><span data-stu-id="4b293-201">i.</span></span> <span data-ttu-id="4b293-202">Kliknij pozycję **Zapisz**.</span><span class="sxs-lookup"><span data-stu-id="4b293-202">Click **Save**.</span></span>

14. <span data-ttu-id="4b293-203">W okienku nawigacji po lewej stronie powitania w hello **Administruj** , kliknij przycisk **Zarządzanie domenami** tooexpand hello powiązanych sekcji, a następnie kliknij przycisk **Moje domeny** tooopen hello  **Mojej domeny** strony.</span><span class="sxs-lookup"><span data-stu-id="4b293-203">On hello left navigation pane, in hello **Administer** section, click **Domain Management** tooexpand hello related section, and then click **My Domain** tooopen hello **My Domain** page.</span></span> 
    
    <span data-ttu-id="4b293-204">![Mojej domeny](./media/active-directory-saas-jobscience-tutorial/ic767825.png "mojej domeny")</span><span class="sxs-lookup"><span data-stu-id="4b293-204">![My Domain](./media/active-directory-saas-jobscience-tutorial/ic767825.png "My Domain")</span></span>

15. <span data-ttu-id="4b293-205">Na powitania **Moje domeny** strony w hello **znakowanie strony logowania** kliknij **Edytuj**.</span><span class="sxs-lookup"><span data-stu-id="4b293-205">On hello **My Domain** page, in hello **Login Page Branding** section, click **Edit**.</span></span>
    
    <span data-ttu-id="4b293-206">![Znakowanie strony logowania](./media/active-directory-saas-jobscience-tutorial/ic767826.png "znakowanie strony logowania")</span><span class="sxs-lookup"><span data-stu-id="4b293-206">![Login Page Branding](./media/active-directory-saas-jobscience-tutorial/ic767826.png "Login Page Branding")</span></span>

16. <span data-ttu-id="4b293-207">Na powitania **znakowanie strony logowania** strony w hello **usługi uwierzytelniania** sekcji, hello nazwę Twojej **ustawienia logowania jednokrotnego SAML** jest wyświetlany.</span><span class="sxs-lookup"><span data-stu-id="4b293-207">On hello **Login Page Branding** page, in hello **Authentication Service** section, hello name of your **SAML SSO Settings** is displayed.</span></span> <span data-ttu-id="4b293-208">Wybierz go, a następnie kliknij przycisk **zapisać**.</span><span class="sxs-lookup"><span data-stu-id="4b293-208">Select it, and then click **Save**.</span></span>
    
    <span data-ttu-id="4b293-209">![Znakowanie strony logowania](./media/active-directory-saas-jobscience-tutorial/ic784366.png "znakowanie strony logowania")</span><span class="sxs-lookup"><span data-stu-id="4b293-209">![Login Page Branding](./media/active-directory-saas-jobscience-tutorial/ic784366.png "Login Page Branding")</span></span>

17. <span data-ttu-id="4b293-210">tooget hello SP zainicjował jednokrotnego kliknij adres URL logowania na powitania **ustawień rejestracji jednokrotnej** w hello **kontroli bezpieczeństwa** części menu.</span><span class="sxs-lookup"><span data-stu-id="4b293-210">tooget hello SP initiated Single Sign on Login URL click on hello **Single Sign On settings** in hello **Security Controls** menu section.</span></span>

    <span data-ttu-id="4b293-211">![Opcje zabezpieczeń](./media/active-directory-saas-jobscience-tutorial/ic784368.png "środki zabezpieczające.")</span><span class="sxs-lookup"><span data-stu-id="4b293-211">![Security Controls](./media/active-directory-saas-jobscience-tutorial/ic784368.png "Security Controls")</span></span>
    
    <span data-ttu-id="4b293-212">Kliknij profil rejestracji Jednokrotnej hello, utworzony w poprzednim kroku hello.</span><span class="sxs-lookup"><span data-stu-id="4b293-212">Click hello SSO profile you have created in hello step above.</span></span> <span data-ttu-id="4b293-213">Na tej stronie znajduje hello rejestracji jednokrotnej adres URL dla Twojej firmy (na przykład [https://companyname.my.salesforce.com?so=companyid](https://companyname.my.salesforce.com?so=companyid).</span><span class="sxs-lookup"><span data-stu-id="4b293-213">This page shows hello Single Sign on URL for your company (for example, [https://companyname.my.salesforce.com?so=companyid](https://companyname.my.salesforce.com?so=companyid).</span></span>    

> [!TIP]
> <span data-ttu-id="4b293-214">Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz hello [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji hello!</span><span class="sxs-lookup"><span data-stu-id="4b293-214">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="4b293-215">Po dodaniu tej aplikacji z hello **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij hello **rejestracji jednokrotnej** hello kartę i dostępu do osadzonych dokumentacji za pośrednictwem hello  **Konfiguracja** sekcji u dołu hello.</span><span class="sxs-lookup"><span data-stu-id="4b293-215">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="4b293-216">Więcej o hello osadzonych dokumentacji funkcji w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="4b293-216">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="4b293-217">Tworzenie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="4b293-217">Creating an Azure AD test user</span></span>
<span data-ttu-id="4b293-218">Celem Hello w tej sekcji jest toocreate użytkownika testowego, w portalu Azure o nazwie Simona Britta hello.</span><span class="sxs-lookup"><span data-stu-id="4b293-218">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Tworzenie użytkowników usługi Azure AD][100]

<span data-ttu-id="4b293-220">**toocreate użytkownika testowego w usłudze Azure AD, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="4b293-220">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="4b293-221">W hello **portalu Azure**na temat hello w lewym okienku nawigacji, kliknij przycisk **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="4b293-221">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-jobscience-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="4b293-223">toodisplay hello listę użytkowników, przejdź zbyt**użytkowników i grup** i kliknij przycisk **wszyscy użytkownicy**.</span><span class="sxs-lookup"><span data-stu-id="4b293-223">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-jobscience-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="4b293-225">Witaj tooopen **użytkownika** okna dialogowego, kliknij przycisk **Dodaj** u góry hello hello okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="4b293-225">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-jobscience-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="4b293-227">Na powitania **użytkownika** okna dialogowego wykonaj hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="4b293-227">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-jobscience-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="4b293-229">a.</span><span class="sxs-lookup"><span data-stu-id="4b293-229">a.</span></span> <span data-ttu-id="4b293-230">W hello **nazwa** pole tekstowe, typ **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="4b293-230">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="4b293-231">b.</span><span class="sxs-lookup"><span data-stu-id="4b293-231">b.</span></span> <span data-ttu-id="4b293-232">W hello **nazwy użytkownika** pole tekstowe, hello typu **adres e-mail** z BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="4b293-232">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="4b293-233">c.</span><span class="sxs-lookup"><span data-stu-id="4b293-233">c.</span></span> <span data-ttu-id="4b293-234">Wybierz **Pokaż hasło** i zanotuj wartość hello hello **hasło**.</span><span class="sxs-lookup"><span data-stu-id="4b293-234">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="4b293-235">d.</span><span class="sxs-lookup"><span data-stu-id="4b293-235">d.</span></span> <span data-ttu-id="4b293-236">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="4b293-236">Click **Create**.</span></span>
 
### <a name="creating-a-jobscience-test-user"></a><span data-ttu-id="4b293-237">Tworzenie użytkownika testowego Jobscience</span><span class="sxs-lookup"><span data-stu-id="4b293-237">Creating a Jobscience test user</span></span>

<span data-ttu-id="4b293-238">W przypadku użytkowników usługi Azure AD toolog kolejności tooenable w tooJobscience muszą mieć przydzielone do Jobscience.</span><span class="sxs-lookup"><span data-stu-id="4b293-238">In order tooenable Azure AD users toolog in tooJobscience, they must be provisioned into Jobscience.</span></span> <span data-ttu-id="4b293-239">W przypadku hello Jobscience Inicjowanie obsługi to zadanie ręczne.</span><span class="sxs-lookup"><span data-stu-id="4b293-239">In hello case of Jobscience, provisioning is a manual task.</span></span>

>[!NOTE]
><span data-ttu-id="4b293-240">Możesz użyć innych Jobscience użytkownika konta tworzenia narzędzi lub interfejsów API dostarczonych przez tooprovision Jobscience usługi Azure Active Directory kont użytkowników.</span><span class="sxs-lookup"><span data-stu-id="4b293-240">You can use any other Jobscience user account creation tools or APIs provided by Jobscience tooprovision Azure Active Directory user accounts.</span></span>
>  
        
<span data-ttu-id="4b293-241">**tooconfigure aprowizacji użytkowników, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="4b293-241">**tooconfigure user provisioning, perform hello following steps:**</span></span>

1. <span data-ttu-id="4b293-242">Zaloguj się za tooyour **Jobscience** witryny firmy jako administrator.</span><span class="sxs-lookup"><span data-stu-id="4b293-242">Log in tooyour **Jobscience** company site as administrator.</span></span>

2. <span data-ttu-id="4b293-243">Przejdź tooSetup.</span><span class="sxs-lookup"><span data-stu-id="4b293-243">Go tooSetup.</span></span>
   
   <span data-ttu-id="4b293-244">![Instalator](./media/active-directory-saas-jobscience-tutorial/ic784358.png "Instalatora")</span><span class="sxs-lookup"><span data-stu-id="4b293-244">![Setup](./media/active-directory-saas-jobscience-tutorial/ic784358.png "Setup")</span></span>
3. <span data-ttu-id="4b293-245">Przejdź za**Zarządzanie użytkownikami \> użytkowników**.</span><span class="sxs-lookup"><span data-stu-id="4b293-245">Go too**Manage Users \> Users**.</span></span>
   
   <span data-ttu-id="4b293-246">![Użytkownicy](./media/active-directory-saas-jobscience-tutorial/ic784369.png "użytkowników")</span><span class="sxs-lookup"><span data-stu-id="4b293-246">![Users](./media/active-directory-saas-jobscience-tutorial/ic784369.png "Users")</span></span>
4. <span data-ttu-id="4b293-247">Kliknij przycisk **nowego użytkownika**.</span><span class="sxs-lookup"><span data-stu-id="4b293-247">Click **New User**.</span></span>
   
   <span data-ttu-id="4b293-248">![Wszyscy użytkownicy](./media/active-directory-saas-jobscience-tutorial/ic784370.png "wszyscy użytkownicy")</span><span class="sxs-lookup"><span data-stu-id="4b293-248">![All Users](./media/active-directory-saas-jobscience-tutorial/ic784370.png "All Users")</span></span>
5. <span data-ttu-id="4b293-249">Na powitania **Edytowanie użytkownika** okna dialogowego, wykonaj następujące kroki hello:</span><span class="sxs-lookup"><span data-stu-id="4b293-249">On hello **Edit User** dialog, perform hello following steps:</span></span>
   
   <span data-ttu-id="4b293-250">![Edycja użytkownika](./media/active-directory-saas-jobscience-tutorial/ic784371.png "Edycja użytkownika")</span><span class="sxs-lookup"><span data-stu-id="4b293-250">![User Edit](./media/active-directory-saas-jobscience-tutorial/ic784371.png "User Edit")</span></span>
   
   <span data-ttu-id="4b293-251">a.</span><span class="sxs-lookup"><span data-stu-id="4b293-251">a.</span></span> <span data-ttu-id="4b293-252">W hello **imię** tekstowym, wpisz imię użytkownika hello, takich jak Britta.</span><span class="sxs-lookup"><span data-stu-id="4b293-252">In hello **First Name** textbox, type a first name of hello user like Britta.</span></span>
   
   <span data-ttu-id="4b293-253">b.</span><span class="sxs-lookup"><span data-stu-id="4b293-253">b.</span></span> <span data-ttu-id="4b293-254">W hello **nazwisko** tekstowym, wpisz nazwisko użytkownika hello, takich jak Simona.</span><span class="sxs-lookup"><span data-stu-id="4b293-254">In hello **Last Name** textbox, type a last name of hello user like Simon.</span></span>
   
   <span data-ttu-id="4b293-255">c.</span><span class="sxs-lookup"><span data-stu-id="4b293-255">c.</span></span> <span data-ttu-id="4b293-256">W hello **Alias** tekstowym, wpisz nazwę aliasu hello użytkownika, takich jak brittas.</span><span class="sxs-lookup"><span data-stu-id="4b293-256">In hello **Alias** textbox, type an alias name of hello user like brittas.</span></span>

   <span data-ttu-id="4b293-257">d.</span><span class="sxs-lookup"><span data-stu-id="4b293-257">d.</span></span> <span data-ttu-id="4b293-258">W hello **E-mail** pole tekstowe, typ hello adres e-mail użytkownika, takich jak Brittasimon@contoso.com.</span><span class="sxs-lookup"><span data-stu-id="4b293-258">In hello **Email** textbox, type hello email address of user like Brittasimon@contoso.com.</span></span>

   <span data-ttu-id="4b293-259">e.</span><span class="sxs-lookup"><span data-stu-id="4b293-259">e.</span></span> <span data-ttu-id="4b293-260">W hello **nazwy użytkownika** tekstowym, wpisz nazwę użytkownika użytkownika, takich jak Brittasimon@contoso.com.</span><span class="sxs-lookup"><span data-stu-id="4b293-260">In hello **User Name** textbox, type a user name of user like Brittasimon@contoso.com.</span></span>

   <span data-ttu-id="4b293-261">f.</span><span class="sxs-lookup"><span data-stu-id="4b293-261">f.</span></span> <span data-ttu-id="4b293-262">W hello **pseudonim** tekstowym, wpisz nazwę użytkownika, takich jak Simona nick.</span><span class="sxs-lookup"><span data-stu-id="4b293-262">In hello **Nick Name** textbox, type a nick name of user like Simon.</span></span>

   <span data-ttu-id="4b293-263">g.</span><span class="sxs-lookup"><span data-stu-id="4b293-263">g.</span></span> <span data-ttu-id="4b293-264">Kliknij pozycję **Zapisz**.</span><span class="sxs-lookup"><span data-stu-id="4b293-264">Click **Save**.</span></span>

    
> [!NOTE]
> <span data-ttu-id="4b293-265">Właściciel konta usługi Azure Active Directory Hello otrzymuje wiadomość e-mail i następuje tooconfirm łącze swojego konta, zanim staje się aktywny.</span><span class="sxs-lookup"><span data-stu-id="4b293-265">hello Azure Active Directory account holder receives an email and follows a link tooconfirm their account before it becomes active.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="4b293-266">Przypisanie użytkownika testowego hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="4b293-266">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="4b293-267">W tej sekcji możesz włączyć toouse Simona Britta Azure logowania jednokrotnego za udzielanie dostępu tooJobscience.</span><span class="sxs-lookup"><span data-stu-id="4b293-267">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooJobscience.</span></span>

![Przypisz użytkownika][200] 

<span data-ttu-id="4b293-269">**tooassign tooJobscience Simona Britta wykonaj hello następujące kroki:**</span><span class="sxs-lookup"><span data-stu-id="4b293-269">**tooassign Britta Simon tooJobscience, perform hello following steps:**</span></span>

1. <span data-ttu-id="4b293-270">W portalu Azure hello, otwórz widok aplikacji hello, a następnie przejdź do widoku katalogu toohello i przejść za**aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="4b293-270">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Przypisz użytkownika][201] 

2. <span data-ttu-id="4b293-272">Z listy aplikacji hello wybierz **Jobscience**.</span><span class="sxs-lookup"><span data-stu-id="4b293-272">In hello applications list, select **Jobscience**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-jobscience-tutorial/tutorial_jobscience_app.png) 

3. <span data-ttu-id="4b293-274">W menu powitania po lewej stronie powitania kliknij **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="4b293-274">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Przypisz użytkownika][202] 

4. <span data-ttu-id="4b293-276">Kliknij przycisk **Dodaj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="4b293-276">Click **Add** button.</span></span> <span data-ttu-id="4b293-277">Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="4b293-277">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Przypisz użytkownika][203]

5. <span data-ttu-id="4b293-279">Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** hello listy użytkowników.</span><span class="sxs-lookup"><span data-stu-id="4b293-279">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="4b293-280">Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="4b293-280">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="4b293-281">Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="4b293-281">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="4b293-282">Testowanie rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="4b293-282">Testing single sign-on</span></span>

<span data-ttu-id="4b293-283">W tej sekcji można przetestować konfiguracji usługi Azure AD pojedynczego logowania jednokrotnego przy użyciu hello panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="4b293-283">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="4b293-284">Po kliknięciu kafelka Jobscience hello w hello Panel dostępu, należy pobrać automatycznie zalogowane tooyour Jobscience aplikacji.</span><span class="sxs-lookup"><span data-stu-id="4b293-284">When you click hello Jobscience tile in hello Access Panel, you should get automatically signed-on tooyour Jobscience application.</span></span>
<span data-ttu-id="4b293-285">Aby uzyskać więcej informacji na temat hello Panel dostępu, zobacz [toohello wprowadzenie panelu dostępu](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="4b293-285">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="4b293-286">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="4b293-286">Additional resources</span></span>

* [<span data-ttu-id="4b293-287">Lista samouczków dotyczących tooIntegrate aplikacji SaaS w usłudze Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="4b293-287">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="4b293-288">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="4b293-288">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-jobscience-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-jobscience-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-jobscience-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-jobscience-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-jobscience-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-jobscience-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-jobscience-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-jobscience-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-jobscience-tutorial/tutorial_general_203.png

