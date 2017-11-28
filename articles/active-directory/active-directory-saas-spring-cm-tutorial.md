---
title: 'Samouczek: Integracji Azure Active Directory z SpringCM | Dokumentacja firmy Microsoft'
description: "Dowiedz się, jak tooconfigure logowanie jednokrotne między usługą Azure Active Directory i SpringCM."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 4a42f797-ac58-4aca-a8e6-53bfe5529083
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/26/2017
ms.author: jeedes
ms.openlocfilehash: 12c8ebe765e2c6e61115256e9343d90ec132e1f8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-springcm"></a><span data-ttu-id="27450-103">Samouczek: Integracji Azure Active Directory z SpringCM</span><span class="sxs-lookup"><span data-stu-id="27450-103">Tutorial: Azure Active Directory integration with SpringCM</span></span>

<span data-ttu-id="27450-104">Z tego samouczka, dowiesz się, jak toointegrate SpringCM w usłudze Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="27450-104">In this tutorial, you learn how toointegrate SpringCM with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="27450-105">Integracja z usługą Azure AD SpringCM zapewnia hello następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="27450-105">Integrating SpringCM with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="27450-106">Można kontrolować w usłudze Azure AD, kto ma dostęp do tooSpringCM</span><span class="sxs-lookup"><span data-stu-id="27450-106">You can control in Azure AD who has access tooSpringCM</span></span>
- <span data-ttu-id="27450-107">Można włączyć użytkownika użytkownicy tooautomatically get zalogowane tooSpringCM (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="27450-107">You can enable your users tooautomatically get signed-on tooSpringCM (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="27450-108">Możesz zarządzać kont w jednej centralnej lokalizacji - hello portalu Azure</span><span class="sxs-lookup"><span data-stu-id="27450-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="27450-109">Jeśli chcesz tooknow więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="27450-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="27450-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="27450-110">Prerequisites</span></span>

<span data-ttu-id="27450-111">tooconfigure integracji z usługą Azure AD z SpringCM należy hello następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="27450-111">tooconfigure Azure AD integration with SpringCM, you need hello following items:</span></span>

- <span data-ttu-id="27450-112">Subskrypcję usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="27450-112">An Azure AD subscription</span></span>
- <span data-ttu-id="27450-113">SpringCM logowanie jednokrotne włączone subskrypcji</span><span class="sxs-lookup"><span data-stu-id="27450-113">A SpringCM single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="27450-114">tootest hello kroków w tym samouczku, zaleca się przy użyciu środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="27450-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="27450-115">tootest hello kroki opisane w tym samouczku, należy stosować te zalecenia:</span><span class="sxs-lookup"><span data-stu-id="27450-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="27450-116">Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="27450-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="27450-117">Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz pobrać miesięczna wersja próbna [tutaj](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="27450-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="27450-118">Opis scenariusza</span><span class="sxs-lookup"><span data-stu-id="27450-118">Scenario description</span></span>
<span data-ttu-id="27450-119">W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym.</span><span class="sxs-lookup"><span data-stu-id="27450-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="27450-120">Scenariusz Hello opisane w tym samouczku składa się z dwóch głównych elementów:</span><span class="sxs-lookup"><span data-stu-id="27450-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="27450-121">Dodawanie SpringCM z galerii hello</span><span class="sxs-lookup"><span data-stu-id="27450-121">Adding SpringCM from hello gallery</span></span>
2. <span data-ttu-id="27450-122">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="27450-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-springcm-from-hello-gallery"></a><span data-ttu-id="27450-123">Dodawanie SpringCM z galerii hello</span><span class="sxs-lookup"><span data-stu-id="27450-123">Adding SpringCM from hello gallery</span></span>
<span data-ttu-id="27450-124">tooconfigure hello integracji SpringCM do usługi Azure AD, należy tooadd SpringCM z hello galerii tooyour listę zarządzanych aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="27450-124">tooconfigure hello integration of SpringCM into Azure AD, you need tooadd SpringCM from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="27450-125">**tooadd SpringCM z galerii hello, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="27450-125">**tooadd SpringCM from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="27450-126">W hello  **[portalu Azure](https://portal.azure.com)**na temat hello panelu nawigacji po lewej stronie, kliknij przycisk **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="27450-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Usługa Active Directory][1]

2. <span data-ttu-id="27450-128">Przejdź za**aplikacje dla przedsiębiorstw**.</span><span class="sxs-lookup"><span data-stu-id="27450-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="27450-129">Następnie przejdź zbyt**wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="27450-129">Then go too**All applications**.</span></span>

    ![Aplikacje][2]
    
3. <span data-ttu-id="27450-131">tooadd nową aplikację, kliknij przycisk **nowej aplikacji** przycisk u góry hello okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="27450-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplikacje][3]

4. <span data-ttu-id="27450-133">W polu wyszukiwania hello wpisz **SpringCM**.</span><span class="sxs-lookup"><span data-stu-id="27450-133">In hello search box, type **SpringCM**.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-spring-cm-tutorial/tutorial_springcm_search.png)

5. <span data-ttu-id="27450-135">W panelu wyników hello zaznacz **SpringCM**, a następnie kliknij przycisk **Dodaj** przycisk aplikacji hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="27450-135">In hello results panel, select **SpringCM**, and then click **Add** button tooadd hello application.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-spring-cm-tutorial/tutorial_springcm_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="27450-137">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="27450-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="27450-138">W tej sekcji możesz skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z SpringCM na podstawie użytkownika testowego, nazywany "Britta Simona".</span><span class="sxs-lookup"><span data-stu-id="27450-138">In this section, you configure and test Azure AD single sign-on with SpringCM based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="27450-139">Dla pojedynczego logowania jednokrotnego toowork usługi Azure AD musi tooknow użytkownika odpowiednikiem hello w SpringCM jest tooa użytkownika w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="27450-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in SpringCM is tooa user in Azure AD.</span></span> <span data-ttu-id="27450-140">Innymi słowy relację łącza między użytkownika usługi Azure AD i hello użytkownikowi w SpringCM musi toobe ustanowione.</span><span class="sxs-lookup"><span data-stu-id="27450-140">In other words, a link relationship between an Azure AD user and hello related user in SpringCM needs toobe established.</span></span>

<span data-ttu-id="27450-141">W SpringCM, należy przypisać wartość hello hello **nazwy użytkownika** w usłudze Azure AD jako wartość hello hello **Username** tooestablish hello łącze relacji.</span><span class="sxs-lookup"><span data-stu-id="27450-141">In SpringCM, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="27450-142">tooconfigure i testowych usługi Azure AD rejestracji jednokrotnej z SpringCM, należy po bloków konstrukcyjnych hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="27450-142">tooconfigure and test Azure AD single sign-on with SpringCM, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="27450-143">**[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configuring-azure-ad-single-sign-on)**  -tooenable Twojego toouse użytkowników tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="27450-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="27450-144">**[Tworzenie użytkownika testowego usługi Azure AD](#creating-an-azure-ad-test-user)**  -tootest usługi Azure AD rejestracji jednokrotnej z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="27450-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="27450-145">**[Tworzenie użytkownika testowego SpringCM](#creating-a-springcm-test-user)**  -toohave odpowiednikiem Simona Britta w SpringCM, który jest połączony toohello usługi Azure AD reprezentację użytkownika.</span><span class="sxs-lookup"><span data-stu-id="27450-145">**[Creating a SpringCM test user](#creating-a-springcm-test-user)** - toohave a counterpart of Britta Simon in SpringCM that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="27450-146">**[Przypisanie użytkownika testowego hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Simona Britta toouse usługi Azure AD rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="27450-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="27450-147">**[Testowanie rejestracji jednokrotnej](#testing-single-sign-on)**  -tooverify czy hello konfiguracji działania.</span><span class="sxs-lookup"><span data-stu-id="27450-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="27450-148">Konfigurowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="27450-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="27450-149">W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w portalu Azure hello i skonfigurować logowanie jednokrotne w aplikacji SpringCM.</span><span class="sxs-lookup"><span data-stu-id="27450-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your SpringCM application.</span></span>

<span data-ttu-id="27450-150">**tooconfigure usługi Azure AD rejestracji jednokrotnej z SpringCM, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="27450-150">**tooconfigure Azure AD single sign-on with SpringCM, perform hello following steps:**</span></span>

1. <span data-ttu-id="27450-151">W portalu Azure na powitania hello **SpringCM** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.</span><span class="sxs-lookup"><span data-stu-id="27450-151">In hello Azure portal, on hello **SpringCM** application integration page, click **Single sign-on**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej][4]

2. <span data-ttu-id="27450-153">Na powitania **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** tooenable rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="27450-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-spring-cm-tutorial/tutorial_springcm_samlbase.png)

3. <span data-ttu-id="27450-155">Na powitania **SpringCM domeny i adres URL** sekcji, wykonaj następujące kroki hello:</span><span class="sxs-lookup"><span data-stu-id="27450-155">On hello **SpringCM Domain and URLs** section, perform hello following steps:</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-spring-cm-tutorial/tutorial_springcm_url.png)

    <span data-ttu-id="27450-157">W hello **adres URL logowania** tekstowym, wpisz adres URL za pomocą hello następującego wzorca:`https://na11.springcm.com/atlas/SSO/SSOEndpoint.ashx?aid=<identifier>`</span><span class="sxs-lookup"><span data-stu-id="27450-157">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://na11.springcm.com/atlas/SSO/SSOEndpoint.ashx?aid=<identifier>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="27450-158">Ta wartość nie jest prawdziwe.</span><span class="sxs-lookup"><span data-stu-id="27450-158">This value is not real.</span></span> <span data-ttu-id="27450-159">Zaktualizuj tę wartość z hello rzeczywisty adres URL logowania.</span><span class="sxs-lookup"><span data-stu-id="27450-159">Update this value with hello actual Sign-On URL.</span></span> <span data-ttu-id="27450-160">Skontaktuj się z [zespołem pomocy technicznej klienta SpringCM](https://knowledge.springcm.com/support) tooget tej wartości.</span><span class="sxs-lookup"><span data-stu-id="27450-160">Contact [SpringCM Client support team](https://knowledge.springcm.com/support) tooget this value.</span></span> 
 
4. <span data-ttu-id="27450-161">Na powitania **certyfikat podpisywania SAML** kliknij **Certificate(Raw)** , a następnie zapisz plik certyfikatu hello na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="27450-161">On hello **SAML Signing Certificate** section, click **Certificate(Raw)** and then save hello certificate file on your computer.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-spring-cm-tutorial/tutorial_springcm_certificate.png) 

