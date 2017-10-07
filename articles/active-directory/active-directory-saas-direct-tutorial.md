---
title: "Samouczek: Integracji Azure Active Directory bezpośrednio | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak tooconfigure logowanie jednokrotne między usługą Azure Active Directory i bezpośrednie."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 7c2cd1f0-d14c-42f0-94a8-9b800008b285
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/16/2017
ms.author: jeedes
ms.openlocfilehash: ac663070b39e55eade2c43814b63a9d0374c7316
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-direct"></a><span data-ttu-id="3efa3-103">Samouczek: Integracji Azure Active Directory bezpośrednio</span><span class="sxs-lookup"><span data-stu-id="3efa3-103">Tutorial: Azure Active Directory integration with Direct</span></span>

<span data-ttu-id="3efa3-104">Z tego samouczka, dowiesz się, jak toointegrate bezpośrednio w usłudze Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="3efa3-104">In this tutorial, you learn how toointegrate Direct with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="3efa3-105">Integrowanie bezpośrednio z usługą Azure AD zapewnia hello następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="3efa3-105">Integrating Direct with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="3efa3-106">Można kontrolować w usłudze Azure AD, kto ma dostęp do tooDirect</span><span class="sxs-lookup"><span data-stu-id="3efa3-106">You can control in Azure AD who has access tooDirect</span></span>
- <span data-ttu-id="3efa3-107">Można włączyć użytkownika użytkownicy tooautomatically get zalogowane tooDirect (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="3efa3-107">You can enable your users tooautomatically get signed-on tooDirect (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="3efa3-108">Możesz zarządzać kont w jednej centralnej lokalizacji - hello portalu Azure</span><span class="sxs-lookup"><span data-stu-id="3efa3-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="3efa3-109">Jeśli chcesz tooknow więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="3efa3-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="3efa3-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="3efa3-110">Prerequisites</span></span>

<span data-ttu-id="3efa3-111">tooconfigure integracji z usługą Azure AD bezpośrednio, należy hello następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="3efa3-111">tooconfigure Azure AD integration with Direct, you need hello following items:</span></span>

- <span data-ttu-id="3efa3-112">Subskrypcję usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="3efa3-112">An Azure AD subscription</span></span>
- <span data-ttu-id="3efa3-113">Bezpośrednie logowanie jednokrotne włączone subskrypcji</span><span class="sxs-lookup"><span data-stu-id="3efa3-113">A Direct single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="3efa3-114">tootest hello kroków w tym samouczku, zaleca się przy użyciu środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="3efa3-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="3efa3-115">tootest hello kroki opisane w tym samouczku, należy stosować te zalecenia:</span><span class="sxs-lookup"><span data-stu-id="3efa3-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="3efa3-116">Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="3efa3-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="3efa3-117">Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz pobrać miesięczna wersja próbna [tutaj](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="3efa3-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="3efa3-118">Opis scenariusza</span><span class="sxs-lookup"><span data-stu-id="3efa3-118">Scenario description</span></span>
<span data-ttu-id="3efa3-119">W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym.</span><span class="sxs-lookup"><span data-stu-id="3efa3-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="3efa3-120">Scenariusz Hello opisane w tym samouczku składa się z dwóch głównych elementów:</span><span class="sxs-lookup"><span data-stu-id="3efa3-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="3efa3-121">Dodawanie bezpośrednio z galerii hello</span><span class="sxs-lookup"><span data-stu-id="3efa3-121">Adding Direct from hello gallery</span></span>
2. <span data-ttu-id="3efa3-122">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="3efa3-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-direct-from-hello-gallery"></a><span data-ttu-id="3efa3-123">Dodawanie bezpośrednio z galerii hello</span><span class="sxs-lookup"><span data-stu-id="3efa3-123">Adding Direct from hello gallery</span></span>
<span data-ttu-id="3efa3-124">tooconfigure hello integracji bezpośrednio do usługi Azure AD, należy tooadd bezpośrednio z hello galerii tooyour listę zarządzanych aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="3efa3-124">tooconfigure hello integration of Direct into Azure AD, you need tooadd Direct from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="3efa3-125">**tooadd bezpośrednio z galerii hello, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="3efa3-125">**tooadd Direct from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="3efa3-126">W hello  **[portalu Azure](https://portal.azure.com)**na temat hello panelu nawigacji po lewej stronie, kliknij przycisk **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="3efa3-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Usługa Active Directory][1]

2. <span data-ttu-id="3efa3-128">Przejdź za**aplikacje dla przedsiębiorstw**.</span><span class="sxs-lookup"><span data-stu-id="3efa3-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="3efa3-129">Następnie przejdź zbyt**wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="3efa3-129">Then go too**All applications**.</span></span>

    ![Aplikacje][2]
    
3. <span data-ttu-id="3efa3-131">tooadd nową aplikację, kliknij przycisk **nowej aplikacji** przycisk u góry hello okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="3efa3-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplikacje][3]

4. <span data-ttu-id="3efa3-133">W polu wyszukiwania hello wpisz **bezpośredniego**.</span><span class="sxs-lookup"><span data-stu-id="3efa3-133">In hello search box, type **Direct**.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-direct-tutorial/tutorial_direct_search.png)

5. <span data-ttu-id="3efa3-135">W panelu wyników hello, wybierz **bezpośredniego**, a następnie kliknij przycisk **Dodaj** przycisk aplikacji hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="3efa3-135">In hello results panel, select **Direct**, and then click **Add** button tooadd hello application.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-direct-tutorial/tutorial_direct_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="3efa3-137">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="3efa3-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="3efa3-138">W tej sekcji Konfigurowanie i testowanie usługi Azure AD rejestracji jednokrotnej z bezpośrednio na podstawie testu użytkownika o nazwie "Britta Simona".</span><span class="sxs-lookup"><span data-stu-id="3efa3-138">In this section, you configure and test Azure AD single sign-on with Direct based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="3efa3-139">Dla pojedynczego logowania jednokrotnego toowork usługi Azure AD musi tooknow użytkownika odpowiednikiem hello w bezpośrednie jest tooa użytkownika w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="3efa3-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Direct is tooa user in Azure AD.</span></span> <span data-ttu-id="3efa3-140">Innymi słowy relację łącza między użytkownika usługi Azure AD i hello powiązanych użytkownika na potrzeby bezpośredniego toobe ustanowić.</span><span class="sxs-lookup"><span data-stu-id="3efa3-140">In other words, a link relationship between an Azure AD user and hello related user in Direct needs toobe established.</span></span>

<span data-ttu-id="3efa3-141">Bezpośrednie, przypisywanie wartości hello hello **nazwy użytkownika** w usłudze Azure AD jako wartość hello hello **Username** tooestablish hello łącze relacji.</span><span class="sxs-lookup"><span data-stu-id="3efa3-141">In Direct, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="3efa3-142">tooconfigure i testowych usługi Azure AD logowanie jednokrotne bezpośrednio, należy po bloków konstrukcyjnych hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="3efa3-142">tooconfigure and test Azure AD single sign-on with Direct, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="3efa3-143">**[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configuring-azure-ad-single-sign-on)**  -tooenable Twojego toouse użytkowników tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="3efa3-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="3efa3-144">**[Tworzenie użytkownika testowego usługi Azure AD](#creating-an-azure-ad-test-user)**  -tootest usługi Azure AD rejestracji jednokrotnej z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="3efa3-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="3efa3-145">**[Tworzenie użytkownika testowego bezpośredniego](#creating-a-direct-test-user)**  -toohave odpowiednikiem Simona Britta w bezpośredniej, który jest połączony toohello usługi Azure AD reprezentację użytkownika.</span><span class="sxs-lookup"><span data-stu-id="3efa3-145">**[Creating a Direct test user](#creating-a-direct-test-user)** - toohave a counterpart of Britta Simon in Direct that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="3efa3-146">**[Przypisanie użytkownika testowego hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Simona Britta toouse usługi Azure AD rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="3efa3-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="3efa3-147">**[Testowanie rejestracji jednokrotnej](#testing-single-sign-on)**  -tooverify czy hello konfiguracji działania.</span><span class="sxs-lookup"><span data-stu-id="3efa3-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="3efa3-148">Konfigurowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="3efa3-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="3efa3-149">W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w hello portalu Azure i skonfigurować logowanie jednokrotne w aplikacji bezpośrednio.</span><span class="sxs-lookup"><span data-stu-id="3efa3-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Direct application.</span></span>

<span data-ttu-id="3efa3-150">**tooconfigure usługi Azure AD rejestracji jednokrotnej bezpośrednio, wykonaj hello następujące kroki:**</span><span class="sxs-lookup"><span data-stu-id="3efa3-150">**tooconfigure Azure AD single sign-on with Direct, perform hello following steps:**</span></span>

1. <span data-ttu-id="3efa3-151">W portalu Azure na powitania hello **bezpośredniego** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.</span><span class="sxs-lookup"><span data-stu-id="3efa3-151">In hello Azure portal, on hello **Direct** application integration page, click **Single sign-on**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej][4]

2. <span data-ttu-id="3efa3-153">Na powitania **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** tooenable rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="3efa3-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-direct-tutorial/tutorial_direct_samlbase.png)

3. <span data-ttu-id="3efa3-155">Na powitania **adresy URL i bezpośredniego domeny** sekcji, jeśli chcesz, aby aplikacja hello tooconfigure w **IDP** inicjowane tryb:</span><span class="sxs-lookup"><span data-stu-id="3efa3-155">On hello **Direct Domain and URLs** section, If you wish tooconfigure hello application in **IDP** initiated mode:</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-direct-tutorial/tutorial_direct_url.png)

    <span data-ttu-id="3efa3-157">W hello **identyfikator** pole tekstowe, wprowadź adres URL hello:`https://direct4b.com/`</span><span class="sxs-lookup"><span data-stu-id="3efa3-157">In hello **Identifier** textbox, type hello URL: `https://direct4b.com/`</span></span>

4. <span data-ttu-id="3efa3-158">Sprawdź **Pokaż zaawansowane ustawienia adresu URL**, jeśli chcesz, aby aplikacja hello tooconfigure w **SP** inicjowane tryb:</span><span class="sxs-lookup"><span data-stu-id="3efa3-158">Check **Show advanced URL settings**, If you wish tooconfigure hello application in **SP** initiated mode:</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-direct-tutorial/tutorial_direct_url1.png)

     <span data-ttu-id="3efa3-160">W hello **adres URL logowania** pole tekstowe, wprowadź adres URL hello:`https://direct4b.com/sso`</span><span class="sxs-lookup"><span data-stu-id="3efa3-160">In hello **Sign-on URL** textbox, type hello URL: `https://direct4b.com/sso`</span></span> 
    
