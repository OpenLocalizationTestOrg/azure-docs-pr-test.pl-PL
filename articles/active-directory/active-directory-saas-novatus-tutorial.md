---
title: 'Samouczek: Integracji Azure Active Directory z Novatus | Dokumentacja firmy Microsoft'
description: "Dowiedz się, jak tooconfigure logowanie jednokrotne między usługą Azure Active Directory i Novatus."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: d2f13779-bdb7-4408-9738-be67ed3de4e5
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/02/2017
ms.author: jeedes
ms.openlocfilehash: 7ff13f56f0f47d0c2667c9ca555801a7a06a2fa7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-novatus"></a><span data-ttu-id="ca414-103">Samouczek: Integracji Azure Active Directory z Novatus</span><span class="sxs-lookup"><span data-stu-id="ca414-103">Tutorial: Azure Active Directory integration with Novatus</span></span>

<span data-ttu-id="ca414-104">Z tego samouczka, dowiesz się, jak toointegrate Novatus w usłudze Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="ca414-104">In this tutorial, you learn how toointegrate Novatus with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="ca414-105">Integracja z usługą Azure AD Novatus zapewnia hello następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="ca414-105">Integrating Novatus with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="ca414-106">Można kontrolować w usłudze Azure AD, kto ma dostęp do tooNovatus</span><span class="sxs-lookup"><span data-stu-id="ca414-106">You can control in Azure AD who has access tooNovatus</span></span>
- <span data-ttu-id="ca414-107">Można włączyć użytkownika użytkownicy tooautomatically get zalogowane tooNovatus (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="ca414-107">You can enable your users tooautomatically get signed-on tooNovatus (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="ca414-108">Możesz zarządzać kont w jednej centralnej lokalizacji - hello portalu Azure</span><span class="sxs-lookup"><span data-stu-id="ca414-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="ca414-109">Jeśli chcesz tooknow więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="ca414-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ca414-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="ca414-110">Prerequisites</span></span>

<span data-ttu-id="ca414-111">tooconfigure integracji z usługą Azure AD z Novatus należy hello następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="ca414-111">tooconfigure Azure AD integration with Novatus, you need hello following items:</span></span>

- <span data-ttu-id="ca414-112">Subskrypcję usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="ca414-112">An Azure AD subscription</span></span>
- <span data-ttu-id="ca414-113">Novatus logowanie jednokrotne włączone subskrypcji</span><span class="sxs-lookup"><span data-stu-id="ca414-113">A Novatus single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="ca414-114">tootest hello kroków w tym samouczku, zaleca się przy użyciu środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="ca414-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="ca414-115">tootest hello kroki opisane w tym samouczku, należy stosować te zalecenia:</span><span class="sxs-lookup"><span data-stu-id="ca414-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="ca414-116">Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="ca414-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="ca414-117">Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz pobrać miesięczna wersja próbna [tutaj](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="ca414-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="ca414-118">Opis scenariusza</span><span class="sxs-lookup"><span data-stu-id="ca414-118">Scenario description</span></span>
<span data-ttu-id="ca414-119">W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym.</span><span class="sxs-lookup"><span data-stu-id="ca414-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="ca414-120">Scenariusz Hello opisane w tym samouczku składa się z dwóch głównych elementów:</span><span class="sxs-lookup"><span data-stu-id="ca414-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="ca414-121">Dodawanie Novatus z galerii hello</span><span class="sxs-lookup"><span data-stu-id="ca414-121">Adding Novatus from hello gallery</span></span>
2. <span data-ttu-id="ca414-122">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="ca414-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-novatus-from-hello-gallery"></a><span data-ttu-id="ca414-123">Dodawanie Novatus z galerii hello</span><span class="sxs-lookup"><span data-stu-id="ca414-123">Adding Novatus from hello gallery</span></span>
<span data-ttu-id="ca414-124">tooconfigure hello integracji Novatus do usługi Azure AD, należy tooadd Novatus z hello galerii tooyour listę zarządzanych aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="ca414-124">tooconfigure hello integration of Novatus into Azure AD, you need tooadd Novatus from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="ca414-125">**tooadd Novatus z galerii hello, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="ca414-125">**tooadd Novatus from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="ca414-126">W hello  **[portalu Azure](https://portal.azure.com)**na temat hello panelu nawigacji po lewej stronie, kliknij przycisk **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="ca414-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Usługa Active Directory][1]

2. <span data-ttu-id="ca414-128">Przejdź za**aplikacje dla przedsiębiorstw**.</span><span class="sxs-lookup"><span data-stu-id="ca414-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="ca414-129">Następnie przejdź zbyt**wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="ca414-129">Then go too**All applications**.</span></span>

    ![Aplikacje][2]
    
3. <span data-ttu-id="ca414-131">tooadd nową aplikację, kliknij przycisk **nowej aplikacji** przycisk u góry hello okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="ca414-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplikacje][3]

4. <span data-ttu-id="ca414-133">W polu wyszukiwania hello wpisz **Novatus**.</span><span class="sxs-lookup"><span data-stu-id="ca414-133">In hello search box, type **Novatus**.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-novatus-tutorial/tutorial_novatus_search.png)

5. <span data-ttu-id="ca414-135">W panelu wyników hello zaznacz **Novatus**, a następnie kliknij przycisk **Dodaj** przycisk aplikacji hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="ca414-135">In hello results panel, select **Novatus**, and then click **Add** button tooadd hello application.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-novatus-tutorial/tutorial_novatus_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="ca414-137">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="ca414-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="ca414-138">W tej sekcji skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z Novatus w oparciu o nazwie "Britta Simona" użytkownika testowego.</span><span class="sxs-lookup"><span data-stu-id="ca414-138">In this section, you configure and test Azure AD single sign-on with Novatus based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="ca414-139">Dla pojedynczego logowania jednokrotnego toowork usługi Azure AD musi tooknow użytkownika odpowiednikiem hello w Novatus jest tooa użytkownika w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="ca414-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Novatus is tooa user in Azure AD.</span></span> <span data-ttu-id="ca414-140">Innymi słowy relację łącza między użytkownika usługi Azure AD i hello użytkownikowi w Novatus musi toobe ustanowione.</span><span class="sxs-lookup"><span data-stu-id="ca414-140">In other words, a link relationship between an Azure AD user and hello related user in Novatus needs toobe established.</span></span>

<span data-ttu-id="ca414-141">W Novatus, należy przypisać wartość hello hello **nazwy użytkownika** w usłudze Azure AD jako wartość hello hello **Username** tooestablish hello łącze relacji.</span><span class="sxs-lookup"><span data-stu-id="ca414-141">In Novatus, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="ca414-142">tooconfigure i testowych usługi Azure AD rejestracji jednokrotnej z Novatus, należy po bloków konstrukcyjnych hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="ca414-142">tooconfigure and test Azure AD single sign-on with Novatus, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="ca414-143">**[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configuring-azure-ad-single-sign-on)**  -tooenable Twojego toouse użytkowników tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="ca414-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="ca414-144">**[Tworzenie użytkownika testowego usługi Azure AD](#creating-an-azure-ad-test-user)**  -tootest usługi Azure AD rejestracji jednokrotnej z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="ca414-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="ca414-145">**[Tworzenie użytkownika testowego Novatus](#creating-a-novatus-test-user)**  -toohave odpowiednikiem Simona Britta w Novatus, który jest połączony toohello usługi Azure AD reprezentację użytkownika.</span><span class="sxs-lookup"><span data-stu-id="ca414-145">**[Creating a Novatus test user](#creating-a-novatus-test-user)** - toohave a counterpart of Britta Simon in Novatus that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="ca414-146">**[Przypisanie użytkownika testowego hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Simona Britta toouse usługi Azure AD rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="ca414-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="ca414-147">**[Testowanie rejestracji jednokrotnej](#testing-single-sign-on)**  -tooverify czy hello konfiguracji działania.</span><span class="sxs-lookup"><span data-stu-id="ca414-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="ca414-148">Konfigurowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="ca414-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="ca414-149">W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w portalu Azure hello i skonfigurować logowanie jednokrotne w aplikacji Novatus.</span><span class="sxs-lookup"><span data-stu-id="ca414-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Novatus application.</span></span>

<span data-ttu-id="ca414-150">**tooconfigure usługi Azure AD rejestracji jednokrotnej z Novatus, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="ca414-150">**tooconfigure Azure AD single sign-on with Novatus, perform hello following steps:**</span></span>

1. <span data-ttu-id="ca414-151">W portalu Azure na powitania hello **Novatus** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.</span><span class="sxs-lookup"><span data-stu-id="ca414-151">In hello Azure portal, on hello **Novatus** application integration page, click **Single sign-on**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej][4]

2. <span data-ttu-id="ca414-153">Na powitania **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** tooenable rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="ca414-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-novatus-tutorial/tutorial_novatus_samlbase.png)

3. <span data-ttu-id="ca414-155">Na powitania **Novatus domeny i adres URL** sekcji, wykonaj następujące kroki hello:</span><span class="sxs-lookup"><span data-stu-id="ca414-155">On hello **Novatus Domain and URLs** section, perform hello following steps:</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-novatus-tutorial/tutorial_novatus_url.png)

     <span data-ttu-id="ca414-157">W hello **adres URL logowania** tekstowym, wpisz adres URL za pomocą hello następującego wzorca:`https://sso.novatuscontracts.com/<companyname>`</span><span class="sxs-lookup"><span data-stu-id="ca414-157">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://sso.novatuscontracts.com/<companyname>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="ca414-158">Ta wartość nie jest prawdziwe.</span><span class="sxs-lookup"><span data-stu-id="ca414-158">This value is not real.</span></span> <span data-ttu-id="ca414-159">Zaktualizuj tę wartość z hello rzeczywisty adres URL logowania.</span><span class="sxs-lookup"><span data-stu-id="ca414-159">Update this value with hello actual Sign-On URL.</span></span> <span data-ttu-id="ca414-160">Skontaktuj się z [zespołem pomocy technicznej klienta Novatus](mailto:jvinci@novatusinc.com) tooget tej wartości.</span><span class="sxs-lookup"><span data-stu-id="ca414-160">Contact [Novatus Client support team](mailto:jvinci@novatusinc.com) tooget this value.</span></span> 
 


4. <span data-ttu-id="ca414-161">Na powitania **certyfikat podpisywania SAML** kliknij **Certificate(Base64)** , a następnie zapisz plik certyfikatu hello na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="ca414-161">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-novatus-tutorial/tutorial_novatus_certificate.png) 

