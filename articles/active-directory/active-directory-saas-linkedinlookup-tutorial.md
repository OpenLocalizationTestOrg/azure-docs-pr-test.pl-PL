---
title: 'Samouczek: Integracji Azure Active Directory z wyszukiwania LinkedIn | Dokumentacja firmy Microsoft'
description: "Dowiedz się, jak tooconfigure logowanie jednokrotne między usługą Azure Active Directory i LinkedIn wyszukiwania."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: a2757a39-1ead-4a3e-91e4-270be3055683
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/14/2017
ms.author: jeedes
ms.openlocfilehash: d79c34baa676391699e4b49806f16422fcfe73e1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-linkedin-lookup"></a><span data-ttu-id="aeee9-103">Samouczek: Integracji Azure Active Directory z LinkedIn wyszukiwania</span><span class="sxs-lookup"><span data-stu-id="aeee9-103">Tutorial: Azure Active Directory integration with LinkedIn Lookup</span></span>

<span data-ttu-id="aeee9-104">Z tego samouczka, dowiesz się, jak toointegrate LinkedIn wyszukiwania w usłudze Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="aeee9-104">In this tutorial, you learn how toointegrate LinkedIn Lookup with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="aeee9-105">Integrowanie wyszukiwania LinkedIn z usługą Azure AD zapewnia hello następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="aeee9-105">Integrating LinkedIn Lookup with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="aeee9-106">Można kontrolować w usłudze Azure AD, kto ma dostęp do tooLinkedIn wyszukiwania</span><span class="sxs-lookup"><span data-stu-id="aeee9-106">You can control in Azure AD who has access tooLinkedIn Lookup</span></span>
- <span data-ttu-id="aeee9-107">Można włączyć użytkownika użytkownicy tooautomatically get zalogowane tooLinkedIn wyszukiwania (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="aeee9-107">You can enable your users tooautomatically get signed-on tooLinkedIn Lookup (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="aeee9-108">Możesz zarządzać kont w jednej centralnej lokalizacji - hello portalu Azure</span><span class="sxs-lookup"><span data-stu-id="aeee9-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="aeee9-109">Jeśli chcesz tooknow więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="aeee9-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="aeee9-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="aeee9-110">Prerequisites</span></span>

<span data-ttu-id="aeee9-111">tooconfigure integracji usługi Azure AD z LinkedIn wyszukiwania należy hello następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="aeee9-111">tooconfigure Azure AD integration with LinkedIn Lookup, you need hello following items:</span></span>

- <span data-ttu-id="aeee9-112">Subskrypcję usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="aeee9-112">An Azure AD subscription</span></span>
- <span data-ttu-id="aeee9-113">Wyszukiwanie LinkedIn jednokrotnego włączone subskrypcji</span><span class="sxs-lookup"><span data-stu-id="aeee9-113">An LinkedIn Lookup single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="aeee9-114">tootest hello kroków w tym samouczku, zaleca się przy użyciu środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="aeee9-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="aeee9-115">tootest hello kroki opisane w tym samouczku, należy stosować te zalecenia:</span><span class="sxs-lookup"><span data-stu-id="aeee9-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="aeee9-116">Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="aeee9-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="aeee9-117">Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz pobrać miesięczna wersja próbna [tutaj](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="aeee9-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="aeee9-118">Opis scenariusza</span><span class="sxs-lookup"><span data-stu-id="aeee9-118">Scenario description</span></span>
<span data-ttu-id="aeee9-119">W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym.</span><span class="sxs-lookup"><span data-stu-id="aeee9-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="aeee9-120">Scenariusz Hello opisane w tym samouczku składa się z dwóch głównych elementów:</span><span class="sxs-lookup"><span data-stu-id="aeee9-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="aeee9-121">Dodawanie wyszukiwania LinkedIn z galerii hello</span><span class="sxs-lookup"><span data-stu-id="aeee9-121">Adding LinkedIn Lookup from hello gallery</span></span>
2. <span data-ttu-id="aeee9-122">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="aeee9-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-linkedin-lookup-from-hello-gallery"></a><span data-ttu-id="aeee9-123">Dodawanie wyszukiwania LinkedIn z galerii hello</span><span class="sxs-lookup"><span data-stu-id="aeee9-123">Adding LinkedIn Lookup from hello gallery</span></span>
<span data-ttu-id="aeee9-124">tooconfigure hello integracji LinkedIn wyszukiwania w usłudze Azure Active Directory, należy tooadd LinkedIn wyszukiwania z listy tooyour galerii hello zarządzanych aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="aeee9-124">tooconfigure hello integration of LinkedIn Lookup into Azure AD, you need tooadd LinkedIn Lookup from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="aeee9-125">**tooadd wyszukiwania LinkedIn z galerii hello wykonaj hello następujące kroki:**</span><span class="sxs-lookup"><span data-stu-id="aeee9-125">**tooadd LinkedIn Lookup from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="aeee9-126">W hello  **[portalu Azure](https://portal.azure.com)**na temat hello panelu nawigacji po lewej stronie, kliknij przycisk **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="aeee9-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Usługa Active Directory][1]

2. <span data-ttu-id="aeee9-128">Przejdź za**aplikacje dla przedsiębiorstw**.</span><span class="sxs-lookup"><span data-stu-id="aeee9-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="aeee9-129">Następnie przejdź zbyt**wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="aeee9-129">Then go too**All applications**.</span></span>

    ![Aplikacje][2]
    
3. <span data-ttu-id="aeee9-131">Kliknij przycisk **nowej aplikacji** przycisk na powitania górnej części okna dialogowego hello tooadd nowej aplikacji.</span><span class="sxs-lookup"><span data-stu-id="aeee9-131">Click **New application** button on hello top of hello dialog tooadd new application.</span></span>

    ![Aplikacje][3]

4. <span data-ttu-id="aeee9-133">W polu wyszukiwania hello wpisz **wyszukiwania LinkedIn**.</span><span class="sxs-lookup"><span data-stu-id="aeee9-133">In hello search box, type **LinkedIn Lookup**.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_linkedInlookup_search.png)

5. <span data-ttu-id="aeee9-135">W panelu wyników hello, wybierz **wyszukiwania LinkedIn**, a następnie kliknij przycisk **Dodaj** przycisk aplikacji hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="aeee9-135">In hello results panel, select **LinkedIn Lookup**, and then click **Add** button tooadd hello application.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_linkedInlookup_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="aeee9-137">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="aeee9-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="aeee9-138">W tej sekcji możesz skonfigurować i test usługi Azure AD rejestracji jednokrotnej z LinkedIn wyszukiwania w oparciu o nazwie "Britta Simona" użytkownika testowego.</span><span class="sxs-lookup"><span data-stu-id="aeee9-138">In this section, you configure and test Azure AD single sign-on with LinkedIn Lookup based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="aeee9-139">Dla pojedynczego logowania jednokrotnego toowork usługi Azure AD musi tooknow użytkownika odpowiednikiem hello odnośnika LinkedIn jest tooa użytkownika w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="aeee9-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in LinkedIn Lookup is tooa user in Azure AD.</span></span> <span data-ttu-id="aeee9-140">Innymi słowy relację łącza między użytkownika usługi Azure AD i hello użytkownikowi w wyszukiwaniu LinkedIn musi toobe ustanowione.</span><span class="sxs-lookup"><span data-stu-id="aeee9-140">In other words, a link relationship between an Azure AD user and hello related user in LinkedIn Lookup needs toobe established.</span></span>

<span data-ttu-id="aeee9-141">Ta relacja łącza zostanie nawiązane, przypisując wartość hello hello **nazwy użytkownika** w usłudze Azure AD jako wartość hello hello **Username** odnośnika LinkedIn.</span><span class="sxs-lookup"><span data-stu-id="aeee9-141">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in LinkedIn Lookup.</span></span>

<span data-ttu-id="aeee9-142">tooconfigure i testowych usługi Azure AD rejestracji jednokrotnej z LinkedIn wyszukiwania, należy po bloków konstrukcyjnych hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="aeee9-142">tooconfigure and test Azure AD single sign-on with LinkedIn Lookup, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="aeee9-143">**[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configuring-azure-ad-single-sign-on)**  -tooenable Twojego toouse użytkowników tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="aeee9-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="aeee9-144">**[Tworzenie użytkownika testowego usługi Azure AD](#creating-an-azure-ad-test-user)**  -tootest usługi Azure AD rejestracji jednokrotnej z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="aeee9-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="aeee9-145">**[Tworzenie użytkownika testowego wyszukiwania LinkedIn](#creating-an-linkedin-lookup-test-user)**  -toohave odpowiednikiem Simona Britta odnośnika LinkedIn, który jest odpowiednikiem połączonych toohello usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="aeee9-145">**[Creating an LinkedIn Lookup test user](#creating-an-linkedin-lookup-test-user)** - toohave a counterpart of Britta Simon in LinkedIn Lookup that is linked toohello Azure AD representation.</span></span>
4. <span data-ttu-id="aeee9-146">**[Przypisanie użytkownika testowego hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Simona Britta toouse usługi Azure AD rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="aeee9-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="aeee9-147">**[Testowanie rejestracji jednokrotnej](#testing-single-sign-on)**  -tooverify czy hello konfiguracji działania.</span><span class="sxs-lookup"><span data-stu-id="aeee9-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="aeee9-148">Konfigurowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="aeee9-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="aeee9-149">W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w hello portalu Azure i skonfigurować logowanie jednokrotne w aplikacji wyszukiwania LinkedIn.</span><span class="sxs-lookup"><span data-stu-id="aeee9-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your LinkedIn Lookup application.</span></span>

<span data-ttu-id="aeee9-150">**tooconfigure usługi Azure AD rejestracji jednokrotnej z LinkedIn wyszukiwanie, należy wykonać hello następujące kroki:**</span><span class="sxs-lookup"><span data-stu-id="aeee9-150">**tooconfigure Azure AD single sign-on with LinkedIn Lookup, perform hello following steps:**</span></span>

1. <span data-ttu-id="aeee9-151">W portalu Azure na powitania hello **wyszukiwania LinkedIn** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.</span><span class="sxs-lookup"><span data-stu-id="aeee9-151">In hello Azure portal, on hello **LinkedIn Lookup** application integration page, click **Single sign-on**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej][4]

2. <span data-ttu-id="aeee9-153">Na powitania **logowanie jednokrotne** okna dialogowego, w **tryb** wybierz **na języku SAML logowania jednokrotnego** tooenable rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="aeee9-153">On hello **Single sign-on** dialog, in **Mode** select **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_linkedInlookup_samlbase.png)

3. <span data-ttu-id="aeee9-155">W oknie przeglądarki innej witryny sieci web, logowania jednokrotnego tooyour **wyszukiwania LinkedIn** witryny sieci Web jako administrator.</span><span class="sxs-lookup"><span data-stu-id="aeee9-155">In a different web browser window, sign-on tooyour **LinkedIn Lookup** website as an administrator.</span></span>

4. <span data-ttu-id="aeee9-156">W **Centrum konta**, kliknij przycisk **ustawienia globalne** w obszarze **ustawienia**.</span><span class="sxs-lookup"><span data-stu-id="aeee9-156">In **Account Center**, click **Global Settings** under **Settings**.</span></span> <span data-ttu-id="aeee9-157">Zaznacz również **wyszukiwania** z listy rozwijanej hello.</span><span class="sxs-lookup"><span data-stu-id="aeee9-157">Also, select **Lookup** from hello dropdown list.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_LinkedIn_admin_011.png)

5. <span data-ttu-id="aeee9-159">Kliknij przycisk **lub kliknij tutaj tooload i skopiuj poszczególnych pól formularza hello** i skopiuj **identyfikator jednostki** i **adresu Url potwierdzenia konsumenta dostępu (ACS)**</span><span class="sxs-lookup"><span data-stu-id="aeee9-159">Click **OR Click Here tooload and copy individual fields from hello form** and copy **Entity Id** and **Assertion Consumer Access (ACS) Url**</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_LinkedIn_admin_032.png)