5. <span data-ttu-id="3efa3-161">Na powitania **certyfikat podpisywania SAML** kliknij **XML metadanych** , a następnie zapisz plik metadanych hello na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="3efa3-161">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-direct-tutorial/tutorial_direct_certificate.png) 

6. <span data-ttu-id="3efa3-163">Kliknij przycisk **zapisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="3efa3-163">Click **Save** button.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-direct-tutorial/tutorial_general_400.png)

7. <span data-ttu-id="3efa3-165">tooconfigure rejestracji jednokrotnej w **bezpośredniego** strony, należy pobrać hello toosend **XML metadanych** za[bezpośrednio z pomocą techniczną](https://direct4b.com/ja/support.html#inquiry).</span><span class="sxs-lookup"><span data-stu-id="3efa3-165">tooconfigure single sign-on on **Direct** side, you need toosend hello downloaded **Metadata XML** too[Direct support team](https://direct4b.com/ja/support.html#inquiry).</span></span> 

> [!TIP]
> <span data-ttu-id="3efa3-166">Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz hello [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji hello!</span><span class="sxs-lookup"><span data-stu-id="3efa3-166">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="3efa3-167">Po dodaniu tej aplikacji z hello **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij hello **rejestracji jednokrotnej** hello kartę i dostępu do osadzonych dokumentacji za pośrednictwem hello  **Konfiguracja** sekcji u dołu hello.</span><span class="sxs-lookup"><span data-stu-id="3efa3-167">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="3efa3-168">Więcej o hello osadzonych dokumentacji funkcji w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="3efa3-168">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="3efa3-169">Tworzenie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="3efa3-169">Creating an Azure AD test user</span></span>
<span data-ttu-id="3efa3-170">Celem Hello w tej sekcji jest toocreate użytkownika testowego, w portalu Azure o nazwie Simona Britta hello.</span><span class="sxs-lookup"><span data-stu-id="3efa3-170">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Tworzenie użytkowników usługi Azure AD][100]

<span data-ttu-id="3efa3-172">**toocreate użytkownika testowego w usłudze Azure AD, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="3efa3-172">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="3efa3-173">W hello **portalu Azure**na temat hello w lewym okienku nawigacji, kliknij przycisk **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="3efa3-173">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-direct-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="3efa3-175">toodisplay hello listę użytkowników, przejdź zbyt**użytkowników i grup** i kliknij przycisk **wszyscy użytkownicy**.</span><span class="sxs-lookup"><span data-stu-id="3efa3-175">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-direct-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="3efa3-177">Witaj tooopen **użytkownika** okna dialogowego, kliknij przycisk **Dodaj** u góry hello hello okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="3efa3-177">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-direct-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="3efa3-179">Na powitania **użytkownika** okna dialogowego wykonaj hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="3efa3-179">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-direct-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="3efa3-181">a.</span><span class="sxs-lookup"><span data-stu-id="3efa3-181">a.</span></span> <span data-ttu-id="3efa3-182">W hello **nazwa** pole tekstowe, typ **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="3efa3-182">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="3efa3-183">b.</span><span class="sxs-lookup"><span data-stu-id="3efa3-183">b.</span></span> <span data-ttu-id="3efa3-184">W hello **nazwy użytkownika** pole tekstowe, hello typu **adres e-mail** z BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="3efa3-184">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="3efa3-185">c.</span><span class="sxs-lookup"><span data-stu-id="3efa3-185">c.</span></span> <span data-ttu-id="3efa3-186">Wybierz **Pokaż hasło** i zanotuj wartość hello hello **hasło**.</span><span class="sxs-lookup"><span data-stu-id="3efa3-186">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="3efa3-187">d.</span><span class="sxs-lookup"><span data-stu-id="3efa3-187">d.</span></span> <span data-ttu-id="3efa3-188">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="3efa3-188">Click **Create**.</span></span>
 
### <a name="creating-a-direct-test-user"></a><span data-ttu-id="3efa3-189">Tworzenie użytkownika Direct — test</span><span class="sxs-lookup"><span data-stu-id="3efa3-189">Creating a Direct test user</span></span>

<span data-ttu-id="3efa3-190">W tej sekcji należy utworzyć użytkownika o nazwie Simona Britta w bezpośredniej.</span><span class="sxs-lookup"><span data-stu-id="3efa3-190">In this section, you create a user called Britta Simon in Direct.</span></span> <span data-ttu-id="3efa3-191">Praca z [bezpośrednio z pomocą techniczną](https://direct4b.com/ja/support.html#inquiry) do dodawania użytkowników hello hello bezpośredniego platformy.</span><span class="sxs-lookup"><span data-stu-id="3efa3-191">Work with [Direct support team](https://direct4b.com/ja/support.html#inquiry) to add hello users in hello Direct platform.</span></span> <span data-ttu-id="3efa3-192">Użytkownicy muszą utworzyć i aktywowana, aby użyć rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="3efa3-192">Users must be created and activated before you use single sign-on.</span></span> 

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="3efa3-193">Przypisanie użytkownika testowego hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="3efa3-193">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="3efa3-194">W tej sekcji możesz włączyć toouse Simona Britta Azure logowania jednokrotnego za udzielanie dostępu tooDirect.</span><span class="sxs-lookup"><span data-stu-id="3efa3-194">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooDirect.</span></span>

![Przypisz użytkownika][200] 

<span data-ttu-id="3efa3-196">**tooassign tooDirect Simona Britta wykonaj hello następujące kroki:**</span><span class="sxs-lookup"><span data-stu-id="3efa3-196">**tooassign Britta Simon tooDirect, perform hello following steps:**</span></span>

1. <span data-ttu-id="3efa3-197">W portalu Azure hello, otwórz widok aplikacji hello, a następnie przejdź do widoku katalogu toohello i przejść za**aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="3efa3-197">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Przypisz użytkownika][201] 

2. <span data-ttu-id="3efa3-199">Z listy aplikacji hello wybierz **bezpośredniego**.</span><span class="sxs-lookup"><span data-stu-id="3efa3-199">In hello applications list, select **Direct**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-direct-tutorial/tutorial_direct_app.png) 

