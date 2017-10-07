---
title: 'Samouczek: Integracji Azure Active Directory z Wikispaces | Dokumentacja firmy Microsoft'
description: "Dowiedz się, jak tooconfigure logowanie jednokrotne między usługą Azure Active Directory i Wikispaces."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 665b95aa-f7f5-4406-9e2a-6fc299a1599c
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/08/2017
ms.author: jeedes
ms.openlocfilehash: eb5b72e60b415cb657b70ba530df731ae14b0425
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-wikispaces"></a><span data-ttu-id="ea261-103">Samouczek: Integracji Azure Active Directory z Wikispaces</span><span class="sxs-lookup"><span data-stu-id="ea261-103">Tutorial: Azure Active Directory integration with Wikispaces</span></span>

<span data-ttu-id="ea261-104">Z tego samouczka, dowiesz się, jak toointegrate Wikispaces w usłudze Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="ea261-104">In this tutorial, you learn how toointegrate Wikispaces with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="ea261-105">Integracja z usługą Azure AD Wikispaces zapewnia hello następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="ea261-105">Integrating Wikispaces with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="ea261-106">Można kontrolować w usłudze Azure AD, kto ma dostęp do tooWikispaces</span><span class="sxs-lookup"><span data-stu-id="ea261-106">You can control in Azure AD who has access tooWikispaces</span></span>
- <span data-ttu-id="ea261-107">Można włączyć użytkownika użytkownicy tooautomatically get zalogowane tooWikispaces (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="ea261-107">You can enable your users tooautomatically get signed-on tooWikispaces (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="ea261-108">Możesz zarządzać kont w jednej centralnej lokalizacji - hello portalu Azure</span><span class="sxs-lookup"><span data-stu-id="ea261-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="ea261-109">Jeśli chcesz tooknow więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="ea261-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ea261-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="ea261-110">Prerequisites</span></span>

<span data-ttu-id="ea261-111">tooconfigure integracji z usługą Azure AD z Wikispaces należy hello następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="ea261-111">tooconfigure Azure AD integration with Wikispaces, you need hello following items:</span></span>

- <span data-ttu-id="ea261-112">Subskrypcję usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="ea261-112">An Azure AD subscription</span></span>
- <span data-ttu-id="ea261-113">Wikispaces logowanie jednokrotne włączone subskrypcji</span><span class="sxs-lookup"><span data-stu-id="ea261-113">A Wikispaces single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="ea261-114">tootest hello kroków w tym samouczku, zaleca się przy użyciu środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="ea261-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="ea261-115">tootest hello kroki opisane w tym samouczku, należy stosować te zalecenia:</span><span class="sxs-lookup"><span data-stu-id="ea261-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="ea261-116">Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="ea261-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="ea261-117">Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz pobrać miesięczna wersja próbna [tutaj](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="ea261-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="ea261-118">Opis scenariusza</span><span class="sxs-lookup"><span data-stu-id="ea261-118">Scenario description</span></span>
<span data-ttu-id="ea261-119">W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym.</span><span class="sxs-lookup"><span data-stu-id="ea261-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="ea261-120">Scenariusz Hello opisane w tym samouczku składa się z dwóch głównych elementów:</span><span class="sxs-lookup"><span data-stu-id="ea261-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="ea261-121">Dodawanie Wikispaces z galerii hello</span><span class="sxs-lookup"><span data-stu-id="ea261-121">Adding Wikispaces from hello gallery</span></span>
2. <span data-ttu-id="ea261-122">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="ea261-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-wikispaces-from-hello-gallery"></a><span data-ttu-id="ea261-123">Dodawanie Wikispaces z galerii hello</span><span class="sxs-lookup"><span data-stu-id="ea261-123">Adding Wikispaces from hello gallery</span></span>
<span data-ttu-id="ea261-124">tooconfigure hello integracji Wikispaces do usługi Azure AD, należy tooadd Wikispaces z hello galerii tooyour listę zarządzanych aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="ea261-124">tooconfigure hello integration of Wikispaces into Azure AD, you need tooadd Wikispaces from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="ea261-125">**tooadd Wikispaces z galerii hello, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="ea261-125">**tooadd Wikispaces from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="ea261-126">W hello  **[portalu Azure](https://portal.azure.com)**na temat hello panelu nawigacji po lewej stronie, kliknij przycisk **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="ea261-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Usługa Active Directory][1]

2. <span data-ttu-id="ea261-128">Przejdź za**aplikacje dla przedsiębiorstw**.</span><span class="sxs-lookup"><span data-stu-id="ea261-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="ea261-129">Następnie przejdź zbyt**wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="ea261-129">Then go too**All applications**.</span></span>

    ![Aplikacje][2]
    
3. <span data-ttu-id="ea261-131">tooadd nową aplikację, kliknij przycisk **nowej aplikacji** przycisk u góry hello okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="ea261-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplikacje][3]

4. <span data-ttu-id="ea261-133">W polu wyszukiwania hello wpisz **Wikispaces**.</span><span class="sxs-lookup"><span data-stu-id="ea261-133">In hello search box, type **Wikispaces**.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-wikispaces-tutorial/tutorial_wikispaces_search.png)

5. <span data-ttu-id="ea261-135">W panelu wyników hello zaznacz **Wikispaces**, a następnie kliknij przycisk **Dodaj** przycisk aplikacji hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="ea261-135">In hello results panel, select **Wikispaces**, and then click **Add** button tooadd hello application.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-wikispaces-tutorial/tutorial_wikispaces_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="ea261-137">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="ea261-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="ea261-138">W tej sekcji skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z Wikispaces w oparciu o nazwie "Britta Simona" użytkownika testowego.</span><span class="sxs-lookup"><span data-stu-id="ea261-138">In this section, you configure and test Azure AD single sign-on with Wikispaces based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="ea261-139">Dla pojedynczego logowania jednokrotnego toowork usługi Azure AD musi tooknow użytkownika odpowiednikiem hello w Wikispaces jest tooa użytkownika w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="ea261-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Wikispaces is tooa user in Azure AD.</span></span> <span data-ttu-id="ea261-140">Innymi słowy relację łącza między użytkownika usługi Azure AD i hello użytkownikowi w Wikispaces musi toobe ustanowione.</span><span class="sxs-lookup"><span data-stu-id="ea261-140">In other words, a link relationship between an Azure AD user and hello related user in Wikispaces needs toobe established.</span></span>

<span data-ttu-id="ea261-141">W Wikispaces, należy przypisać wartość hello hello **nazwy użytkownika** w usłudze Azure AD jako wartość hello hello **Username** tooestablish hello łącze relacji.</span><span class="sxs-lookup"><span data-stu-id="ea261-141">In Wikispaces, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="ea261-142">tooconfigure i testowych usługi Azure AD rejestracji jednokrotnej z Wikispaces, należy po bloków konstrukcyjnych hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="ea261-142">tooconfigure and test Azure AD single sign-on with Wikispaces, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="ea261-143">**[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configuring-azure-ad-single-sign-on)**  -tooenable Twojego toouse użytkowników tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="ea261-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="ea261-144">**[Tworzenie użytkownika testowego usługi Azure AD](#creating-an-azure-ad-test-user)**  -tootest usługi Azure AD rejestracji jednokrotnej z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="ea261-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="ea261-145">**[Tworzenie użytkownika testowego Wikispaces](#creating-a-wikispaces-test-user)**  -toohave odpowiednikiem Simona Britta w Wikispaces, który jest połączony toohello usługi Azure AD reprezentację użytkownika.</span><span class="sxs-lookup"><span data-stu-id="ea261-145">**[Creating a Wikispaces test user](#creating-a-wikispaces-test-user)** - toohave a counterpart of Britta Simon in Wikispaces that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="ea261-146">**[Przypisanie użytkownika testowego hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Simona Britta toouse usługi Azure AD rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="ea261-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="ea261-147">**[Testowanie rejestracji jednokrotnej](#testing-single-sign-on)**  -tooverify czy hello konfiguracji działania.</span><span class="sxs-lookup"><span data-stu-id="ea261-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="ea261-148">Konfigurowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="ea261-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="ea261-149">W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w portalu Azure hello i skonfigurować logowanie jednokrotne w aplikacji Wikispaces.</span><span class="sxs-lookup"><span data-stu-id="ea261-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Wikispaces application.</span></span>

<span data-ttu-id="ea261-150">**tooconfigure usługi Azure AD rejestracji jednokrotnej z Wikispaces, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="ea261-150">**tooconfigure Azure AD single sign-on with Wikispaces, perform hello following steps:**</span></span>

1. <span data-ttu-id="ea261-151">W portalu Azure na powitania hello **Wikispaces** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.</span><span class="sxs-lookup"><span data-stu-id="ea261-151">In hello Azure portal, on hello **Wikispaces** application integration page, click **Single sign-on**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej][4]

2. <span data-ttu-id="ea261-153">Na powitania **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** tooenable rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="ea261-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-wikispaces-tutorial/tutorial_wikispaces_samlbase.png)

3. <span data-ttu-id="ea261-155">Na powitania **Wikispaces domeny i adres URL** sekcji, wykonaj następujące kroki hello:</span><span class="sxs-lookup"><span data-stu-id="ea261-155">On hello **Wikispaces Domain and URLs** section, perform hello following steps:</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-wikispaces-tutorial/tutorial_wikispaces_url.png)

    <span data-ttu-id="ea261-157">a.</span><span class="sxs-lookup"><span data-stu-id="ea261-157">a.</span></span> <span data-ttu-id="ea261-158">W hello **adres URL logowania** tekstowym, wpisz adres URL za pomocą hello następującego wzorca:`https://<companyname>.wikispaces.net`</span><span class="sxs-lookup"><span data-stu-id="ea261-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<companyname>.wikispaces.net`</span></span>

    <span data-ttu-id="ea261-159">b.</span><span class="sxs-lookup"><span data-stu-id="ea261-159">b.</span></span> <span data-ttu-id="ea261-160">W hello **identyfikator** tekstowym, wpisz adres URL za pomocą hello następującego wzorca:`https://session.wikispaces.net/<instancename>`</span><span class="sxs-lookup"><span data-stu-id="ea261-160">In hello **Identifier** textbox, type a URL using hello following pattern: `https://session.wikispaces.net/<instancename>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="ea261-161">Wartości te nie są prawdziwe.</span><span class="sxs-lookup"><span data-stu-id="ea261-161">These values are not real.</span></span> <span data-ttu-id="ea261-162">Zaktualizować te wartości z hello rzeczywisty adres URL logowania i identyfikator.</span><span class="sxs-lookup"><span data-stu-id="ea261-162">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="ea261-163">Skontaktuj się z [zespołem pomocy technicznej klienta Wikispaces](https://www.wikispaces.com/site/help) tooget tych wartości.</span><span class="sxs-lookup"><span data-stu-id="ea261-163">Contact [Wikispaces Client support team](https://www.wikispaces.com/site/help) tooget these values.</span></span> 

4. <span data-ttu-id="ea261-164">Na powitania **certyfikat podpisywania SAML** kliknij **XML metadanych** , a następnie zapisz plik metadanych hello na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="ea261-164">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-wikispaces-tutorial/tutorial_wikispaces_certificate.png) 

5. <span data-ttu-id="ea261-166">Kliknij przycisk **zapisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="ea261-166">Click **Save** button.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-wikispaces-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="ea261-168">tooconfigure rejestracji jednokrotnej w **Wikispaces** strony, należy pobrać hello toosend **XML metadanych** za[Wikispaces obsługuje zespołu](https://www.wikispaces.com/site/help).</span><span class="sxs-lookup"><span data-stu-id="ea261-168">tooconfigure single sign-on on **Wikispaces** side, you need toosend hello downloaded **Metadata XML** too[Wikispaces support team](https://www.wikispaces.com/site/help).</span></span> <span data-ttu-id="ea261-169">Otrzymasz powiadomienie, jak hello konfiguracji została ukończona.</span><span class="sxs-lookup"><span data-stu-id="ea261-169">You will get a notification as soon as hello configuration has been completed.</span></span>

> [!TIP]
> <span data-ttu-id="ea261-170">Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz hello [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji hello!</span><span class="sxs-lookup"><span data-stu-id="ea261-170">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="ea261-171">Po dodaniu tej aplikacji z hello **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij hello **rejestracji jednokrotnej** hello kartę i dostępu do osadzonych dokumentacji za pośrednictwem hello  **Konfiguracja** sekcji u dołu hello.</span><span class="sxs-lookup"><span data-stu-id="ea261-171">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="ea261-172">Więcej o hello osadzonych dokumentacji funkcji w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="ea261-172">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="ea261-173">Tworzenie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="ea261-173">Creating an Azure AD test user</span></span>
<span data-ttu-id="ea261-174">Celem Hello w tej sekcji jest toocreate użytkownika testowego, w portalu Azure o nazwie Simona Britta hello.</span><span class="sxs-lookup"><span data-stu-id="ea261-174">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Tworzenie użytkowników usługi Azure AD][100]

<span data-ttu-id="ea261-176">**toocreate użytkownika testowego w usłudze Azure AD, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="ea261-176">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="ea261-177">W hello **portalu Azure**na temat hello w lewym okienku nawigacji, kliknij przycisk **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="ea261-177">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-wikispaces-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="ea261-179">toodisplay hello listę użytkowników, przejdź zbyt**użytkowników i grup** i kliknij przycisk **wszyscy użytkownicy**.</span><span class="sxs-lookup"><span data-stu-id="ea261-179">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-wikispaces-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="ea261-181">Witaj tooopen **użytkownika** okna dialogowego, kliknij przycisk **Dodaj** u góry hello hello okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="ea261-181">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-wikispaces-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="ea261-183">Na powitania **użytkownika** okna dialogowego wykonaj hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="ea261-183">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-wikispaces-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="ea261-185">a.</span><span class="sxs-lookup"><span data-stu-id="ea261-185">a.</span></span> <span data-ttu-id="ea261-186">W hello **nazwa** pole tekstowe, typ **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="ea261-186">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="ea261-187">b.</span><span class="sxs-lookup"><span data-stu-id="ea261-187">b.</span></span> <span data-ttu-id="ea261-188">W hello **nazwy użytkownika** pole tekstowe, hello typu **adres e-mail** z BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="ea261-188">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="ea261-189">c.</span><span class="sxs-lookup"><span data-stu-id="ea261-189">c.</span></span> <span data-ttu-id="ea261-190">Wybierz **Pokaż hasło** i zanotuj wartość hello hello **hasło**.</span><span class="sxs-lookup"><span data-stu-id="ea261-190">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="ea261-191">d.</span><span class="sxs-lookup"><span data-stu-id="ea261-191">d.</span></span> <span data-ttu-id="ea261-192">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="ea261-192">Click **Create**.</span></span>
 
### <a name="creating-a-wikispaces-test-user"></a><span data-ttu-id="ea261-193">Tworzenie użytkownika testowego Wikispaces</span><span class="sxs-lookup"><span data-stu-id="ea261-193">Creating a Wikispaces test user</span></span>

<span data-ttu-id="ea261-194">W przypadku użytkowników usługi Azure AD toolog kolejności tooenable w tooWikispaces muszą mieć przydzielone do Wikispaces.</span><span class="sxs-lookup"><span data-stu-id="ea261-194">In order tooenable Azure AD users toolog in tooWikispaces, they must be provisioned into Wikispaces.</span></span> <span data-ttu-id="ea261-195">W przypadku hello Wikispaces Inicjowanie obsługi to zadanie ręczne.</span><span class="sxs-lookup"><span data-stu-id="ea261-195">In hello case of Wikispaces, provisioning is a manual task.</span></span>

### <a name="tooprovision-a-user-accounts-perform-hello-following-steps"></a><span data-ttu-id="ea261-196">tooprovision kont użytkowników, wykonaj hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="ea261-196">tooprovision a user accounts, perform hello following steps:</span></span>
1. <span data-ttu-id="ea261-197">Zaloguj się za tooyour **Wikispaces** witryny firmy jako administrator.</span><span class="sxs-lookup"><span data-stu-id="ea261-197">Log in tooyour **Wikispaces** company site as an administrator.</span></span>

2. <span data-ttu-id="ea261-198">Przejdź za**członków**.</span><span class="sxs-lookup"><span data-stu-id="ea261-198">Go too**Members**.</span></span>
   
    <span data-ttu-id="ea261-199">![Elementy członkowskie](./media/active-directory-saas-wikispaces-tutorial/ic787193.png "elementy członkowskie")</span><span class="sxs-lookup"><span data-stu-id="ea261-199">![Members](./media/active-directory-saas-wikispaces-tutorial/ic787193.png "Members")</span></span>

3. <span data-ttu-id="ea261-200">Kliknij przycisk hello **zaprosić użytkowników**.</span><span class="sxs-lookup"><span data-stu-id="ea261-200">Click hello **Invite People**.</span></span>
   
    <span data-ttu-id="ea261-201">![Zaproś inne osoby](./media/active-directory-saas-wikispaces-tutorial/ic787194.png "Zaproś inne osoby")</span><span class="sxs-lookup"><span data-stu-id="ea261-201">![Invite People](./media/active-directory-saas-wikispaces-tutorial/ic787194.png "Invite People")</span></span>

4. <span data-ttu-id="ea261-202">W hello **zaprosić użytkowników** sekcji, wykonaj następujące kroki hello:</span><span class="sxs-lookup"><span data-stu-id="ea261-202">In hello **Invite People** section, perform hello following steps:</span></span>
   
    <span data-ttu-id="ea261-203">![Zaproś inne osoby](./media/active-directory-saas-wikispaces-tutorial/ic787208.png "Zaproś inne osoby")</span><span class="sxs-lookup"><span data-stu-id="ea261-203">![Invite People](./media/active-directory-saas-wikispaces-tutorial/ic787208.png "Invite People")</span></span>
   
    <span data-ttu-id="ea261-204">a.</span><span class="sxs-lookup"><span data-stu-id="ea261-204">a.</span></span> <span data-ttu-id="ea261-205">Typ hello **nazwy użytkowników lub adres E-mail** z prawidłowego konta usługi AAD mają tooprovision w hello związane z pól tekstowych.</span><span class="sxs-lookup"><span data-stu-id="ea261-205">Type hello **Usernames or Email Address** of a valid AAD account you want tooprovision into hello related textboxes.</span></span>
   
    <span data-ttu-id="ea261-206">b.</span><span class="sxs-lookup"><span data-stu-id="ea261-206">b.</span></span> <span data-ttu-id="ea261-207">Kliknij przycisk **wysyłania**.</span><span class="sxs-lookup"><span data-stu-id="ea261-207">Click **Send**.</span></span>  
      
    > [!NOTE]
    > <span data-ttu-id="ea261-208">właścicielem konta usługi Azure Active Directory Hello otrzymuje wiadomość e-mail z tym kontem hello tooconfirm łącze zanim staje się aktywny.</span><span class="sxs-lookup"><span data-stu-id="ea261-208">hello Azure Active Directory account holder receives an email including a link tooconfirm hello account before it becomes active.</span></span>
    
> [!NOTE]
> <span data-ttu-id="ea261-209">Możesz użyć innych Wikispaces użytkownika konta tworzenia narzędzi lub interfejsów API dostarczonych przez Wikispaces tooprovision kont użytkowników usługi AAD.</span><span class="sxs-lookup"><span data-stu-id="ea261-209">You can use any other Wikispaces user account creation tools or APIs provided by Wikispaces tooprovision AAD user accounts.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="ea261-210">Przypisanie użytkownika testowego hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="ea261-210">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="ea261-211">W tej sekcji możesz włączyć toouse Simona Britta Azure logowania jednokrotnego za udzielanie dostępu tooWikispaces.</span><span class="sxs-lookup"><span data-stu-id="ea261-211">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooWikispaces.</span></span>

![Przypisz użytkownika][200] 

<span data-ttu-id="ea261-213">**tooassign tooWikispaces Simona Britta wykonaj hello następujące kroki:**</span><span class="sxs-lookup"><span data-stu-id="ea261-213">**tooassign Britta Simon tooWikispaces, perform hello following steps:**</span></span>

1. <span data-ttu-id="ea261-214">W portalu Azure hello, otwórz widok aplikacji hello, a następnie przejdź do widoku katalogu toohello i przejść za**aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="ea261-214">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Przypisz użytkownika][201] 

2. <span data-ttu-id="ea261-216">Z listy aplikacji hello wybierz **Wikispaces**.</span><span class="sxs-lookup"><span data-stu-id="ea261-216">In hello applications list, select **Wikispaces**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-wikispaces-tutorial/tutorial_wikispaces_app.png) 

3. <span data-ttu-id="ea261-218">W menu powitania po lewej stronie powitania kliknij **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="ea261-218">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Przypisz użytkownika][202] 

4. <span data-ttu-id="ea261-220">Kliknij przycisk **Dodaj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="ea261-220">Click **Add** button.</span></span> <span data-ttu-id="ea261-221">Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="ea261-221">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Przypisz użytkownika][203]

5. <span data-ttu-id="ea261-223">Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** hello listy użytkowników.</span><span class="sxs-lookup"><span data-stu-id="ea261-223">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="ea261-224">Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="ea261-224">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="ea261-225">Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="ea261-225">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="ea261-226">Testowanie rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="ea261-226">Testing single sign-on</span></span>

<span data-ttu-id="ea261-227">W tej sekcji można przetestować konfiguracji usługi Azure AD pojedynczego logowania jednokrotnego przy użyciu hello panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="ea261-227">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="ea261-228">Po kliknięciu powitalne Wikispaces kafelka w hello Panel dostępu, należy pobrać automatycznie zalogowane tooyour Wikispaces aplikacji.</span><span class="sxs-lookup"><span data-stu-id="ea261-228">When you click hello Wikispaces tile in hello Access Panel, you should get automatically signed-on tooyour Wikispaces application.</span></span>
<span data-ttu-id="ea261-229">Aby uzyskać więcej informacji na temat hello Panel dostępu, zobacz [toohello wprowadzenie panelu dostępu](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="ea261-229">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="ea261-230">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="ea261-230">Additional resources</span></span>

* [<span data-ttu-id="ea261-231">Lista samouczków dotyczących tooIntegrate aplikacji SaaS w usłudze Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="ea261-231">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="ea261-232">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="ea261-232">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-wikispaces-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-wikispaces-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-wikispaces-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-wikispaces-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-wikispaces-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-wikispaces-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-wikispaces-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-wikispaces-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-wikispaces-tutorial/tutorial_general_203.png

