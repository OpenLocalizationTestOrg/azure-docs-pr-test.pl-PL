---
title: "Samouczek: Integracji Azure Active Directory z chmurą Creative Adobe | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak tooconfigure logowanie jednokrotne między usługą Azure Active Directory i Adobe Creative chmury."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 9ba1171e-56b1-4475-b308-58637d35e5a7
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/04/2017
ms.author: jeedes
ms.openlocfilehash: 5e66255e9785465974a23cd3ef79c24e28c0250f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-adobe-creative-cloud"></a><span data-ttu-id="638bf-103">Samouczek: Integracji Azure Active Directory z chmurą Creative Adobe</span><span class="sxs-lookup"><span data-stu-id="638bf-103">Tutorial: Azure Active Directory integration with Adobe Creative Cloud</span></span>

<span data-ttu-id="638bf-104">Z tego samouczka, dowiesz się, jak toointegrate Adobe Creative chmury w usłudze Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="638bf-104">In this tutorial, you learn how toointegrate Adobe Creative Cloud with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="638bf-105">Integrowanie Adobe Creative chmurze z usługą Azure AD zapewnia hello następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="638bf-105">Integrating Adobe Creative Cloud with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="638bf-106">Można kontrolować w usłudze Azure AD, kto ma dostęp tooAdobe Creative chmury</span><span class="sxs-lookup"><span data-stu-id="638bf-106">You can control in Azure AD who has access tooAdobe Creative Cloud</span></span>
- <span data-ttu-id="638bf-107">Można włączyć użytkownika użytkownicy tooautomatically get zalogowane tooAdobe Creative chmury (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="638bf-107">You can enable your users tooautomatically get signed-on tooAdobe Creative Cloud (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="638bf-108">Możesz zarządzać kont w jednej centralnej lokalizacji - hello portalu zarządzania Azure</span><span class="sxs-lookup"><span data-stu-id="638bf-108">You can manage your accounts in one central location - hello Azure Management portal</span></span>

<span data-ttu-id="638bf-109">Jeśli chcesz tooknow więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="638bf-109">If you want tooknow more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="638bf-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="638bf-110">Prerequisites</span></span>

<span data-ttu-id="638bf-111">tooconfigure integracji usługi Azure AD z chmurą Creative Adobe należy hello następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="638bf-111">tooconfigure Azure AD integration with Adobe Creative Cloud, you need hello following items:</span></span>

- <span data-ttu-id="638bf-112">Subskrypcję usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="638bf-112">An Azure AD subscription</span></span>
- <span data-ttu-id="638bf-113">Adobe Creative chmury jednokrotnego włączone subskrypcji</span><span class="sxs-lookup"><span data-stu-id="638bf-113">A Adobe Creative Cloud single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="638bf-114">tootest hello kroków w tym samouczku, zaleca się przy użyciu środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="638bf-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="638bf-115">tootest hello kroki opisane w tym samouczku, należy stosować te zalecenia:</span><span class="sxs-lookup"><span data-stu-id="638bf-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="638bf-116">Nie należy używać środowiska produkcyjnego, chyba że jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="638bf-116">You should not use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="638bf-117">Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz pobrać miesięczna wersja próbna [tutaj](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="638bf-117">If you don't have an Azure AD trial environment, you can get an one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="638bf-118">Opis scenariusza</span><span class="sxs-lookup"><span data-stu-id="638bf-118">Scenario description</span></span>
<span data-ttu-id="638bf-119">W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym.</span><span class="sxs-lookup"><span data-stu-id="638bf-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="638bf-120">Scenariusz Hello opisane w tym samouczku składa się z dwóch głównych elementów:</span><span class="sxs-lookup"><span data-stu-id="638bf-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="638bf-121">Dodawanie Adobe Creative chmury z galerii hello</span><span class="sxs-lookup"><span data-stu-id="638bf-121">Adding Adobe Creative Cloud from hello gallery</span></span>
2. <span data-ttu-id="638bf-122">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="638bf-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-adobe-creative-cloud-from-hello-gallery"></a><span data-ttu-id="638bf-123">Dodawanie Adobe Creative chmury z galerii hello</span><span class="sxs-lookup"><span data-stu-id="638bf-123">Adding Adobe Creative Cloud from hello gallery</span></span>
<span data-ttu-id="638bf-124">tooconfigure hello integracji Adobe Creative chmury do usługi Azure AD, należy tooadd Adobe Creative chmury z hello galerii tooyour listę zarządzanych aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="638bf-124">tooconfigure hello integration of Adobe Creative Cloud into Azure AD, you need tooadd Adobe Creative Cloud from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="638bf-125">**tooadd Adobe Creative chmury z galerii hello wykonaj hello następujące kroki:**</span><span class="sxs-lookup"><span data-stu-id="638bf-125">**tooadd Adobe Creative Cloud from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="638bf-126">W hello  **[portalu zarządzania Azure](https://portal.azure.com)**na temat hello panelu nawigacji po lewej stronie, kliknij przycisk **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="638bf-126">In hello **[Azure Management Portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Usługa Active Directory][1]

2. <span data-ttu-id="638bf-128">Przejdź za**aplikacje dla przedsiębiorstw**.</span><span class="sxs-lookup"><span data-stu-id="638bf-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="638bf-129">Następnie przejdź zbyt**wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="638bf-129">Then go too**All applications**.</span></span>

    ![Aplikacje][2]
    
3. <span data-ttu-id="638bf-131">Kliknij przycisk **Dodaj** przycisk u góry hello hello okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="638bf-131">Click **Add** button on hello top of hello dialog.</span></span>

    ![Aplikacje][3]

4. <span data-ttu-id="638bf-133">W polu wyszukiwania hello wpisz **chmury Creative Adobe**.</span><span class="sxs-lookup"><span data-stu-id="638bf-133">In hello search box, type **Adobe Creative Cloud**.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_adobe-creative-cloud_000.png)

5. <span data-ttu-id="638bf-135">W panelu wyników hello, wybierz **chmury Creative Adobe**, a następnie kliknij przycisk **Dodaj** przycisk aplikacji hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="638bf-135">In hello results panel, select **Adobe Creative Cloud**, and then click **Add** button tooadd hello application.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_adobe-creative-cloud_0001.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="638bf-137">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="638bf-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="638bf-138">W tej sekcji skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z Adobe Creative w chmurze na koncie użytkownika testu o nazwie "Britta Simona".</span><span class="sxs-lookup"><span data-stu-id="638bf-138">In this section, you configure and test Azure AD single sign-on with Adobe Creative Cloud based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="638bf-139">Dla pojedynczego logowania jednokrotnego toowork usługi Azure AD musi tooknow użytkownika odpowiednikiem hello w chmurze Creative Adobe jest tooa użytkownika w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="638bf-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Adobe Creative Cloud is tooa user in Azure AD.</span></span> <span data-ttu-id="638bf-140">Innymi słowy relację łącza między użytkownika usługi Azure AD i hello użytkownikowi w chmurze Creative Adobe musi toobe ustanowione.</span><span class="sxs-lookup"><span data-stu-id="638bf-140">In other words, a link relationship between an Azure AD user and hello related user in Adobe Creative Cloud needs toobe established.</span></span>

<span data-ttu-id="638bf-141">Ta relacja łącza zostanie nawiązane, przypisując wartość hello hello **nazwy użytkownika** w usłudze Azure AD jako wartość hello hello **Username** w chmurze Creative Adobe.</span><span class="sxs-lookup"><span data-stu-id="638bf-141">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in Adobe Creative Cloud.</span></span>

<span data-ttu-id="638bf-142">tooconfigure i testowych usługi Azure AD rejestracji jednokrotnej z chmurą Creative Adobe, należy po bloków konstrukcyjnych hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="638bf-142">tooconfigure and test Azure AD single sign-on with Adobe Creative Cloud, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="638bf-143">**[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configuring-azure-ad-single-sign-on)**  -tooenable Twojego toouse użytkowników tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="638bf-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="638bf-144">**[Tworzenie użytkownika testowego usługi Azure AD](#creating-an-azure-ad-test-user)**  -tootest usługi Azure AD rejestracji jednokrotnej z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="638bf-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="638bf-145">**[Tworzenie użytkownika testowego chmury Creative Adobe](#creating-an-adobe-creative-cloud-test-user)**  -toohave odpowiednikiem Simona Britta w chmurze Creative Adobe, która jest jego reprezentacja toohello połączonej usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="638bf-145">**[Creating an Adobe Creative Cloud test user](#creating-an-adobe-creative-cloud-test-user)** - toohave a counterpart of Britta Simon in Adobe Creative Cloud that is linked toohello Azure AD representation of her.</span></span>
4. <span data-ttu-id="638bf-146">**[Przypisanie użytkownika testowego hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Simona Britta toouse usługi Azure AD rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="638bf-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="638bf-147">**[Testowanie rejestracji jednokrotnej](#testing-single-sign-on)**  -tooverify czy hello konfiguracji działania.</span><span class="sxs-lookup"><span data-stu-id="638bf-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="638bf-148">Konfigurowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="638bf-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="638bf-149">W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w portalu zarządzania Azure hello i skonfigurować logowanie jednokrotne do aplikacji w chmurze Creative Adobe.</span><span class="sxs-lookup"><span data-stu-id="638bf-149">In this section, you enable Azure AD single sign-on in hello Azure Management portal and configure single sign-on in your Adobe Creative Cloud application.</span></span>

<span data-ttu-id="638bf-150">**tooconfigure usługi Azure AD rejestracji jednokrotnej z Adobe Creative chmury, wykonaj hello następujące kroki:**</span><span class="sxs-lookup"><span data-stu-id="638bf-150">**tooconfigure Azure AD single sign-on with Adobe Creative Cloud, perform hello following steps:**</span></span>

1. <span data-ttu-id="638bf-151">W portalu zarządzania Azure hello na powitania **chmury Creative Adobe** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.</span><span class="sxs-lookup"><span data-stu-id="638bf-151">In hello Azure Management portal, on hello **Adobe Creative Cloud** application integration page, click **Single sign-on**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej][4]

2. <span data-ttu-id="638bf-153">Na powitania **logowanie jednokrotne** okna dialogowego, jako **tryb** wybierz **na języku SAML logowania jednokrotnego** tooenable logowania jednokrotnego.</span><span class="sxs-lookup"><span data-stu-id="638bf-153">On hello **Single sign-on** dialog, as **Mode** select **SAML-based Sign-on** tooenable single sign on.</span></span>
 
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_adobe-creative-cloud_01.png)

3. <span data-ttu-id="638bf-155">Na powitania **adresy URL i Adobe Creative domenę chmury** sekcji, wykonaj następujące kroki, jeśli chcesz, aby aplikacja hello tooconfigure w hello **IDP** inicjowane tryb:</span><span class="sxs-lookup"><span data-stu-id="638bf-155">On hello **Adobe Creative Cloud Domain and URLs** section, perform hello following steps if you wish tooconfigure hello application in **IDP** initiated mode:</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_adobe-creative-cloud_url1.png)

    <span data-ttu-id="638bf-157">a.</span><span class="sxs-lookup"><span data-stu-id="638bf-157">a.</span></span> <span data-ttu-id="638bf-158">W hello **identyfikator** pole tekstowe, wartość hello typu jako:`https://www.okta.com/saml2/service-provider/<token>`</span><span class="sxs-lookup"><span data-stu-id="638bf-158">In hello **Identifier** textbox, type hello value as: `https://www.okta.com/saml2/service-provider/<token>`</span></span>

    <span data-ttu-id="638bf-159">b.</span><span class="sxs-lookup"><span data-stu-id="638bf-159">b.</span></span> <span data-ttu-id="638bf-160">W hello **adres URL odpowiedzi** tekstowym, wpisz adres URL za pomocą hello następującego wzorca:`https://<company name>.okta.com/auth/saml20/accauthlinktest`</span><span class="sxs-lookup"><span data-stu-id="638bf-160">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://<company name>.okta.com/auth/saml20/accauthlinktest`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="638bf-161">Należy pamiętać, że nie są one hello wartości rzeczywistych.</span><span class="sxs-lookup"><span data-stu-id="638bf-161">Please note that these are not hello real values.</span></span> <span data-ttu-id="638bf-162">Masz tooupdate tych wartości za pomocą hello rzeczywisty identyfikator i odpowiedzi adresu URL.</span><span class="sxs-lookup"><span data-stu-id="638bf-162">You have tooupdate these values with hello actual Identifier and Reply URL.</span></span> <span data-ttu-id="638bf-163">W tym miejscu zalecamy możesz toouse hello unikatową wartość ciągu w hello identyfikator.</span><span class="sxs-lookup"><span data-stu-id="638bf-163">Here we suggest you toouse hello unique value of string in hello Identifier.</span></span> <span data-ttu-id="638bf-164">Należy ręcznie toocreate użytkownika, należy najpierw toocontact hello Adobe Creative chmury z pomocą techniczną.</span><span class="sxs-lookup"><span data-stu-id="638bf-164">If you need toocreate an user manually, you need toocontact hello Adobe Creative Cloud support team.</span></span>

4. <span data-ttu-id="638bf-165">Na powitania **adresy URL i Adobe Creative domenę chmury** sekcji, wykonaj następujące kroki, jeśli chcesz, aby aplikacja hello tooconfigure w hello **SP** inicjowane tryb:</span><span class="sxs-lookup"><span data-stu-id="638bf-165">On hello **Adobe Creative Cloud Domain and URLs** section, perform hello following steps if you wish tooconfigure hello application in **SP** initiated mode:</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_adobe-creative-cloud_url2.png)

    <span data-ttu-id="638bf-167">a.</span><span class="sxs-lookup"><span data-stu-id="638bf-167">a.</span></span> <span data-ttu-id="638bf-168">Polecenie hello **Pokaż zaawansowane ustawienia adresu URL** opcji</span><span class="sxs-lookup"><span data-stu-id="638bf-168">Click on hello **Show advanced URL settings** option</span></span>

    <span data-ttu-id="638bf-169">b.</span><span class="sxs-lookup"><span data-stu-id="638bf-169">b.</span></span> <span data-ttu-id="638bf-170">W hello **adres URL logowania** pole tekstowe, wartość hello typu jako:`https://adobe.com`</span><span class="sxs-lookup"><span data-stu-id="638bf-170">In hello **Sign-on URL** textbox, type hello value as: `https://adobe.com`</span></span>

5. <span data-ttu-id="638bf-171">Na powitania **certyfikat podpisywania SAML** kliknij **certyfikatu (Base64)** , a następnie zapisz plik certyfikatu hello na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="638bf-171">On hello **SAML Signing Certificate** section, click **Certificate (Base64)** and then save hello certificate file on your computer.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_adobe-creative-cloud_05.png) 