3. <span data-ttu-id="3efa3-201">W menu powitania po lewej stronie powitania kliknij **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="3efa3-201">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Przypisz użytkownika][202] 

4. <span data-ttu-id="3efa3-203">Kliknij przycisk **Dodaj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="3efa3-203">Click **Add** button.</span></span> <span data-ttu-id="3efa3-204">Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="3efa3-204">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Przypisz użytkownika][203]

5. <span data-ttu-id="3efa3-206">Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** hello listy użytkowników.</span><span class="sxs-lookup"><span data-stu-id="3efa3-206">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="3efa3-207">Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="3efa3-207">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="3efa3-208">Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="3efa3-208">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="3efa3-209">Testowanie rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="3efa3-209">Testing single sign-on</span></span>

<span data-ttu-id="3efa3-210">W tej sekcji można przetestować konfiguracji usługi Azure AD pojedynczego logowania jednokrotnego przy użyciu hello panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="3efa3-210">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

1. <span data-ttu-id="3efa3-211">Jeśli chcesz, aby tootest w **tryb zainicjował IDP**:</span><span class="sxs-lookup"><span data-stu-id="3efa3-211">If you wish tootest in **IDP Initiated Mode**:</span></span>

    <span data-ttu-id="3efa3-212">Po kliknięciu hello **bezpośredniego** kafelka w hello Panel dostępu, należy pobrać zalogowane automatycznie tooyour **bezpośredniego** aplikacji.</span><span class="sxs-lookup"><span data-stu-id="3efa3-212">When you click hello **Direct** tile in hello Access Panel, you should get automatically signed-on tooyour **Direct** application.</span></span>

