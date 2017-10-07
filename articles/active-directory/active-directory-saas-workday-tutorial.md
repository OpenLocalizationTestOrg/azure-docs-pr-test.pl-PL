---
title: 'Samouczek: Azure Active Directory integracji z produktem Workday | Dokumentacja firmy Microsoft'
description: "Dowiedz się, jak tooconfigure logowanie jednokrotne między usługą Azure Active Directory i dzień roboczy."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: e9da692e-4a65-4231-8ab3-bc9a87b10bca
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: jeedes
ms.openlocfilehash: aaa41e372e45f464c4540a70fc79c98dbc06d6b4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-workday"></a><span data-ttu-id="ddb71-103">Samouczek: Azure Active Directory integracji z produktem Workday</span><span class="sxs-lookup"><span data-stu-id="ddb71-103">Tutorial: Azure Active Directory integration with Workday</span></span>

<span data-ttu-id="ddb71-104">Z tego samouczka, dowiesz się, jak toointegrate produktu Workday w usłudze Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="ddb71-104">In this tutorial, you learn how toointegrate Workday with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="ddb71-105">Integrowanie pracy z usługą Azure AD zapewnia hello następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="ddb71-105">Integrating Workday with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="ddb71-106">Można kontrolować w usłudze Azure AD, kto ma dostęp do tooWorkday</span><span class="sxs-lookup"><span data-stu-id="ddb71-106">You can control in Azure AD who has access tooWorkday</span></span>
- <span data-ttu-id="ddb71-107">Można włączyć użytkownika użytkownicy tooautomatically get zalogowane tooWorkday (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="ddb71-107">You can enable your users tooautomatically get signed-on tooWorkday (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="ddb71-108">Możesz zarządzać kont w jednej centralnej lokalizacji - hello portalu Azure</span><span class="sxs-lookup"><span data-stu-id="ddb71-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="ddb71-109">Jeśli chcesz tooknow więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="ddb71-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ddb71-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="ddb71-110">Prerequisites</span></span>

<span data-ttu-id="ddb71-111">tooconfigure integracji z usługą Azure AD z produktem Workday, należy hello następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="ddb71-111">tooconfigure Azure AD integration with Workday, you need hello following items:</span></span>

- <span data-ttu-id="ddb71-112">Subskrypcję usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="ddb71-112">An Azure AD subscription</span></span>
- <span data-ttu-id="ddb71-113">Produktu Workday jednokrotnego włączone subskrypcji</span><span class="sxs-lookup"><span data-stu-id="ddb71-113">A Workday single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="ddb71-114">tootest hello kroków w tym samouczku, zaleca się przy użyciu środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="ddb71-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="ddb71-115">tootest hello kroki opisane w tym samouczku, należy stosować te zalecenia:</span><span class="sxs-lookup"><span data-stu-id="ddb71-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="ddb71-116">Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="ddb71-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="ddb71-117">Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz pobrać miesięczna wersja próbna [tutaj](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="ddb71-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="ddb71-118">Opis scenariusza</span><span class="sxs-lookup"><span data-stu-id="ddb71-118">Scenario description</span></span>
<span data-ttu-id="ddb71-119">W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym.</span><span class="sxs-lookup"><span data-stu-id="ddb71-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="ddb71-120">Scenariusz Hello opisane w tym samouczku składa się z dwóch głównych elementów:</span><span class="sxs-lookup"><span data-stu-id="ddb71-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="ddb71-121">Dodawanie produktu Workday z galerii hello</span><span class="sxs-lookup"><span data-stu-id="ddb71-121">Adding Workday from hello gallery</span></span>
2. <span data-ttu-id="ddb71-122">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="ddb71-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-workday-from-hello-gallery"></a><span data-ttu-id="ddb71-123">Dodawanie produktu Workday z galerii hello</span><span class="sxs-lookup"><span data-stu-id="ddb71-123">Adding Workday from hello gallery</span></span>
<span data-ttu-id="ddb71-124">tooconfigure hello integracji z produktem Workday do usługi Azure AD, należy tooadd produktu Workday z hello galerii tooyour listę zarządzanych aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="ddb71-124">tooconfigure hello integration of Workday into Azure AD, you need tooadd Workday from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="ddb71-125">**tooadd produktu Workday z galerii hello wykonaj hello następujące kroki:**</span><span class="sxs-lookup"><span data-stu-id="ddb71-125">**tooadd Workday from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="ddb71-126">W hello  **[portalu Azure](https://portal.azure.com)**na temat hello panelu nawigacji po lewej stronie, kliknij przycisk **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="ddb71-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Usługa Active Directory][1]

2. <span data-ttu-id="ddb71-128">Przejdź za**aplikacje dla przedsiębiorstw**.</span><span class="sxs-lookup"><span data-stu-id="ddb71-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="ddb71-129">Następnie przejdź zbyt**wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="ddb71-129">Then go too**All applications**.</span></span>

    ![Aplikacje][2]
    
3. <span data-ttu-id="ddb71-131">tooadd nową aplikację, kliknij przycisk **nowej aplikacji** przycisk u góry hello okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="ddb71-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplikacje][3]

4. <span data-ttu-id="ddb71-133">W polu wyszukiwania hello wpisz **produktu Workday**.</span><span class="sxs-lookup"><span data-stu-id="ddb71-133">In hello search box, type **Workday**.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-workday-tutorial/tutorial_workday_search.png)

5. <span data-ttu-id="ddb71-135">W panelu wyników hello zaznacz **produktu Workday**, a następnie kliknij przycisk **Dodaj** przycisk aplikacji hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="ddb71-135">In hello results panel, select **Workday**, and then click **Add** button tooadd hello application.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-workday-tutorial/tutorial_workday_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="ddb71-137">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="ddb71-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="ddb71-138">W tej sekcji możesz skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z produktu Workday oparte na koncie użytkownika testu o nazwie "Britta Simona".</span><span class="sxs-lookup"><span data-stu-id="ddb71-138">In this section, you configure and test Azure AD single sign-on with Workday based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="ddb71-139">Dla pojedynczego logowania jednokrotnego toowork usługi Azure AD musi tooknow użytkownika odpowiednikiem hello w produktu Workday jest tooa użytkownika w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="ddb71-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Workday is tooa user in Azure AD.</span></span> <span data-ttu-id="ddb71-140">Innymi słowy relację łącza między użytkownika usługi Azure AD i hello użytkownikowi w pracy musi toobe ustanowione.</span><span class="sxs-lookup"><span data-stu-id="ddb71-140">In other words, a link relationship between an Azure AD user and hello related user in Workday needs toobe established.</span></span>

<span data-ttu-id="ddb71-141">Ta relacja łącza zostanie nawiązane, przypisując wartość hello hello **nazwy użytkownika** w usłudze Azure AD jako wartość hello hello **Username** w pracy.</span><span class="sxs-lookup"><span data-stu-id="ddb71-141">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in Workday.</span></span>

<span data-ttu-id="ddb71-142">tooconfigure i testowych usługi Azure AD rejestracji jednokrotnej z produktem Workday, należy po bloków konstrukcyjnych hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="ddb71-142">tooconfigure and test Azure AD single sign-on with Workday, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="ddb71-143">**[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configuring-azure-ad-single-sign-on)**  -tooenable Twojego toouse użytkowników tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="ddb71-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="ddb71-144">**[Tworzenie użytkownika testowego usługi Azure AD](#creating-an-azure-ad-test-user)**  -tootest usługi Azure AD rejestracji jednokrotnej z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="ddb71-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="ddb71-145">**[Tworzenie użytkownika testowego produktu Workday](#creating-a-workday-test-user)**  -toohave odpowiednikiem Simona Britta w pracy, który jest połączony toohello usługi Azure AD reprezentację użytkownika.</span><span class="sxs-lookup"><span data-stu-id="ddb71-145">**[Creating a Workday test user](#creating-a-workday-test-user)** - toohave a counterpart of Britta Simon in Workday that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="ddb71-146">**[Przypisanie użytkownika testowego hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Simona Britta toouse usługi Azure AD rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="ddb71-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="ddb71-147">**[Testowanie rejestracji jednokrotnej](#testing-single-sign-on)**  -tooverify czy hello konfiguracji działania.</span><span class="sxs-lookup"><span data-stu-id="ddb71-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="ddb71-148">Konfigurowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="ddb71-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="ddb71-149">W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w hello portalu Azure i skonfigurować logowanie jednokrotne w aplikacji produktu Workday.</span><span class="sxs-lookup"><span data-stu-id="ddb71-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Workday application.</span></span>

<span data-ttu-id="ddb71-150">**tooconfigure usługi Azure AD rejestracji jednokrotnej z produktem Workday, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="ddb71-150">**tooconfigure Azure AD single sign-on with Workday, perform hello following steps:**</span></span>

1. <span data-ttu-id="ddb71-151">W portalu Azure na powitania hello **produktu Workday** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.</span><span class="sxs-lookup"><span data-stu-id="ddb71-151">In hello Azure portal, on hello **Workday** application integration page, click **Single sign-on**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej][4]

2. <span data-ttu-id="ddb71-153">Na powitania **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** tooenable rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="ddb71-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-workday-tutorial/tutorial_workday_samlbase.png)

3. <span data-ttu-id="ddb71-155">Na powitania **produktu Workday domeny i adres URL** sekcji, wykonaj następujące kroki hello:</span><span class="sxs-lookup"><span data-stu-id="ddb71-155">On hello **Workday Domain and URLs** section, perform hello following steps:</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-workday-tutorial/tutorial_workday_url.png)

    <span data-ttu-id="ddb71-157">a.</span><span class="sxs-lookup"><span data-stu-id="ddb71-157">a.</span></span> <span data-ttu-id="ddb71-158">W hello **adres URL logowania** pole tekstowe, wartość hello typu jako:`https://impl.workday.com/<tenant>/login-saml2.htmld`</span><span class="sxs-lookup"><span data-stu-id="ddb71-158">In hello **Sign-on URL** textbox, type hello value as: `https://impl.workday.com/<tenant>/login-saml2.htmld`</span></span>

    <span data-ttu-id="ddb71-159">b.</span><span class="sxs-lookup"><span data-stu-id="ddb71-159">b.</span></span> <span data-ttu-id="ddb71-160">W hello **adres URL odpowiedzi** tekstowym, wpisz adres URL za pomocą hello następującego wzorca:`https://impl.workday.com/<tenant>/login-saml.htmld`</span><span class="sxs-lookup"><span data-stu-id="ddb71-160">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://impl.workday.com/<tenant>/login-saml.htmld`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="ddb71-161">Wartości te nie są hello prawdziwe.</span><span class="sxs-lookup"><span data-stu-id="ddb71-161">These values are not hello real.</span></span> <span data-ttu-id="ddb71-162">Witaj rzeczywisty adres URL logowania i adres URL odpowiedzi, należy zaktualizować te wartości.</span><span class="sxs-lookup"><span data-stu-id="ddb71-162">Update these values with hello actual Sign-on URL and Reply URL.</span></span> <span data-ttu-id="ddb71-163">Adres URL odpowiedzi muszą mieć poddomeny na przykład: www, wd2, wd3, wd3 impl, wd5, wd5 impl).</span><span class="sxs-lookup"><span data-stu-id="ddb71-163">Your reply URL must have a subdomain for example: www, wd2, wd3, wd3-impl, wd5, wd5-impl).</span></span> <span data-ttu-id="ddb71-164">Przy użyciu przypominać "*http://www.myworkday.com*" działa, ale "*http://myworkday.com*" nie ma.</span><span class="sxs-lookup"><span data-stu-id="ddb71-164">Using something like "*http://www.myworkday.com*" works but "*http://myworkday.com*" does not.</span></span> <span data-ttu-id="ddb71-165">Skontaktuj się z [zespołem pomocy technicznej klienta produktu Workday](https://www.workday.com/en-us/partners-services/services/support.html) tooget tych wartości.</span><span class="sxs-lookup"><span data-stu-id="ddb71-165">Contact [Workday Client support team](https://www.workday.com/en-us/partners-services/services/support.html) tooget these values.</span></span> 
 

4. <span data-ttu-id="ddb71-166">Na powitania **certyfikat podpisywania SAML** kliknij **certyfikatu (Base64)** , a następnie zapisz plik certyfikatu hello na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="ddb71-166">On hello **SAML Signing Certificate** section, click **Certificate (Base64)** and then save hello certificate file on your computer.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-workday-tutorial/tutorial_workday_certificate.png) 

