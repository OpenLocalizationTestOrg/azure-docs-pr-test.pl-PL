---
title: 'Samouczek: Integracji Azure Active Directory z LinkedInSalesNavigator | Dokumentacja firmy Microsoft'
description: "Dowiedz się, jak tooconfigure logowanie jednokrotne między usługą Azure Active Directory i LinkedInSalesNavigator."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 7a9fa8f3-d611-4ffe-8d50-04e9586b24da
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/14/2017
ms.author: jeedes
ms.openlocfilehash: 443d302d40d7af16aba5114e00963f23ea8d12d6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-linkedin-sales-navigator"></a><span data-ttu-id="b6e62-103">Samouczek: Integracji Azure Active Directory z Nawigatora sprzedaży LinkedIn</span><span class="sxs-lookup"><span data-stu-id="b6e62-103">Tutorial: Azure Active Directory integration with LinkedIn Sales Navigator</span></span>

<span data-ttu-id="b6e62-104">Z tego samouczka, dowiesz się, jak toointegrate LinkedIn Navigator sprzedaży w usłudze Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="b6e62-104">In this tutorial, you learn how toointegrate LinkedIn Sales Navigator with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="b6e62-105">Integrowanie Navigator sprzedaży LinkedIn z usługą Azure AD zapewnia hello następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="b6e62-105">Integrating LinkedIn Sales Navigator with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="b6e62-106">Można kontrolować w usłudze Azure AD, kto ma dostęp tooLinkedIn Nawigator sprzedaży</span><span class="sxs-lookup"><span data-stu-id="b6e62-106">You can control in Azure AD who has access tooLinkedIn Sales Navigator</span></span>
- <span data-ttu-id="b6e62-107">Można włączyć użytkownika użytkownicy tooautomatically get zalogowane tooLinkedIn Nawigator sprzedaży (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="b6e62-107">You can enable your users tooautomatically get signed-on tooLinkedIn Sales Navigator (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="b6e62-108">Możesz zarządzać kont w jednej centralnej lokalizacji - hello portalu Azure</span><span class="sxs-lookup"><span data-stu-id="b6e62-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="b6e62-109">Jeśli chcesz tooknow więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, przeglądać [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="b6e62-109">If you want tooknow more details about SaaS app integration with Azure AD, browse [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b6e62-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="b6e62-110">Prerequisites</span></span>

<span data-ttu-id="b6e62-111">tooconfigure integracji usługi Azure AD z Nawigatora sprzedaży LinkedIn należy hello następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="b6e62-111">tooconfigure Azure AD integration with LinkedIn Sales Navigator, you need hello following items:</span></span>

- <span data-ttu-id="b6e62-112">Subskrypcję usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="b6e62-112">An Azure AD subscription</span></span>
- <span data-ttu-id="b6e62-113">Nawigator sprzedaży LinkedIn jednokrotnego włączone subskrypcji</span><span class="sxs-lookup"><span data-stu-id="b6e62-113">A LinkedIn Sales Navigator single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="b6e62-114">tootest hello kroków w tym samouczku, zaleca się przy użyciu środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="b6e62-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="b6e62-115">tootest hello kroki opisane w tym samouczku, należy stosować te zalecenia:</span><span class="sxs-lookup"><span data-stu-id="b6e62-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="b6e62-116">Unikaj używania środowiska produkcyjnego, jeśli jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="b6e62-116">Avoid using your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="b6e62-117">Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz pobrać miesięczna wersja próbna [tutaj](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="b6e62-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="b6e62-118">Opis scenariusza</span><span class="sxs-lookup"><span data-stu-id="b6e62-118">Scenario description</span></span>
<span data-ttu-id="b6e62-119">W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym.</span><span class="sxs-lookup"><span data-stu-id="b6e62-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="b6e62-120">Scenariusz Hello opisane w tym samouczku składa się z dwóch głównych elementów:</span><span class="sxs-lookup"><span data-stu-id="b6e62-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="b6e62-121">Dodawanie Navigator sprzedaży LinkedIn z galerii hello</span><span class="sxs-lookup"><span data-stu-id="b6e62-121">Adding LinkedIn Sales Navigator from hello gallery</span></span>
2. <span data-ttu-id="b6e62-122">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="b6e62-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-linkedin-sales-navigator-from-hello-gallery"></a><span data-ttu-id="b6e62-123">Dodawanie Navigator sprzedaży LinkedIn z galerii hello</span><span class="sxs-lookup"><span data-stu-id="b6e62-123">Adding LinkedIn Sales Navigator from hello gallery</span></span>
<span data-ttu-id="b6e62-124">tooconfigure hello integracji LinkedIn Nawigator sprzedaży w usłudze Azure Active Directory, należy tooadd Nawigator sprzedaży LinkedIn z hello galerii tooyour listę zarządzanych aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="b6e62-124">tooconfigure hello integration of LinkedIn Sales Navigator into Azure AD, you need tooadd LinkedIn Sales Navigator from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="b6e62-125">**tooadd Nawigator sprzedaży LinkedIn z galerii hello wykonaj hello następujące kroki:**</span><span class="sxs-lookup"><span data-stu-id="b6e62-125">**tooadd LinkedIn Sales Navigator from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="b6e62-126">W hello  **[portalu Azure](https://portal.azure.com)**na temat hello panelu nawigacji po lewej stronie, kliknij przycisk **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="b6e62-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Usługa Active Directory][1]

2. <span data-ttu-id="b6e62-128">Przejdź za**aplikacje dla przedsiębiorstw**.</span><span class="sxs-lookup"><span data-stu-id="b6e62-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="b6e62-129">Następnie przejdź zbyt**wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="b6e62-129">Then go too**All applications**.</span></span>

    ![Aplikacje][2]
    
3. <span data-ttu-id="b6e62-131">Kliknij przycisk **nowej aplikacji** przycisk u góry hello hello okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="b6e62-131">Click **New application** button on hello top of hello dialog.</span></span>

    ![Aplikacje][3]

4. <span data-ttu-id="b6e62-133">W polu wyszukiwania hello wpisz **LinkedIn sprzedaży Navigator**.</span><span class="sxs-lookup"><span data-stu-id="b6e62-133">In hello search box, type **LinkedIn Sales Navigator**.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-linkedinsalesnavigator-tutorial/tutorial_linkedinsalesnavigator_search.png)

5. <span data-ttu-id="b6e62-135">W panelu wyników hello, wybierz **Nawigator sprzedaży LinkedIn**, a następnie kliknij przycisk **Dodaj** przycisk aplikacji hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="b6e62-135">In hello results panel, select **LinkedIn Sales Navigator**, and then click **Add** button tooadd hello application.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-linkedinsalesnavigator-tutorial/tutorial_linkedinsalesnavigator_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="b6e62-137">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="b6e62-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="b6e62-138">W tej sekcji skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z LinkedIn Nawigator sprzedaży w oparciu o nazwie "Britta Simona" użytkownika testowego.</span><span class="sxs-lookup"><span data-stu-id="b6e62-138">In this section, you configure and test Azure AD single sign-on with LinkedIn Sales Navigator based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="b6e62-139">Dla pojedynczego logowania jednokrotnego toowork usługi Azure AD musi tooknow użytkownika odpowiednikiem hello w Nawigatorze sprzedaży LinkedIn jest tooa użytkownika w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="b6e62-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in LinkedIn Sales Navigator is tooa user in Azure AD.</span></span> <span data-ttu-id="b6e62-140">Innymi słowy relację łącza między użytkownika usługi Azure AD i hello użytkownikowi w Nawigatorze sprzedaży LinkedIn musi toobe ustanowione.</span><span class="sxs-lookup"><span data-stu-id="b6e62-140">In other words, a link relationship between an Azure AD user and hello related user in LinkedIn Sales Navigator needs toobe established.</span></span>

<span data-ttu-id="b6e62-141">Ta relacja łącza zostanie nawiązane, przypisując wartość hello hello **nazwy użytkownika** w usłudze Azure AD jako wartość hello hello **Username** w Nawigatorze sprzedaży LinkedIn.</span><span class="sxs-lookup"><span data-stu-id="b6e62-141">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in LinkedIn Sales Navigator.</span></span>

<span data-ttu-id="b6e62-142">tooconfigure i testowych usługi Azure AD rejestracji jednokrotnej z LinkedIn Nawigator sprzedaży, należy po bloków konstrukcyjnych hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="b6e62-142">tooconfigure and test Azure AD single sign-on with LinkedIn Sales Navigator, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="b6e62-143">**[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configuring-azure-ad-single-sign-on)**  -tooenable Twojego toouse użytkowników tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="b6e62-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="b6e62-144">**[Tworzenie użytkownika testowego usługi Azure AD](#creating-an-azure-ad-test-user)**  -tootest usługi Azure AD rejestracji jednokrotnej z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="b6e62-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="b6e62-145">**[Tworzenie użytkownika testowego Navigator sprzedaży LinkedIn](#creating-a-linkedin-sales-navigator-test-user)**  -toohave odpowiednikiem Simona Britta w Nawigatorze sprzedaży LinkedIn, będący toohello połączonej usługi Azure AD reprezentację hello użytkownika.</span><span class="sxs-lookup"><span data-stu-id="b6e62-145">**[Creating a LinkedIn Sales Navigator test user](#creating-a-linkedin-sales-navigator-test-user)** - toohave a counterpart of Britta Simon in LinkedIn Sales Navigator that is linked toohello Azure AD representation of hello user.</span></span>
4. <span data-ttu-id="b6e62-146">**[Przypisanie użytkownika testowego hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Simona Britta toouse usługi Azure AD rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="b6e62-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="b6e62-147">**[Testowanie rejestracji jednokrotnej](#testing-single-sign-on)**  -tooverify czy hello konfiguracji działania.</span><span class="sxs-lookup"><span data-stu-id="b6e62-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="b6e62-148">Konfigurowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="b6e62-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="b6e62-149">W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w portalu Azure hello i skonfigurować rejestracji jednokrotnej w aplikacji LinkedIn sprzedaży nawigatora.</span><span class="sxs-lookup"><span data-stu-id="b6e62-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your LinkedIn Sales Navigator application.</span></span>

<span data-ttu-id="b6e62-150">**tooconfigure usługi Azure AD rejestracji jednokrotnej z LinkedIn Nawigator sprzedaży, wykonaj hello następujące kroki:**</span><span class="sxs-lookup"><span data-stu-id="b6e62-150">**tooconfigure Azure AD single sign-on with LinkedIn Sales Navigator, perform hello following steps:**</span></span>

1. <span data-ttu-id="b6e62-151">W portalu Azure na powitania hello **Nawigator sprzedaży LinkedIn** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.</span><span class="sxs-lookup"><span data-stu-id="b6e62-151">In hello Azure portal, on hello **LinkedIn Sales Navigator** application integration page, click **Single sign-on**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej][4]

2. <span data-ttu-id="b6e62-153">Na powitania **logowanie jednokrotne** okna dialogowego, w **tryb** wybierz **na języku SAML logowania jednokrotnego** tooenable rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="b6e62-153">On hello **Single sign-on** dialog, in **Mode** select **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-linkedinsalesnavigator-tutorial/tutorial_linkedinsalesnavigator_samlbase.png)

3. <span data-ttu-id="b6e62-155">W oknie przeglądarki innej witryny sieci web, logowania jednokrotnego tooyour **LinkedIn sprzedaży Navigator** witryny sieci Web jako administrator.</span><span class="sxs-lookup"><span data-stu-id="b6e62-155">In a different web browser window, sign-on tooyour **LinkedIn Sales Navigator** website as an administrator.</span></span>

4. <span data-ttu-id="b6e62-156">W **Centrum konta**, kliknij przycisk **ustawienia globalne** w obszarze **ustawienia**.</span><span class="sxs-lookup"><span data-stu-id="b6e62-156">In **Account Center**, click **Global Settings** under **Settings**.</span></span> <span data-ttu-id="b6e62-157">Zaznacz również **Nawigator sprzedaży** z listy rozwijanej hello.</span><span class="sxs-lookup"><span data-stu-id="b6e62-157">Also, select **Sales Navigator** from hello dropdown list.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-linkedinsalesnavigator-tutorial/tutorial_linkedin_admin_01.png)

5. <span data-ttu-id="b6e62-159">Kliknij przycisk **lub kliknij tutaj tooload i skopiuj poszczególnych pól formularza hello** i skopiuj **identyfikator jednostki** i **potwierdzenia konsumenta dostępu (ACS) adres Url**.</span><span class="sxs-lookup"><span data-stu-id="b6e62-159">Click **OR Click Here tooload and copy individual fields from hello form** and copy **Entity Id** and **Assertion Consumer Access (ACS) Url**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-linkedinsalesnavigator-tutorial/tutorial_linkedin_admin_031.png)

6. <span data-ttu-id="b6e62-161">W portalu Azure w obszarze **LinkedIn sprzedaży Navigator domeny i adres URL** sekcji, wykonaj następujące kroki, jeśli chcesz, aby aplikacja hello tooconfigure w hello **IDP** inicjowane tryb.</span><span class="sxs-lookup"><span data-stu-id="b6e62-161">On Azure portal, under **LinkedIn Sales Navigator Domain and URLs** section, perform hello following steps if you wish tooconfigure hello application in **IDP** initiated mode.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-linkedinsalesnavigator-tutorial/tutorial_linkedinsalesnavigator_url1.png)

    <span data-ttu-id="b6e62-163">a.</span><span class="sxs-lookup"><span data-stu-id="b6e62-163">a.</span></span> <span data-ttu-id="b6e62-164">W hello **identyfikator** pole tekstowe, wprowadź hello **identyfikator jednostki** skopiowany z portalu LinkedIn</span><span class="sxs-lookup"><span data-stu-id="b6e62-164">In hello **Identifier** textbox, enter hello **Entity ID** copied from LinkedIn Portal</span></span> 

    <span data-ttu-id="b6e62-165">b.</span><span class="sxs-lookup"><span data-stu-id="b6e62-165">b.</span></span> <span data-ttu-id="b6e62-166">W hello **adres URL odpowiedzi** pole tekstowe, wprowadź hello **potwierdzenia konsumenta dostępu (ACS) adres Url** skopiowany z portalu LinkedIn</span><span class="sxs-lookup"><span data-stu-id="b6e62-166">In hello **Reply URL** textbox, enter hello **Assertion Consumer Access (ACS) Url** copied from LinkedIn Portal</span></span>

