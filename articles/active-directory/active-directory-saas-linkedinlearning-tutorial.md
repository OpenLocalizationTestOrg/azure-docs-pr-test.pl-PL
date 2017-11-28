---
title: 'Samouczek: Integracji Azure Active Directory z LinkedIn Learning | Dokumentacja firmy Microsoft'
description: "Dowiedz się, jak tooconfigure logowanie jednokrotne między usługą Azure Active Directory i uczenie się LinkedIn."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: d5857070-bf79-4bd3-9a2a-4c1919a74946
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/15/2017
ms.author: jeedes
ms.openlocfilehash: 14610a25132ed0ccf5892cad6ccc4e1ef03ff280
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-linkedin-learning"></a><span data-ttu-id="994a4-103">Samouczek: Integracji Azure Active Directory z LinkedIn Learning</span><span class="sxs-lookup"><span data-stu-id="994a4-103">Tutorial: Azure Active Directory integration with LinkedIn Learning</span></span>

<span data-ttu-id="994a4-104">Z tego samouczka, dowiesz się, jak toointegrate LinkedIn Learning z usługą Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="994a4-104">In this tutorial, you learn how toointegrate LinkedIn Learning with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="994a4-105">Integrowanie LinkedIn Learning z usługą Azure AD zapewnia hello następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="994a4-105">Integrating LinkedIn Learning with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="994a4-106">Można kontrolować w usłudze Azure AD, kto ma dostęp do tooLinkedIn nauki</span><span class="sxs-lookup"><span data-stu-id="994a4-106">You can control in Azure AD who has access tooLinkedIn Learning</span></span>
- <span data-ttu-id="994a4-107">Można włączyć użytkownika użytkownicy tooautomatically get zalogowane tooLinkedIn Learning (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="994a4-107">You can enable your users tooautomatically get signed-on tooLinkedIn Learning (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="994a4-108">Możesz zarządzać kont w jednej centralnej lokalizacji - hello portalu Azure</span><span class="sxs-lookup"><span data-stu-id="994a4-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="994a4-109">Jeśli chcesz tooknow więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="994a4-109">If you want tooknow more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="994a4-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="994a4-110">Prerequisites</span></span>

<span data-ttu-id="994a4-111">tooconfigure integracji usługi Azure AD przy użyciu LinkedIn Learning należy hello następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="994a4-111">tooconfigure Azure AD integration with LinkedIn Learning, you need hello following items:</span></span>

- <span data-ttu-id="994a4-112">Subskrypcję usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="994a4-112">An Azure AD subscription</span></span>
- <span data-ttu-id="994a4-113">LinkedIn Learning jednokrotnego włączone subskrypcji</span><span class="sxs-lookup"><span data-stu-id="994a4-113">A LinkedIn Learning single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="994a4-114">tootest hello kroków w tym samouczku, zaleca się przy użyciu środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="994a4-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="994a4-115">tootest hello kroki opisane w tym samouczku, należy stosować te zalecenia:</span><span class="sxs-lookup"><span data-stu-id="994a4-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="994a4-116">Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="994a4-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="994a4-117">Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz pobrać miesięczna wersja próbna [tutaj](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="994a4-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="994a4-118">Opis scenariusza</span><span class="sxs-lookup"><span data-stu-id="994a4-118">Scenario description</span></span>
<span data-ttu-id="994a4-119">W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym.</span><span class="sxs-lookup"><span data-stu-id="994a4-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="994a4-120">Scenariusz Hello opisane w tym samouczku składa się z dwóch głównych elementów:</span><span class="sxs-lookup"><span data-stu-id="994a4-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="994a4-121">Dodawanie LinkedIn Learning z galerii hello</span><span class="sxs-lookup"><span data-stu-id="994a4-121">Adding LinkedIn Learning from hello gallery</span></span>
2. <span data-ttu-id="994a4-122">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="994a4-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-linkedin-learning-from-hello-gallery"></a><span data-ttu-id="994a4-123">Dodawanie LinkedIn Learning z galerii hello</span><span class="sxs-lookup"><span data-stu-id="994a4-123">Adding LinkedIn Learning from hello gallery</span></span>
<span data-ttu-id="994a4-124">tooconfigure hello integracji LinkedIn Learning z usługą Azure AD, należy tooadd LinkedIn Learning z hello galerii tooyour listę zarządzanych aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="994a4-124">tooconfigure hello integration of LinkedIn Learning into Azure AD, you need tooadd LinkedIn Learning from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="994a4-125">**tooadd Learning LinkedIn z galerii hello wykonaj hello następujące kroki:**</span><span class="sxs-lookup"><span data-stu-id="994a4-125">**tooadd LinkedIn Learning from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="994a4-126">W hello  **[portalu Azure](https://portal.azure.com)**na temat hello panelu nawigacji po lewej stronie, kliknij przycisk **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="994a4-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Usługa Active Directory][1]

2. <span data-ttu-id="994a4-128">Przejdź za**aplikacje dla przedsiębiorstw**.</span><span class="sxs-lookup"><span data-stu-id="994a4-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="994a4-129">Następnie przejdź zbyt**wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="994a4-129">Then go too**All applications**.</span></span>

    ![Aplikacje][2]
    
3. <span data-ttu-id="994a4-131">Kliknij przycisk **Dodaj** przycisk u góry hello hello okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="994a4-131">Click **Add** button on hello top of hello dialog.</span></span>

    ![Aplikacje][3]

4. <span data-ttu-id="994a4-133">W polu wyszukiwania hello wpisz **LinkedIn Learning**.</span><span class="sxs-lookup"><span data-stu-id="994a4-133">In hello search box, type **LinkedIn Learning**.</span></span> <span data-ttu-id="994a4-134">Z poziomu panelu wyników, kliknij przycisk **LinkedIn Learning** tooadd hello aplikacji.</span><span class="sxs-lookup"><span data-stu-id="994a4-134">From results panel, click **LinkedIn Learning** tooadd hello application.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-linkedinlearning-tutorial/tutorial-linkedinlearning_000.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="994a4-136">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="994a4-136">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="994a4-137">W tej sekcji skonfigurować i przetestować usługi Azure AD logowania jednokrotnego przy użyciu Learning LinkedIn w oparciu o nazwie "Britta Simona" użytkownika testowego.</span><span class="sxs-lookup"><span data-stu-id="994a4-137">In this section, you configure and test Azure AD single sign-on with LinkedIn Learning based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="994a4-138">Dla pojedynczego logowania jednokrotnego toowork usługi Azure AD musi tooknow użytkownika odpowiednikiem hello w uczeniu LinkedIn jest tooa użytkownika w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="994a4-138">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in LinkedIn Learning is tooa user in Azure AD.</span></span> <span data-ttu-id="994a4-139">Innymi słowy relację łącza między użytkownika usługi Azure AD i hello użytkownikowi w uczeniu LinkedIn musi toobe ustanowione.</span><span class="sxs-lookup"><span data-stu-id="994a4-139">In other words, a link relationship between an Azure AD user and hello related user in LinkedIn Learning needs toobe established.</span></span>

<span data-ttu-id="994a4-140">Ta relacja łącza zostanie nawiązane, przypisując wartość hello hello **nazwy użytkownika** w usłudze Azure AD jako wartość hello hello **Username** w uczeniu LinkedIn.</span><span class="sxs-lookup"><span data-stu-id="994a4-140">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in LinkedIn Learning.</span></span>

<span data-ttu-id="994a4-141">tooconfigure i testowych usługi Azure AD logowania jednokrotnego przy użyciu LinkedIn Learning, należy po bloków konstrukcyjnych hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="994a4-141">tooconfigure and test Azure AD single sign-on with LinkedIn Learning, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="994a4-142">**[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configuring-azure-ad-single-sign-on)**  -tooenable Twojego toouse użytkowników tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="994a4-142">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="994a4-143">**[Tworzenie użytkownika testowego usługi Azure AD](#creating-an-azure-ad-test-user)**  -tootest usługi Azure AD rejestracji jednokrotnej z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="994a4-143">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="994a4-144">**[Tworzenie użytkownika testowego LinkedIn Learning](#creating-a-linkedin-learning-test-user)**  -tootest usługi Azure AD rejestracji jednokrotnej z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="994a4-144">**[Creating a LinkedIn Learning test user](#creating-a-linkedin-learning-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
4. <span data-ttu-id="994a4-145">**[Przypisanie użytkownika testowego hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Simona Britta toouse usługi Azure AD rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="994a4-145">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="994a4-146">**[Testowanie rejestracji jednokrotnej](#testing-single-sign-on)**  -tooverify czy hello konfiguracji działania.</span><span class="sxs-lookup"><span data-stu-id="994a4-146">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="994a4-147">Konfigurowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="994a4-147">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="994a4-148">W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w hello portalu Azure i skonfigurować rejestracji jednokrotnej w aplikacji LinkedIn Learning.</span><span class="sxs-lookup"><span data-stu-id="994a4-148">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your LinkedIn Learning application.</span></span>

<span data-ttu-id="994a4-149">**tooconfigure usługi Azure AD logowania jednokrotnego przy użyciu LinkedIn Learning wykonaj hello następujące kroki:**</span><span class="sxs-lookup"><span data-stu-id="994a4-149">**tooconfigure Azure AD single sign-on with LinkedIn Learning, perform hello following steps:**</span></span>

1. <span data-ttu-id="994a4-150">W portalu Azure na powitania hello **LinkedIn Learning** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.</span><span class="sxs-lookup"><span data-stu-id="994a4-150">In hello Azure portal, on hello **LinkedIn Learning** application integration page, click **Single sign-on**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej][4]

2. <span data-ttu-id="994a4-152">Na powitania **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** tooenable rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="994a4-152">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-linkedinlearning-tutorial/tutorial-linkedin_01.png)

3. <span data-ttu-id="994a4-154">W oknie przeglądarki innej witryny sieci web, logowania jednokrotnego tooyour LinkedIn Learning dzierżawy z uprawnieniami administratora.</span><span class="sxs-lookup"><span data-stu-id="994a4-154">In a different web browser window, sign-on tooyour LinkedIn Learning tenant as an administrator.</span></span>

4. <span data-ttu-id="994a4-155">W **Centrum konta**, kliknij przycisk **ustawienia globalne** w obszarze **ustawienia**.</span><span class="sxs-lookup"><span data-stu-id="994a4-155">In **Account Center**, click **Global Settings** under **Settings**.</span></span> <span data-ttu-id="994a4-156">Zaznacz również **Learning - domyślne** z listy rozwijanej hello.</span><span class="sxs-lookup"><span data-stu-id="994a4-156">Also, select **Learning - Default** from hello dropdown list.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-linkedinlearning-tutorial/tutorial_linkedin_admin_01.png)

5. <span data-ttu-id="994a4-158">Kliknij przycisk **lub kliknij tutaj tooload i skopiuj poszczególnych pól formularza hello** i skopiuj **identyfikator jednostki** i **adresu Url potwierdzenia konsumenta dostępu (ACS)**</span><span class="sxs-lookup"><span data-stu-id="994a4-158">Click **OR Click Here tooload and copy individual fields from hello form** and copy **Entity Id** and **Assertion Consumer Access (ACS) Url**</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-linkedinlearning-tutorial/tutorial_linkedin_admin_03.png)

6. <span data-ttu-id="994a4-160">W portalu Azure w obszarze **domeny Learning LinkedIn i adres URL**, wykonaj następujące kroki, jeśli chcesz, aby tooconfigure logowania jednokrotnego hello w **inicjowane IdP** tryb</span><span class="sxs-lookup"><span data-stu-id="994a4-160">On Azure portal, under **LinkedIn Learning Domain and URLs**, perform hello following steps if you want tooconfigure SSO in **IdP Initiated** mode</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-linkedinlearning-tutorial/tutorial_linkedin_signon_01.png)

    <span data-ttu-id="994a4-162">a.</span><span class="sxs-lookup"><span data-stu-id="994a4-162">a.</span></span> <span data-ttu-id="994a4-163">W hello **identyfikator** pole tekstowe, wprowadź hello **identyfikator jednostki** skopiowany z portalu LinkedIn</span><span class="sxs-lookup"><span data-stu-id="994a4-163">In hello **Identifier** textbox, enter hello **Entity ID** copied from LinkedIn Portal</span></span> 

    <span data-ttu-id="994a4-164">b.</span><span class="sxs-lookup"><span data-stu-id="994a4-164">b.</span></span> <span data-ttu-id="994a4-165">W hello **adres URL odpowiedzi** pole tekstowe, wprowadź hello **potwierdzenia konsumenta dostępu (ACS) adres Url** skopiowany z portalu LinkedIn</span><span class="sxs-lookup"><span data-stu-id="994a4-165">In hello **Reply URL** textbox, enter hello **Assertion Consumer Access (ACS) Url** copied from LinkedIn Portal</span></span>

7. <span data-ttu-id="994a4-166">Jeśli chcesz, aby tooconfigure logowania jednokrotnego w **inicjowane SP**, następnie kliknij opcję Ustawienia Pokaż zaawansowane adres URL w sekcji konfiguracji hello i skonfigurować hello adres URL logowania z hello następującego wzorca:</span><span class="sxs-lookup"><span data-stu-id="994a4-166">If you want tooconfigure SSO in **SP Initiated**, then click Show Advanced URL setting option in hello configuration section and configure hello sign-on URL with hello following pattern:</span></span>

    `https://www.linkedin.com/checkpoint/enterprise/login/<AccountId>?application=learning&applicationInstanceId=<InstanceId>`

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-linkedinlearning-tutorial/tutorial_linkedin_signon_02.png)   
    