5. <span data-ttu-id="ddb71-168">Kliknij przycisk **zapisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="ddb71-168">Click **Save** button.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-workday-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="ddb71-170">Na powitania **konfiguracji produktu Workday** kliknij **Konfigurowanie produktu Workday** tooopen **Konfigurowanie logowania jednokrotnego** okna.</span><span class="sxs-lookup"><span data-stu-id="ddb71-170">On hello **Workday Configuration** section, click **Configure Workday** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="ddb71-171">Kopiuj hello **Sign-Out adres URL, identyfikator jednostki SAML i SAML pojedynczy znak na adres URL usługi** z hello **sekcji krótkimi opisami.**</span><span class="sxs-lookup"><span data-stu-id="ddb71-171">Copy hello **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    <span data-ttu-id="ddb71-172">![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-workday-tutorial/tutorial_workday_configure.png) 
<CS></span><span class="sxs-lookup"><span data-stu-id="ddb71-172">![Configure Single Sign-On](./media/active-directory-saas-workday-tutorial/tutorial_workday_configure.png) 
<CS></span></span>
7. <span data-ttu-id="ddb71-173">W oknie przeglądarki innej witryny sieci web Zaloguj się w witrynie firmy produktu Workday tooyour jako administrator.</span><span class="sxs-lookup"><span data-stu-id="ddb71-173">In a different web browser window, log in tooyour Workday company site as an administrator.</span></span>