2. <span data-ttu-id="3efa3-213">Jeśli chcesz, aby tootest w **SP zainicjował tryb**:</span><span class="sxs-lookup"><span data-stu-id="3efa3-213">If you wish tootest in **SP Initiated Mode**:</span></span>
    
    <span data-ttu-id="3efa3-214">a.</span><span class="sxs-lookup"><span data-stu-id="3efa3-214">a.</span></span> <span data-ttu-id="3efa3-215">Polecenie hello **bezpośredniego** kafelka w hello panelu dostępu i będzie strona logowania aplikacji toohello przekierowane.</span><span class="sxs-lookup"><span data-stu-id="3efa3-215">Click on hello **Direct** tile in hello Access Panel and you will be redirected toohello application sign-on page.</span></span>

    <span data-ttu-id="3efa3-216">b.</span><span class="sxs-lookup"><span data-stu-id="3efa3-216">b.</span></span> <span data-ttu-id="3efa3-217">Dane wejściowe użytkownika `subdomain` w pole tekstowe hello wyświetlane i naciśnij klawisz "次へ (dalej)", a powinien uzyskać automatycznie zalogowane tooyour **bezpośredniego** aplikacji.</span><span class="sxs-lookup"><span data-stu-id="3efa3-217">Input your `subdomain` in hello textbox displayed and press '次へ (Next)' and you should get automatically signed-on tooyour **Direct** application .</span></span>
    
<span data-ttu-id="3efa3-218">Aby uzyskać więcej informacji na temat panelu dostępu, zobacz [toohello wprowadzenie panelu dostępu](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="3efa3-218">For more information about the Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="3efa3-219">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="3efa3-219">Additional resources</span></span>

* [<span data-ttu-id="3efa3-220">Lista samouczków dotyczących tooIntegrate aplikacji SaaS w usłudze Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="3efa3-220">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="3efa3-221">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="3efa3-221">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-direct-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-direct-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-direct-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-direct-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-direct-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-direct-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-direct-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-direct-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-direct-tutorial/tutorial_general_203.png