7. <span data-ttu-id="b6e62-167">Sprawdź **Pokaż zaawansowane ustawienia adresu URL**, jeśli chcesz, aby aplikacja hello tooconfigure w **SP** inicjowane tryb.</span><span class="sxs-lookup"><span data-stu-id="b6e62-167">Check **Show advanced URL settings**, if you wish tooconfigure hello application in **SP** initiated mode.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-linkedinsalesnavigator-tutorial/tutorial_linkedinsalesnavigator_url2.png)

    <span data-ttu-id="b6e62-169">W hello **adres URL logowania** pole tekstowe, wartość hello typu przy użyciu hello następującego wzorca:`https://www.linkedin.com/checkpoint/enterprise/login/<account id>?application=salesNavigator`</span><span class="sxs-lookup"><span data-stu-id="b6e62-169">In hello **Sign-on URL** textbox, type hello value using hello following pattern: `https://www.linkedin.com/checkpoint/enterprise/login/<account id>?application=salesNavigator`</span></span>

8. <span data-ttu-id="b6e62-170">Twoje **LinkedIn sprzedaży Navigator** aplikacji oczekuje potwierdzenia SAML hello w określonym formacie wymaga konfiguracja atrybutów tokenu SAML mapowania tooyour tooadd atrybutu niestandardowego.</span><span class="sxs-lookup"><span data-stu-id="b6e62-170">Your **LinkedIn Sales Navigator** application expects hello SAML assertions in a specific format, which requires you tooadd custom attribute mappings tooyour SAML token attributes configuration.</span></span> <span data-ttu-id="b6e62-171">powitania po zrzut ekranu przedstawia przykład.</span><span class="sxs-lookup"><span data-stu-id="b6e62-171">hello following screenshot shows an example.</span></span> <span data-ttu-id="b6e62-172">Witaj wartość domyślną **identyfikator użytkownika** jest **user.userprincipalname** , ale Nawigator sprzedaży LinkedIn oczekuje toobe zamapowana adres e-mail użytkownika hello.</span><span class="sxs-lookup"><span data-stu-id="b6e62-172">hello default value of **User Identifier** is **user.userprincipalname** but LinkedIn Sales Navigator expects it toobe mapped with hello user's email address.</span></span> <span data-ttu-id="b6e62-173">Można użyć **user.mail** atrybutu z listy hello lub użyj wartości atrybutu odpowiednie hello zgodnie z konfiguracją organizacji.</span><span class="sxs-lookup"><span data-stu-id="b6e62-173">You can use **user.mail** attribute from hello list or use hello appropriate attribute value based on your organization configuration.</span></span> 

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-linkedinsalesnavigator-tutorial/updateusermail.png)
    
