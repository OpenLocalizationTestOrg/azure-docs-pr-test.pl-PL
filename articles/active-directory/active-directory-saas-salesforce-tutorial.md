---
title: "Samouczek: Integracji Azure Active Directory z usług Salesforce | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak tooconfigure logowanie jednokrotne między usługą Azure Active Directory i Salesforce."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: d2d7d420-dc91-41b8-a6b3-59579e043b35
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/19/2017
ms.author: jeedes
ms.openlocfilehash: 1d848518ee30910e051cdc4746c599219f3b5a3b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-salesforce"></a><span data-ttu-id="5bc5f-103">Samouczek: Integracji Azure Active Directory z usług Salesforce</span><span class="sxs-lookup"><span data-stu-id="5bc5f-103">Tutorial: Azure Active Directory integration with Salesforce</span></span>

<span data-ttu-id="5bc5f-104">Z tego samouczka, dowiesz się, jak toointegrate Salesforce z usługą Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="5bc5f-104">In this tutorial, you learn how toointegrate Salesforce with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="5bc5f-105">Integrowanie usługi Salesforce z usługą Azure AD zapewnia hello następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="5bc5f-105">Integrating Salesforce with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="5bc5f-106">Można kontrolować w usłudze Azure AD, kto ma dostęp do tooSalesforce</span><span class="sxs-lookup"><span data-stu-id="5bc5f-106">You can control in Azure AD who has access tooSalesforce</span></span>
- <span data-ttu-id="5bc5f-107">Można włączyć użytkownika użytkownicy tooautomatically get zalogowane tooSalesforce (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="5bc5f-107">You can enable your users tooautomatically get signed-on tooSalesforce (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="5bc5f-108">Możesz zarządzać kont w jednej centralnej lokalizacji - hello portalu Azure</span><span class="sxs-lookup"><span data-stu-id="5bc5f-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="5bc5f-109">Jeśli chcesz tooknow więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="5bc5f-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="5bc5f-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="5bc5f-110">Prerequisites</span></span>

<span data-ttu-id="5bc5f-111">tooconfigure integracji usługi Azure AD z usług Salesforce, należy hello następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="5bc5f-111">tooconfigure Azure AD integration with Salesforce, you need hello following items:</span></span>

- <span data-ttu-id="5bc5f-112">Subskrypcję usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="5bc5f-112">An Azure AD subscription</span></span>
- <span data-ttu-id="5bc5f-113">Salesforce jednokrotnego włączone subskrypcji</span><span class="sxs-lookup"><span data-stu-id="5bc5f-113">A Salesforce single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="5bc5f-114">tootest hello kroków w tym samouczku, zaleca się przy użyciu środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="5bc5f-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="5bc5f-115">tootest hello kroki opisane w tym samouczku, należy stosować te zalecenia:</span><span class="sxs-lookup"><span data-stu-id="5bc5f-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="5bc5f-116">Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="5bc5f-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="5bc5f-117">Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz pobrać miesięczna wersja próbna [tutaj](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="5bc5f-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="5bc5f-118">Opis scenariusza</span><span class="sxs-lookup"><span data-stu-id="5bc5f-118">Scenario description</span></span>
<span data-ttu-id="5bc5f-119">W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym.</span><span class="sxs-lookup"><span data-stu-id="5bc5f-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="5bc5f-120">Scenariusz Hello opisane w tym samouczku składa się z dwóch głównych elementów:</span><span class="sxs-lookup"><span data-stu-id="5bc5f-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="5bc5f-121">Dodawanie usługi Salesforce z galerii hello</span><span class="sxs-lookup"><span data-stu-id="5bc5f-121">Adding Salesforce from hello gallery</span></span>
2. <span data-ttu-id="5bc5f-122">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="5bc5f-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-salesforce-from-hello-gallery"></a><span data-ttu-id="5bc5f-123">Dodawanie usługi Salesforce z galerii hello</span><span class="sxs-lookup"><span data-stu-id="5bc5f-123">Adding Salesforce from hello gallery</span></span>
<span data-ttu-id="5bc5f-124">tooconfigure hello integracji usługi Salesforce z usługą Azure AD, należy tooadd Salesforce z hello galerii tooyour listę zarządzanych aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="5bc5f-124">tooconfigure hello integration of Salesforce into Azure AD, you need tooadd Salesforce from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="5bc5f-125">**tooadd Salesforce z galerii hello wykonaj hello następujące kroki:**</span><span class="sxs-lookup"><span data-stu-id="5bc5f-125">**tooadd Salesforce from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="5bc5f-126">W hello  **[portalu Azure](https://portal.azure.com)**na temat hello panelu nawigacji po lewej stronie, kliknij przycisk **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="5bc5f-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Usługa Active Directory][1]

2. <span data-ttu-id="5bc5f-128">Przejdź za**aplikacje dla przedsiębiorstw**.</span><span class="sxs-lookup"><span data-stu-id="5bc5f-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="5bc5f-129">Następnie przejdź zbyt**wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="5bc5f-129">Then go too**All applications**.</span></span>

    ![Aplikacje][2]
    
3. <span data-ttu-id="5bc5f-131">Kliknij przycisk **nowej aplikacji** przycisk u góry hello hello okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="5bc5f-131">Click **New application** button on hello top of hello dialog.</span></span>

    ![Aplikacje][3]

4. <span data-ttu-id="5bc5f-133">W polu wyszukiwania hello wpisz **Salesforce**.</span><span class="sxs-lookup"><span data-stu-id="5bc5f-133">In hello search box, type **Salesforce**.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-salesforce-tutorial/tutorial_salesforce_search.png)

5. <span data-ttu-id="5bc5f-135">W panelu wyników hello, wybierz **Salesforce**, a następnie kliknij przycisk **Dodaj** przycisk tooadd hello aplikacji.</span><span class="sxs-lookup"><span data-stu-id="5bc5f-135">In hello results panel, select **Salesforce**, and then click **Add** button tooadd hello application.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-salesforce-tutorial/tutorial_salesforce_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="5bc5f-137">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="5bc5f-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="5bc5f-138">W tej sekcji możesz skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z Salesforce na podstawie użytkownika testowego, nazywany "Britta Simona".</span><span class="sxs-lookup"><span data-stu-id="5bc5f-138">In this section, you configure and test Azure AD single sign-on with Salesforce based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="5bc5f-139">Dla pojedynczego logowania jednokrotnego toowork usługi Azure AD musi tooknow hello odpowiednikiem użytkownika w usłudze Salesforce jest tooa użytkownika w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="5bc5f-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Salesforce is tooa user in Azure AD.</span></span> <span data-ttu-id="5bc5f-140">Innymi słowy relację łącza między użytkownika usługi Azure AD i hello użytkownikowi w usłudze Salesforce musi toobe ustanowione.</span><span class="sxs-lookup"><span data-stu-id="5bc5f-140">In other words, a link relationship between an Azure AD user and hello related user in Salesforce needs toobe established.</span></span>

<span data-ttu-id="5bc5f-141">Ta relacja łącza zostanie nawiązane, przypisując wartość hello hello **nazwy użytkownika** w usłudze Azure AD jako wartość hello hello **Username** w usłudze Salesforce.</span><span class="sxs-lookup"><span data-stu-id="5bc5f-141">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in Salesforce.</span></span>

<span data-ttu-id="5bc5f-142">tooconfigure i testowych usługi Azure AD rejestracji jednokrotnej z usług Salesforce, należy po bloków konstrukcyjnych hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="5bc5f-142">tooconfigure and test Azure AD single sign-on with Salesforce, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="5bc5f-143">**[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configuring-azure-ad-single-sign-on)**  -tooenable Twojego toouse użytkowników tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="5bc5f-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="5bc5f-144">**[Tworzenie użytkownika testowego usługi Azure AD](#creating-an-azure-ad-test-user)**  -tootest usługi Azure AD rejestracji jednokrotnej z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="5bc5f-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="5bc5f-145">**[Tworzenie użytkownika testowego Salesforce](#creating-a-salesforce-test-user)**  -toohave odpowiednikiem Simona Britta w usłudze Salesforce, który jest połączony toohello usługi Azure AD reprezentację użytkownika.</span><span class="sxs-lookup"><span data-stu-id="5bc5f-145">**[Creating a Salesforce test user](#creating-a-salesforce-test-user)** - toohave a counterpart of Britta Simon in Salesforce that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="5bc5f-146">**[Przypisanie użytkownika testowego hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Simona Britta toouse usługi Azure AD rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="5bc5f-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="5bc5f-147">**[Testowanie rejestracji jednokrotnej](#testing-single-sign-on)**  -tooverify czy hello konfiguracji działania.</span><span class="sxs-lookup"><span data-stu-id="5bc5f-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="5bc5f-148">Konfigurowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="5bc5f-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="5bc5f-149">W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w portalu Azure hello i skonfigurować logowanie jednokrotne w aplikacji Salesforce.</span><span class="sxs-lookup"><span data-stu-id="5bc5f-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Salesforce application.</span></span>

<span data-ttu-id="5bc5f-150">**tooconfigure usługi Azure AD rejestracji jednokrotnej z usług Salesforce, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="5bc5f-150">**tooconfigure Azure AD single sign-on with Salesforce, perform hello following steps:**</span></span>

1. <span data-ttu-id="5bc5f-151">W portalu Azure na powitania hello **Salesforce** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.</span><span class="sxs-lookup"><span data-stu-id="5bc5f-151">In hello Azure portal, on hello **Salesforce** application integration page, click **Single sign-on**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej][4]

2. <span data-ttu-id="5bc5f-153">Na powitania **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** tooenable rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="5bc5f-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-salesforce-tutorial/tutorial_salesforce_samlbase.png)

3. <span data-ttu-id="5bc5f-155">Na powitania **domeny Salesforce i adres URL** sekcji, wykonaj następujące kroki hello:</span><span class="sxs-lookup"><span data-stu-id="5bc5f-155">On hello **Salesforce Domain and URLs** section, perform hello following steps:</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-salesforce-tutorial/tutorial_salesforce_url.png)

    <span data-ttu-id="5bc5f-157">W hello **adres URL logowania** pole tekstowe, wartość hello typu przy użyciu hello następującego wzorca:</span><span class="sxs-lookup"><span data-stu-id="5bc5f-157">In hello **Sign-on URL** textbox, type hello value using hello following pattern:</span></span> 
   * <span data-ttu-id="5bc5f-158">Konto przedsiębiorstwa:`https://<subdomain>.my.salesforce.com`</span><span class="sxs-lookup"><span data-stu-id="5bc5f-158">Enterprise account: `https://<subdomain>.my.salesforce.com`</span></span>
   * <span data-ttu-id="5bc5f-159">Konta dewelopera:`https://<subdomain>-dev-ed.my.salesforce.com`</span><span class="sxs-lookup"><span data-stu-id="5bc5f-159">Developer account: `https://<subdomain>-dev-ed.my.salesforce.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="5bc5f-160">Wartości te nie są hello prawdziwe.</span><span class="sxs-lookup"><span data-stu-id="5bc5f-160">These values are not hello real.</span></span> <span data-ttu-id="5bc5f-161">Z hello rzeczywisty adres URL logowania, należy zaktualizować te wartości.</span><span class="sxs-lookup"><span data-stu-id="5bc5f-161">Update these values with hello actual Sign-on URL.</span></span> <span data-ttu-id="5bc5f-162">Skontaktuj się z [zespołem pomocy technicznej klienta usług Salesforce](https://help.salesforce.com/support) tooget tych wartości.</span><span class="sxs-lookup"><span data-stu-id="5bc5f-162">Contact [Salesforce Client support team](https://help.salesforce.com/support) tooget these values.</span></span> 
 
4. <span data-ttu-id="5bc5f-163">Na powitania **certyfikat podpisywania SAML** kliknij **certyfikatu** , a następnie zapisz plik certyfikatu hello na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="5bc5f-163">On hello **SAML Signing Certificate** section, click **Certificate** and then save hello certificate file on your computer.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-salesforce-tutorial/tutorial_salesforce_certificate.png) 

5. <span data-ttu-id="5bc5f-165">Kliknij przycisk **zapisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="5bc5f-165">Click **Save** button.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-salesforce-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="5bc5f-167">Na powitania **konfiguracji Salesforce** , kliknij przycisk **skonfigurować Salesforce** tooopen **Konfigurowanie logowania jednokrotnego** okna.</span><span class="sxs-lookup"><span data-stu-id="5bc5f-167">On hello **Salesforce Configuration** section, click **Configure Salesforce** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="5bc5f-168">Kopiuj hello **identyfikator jednostki SAML i SAML pojedynczy znak na adres URL usługi** z hello **sekcji krótkimi opisami.**</span><span class="sxs-lookup"><span data-stu-id="5bc5f-168">Copy hello **SAML Entity ID and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span> 

    <span data-ttu-id="5bc5f-169">![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-salesforce-tutorial/tutorial_salesforce_configure.png) 
<CS></span><span class="sxs-lookup"><span data-stu-id="5bc5f-169">![Configure Single Sign-On](./media/active-directory-saas-salesforce-tutorial/tutorial_salesforce_configure.png) 
<CS></span></span>
7.  <span data-ttu-id="5bc5f-170">Otwórz nową kartę w przeglądarce i zaloguj tooyour konto administratora usług Salesforce.</span><span class="sxs-lookup"><span data-stu-id="5bc5f-170">Open a new tab in your browser and log in tooyour Salesforce administrator account.</span></span>

8.  <span data-ttu-id="5bc5f-171">W obszarze hello **administratora** okienka nawigacji kliknij **kontroli bezpieczeństwa** tooexpand hello związane z sekcji.</span><span class="sxs-lookup"><span data-stu-id="5bc5f-171">Under hello **Administrator** navigation pane, click **Security Controls** tooexpand hello related section.</span></span> <span data-ttu-id="5bc5f-172">Następnie kliknij przycisk **ustawień rejestracji jednokrotnej**.</span><span class="sxs-lookup"><span data-stu-id="5bc5f-172">Then click **Single Sign-On Settings**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-salesforce-tutorial/sf-admin-sso.png)

9.  <span data-ttu-id="5bc5f-174">Na powitania **ustawień rejestracji jednokrotnej** kliknij przycisk hello **Edytuj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="5bc5f-174">On hello **Single Sign-On Settings** page, click hello **Edit** button.</span></span>
    <span data-ttu-id="5bc5f-175">![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-salesforce-tutorial/sf-admin-sso-edit.png)</span><span class="sxs-lookup"><span data-stu-id="5bc5f-175">![Configure Single Sign-On](./media/active-directory-saas-salesforce-tutorial/sf-admin-sso-edit.png)</span></span>

      > [!NOTE]
      > <span data-ttu-id="5bc5f-176">Jeśli użytkownik tooenable rejestracji jednokrotnej ustawienia konta usług Salesforce, może być konieczne toocontact [zespołem pomocy technicznej klienta usług Salesforce](https://help.salesforce.com/support).</span><span class="sxs-lookup"><span data-stu-id="5bc5f-176">If you are unable tooenable Single Sign-On settings for your Salesforce account, you may need toocontact [Salesforce Client support team](https://help.salesforce.com/support).</span></span> 

10. <span data-ttu-id="5bc5f-177">Wybierz **włączone SAML**, a następnie kliknij przycisk **zapisać**.</span><span class="sxs-lookup"><span data-stu-id="5bc5f-177">Select **SAML Enabled**, and then click **Save**.</span></span>

      ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-salesforce-tutorial/sf-enable-saml.png)
11. <span data-ttu-id="5bc5f-179">tooconfigure SAML pojedynczego logowania jednokrotnego ustawienia, kliknij przycisk **nowy**.</span><span class="sxs-lookup"><span data-stu-id="5bc5f-179">tooconfigure your SAML single sign-on settings, click **New**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-salesforce-tutorial/sf-admin-sso-new.png)

12. <span data-ttu-id="5bc5f-181">Na powitania **SAML pojedynczego logowania jednokrotnego ustawienie Edytuj** upewnij hello następujące konfiguracje:</span><span class="sxs-lookup"><span data-stu-id="5bc5f-181">On hello **SAML Single Sign-On Setting Edit** page, make hello following configurations:</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-salesforce-tutorial/sf-saml-config.png)

    <span data-ttu-id="5bc5f-183">a.</span><span class="sxs-lookup"><span data-stu-id="5bc5f-183">a.</span></span> <span data-ttu-id="5bc5f-184">Dla hello **nazwa** wpisz przyjazną nazwę dla tej konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="5bc5f-184">For hello **Name** field, type in a friendly name for this configuration.</span></span> <span data-ttu-id="5bc5f-185">Wartość dla **nazwa** automatycznie wypełnić hello **Nazwa interfejsu API** pola tekstowego.</span><span class="sxs-lookup"><span data-stu-id="5bc5f-185">Providing a value for **Name** automatically populate hello **API Name** textbox.</span></span>

    <span data-ttu-id="5bc5f-186">b.</span><span class="sxs-lookup"><span data-stu-id="5bc5f-186">b.</span></span> <span data-ttu-id="5bc5f-187">Wklej **identyfikator jednostki SMAL** wartości do hello **wystawcy** w Salesforce.</span><span class="sxs-lookup"><span data-stu-id="5bc5f-187">Paste **SMAL Entity ID** value into hello **Issuer** field in Salesforce.</span></span>

    <span data-ttu-id="5bc5f-188">c.</span><span class="sxs-lookup"><span data-stu-id="5bc5f-188">c.</span></span> <span data-ttu-id="5bc5f-189">W hello **textbox identyfikator jednostki**, wpisz nazwę domeny witryny Salesforce przy użyciu hello następującego wzorca:</span><span class="sxs-lookup"><span data-stu-id="5bc5f-189">In hello **Entity Id textbox**, type your Salesforce domain name using hello following pattern:</span></span>
      
      * <span data-ttu-id="5bc5f-190">Konto przedsiębiorstwa:`https://<subdomain>.my.salesforce.com`</span><span class="sxs-lookup"><span data-stu-id="5bc5f-190">Enterprise account: `https://<subdomain>.my.salesforce.com`</span></span>
      * <span data-ttu-id="5bc5f-191">Konta dewelopera:`https://<subdomain>-dev-ed.my.salesforce.com`</span><span class="sxs-lookup"><span data-stu-id="5bc5f-191">Developer account: `https://<subdomain>-dev-ed.my.salesforce.com`</span></span>
      
    <span data-ttu-id="5bc5f-192">d.</span><span class="sxs-lookup"><span data-stu-id="5bc5f-192">d.</span></span> <span data-ttu-id="5bc5f-193">Kliknij przycisk **Przeglądaj** lub **wybierz plik** tooopen hello **tooUpload wybierz plik** okno dialogowe, wybierz certyfikat usług Salesforce, a następnie kliknij przycisk **Otwórz**tooupload hello certyfikatu.</span><span class="sxs-lookup"><span data-stu-id="5bc5f-193">Click **Browse** or **Choose File** tooopen hello **Choose File tooUpload** dialog, select your Salesforce certificate, and then click **Open** tooupload hello certificate.</span></span>

    <span data-ttu-id="5bc5f-194">e.</span><span class="sxs-lookup"><span data-stu-id="5bc5f-194">e.</span></span> <span data-ttu-id="5bc5f-195">Dla **typ tożsamości SAML**, wybierz pozycję **potwierdzenia zawiera użytkownika witryny salesforce.com**.</span><span class="sxs-lookup"><span data-stu-id="5bc5f-195">For **SAML Identity Type**, select **Assertion contains User's salesforce.com username**.</span></span>

    <span data-ttu-id="5bc5f-196">f.</span><span class="sxs-lookup"><span data-stu-id="5bc5f-196">f.</span></span> <span data-ttu-id="5bc5f-197">Dla **lokalizacji tożsamości SAML**, wybierz pozycję **jest tożsamość w elemencie NameIdentifier hello hello instrukcji podmiotu**</span><span class="sxs-lookup"><span data-stu-id="5bc5f-197">For **SAML Identity Location**, select **Identity is in hello NameIdentifier element of hello Subject statement**</span></span>

    <span data-ttu-id="5bc5f-198">g.</span><span class="sxs-lookup"><span data-stu-id="5bc5f-198">g.</span></span> <span data-ttu-id="5bc5f-199">Wklej **pojedynczy znak na adres URL usługi** do hello **adresu URL logowania do dostawcy tożsamości** w Salesforce.</span><span class="sxs-lookup"><span data-stu-id="5bc5f-199">Paste **Single Sign-On Service URL** into hello **Identity Provider Login URL** field in Salesforce.</span></span>
    
    <span data-ttu-id="5bc5f-200">h.</span><span class="sxs-lookup"><span data-stu-id="5bc5f-200">h.</span></span> <span data-ttu-id="5bc5f-201">Dla **dostawcy zainicjował żądanie powiązania usługi**, wybierz pozycję **przekierowywanie HTTP**.</span><span class="sxs-lookup"><span data-stu-id="5bc5f-201">For **Service Provider Initiated Request Binding**, select **HTTP Redirect**.</span></span>
    
    <span data-ttu-id="5bc5f-202">i.</span><span class="sxs-lookup"><span data-stu-id="5bc5f-202">i.</span></span> <span data-ttu-id="5bc5f-203">Na koniec kliknij **zapisać** tooapply SAML pojedynczego logowania jednokrotnego ustawień.</span><span class="sxs-lookup"><span data-stu-id="5bc5f-203">Finally, click **Save** tooapply your SAML single sign-on settings.</span></span>

13. <span data-ttu-id="5bc5f-204">W okienku nawigacji po lewej stronie powitania w usłudze Salesforce kliknij **Zarządzanie domenami** tooexpand hello powiązanych sekcji, a następnie kliknij przycisk **Moje domeny**.</span><span class="sxs-lookup"><span data-stu-id="5bc5f-204">On hello left navigation pane in Salesforce, click **Domain Management** tooexpand hello related section, and then click **My Domain**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-salesforce-tutorial/sf-my-domain.png)