6. <span data-ttu-id="aeee9-161">W portalu Azure w obszarze **domeny wyszukiwania LinkedIn i adres URL** sekcji, wykonaj następujące kroki, jeśli chcesz, aby aplikacja hello tooconfigure w hello **IDP** inicjowane tryb:</span><span class="sxs-lookup"><span data-stu-id="aeee9-161">On Azure portal, under **LinkedIn Lookup Domain and URLs** section, perform hello following steps if you wish tooconfigure hello application in **IDP** initiated mode:</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_linkedInlookup_url.png)

    <span data-ttu-id="aeee9-163">a.</span><span class="sxs-lookup"><span data-stu-id="aeee9-163">a.</span></span> <span data-ttu-id="aeee9-164">W hello **identyfikator** pole tekstowe, wprowadź hello **identyfikator jednostki** skopiowany z portalu LinkedIn</span><span class="sxs-lookup"><span data-stu-id="aeee9-164">In hello **Identifier** textbox, enter hello **Entity ID** copied from LinkedIn Portal</span></span> 

    <span data-ttu-id="aeee9-165">b.</span><span class="sxs-lookup"><span data-stu-id="aeee9-165">b.</span></span> <span data-ttu-id="aeee9-166">W hello **adres URL odpowiedzi** pole tekstowe, wprowadź hello **potwierdzenia konsumenta dostępu (ACS) adres Url** skopiowany z portalu LinkedIn</span><span class="sxs-lookup"><span data-stu-id="aeee9-166">In hello **Reply URL** textbox, enter hello **Assertion Consumer Access (ACS) Url** copied from LinkedIn Portal</span></span>