5. <span data-ttu-id="ca414-163">Kliknij przycisk **zapisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="ca414-163">Click **Save** button.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-novatus-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="ca414-165">Na powitania **konfiguracji Novatus** kliknij **skonfigurować Novatus** tooopen **Konfigurowanie logowania jednokrotnego** okna.</span><span class="sxs-lookup"><span data-stu-id="ca414-165">On hello **Novatus Configuration** section, click **Configure Novatus** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="ca414-166">Kopiuj hello **Sign-Out adres URL, identyfikator jednostki SAML i SAML pojedynczy znak na adres URL usługi** z hello **sekcji krótkimi opisami.**</span><span class="sxs-lookup"><span data-stu-id="ca414-166">Copy hello **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-novatus-tutorial/tutorial_novatus_configure.png) 

7. <span data-ttu-id="ca414-168">tooget logowania jednokrotnego skonfigurowane dla aplikacji, skontaktuj się z [Novatus obsługuje zespołu](mailto:jvinci@novatusinc.com).</span><span class="sxs-lookup"><span data-stu-id="ca414-168">tooget SSO configured for your application, contact your [Novatus support team](mailto:jvinci@novatusinc.com).</span></span> <span data-ttu-id="ca414-169">Dołącz hello **pobrany certyfikat** hello poczty i udziału tooyour pliku **adresy URL metadanych** (**Sign-Out adres URL, identyfikator jednostki SAML i SAML pojedynczy znak na adres URL usługi**) z Novatus zespołu tooset się rejestracji Jednokrotnej w bok.</span><span class="sxs-lookup"><span data-stu-id="ca414-169">Attach hello **downloaded certificate** file tooyour mail and share hello **metadata urls** (**Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL**) with Novatus team tooset up SSO on their side.</span></span>