14. <span data-ttu-id="5bc5f-206">Przewiń w dół toohello **konfiguracji uwierzytelniania** sekcji, a następnie kliknij polecenie hello **Edytuj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="5bc5f-206">Scroll down toohello **Authentication Configuration** section, and click hello **Edit** button.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-salesforce-tutorial/sf-edit-auth-config.png)

15. <span data-ttu-id="5bc5f-208">W hello **usługi uwierzytelniania** sekcji wybierz hello przyjazną nazwę konfiguracji logowania jednokrotnego SAML, a następnie kliknij przycisk **zapisać**.</span><span class="sxs-lookup"><span data-stu-id="5bc5f-208">In hello **Authentication Service** section, select hello friendly name of your SAML SSO configuration, and then click **Save**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-salesforce-tutorial/sf-auth-config.png)

    > [!NOTE]
    > <span data-ttu-id="5bc5f-210">Jeśli zostanie wybrana więcej niż jedna usługa uwierzytelniania, użytkownicy są zostanie wyświetlony monit o tooselect usługi uwierzytelniania, która ich, takich jak toosign się podczas inicjowania środowiska usług Salesforce tooyour rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="5bc5f-210">If more than one authentication service is selected, users are prompted tooselect which authentication service they like toosign in with while initiating single sign-on tooyour Salesforce environment.</span></span> <span data-ttu-id="5bc5f-211">Jeśli nie chcesz toohappen, a następnie wykonaj następujące czynności **pozostawienie jej niezaznaczonej innych usług uwierzytelniania**.</span><span class="sxs-lookup"><span data-stu-id="5bc5f-211">If you don’t want it toohappen, then you should **leave all other authentication services unchecked**.</span></span>