8. <span data-ttu-id="994a4-168">Aplikacja LinkedIn Learning oczekuje potwierdzenia SAML hello w określonym formacie wymaga możesz tooadd atrybutu niestandardowego mapowania tooyour SAML tokenu atrybuty konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="994a4-168">Your LinkedIn Learning application expects hello SAML assertions in a specific format, which requires you tooadd custom attribute mappings tooyour SAML token attributes configuration.</span></span> <span data-ttu-id="994a4-169">powitania po zrzut ekranu przedstawia przykład tego.</span><span class="sxs-lookup"><span data-stu-id="994a4-169">hello following screenshot shows an example for this.</span></span> <span data-ttu-id="994a4-170">Witaj wartość domyślną **identyfikator użytkownika** jest **user.userprincipalname** , ale ten toobe zamapowana adres e-mail użytkownika hello oczekuje LinkedIn Learning.</span><span class="sxs-lookup"><span data-stu-id="994a4-170">hello default value of **User Identifier** is **user.userprincipalname** but LinkedIn Learning expects this toobe mapped with hello user's email address.</span></span> <span data-ttu-id="994a4-171">W przypadku którego można użyć **user.mail** atrybutu z listy hello lub użyj wartości atrybutu odpowiednie hello zgodnie z konfiguracją organizacji.</span><span class="sxs-lookup"><span data-stu-id="994a4-171">For that you can use **user.mail** attribute from hello list or use hello appropriate attribute value based on your organization configuration.</span></span> 

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-linkedinlearning-tutorial/updateusermail.png)
    