8. <span data-ttu-id="ddb71-174">Przejdź za**Menu \> Workbench**.</span><span class="sxs-lookup"><span data-stu-id="ddb71-174">Go too**Menu \> Workbench**.</span></span>
   
    <span data-ttu-id="ddb71-175">![Workbench](./media/active-directory-saas-workday-tutorial/IC782923.png "Workbench")</span><span class="sxs-lookup"><span data-stu-id="ddb71-175">![Workbench](./media/active-directory-saas-workday-tutorial/IC782923.png "Workbench")</span></span>

9. <span data-ttu-id="ddb71-176">Przejdź za**administrowania kontami**.</span><span class="sxs-lookup"><span data-stu-id="ddb71-176">Go too**Account Administration**.</span></span>
   
    <span data-ttu-id="ddb71-177">![Konto administracji](./media/active-directory-saas-workday-tutorial/IC782924.png "konta administracji")</span><span class="sxs-lookup"><span data-stu-id="ddb71-177">![Account Administration](./media/active-directory-saas-workday-tutorial/IC782924.png "Account Administration")</span></span>

10. <span data-ttu-id="ddb71-178">Przejdź za**Edytuj ustawienia dzierżawy — zabezpieczeń**.</span><span class="sxs-lookup"><span data-stu-id="ddb71-178">Go too**Edit Tenant Setup – Security**.</span></span>
   
    <span data-ttu-id="ddb71-179">![Edytuj zabezpieczenia dzierżawy](./media/active-directory-saas-workday-tutorial/IC782925.png "Edytuj zabezpieczenia dzierżawy")</span><span class="sxs-lookup"><span data-stu-id="ddb71-179">![Edit Tenant Security](./media/active-directory-saas-workday-tutorial/IC782925.png "Edit Tenant Security")</span></span>