7. <span data-ttu-id="aeee9-167">Sprawdź **Pokaż zaawansowane ustawienia adresu URL**, jeśli chcesz, aby aplikacja hello tooconfigure w **SP** inicjowane tryb:</span><span class="sxs-lookup"><span data-stu-id="aeee9-167">Check **Show advanced URL settings**, if you wish tooconfigure hello application in **SP** initiated mode:</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_linkedInlookup_url1.png)

    <span data-ttu-id="aeee9-169">W hello **adres URL logowania** tekstowym, wpisz adres URL za pomocą hello następującego wzorca:`https://www.linkedIn.com/checkpoint/enterprise/login/<AccountId>?application=lookup`</span><span class="sxs-lookup"><span data-stu-id="aeee9-169">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://www.linkedIn.com/checkpoint/enterprise/login/<AccountId>?application=lookup`</span></span>
     
    > [!NOTE] 
    > <span data-ttu-id="aeee9-170">To nie jest rzeczywistą wartość.</span><span class="sxs-lookup"><span data-stu-id="aeee9-170">This is not real value.</span></span> <span data-ttu-id="aeee9-171">Użytkownik Hello ma tooupdate tych wartości za pomocą hello rzeczywisty adres URL logowania.</span><span class="sxs-lookup"><span data-stu-id="aeee9-171">hello user has tooupdate these values with hello actual Sign-On URL.</span></span> <span data-ttu-id="aeee9-172">Skontaktuj się z [zespołem pomocy technicznej klienta wyszukiwania LinkedIn](https://business.LinkedIn.com/lookup) tooget tej wartości.</span><span class="sxs-lookup"><span data-stu-id="aeee9-172">Contact [LinkedIn Lookup Client support team](https://business.LinkedIn.com/lookup) tooget this value.</span></span>

8. <span data-ttu-id="aeee9-173">Twoje **wyszukiwania LinkedIn** aplikacji oczekuje potwierdzenia SAML hello w określonym formacie.</span><span class="sxs-lookup"><span data-stu-id="aeee9-173">Your **LinkedIn Lookup** application expects hello SAML assertions in a specific format.</span></span> <span data-ttu-id="aeee9-174">Użytkownik Hello ma konfiguracja atrybutów tokenu SAML mapowania toohello tooadd atrybutu niestandardowego.</span><span class="sxs-lookup"><span data-stu-id="aeee9-174">hello user has tooadd custom attribute mappings toohello SAML token attributes configuration.</span></span> <span data-ttu-id="aeee9-175">powitania po zrzut ekranu przedstawia przykład.</span><span class="sxs-lookup"><span data-stu-id="aeee9-175">hello following screenshot shows an example.</span></span> <span data-ttu-id="aeee9-176">Witaj wartość domyślną **identyfikator użytkownika** jest **user.userprincipalname** , ale ta toobe zamapowana adres e-mail użytkownika hello oczekuje LinkedIn wyszukiwania.</span><span class="sxs-lookup"><span data-stu-id="aeee9-176">hello default value of **User Identifier** is **user.userprincipalname** but LinkedIn Lookup expects this toobe mapped with hello user's email address.</span></span> <span data-ttu-id="aeee9-177">Można użyć **user.mail** atrybutu z listy hello lub użyj wartości atrybutu odpowiednie hello zgodnie z konfiguracją organizacji.</span><span class="sxs-lookup"><span data-stu-id="aeee9-177">You can use **user.mail** attribute from hello list or use hello appropriate attribute value based on your organization configuration.</span></span> 

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-LinkedInlookup-tutorial/updateusermail.png)
    