6. <span data-ttu-id="638bf-173">Na powitania **Adobe Creative konfiguracji chmury** kliknij **Konfigurowanie chmury Creative Adobe** tooopen **Konfigurowanie logowania jednokrotnego** okna.</span><span class="sxs-lookup"><span data-stu-id="638bf-173">On hello **Adobe Creative Cloud Configuration** section, click **Configure Adobe Creative Cloud** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="638bf-174">Skopiuj hello **identyfikator jednostki SAML** i **adres URL usługi logowania jednokrotnego SAML** z krótkimi opisami sekcji.</span><span class="sxs-lookup"><span data-stu-id="638bf-174">Please copy hello **SAML Entity Id** and **SAML SSO Service URL** from Quick Reference section.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_adobe-creative-cloud_06.png) 

7. <span data-ttu-id="638bf-176">W oknie przeglądarki innej witryny sieci web, tooyour logowania w chmurze Creative Adobe dzierżawy jako administrator.</span><span class="sxs-lookup"><span data-stu-id="638bf-176">In a different web browser window, sign-on tooyour Adobe Creative Cloud tenant as an administrator.</span></span>

8.  <span data-ttu-id="638bf-177">Przejdź za**tożsamości** hello okienka nawigacji po lewej stronie i kliknij domenę.</span><span class="sxs-lookup"><span data-stu-id="638bf-177">Go too**Identity** on hello left navigation pane and click your domain.</span></span> <span data-ttu-id="638bf-178">Następnie wykonaj następujące kroki powitania **pojedynczy znak na wymagana konfiguracja** sekcji.</span><span class="sxs-lookup"><span data-stu-id="638bf-178">Then perform hello following steps on **Single Sign On Configuration Required** section.</span></span>

    <span data-ttu-id="638bf-179">![Ustawienia](./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_adobe-creative-cloud_001.png "ustawienia")</span><span class="sxs-lookup"><span data-stu-id="638bf-179">![Settings](./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_adobe-creative-cloud_001.png "Settings")</span></span>