5. <span data-ttu-id="27450-163">Kliknij przycisk **zapisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="27450-163">Click **Save** button.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-spring-cm-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="27450-165">Na powitania **konfiguracji SpringCM** kliknij **skonfigurować SpringCM** tooopen **Konfigurowanie logowania jednokrotnego** okna.</span><span class="sxs-lookup"><span data-stu-id="27450-165">On hello **SpringCM Configuration** section, click **Configure SpringCM** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="27450-166">Kopiuj hello **identyfikator jednostki SAML i SAML pojedynczy znak na adres URL usługi** z hello **sekcji krótkimi opisami.**</span><span class="sxs-lookup"><span data-stu-id="27450-166">Copy hello **SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-spring-cm-tutorial/tutorial_springcm_configure.png)   

7. <span data-ttu-id="27450-168">W oknie przeglądarki innej witryny sieci web, zaloguj się na tooyour **SpringCM** witryny firmy jako administrator.</span><span class="sxs-lookup"><span data-stu-id="27450-168">In a different web browser window, sign on tooyour **SpringCM** company site as administrator.</span></span>

8. <span data-ttu-id="27450-169">Hello menu u góry hello, kliknij przycisk **przejdź do**, kliknij przycisk **preferencje**, a następnie na powitania **preferencje konta** kliknij **logowania jednokrotnego SAML**.</span><span class="sxs-lookup"><span data-stu-id="27450-169">In hello menu on hello top, click **GO TO**, click **Preferences**, and then, in hello **Account Preferences** section, click **SAML SSO**.</span></span>
   
    <span data-ttu-id="27450-170">![LOGOWANIA JEDNOKROTNEGO SAML](./media/active-directory-saas-spring-cm-tutorial/ic797051.png "LOGOWANIA JEDNOKROTNEGO SAML")</span><span class="sxs-lookup"><span data-stu-id="27450-170">![SAML SSO](./media/active-directory-saas-spring-cm-tutorial/ic797051.png "SAML SSO")</span></span>