9. <span data-ttu-id="994a4-173">W **atrybuty użytkownika** kliknij **widoku i edytować wszystkie atrybuty użytkowników** i ustaw hello atrybuty.</span><span class="sxs-lookup"><span data-stu-id="994a4-173">In **User Attributes** section, click **View and edit all other user attributes** and set hello attributes.</span></span> <span data-ttu-id="994a4-174">Hello użytkownik powinien tooadd oświadczeń cztery o nazwie **e-mail**, **działu**, **imię**, i **nazwisko** i wartość hello jest zamapowana z toobe **user.mail**, **user.department**, **user.givenname**, i **user.surname** odpowiednio</span><span class="sxs-lookup"><span data-stu-id="994a4-174">hello user needs tooadd four claims named **email**, **department**, **firstname**, and **lastname** and hello value is toobe mapped with **user.mail**, **user.department**, **user.givenname**, and **user.surname** respectively</span></span>

    | <span data-ttu-id="994a4-175">Nazwa atrybutu</span><span class="sxs-lookup"><span data-stu-id="994a4-175">Attribute Name</span></span> | <span data-ttu-id="994a4-176">Wartość atrybutu</span><span class="sxs-lookup"><span data-stu-id="994a4-176">Attribute Value</span></span> |
    | --- | --- |
    | <span data-ttu-id="994a4-177">Adres e-mail</span><span class="sxs-lookup"><span data-stu-id="994a4-177">email</span></span>| <span data-ttu-id="994a4-178">User.mail</span><span class="sxs-lookup"><span data-stu-id="994a4-178">user.mail</span></span> |    
    | <span data-ttu-id="994a4-179">Dział</span><span class="sxs-lookup"><span data-stu-id="994a4-179">department</span></span>| <span data-ttu-id="994a4-180">User.Department</span><span class="sxs-lookup"><span data-stu-id="994a4-180">user.department</span></span> |
    | <span data-ttu-id="994a4-181">Imię</span><span class="sxs-lookup"><span data-stu-id="994a4-181">firstname</span></span>| <span data-ttu-id="994a4-182">User.givenName</span><span class="sxs-lookup"><span data-stu-id="994a4-182">user.givenname</span></span> |
    | <span data-ttu-id="994a4-183">nazwisko</span><span class="sxs-lookup"><span data-stu-id="994a4-183">lastname</span></span>| <span data-ttu-id="994a4-184">User.surname</span><span class="sxs-lookup"><span data-stu-id="994a4-184">user.surname</span></span> |
    
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-linkedinlearning-tutorial/userattribute.png)
    
    <span data-ttu-id="994a4-186">a.</span><span class="sxs-lookup"><span data-stu-id="994a4-186">a.</span></span> <span data-ttu-id="994a4-187">Kliknij przycisk **Dodawanie atrybutu** tooopen hello atrybutu w oknie dialogowym.</span><span class="sxs-lookup"><span data-stu-id="994a4-187">Click **Add Attribute** tooopen hello attribute dialog.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-linkedinLearning-tutorial/tutorial_attribute_04.png)

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-linkedinLearning-tutorial/tutorial_attribute_05.png)
    
    <span data-ttu-id="994a4-190">b.</span><span class="sxs-lookup"><span data-stu-id="994a4-190">b.</span></span> <span data-ttu-id="994a4-191">W hello **nazwa** pole tekstowe, nazwa atrybutu hello typu wyświetlany dla danego wiersza.</span><span class="sxs-lookup"><span data-stu-id="994a4-191">In hello **Name** textbox, type hello attribute name shown for that row.</span></span>
    
    <span data-ttu-id="994a4-192">c.</span><span class="sxs-lookup"><span data-stu-id="994a4-192">c.</span></span> <span data-ttu-id="994a4-193">Z hello **wartość** listy wartości atrybutu hello typ wyświetlanego dla tego wiersza.</span><span class="sxs-lookup"><span data-stu-id="994a4-193">From hello **Value** list, type hello attribute value shown for that row.</span></span>
    
    <span data-ttu-id="994a4-194">d.</span><span class="sxs-lookup"><span data-stu-id="994a4-194">d.</span></span> <span data-ttu-id="994a4-195">Kliknij przycisk **Ok**</span><span class="sxs-lookup"><span data-stu-id="994a4-195">Click **Ok**</span></span>