9. <span data-ttu-id="638bf-180">Kliknij przycisk **Przeglądaj** tooupload hello pobrać certyfikatu z usługi Azure AD za**certyfikatu IDP**.</span><span class="sxs-lookup"><span data-stu-id="638bf-180">Click **Browse** tooupload hello downloaded certificate from Azure AD too**IDP Certificate**.</span></span>

10. <span data-ttu-id="638bf-181">W hello **wystawcy IDP** pole tekstowe, umieść wartość hello **identyfikator jednostki SAML** którego skopiowany z **Konfigurowanie logowania jednokrotnego** sekcji w portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="638bf-181">In hello **IDP issuer** textbox, put hello value of **SAML Entity Id** which you copied from **Configure sign-on** section in Azure portal.</span></span>

11. <span data-ttu-id="638bf-182">W hello **adres URL logowania IDP** pole tekstowe, umieść wartość hello **adres URL usługi logowania jednokrotnego SAML** , które zostały skopiowane z **Konfigurowanie logowania jednokrotnego** sekcji w portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="638bf-182">In hello **IDP Login URL** textbox, put hello value of **SAML SSO Service URL** which you copied from **Configure sign-on** section in Azure portal.</span></span>

12. <span data-ttu-id="638bf-183">Wybierz **HTTP - przekierowania** jako **powiązania IDP**.</span><span class="sxs-lookup"><span data-stu-id="638bf-183">Select **HTTP - Redirect** as **IDP Binding**.</span></span>