9. <span data-ttu-id="b6e62-175">W **atrybuty użytkownika** kliknij **widoku i edytować wszystkie atrybuty użytkowników** i ustaw hello atrybuty.</span><span class="sxs-lookup"><span data-stu-id="b6e62-175">In **User Attributes** section, click **View and edit all other user attributes** and set hello attributes.</span></span> <span data-ttu-id="b6e62-176">Hello użytkownik powinien tooadd oświadczeń cztery o nazwie **e-mail**, **działu**, **imię**, i **nazwisko** i wartość hello jest zamapowana z toobe **user.mail**, **user.department**, **user.givenname**, i **user.surname** odpowiednio</span><span class="sxs-lookup"><span data-stu-id="b6e62-176">hello user needs tooadd four claims named **email**, **department**, **firstname**, and **lastname** and hello value is toobe mapped with **user.mail**, **user.department**, **user.givenname**, and **user.surname** respectively</span></span>

    | <span data-ttu-id="b6e62-177">Nazwa atrybutu</span><span class="sxs-lookup"><span data-stu-id="b6e62-177">Attribute Name</span></span> | <span data-ttu-id="b6e62-178">Wartość atrybutu</span><span class="sxs-lookup"><span data-stu-id="b6e62-178">Attribute Value</span></span> |
    | --- | --- |    
    | <span data-ttu-id="b6e62-179">Adres e-mail</span><span class="sxs-lookup"><span data-stu-id="b6e62-179">email</span></span>| <span data-ttu-id="b6e62-180">User.mail</span><span class="sxs-lookup"><span data-stu-id="b6e62-180">user.mail</span></span> |
    | <span data-ttu-id="b6e62-181">Dział</span><span class="sxs-lookup"><span data-stu-id="b6e62-181">department</span></span>| <span data-ttu-id="b6e62-182">User.Department</span><span class="sxs-lookup"><span data-stu-id="b6e62-182">user.department</span></span> |
    | <span data-ttu-id="b6e62-183">Imię</span><span class="sxs-lookup"><span data-stu-id="b6e62-183">firstname</span></span>| <span data-ttu-id="b6e62-184">User.givenName</span><span class="sxs-lookup"><span data-stu-id="b6e62-184">user.givenname</span></span> |
    | <span data-ttu-id="b6e62-185">nazwisko</span><span class="sxs-lookup"><span data-stu-id="b6e62-185">lastname</span></span>| <span data-ttu-id="b6e62-186">User.surname</span><span class="sxs-lookup"><span data-stu-id="b6e62-186">user.surname</span></span> |
    
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-linkedinsalesnavigator-tutorial/userattribute.png)
    
    <span data-ttu-id="b6e62-188">a.</span><span class="sxs-lookup"><span data-stu-id="b6e62-188">a.</span></span> <span data-ttu-id="b6e62-189">Polecenie **Dodawanie atrybutu** tooopen hello atrybutu w oknie dialogowym.</span><span class="sxs-lookup"><span data-stu-id="b6e62-189">Click on **Add Attribute** tooopen hello attribute dialog.</span></span>
    
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-linkedinsalesnavigator-tutorial/tutorial_attribute_04.png)
    
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-linkedinsalesnavigator-tutorial/tutorial_attribute_05.png)
   
    <span data-ttu-id="b6e62-192">b.</span><span class="sxs-lookup"><span data-stu-id="b6e62-192">b.</span></span> <span data-ttu-id="b6e62-193">W hello **nazwa** pole tekstowe, nazwa atrybutu hello typu wyświetlany dla danego wiersza.</span><span class="sxs-lookup"><span data-stu-id="b6e62-193">In hello **Name** textbox, type hello attribute name shown for that row.</span></span>
    
    <span data-ttu-id="b6e62-194">c.</span><span class="sxs-lookup"><span data-stu-id="b6e62-194">c.</span></span> <span data-ttu-id="b6e62-195">Z hello **wartość** listy wartości atrybutu hello typ wyświetlanego dla tego wiersza.</span><span class="sxs-lookup"><span data-stu-id="b6e62-195">From hello **Value** list, type hello attribute value shown for that row.</span></span>
    
    <span data-ttu-id="b6e62-196">d.</span><span class="sxs-lookup"><span data-stu-id="b6e62-196">d.</span></span> <span data-ttu-id="b6e62-197">Kliknij przycisk **Ok**</span><span class="sxs-lookup"><span data-stu-id="b6e62-197">Click **Ok**</span></span>