10. <span data-ttu-id="994a4-196">Wykonaj następujące kroki na powitania hello **nazwa** — atrybut</span><span class="sxs-lookup"><span data-stu-id="994a4-196">Perform hello following steps on hello **name** attribute-</span></span>

    <span data-ttu-id="994a4-197">a.</span><span class="sxs-lookup"><span data-stu-id="994a4-197">a.</span></span> <span data-ttu-id="994a4-198">Polecenie hello atrybutu tooopen hello **atrybutu Edytuj** okna.</span><span class="sxs-lookup"><span data-stu-id="994a4-198">Click on hello attribute tooopen hello **Edit Attribute** window.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-linkedinLearning-tutorial/url_update.png)

    <span data-ttu-id="994a4-200">b.</span><span class="sxs-lookup"><span data-stu-id="994a4-200">b.</span></span> <span data-ttu-id="994a4-201">Usuń wartość adresu URL hello z hello **przestrzeni nazw**.</span><span class="sxs-lookup"><span data-stu-id="994a4-201">Delete hello URL value from hello **namespace**.</span></span>
    
    <span data-ttu-id="994a4-202">c.</span><span class="sxs-lookup"><span data-stu-id="994a4-202">c.</span></span> <span data-ttu-id="994a4-203">Kliknij przycisk **Ok** toosave hello ustawienie.</span><span class="sxs-lookup"><span data-stu-id="994a4-203">Click **Ok** toosave hello setting.</span></span>