11. <span data-ttu-id="ddb71-180">W hello **adresów URL przekierowań** sekcji, wykonaj następujące kroki hello:</span><span class="sxs-lookup"><span data-stu-id="ddb71-180">In hello **Redirection URLs** section, perform hello following steps:</span></span>
   
    <span data-ttu-id="ddb71-181">![Adresy URL przekierowania](./media/active-directory-saas-workday-tutorial/IC7829581.png "adresów URL przekierowań")</span><span class="sxs-lookup"><span data-stu-id="ddb71-181">![Redirection URLs](./media/active-directory-saas-workday-tutorial/IC7829581.png "Redirection URLs")</span></span>
   
    <span data-ttu-id="ddb71-182">a.</span><span class="sxs-lookup"><span data-stu-id="ddb71-182">a.</span></span> <span data-ttu-id="ddb71-183">Kliknij przycisk **Dodaj wiersz**.</span><span class="sxs-lookup"><span data-stu-id="ddb71-183">Click **Add Row**.</span></span>
   
    <span data-ttu-id="ddb71-184">b.</span><span class="sxs-lookup"><span data-stu-id="ddb71-184">b.</span></span> <span data-ttu-id="ddb71-185">W hello **Przekierowywanie adresu URL logowania do** pole tekstowe i hello **adresem URL przekierowania Mobile** pole tekstowe, hello typu **adres URL logowania** wprowadzono hello **produktu Workday domeny i Adresy URL** sekcji hello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="ddb71-185">In hello **Login Redirect URL** textbox and hello **Mobile Redirect URL** textbox, type hello **Sign-on URL** you have entered on hello **Workday Domain and URLs** section of hello Azure portal.</span></span>
   
    <span data-ttu-id="ddb71-186">c.</span><span class="sxs-lookup"><span data-stu-id="ddb71-186">c.</span></span> <span data-ttu-id="ddb71-187">W portalu Azure na powitania hello **Konfigurowanie logowania jednokrotnego** okna, hello kopii **Sign-Out URL**, a następnie wklej go do hello **adresem URL przekierowania wylogowania** pola tekstowego.</span><span class="sxs-lookup"><span data-stu-id="ddb71-187">In hello Azure portal, on hello **Configure sign-on** window, copy hello **Sign-Out URL**, and then paste it into hello **Logout Redirect URL** textbox.</span></span>
   
    <span data-ttu-id="ddb71-188">d.</span><span class="sxs-lookup"><span data-stu-id="ddb71-188">d.</span></span>  <span data-ttu-id="ddb71-189">W **środowiska** pole tekstowe, nazwa środowiska hello typu.</span><span class="sxs-lookup"><span data-stu-id="ddb71-189">In **Environment** textbox, type hello environment name.</span></span>  

    >[!NOTE]
    > <span data-ttu-id="ddb71-190">Witaj wartość atrybutu środowisko hello jest powiązany adres URL dzierżawy hello toohello wartość:</span><span class="sxs-lookup"><span data-stu-id="ddb71-190">hello value of hello Environment attribute is tied toohello value of hello tenant URL:</span></span>  
    ><span data-ttu-id="ddb71-191">— Czy nazwa domeny hello adres URL dzierżawy produktu Workday hello rozpoczyna się od impl na przykład: *https://impl.workday.com/\<dzierżawy\>/login-saml2.htmld*), hello **środowiska** Atrybut musi być ustawiona tooImplementation.</span><span class="sxs-lookup"><span data-stu-id="ddb71-191">-If hello domain name of hello Workday tenant URL starts with impl for example: *https://impl.workday.com/\<tenant\>/login-saml2.htmld*), hello **Environment** attribute must be set tooImplementation.</span></span>  
    ><span data-ttu-id="ddb71-192">— Jeśli hello nazwy domeny rozpoczynają się od czegoś innego, należy toocontact [zespołem pomocy technicznej klienta produktu Workday](https://www.workday.com/en-us/partners-services/services/support.html) dopasowania hello tooget **środowiska** wartość.</span><span class="sxs-lookup"><span data-stu-id="ddb71-192">-If hello domain name starts with something else, you need toocontact [Workday Client support team](https://www.workday.com/en-us/partners-services/services/support.html) tooget hello matching **Environment** value.</span></span>

12. <span data-ttu-id="ddb71-193">W hello **Instalatora SAML** sekcji, wykonaj następujące kroki hello:</span><span class="sxs-lookup"><span data-stu-id="ddb71-193">In hello **SAML Setup** section, perform hello following steps:</span></span>
   
    <span data-ttu-id="ddb71-194">![Instalator SAML](./media/active-directory-saas-workday-tutorial/IC782926.png "Instalatora SAML")</span><span class="sxs-lookup"><span data-stu-id="ddb71-194">![SAML Setup](./media/active-directory-saas-workday-tutorial/IC782926.png "SAML Setup")</span></span>
   
    <span data-ttu-id="ddb71-195">a.</span><span class="sxs-lookup"><span data-stu-id="ddb71-195">a.</span></span>  <span data-ttu-id="ddb71-196">Wybierz **włączyć uwierzytelnianie SAML**.</span><span class="sxs-lookup"><span data-stu-id="ddb71-196">Select **Enable SAML Authentication**.</span></span>
   
    <span data-ttu-id="ddb71-197">b.</span><span class="sxs-lookup"><span data-stu-id="ddb71-197">b.</span></span>  <span data-ttu-id="ddb71-198">Kliknij przycisk **Dodaj wiersz**.</span><span class="sxs-lookup"><span data-stu-id="ddb71-198">Click **Add Row**.</span></span>

13. <span data-ttu-id="ddb71-199">W sekcji dostawców tożsamości SAML hello wykonaj hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="ddb71-199">In hello SAML Identity Providers section, perform hello following steps:</span></span>
   
    <span data-ttu-id="ddb71-200">![Dostawców tożsamości SAML](./media/active-directory-saas-workday-tutorial/IC7829271.png "dostawców tożsamości SAML")</span><span class="sxs-lookup"><span data-stu-id="ddb71-200">![SAML Identity Providers](./media/active-directory-saas-workday-tutorial/IC7829271.png "SAML Identity Providers")</span></span>
   
    <span data-ttu-id="ddb71-201">a.</span><span class="sxs-lookup"><span data-stu-id="ddb71-201">a.</span></span> <span data-ttu-id="ddb71-202">W polu tekstowym Nazwa dostawcy tożsamości hello, wpisz nazwę dostawcy (na przykład: *SPInitiatedSSO*).</span><span class="sxs-lookup"><span data-stu-id="ddb71-202">In hello Identity Provider Name textbox, type a provider name (for example: *SPInitiatedSSO*).</span></span>
   
    <span data-ttu-id="ddb71-203">b.</span><span class="sxs-lookup"><span data-stu-id="ddb71-203">b.</span></span> <span data-ttu-id="ddb71-204">W portalu Azure na powitania hello **Konfigurowanie logowania jednokrotnego** okna, hello kopiowania **identyfikator jednostki SAML** wartość, a następnie wklej go do hello **wystawcy** pola tekstowego.</span><span class="sxs-lookup"><span data-stu-id="ddb71-204">In hello Azure portal, on hello **Configure sign-on** window, copy hello **SAML Entity ID** value, and then paste it into hello **Issuer** textbox.</span></span>
   
    <span data-ttu-id="ddb71-205">c.</span><span class="sxs-lookup"><span data-stu-id="ddb71-205">c.</span></span> <span data-ttu-id="ddb71-206">Wybierz **włączyć Workday wylogowania inicjowane**.</span><span class="sxs-lookup"><span data-stu-id="ddb71-206">Select **Enable Workday Initiated Logout**.</span></span>
   
    <span data-ttu-id="ddb71-207">d.</span><span class="sxs-lookup"><span data-stu-id="ddb71-207">d.</span></span> <span data-ttu-id="ddb71-208">W portalu Azure na powitania hello **Konfigurowanie logowania jednokrotnego** okna, hello kopiowania **Sign-Out URL** wartość, a następnie wklej go do hello **adresu URL wylogowania żądania** pola tekstowego.</span><span class="sxs-lookup"><span data-stu-id="ddb71-208">In hello Azure portal, on hello **Configure sign-on** window, copy hello **Sign-Out URL** value, and then paste it into hello **Logout Request URL** textbox.</span></span>

    <span data-ttu-id="ddb71-209">e.</span><span class="sxs-lookup"><span data-stu-id="ddb71-209">e.</span></span> <span data-ttu-id="ddb71-210">Kliknij przycisk **certyfikatu klucza publicznego dostawcy tożsamości**, a następnie kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="ddb71-210">Click **Identity Provider Public Key Certificate**, and then click **Create**.</span></span> 

    <span data-ttu-id="ddb71-211">![Utwórz](./media/active-directory-saas-workday-tutorial/IC782928.png "tworzenie")</span><span class="sxs-lookup"><span data-stu-id="ddb71-211">![Create](./media/active-directory-saas-workday-tutorial/IC782928.png "Create")</span></span>

    <span data-ttu-id="ddb71-212">f.</span><span class="sxs-lookup"><span data-stu-id="ddb71-212">f.</span></span> <span data-ttu-id="ddb71-213">Kliknij przycisk **x509 Utwórz klucz publiczny**.</span><span class="sxs-lookup"><span data-stu-id="ddb71-213">Click **Create x509 Public Key**.</span></span> 

    <span data-ttu-id="ddb71-214">![Utwórz](./media/active-directory-saas-workday-tutorial/IC782929.png "tworzenie")</span><span class="sxs-lookup"><span data-stu-id="ddb71-214">![Create](./media/active-directory-saas-workday-tutorial/IC782929.png "Create")</span></span>


14. <span data-ttu-id="ddb71-215">W hello **klucza publicznego widoku x509** sekcji, wykonaj następujące kroki hello:</span><span class="sxs-lookup"><span data-stu-id="ddb71-215">In hello **View x509 Public Key** section, perform hello following steps:</span></span> 
   
    <span data-ttu-id="ddb71-216">![Klucz publiczny widoku x509](./media/active-directory-saas-workday-tutorial/IC782930.png "widoku x509 klucza publicznego")</span><span class="sxs-lookup"><span data-stu-id="ddb71-216">![View x509 Public Key](./media/active-directory-saas-workday-tutorial/IC782930.png "View x509 Public Key")</span></span> 
   
    <span data-ttu-id="ddb71-217">a.</span><span class="sxs-lookup"><span data-stu-id="ddb71-217">a.</span></span> <span data-ttu-id="ddb71-218">W hello **nazwa** tekstowym, wpisz nazwę dla certyfikatu (na przykład: *ŚOI\_SP*).</span><span class="sxs-lookup"><span data-stu-id="ddb71-218">In hello **Name** textbox, type a name for your certificate (for example: *PPE\_SP*).</span></span>
   
    <span data-ttu-id="ddb71-219">b.</span><span class="sxs-lookup"><span data-stu-id="ddb71-219">b.</span></span> <span data-ttu-id="ddb71-220">W hello **ważny od** pole tekstowe, typ hello ważny od wartości atrybutu certyfikatu.</span><span class="sxs-lookup"><span data-stu-id="ddb71-220">In hello **Valid From** textbox, type hello valid from attribute value of your certificate.</span></span>
   
    <span data-ttu-id="ddb71-221">c.</span><span class="sxs-lookup"><span data-stu-id="ddb71-221">c.</span></span>  <span data-ttu-id="ddb71-222">W hello **ważny do** pole tekstowe, wartość prawidłowy tooattribute hello typu certyfikatu.</span><span class="sxs-lookup"><span data-stu-id="ddb71-222">In hello **Valid To** textbox, type hello valid tooattribute value of your certificate.</span></span>
   
    > [!NOTE]
    > <span data-ttu-id="ddb71-223">Można odczytać hello prawidłową datę i hello prawidłową toodate z hello pobrany certyfikat, kliknij go dwukrotnie.</span><span class="sxs-lookup"><span data-stu-id="ddb71-223">You can get hello valid from date and hello valid toodate from hello downloaded certificate by double-clicking it.</span></span>  <span data-ttu-id="ddb71-224">Witaj daty są wyświetlane w obszarze hello **szczegóły** kartę.</span><span class="sxs-lookup"><span data-stu-id="ddb71-224">hello dates are listed under hello **Details** tab.</span></span>
    > 
    >
   
    <span data-ttu-id="ddb71-225">d.</span><span class="sxs-lookup"><span data-stu-id="ddb71-225">d.</span></span>  <span data-ttu-id="ddb71-226">Otwórz certyfikatu zakodowanego base-64 w Notatniku i hello kopiowania zawartości z niego.</span><span class="sxs-lookup"><span data-stu-id="ddb71-226">Open your base-64 encoded certificate in notepad, and then copy hello content of it.</span></span>
   
    <span data-ttu-id="ddb71-227">e.</span><span class="sxs-lookup"><span data-stu-id="ddb71-227">e.</span></span>  <span data-ttu-id="ddb71-228">W hello **certyfikatu** pole tekstowe, hello Wklej zawartość Schowka.</span><span class="sxs-lookup"><span data-stu-id="ddb71-228">In hello **Certificate** textbox, paste hello content of your clipboard.</span></span>
   
    <span data-ttu-id="ddb71-229">f.</span><span class="sxs-lookup"><span data-stu-id="ddb71-229">f.</span></span>  <span data-ttu-id="ddb71-230">Kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="ddb71-230">Click **OK**.</span></span>

15. <span data-ttu-id="ddb71-231">Wykonaj następujące kroki hello:</span><span class="sxs-lookup"><span data-stu-id="ddb71-231">Perform hello following steps:</span></span> 
   
    <span data-ttu-id="ddb71-232">![Konfiguracja rejestracji Jednokrotnej](./media/active-directory-saas-workday-tutorial/WorkdaySSOConfiguratio.png "konfiguracji logowania jednokrotnego")</span><span class="sxs-lookup"><span data-stu-id="ddb71-232">![SSO configuration](./media/active-directory-saas-workday-tutorial/WorkdaySSOConfiguratio.png "SSO configuration")</span></span>
   
    <span data-ttu-id="ddb71-233">a.</span><span class="sxs-lookup"><span data-stu-id="ddb71-233">a.</span></span>  <span data-ttu-id="ddb71-234">Włącz hello **x509 pary klucza prywatnego**.</span><span class="sxs-lookup"><span data-stu-id="ddb71-234">Enable hello **x509 Private Key Pair**.</span></span>
   
    <span data-ttu-id="ddb71-235">b.</span><span class="sxs-lookup"><span data-stu-id="ddb71-235">b.</span></span>  <span data-ttu-id="ddb71-236">W hello **identyfikator dostawcy usługi** pole tekstowe, typ **http://www.workday.com**.</span><span class="sxs-lookup"><span data-stu-id="ddb71-236">In hello **Service Provider ID** textbox, type **http://www.workday.com**.</span></span>
   
    <span data-ttu-id="ddb71-237">c.</span><span class="sxs-lookup"><span data-stu-id="ddb71-237">c.</span></span>  <span data-ttu-id="ddb71-238">Wybierz **Włącz SP zainicjował uwierzytelnianie SAML**.</span><span class="sxs-lookup"><span data-stu-id="ddb71-238">Select **Enable SP Initiated SAML Authentication**.</span></span>
   
    <span data-ttu-id="ddb71-239">d.</span><span class="sxs-lookup"><span data-stu-id="ddb71-239">d.</span></span>  <span data-ttu-id="ddb71-240">W portalu Azure na powitania hello **Konfigurowanie logowania jednokrotnego** okna, hello kopiowania **SAML pojedynczy znak na adres URL usługi** wartość, a następnie wklej go do hello **adres URL usługi logowania jednokrotnego IdP** pola tekstowego.</span><span class="sxs-lookup"><span data-stu-id="ddb71-240">In hello Azure portal, on hello **Configure sign-on** window, copy hello **SAML Single Sign-On Service URL** value, and then paste it into hello **IdP SSO Service URL** textbox.</span></span>
   
    <span data-ttu-id="ddb71-241">e.</span><span class="sxs-lookup"><span data-stu-id="ddb71-241">e.</span></span> <span data-ttu-id="ddb71-242">Wybierz **nie Deflate żądania uwierzytelnienia zainicjowane SP**.</span><span class="sxs-lookup"><span data-stu-id="ddb71-242">Select **Do Not Deflate SP-initiated Authentication Request**.</span></span>
   
    <span data-ttu-id="ddb71-243">f.</span><span class="sxs-lookup"><span data-stu-id="ddb71-243">f.</span></span> <span data-ttu-id="ddb71-244">Jako **podpisu żądania uwierzytelnienia**, wybierz pozycję **SHA256**.</span><span class="sxs-lookup"><span data-stu-id="ddb71-244">As **Authentication Request Signature Method**, select **SHA256**.</span></span> 
   
    <span data-ttu-id="ddb71-245">![Metoda podpisu żądania uwierzytelniania](./media/active-directory-saas-workday-tutorial/WorkdaySSOConfiguration.png "metoda podpisu żądania uwierzytelniania")</span><span class="sxs-lookup"><span data-stu-id="ddb71-245">![Authentication Request Signature Method](./media/active-directory-saas-workday-tutorial/WorkdaySSOConfiguration.png "Authentication Request Signature Method")</span></span> 
   
    <span data-ttu-id="ddb71-246">g.</span><span class="sxs-lookup"><span data-stu-id="ddb71-246">g.</span></span> <span data-ttu-id="ddb71-247">Kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="ddb71-247">Click **OK**.</span></span> 
   
    <span data-ttu-id="ddb71-248">![OK](./media/active-directory-saas-workday-tutorial/IC782933.png "OK")
<CE></span><span class="sxs-lookup"><span data-stu-id="ddb71-248">![OK](./media/active-directory-saas-workday-tutorial/IC782933.png "OK")
<CE></span></span>

> [!TIP]
> <span data-ttu-id="ddb71-249">Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz hello [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji hello!</span><span class="sxs-lookup"><span data-stu-id="ddb71-249">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="ddb71-250">Po dodaniu tej aplikacji z hello **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij hello **rejestracji jednokrotnej** hello kartę i dostępu do osadzonych dokumentacji za pośrednictwem hello  **Konfiguracja** sekcji u dołu hello.</span><span class="sxs-lookup"><span data-stu-id="ddb71-250">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="ddb71-251">Więcej o hello osadzonych dokumentacji funkcji w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="ddb71-251">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="ddb71-252">Tworzenie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="ddb71-252">Creating an Azure AD test user</span></span>
<span data-ttu-id="ddb71-253">Celem Hello w tej sekcji jest toocreate użytkownika testowego, w portalu Azure o nazwie Simona Britta hello.</span><span class="sxs-lookup"><span data-stu-id="ddb71-253">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Tworzenie użytkowników usługi Azure AD][100]

<span data-ttu-id="ddb71-255">**toocreate użytkownika testowego w usłudze Azure AD, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="ddb71-255">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="ddb71-256">W hello **portalu Azure**na temat hello w lewym okienku nawigacji, kliknij przycisk **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="ddb71-256">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-workday-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="ddb71-258">toodisplay hello listę użytkowników, przejdź zbyt**użytkowników i grup** i kliknij przycisk **wszyscy użytkownicy**.</span><span class="sxs-lookup"><span data-stu-id="ddb71-258">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-workday-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="ddb71-260">Witaj tooopen **użytkownika** okna dialogowego, kliknij przycisk **Dodaj** u góry hello hello okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="ddb71-260">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-workday-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="ddb71-262">Na powitania **użytkownika** okna dialogowego wykonaj hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="ddb71-262">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-workday-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="ddb71-264">a.</span><span class="sxs-lookup"><span data-stu-id="ddb71-264">a.</span></span> <span data-ttu-id="ddb71-265">W hello **nazwa** pole tekstowe, typ **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="ddb71-265">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="ddb71-266">b.</span><span class="sxs-lookup"><span data-stu-id="ddb71-266">b.</span></span> <span data-ttu-id="ddb71-267">W hello **nazwy użytkownika** pole tekstowe, hello typu **adres e-mail** z BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="ddb71-267">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="ddb71-268">c.</span><span class="sxs-lookup"><span data-stu-id="ddb71-268">c.</span></span> <span data-ttu-id="ddb71-269">Wybierz **Pokaż hasło** i zanotuj wartość hello hello **hasło**.</span><span class="sxs-lookup"><span data-stu-id="ddb71-269">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="ddb71-270">d.</span><span class="sxs-lookup"><span data-stu-id="ddb71-270">d.</span></span> <span data-ttu-id="ddb71-271">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="ddb71-271">Click **Create**.</span></span>
 
### <a name="creating-a-workday-test-user"></a><span data-ttu-id="ddb71-272">Tworzenie użytkownika testowego produktu Workday</span><span class="sxs-lookup"><span data-stu-id="ddb71-272">Creating a Workday test user</span></span>

<span data-ttu-id="ddb71-273">tooget użytkownika testowego udostępnione do produktu Workday należy toocontact hello [zespołem pomocy technicznej klienta produktu Workday](https://www.workday.com/en-us/partners-services/services/support.html).</span><span class="sxs-lookup"><span data-stu-id="ddb71-273">tooget a test user provisioned into Workday, you need toocontact hello [Workday Client support team](https://www.workday.com/en-us/partners-services/services/support.html).</span></span>
<span data-ttu-id="ddb71-274">Witaj [zespołem pomocy technicznej klienta produktu Workday](https://www.workday.com/en-us/partners-services/services/support.html) tworzy hello użytkownika.</span><span class="sxs-lookup"><span data-stu-id="ddb71-274">hello [Workday Client support team](https://www.workday.com/en-us/partners-services/services/support.html) creates hello user for you.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="ddb71-275">Przypisanie użytkownika testowego hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="ddb71-275">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="ddb71-276">W tej sekcji możesz włączyć toouse Simona Britta Azure logowania jednokrotnego za udzielanie dostępu tooWorkday.</span><span class="sxs-lookup"><span data-stu-id="ddb71-276">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooWorkday.</span></span>

![Przypisz użytkownika][200] 

<span data-ttu-id="ddb71-278">**tooassign tooWorkday Simona Britta wykonaj hello następujące kroki:**</span><span class="sxs-lookup"><span data-stu-id="ddb71-278">**tooassign Britta Simon tooWorkday, perform hello following steps:**</span></span>

1. <span data-ttu-id="ddb71-279">W portalu Azure hello, otwórz widok aplikacji hello, a następnie przejdź do widoku katalogu toohello i przejść za**aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="ddb71-279">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Przypisz użytkownika][201] 

2. <span data-ttu-id="ddb71-281">Z listy aplikacji hello wybierz **produktu Workday**.</span><span class="sxs-lookup"><span data-stu-id="ddb71-281">In hello applications list, select **Workday**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-workday-tutorial/tutorial_workday_app.png) 

3. <span data-ttu-id="ddb71-283">W menu powitania po lewej stronie powitania kliknij **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="ddb71-283">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Przypisz użytkownika][202] 