10. <span data-ttu-id="b6e62-198">Wykonaj następujące kroki na powitania hello **nazwa** — atrybut</span><span class="sxs-lookup"><span data-stu-id="b6e62-198">Perform hello following steps on hello **name** attribute-</span></span>

    <span data-ttu-id="b6e62-199">a.</span><span class="sxs-lookup"><span data-stu-id="b6e62-199">a.</span></span> <span data-ttu-id="b6e62-200">Polecenie hello atrybutu tooopen hello **atrybutu Edytuj** okna.</span><span class="sxs-lookup"><span data-stu-id="b6e62-200">Click on hello attribute tooopen hello **Edit Attribute** window.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-linkedinsalesnavigator-tutorial/url_update.png)

    <span data-ttu-id="b6e62-202">b.</span><span class="sxs-lookup"><span data-stu-id="b6e62-202">b.</span></span> <span data-ttu-id="b6e62-203">Usuń wartość adresu URL hello z hello **przestrzeni nazw**.</span><span class="sxs-lookup"><span data-stu-id="b6e62-203">Delete hello URL value from hello **namespace**.</span></span>
    
    <span data-ttu-id="b6e62-204">c.</span><span class="sxs-lookup"><span data-stu-id="b6e62-204">c.</span></span> <span data-ttu-id="b6e62-205">Kliknij przycisk **Ok** toosave hello ustawienie.</span><span class="sxs-lookup"><span data-stu-id="b6e62-205">Click **Ok** toosave hello setting.</span></span>