<CE>    
> [!TIP]
> <span data-ttu-id="5bc5f-212">Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz hello [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji hello!</span><span class="sxs-lookup"><span data-stu-id="5bc5f-212">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="5bc5f-213">Po dodaniu tej aplikacji z hello **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij **rejestracji jednokrotnej** hello kartę i dostępu do osadzonych dokumentacji za pośrednictwem hello  **Konfiguracja** sekcji u dołu hello.</span><span class="sxs-lookup"><span data-stu-id="5bc5f-213">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="5bc5f-214">Więcej o hello osadzonych dokumentacji funkcji w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="5bc5f-214">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>


### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="5bc5f-215">Tworzenie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="5bc5f-215">Creating an Azure AD test user</span></span>
<span data-ttu-id="5bc5f-216">Celem Hello w tej sekcji jest toocreate użytkownika testowego, w portalu Azure o nazwie Simona Britta hello.</span><span class="sxs-lookup"><span data-stu-id="5bc5f-216">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Tworzenie użytkowników usługi Azure AD][100]

<span data-ttu-id="5bc5f-218">**toocreate użytkownika testowego w usłudze Azure AD, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="5bc5f-218">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="5bc5f-219">W okienku nawigacji po lewej stronie powitania w hello **portalu Azure**, kliknij przycisk **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="5bc5f-219">On hello left navigation pane in hello **Azure portal**, click **Azure Active Directory** icon.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-salesforce-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="5bc5f-221">toodisplay hello listę użytkowników, przejdź zbyt**użytkowników i grup** i kliknij przycisk **wszyscy użytkownicy**.</span><span class="sxs-lookup"><span data-stu-id="5bc5f-221">toodisplay hello list of users, Go too**Users and groups** and click **All users**.</span></span>
    
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-salesforce-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="5bc5f-223">U góry okna dialogowego hello hello, kliknij przycisk **Dodaj** tooopen hello **użytkownika** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="5bc5f-223">At hello top of hello dialog, click **Add** tooopen hello **User** dialog.</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-salesforce-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="5bc5f-225">Na powitania **użytkownika** okna dialogowego wykonaj hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="5bc5f-225">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-salesforce-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="5bc5f-227">a.</span><span class="sxs-lookup"><span data-stu-id="5bc5f-227">a.</span></span> <span data-ttu-id="5bc5f-228">W hello **nazwa** pole tekstowe, typ **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="5bc5f-228">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="5bc5f-229">b.</span><span class="sxs-lookup"><span data-stu-id="5bc5f-229">b.</span></span> <span data-ttu-id="5bc5f-230">W hello **nazwy użytkownika** pole tekstowe, hello typu **adres e-mail** z BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="5bc5f-230">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="5bc5f-231">c.</span><span class="sxs-lookup"><span data-stu-id="5bc5f-231">c.</span></span> <span data-ttu-id="5bc5f-232">Wybierz **Pokaż hasło** i zanotuj wartość hello hello **hasło**.</span><span class="sxs-lookup"><span data-stu-id="5bc5f-232">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="5bc5f-233">d.</span><span class="sxs-lookup"><span data-stu-id="5bc5f-233">d.</span></span> <span data-ttu-id="5bc5f-234">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="5bc5f-234">Click **Create**.</span></span>
 