9. <span data-ttu-id="aeee9-179">W **atrybuty użytkownika** kliknij **widoku i edytować wszystkie atrybuty użytkowników** i ustaw hello atrybuty.</span><span class="sxs-lookup"><span data-stu-id="aeee9-179">In **User Attributes** section, click **View and edit all other user attributes** and set hello attributes.</span></span> <span data-ttu-id="aeee9-180">Hello użytkownik powinien tooadd oświadczeń cztery o nazwie **e-mail**, **działu**, **imię**, i **nazwisko** i wartość hello jest zamapowana z toobe **user.mail**, **user.department**, **user.givenname**, i **user.surname** odpowiednio</span><span class="sxs-lookup"><span data-stu-id="aeee9-180">hello user needs tooadd four claims named **email**,  **department**, **firstname**, and **lastname** and hello value is toobe mapped with **user.mail**, **user.department**, **user.givenname**, and **user.surname** respectively</span></span>

    | <span data-ttu-id="aeee9-181">Nazwa atrybutu</span><span class="sxs-lookup"><span data-stu-id="aeee9-181">Attribute Name</span></span> | <span data-ttu-id="aeee9-182">Wartość atrybutu</span><span class="sxs-lookup"><span data-stu-id="aeee9-182">Attribute Value</span></span> |
    | --- | --- |
    | <span data-ttu-id="aeee9-183">Adres e-mail</span><span class="sxs-lookup"><span data-stu-id="aeee9-183">email</span></span>| <span data-ttu-id="aeee9-184">User.mail</span><span class="sxs-lookup"><span data-stu-id="aeee9-184">user.mail</span></span> |    
    | <span data-ttu-id="aeee9-185">Dział</span><span class="sxs-lookup"><span data-stu-id="aeee9-185">department</span></span>| <span data-ttu-id="aeee9-186">User.Department</span><span class="sxs-lookup"><span data-stu-id="aeee9-186">user.department</span></span> |
    | <span data-ttu-id="aeee9-187">Imię</span><span class="sxs-lookup"><span data-stu-id="aeee9-187">firstname</span></span>| <span data-ttu-id="aeee9-188">User.givenName</span><span class="sxs-lookup"><span data-stu-id="aeee9-188">user.givenname</span></span> |
    | <span data-ttu-id="aeee9-189">nazwisko</span><span class="sxs-lookup"><span data-stu-id="aeee9-189">lastname</span></span>| <span data-ttu-id="aeee9-190">User.surname</span><span class="sxs-lookup"><span data-stu-id="aeee9-190">user.surname</span></span> |

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-LinkedInlookup-tutorial/userattribute.png)

    <span data-ttu-id="aeee9-192">a.</span><span class="sxs-lookup"><span data-stu-id="aeee9-192">a.</span></span> <span data-ttu-id="aeee9-193">Kliknij przycisk **Dodawanie atrybutu** tooopen hello **Dodawanie atrybutu** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="aeee9-193">Click **Add Attribute** tooopen hello **Add Attribute** dialog.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-LinkedInlookup-tutorial/4.png)
   
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-LinkedInlookup-tutorial/5.png)
   
    <span data-ttu-id="aeee9-196">b.</span><span class="sxs-lookup"><span data-stu-id="aeee9-196">b.</span></span> <span data-ttu-id="aeee9-197">W hello **nazwa** pole tekstowe, nazwa atrybutu hello typu wyświetlany dla danego wiersza.</span><span class="sxs-lookup"><span data-stu-id="aeee9-197">In hello **Name** textbox, type hello attribute name shown for that row.</span></span>
    
    <span data-ttu-id="aeee9-198">c.</span><span class="sxs-lookup"><span data-stu-id="aeee9-198">c.</span></span> <span data-ttu-id="aeee9-199">Z hello **wartość** listy wartości atrybutu hello typ wyświetlanego dla tego wiersza.</span><span class="sxs-lookup"><span data-stu-id="aeee9-199">From hello **Value** list, type hello attribute value shown for that row.</span></span>
    
    <span data-ttu-id="aeee9-200">d.</span><span class="sxs-lookup"><span data-stu-id="aeee9-200">d.</span></span> <span data-ttu-id="aeee9-201">Kliknij przycisk **Ok**</span><span class="sxs-lookup"><span data-stu-id="aeee9-201">Click **Ok**</span></span>