11. <span data-ttu-id="994a4-204">Na powitania **certyfikat podpisywania SAML** kliknij **XML metadanych** , a następnie zapisz plik XML hello na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="994a4-204">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello XML file on your computer.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-linkedinlearning-tutorial/tutorial-linkedinlearning_certificate.png) 

12. <span data-ttu-id="994a4-206">Kliknij pozycję **Zapisz**.</span><span class="sxs-lookup"><span data-stu-id="994a4-206">Click **Save**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-linkedinlearning-tutorial/tutorial_general_400.png)

13. <span data-ttu-id="994a4-208">Przejdź za**ustawienia administratora LinkedIn** sekcji.</span><span class="sxs-lookup"><span data-stu-id="994a4-208">Go too**LinkedIn Admin Settings** section.</span></span> <span data-ttu-id="994a4-209">Przekaż hello pliku XML, który został pobrany z hello portalu Azure, klikając opcję pliku XML, Przekaż hello.</span><span class="sxs-lookup"><span data-stu-id="994a4-209">Upload hello XML file you downloaded from hello Azure portal by clicking hello Upload XML file option.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-linkedinlearning-tutorial/tutorial_linkedin_metadata_03.png)

14. <span data-ttu-id="994a4-211">Kliknij przycisk **na** tooenable logowania jednokrotnego.</span><span class="sxs-lookup"><span data-stu-id="994a4-211">Click **On** tooenable SSO.</span></span> <span data-ttu-id="994a4-212">Zmiany stanu rejestracji Jednokrotnej z **niepołączone** zbyt**połączony**</span><span class="sxs-lookup"><span data-stu-id="994a4-212">SSO status changes from **Not Connected** too**Connected**</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-linkedinlearning-tutorial/tutorial_linkedin_admin_05.png)

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="994a4-214">Tworzenie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="994a4-214">Creating an Azure AD test user</span></span>
<span data-ttu-id="994a4-215">Celem Hello w tej sekcji jest toocreate użytkownika testowego, w portalu Azure o nazwie Simona Britta hello.</span><span class="sxs-lookup"><span data-stu-id="994a4-215">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Tworzenie użytkowników usługi Azure AD][100]