9. <span data-ttu-id="27450-171">W sekcji konfiguracji dostawcy tożsamości hello wykonaj hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="27450-171">In hello Identity Provider Configuration section, perform hello following steps:</span></span>
   
    <span data-ttu-id="27450-172">![Konfiguracja dostawcy tożsamości](./media/active-directory-saas-spring-cm-tutorial/ic797052.png "konfiguracji dostawcy tożsamości")</span><span class="sxs-lookup"><span data-stu-id="27450-172">![Identity Provider Configuration](./media/active-directory-saas-spring-cm-tutorial/ic797052.png "Identity Provider Configuration")</span></span>
    
    <span data-ttu-id="27450-173">a.</span><span class="sxs-lookup"><span data-stu-id="27450-173">a.</span></span> <span data-ttu-id="27450-174">tooupload pobrany certyfikat usługi Azure Active Directory, kliknij przycisk **wybierz wystawcy certyfikatu** lub **zmiany wystawcy certyfikatu**.</span><span class="sxs-lookup"><span data-stu-id="27450-174">tooupload your downloaded Azure Active Directory certificate, click **Select Issuer Certificate** or **Change Issuer Certificate**.</span></span>
    
    <span data-ttu-id="27450-175">b.</span><span class="sxs-lookup"><span data-stu-id="27450-175">b.</span></span> <span data-ttu-id="27450-176">Wklej **identyfikator jednostki SAML** wartość, która została skopiowana z portalu Azure do hello **wystawcy** pola tekstowego.</span><span class="sxs-lookup"><span data-stu-id="27450-176">Paste **SAML Entity ID** value, which you have copied from Azure portal into hello **Issuer** textbox.</span></span>
    
    <span data-ttu-id="27450-177">c.</span><span class="sxs-lookup"><span data-stu-id="27450-177">c.</span></span> <span data-ttu-id="27450-178">Wklej **SAML pojedynczy znak na adres URL usługi** wartość, która została skopiowana z hello portalu Azure do hello **punktu końcowego usługi dostawcy (SP) zainicjował** pola tekstowego.</span><span class="sxs-lookup"><span data-stu-id="27450-178">Paste **SAML Single Sign-On Service URL** value, which you have copied from hello Azure portal into hello **Service Provider (SP) Initiated Endpoint** textbox.</span></span>
            
    <span data-ttu-id="27450-179">d.</span><span class="sxs-lookup"><span data-stu-id="27450-179">d.</span></span> <span data-ttu-id="27450-180">Wybierz **SAML włączone** jako **włączyć**.</span><span class="sxs-lookup"><span data-stu-id="27450-180">Select **SAML Enabled** as **Enable**.</span></span>

    <span data-ttu-id="27450-181">e.</span><span class="sxs-lookup"><span data-stu-id="27450-181">e.</span></span> <span data-ttu-id="27450-182">Kliknij pozycję **Zapisz**.</span><span class="sxs-lookup"><span data-stu-id="27450-182">Click **Save**.</span></span>
 