### <a name="creating-a-salesforce-test-user"></a><span data-ttu-id="5bc5f-235">Tworzenie użytkownika testowego usług Salesforce</span><span class="sxs-lookup"><span data-stu-id="5bc5f-235">Creating a Salesforce test user</span></span>

<span data-ttu-id="5bc5f-236">W tej sekcji użytkownika o nazwie Simona Britta jest tworzony w Salesforce.</span><span class="sxs-lookup"><span data-stu-id="5bc5f-236">In this section, a user called Britta Simon is created in Salesforce.</span></span> <span data-ttu-id="5bc5f-237">SalesForce obsługę w czasie, który jest domyślnie włączona.</span><span class="sxs-lookup"><span data-stu-id="5bc5f-237">Salesforce supports just-in-time provisioning, which is enabled by default.</span></span>
<span data-ttu-id="5bc5f-238">Nie ma elementu akcji można w tej sekcji.</span><span class="sxs-lookup"><span data-stu-id="5bc5f-238">There is no action item for you in this section.</span></span> <span data-ttu-id="5bc5f-239">Jeśli użytkownik nie istnieje w usłudze Salesforce, nowy jest tworzony podczas próby tooaccess Salesforce.</span><span class="sxs-lookup"><span data-stu-id="5bc5f-239">If a user doesn't already exist in Salesforce, a new one is created when you attempt tooaccess Salesforce.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="5bc5f-240">Przypisanie użytkownika testowego hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="5bc5f-240">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="5bc5f-241">W tej sekcji możesz włączyć toouse Simona Britta Azure logowania jednokrotnego za udzielanie dostępu tooSalesforce.</span><span class="sxs-lookup"><span data-stu-id="5bc5f-241">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooSalesforce.</span></span>