<span data-ttu-id="994a4-217">**toocreate użytkownika testowego w usłudze Azure AD, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="994a4-217">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="994a4-218">W hello **portalu Azure**na temat hello w lewym okienku nawigacji, kliknij przycisk **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="994a4-218">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-linkedinlearning-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="994a4-220">toodisplay hello listę użytkowników, przejdź zbyt**użytkowników i grup** i kliknij przycisk **wszyscy użytkownicy**.</span><span class="sxs-lookup"><span data-stu-id="994a4-220">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-linkedinlearning-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="994a4-222">Witaj tooopen **użytkownika** okna dialogowego, kliknij przycisk **Dodaj** u góry hello hello okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="994a4-222">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-linkedinlearning-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="994a4-224">Na powitania **użytkownika** okna dialogowego wykonaj hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="994a4-224">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-linkedinlearning-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="994a4-226">a.</span><span class="sxs-lookup"><span data-stu-id="994a4-226">a.</span></span> <span data-ttu-id="994a4-227">W hello **nazwa** pole tekstowe, typ **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="994a4-227">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="994a4-228">b.</span><span class="sxs-lookup"><span data-stu-id="994a4-228">b.</span></span> <span data-ttu-id="994a4-229">W hello **nazwy użytkownika** pole tekstowe, hello typu **adres e-mail** z BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="994a4-229">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="994a4-230">c.</span><span class="sxs-lookup"><span data-stu-id="994a4-230">c.</span></span> <span data-ttu-id="994a4-231">Wybierz **Pokaż hasło** i zanotuj wartość hello hello **hasło**.</span><span class="sxs-lookup"><span data-stu-id="994a4-231">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="994a4-232">d.</span><span class="sxs-lookup"><span data-stu-id="994a4-232">d.</span></span> <span data-ttu-id="994a4-233">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="994a4-233">Click **Create**.</span></span> 

### <a name="creating-a-linkedin-learning-test-user"></a><span data-ttu-id="994a4-234">Tworzenie użytkownika testowego LinkedIn Learning</span><span class="sxs-lookup"><span data-stu-id="994a4-234">Creating a LinkedIn Learning test user</span></span>