> [!TIP]
> <span data-ttu-id="27450-183">Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz hello [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji hello!</span><span class="sxs-lookup"><span data-stu-id="27450-183">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="27450-184">Po dodaniu tej aplikacji z hello **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij hello **rejestracji jednokrotnej** hello kartę i dostępu do osadzonych dokumentacji za pośrednictwem hello  **Konfiguracja** sekcji u dołu hello.</span><span class="sxs-lookup"><span data-stu-id="27450-184">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="27450-185">Więcej o hello osadzonych dokumentacji funkcji w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="27450-185">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="27450-186">Tworzenie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="27450-186">Creating an Azure AD test user</span></span>
<span data-ttu-id="27450-187">Celem Hello w tej sekcji jest toocreate użytkownika testowego, w portalu Azure o nazwie Simona Britta hello.</span><span class="sxs-lookup"><span data-stu-id="27450-187">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Tworzenie użytkowników usługi Azure AD][100]

<span data-ttu-id="27450-189">**toocreate użytkownika testowego w usłudze Azure AD, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="27450-189">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="27450-190">W hello **portalu Azure**na temat hello w lewym okienku nawigacji, kliknij przycisk **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="27450-190">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-spring-cm-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="27450-192">toodisplay hello listę użytkowników, przejdź zbyt**użytkowników i grup** i kliknij przycisk **wszyscy użytkownicy**.</span><span class="sxs-lookup"><span data-stu-id="27450-192">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-spring-cm-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="27450-194">Witaj tooopen **użytkownika** okna dialogowego, kliknij przycisk **Dodaj** u góry hello hello okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="27450-194">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-spring-cm-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="27450-196">Na powitania **użytkownika** okna dialogowego wykonaj hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="27450-196">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-spring-cm-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="27450-198">a.</span><span class="sxs-lookup"><span data-stu-id="27450-198">a.</span></span> <span data-ttu-id="27450-199">W hello **nazwa** pole tekstowe, typ **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="27450-199">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="27450-200">b.</span><span class="sxs-lookup"><span data-stu-id="27450-200">b.</span></span> <span data-ttu-id="27450-201">W hello **nazwy użytkownika** pole tekstowe, hello typu **adres e-mail** z BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="27450-201">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="27450-202">c.</span><span class="sxs-lookup"><span data-stu-id="27450-202">c.</span></span> <span data-ttu-id="27450-203">Wybierz **Pokaż hasło** i zanotuj wartość hello hello **hasło**.</span><span class="sxs-lookup"><span data-stu-id="27450-203">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="27450-204">d.</span><span class="sxs-lookup"><span data-stu-id="27450-204">d.</span></span> <span data-ttu-id="27450-205">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="27450-205">Click **Create**.</span></span>
 