10. <span data-ttu-id="aeee9-202">Wykonaj następujące kroki na powitania hello **nazwa** — atrybut</span><span class="sxs-lookup"><span data-stu-id="aeee9-202">Perform hello following steps on hello **name** attribute-</span></span>

    <span data-ttu-id="aeee9-203">a.</span><span class="sxs-lookup"><span data-stu-id="aeee9-203">a.</span></span> <span data-ttu-id="aeee9-204">Polecenie hello atrybutu tooopen hello **atrybutu Edytuj** okna.</span><span class="sxs-lookup"><span data-stu-id="aeee9-204">Click on hello attribute tooopen hello **Edit Attribute** window.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-LinkedInlookup-tutorial/url_update.png)

    <span data-ttu-id="aeee9-206">b.</span><span class="sxs-lookup"><span data-stu-id="aeee9-206">b.</span></span> <span data-ttu-id="aeee9-207">Usuń wartość adresu URL hello z hello **przestrzeni nazw**.</span><span class="sxs-lookup"><span data-stu-id="aeee9-207">Delete hello URL value from hello **namespace**.</span></span>
    
    <span data-ttu-id="aeee9-208">c.</span><span class="sxs-lookup"><span data-stu-id="aeee9-208">c.</span></span> <span data-ttu-id="aeee9-209">Kliknij przycisk **Ok** toosave hello ustawienie.</span><span class="sxs-lookup"><span data-stu-id="aeee9-209">Click **Ok** toosave hello setting.</span></span>