13. <span data-ttu-id="638bf-184">Wybierz **adres E-mail** jako **ustawienia logowania użytkownika**.</span><span class="sxs-lookup"><span data-stu-id="638bf-184">Select **Email Address** as **User Login Setting**.</span></span>
 
14. <span data-ttu-id="638bf-185">Kliknij przycisk **zapisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="638bf-185">Click **Save** button.</span></span>

15. <span data-ttu-id="638bf-186">pulpit nawigacyjny Hello teraz przedstawi hello XML **"Pobieranie metadanych"** pliku.</span><span class="sxs-lookup"><span data-stu-id="638bf-186">hello dashboard will now present hello XML **"Download Metadata"** file.</span></span> <span data-ttu-id="638bf-187">Zawiera adres URL EntityDescriptor Adobe i AssertionConsumerService adresu URL.</span><span class="sxs-lookup"><span data-stu-id="638bf-187">It contains Adobe’s EntityDescriptor URL and AssertionConsumerService URL.</span></span> <span data-ttu-id="638bf-188">Otwórz plik hello i skonfigurować je w hello aplikacji usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="638bf-188">Please open hello file and configure them in hello Azure AD application.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej po stronie aplikacji](./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_adobe-creative-cloud_002.png)

    ![Konfigurowanie rejestracji jednokrotnej po stronie aplikacji](./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_adobe-creative-cloud_003.png)

    <span data-ttu-id="638bf-191">a.</span><span class="sxs-lookup"><span data-stu-id="638bf-191">a.</span></span> <span data-ttu-id="638bf-192">Użyj hello wartość EntityDescriptor Adobe dostarczył dla **identyfikator** na powitania **Konfigurowanie ustawień aplikacji** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="638bf-192">Use hello EntityDescriptor value Adobe provided you for **Identifier** on hello **Configure App Settings** dialog.</span></span>

    <span data-ttu-id="638bf-193">b.</span><span class="sxs-lookup"><span data-stu-id="638bf-193">b.</span></span> <span data-ttu-id="638bf-194">Użyj hello wartość AssertionConsumerService Adobe dostarczył dla **adres URL odpowiedzi** na powitania **Konfigurowanie ustawień aplikacji** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="638bf-194">Use hello AssertionConsumerService value Adobe provided you for **Reply URL** on hello **Configure App Settings** dialog.</span></span>
 
### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="638bf-195">Tworzenie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="638bf-195">Creating an Azure AD test user</span></span>
<span data-ttu-id="638bf-196">Celem Hello w tej sekcji jest toocreate użytkownika testowego, w portalu zarządzania Azure hello o nazwie Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="638bf-196">hello objective of this section is toocreate a test user in hello Azure Management portal called Britta Simon.</span></span>

![Tworzenie użytkowników usługi Azure AD][100]

<span data-ttu-id="638bf-198">**toocreate użytkownika testowego w usłudze Azure AD, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="638bf-198">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="638bf-199">W hello **portalu zarządzania Azure**na temat hello w lewym okienku nawigacji, kliknij przycisk **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="638bf-199">In hello **Azure Management portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-adobe-creative-cloud-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="638bf-201">Przejdź za**użytkowników i grup** i kliknij przycisk **wszyscy użytkownicy** toodisplay hello listy użytkowników.</span><span class="sxs-lookup"><span data-stu-id="638bf-201">Go too**Users and groups** and click **All users** toodisplay hello list of users.</span></span>
    
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-adobe-creative-cloud-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="638bf-203">U góry okna dialogowego hello powitania kliknij **Dodaj** tooopen hello **użytkownika** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="638bf-203">At hello top of hello dialog click **Add** tooopen hello **User** dialog.</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-adobe-creative-cloud-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="638bf-205">Na powitania **użytkownika** okna dialogowego wykonaj hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="638bf-205">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-adobe-creative-cloud-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="638bf-207">a.</span><span class="sxs-lookup"><span data-stu-id="638bf-207">a.</span></span> <span data-ttu-id="638bf-208">W hello **nazwa** pole tekstowe, typ **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="638bf-208">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="638bf-209">b.</span><span class="sxs-lookup"><span data-stu-id="638bf-209">b.</span></span> <span data-ttu-id="638bf-210">W hello **nazwy użytkownika** pole tekstowe, hello typu **adres e-mail** z BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="638bf-210">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="638bf-211">c.</span><span class="sxs-lookup"><span data-stu-id="638bf-211">c.</span></span> <span data-ttu-id="638bf-212">Wybierz **Pokaż hasło** i zanotuj wartość hello hello **hasło**.</span><span class="sxs-lookup"><span data-stu-id="638bf-212">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="638bf-213">d.</span><span class="sxs-lookup"><span data-stu-id="638bf-213">d.</span></span> <span data-ttu-id="638bf-214">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="638bf-214">Click **Create**.</span></span> 