### <a name="creating-a-springcm-test-user"></a><span data-ttu-id="27450-206">Tworzenie użytkownika testowego SpringCM</span><span class="sxs-lookup"><span data-stu-id="27450-206">Creating a SpringCM test user</span></span>

<span data-ttu-id="27450-207">toolog użytkowników usługi Azure Active Directory tooenable w tooSpringCM, muszą mieć przydzielone do SpringCM.</span><span class="sxs-lookup"><span data-stu-id="27450-207">tooenable Azure Active Directory users toolog in tooSpringCM, they must be provisioned into SpringCM.</span></span> <span data-ttu-id="27450-208">W przypadku hello SpringCM Inicjowanie obsługi to zadanie ręczne.</span><span class="sxs-lookup"><span data-stu-id="27450-208">In hello case of SpringCM, provisioning is a manual task.</span></span>

>[!NOTE]
><span data-ttu-id="27450-209">Aby uzyskać więcej informacji, zobacz [tworzenie i edytowanie użytkownika SpringCM](http://knowledge.springcm.com/create-and-edit-a-springcm-user).</span><span class="sxs-lookup"><span data-stu-id="27450-209">For more information, see [Create and Edit a SpringCM User](http://knowledge.springcm.com/create-and-edit-a-springcm-user).</span></span> 

<span data-ttu-id="27450-210">**tooprovision tooSpringCM konta użytkownika, należy wykonać hello następujące kroki:**</span><span class="sxs-lookup"><span data-stu-id="27450-210">**tooprovision a user account tooSpringCM, perform hello following steps:**</span></span>

1. <span data-ttu-id="27450-211">Zaloguj się za tooyour **SpringCM** witryny firmy jako administrator.</span><span class="sxs-lookup"><span data-stu-id="27450-211">Log in tooyour **SpringCM** company site as administrator.</span></span>

2. <span data-ttu-id="27450-212">Kliknij przycisk **GOTO**, a następnie kliknij przycisk **KSIĄŻKI ADRESOWEJ**.</span><span class="sxs-lookup"><span data-stu-id="27450-212">Click **GOTO**, and then click **ADDRESS BOOK**.</span></span>
   
    <span data-ttu-id="27450-213">![Utwórz użytkownika](./media/active-directory-saas-spring-cm-tutorial/ic797054.png "Tworzenie użytkownika")</span><span class="sxs-lookup"><span data-stu-id="27450-213">![Create User](./media/active-directory-saas-spring-cm-tutorial/ic797054.png "Create User")</span></span>

3. <span data-ttu-id="27450-214">Kliknij przycisk **Utwórz użytkownika**.</span><span class="sxs-lookup"><span data-stu-id="27450-214">Click **Create User**.</span></span>

4. <span data-ttu-id="27450-215">Wybierz **roli użytkownika**.</span><span class="sxs-lookup"><span data-stu-id="27450-215">Select a **User Role**.</span></span>

5. <span data-ttu-id="27450-216">Wybierz **wysyłania wiadomości E-mail o aktywacji**.</span><span class="sxs-lookup"><span data-stu-id="27450-216">Select **Send Activation Email**.</span></span>

6. <span data-ttu-id="27450-217">Typ hello imię, nazwisko i adres e-mail prawidłowe konto użytkownika usługi Azure Active Directory, które chcesz tooprovision do hello związanych z pól tekstowych.</span><span class="sxs-lookup"><span data-stu-id="27450-217">Type hello first name, last name, and email address of a valid Azure Active Directory user account you want tooprovision into hello related textboxes.</span></span>

7. <span data-ttu-id="27450-218">Dodaj hello użytkownika tooa **grupy zabezpieczeń**.</span><span class="sxs-lookup"><span data-stu-id="27450-218">Add hello user tooa **Security group**.</span></span>

8. <span data-ttu-id="27450-219">Kliknij pozycję **Zapisz**.</span><span class="sxs-lookup"><span data-stu-id="27450-219">Click **Save**.</span></span>

  >[!NOTE]
  ><span data-ttu-id="27450-220">Możesz użyć innych SpringCM użytkownika konta tworzenia narzędzi lub interfejsów API dostarczonych przez SpringCM tooprovision kont użytkowników usługi AAD.</span><span class="sxs-lookup"><span data-stu-id="27450-220">You can use any other SpringCM user account creation tools or APIs provided by SpringCM tooprovision AAD user accounts.</span></span>  
  > 

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="27450-221">Przypisanie użytkownika testowego hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="27450-221">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="27450-222">W tej sekcji możesz włączyć toouse Simona Britta Azure logowania jednokrotnego za udzielanie dostępu tooSpringCM.</span><span class="sxs-lookup"><span data-stu-id="27450-222">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooSpringCM.</span></span>

![Przypisz użytkownika][200] 

<span data-ttu-id="27450-224">**tooassign tooSpringCM Simona Britta wykonaj hello następujące kroki:**</span><span class="sxs-lookup"><span data-stu-id="27450-224">**tooassign Britta Simon tooSpringCM, perform hello following steps:**</span></span>

1. <span data-ttu-id="27450-225">W portalu Azure hello, otwórz widok aplikacji hello, a następnie przejdź do widoku katalogu toohello i przejść za**aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="27450-225">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Przypisz użytkownika][201] 

