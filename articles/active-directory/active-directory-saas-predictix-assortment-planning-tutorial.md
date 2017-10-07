---
title: "Samouczek: Integracji Azure Active Directory z planowaniem wybór Predictix | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak tooconfigure logowanie jednokrotne między usługą Azure Active Directory i planowania wybór Predictix."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 37e686ff-f8e5-40b1-9d7e-f64b076917b7
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/20/2017
ms.author: jeedes
ms.openlocfilehash: 1294b712caf12fdafaf65d70a02ee9fbdc3e84a8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-predictix-assortment-planning"></a><span data-ttu-id="12993-103">Samouczek: Integracji Azure Active Directory z planowaniem wybór Predictix</span><span class="sxs-lookup"><span data-stu-id="12993-103">Tutorial: Azure Active Directory integration with Predictix Assortment Planning</span></span>

<span data-ttu-id="12993-104">Z tego samouczka, dowiesz się, jak toointegrate Predictix wybór planowania w usłudze Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="12993-104">In this tutorial, you learn how toointegrate Predictix Assortment Planning with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="12993-105">Integrowanie planowania wybór Predictix z usługą Azure AD zapewnia hello następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="12993-105">Integrating Predictix Assortment Planning with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="12993-106">Można kontrolować w usłudze Azure AD, kto ma dostęp tooPredictix wybór planowania.</span><span class="sxs-lookup"><span data-stu-id="12993-106">You can control in Azure AD who has access tooPredictix Assortment Planning.</span></span>
- <span data-ttu-id="12993-107">Można włączyć użytkownika użytkownicy tooautomatically get zalogowane tooPredictix wybór planowania (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="12993-107">You can enable your users tooautomatically get signed-on tooPredictix Assortment Planning (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="12993-108">Możesz zarządzać kont w jednej centralnej lokalizacji - hello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="12993-108">You can manage your accounts in one central location - hello Azure portal.</span></span>

<span data-ttu-id="12993-109">Jeśli chcesz tooknow więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="12993-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="12993-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="12993-110">Prerequisites</span></span>

<span data-ttu-id="12993-111">tooconfigure integracji usługi Azure AD z planowaniem wybór Predictix należy hello następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="12993-111">tooconfigure Azure AD integration with Predictix Assortment Planning, you need hello following items:</span></span>

- <span data-ttu-id="12993-112">Subskrypcję usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="12993-112">An Azure AD subscription</span></span>
- <span data-ttu-id="12993-113">Planowanie wybór Predictix logowanie jednokrotne włączone subskrypcji</span><span class="sxs-lookup"><span data-stu-id="12993-113">A Predictix Assortment Planning single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="12993-114">tootest hello kroków w tym samouczku, zaleca się przy użyciu środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="12993-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="12993-115">tootest hello kroki opisane w tym samouczku, należy stosować te zalecenia:</span><span class="sxs-lookup"><span data-stu-id="12993-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="12993-116">Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="12993-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="12993-117">Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz [uzyskać miesięczna wersja próbna](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="12993-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="12993-118">Opis scenariusza</span><span class="sxs-lookup"><span data-stu-id="12993-118">Scenario description</span></span>
<span data-ttu-id="12993-119">W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym.</span><span class="sxs-lookup"><span data-stu-id="12993-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="12993-120">Scenariusz Hello opisane w tym samouczku składa się z dwóch głównych elementów:</span><span class="sxs-lookup"><span data-stu-id="12993-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="12993-121">Dodawanie planowania wybór Predictix z galerii hello</span><span class="sxs-lookup"><span data-stu-id="12993-121">Adding Predictix Assortment Planning from hello gallery</span></span>
2. <span data-ttu-id="12993-122">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="12993-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-predictix-assortment-planning-from-hello-gallery"></a><span data-ttu-id="12993-123">Dodawanie planowania wybór Predictix z galerii hello</span><span class="sxs-lookup"><span data-stu-id="12993-123">Adding Predictix Assortment Planning from hello gallery</span></span>
<span data-ttu-id="12993-124">tooconfigure hello integracja Predictix wybór planowania programu Azure AD, należy tooadd planowania wybór Predictix z hello galerii tooyour listę zarządzanych aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="12993-124">tooconfigure hello integration of Predictix Assortment Planning into Azure AD, you need tooadd Predictix Assortment Planning from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="12993-125">**tooadd Predictix wybór planowania z galerii hello, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="12993-125">**tooadd Predictix Assortment Planning from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="12993-126">W hello  **[portalu Azure](https://portal.azure.com)**na temat hello panelu nawigacji po lewej stronie, kliknij przycisk **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="12993-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![przycisk usługi Azure Active Directory Hello][1]

2. <span data-ttu-id="12993-128">Przejdź za**aplikacje dla przedsiębiorstw**.</span><span class="sxs-lookup"><span data-stu-id="12993-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="12993-129">Następnie przejdź zbyt**wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="12993-129">Then go too**All applications**.</span></span>

    ![Blok aplikacje przedsiębiorstwa Hello][2]
    
3. <span data-ttu-id="12993-131">tooadd nową aplikację, kliknij przycisk **nowej aplikacji** przycisk u góry hello okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="12993-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Nowy przycisk aplikacji Hello][3]

4. <span data-ttu-id="12993-133">W hello wyszukiwania wpisz **planowania wybór Predictix**, wybierz pozycję **planowania wybór Predictix** z panelu wyników kliknięcie **Dodaj** przycisk aplikacji hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="12993-133">In hello search box, type **Predictix Assortment Planning**, select **Predictix Assortment Planning** from result panel then click **Add** button tooadd hello application.</span></span>

    ![Predictix wybór planowania hello listy wyników](./media/active-directory-saas-predictix-assortment-planning-tutorial/tutorial_predictixassortmentplanning_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="12993-135">Konfiguracja i testowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="12993-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="12993-136">W tej sekcji możesz skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z Predictix wybór planowanie w oparciu o użytkownika testowego o nazwie "Britta Simona".</span><span class="sxs-lookup"><span data-stu-id="12993-136">In this section, you configure and test Azure AD single sign-on with Predictix Assortment Planning based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="12993-137">Dla pojedynczego logowania jednokrotnego toowork usługi Azure AD musi tooknow użytkownika odpowiednikiem hello planowania wybór Predictix jest tooa użytkownika w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="12993-137">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Predictix Assortment Planning is tooa user in Azure AD.</span></span> <span data-ttu-id="12993-138">Innymi słowy relację łącza między użytkownika usługi Azure AD i hello użytkownikowi w planowaniu wybór Predictix musi toobe ustanowione.</span><span class="sxs-lookup"><span data-stu-id="12993-138">In other words, a link relationship between an Azure AD user and hello related user in Predictix Assortment Planning needs toobe established.</span></span>

<span data-ttu-id="12993-139">W planowaniu wybór Predictix przypisać wartość hello hello **nazwy użytkownika** w usłudze Azure AD jako wartość hello hello **Username** tooestablish hello łącze relacji.</span><span class="sxs-lookup"><span data-stu-id="12993-139">In Predictix Assortment Planning, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="12993-140">tooconfigure i testowych usługi Azure AD rejestracji jednokrotnej z planowaniem wybór Predictix, należy po bloków konstrukcyjnych hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="12993-140">tooconfigure and test Azure AD single sign-on with Predictix Assortment Planning, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="12993-141">**[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configure-azure-ad-single-sign-on)**  -tooenable Twojego toouse użytkowników tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="12993-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="12993-142">**[Tworzenie użytkownika testowego usługi Azure AD](#create-an-azure-ad-test-user)**  -tootest usługi Azure AD rejestracji jednokrotnej z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="12993-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="12993-143">**[Tworzenie użytkownika testowego planowania wybór Predictix](#create-a-predictix-assortment-planning-test-user)**  -toohave odpowiednikiem Simona Britta Predictix wybór planowania, który jest połączony toohello usługi Azure AD reprezentację użytkownika.</span><span class="sxs-lookup"><span data-stu-id="12993-143">**[Create a Predictix Assortment Planning test user](#create-a-predictix-assortment-planning-test-user)** - toohave a counterpart of Britta Simon in Predictix Assortment Planning that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="12993-144">**[Przypisz użytkownika testowego hello Azure AD](#assign-the-azure-ad-test-user)**  -tooenable Simona Britta toouse usługi Azure AD rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="12993-144">**[Assign hello Azure AD test user](#assign-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="12993-145">**[Test rejestracji jednokrotnej](#test-single-sign-on)**  -tooverify czy hello konfiguracji działania.</span><span class="sxs-lookup"><span data-stu-id="12993-145">**[Test single sign-on](#test-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="12993-146">Konfigurowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="12993-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="12993-147">W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w hello portalu Azure i skonfigurować rejestracji jednokrotnej w aplikacji Predictix wybór planowania.</span><span class="sxs-lookup"><span data-stu-id="12993-147">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Predictix Assortment Planning application.</span></span>

<span data-ttu-id="12993-148">**tooconfigure usługi Azure AD rejestracji jednokrotnej z planowaniem wybór Predictix wykonaj hello następujące kroki:**</span><span class="sxs-lookup"><span data-stu-id="12993-148">**tooconfigure Azure AD single sign-on with Predictix Assortment Planning, perform hello following steps:**</span></span>

1. <span data-ttu-id="12993-149">W portalu Azure na powitania hello **planowania wybór Predictix** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.</span><span class="sxs-lookup"><span data-stu-id="12993-149">In hello Azure portal, on hello **Predictix Assortment Planning** application integration page, click **Single sign-on**.</span></span>

    ![Skonfigurować łącze rejestracji jednokrotnej][4]

2. <span data-ttu-id="12993-151">Na powitania **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** tooenable rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="12993-151">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Okno dialogowe rejestracji jednokrotnej](./media/active-directory-saas-predictix-assortment-planning-tutorial/tutorial_predictixassortmentplanning_samlbase.png)

3. <span data-ttu-id="12993-153">Na powitania **Predictix wybór planowania domeny i adres URL** sekcji, wykonaj następujące kroki hello:</span><span class="sxs-lookup"><span data-stu-id="12993-153">On hello **Predictix Assortment Planning Domain and URLs** section, perform hello following steps:</span></span>

    ![Adresy URL i domeny planowania wybór Predictix pojedynczy informacje logowania jednokrotnego](./media/active-directory-saas-predictix-assortment-planning-tutorial/tutorial_predictixassortmentplanning_url.png)

    <span data-ttu-id="12993-155">a.</span><span class="sxs-lookup"><span data-stu-id="12993-155">a.</span></span> <span data-ttu-id="12993-156">W hello **adres URL logowania** tekstowym, wpisz adres URL za pomocą hello następującego wzorca:</span><span class="sxs-lookup"><span data-stu-id="12993-156">In hello **Sign-on URL** textbox, type a URL using hello following pattern:</span></span>
    | |
    |--|--|
    | `https://<sub-domain>.ap.predictix.com/sso/request`|
    | `https://<sub-domain>.dev.ap.predictix.com/`|

    <span data-ttu-id="12993-157">b.</span><span class="sxs-lookup"><span data-stu-id="12993-157">b.</span></span> <span data-ttu-id="12993-158">W hello **identyfikator** tekstowym, wpisz adres URL za pomocą hello następującego wzorca:</span><span class="sxs-lookup"><span data-stu-id="12993-158">In hello **Identifier** textbox, type a URL using hello following pattern:</span></span>
    | |
    |--|--|
    | `https://<sub-domain>.ap.predictix.com`|
    | `https://<sub-domain>.dev.ap.predictix.com`|
    
    > [!NOTE] 
    > <span data-ttu-id="12993-159">Wartości te nie są prawdziwe.</span><span class="sxs-lookup"><span data-stu-id="12993-159">These values are not real.</span></span> <span data-ttu-id="12993-160">Zaktualizować te wartości z hello rzeczywisty adres URL logowania i identyfikator.</span><span class="sxs-lookup"><span data-stu-id="12993-160">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="12993-161">Skontaktuj się z [zespołem pomocy technicznej klienta planowania wybór Predictix](http://www.infor.com/support) tooget tych wartości.</span><span class="sxs-lookup"><span data-stu-id="12993-161">Contact [Predictix Assortment Planning Client support team](http://www.infor.com/support) tooget these values.</span></span> 
 


4. <span data-ttu-id="12993-162">Na powitania **certyfikat podpisywania SAML** kliknij **Certificate(Base64)** , a następnie zapisz plik certyfikatu hello na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="12993-162">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![link do pobierania certyfikatu Hello](./media/active-directory-saas-predictix-assortment-planning-tutorial/tutorial_predictixassortmentplanning_certificate.png) 

5. <span data-ttu-id="12993-164">Kliknij przycisk **zapisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="12993-164">Click **Save** button.</span></span>

    ![Skonfiguruj przycisk pojedynczego logowania jednokrotnego Zapisz](./media/active-directory-saas-predictix-assortment-planning-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="12993-166">Na powitania **Predictix wybór planowania konfiguracji** kliknij **skonfigurować planowania wybór Predictix** tooopen **Konfigurowanie logowania jednokrotnego** okna.</span><span class="sxs-lookup"><span data-stu-id="12993-166">On hello **Predictix Assortment Planning Configuration** section, click **Configure Predictix Assortment Planning** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="12993-167">Kopiuj hello **Sign-Out adres URL, identyfikator jednostki SAML i SAML pojedynczy znak na adres URL usługi** z hello **sekcji krótkimi opisami.**</span><span class="sxs-lookup"><span data-stu-id="12993-167">Copy hello **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Predictix wybór planowania konfiguracji](./media/active-directory-saas-predictix-assortment-planning-tutorial/tutorial_predictixassortmentplanning_configure.png) 

7. <span data-ttu-id="12993-169">tooconfigure rejestracji jednokrotnej w **planowania wybór Predictix** strony, należy pobrać hello toosend **Certificate(Base64)**, **identyfikator jednostki SAML**,  **SAML pojedynczy znak na adres URL usługi**, i **Sign-Out URL** za[Predictix wybór planowania zespołem pomocy technicznej](http://www.infor.com/support).</span><span class="sxs-lookup"><span data-stu-id="12993-169">tooconfigure single sign-on on **Predictix Assortment Planning** side, you need toosend hello downloaded **Certificate(Base64)**, **SAML Entity ID**, **SAML Single Sign-On Service URL**, and **Sign-Out URL**  too[Predictix Assortment Planning support team](http://www.infor.com/support).</span></span> <span data-ttu-id="12993-170">To ustawienie toohave hello prawidłowo po obu stronach połączenia logowania jednokrotnego SAML one ustawić.</span><span class="sxs-lookup"><span data-stu-id="12993-170">They set this setting toohave hello SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="12993-171">Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz hello [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji hello!</span><span class="sxs-lookup"><span data-stu-id="12993-171">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="12993-172">Po dodaniu tej aplikacji z hello **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij hello **rejestracji jednokrotnej** hello kartę i dostępu do osadzonych dokumentacji za pośrednictwem hello  **Konfiguracja** sekcji u dołu hello.</span><span class="sxs-lookup"><span data-stu-id="12993-172">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="12993-173">Więcej o hello osadzonych dokumentacji funkcji w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="12993-173">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="12993-174">Tworzenie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="12993-174">Create an Azure AD test user</span></span>

<span data-ttu-id="12993-175">Celem Hello w tej sekcji jest toocreate użytkownika testowego, w portalu Azure o nazwie Simona Britta hello.</span><span class="sxs-lookup"><span data-stu-id="12993-175">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

   ![Tworzenie użytkownika testowego usługi Azure AD][100]

<span data-ttu-id="12993-177">**toocreate użytkownika testowego w usłudze Azure AD, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="12993-177">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="12993-178">W portalu Azure, w okienku po lewej stronie powitania hello kliknij hello **usługi Azure Active Directory** przycisku.</span><span class="sxs-lookup"><span data-stu-id="12993-178">In hello Azure portal, in hello left pane, click hello **Azure Active Directory** button.</span></span>

    ![przycisk usługi Azure Active Directory Hello](./media/active-directory-saas-predictix-assortment-planning-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="12993-180">toodisplay hello listę użytkowników, przejdź zbyt**użytkowników i grup**, a następnie kliknij przycisk **wszyscy użytkownicy**.</span><span class="sxs-lookup"><span data-stu-id="12993-180">toodisplay hello list of users, go too**Users and groups**, and then click **All users**.</span></span>

    ![Witaj, "Użytkownicy i grupy" i "Wszyscy użytkownicy" łącza](./media/active-directory-saas-predictix-assortment-planning-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="12993-182">Witaj tooopen **użytkownika** okno dialogowe, kliknij przycisk **Dodaj** u góry hello hello **wszyscy użytkownicy** okno dialogowe.</span><span class="sxs-lookup"><span data-stu-id="12993-182">tooopen hello **User** dialog box, click **Add** at hello top of hello **All Users** dialog box.</span></span>

    ![przycisk Dodaj Hello](./media/active-directory-saas-predictix-assortment-planning-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="12993-184">W hello **użytkownika** okna dialogowego wykonaj hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="12993-184">In hello **User** dialog box, perform hello following steps:</span></span>

    ![okno dialogowe Hello użytkownika](./media/active-directory-saas-predictix-assortment-planning-tutorial/create_aaduser_04.png)

    <span data-ttu-id="12993-186">a.</span><span class="sxs-lookup"><span data-stu-id="12993-186">a.</span></span> <span data-ttu-id="12993-187">W hello **nazwa** wpisz **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="12993-187">In hello **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="12993-188">b.</span><span class="sxs-lookup"><span data-stu-id="12993-188">b.</span></span> <span data-ttu-id="12993-189">W hello **nazwy użytkownika** pole typu hello adres e-mail użytkownika Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="12993-189">In hello **User name** box, type hello email address of user Britta Simon.</span></span>

    <span data-ttu-id="12993-190">c.</span><span class="sxs-lookup"><span data-stu-id="12993-190">c.</span></span> <span data-ttu-id="12993-191">Wybierz hello **Pokaż hasło** pole wyboru, a następnie zapisz hello wartość, która jest wyświetlana w hello **hasło** pole.</span><span class="sxs-lookup"><span data-stu-id="12993-191">Select hello **Show Password** check box, and then write down hello value that's displayed in hello **Password** box.</span></span>

    <span data-ttu-id="12993-192">d.</span><span class="sxs-lookup"><span data-stu-id="12993-192">d.</span></span> <span data-ttu-id="12993-193">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="12993-193">Click **Create**.</span></span>
 
### <a name="create-a-predictix-assortment-planning-test-user"></a><span data-ttu-id="12993-194">Tworzenie użytkownika testowego Predictix wybór planowania</span><span class="sxs-lookup"><span data-stu-id="12993-194">Create a Predictix Assortment Planning test user</span></span>

<span data-ttu-id="12993-195">W tej sekcji należy utworzyć użytkownika o nazwie Simona Britta Predictix wybór planowania.</span><span class="sxs-lookup"><span data-stu-id="12993-195">In this section, you create a user called Britta Simon in Predictix Assortment Planning.</span></span> <span data-ttu-id="12993-196">We współpracy z [Predictix wybór planowania zespołem pomocy technicznej](http://www.infor.com/contact/) użytkowników hello tooadd hello planowania wybór Predictix platformy.</span><span class="sxs-lookup"><span data-stu-id="12993-196">Please work with [Predictix Assortment Planning support team](http://www.infor.com/contact/) tooadd hello users in hello Predictix Assortment Planning platform.</span></span>
 > [!NOTE]
 > <span data-ttu-id="12993-197">Właściciel konta usługi Azure Active Directory Hello otrzymuje wiadomość e-mail i następuje tooconfirm łącze swojego konta, zanim staje się aktywny.</span><span class="sxs-lookup"><span data-stu-id="12993-197">hello Azure Active Directory account holder receives an email and follows a link tooconfirm their account before it becomes active.</span></span>

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="12993-198">Przypisz użytkownika testowego hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="12993-198">Assign hello Azure AD test user</span></span>

<span data-ttu-id="12993-199">W tej sekcji możesz włączyć toouse Simona Britta Azure logowania jednokrotnego za udzielanie dostępu tooPredictix wybór planowania.</span><span class="sxs-lookup"><span data-stu-id="12993-199">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooPredictix Assortment Planning.</span></span>

![Przypisanie roli użytkownika hello][200] 

<span data-ttu-id="12993-201">**tooassign tooPredictix Simona Britta wybór planowania należy wykonać hello następujące kroki:**</span><span class="sxs-lookup"><span data-stu-id="12993-201">**tooassign Britta Simon tooPredictix Assortment Planning, perform hello following steps:**</span></span>

1. <span data-ttu-id="12993-202">W portalu Azure hello, otwórz widok aplikacji hello, a następnie przejdź do widoku katalogu toohello i przejść za**aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="12993-202">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Przypisz użytkownika][201] 

2. <span data-ttu-id="12993-204">Z listy aplikacji hello wybierz **planowania wybór Predictix**.</span><span class="sxs-lookup"><span data-stu-id="12993-204">In hello applications list, select **Predictix Assortment Planning**.</span></span>

    ![Hello planowania wybór Predictix łącza na liście aplikacji hello](./media/active-directory-saas-predictix-assortment-planning-tutorial/tutorial_predictixassortmentplanning_app.png)  

3. <span data-ttu-id="12993-206">W menu powitania po lewej stronie powitania kliknij **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="12993-206">In hello menu on hello left, click **Users and groups**.</span></span>

    ![łącze "Użytkownicy i grupy" Hello][202]

4. <span data-ttu-id="12993-208">Kliknij przycisk **Dodaj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="12993-208">Click **Add** button.</span></span> <span data-ttu-id="12993-209">Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="12993-209">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Okienko Dodaj przypisania Hello][203]

5. <span data-ttu-id="12993-211">Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** hello listy użytkowników.</span><span class="sxs-lookup"><span data-stu-id="12993-211">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="12993-212">Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="12993-212">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="12993-213">Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="12993-213">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="12993-214">Test rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="12993-214">Test single sign-on</span></span>

<span data-ttu-id="12993-215">W tej sekcji można przetestować konfiguracji usługi Azure AD pojedynczego logowania jednokrotnego przy użyciu hello panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="12993-215">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="12993-216">Po kliknięciu kafelka planowania wybór Predictix hello w hello Panel dostępu, należy pobrać automatycznie zalogowane tooyour planowania wybór Predictix aplikacji.</span><span class="sxs-lookup"><span data-stu-id="12993-216">When you click hello Predictix Assortment Planning tile in hello Access Panel, you should get automatically signed-on tooyour Predictix Assortment Planning application.</span></span>
<span data-ttu-id="12993-217">Aby uzyskać więcej informacji na temat panelu dostępu, zobacz [toohello wprowadzenie panelu dostępu](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="12993-217">For more information about the Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="12993-218">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="12993-218">Additional resources</span></span>

* [<span data-ttu-id="12993-219">Lista samouczków dotyczących tooIntegrate aplikacji SaaS w usłudze Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="12993-219">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="12993-220">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="12993-220">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-predictix-assortment-planning-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-predictix-assortment-planning-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-predictix-assortment-planning-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-predictix-assortment-planning-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-predictix-assortment-planning-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-predictix-assortment-planning-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-predictix-assortment-planning-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-predictix-assortment-planning-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-predictix-assortment-planning-tutorial/tutorial_general_203.png