### <a name="creating-an-adobe-creative-cloud-test-user"></a><span data-ttu-id="638bf-215">Tworzenie użytkownika testowego Adobe Creative chmury</span><span class="sxs-lookup"><span data-stu-id="638bf-215">Creating an Adobe Creative Cloud test user</span></span>

<span data-ttu-id="638bf-216">W przypadku użytkowników usługi Azure AD toolog kolejności tooenable w chmurze Creative Adobe muszą mieć przydzielone do Adobe Creative chmury.</span><span class="sxs-lookup"><span data-stu-id="638bf-216">In order tooenable Azure AD users toolog into Adobe Creative Cloud, they must be provisioned into Adobe Creative Cloud.</span></span>  
<span data-ttu-id="638bf-217">W przypadku hello Adobe Creative chmury Inicjowanie obsługi to zadanie ręczne.</span><span class="sxs-lookup"><span data-stu-id="638bf-217">In hello case of Adobe Creative Cloud, provisioning is a manual task.</span></span>

<span data-ttu-id="638bf-218">**tooprovision kont użytkowników, wykonaj hello następujące kroki:**</span><span class="sxs-lookup"><span data-stu-id="638bf-218">**tooprovision a user accounts, perform hello following steps:**</span></span>

1. <span data-ttu-id="638bf-219">Zaloguj się za tooyour witryny firmy Adobe Creative chmurze jako administrator.</span><span class="sxs-lookup"><span data-stu-id="638bf-219">Log in tooyour Adobe Creative Cloud company site as an administrator.</span></span>

