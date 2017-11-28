---
title: 'Samouczek: Integracji Azure Active Directory z RealtimeBoard | Dokumentacja firmy Microsoft'
description: "Dowiedz się, jak tooconfigure logowanie jednokrotne między usługą Azure Active Directory i RealtimeBoard."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: a37fc1c0-4bae-4173-989b-00de53a0076f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/31/2017
ms.author: jeedes
ms.openlocfilehash: 76644c9ba643d61a903295dea4d417716a47774a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-realtimeboard"></a><span data-ttu-id="be11c-103">Samouczek: Integracji Azure Active Directory z RealtimeBoard</span><span class="sxs-lookup"><span data-stu-id="be11c-103">Tutorial: Azure Active Directory integration with RealtimeBoard</span></span>

<span data-ttu-id="be11c-104">Z tego samouczka, dowiesz się, jak toointegrate RealtimeBoard w usłudze Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="be11c-104">In this tutorial, you learn how toointegrate RealtimeBoard with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="be11c-105">Integracja z usługą Azure AD RealtimeBoard zapewnia hello następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="be11c-105">Integrating RealtimeBoard with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="be11c-106">Można kontrolować w usłudze Azure AD, kto ma dostęp do tooRealtimeBoard.</span><span class="sxs-lookup"><span data-stu-id="be11c-106">You can control in Azure AD who has access tooRealtimeBoard.</span></span>
- <span data-ttu-id="be11c-107">Można włączyć użytkownika użytkownicy tooautomatically get zalogowane tooRealtimeBoard (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="be11c-107">You can enable your users tooautomatically get signed-on tooRealtimeBoard (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="be11c-108">Możesz zarządzać kont w jednej centralnej lokalizacji - hello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="be11c-108">You can manage your accounts in one central location - hello Azure portal.</span></span>

<span data-ttu-id="be11c-109">Jeśli chcesz tooknow więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="be11c-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="be11c-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="be11c-110">Prerequisites</span></span>

<span data-ttu-id="be11c-111">tooconfigure integracji z usługą Azure AD z RealtimeBoard należy hello następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="be11c-111">tooconfigure Azure AD integration with RealtimeBoard, you need hello following items:</span></span>

- <span data-ttu-id="be11c-112">Subskrypcję usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="be11c-112">An Azure AD subscription</span></span>
- <span data-ttu-id="be11c-113">RealtimeBoard logowanie jednokrotne włączone subskrypcji</span><span class="sxs-lookup"><span data-stu-id="be11c-113">A RealtimeBoard single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="be11c-114">tootest hello kroków w tym samouczku, zaleca się przy użyciu środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="be11c-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="be11c-115">tootest hello kroki opisane w tym samouczku, należy stosować te zalecenia:</span><span class="sxs-lookup"><span data-stu-id="be11c-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="be11c-116">Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="be11c-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="be11c-117">Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz [uzyskać miesięczna wersja próbna](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="be11c-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="be11c-118">Opis scenariusza</span><span class="sxs-lookup"><span data-stu-id="be11c-118">Scenario description</span></span>
<span data-ttu-id="be11c-119">W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym.</span><span class="sxs-lookup"><span data-stu-id="be11c-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="be11c-120">Scenariusz Hello opisane w tym samouczku składa się z dwóch głównych elementów:</span><span class="sxs-lookup"><span data-stu-id="be11c-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="be11c-121">Dodawanie RealtimeBoard z galerii hello</span><span class="sxs-lookup"><span data-stu-id="be11c-121">Adding RealtimeBoard from hello gallery</span></span>
2. <span data-ttu-id="be11c-122">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="be11c-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-realtimeboard-from-hello-gallery"></a><span data-ttu-id="be11c-123">Dodawanie RealtimeBoard z galerii hello</span><span class="sxs-lookup"><span data-stu-id="be11c-123">Adding RealtimeBoard from hello gallery</span></span>
<span data-ttu-id="be11c-124">tooconfigure hello integracji RealtimeBoard do usługi Azure AD, należy tooadd RealtimeBoard z hello galerii tooyour listę zarządzanych aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="be11c-124">tooconfigure hello integration of RealtimeBoard into Azure AD, you need tooadd RealtimeBoard from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="be11c-125">**tooadd RealtimeBoard z galerii hello, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="be11c-125">**tooadd RealtimeBoard from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="be11c-126">W hello  **[portalu Azure](https://portal.azure.com)**na temat hello panelu nawigacji po lewej stronie, kliknij przycisk **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="be11c-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![przycisk usługi Azure Active Directory Hello][1]

2. <span data-ttu-id="be11c-128">Przejdź za**aplikacje dla przedsiębiorstw**.</span><span class="sxs-lookup"><span data-stu-id="be11c-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="be11c-129">Następnie przejdź zbyt**wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="be11c-129">Then go too**All applications**.</span></span>

    ![Blok aplikacje przedsiębiorstwa Hello][2]
    
3. <span data-ttu-id="be11c-131">tooadd nową aplikację, kliknij przycisk **nowej aplikacji** przycisk u góry hello okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="be11c-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Nowy przycisk aplikacji Hello][3]

4. <span data-ttu-id="be11c-133">W polu wyszukiwania hello wpisz **RealtimeBoard**, wybierz pozycję **RealtimeBoard** z panelu wyników następnie kliknij przycisk **Dodaj** przycisk aplikacji hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="be11c-133">In hello search box, type **RealtimeBoard**, select **RealtimeBoard** from result panel then click **Add** button tooadd hello application.</span></span>

    ![RealtimeBoard hello listy wyników](./media/active-directory-saas-realtimeboard-tutorial/tutorial_realtimeboard_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="be11c-135">Konfiguracja i testowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="be11c-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="be11c-136">W tej sekcji skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z RealtimeBoard w oparciu o nazwie "Britta Simona" użytkownika testowego.</span><span class="sxs-lookup"><span data-stu-id="be11c-136">In this section, you configure and test Azure AD single sign-on with RealtimeBoard based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="be11c-137">Dla pojedynczego logowania jednokrotnego toowork usługi Azure AD musi tooknow użytkownika odpowiednikiem hello w RealtimeBoard jest tooa użytkownika w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="be11c-137">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in RealtimeBoard is tooa user in Azure AD.</span></span> <span data-ttu-id="be11c-138">Innymi słowy relację łącza między użytkownika usługi Azure AD i hello użytkownikowi w RealtimeBoard musi toobe ustanowione.</span><span class="sxs-lookup"><span data-stu-id="be11c-138">In other words, a link relationship between an Azure AD user and hello related user in RealtimeBoard needs toobe established.</span></span>

<span data-ttu-id="be11c-139">W RealtimeBoard, należy przypisać wartość hello hello **nazwy użytkownika** w usłudze Azure AD jako wartość hello hello **Username** tooestablish hello łącze relacji.</span><span class="sxs-lookup"><span data-stu-id="be11c-139">In RealtimeBoard, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="be11c-140">tooconfigure i testowych usługi Azure AD rejestracji jednokrotnej z RealtimeBoard, należy po bloków konstrukcyjnych hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="be11c-140">tooconfigure and test Azure AD single sign-on with RealtimeBoard, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="be11c-141">**[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configure-azure-ad-single-sign-on)**  -tooenable Twojego toouse użytkowników tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="be11c-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="be11c-142">**[Tworzenie użytkownika testowego usługi Azure AD](#create-an-azure-ad-test-user)**  -tootest usługi Azure AD rejestracji jednokrotnej z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="be11c-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="be11c-143">**[Tworzenie użytkownika testowego RealtimeBoard](#create-a-realtimeboard-test-user)**  -toohave odpowiednikiem Simona Britta w RealtimeBoard, który jest połączony toohello usługi Azure AD reprezentację użytkownika.</span><span class="sxs-lookup"><span data-stu-id="be11c-143">**[Create a RealtimeBoard test user](#create-a-realtimeboard-test-user)** - toohave a counterpart of Britta Simon in RealtimeBoard that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="be11c-144">**[Przypisz użytkownika testowego hello Azure AD](#assign-the-azure-ad-test-user)**  -tooenable Simona Britta toouse usługi Azure AD rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="be11c-144">**[Assign hello Azure AD test user](#assign-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="be11c-145">**[Test rejestracji jednokrotnej](#test-single-sign-on)**  -tooverify czy hello konfiguracji działania.</span><span class="sxs-lookup"><span data-stu-id="be11c-145">**[Test single sign-on](#test-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="be11c-146">Konfigurowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="be11c-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="be11c-147">W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w portalu Azure hello i skonfigurować logowanie jednokrotne w aplikacji RealtimeBoard.</span><span class="sxs-lookup"><span data-stu-id="be11c-147">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your RealtimeBoard application.</span></span>

<span data-ttu-id="be11c-148">**tooconfigure usługi Azure AD rejestracji jednokrotnej z RealtimeBoard, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="be11c-148">**tooconfigure Azure AD single sign-on with RealtimeBoard, perform hello following steps:**</span></span>

1. <span data-ttu-id="be11c-149">W portalu Azure na powitania hello **RealtimeBoard** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.</span><span class="sxs-lookup"><span data-stu-id="be11c-149">In hello Azure portal, on hello **RealtimeBoard** application integration page, click **Single sign-on**.</span></span>

    ![Skonfigurować łącze rejestracji jednokrotnej][4]

2. <span data-ttu-id="be11c-151">Na powitania **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** tooenable rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="be11c-151">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Okno dialogowe rejestracji jednokrotnej](./media/active-directory-saas-realtimeboard-tutorial/tutorial_realtimeboard_samlbase.png)

3. <span data-ttu-id="be11c-153">Na powitania **RealtimeBoard domeny i adres URL** sekcji, jeśli chcesz, aby aplikacja hello tooconfigure w **IDP** inicjowane tryb:</span><span class="sxs-lookup"><span data-stu-id="be11c-153">On hello **RealtimeBoard Domain and URLs** section, if you wish tooconfigure hello application in **IDP** initiated mode:</span></span>

    ![Adresy URL i domeny RealtimeBoard pojedynczy informacje logowania jednokrotnego](./media/active-directory-saas-realtimeboard-tutorial/tutorial_realtimeboard_url.png)

    <span data-ttu-id="be11c-155">W hello **identyfikator** tekstowym, wpisz adres URL jako:`https://realtimeboard.com/`</span><span class="sxs-lookup"><span data-stu-id="be11c-155">In hello **Identifier** textbox, type a URL as: `https://realtimeboard.com/`</span></span>

4. <span data-ttu-id="be11c-156">Sprawdź **Pokaż zaawansowane ustawienia adresu URL**, jeśli chcesz, aby aplikacja hello tooconfigure w **SP** inicjowane tryb:</span><span class="sxs-lookup"><span data-stu-id="be11c-156">Check **Show advanced URL settings**, if you wish tooconfigure hello application in **SP** initiated mode:</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-realtimeboard-tutorial/tutorial_realtimeboard_url2.png)

    <span data-ttu-id="be11c-158">W hello **adres URL logowania** tekstowym, wpisz adres URL jako:`https://realtimeboard.com/sso/saml`</span><span class="sxs-lookup"><span data-stu-id="be11c-158">In hello **Sign-on URL** textbox, type a URL as: `https://realtimeboard.com/sso/saml`</span></span>

5. <span data-ttu-id="be11c-159">Na powitania **certyfikat podpisywania SAML** kliknij **XML metadanych** , a następnie zapisz plik metadanych hello na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="be11c-159">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![link do pobierania certyfikatu Hello](./media/active-directory-saas-realtimeboard-tutorial/tutorial_realtimeboard_certificate.png) 

6. <span data-ttu-id="be11c-161">Kliknij przycisk **zapisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="be11c-161">Click **Save** button.</span></span>

    ![Skonfiguruj przycisk pojedynczego logowania jednokrotnego Zapisz](./media/active-directory-saas-realtimeboard-tutorial/tutorial_general_400.png)

7. <span data-ttu-id="be11c-163">tooconfigure rejestracji jednokrotnej w **RealtimeBoard** strony, należy pobrać hello toosend **XML metadanych** za[zespołem pomocy technicznej RealtimeBoard](mailto:support@realtimeboard.com).</span><span class="sxs-lookup"><span data-stu-id="be11c-163">tooconfigure single sign-on on **RealtimeBoard** side, you need toosend hello downloaded **Metadata XML** too[RealtimeBoard support team](mailto:support@realtimeboard.com).</span></span> <span data-ttu-id="be11c-164">To ustawienie toohave hello prawidłowo po obu stronach połączenia logowania jednokrotnego SAML one ustawić.</span><span class="sxs-lookup"><span data-stu-id="be11c-164">They set this setting toohave hello SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="be11c-165">Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz hello [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji hello!</span><span class="sxs-lookup"><span data-stu-id="be11c-165">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="be11c-166">Po dodaniu tej aplikacji z hello **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij hello **rejestracji jednokrotnej** hello kartę i dostępu do osadzonych dokumentacji za pośrednictwem hello  **Konfiguracja** sekcji u dołu hello.</span><span class="sxs-lookup"><span data-stu-id="be11c-166">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="be11c-167">Więcej o hello osadzonych dokumentacji funkcji w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="be11c-167">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="be11c-168">Tworzenie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="be11c-168">Create an Azure AD test user</span></span>

<span data-ttu-id="be11c-169">Celem Hello w tej sekcji jest toocreate użytkownika testowego, w portalu Azure o nazwie Simona Britta hello.</span><span class="sxs-lookup"><span data-stu-id="be11c-169">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

   ![Tworzenie użytkownika testowego usługi Azure AD][100]

<span data-ttu-id="be11c-171">**toocreate użytkownika testowego w usłudze Azure AD, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="be11c-171">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="be11c-172">W portalu Azure, w okienku po lewej stronie powitania hello kliknij hello **usługi Azure Active Directory** przycisku.</span><span class="sxs-lookup"><span data-stu-id="be11c-172">In hello Azure portal, in hello left pane, click hello **Azure Active Directory** button.</span></span>

    ![przycisk usługi Azure Active Directory Hello](./media/active-directory-saas-realtimeboard-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="be11c-174">toodisplay hello listę użytkowników, przejdź zbyt**użytkowników i grup**, a następnie kliknij przycisk **wszyscy użytkownicy**.</span><span class="sxs-lookup"><span data-stu-id="be11c-174">toodisplay hello list of users, go too**Users and groups**, and then click **All users**.</span></span>

    ![Witaj, "Użytkownicy i grupy" i "Wszyscy użytkownicy" łącza](./media/active-directory-saas-realtimeboard-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="be11c-176">Witaj tooopen **użytkownika** okno dialogowe, kliknij przycisk **Dodaj** u góry hello hello **wszyscy użytkownicy** okno dialogowe.</span><span class="sxs-lookup"><span data-stu-id="be11c-176">tooopen hello **User** dialog box, click **Add** at hello top of hello **All Users** dialog box.</span></span>

    ![przycisk Dodaj Hello](./media/active-directory-saas-realtimeboard-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="be11c-178">W hello **użytkownika** okna dialogowego wykonaj hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="be11c-178">In hello **User** dialog box, perform hello following steps:</span></span>

    ![okno dialogowe Hello użytkownika](./media/active-directory-saas-realtimeboard-tutorial/create_aaduser_04.png)

    <span data-ttu-id="be11c-180">a.</span><span class="sxs-lookup"><span data-stu-id="be11c-180">a.</span></span> <span data-ttu-id="be11c-181">W hello **nazwa** wpisz **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="be11c-181">In hello **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="be11c-182">b.</span><span class="sxs-lookup"><span data-stu-id="be11c-182">b.</span></span> <span data-ttu-id="be11c-183">W hello **nazwy użytkownika** pole typu hello adres e-mail użytkownika Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="be11c-183">In hello **User name** box, type hello email address of user Britta Simon.</span></span>

    <span data-ttu-id="be11c-184">c.</span><span class="sxs-lookup"><span data-stu-id="be11c-184">c.</span></span> <span data-ttu-id="be11c-185">Wybierz hello **Pokaż hasło** pole wyboru, a następnie zapisz hello wartość, która jest wyświetlana w hello **hasło** pole.</span><span class="sxs-lookup"><span data-stu-id="be11c-185">Select hello **Show Password** check box, and then write down hello value that's displayed in hello **Password** box.</span></span>

    <span data-ttu-id="be11c-186">d.</span><span class="sxs-lookup"><span data-stu-id="be11c-186">d.</span></span> <span data-ttu-id="be11c-187">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="be11c-187">Click **Create**.</span></span>
 
### <a name="create-a-realtimeboard-test-user"></a><span data-ttu-id="be11c-188">Tworzenie użytkownika testowego RealtimeBoard</span><span class="sxs-lookup"><span data-stu-id="be11c-188">Create a RealtimeBoard test user</span></span>

<span data-ttu-id="be11c-189">Celem Hello w tej sekcji jest toocreate użytkownika o nazwie Simona Britta w RealtimeBoard.</span><span class="sxs-lookup"><span data-stu-id="be11c-189">hello objective of this section is toocreate a user called Britta Simon in RealtimeBoard.</span></span> <span data-ttu-id="be11c-190">RealtimeBoard obsługę w czasie, który jest domyślnie włączone.</span><span class="sxs-lookup"><span data-stu-id="be11c-190">RealtimeBoard supports just-in-time provisioning, which is by default enabled.</span></span>

<span data-ttu-id="be11c-191">Nie ma elementu akcji można w tej sekcji.</span><span class="sxs-lookup"><span data-stu-id="be11c-191">There is no action item for you in this section.</span></span> <span data-ttu-id="be11c-192">Jeśli użytkownik nie istnieje w RealtimeBoard, tworzona jest nowy, podczas próby tooaccess RealtimeBoard.</span><span class="sxs-lookup"><span data-stu-id="be11c-192">If a user doesn't already exist in RealtimeBoard, a new one is created when you attempt tooaccess RealtimeBoard.</span></span>

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="be11c-193">Przypisz użytkownika testowego hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="be11c-193">Assign hello Azure AD test user</span></span>

<span data-ttu-id="be11c-194">W tej sekcji możesz włączyć toouse Simona Britta Azure logowania jednokrotnego za udzielanie dostępu tooRealtimeBoard.</span><span class="sxs-lookup"><span data-stu-id="be11c-194">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooRealtimeBoard.</span></span>

![Przypisanie roli użytkownika hello][200] 

<span data-ttu-id="be11c-196">**tooassign tooRealtimeBoard Simona Britta wykonaj hello następujące kroki:**</span><span class="sxs-lookup"><span data-stu-id="be11c-196">**tooassign Britta Simon tooRealtimeBoard, perform hello following steps:**</span></span>

1. <span data-ttu-id="be11c-197">W portalu Azure hello, otwórz widok aplikacji hello, a następnie przejdź do widoku katalogu toohello i przejść za**aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="be11c-197">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Przypisz użytkownika][201] 

2. <span data-ttu-id="be11c-199">Z listy aplikacji hello wybierz **RealtimeBoard**.</span><span class="sxs-lookup"><span data-stu-id="be11c-199">In hello applications list, select **RealtimeBoard**.</span></span>

    ![łącze RealtimeBoard Hello na liście aplikacji hello](./media/active-directory-saas-realtimeboard-tutorial/tutorial_realtimeboard_app.png)  

3. <span data-ttu-id="be11c-201">W menu powitania po lewej stronie powitania kliknij **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="be11c-201">In hello menu on hello left, click **Users and groups**.</span></span>

    ![łącze "Użytkownicy i grupy" Hello][202]

4. <span data-ttu-id="be11c-203">Kliknij przycisk **Dodaj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="be11c-203">Click **Add** button.</span></span> <span data-ttu-id="be11c-204">Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="be11c-204">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Okienko Dodaj przypisania Hello][203]

5. <span data-ttu-id="be11c-206">Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** hello listy użytkowników.</span><span class="sxs-lookup"><span data-stu-id="be11c-206">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="be11c-207">Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="be11c-207">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="be11c-208">Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="be11c-208">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="be11c-209">Test rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="be11c-209">Test single sign-on</span></span>

<span data-ttu-id="be11c-210">W tej sekcji można przetestować konfiguracji usługi Azure AD pojedynczego logowania jednokrotnego przy użyciu hello panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="be11c-210">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="be11c-211">Po kliknięciu kafelka RealtimeBoard hello w hello Panel dostępu, należy pobrać automatycznie zalogowane tooyour RealtimeBoard aplikacji.</span><span class="sxs-lookup"><span data-stu-id="be11c-211">When you click hello RealtimeBoard tile in hello Access Panel, you should get automatically signed-on tooyour RealtimeBoard application.</span></span>
<span data-ttu-id="be11c-212">Aby uzyskać więcej informacji na temat panelu dostępu, zobacz [toohello wprowadzenie panelu dostępu](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="be11c-212">For more information about the Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="be11c-213">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="be11c-213">Additional resources</span></span>

* [<span data-ttu-id="be11c-214">Lista samouczków dotyczących tooIntegrate aplikacji SaaS w usłudze Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="be11c-214">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="be11c-215">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="be11c-215">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-realtimeboard-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-realtimeboard-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-realtimeboard-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-realtimeboard-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-realtimeboard-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-realtimeboard-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-realtimeboard-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-realtimeboard-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-realtimeboard-tutorial/tutorial_general_203.png