> [!TIP]
> <span data-ttu-id="ca414-170">Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz hello [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji hello!</span><span class="sxs-lookup"><span data-stu-id="ca414-170">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="ca414-171">Po dodaniu tej aplikacji z hello **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij hello **rejestracji jednokrotnej** hello kartę i dostępu do osadzonych dokumentacji za pośrednictwem hello  **Konfiguracja** sekcji u dołu hello.</span><span class="sxs-lookup"><span data-stu-id="ca414-171">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="ca414-172">Więcej o hello osadzonych dokumentacji funkcji w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="ca414-172">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="ca414-173">Tworzenie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="ca414-173">Creating an Azure AD test user</span></span>
<span data-ttu-id="ca414-174">Celem Hello w tej sekcji jest toocreate użytkownika testowego, w portalu Azure o nazwie Simona Britta hello.</span><span class="sxs-lookup"><span data-stu-id="ca414-174">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Tworzenie użytkowników usługi Azure AD][100]

<span data-ttu-id="ca414-176">**toocreate użytkownika testowego w usłudze Azure AD, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="ca414-176">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="ca414-177">W hello **portalu Azure**na temat hello w lewym okienku nawigacji, kliknij przycisk **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="ca414-177">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-novatus-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="ca414-179">toodisplay hello listę użytkowników, przejdź zbyt**użytkowników i grup** i kliknij przycisk **wszyscy użytkownicy**.</span><span class="sxs-lookup"><span data-stu-id="ca414-179">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-novatus-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="ca414-181">Witaj tooopen **użytkownika** okna dialogowego, kliknij przycisk **Dodaj** u góry hello hello okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="ca414-181">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-novatus-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="ca414-183">Na powitania **użytkownika** okna dialogowego wykonaj hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="ca414-183">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-novatus-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="ca414-185">a.</span><span class="sxs-lookup"><span data-stu-id="ca414-185">a.</span></span> <span data-ttu-id="ca414-186">W hello **nazwa** pole tekstowe, typ **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="ca414-186">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="ca414-187">b.</span><span class="sxs-lookup"><span data-stu-id="ca414-187">b.</span></span> <span data-ttu-id="ca414-188">W hello **nazwy użytkownika** pole tekstowe, hello typu **adres e-mail** z BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="ca414-188">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="ca414-189">c.</span><span class="sxs-lookup"><span data-stu-id="ca414-189">c.</span></span> <span data-ttu-id="ca414-190">Wybierz **Pokaż hasło** i zanotuj wartość hello hello **hasło**.</span><span class="sxs-lookup"><span data-stu-id="ca414-190">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="ca414-191">d.</span><span class="sxs-lookup"><span data-stu-id="ca414-191">d.</span></span> <span data-ttu-id="ca414-192">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="ca414-192">Click **Create**.</span></span>
 