2. <span data-ttu-id="27450-227">Z listy aplikacji hello wybierz **SpringCM**.</span><span class="sxs-lookup"><span data-stu-id="27450-227">In hello applications list, select **SpringCM**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-spring-cm-tutorial/tutorial_springcm_app.png) 

3. <span data-ttu-id="27450-229">W menu powitania po lewej stronie powitania kliknij **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="27450-229">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Przypisz użytkownika][202] 

4. <span data-ttu-id="27450-231">Kliknij przycisk **Dodaj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="27450-231">Click **Add** button.</span></span> <span data-ttu-id="27450-232">Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="27450-232">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Przypisz użytkownika][203]

5. <span data-ttu-id="27450-234">Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** hello listy użytkowników.</span><span class="sxs-lookup"><span data-stu-id="27450-234">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="27450-235">Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="27450-235">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="27450-236">Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="27450-236">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="27450-237">Testowanie rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="27450-237">Testing single sign-on</span></span>

<span data-ttu-id="27450-238">W tej sekcji można przetestować konfiguracji usługi Azure AD pojedynczego logowania jednokrotnego przy użyciu hello panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="27450-238">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>
 
<span data-ttu-id="27450-239">Po kliknięciu kafelka SpringCM hello w hello Panel dostępu, należy pobrać automatycznie zalogowane tooyour SpringCM aplikacji.</span><span class="sxs-lookup"><span data-stu-id="27450-239">When you click hello SpringCM tile in hello Access Panel, you should get automatically signed-on tooyour SpringCM application.</span></span>

<span data-ttu-id="27450-240">Aby uzyskać więcej informacji na temat hello Panel dostępu, zobacz [toohello wprowadzenie panelu dostępu](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="27450-240">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="27450-241">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="27450-241">Additional resources</span></span>

* [<span data-ttu-id="27450-242">Lista samouczków dotyczących tooIntegrate aplikacji SaaS w usłudze Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="27450-242">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="27450-243">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="27450-243">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-spring-cm-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-spring-cm-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-spring-cm-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-spring-cm-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-spring-cm-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-spring-cm-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-spring-cm-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-spring-cm-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-spring-cm-tutorial/tutorial_general_203.png