<span data-ttu-id="994a4-235">Obsługuje połączonych aplikacji Learning.</span><span class="sxs-lookup"><span data-stu-id="994a4-235">Linked Learning Application supports.</span></span> <span data-ttu-id="994a4-236">Tylko na czas Inicjowanie obsługi użytkowników, a następnie uwierzytelniania użytkowników są tworzone automatycznie w aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="994a4-236">Just in time user provisioning and after authentication users are created in hello application automatically.</span></span> <span data-ttu-id="994a4-237">Na stronie Ustawienia administratora hello na przełączniku portalu hello przerzucania LinkedIn Learning hello **automatycznie przypisywać licencje** tooactive tooenable tylko w czasie inicjowania obsługi administracyjnej i to również przypisać licencję użytkownika toohello.</span><span class="sxs-lookup"><span data-stu-id="994a4-237">On hello admin settings page on hello LinkedIn Learning portal flip hello switch **Automatically Assign licenses** tooactive tooenable Just in time provisioning and this will also assign a license toohello user.</span></span>
   
   ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-linkedinLearning-tutorial/LinkedinUserprovswitch.png)

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="994a4-239">Przypisanie użytkownika testowego hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="994a4-239">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="994a4-240">W tej sekcji, Włącz toouse Simona Britta Azure logowania jednokrotnego za udzielanie dostępu tooLinkedIn Learning.</span><span class="sxs-lookup"><span data-stu-id="994a4-240">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooLinkedIn Learning.</span></span>

![Przypisz użytkownika][200] 

<span data-ttu-id="994a4-242">**tooassign tooLinkedIn Simona Britta uczenia, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="994a4-242">**tooassign Britta Simon tooLinkedIn Learning, perform hello following steps:**</span></span>

1. <span data-ttu-id="994a4-243">W portalu Azure hello, otwórz widok aplikacji hello, a następnie przejdź do widoku katalogu toohello i przejść za**aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="994a4-243">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Przypisz użytkownika][201] 

2. <span data-ttu-id="994a4-245">Z listy aplikacji hello wybierz **LinkedIn Learning**.</span><span class="sxs-lookup"><span data-stu-id="994a4-245">In hello applications list, select **LinkedIn Learning**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-linkedinlearning-tutorial/tutorial-linkedinlearning_0001.png) 

3. <span data-ttu-id="994a4-247">W menu powitania po lewej stronie powitania kliknij **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="994a4-247">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Przypisz użytkownika][202] 

4. <span data-ttu-id="994a4-249">Kliknij przycisk **Dodaj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="994a4-249">Click **Add** button.</span></span> <span data-ttu-id="994a4-250">Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="994a4-250">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Przypisz użytkownika][203]

5. <span data-ttu-id="994a4-252">Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** hello listy użytkowników.</span><span class="sxs-lookup"><span data-stu-id="994a4-252">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="994a4-253">Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="994a4-253">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="994a4-254">Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="994a4-254">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="994a4-255">Testowanie rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="994a4-255">Testing single sign-on</span></span>

<span data-ttu-id="994a4-256">W tej sekcji można przetestować konfiguracji usługi Azure AD pojedynczego logowania jednokrotnego przy użyciu hello panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="994a4-256">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="994a4-257">Po kliknięciu kafelka LinkedIn Learning hello w hello Panel dostępu, należy pobrać hello Azure logowania jednokrotnego strony i na po pomyślnym logowania, należy pobrać do aplikacji LinkedIn Learning.</span><span class="sxs-lookup"><span data-stu-id="994a4-257">When you click hello LinkedIn Learning tile in hello Access Panel, you should get hello Azure Sign-on page and on after successful sign-on, you should get into your LinkedIn Learning application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="994a4-258">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="994a4-258">Additional resources</span></span>

* [<span data-ttu-id="994a4-259">Lista samouczków dotyczących tooIntegrate aplikacji SaaS w usłudze Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="994a4-259">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="994a4-260">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="994a4-260">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-linkedinlearning-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-linkedinlearning-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-linkedinlearning-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-linkedinlearning-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-linkedinlearning-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-linkedinlearning-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-linkedinlearning-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-linkedinlearning-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-linkedinlearning-tutorial/tutorial_general_203.png