2. <span data-ttu-id="638bf-220">Kliknij przycisk **osób**.</span><span class="sxs-lookup"><span data-stu-id="638bf-220">Click **People**.</span></span>

    <span data-ttu-id="638bf-221">![Osoby](./media/active-directory-saas-adobe-creative-cloud-tutorial/create_aaduser_001.png "osób")</span><span class="sxs-lookup"><span data-stu-id="638bf-221">![People](./media/active-directory-saas-adobe-creative-cloud-tutorial/create_aaduser_001.png "People")</span></span>

3. <span data-ttu-id="638bf-222">Kliknij przycisk **zaprosić użytkowników**.</span><span class="sxs-lookup"><span data-stu-id="638bf-222">Click **Invite User**.</span></span>

    <span data-ttu-id="638bf-223">![Zaprosić użytkowników](./media/active-directory-saas-adobe-creative-cloud-tutorial/create_aaduser_002.png "zaprosić użytkowników")</span><span class="sxs-lookup"><span data-stu-id="638bf-223">![Invite Users](./media/active-directory-saas-adobe-creative-cloud-tutorial/create_aaduser_002.png "Invite Users")</span></span>

4. <span data-ttu-id="638bf-224">Na powitania **zaprosić użytkowników** okna dialogowego wykonaj hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="638bf-224">On hello **Invite People** dialog page, perform hello following steps:</span></span>

    <span data-ttu-id="638bf-225">![Zaproś inne osoby](./media/active-directory-saas-adobe-creative-cloud-tutorial/create_aaduser_003.png "Zaproś inne osoby")</span><span class="sxs-lookup"><span data-stu-id="638bf-225">![Invite People](./media/active-directory-saas-adobe-creative-cloud-tutorial/create_aaduser_003.png "Invite People")</span></span>

    <span data-ttu-id="638bf-226">a.</span><span class="sxs-lookup"><span data-stu-id="638bf-226">a.</span></span> <span data-ttu-id="638bf-227">W hello **E-mail** pole tekstowe, adres e-mail hello typu Simona Britta konta.</span><span class="sxs-lookup"><span data-stu-id="638bf-227">In hello **Email** textbox, type hello email address of Britta Simon account.</span></span>
    
    <span data-ttu-id="638bf-228">b.</span><span class="sxs-lookup"><span data-stu-id="638bf-228">b.</span></span> <span data-ttu-id="638bf-229">Kliknij przycisk **zaprosić**.</span><span class="sxs-lookup"><span data-stu-id="638bf-229">Click **Invite**.</span></span>

    > [!NOTE]
    > <span data-ttu-id="638bf-230">właścicielem konta usługi Azure Active Directory Hello będzie otrzymywać wiadomości e-mail i postępuj zgodnie tooconfirm łącze swojego konta przed staje się aktywny.</span><span class="sxs-lookup"><span data-stu-id="638bf-230">hello Azure Active Directory account holder will receive an email and follow a link tooconfirm their account before it becomes active.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="638bf-231">Przypisanie użytkownika testowego hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="638bf-231">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="638bf-232">W tej sekcji możesz włączyć toouse Simona Britta Azure logowania jednokrotnego za udzielanie jej tooAdobe dostępu Creative chmury.</span><span class="sxs-lookup"><span data-stu-id="638bf-232">In this section, you enable Britta Simon toouse Azure single sign-on by granting her access tooAdobe Creative Cloud.</span></span>