11. <span data-ttu-id="b6e62-206">Na powitania **certyfikat podpisywania SAML** kliknij **XML metadanych** , a następnie zapisz plik XML hello na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="b6e62-206">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello XML file on your computer.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-linkedinsalesnavigator-tutorial/tutorial_linkedinsalesnavigator_certificate.png) 

12. <span data-ttu-id="b6e62-208">Kliknij przycisk **zapisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="b6e62-208">Click **Save** button.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-linkedinsalesnavigator-tutorial/tutorial_general_400.png)

13. <span data-ttu-id="b6e62-210">Przejdź za**ustawienia administratora LinkedIn** sekcji.</span><span class="sxs-lookup"><span data-stu-id="b6e62-210">Go too**LinkedIn Admin Settings** section.</span></span> <span data-ttu-id="b6e62-211">Kliknij przycisk **pliku XML, Przekaż** hello tooupload pobranego z portalu Azure hello pliku XML metadanych.</span><span class="sxs-lookup"><span data-stu-id="b6e62-211">Click **Upload XML file** tooupload hello Metadata XML file that you have downloaded from hello Azure portal.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-linkedinsalesnavigator-tutorial/tutorial_linkedin_metadata_03.png)

14. <span data-ttu-id="b6e62-213">Kliknij przycisk **na** tooenable logowania jednokrotnego.</span><span class="sxs-lookup"><span data-stu-id="b6e62-213">Click **On** tooenable SSO.</span></span> <span data-ttu-id="b6e62-214">Zmiany stanu rejestracji Jednokrotnej z **niepołączone** zbyt**połączony**</span><span class="sxs-lookup"><span data-stu-id="b6e62-214">SSO status changes from **Not Connected** too**Connected**</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-linkedinsalesnavigator-tutorial/tutorial_linkedin_admin_05.png)


