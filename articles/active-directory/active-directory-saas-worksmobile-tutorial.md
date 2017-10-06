---
title: "Samouczek: Integracji usługi Azure Active Directory z WORKS MOBILE | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak tooconfigure logowanie jednokrotne między usługi Azure Active Directory i działa MOBILE."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 725f32fd-d0ad-49c7-b137-1cc246bf85d7
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/22/2017
ms.author: jeedes
ms.openlocfilehash: 80192218a2e99a921834bb53e708d5e4fab413f4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-works-mobile"></a><span data-ttu-id="b4fc3-103">Samouczek: Integracji Azure Active Directory z MOBILE działania</span><span class="sxs-lookup"><span data-stu-id="b4fc3-103">Tutorial: Azure Active Directory integration with WORKS MOBILE</span></span>

<span data-ttu-id="b4fc3-104">Z tego samouczka, dowiesz się, jak działa toointegrate MOBILE w usłudze Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="b4fc3-104">In this tutorial, you learn how toointegrate WORKS MOBILE with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="b4fc3-105">Integrowanie MOBILE WSPÓŁPRACUJE z usługą Azure AD zapewnia hello następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="b4fc3-105">Integrating WORKS MOBILE with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="b4fc3-106">Można kontrolować w usłudze Azure AD, kto ma dostęp do tooWORKS MOBILE</span><span class="sxs-lookup"><span data-stu-id="b4fc3-106">You can control in Azure AD who has access tooWORKS MOBILE</span></span>
- <span data-ttu-id="b4fc3-107">Można włączyć użytkownika użytkownicy tooautomatically get zalogowane tooWORKS MOBILE (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="b4fc3-107">You can enable your users tooautomatically get signed-on tooWORKS MOBILE (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="b4fc3-108">Możesz zarządzać kont w jednej centralnej lokalizacji - hello portalu Azure</span><span class="sxs-lookup"><span data-stu-id="b4fc3-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="b4fc3-109">Jeśli chcesz tooknow więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="b4fc3-109">If you want tooknow more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b4fc3-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="b4fc3-110">Prerequisites</span></span>

<span data-ttu-id="b4fc3-111">tooconfigure integracji usługi Azure AD z MOBILE WSPÓŁPRACUJE należy hello następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="b4fc3-111">tooconfigure Azure AD integration with WORKS MOBILE, you need hello following items:</span></span>

- <span data-ttu-id="b4fc3-112">Subskrypcję usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="b4fc3-112">An Azure AD subscription</span></span>
- <span data-ttu-id="b4fc3-113">MOBILE działa logowanie jednokrotne włączone subskrypcji</span><span class="sxs-lookup"><span data-stu-id="b4fc3-113">A WORKS MOBILE single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="b4fc3-114">tootest hello kroków w tym samouczku, zaleca się przy użyciu środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="b4fc3-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="b4fc3-115">tootest hello kroki opisane w tym samouczku, należy stosować te zalecenia:</span><span class="sxs-lookup"><span data-stu-id="b4fc3-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="b4fc3-116">Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="b4fc3-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="b4fc3-117">Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz pobrać miesięczna wersja próbna [tutaj](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="b4fc3-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="b4fc3-118">Opis scenariusza</span><span class="sxs-lookup"><span data-stu-id="b4fc3-118">Scenario description</span></span>
<span data-ttu-id="b4fc3-119">W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym.</span><span class="sxs-lookup"><span data-stu-id="b4fc3-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="b4fc3-120">Scenariusz Hello opisane w tym samouczku składa się z dwóch głównych elementów:</span><span class="sxs-lookup"><span data-stu-id="b4fc3-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="b4fc3-121">Dodawanie MOBILE WSPÓŁPRACUJE z galerii hello</span><span class="sxs-lookup"><span data-stu-id="b4fc3-121">Adding WORKS MOBILE from hello gallery</span></span>
2. <span data-ttu-id="b4fc3-122">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="b4fc3-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-works-mobile-from-hello-gallery"></a><span data-ttu-id="b4fc3-123">Dodawanie MOBILE WSPÓŁPRACUJE z galerii hello</span><span class="sxs-lookup"><span data-stu-id="b4fc3-123">Adding WORKS MOBILE from hello gallery</span></span>
<span data-ttu-id="b4fc3-124">tooconfigure hello integracji MOBILE WSPÓŁPRACUJE z usługą Azure AD, należy tooadd MOBILE WSPÓŁPRACUJE z hello galerii tooyour listę zarządzanych aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="b4fc3-124">tooconfigure hello integration of WORKS MOBILE into Azure AD, you need tooadd WORKS MOBILE from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="b4fc3-125">**tooadd MOBILE WSPÓŁPRACUJE z galerii hello, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="b4fc3-125">**tooadd WORKS MOBILE from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="b4fc3-126">W hello  **[portalu Azure](https://portal.azure.com)**na temat hello panelu nawigacji po lewej stronie, kliknij przycisk **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="b4fc3-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Usługa Active Directory][1]

2. <span data-ttu-id="b4fc3-128">Przejdź za**aplikacje dla przedsiębiorstw**.</span><span class="sxs-lookup"><span data-stu-id="b4fc3-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="b4fc3-129">Następnie przejdź zbyt**wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="b4fc3-129">Then go too**All applications**.</span></span>

    ![Aplikacje][2]
    
3. <span data-ttu-id="b4fc3-131">tooadd nową aplikację, kliknij przycisk **nowej aplikacji** przycisk u góry hello okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="b4fc3-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplikacje][3]

4. <span data-ttu-id="b4fc3-133">W polu wyszukiwania hello wpisz **MOBILE WSPÓŁPRACUJE**.</span><span class="sxs-lookup"><span data-stu-id="b4fc3-133">In hello search box, type **WORKS MOBILE**.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-worksmobile-tutorial/tutorial_worksmobile_search.png)

5. <span data-ttu-id="b4fc3-135">W panelu wyników hello, wybierz **MOBILE WSPÓŁPRACUJE**, a następnie kliknij przycisk **Dodaj** przycisk tooadd hello aplikacji.</span><span class="sxs-lookup"><span data-stu-id="b4fc3-135">In hello results panel, select **WORKS MOBILE**, and then click **Add** button tooadd hello application.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-worksmobile-tutorial/tutorial_worksmobile_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="b4fc3-137">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="b4fc3-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="b4fc3-138">W tej sekcji możesz skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z MOBILE działa na podstawie użytkownika testowego, nazywany "Britta Simona".</span><span class="sxs-lookup"><span data-stu-id="b4fc3-138">In this section, you configure and test Azure AD single sign-on with WORKS MOBILE based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="b4fc3-139">Dla pojedynczego logowania jednokrotnego toowork usługi Azure AD musi tooknow użytkownika odpowiednikiem hello w MOBILE WSPÓŁPRACUJE jest tooa użytkownika w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="b4fc3-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in WORKS MOBILE is tooa user in Azure AD.</span></span> <span data-ttu-id="b4fc3-140">Innymi słowy relację łącza między użytkownika usługi Azure AD i hello użytkownikowi w MOBILE WSPÓŁPRACUJE musi toobe ustanowione.</span><span class="sxs-lookup"><span data-stu-id="b4fc3-140">In other words, a link relationship between an Azure AD user and hello related user in WORKS MOBILE needs toobe established.</span></span>

<span data-ttu-id="b4fc3-141">Ta relacja łącza zostanie nawiązane, przypisując wartość hello hello **nazwy użytkownika** w usłudze Azure AD jako wartość hello hello **Username** w MOBILE WSPÓŁPRACUJE.</span><span class="sxs-lookup"><span data-stu-id="b4fc3-141">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in WORKS MOBILE.</span></span>

<span data-ttu-id="b4fc3-142">tooconfigure i testowych usługi Azure AD rejestracji jednokrotnej z MOBILE działa, należy po bloków konstrukcyjnych hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="b4fc3-142">tooconfigure and test Azure AD single sign-on with WORKS MOBILE, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="b4fc3-143">**[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configuring-azure-ad-single-sign-on)**  -tooenable Twojego toouse użytkowników tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="b4fc3-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="b4fc3-144">**[Tworzenie użytkownika testowego usługi Azure AD](#creating-an-azure-ad-test-user)**  -tootest usługi Azure AD rejestracji jednokrotnej z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="b4fc3-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="b4fc3-145">**[Tworzenie użytkownika testowego MOBILE WSPÓŁPRACUJE](#creating-a-works-mobile-test-user)**  -toohave odpowiednikiem Simona Britta w MOBILE działania, który jest połączony toohello usługi Azure AD reprezentację użytkownika.</span><span class="sxs-lookup"><span data-stu-id="b4fc3-145">**[Creating a WORKS MOBILE test user](#creating-a-works-mobile-test-user)** - toohave a counterpart of Britta Simon in WORKS MOBILE that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="b4fc3-146">**[Przypisanie użytkownika testowego hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Simona Britta toouse usługi Azure AD rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="b4fc3-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="b4fc3-147">**[Testowanie rejestracji jednokrotnej](#testing-single-sign-on)**  -tooverify czy hello konfiguracji działania.</span><span class="sxs-lookup"><span data-stu-id="b4fc3-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="b4fc3-148">Konfigurowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="b4fc3-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="b4fc3-149">W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w hello portalu Azure i skonfigurować rejestracji jednokrotnej w aplikacji MOBILNEJ działa.</span><span class="sxs-lookup"><span data-stu-id="b4fc3-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your WORKS MOBILE application.</span></span>

<span data-ttu-id="b4fc3-150">**tooconfigure usługi Azure AD rejestracji jednokrotnej z urządzeń przenośnych działa, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="b4fc3-150">**tooconfigure Azure AD single sign-on with WORKS MOBILE, perform hello following steps:**</span></span>

1. <span data-ttu-id="b4fc3-151">W portalu Azure na powitania hello **MOBILE WSPÓŁPRACUJE** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.</span><span class="sxs-lookup"><span data-stu-id="b4fc3-151">In hello Azure portal, on hello **WORKS MOBILE** application integration page, click **Single sign-on**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej][4]

2. <span data-ttu-id="b4fc3-153">Na powitania **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** tooenable rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="b4fc3-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-worksmobile-tutorial/tutorial_worksmobile_samlbase.png)

3. <span data-ttu-id="b4fc3-155">Na powitania **WORKS MOBILE domeny i adres URL** sekcji, wykonaj następujące kroki hello:</span><span class="sxs-lookup"><span data-stu-id="b4fc3-155">On hello **WORKS MOBILE Domain and URLs** section, perform hello following steps:</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-worksmobile-tutorial/tutorial_worksmobile_url.png)

    <span data-ttu-id="b4fc3-157">a.</span><span class="sxs-lookup"><span data-stu-id="b4fc3-157">a.</span></span> <span data-ttu-id="b4fc3-158">W hello **adres URL logowania** tekstowym, wpisz adres URL za pomocą hello następującego wzorca:`https://<subdomain>.worksmobile.com/jp/myservice`</span><span class="sxs-lookup"><span data-stu-id="b4fc3-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<subdomain>.worksmobile.com/jp/myservice`</span></span>

    <span data-ttu-id="b4fc3-159">b.</span><span class="sxs-lookup"><span data-stu-id="b4fc3-159">b.</span></span> <span data-ttu-id="b4fc3-160">W hello **identyfikator** pole tekstowe, wartość hello typu jako`worksmobile.com`</span><span class="sxs-lookup"><span data-stu-id="b4fc3-160">In hello **Identifier** textbox, type hello value as `worksmobile.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="b4fc3-161">Ta wartość nie jest prawdziwe.</span><span class="sxs-lookup"><span data-stu-id="b4fc3-161">This value is not real.</span></span> <span data-ttu-id="b4fc3-162">Zaktualizuj tę wartość z hello rzeczywisty adres URL logowania.</span><span class="sxs-lookup"><span data-stu-id="b4fc3-162">Update this value with hello actual Sign-On URL.</span></span> <span data-ttu-id="b4fc3-163">Skontaktuj się z [klienta MOBILE WSPÓŁPRACUJE z pomocą techniczną](mailto:dl_ssoinfo@worksmobile.com) tooget tej wartości.</span><span class="sxs-lookup"><span data-stu-id="b4fc3-163">Contact [WORKS MOBILE Client support team](mailto:dl_ssoinfo@worksmobile.com) tooget this value.</span></span> 
 
4. <span data-ttu-id="b4fc3-164">Na powitania **certyfikat podpisywania SAML** kliknij **Certificate(Raw)** , a następnie zapisz plik certyfikatu hello na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="b4fc3-164">On hello **SAML Signing Certificate** section, click **Certificate(Raw)** and then save hello certificate file on your computer.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-worksmobile-tutorial/tutorial_worksmobile_certificate.png) 

5. <span data-ttu-id="b4fc3-166">Kliknij przycisk **zapisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="b4fc3-166">Click **Save** button.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-worksmobile-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="b4fc3-168">Na powitania **konfiguracji MOBILE WSPÓŁPRACUJE** kliknij **skonfigurować MOBILE WSPÓŁPRACUJE** tooopen **Konfigurowanie logowania jednokrotnego** okna.</span><span class="sxs-lookup"><span data-stu-id="b4fc3-168">On hello **WORKS MOBILE Configuration** section, click **Configure WORKS MOBILE** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="b4fc3-169">Kopiuj hello **Sign-Out adres URL, identyfikator jednostki SAML i SAML pojedynczy znak na adres URL usługi** z hello **sekcji krótkimi opisami.**</span><span class="sxs-lookup"><span data-stu-id="b4fc3-169">Copy hello **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-worksmobile-tutorial/tutorial_worksmobile_configure.png) 

7. <span data-ttu-id="b4fc3-171">tooget logowania jednokrotnego skonfigurowane dla aplikacji, skontaktuj się z [MOBILE WSPÓŁPRACUJE z pomocą techniczną](mailto:dl_ssoinfo@worksmobile.com) i dostarczać hello następujących informacji:</span><span class="sxs-lookup"><span data-stu-id="b4fc3-171">tooget SSO configured for your application, contact [WORKS MOBILE support team](mailto:dl_ssoinfo@worksmobile.com) and provide them with hello following information:</span></span> 

    <span data-ttu-id="b4fc3-172">• hello pobrane **plik certyfikatu**</span><span class="sxs-lookup"><span data-stu-id="b4fc3-172">• hello downloaded **Certificate file**</span></span>

    <span data-ttu-id="b4fc3-173">• hello **SAML pojedynczy znak na adres URL usługi**</span><span class="sxs-lookup"><span data-stu-id="b4fc3-173">• hello **SAML Single Sign-On Service URL**</span></span>

    <span data-ttu-id="b4fc3-174">• hello **identyfikator jednostki SAML**</span><span class="sxs-lookup"><span data-stu-id="b4fc3-174">• hello **SAML Entity ID**</span></span>

    <span data-ttu-id="b4fc3-175">• hello **Sign-Out adresu URL**</span><span class="sxs-lookup"><span data-stu-id="b4fc3-175">• hello **Sign-Out URL**</span></span>

> [!TIP]
> <span data-ttu-id="b4fc3-176">Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz hello [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji hello!</span><span class="sxs-lookup"><span data-stu-id="b4fc3-176">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="b4fc3-177">Po dodaniu tej aplikacji z hello **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij hello **rejestracji jednokrotnej** hello kartę i dostępu do osadzonych dokumentacji za pośrednictwem hello  **Konfiguracja** sekcji u dołu hello.</span><span class="sxs-lookup"><span data-stu-id="b4fc3-177">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="b4fc3-178">Więcej o hello osadzonych dokumentacji funkcji w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="b4fc3-178">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="b4fc3-179">Tworzenie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="b4fc3-179">Creating an Azure AD test user</span></span>
<span data-ttu-id="b4fc3-180">Celem Hello w tej sekcji jest toocreate użytkownika testowego, w portalu Azure o nazwie Simona Britta hello.</span><span class="sxs-lookup"><span data-stu-id="b4fc3-180">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Tworzenie użytkowników usługi Azure AD][100]

<span data-ttu-id="b4fc3-182">**toocreate użytkownika testowego w usłudze Azure AD, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="b4fc3-182">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="b4fc3-183">W hello **portalu Azure**na temat hello w lewym okienku nawigacji, kliknij przycisk **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="b4fc3-183">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-worksmobile-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="b4fc3-185">toodisplay hello listę użytkowników, przejdź zbyt**użytkowników i grup** i kliknij przycisk **wszyscy użytkownicy**.</span><span class="sxs-lookup"><span data-stu-id="b4fc3-185">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-worksmobile-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="b4fc3-187">Witaj tooopen **użytkownika** okna dialogowego, kliknij przycisk **Dodaj** u góry hello hello okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="b4fc3-187">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-worksmobile-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="b4fc3-189">Na powitania **użytkownika** okna dialogowego wykonaj hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="b4fc3-189">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-worksmobile-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="b4fc3-191">a.</span><span class="sxs-lookup"><span data-stu-id="b4fc3-191">a.</span></span> <span data-ttu-id="b4fc3-192">W hello **nazwa** pole tekstowe, typ **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="b4fc3-192">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="b4fc3-193">b.</span><span class="sxs-lookup"><span data-stu-id="b4fc3-193">b.</span></span> <span data-ttu-id="b4fc3-194">W hello **nazwy użytkownika** pole tekstowe, hello typu **adres e-mail** z BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="b4fc3-194">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="b4fc3-195">c.</span><span class="sxs-lookup"><span data-stu-id="b4fc3-195">c.</span></span> <span data-ttu-id="b4fc3-196">Wybierz **Pokaż hasło** i zanotuj wartość hello hello **hasło**.</span><span class="sxs-lookup"><span data-stu-id="b4fc3-196">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="b4fc3-197">d.</span><span class="sxs-lookup"><span data-stu-id="b4fc3-197">d.</span></span> <span data-ttu-id="b4fc3-198">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="b4fc3-198">Click **Create**.</span></span>
 
### <a name="creating-a-works-mobile-test-user"></a><span data-ttu-id="b4fc3-199">Tworzenie użytkownika testowego MOBILE działania</span><span class="sxs-lookup"><span data-stu-id="b4fc3-199">Creating a WORKS MOBILE test user</span></span>

 <span data-ttu-id="b4fc3-200">W tej sekcji należy utworzyć użytkownika o nazwie Simona Britta w przenośnych działa.</span><span class="sxs-lookup"><span data-stu-id="b4fc3-200">In this section, you create a user called Britta Simon in WORKS MOBILE.</span></span> <span data-ttu-id="b4fc3-201">We współpracy z [MOBILE WSPÓŁPRACUJE z pomocą techniczną](mailto:dl_ssoinfo@worksmobile.com) tooadd hello użytkowników platformy MOBILE WSPÓŁPRACUJE hello.</span><span class="sxs-lookup"><span data-stu-id="b4fc3-201">Please work with [WORKS MOBILE support team](mailto:dl_ssoinfo@worksmobile.com) tooadd hello users in hello WORKS MOBILE platform.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="b4fc3-202">Przypisanie użytkownika testowego hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="b4fc3-202">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="b4fc3-203">W tej sekcji możesz włączyć toouse Simona Britta Azure logowania jednokrotnego za udzielanie dostępu tooWORKS MOBILE.</span><span class="sxs-lookup"><span data-stu-id="b4fc3-203">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooWORKS MOBILE.</span></span>

![Przypisz użytkownika][200] 

<span data-ttu-id="b4fc3-205">**tooassign tooWORKS Simona Britta urządzeń przenośnych, należy wykonać hello następujące kroki:**</span><span class="sxs-lookup"><span data-stu-id="b4fc3-205">**tooassign Britta Simon tooWORKS MOBILE, perform hello following steps:**</span></span>

1. <span data-ttu-id="b4fc3-206">W portalu Azure hello, otwórz widok aplikacji hello, a następnie przejdź do widoku katalogu toohello i przejść za**aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="b4fc3-206">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Przypisz użytkownika][201] 

2. <span data-ttu-id="b4fc3-208">Z listy aplikacji hello wybierz **MOBILE WSPÓŁPRACUJE**.</span><span class="sxs-lookup"><span data-stu-id="b4fc3-208">In hello applications list, select **WORKS MOBILE**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-worksmobile-tutorial/tutorial_worksmobile_app.png) 

3. <span data-ttu-id="b4fc3-210">W menu powitania po lewej stronie powitania kliknij **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="b4fc3-210">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Przypisz użytkownika][202] 

4. <span data-ttu-id="b4fc3-212">Kliknij przycisk **Dodaj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="b4fc3-212">Click **Add** button.</span></span> <span data-ttu-id="b4fc3-213">Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="b4fc3-213">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Przypisz użytkownika][203]

5. <span data-ttu-id="b4fc3-215">Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** hello listy użytkowników.</span><span class="sxs-lookup"><span data-stu-id="b4fc3-215">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="b4fc3-216">Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="b4fc3-216">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="b4fc3-217">Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="b4fc3-217">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="b4fc3-218">Testowanie rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="b4fc3-218">Testing single sign-on</span></span>

<span data-ttu-id="b4fc3-219">W tej sekcji można przetestować konfigurację usługi Azure AD z logowania jednokrotnego za pomocą hello panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="b4fc3-219">In this section, you test your Azure AD SSO configuration using hello Access Panel.</span></span>

<span data-ttu-id="b4fc3-220">Po kliknięciu kafelka MOBILE WSPÓŁPRACUJE hello w hello Panel dostępu, należy pobrać automatycznie zalogowane tooyour MOBILE działania aplikacji.</span><span class="sxs-lookup"><span data-stu-id="b4fc3-220">When you click hello WORKS MOBILE tile in hello Access Panel, you should get automatically signed-on tooyour WORKS MOBILE application.</span></span>
<span data-ttu-id="b4fc3-221">Aby uzyskać więcej informacji na temat panelu dostępu, zobacz [toohello wprowadzenie panelu dostępu](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="b4fc3-221">For more information about the Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="b4fc3-222">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="b4fc3-222">Additional resources</span></span>

* [<span data-ttu-id="b4fc3-223">Lista samouczków dotyczących tooIntegrate aplikacji SaaS w usłudze Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="b4fc3-223">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="b4fc3-224">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="b4fc3-224">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-worksmobile-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-worksmobile-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-worksmobile-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-worksmobile-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-worksmobile-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-worksmobile-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-worksmobile-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-worksmobile-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-worksmobile-tutorial/tutorial_general_203.png