![Przypisz użytkownika][200] 

<span data-ttu-id="5bc5f-243">**tooassign tooSalesforce Simona Britta wykonaj hello następujące kroki:**</span><span class="sxs-lookup"><span data-stu-id="5bc5f-243">**tooassign Britta Simon tooSalesforce, perform hello following steps:**</span></span>

1. <span data-ttu-id="5bc5f-244">W portalu Azure hello, otwórz widok aplikacji hello, a następnie przejdź do widoku katalogu toohello i przejść za**aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="5bc5f-244">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Przypisz użytkownika][201] 

2. <span data-ttu-id="5bc5f-246">Z listy aplikacji hello wybierz **Salesforce**.</span><span class="sxs-lookup"><span data-stu-id="5bc5f-246">In hello applications list, select **Salesforce**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-salesforce-tutorial/tutorial_salesforce_app.png) 

3. <span data-ttu-id="5bc5f-248">W menu powitania po lewej stronie powitania kliknij **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="5bc5f-248">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Przypisz użytkownika][202] 

4. <span data-ttu-id="5bc5f-250">Kliknij przycisk **Dodaj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="5bc5f-250">Click **Add** button.</span></span> <span data-ttu-id="5bc5f-251">Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="5bc5f-251">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Przypisz użytkownika][203]