### <a name="creating-a-novatus-test-user"></a><span data-ttu-id="ca414-193">Tworzenie użytkownika testowego Novatus</span><span class="sxs-lookup"><span data-stu-id="ca414-193">Creating a Novatus test user</span></span>

<span data-ttu-id="ca414-194">Celem Hello w tej sekcji jest toocreate użytkownika o nazwie Simona Britta w Novatus.</span><span class="sxs-lookup"><span data-stu-id="ca414-194">hello objective of this section is toocreate a user called Britta Simon in Novatus.</span></span> <span data-ttu-id="ca414-195">Novatus obsługę w czasie, który jest domyślnie włączone.</span><span class="sxs-lookup"><span data-stu-id="ca414-195">Novatus supports just-in-time provisioning, which is by default enabled.</span></span>

<span data-ttu-id="ca414-196">Nie ma elementu akcji można w tej sekcji.</span><span class="sxs-lookup"><span data-stu-id="ca414-196">There is no action item for you in this section.</span></span> <span data-ttu-id="ca414-197">Nowy użytkownik zostanie utworzony podczas próby tooaccess Novatus, jeśli go jeszcze nie istnieje.</span><span class="sxs-lookup"><span data-stu-id="ca414-197">A new user will be created during an attempt tooaccess Novatus if it doesn't exist yet.</span></span>