10. <span data-ttu-id="aeee9-210">Na powitania **certyfikat podpisywania SAML** kliknij **XML metadanych** , a następnie zapisz plik XML hello na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="aeee9-210">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello XML file on your computer.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_linkedInlookup_certificate.png) 

11. <span data-ttu-id="aeee9-212">Kliknij przycisk **zapisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="aeee9-212">Click **Save** button.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_general_400.png)

12. <span data-ttu-id="aeee9-214">Przejdź za**ustawienia administratora LinkedIn** sekcji.</span><span class="sxs-lookup"><span data-stu-id="aeee9-214">Go too**LinkedIn Admin Settings** section.</span></span> <span data-ttu-id="aeee9-215">Plik XML hello przekazywania pobranego z hello portalu Azure, klikając hello **pliku XML, Przekaż** opcji.</span><span class="sxs-lookup"><span data-stu-id="aeee9-215">Upload hello XML file you downloaded from hello Azure portal by clicking hello **Upload XML file** option.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_linkedIn_metadata_03.png)

13. <span data-ttu-id="aeee9-217">Kliknij przycisk **na** tooenable logowania jednokrotnego.</span><span class="sxs-lookup"><span data-stu-id="aeee9-217">Click **On** tooenable SSO.</span></span> <span data-ttu-id="aeee9-218">Zmiany stanu rejestracji Jednokrotnej z **niepołączone** zbyt**połączony**</span><span class="sxs-lookup"><span data-stu-id="aeee9-218">SSO status changes from **Not Connected** too**Connected**</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_linkedIn_admin_05.png)