> [!TIP]
> <span data-ttu-id="b6e62-216">Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz hello [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji hello!</span><span class="sxs-lookup"><span data-stu-id="b6e62-216">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="b6e62-217">Po dodaniu tej aplikacji z hello **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij hello **rejestracji jednokrotnej** hello kartę i dostępu do osadzonych dokumentacji za pośrednictwem hello  **Konfiguracja** sekcji u dołu hello.</span><span class="sxs-lookup"><span data-stu-id="b6e62-217">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="b6e62-218">Więcej o hello osadzonych dokumentacji funkcji w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="b6e62-218">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="b6e62-219">Tworzenie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="b6e62-219">Creating an Azure AD test user</span></span>
<span data-ttu-id="b6e62-220">Celem Hello w tej sekcji jest toocreate użytkownika testowego, w portalu Azure o nazwie Simona Britta hello.</span><span class="sxs-lookup"><span data-stu-id="b6e62-220">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Tworzenie użytkowników usługi Azure AD][100]

<span data-ttu-id="b6e62-222">**toocreate użytkownika testowego w usłudze Azure AD, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="b6e62-222">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="b6e62-223">W hello **portalu Azure**na temat hello w lewym okienku nawigacji, kliknij przycisk **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="b6e62-223">In hello **Azure  portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-linkedinsalesnavigator-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="b6e62-225">Przejdź za**użytkowników i grup** i kliknij przycisk **wszyscy użytkownicy**.</span><span class="sxs-lookup"><span data-stu-id="b6e62-225">Go too**Users and groups** and click **All users**.</span></span>
    
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-linkedinsalesnavigator-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="b6e62-227">U góry okna dialogowego hello powitania kliknij **Dodaj** tooopen hello **użytkownika** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="b6e62-227">At hello top of hello dialog click **Add** tooopen hello **User** dialog.</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-linkedinsalesnavigator-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="b6e62-229">Na powitania **użytkownika** okna dialogowego wykonaj hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="b6e62-229">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-linkedinsalesnavigator-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="b6e62-231">a.</span><span class="sxs-lookup"><span data-stu-id="b6e62-231">a.</span></span> <span data-ttu-id="b6e62-232">W hello **nazwa** pole tekstowe, typ **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="b6e62-232">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="b6e62-233">b.</span><span class="sxs-lookup"><span data-stu-id="b6e62-233">b.</span></span> <span data-ttu-id="b6e62-234">W hello **nazwy użytkownika** pole tekstowe, hello typu **adres e-mail** z BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="b6e62-234">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="b6e62-235">c.</span><span class="sxs-lookup"><span data-stu-id="b6e62-235">c.</span></span> <span data-ttu-id="b6e62-236">Wybierz **Pokaż hasło** i zanotuj wartość hello hello **hasło**.</span><span class="sxs-lookup"><span data-stu-id="b6e62-236">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="b6e62-237">d.</span><span class="sxs-lookup"><span data-stu-id="b6e62-237">d.</span></span> <span data-ttu-id="b6e62-238">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="b6e62-238">Click **Create**.</span></span>
 