![Przypisz użytkownika][200] 

<span data-ttu-id="638bf-234">**tooassign tooAdobe Simona Britta Creative chmury, wykonaj hello następujące kroki:**</span><span class="sxs-lookup"><span data-stu-id="638bf-234">**tooassign Britta Simon tooAdobe Creative Cloud, perform hello following steps:**</span></span>

1. <span data-ttu-id="638bf-235">W portalu zarządzania Azure hello, otwórz widok aplikacji hello, a następnie przejdź widok katalogu toohello i go za**aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="638bf-235">In hello Azure Management portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Przypisz użytkownika][201] 

2. <span data-ttu-id="638bf-237">Z listy aplikacji hello wybierz **chmury Creative Adobe**.</span><span class="sxs-lookup"><span data-stu-id="638bf-237">In hello applications list, select **Adobe Creative Cloud**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_adobe-creative-cloud_50.png) 

3. <span data-ttu-id="638bf-239">W menu powitania po lewej stronie powitania kliknij **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="638bf-239">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Przypisz użytkownika][202] 

4. <span data-ttu-id="638bf-241">Kliknij przycisk **Dodaj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="638bf-241">Click **Add** button.</span></span> <span data-ttu-id="638bf-242">Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="638bf-242">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Przypisz użytkownika][203]

5. <span data-ttu-id="638bf-244">Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** hello listy użytkowników.</span><span class="sxs-lookup"><span data-stu-id="638bf-244">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="638bf-245">Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="638bf-245">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="638bf-246">Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="638bf-246">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="638bf-247">Testowanie rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="638bf-247">Testing single sign-on</span></span>

<span data-ttu-id="638bf-248">W tej sekcji można przetestować konfiguracji usługi Azure AD pojedynczego logowania jednokrotnego przy użyciu hello panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="638bf-248">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="638bf-249">Po kliknięciu kafelka Adobe Creative chmury hello w hello Panel dostępu, należy pobrać aplikacji w chmurze Creative Adobe tooyour zalogowane automatycznie.</span><span class="sxs-lookup"><span data-stu-id="638bf-249">When you click hello Adobe Creative Cloud tile in hello Access Panel, you should get automatically signed-on tooyour Adobe Creative Cloud application.</span></span>


## <a name="additional-resources"></a><span data-ttu-id="638bf-250">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="638bf-250">Additional resources</span></span>

* [<span data-ttu-id="638bf-251">Lista samouczków dotyczących tooIntegrate aplikacji SaaS w usłudze Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="638bf-251">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="638bf-252">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="638bf-252">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_general_203.png