> [!TIP]
> <span data-ttu-id="aeee9-220">Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz hello [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji hello!</span><span class="sxs-lookup"><span data-stu-id="aeee9-220">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="aeee9-221">Po dodaniu tej aplikacji z hello **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij hello **rejestracji jednokrotnej** hello kartę i dostępu do osadzonych dokumentacji za pośrednictwem hello  **Konfiguracja** sekcji u dołu hello.</span><span class="sxs-lookup"><span data-stu-id="aeee9-221">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="aeee9-222">Więcej o hello osadzonych dokumentacji funkcji w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="aeee9-222">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="aeee9-223">Tworzenie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="aeee9-223">Creating an Azure AD test user</span></span>
<span data-ttu-id="aeee9-224">Celem Hello w tej sekcji jest toocreate użytkownika testowego, w portalu Azure o nazwie Simona Britta hello.</span><span class="sxs-lookup"><span data-stu-id="aeee9-224">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Tworzenie użytkowników usługi Azure AD][100]

<span data-ttu-id="aeee9-226">**toocreate użytkownika testowego w usłudze Azure AD, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="aeee9-226">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="aeee9-227">W hello **portalu Azure**na temat hello w lewym okienku nawigacji, kliknij przycisk **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="aeee9-227">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-LinkedInlookup-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="aeee9-229">Przejdź za**użytkowników i grup** i kliknij przycisk **wszyscy użytkownicy**.</span><span class="sxs-lookup"><span data-stu-id="aeee9-229">Go too**Users and groups** and click **All users**.</span></span>
    
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-LinkedInlookup-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="aeee9-231">Kliknij przycisk **Dodaj** tooopen hello **użytkownika** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="aeee9-231">Click **Add** tooopen hello **User** dialog.</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-LinkedInlookup-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="aeee9-233">Na powitania **użytkownika** okna dialogowego wykonaj hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="aeee9-233">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-LinkedInlookup-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="aeee9-235">a.</span><span class="sxs-lookup"><span data-stu-id="aeee9-235">a.</span></span> <span data-ttu-id="aeee9-236">W hello **nazwa** pole tekstowe, typ **Simona Britta**.</span><span class="sxs-lookup"><span data-stu-id="aeee9-236">In hello **Name** textbox, type **Britta Simon**.</span></span>

    <span data-ttu-id="aeee9-237">b.</span><span class="sxs-lookup"><span data-stu-id="aeee9-237">b.</span></span> <span data-ttu-id="aeee9-238">W hello **nazwy użytkownika** pole tekstowe, hello typu **adres e-mail** z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="aeee9-238">In hello **User name** textbox, type hello **email address** of Britta Simon.</span></span>

    <span data-ttu-id="aeee9-239">c.</span><span class="sxs-lookup"><span data-stu-id="aeee9-239">c.</span></span> <span data-ttu-id="aeee9-240">Wybierz **Pokaż hasło** i zanotuj wartość hello hello **hasło**.</span><span class="sxs-lookup"><span data-stu-id="aeee9-240">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="aeee9-241">d.</span><span class="sxs-lookup"><span data-stu-id="aeee9-241">d.</span></span> <span data-ttu-id="aeee9-242">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="aeee9-242">Click **Create**.</span></span>
 
### <a name="creating-an-linkedin-lookup-test-user"></a><span data-ttu-id="aeee9-243">Tworzenie użytkownika testowego LinkedIn wyszukiwania</span><span class="sxs-lookup"><span data-stu-id="aeee9-243">Creating an LinkedIn Lookup test user</span></span>