### <a name="creating-a-linkedin-sales-navigator-test-user"></a><span data-ttu-id="b6e62-239">Tworzenie użytkownika testowego LinkedIn Nawigator sprzedaży</span><span class="sxs-lookup"><span data-stu-id="b6e62-239">Creating a LinkedIn Sales Navigator test user</span></span>

<span data-ttu-id="b6e62-240">Połączonej aplikacji Navigator sprzedaży obsługuje tylko w czasie (JIT) Inicjowanie obsługi użytkowników i uwierzytelnianie użytkowników są tworzone automatycznie w aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="b6e62-240">Linked Sales Navigator Application supports Just in Time (JIT) user provisioning and after authentication users are created in hello application automatically.</span></span> <span data-ttu-id="b6e62-241">Aktywuj **automatycznie przypisać licencje** tooassign toohello licencji użytkownika.</span><span class="sxs-lookup"><span data-stu-id="b6e62-241">Activate **Automatically assign licenses** tooassign a license toohello user.</span></span>
   
   ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-linkedinsalesnavigator-tutorial/LinkedinUserprovswitch.png)

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="b6e62-243">Przypisanie użytkownika testowego hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="b6e62-243">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="b6e62-244">W tej sekcji możesz włączyć toouse Simona Britta Azure logowania jednokrotnego za udzielanie dostępu tooLinkedIn Nawigator sprzedaży.</span><span class="sxs-lookup"><span data-stu-id="b6e62-244">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooLinkedIn Sales Navigator.</span></span>