>[!NOTE]
><span data-ttu-id="ca414-198">Jeśli potrzebujesz ręcznie toocreate użytkownika, należy toocontact hello [Novatus obsługuje zespołu](mailto:jvinci@novatusinc.com).</span><span class="sxs-lookup"><span data-stu-id="ca414-198">If you need toocreate an user manually, you need toocontact hello [Novatus support team](mailto:jvinci@novatusinc.com).</span></span> 
> 

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="ca414-199">Przypisanie użytkownika testowego hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="ca414-199">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="ca414-200">W tej sekcji możesz włączyć toouse Simona Britta Azure logowania jednokrotnego za udzielanie dostępu tooNovatus.</span><span class="sxs-lookup"><span data-stu-id="ca414-200">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooNovatus.</span></span>

![Przypisz użytkownika][200] 

<span data-ttu-id="ca414-202">**tooassign tooNovatus Simona Britta wykonaj hello następujące kroki:**</span><span class="sxs-lookup"><span data-stu-id="ca414-202">**tooassign Britta Simon tooNovatus, perform hello following steps:**</span></span>

1. <span data-ttu-id="ca414-203">W portalu Azure hello, otwórz widok aplikacji hello, a następnie przejdź do widoku katalogu toohello i przejść za**aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="ca414-203">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Przypisz użytkownika][201] 

2. <span data-ttu-id="ca414-205">Z listy aplikacji hello wybierz **Novatus**.</span><span class="sxs-lookup"><span data-stu-id="ca414-205">In hello applications list, select **Novatus**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-novatus-tutorial/tutorial_novatus_app.png) 

3. <span data-ttu-id="ca414-207">W menu powitania po lewej stronie powitania kliknij **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="ca414-207">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Przypisz użytkownika][202] 

4. <span data-ttu-id="ca414-209">Kliknij przycisk **Dodaj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="ca414-209">Click **Add** button.</span></span> <span data-ttu-id="ca414-210">Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="ca414-210">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Przypisz użytkownika][203]

5. <span data-ttu-id="ca414-212">Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** hello listy użytkowników.</span><span class="sxs-lookup"><span data-stu-id="ca414-212">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="ca414-213">Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="ca414-213">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="ca414-214">Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="ca414-214">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="ca414-215">Testowanie rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="ca414-215">Testing single sign-on</span></span>

<span data-ttu-id="ca414-216">Celem Hello w tej sekcji jest tootest użyciu usługi Azure AD konfiguracji rejestracji jednokrotnej hello panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="ca414-216">hello objective of this section is tootest your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="ca414-217">Po kliknięciu powitalne Novatus kafelka w hello Panel dostępu, należy pobrać automatycznie zalogowane tooyour Novatus aplikacji.</span><span class="sxs-lookup"><span data-stu-id="ca414-217">When you click hello Novatus tile in hello Access Panel, you should get automatically signed-on tooyour Novatus application.</span></span> <span data-ttu-id="ca414-218">Aby uzyskać więcej informacji na temat hello Panel dostępu, zobacz [toohello wprowadzenie panelu dostępu](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="ca414-218">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="ca414-219">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="ca414-219">Additional resources</span></span>

* [<span data-ttu-id="ca414-220">Lista samouczków dotyczących tooIntegrate aplikacji SaaS w usłudze Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="ca414-220">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="ca414-221">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="ca414-221">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-novatus-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-novatus-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-novatus-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-novatus-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-novatus-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-novatus-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-novatus-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-novatus-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-novatus-tutorial/tutorial_general_203.png