<span data-ttu-id="aeee9-244">Połączonej aplikacji wyszukiwania obsługuje tylko w czasie (JIT) Inicjowanie obsługi użytkowników i uwierzytelnianie użytkowników są tworzone automatycznie w aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="aeee9-244">Linked Lookup Application supports Just in Time (JIT) user provisioning and after authentication users are created in hello application automatically.</span></span> <span data-ttu-id="aeee9-245">Aktywuj **automatycznie przypisać licencje** tooassign toohello licencji użytkownika.</span><span class="sxs-lookup"><span data-stu-id="aeee9-245">Activate **Automatically assign licenses** tooassign a license toohello user.</span></span>
   
   ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_linkedin_admin_license.png)

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="aeee9-247">Przypisanie użytkownika testowego hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="aeee9-247">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="aeee9-248">W tej sekcji możesz włączyć toouse Simona Britta Azure logowania jednokrotnego za udzielanie dostępu tooLinkedIn wyszukiwania.</span><span class="sxs-lookup"><span data-stu-id="aeee9-248">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooLinkedIn Lookup.</span></span>

![Przypisz użytkownika][200] 

<span data-ttu-id="aeee9-250">**tooassign tooLinkedIn Simona Britta wyszukiwanie, należy wykonać hello następujące kroki:**</span><span class="sxs-lookup"><span data-stu-id="aeee9-250">**tooassign Britta Simon tooLinkedIn Lookup, perform hello following steps:**</span></span>

1. <span data-ttu-id="aeee9-251">W portalu Azure hello, otwórz widok aplikacji hello, a następnie przejdź do widoku katalogu toohello i przejść za**aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="aeee9-251">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Przypisz użytkownika][201] 

2. <span data-ttu-id="aeee9-253">Z listy aplikacji hello wybierz **wyszukiwania LinkedIn**.</span><span class="sxs-lookup"><span data-stu-id="aeee9-253">In hello applications list, select **LinkedIn Lookup**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_linkedInlookup_app.png) 

3. <span data-ttu-id="aeee9-255">W menu powitania po lewej stronie powitania kliknij **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="aeee9-255">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Przypisz użytkownika][202] 

4. <span data-ttu-id="aeee9-257">Kliknij przycisk **Dodaj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="aeee9-257">Click **Add** button.</span></span> <span data-ttu-id="aeee9-258">Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="aeee9-258">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Przypisz użytkownika][203]

5. <span data-ttu-id="aeee9-260">Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** hello listy użytkowników.</span><span class="sxs-lookup"><span data-stu-id="aeee9-260">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="aeee9-261">Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="aeee9-261">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="aeee9-262">Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="aeee9-262">Click **Assign** button on **Add Assignment** dialog.</span></span>

    
### <a name="testing-single-sign-on"></a><span data-ttu-id="aeee9-263">Testowanie rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="aeee9-263">Testing single sign-on</span></span>

<span data-ttu-id="aeee9-264">W tej sekcji można przetestować konfiguracji usługi Azure AD pojedynczego logowania jednokrotnego przy użyciu hello panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="aeee9-264">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="aeee9-265">Po kliknięciu hello wyszukiwania LinkedIn kafelka w hello panelu dostępu należy strony przekierowanego tooOrganizational gdzie masz tooprovide informacje osobowe konta LinkedIn.</span><span class="sxs-lookup"><span data-stu-id="aeee9-265">When you click hello LinkedIn Lookup tile in hello Access Panel, you should be redirected tooOrganizational page where you have tooprovide your personal LinkedIn account details.</span></span> <span data-ttu-id="aeee9-266">Łączy konto osobiste konta firmowego LinkedIn.</span><span class="sxs-lookup"><span data-stu-id="aeee9-266">It links your personal account with your LinkedIn business account.</span></span> 

<span data-ttu-id="aeee9-267">Aby uzyskać więcej informacji na temat panelu dostępu, zobacz [wprowadzenie do panelu dostępu](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="aeee9-267">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="aeee9-268">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="aeee9-268">Additional resources</span></span>

* [<span data-ttu-id="aeee9-269">Lista samouczków dotyczących tooIntegrate aplikacji SaaS w usłudze Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="aeee9-269">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="aeee9-270">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="aeee9-270">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_general_203.png