![Przypisz użytkownika][200] 

<span data-ttu-id="b6e62-246">**tooassign tooLinkedIn Simona Britta Nawigator sprzedaży, wykonaj hello następujące kroki:**</span><span class="sxs-lookup"><span data-stu-id="b6e62-246">**tooassign Britta Simon tooLinkedIn Sales Navigator, perform hello following steps:**</span></span>

1. <span data-ttu-id="b6e62-247">W portalu Azure hello, otwórz widok aplikacji hello, a następnie przejdź do widoku katalogu toohello i przejść za**aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="b6e62-247">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Przypisz użytkownika][201] 

2. <span data-ttu-id="b6e62-249">Z listy aplikacji hello wybierz **LinkedIn sprzedaży Navigator**.</span><span class="sxs-lookup"><span data-stu-id="b6e62-249">In hello applications list, select **LinkedIn Sales Navigator**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-linkedinsalesnavigator-tutorial/tutorial_linkedinsalesnavigator_app.png) 

3. <span data-ttu-id="b6e62-251">W menu powitania po lewej stronie powitania kliknij **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="b6e62-251">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Przypisz użytkownika][202] 

4. <span data-ttu-id="b6e62-253">Kliknij przycisk **Dodaj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="b6e62-253">Click **Add** button.</span></span> <span data-ttu-id="b6e62-254">Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="b6e62-254">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Przypisz użytkownika][203]

5. <span data-ttu-id="b6e62-256">Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** hello listy użytkowników.</span><span class="sxs-lookup"><span data-stu-id="b6e62-256">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="b6e62-257">Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="b6e62-257">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="b6e62-258">Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="b6e62-258">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="b6e62-259">Testowanie rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="b6e62-259">Testing single sign-on</span></span>

<span data-ttu-id="b6e62-260">W tej sekcji można przetestować konfiguracji usługi Azure AD pojedynczego logowania jednokrotnego przy użyciu hello panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="b6e62-260">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="b6e62-261">Po kliknięciu kafelka Navigator sprzedaży LinkedIn hello w hello panelu dostępu należy strony przekierowanego tooOrganizational gdzie masz tooprovide informacje osobowe konta LinkedIn.</span><span class="sxs-lookup"><span data-stu-id="b6e62-261">When you click hello LinkedIn Sales Navigator tile in hello Access Panel, you should be redirected tooOrganizational page where you have tooprovide your personal LinkedIn account details.</span></span> <span data-ttu-id="b6e62-262">Łączy konto osobiste konta firmowego LinkedIn.</span><span class="sxs-lookup"><span data-stu-id="b6e62-262">It links your personal account with your LinkedIn business account.</span></span> <span data-ttu-id="b6e62-263">Aby uzyskać więcej informacji na temat hello Panel dostępu, zobacz [wprowadzenie do panelu dostępu](https://msdn.microsoft.com/library/dn308586).</span><span class="sxs-lookup"><span data-stu-id="b6e62-263">For more information about hello Access Panel, see [Introduction to the Access Panel](https://msdn.microsoft.com/library/dn308586).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="b6e62-264">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="b6e62-264">Additional resources</span></span>

* [<span data-ttu-id="b6e62-265">Lista samouczków dotyczących tooIntegrate aplikacji SaaS w usłudze Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="b6e62-265">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="b6e62-266">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="b6e62-266">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-linkedinsalesnavigator-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-linkedinsalesnavigator-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-linkedinsalesnavigator-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-linkedinsalesnavigator-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-linkedinsalesnavigator-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-linkedinsalesnavigator-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-linkedinsalesnavigator-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-linkedinsalesnavigator-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-linkedinsalesnavigator-tutorial/tutorial_general_203.png