4. <span data-ttu-id="ddb71-285">Kliknij przycisk **Dodaj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="ddb71-285">Click **Add** button.</span></span> <span data-ttu-id="ddb71-286">Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="ddb71-286">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Przypisz użytkownika][203]

5. <span data-ttu-id="ddb71-288">Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** hello listy użytkowników.</span><span class="sxs-lookup"><span data-stu-id="ddb71-288">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="ddb71-289">Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="ddb71-289">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="ddb71-290">Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="ddb71-290">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="ddb71-291">Testowanie rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="ddb71-291">Testing single sign-on</span></span>

<span data-ttu-id="ddb71-292">Jeśli chcesz tootest jednego ustawienia logowania jednokrotnego, otwórz hello panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="ddb71-292">If you want tootest your single sign-on settings, open hello Access Panel.</span></span> <span data-ttu-id="ddb71-293">Aby uzyskać więcej informacji na temat hello Panel dostępu, zobacz [toohello wprowadzenie panelu dostępu](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="ddb71-293">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="ddb71-294">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="ddb71-294">Additional resources</span></span>

* [<span data-ttu-id="ddb71-295">Lista samouczków dotyczących tooIntegrate aplikacji SaaS w usłudze Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="ddb71-295">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="ddb71-296">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="ddb71-296">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)
* [<span data-ttu-id="ddb71-297">Skonfiguruj Inicjowanie obsługi użytkowników</span><span class="sxs-lookup"><span data-stu-id="ddb71-297">Configure User Provisioning</span></span>](active-directory-saas-workday-inbound-tutorial.md)



<!--Image references-->

[1]: ./media/active-directory-saas-workday-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-workday-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-workday-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-workday-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-workday-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-workday-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-workday-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-workday-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-workday-tutorial/tutorial_general_203.png