5. <span data-ttu-id="5bc5f-253">Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** hello listy użytkowników.</span><span class="sxs-lookup"><span data-stu-id="5bc5f-253">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="5bc5f-254">Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="5bc5f-254">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="5bc5f-255">Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="5bc5f-255">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="5bc5f-256">Testowanie rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="5bc5f-256">Testing single sign-on</span></span>

<span data-ttu-id="5bc5f-257">tootest pojedynczego logowania jednokrotnego ustawienia, otwórz hello panelu dostępu pod adresem [https://myapps.microsoft.com](https://myapps.microsoft.com/), następnie zaloguj się do konta testowego hello i kliknij przycisk **Salesforce**.</span><span class="sxs-lookup"><span data-stu-id="5bc5f-257">tootest your single sign-on settings, open hello Access Panel at [https://myapps.microsoft.com](https://myapps.microsoft.com/), then sign into hello test account, and click **Salesforce**.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="5bc5f-258">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="5bc5f-258">Additional resources</span></span>

* [<span data-ttu-id="5bc5f-259">Lista samouczków dotyczących tooIntegrate aplikacji SaaS w usłudze Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="5bc5f-259">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="5bc5f-260">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="5bc5f-260">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)
* [<span data-ttu-id="5bc5f-261">Skonfiguruj Inicjowanie obsługi użytkowników</span><span class="sxs-lookup"><span data-stu-id="5bc5f-261">Configure User Provisioning</span></span>](active-directory-saas-salesforce-provisioning-tutorial.md)

<!--Image references-->

[1]: ./media/active-directory-saas-salesforce-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-salesforce-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-salesforce-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-salesforce-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-salesforce-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-salesforce-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-salesforce-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-salesforce-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-salesforce-tutorial/tutorial_general_203.png

