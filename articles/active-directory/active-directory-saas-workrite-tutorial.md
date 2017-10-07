---
title: 'Samouczek: Integracji Azure Active Directory z Workrite | Dokumentacja firmy Microsoft'
description: "Dowiedz się, jak tooconfigure logowanie jednokrotne między usługą Azure Active Directory i Workrite."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 2a5c2956-a011-4d5c-877b-80679b6587b5
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/19/2017
ms.author: jeedes
ms.openlocfilehash: a663374ae3c8b102b53d8cf05a9cb083b80dbb83
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-workrite"></a><span data-ttu-id="b3510-103">Samouczek: Integracji Azure Active Directory z Workrite</span><span class="sxs-lookup"><span data-stu-id="b3510-103">Tutorial: Azure Active Directory integration with Workrite</span></span>

<span data-ttu-id="b3510-104">Z tego samouczka, dowiesz się, jak toointegrate Workrite w usłudze Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="b3510-104">In this tutorial, you learn how toointegrate Workrite with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="b3510-105">Integracja z usługą Azure AD Workrite zapewnia hello następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="b3510-105">Integrating Workrite with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="b3510-106">Można kontrolować w usłudze Azure AD, kto ma dostęp do tooWorkrite.</span><span class="sxs-lookup"><span data-stu-id="b3510-106">You can control in Azure AD who has access tooWorkrite.</span></span>
- <span data-ttu-id="b3510-107">Można włączyć użytkownika użytkownicy tooautomatically get zalogowane tooWorkrite (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="b3510-107">You can enable your users tooautomatically get signed-on tooWorkrite (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="b3510-108">Możesz zarządzać kont w jednej centralnej lokalizacji - hello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="b3510-108">You can manage your accounts in one central location - hello Azure portal.</span></span>

<span data-ttu-id="b3510-109">Jeśli chcesz tooknow więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="b3510-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b3510-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="b3510-110">Prerequisites</span></span>

<span data-ttu-id="b3510-111">tooconfigure integracji z usługą Azure AD z Workrite należy hello następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="b3510-111">tooconfigure Azure AD integration with Workrite, you need hello following items:</span></span>

- <span data-ttu-id="b3510-112">Subskrypcję usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="b3510-112">An Azure AD subscription</span></span>
- <span data-ttu-id="b3510-113">Workrite logowanie jednokrotne włączone subskrypcji</span><span class="sxs-lookup"><span data-stu-id="b3510-113">A Workrite single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="b3510-114">tootest hello kroków w tym samouczku, zaleca się przy użyciu środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="b3510-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="b3510-115">tootest hello kroki opisane w tym samouczku, należy stosować te zalecenia:</span><span class="sxs-lookup"><span data-stu-id="b3510-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="b3510-116">Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="b3510-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="b3510-117">Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz [uzyskać miesięczna wersja próbna](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="b3510-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="b3510-118">Opis scenariusza</span><span class="sxs-lookup"><span data-stu-id="b3510-118">Scenario description</span></span>
<span data-ttu-id="b3510-119">W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym.</span><span class="sxs-lookup"><span data-stu-id="b3510-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="b3510-120">Scenariusz Hello opisane w tym samouczku składa się z dwóch głównych elementów:</span><span class="sxs-lookup"><span data-stu-id="b3510-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="b3510-121">Dodawanie Workrite z galerii hello</span><span class="sxs-lookup"><span data-stu-id="b3510-121">Adding Workrite from hello gallery</span></span>
2. <span data-ttu-id="b3510-122">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="b3510-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-workrite-from-hello-gallery"></a><span data-ttu-id="b3510-123">Dodawanie Workrite z galerii hello</span><span class="sxs-lookup"><span data-stu-id="b3510-123">Adding Workrite from hello gallery</span></span>
<span data-ttu-id="b3510-124">tooconfigure hello integracji Workrite do usługi Azure AD, należy tooadd Workrite z hello galerii tooyour listę zarządzanych aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="b3510-124">tooconfigure hello integration of Workrite into Azure AD, you need tooadd Workrite from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="b3510-125">**tooadd Workrite z galerii hello, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="b3510-125">**tooadd Workrite from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="b3510-126">W hello  **[portalu Azure](https://portal.azure.com)**na temat hello panelu nawigacji po lewej stronie, kliknij przycisk **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="b3510-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![przycisk usługi Azure Active Directory Hello][1]

2. <span data-ttu-id="b3510-128">Przejdź za**aplikacje dla przedsiębiorstw**.</span><span class="sxs-lookup"><span data-stu-id="b3510-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="b3510-129">Następnie przejdź zbyt**wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="b3510-129">Then go too**All applications**.</span></span>

    ![Blok aplikacje przedsiębiorstwa Hello][2]
    
3. <span data-ttu-id="b3510-131">tooadd nową aplikację, kliknij przycisk **nowej aplikacji** przycisk u góry hello okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="b3510-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Nowy przycisk aplikacji Hello][3]

4. <span data-ttu-id="b3510-133">W polu wyszukiwania hello wpisz **Workrite**, wybierz pozycję **Workrite** z panelu wyników następnie kliknij przycisk **Dodaj** przycisk aplikacji hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="b3510-133">In hello search box, type **Workrite**, select **Workrite** from result panel then click **Add** button tooadd hello application.</span></span>

    ![Workrite hello listy wyników](./media/active-directory-saas-workrite-tutorial/tutorial_workrite_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="b3510-135">Konfiguracja i testowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="b3510-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="b3510-136">W tej sekcji skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z Workrite w oparciu o nazwie "Britta Simona" użytkownika testowego.</span><span class="sxs-lookup"><span data-stu-id="b3510-136">In this section, you configure and test Azure AD single sign-on with Workrite based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="b3510-137">Dla pojedynczego logowania jednokrotnego toowork usługi Azure AD musi tooknow użytkownika odpowiednikiem hello w Workrite jest tooa użytkownika w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="b3510-137">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Workrite is tooa user in Azure AD.</span></span> <span data-ttu-id="b3510-138">Innymi słowy relację łącza między użytkownika usługi Azure AD i hello użytkownikowi w Workrite musi toobe ustanowione.</span><span class="sxs-lookup"><span data-stu-id="b3510-138">In other words, a link relationship between an Azure AD user and hello related user in Workrite needs toobe established.</span></span>

<span data-ttu-id="b3510-139">W Workrite, należy przypisać wartość hello hello **nazwy użytkownika** w usłudze Azure AD jako wartość hello hello **Username** tooestablish hello łącze relacji.</span><span class="sxs-lookup"><span data-stu-id="b3510-139">In Workrite, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="b3510-140">tooconfigure i testowych usługi Azure AD rejestracji jednokrotnej z Workrite, należy po bloków konstrukcyjnych hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="b3510-140">tooconfigure and test Azure AD single sign-on with Workrite, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="b3510-141">**[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configure-azure-ad-single-sign-on)**  -tooenable Twojego toouse użytkowników tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="b3510-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="b3510-142">**[Tworzenie użytkownika testowego usługi Azure AD](#create-an-azure-ad-test-user)**  -tootest usługi Azure AD rejestracji jednokrotnej z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="b3510-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="b3510-143">**[Tworzenie użytkownika testowego Workrite](#create-a-workrite-test-user)**  -toohave odpowiednikiem Simona Britta w Workrite, który jest połączony toohello usługi Azure AD reprezentację użytkownika.</span><span class="sxs-lookup"><span data-stu-id="b3510-143">**[Create a Workrite test user](#create-a-workrite-test-user)** - toohave a counterpart of Britta Simon in Workrite that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="b3510-144">**[Przypisz użytkownika testowego hello Azure AD](#assign-the-azure-ad-test-user)**  -tooenable Simona Britta toouse usługi Azure AD rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="b3510-144">**[Assign hello Azure AD test user](#assign-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="b3510-145">**[Test rejestracji jednokrotnej](#test-single-sign-on)**  -tooverify czy hello konfiguracji działania.</span><span class="sxs-lookup"><span data-stu-id="b3510-145">**[Test single sign-on](#test-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="b3510-146">Konfigurowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="b3510-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="b3510-147">W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w portalu Azure hello i skonfigurować logowanie jednokrotne w aplikacji Workrite.</span><span class="sxs-lookup"><span data-stu-id="b3510-147">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Workrite application.</span></span>

<span data-ttu-id="b3510-148">**tooconfigure usługi Azure AD rejestracji jednokrotnej z Workrite, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="b3510-148">**tooconfigure Azure AD single sign-on with Workrite, perform hello following steps:**</span></span>

1. <span data-ttu-id="b3510-149">W portalu Azure na powitania hello **Workrite** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.</span><span class="sxs-lookup"><span data-stu-id="b3510-149">In hello Azure portal, on hello **Workrite** application integration page, click **Single sign-on**.</span></span>

    ![Skonfigurować łącze rejestracji jednokrotnej][4]

2. <span data-ttu-id="b3510-151">Na powitania **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** tooenable rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="b3510-151">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Okno dialogowe rejestracji jednokrotnej](./media/active-directory-saas-workrite-tutorial/tutorial_workrite_samlbase.png)

3. <span data-ttu-id="b3510-153">Na powitania **Workrite domeny i adres URL** sekcji, wykonaj następujące kroki hello:</span><span class="sxs-lookup"><span data-stu-id="b3510-153">On hello **Workrite Domain and URLs** section, perform hello following steps:</span></span>

    ![Adresy URL i domeny Workrite pojedynczy informacje logowania jednokrotnego](./media/active-directory-saas-workrite-tutorial/tutorial_workrite_url.png)

    <span data-ttu-id="b3510-155">W hello **adres URL logowania** tekstowym, wpisz adres URL za pomocą hello następującego wzorca:`https://app.workrite.co.uk/securelogin/samlgateway.aspx?id=<uniqueid>`</span><span class="sxs-lookup"><span data-stu-id="b3510-155">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://app.workrite.co.uk/securelogin/samlgateway.aspx?id=<uniqueid>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="b3510-156">Ta wartość nie jest prawdziwe.</span><span class="sxs-lookup"><span data-stu-id="b3510-156">This value is not real.</span></span> <span data-ttu-id="b3510-157">Zaktualizuj tę wartość z hello rzeczywisty adres URL logowania.</span><span class="sxs-lookup"><span data-stu-id="b3510-157">Update this value with hello actual Sign-On URL.</span></span> <span data-ttu-id="b3510-158">Skontaktuj się z [zespołem pomocy technicznej klienta Workrite](mailto:support@workrite.co.uk) tooget tej wartości.</span><span class="sxs-lookup"><span data-stu-id="b3510-158">Contact [Workrite Client support team](mailto:support@workrite.co.uk) tooget this value.</span></span>

4. <span data-ttu-id="b3510-159">Na powitania **certyfikat podpisywania SAML** kliknij **Certificate(Base64)** , a następnie zapisz plik certyfikatu hello na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="b3510-159">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![link do pobierania certyfikatu Hello](./media/active-directory-saas-workrite-tutorial/tutorial_workrite_certificate.png) 

5. <span data-ttu-id="b3510-161">Kliknij przycisk **zapisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="b3510-161">Click **Save** button.</span></span>

    ![Skonfiguruj przycisk pojedynczego logowania jednokrotnego Zapisz](./media/active-directory-saas-workrite-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="b3510-163">Na powitania **konfiguracji Workrite** kliknij **skonfigurować Workrite** tooopen **Konfigurowanie logowania jednokrotnego** okna.</span><span class="sxs-lookup"><span data-stu-id="b3510-163">On hello **Workrite Configuration** section, click **Configure Workrite** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="b3510-164">Kopiuj hello **Sign-Out adres URL, identyfikator jednostki SAML i SAML pojedynczy znak na adres URL usługi** z hello **sekcji krótkimi opisami.**</span><span class="sxs-lookup"><span data-stu-id="b3510-164">Copy hello **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Konfiguracja Workrite](./media/active-directory-saas-workrite-tutorial/tutorial_workrite_configure.png) 

7. <span data-ttu-id="b3510-166">tooconfigure rejestracji jednokrotnej w **Workrite** strony, należy pobrać hello toosend **Certificate(Base64), adres URL Sign-Out, identyfikator jednostki SAML i SAML pojedynczy znak na adres URL usługi** zbyt[Workrite obsługuje zespołu](mailto:support@workrite.co.uk).</span><span class="sxs-lookup"><span data-stu-id="b3510-166">tooconfigure single sign-on on **Workrite** side, you need toosend hello downloaded **Certificate(Base64), Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** too[Workrite support team](mailto:support@workrite.co.uk).</span></span>

> [!TIP]
> <span data-ttu-id="b3510-167">Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz hello [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji hello!</span><span class="sxs-lookup"><span data-stu-id="b3510-167">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="b3510-168">Po dodaniu tej aplikacji z hello **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij hello **rejestracji jednokrotnej** hello kartę i dostępu do osadzonych dokumentacji za pośrednictwem hello  **Konfiguracja** sekcji u dołu hello.</span><span class="sxs-lookup"><span data-stu-id="b3510-168">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="b3510-169">Więcej o hello osadzonych dokumentacji funkcji w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="b3510-169">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="b3510-170">Tworzenie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="b3510-170">Create an Azure AD test user</span></span>

<span data-ttu-id="b3510-171">Celem Hello w tej sekcji jest toocreate użytkownika testowego, w portalu Azure o nazwie Simona Britta hello.</span><span class="sxs-lookup"><span data-stu-id="b3510-171">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

   ![Tworzenie użytkownika testowego usługi Azure AD][100]

<span data-ttu-id="b3510-173">**toocreate użytkownika testowego w usłudze Azure AD, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="b3510-173">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="b3510-174">W portalu Azure, w okienku po lewej stronie powitania hello kliknij hello **usługi Azure Active Directory** przycisku.</span><span class="sxs-lookup"><span data-stu-id="b3510-174">In hello Azure portal, in hello left pane, click hello **Azure Active Directory** button.</span></span>

    ![przycisk usługi Azure Active Directory Hello](./media/active-directory-saas-workrite-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="b3510-176">toodisplay hello listę użytkowników, przejdź zbyt**użytkowników i grup**, a następnie kliknij przycisk **wszyscy użytkownicy**.</span><span class="sxs-lookup"><span data-stu-id="b3510-176">toodisplay hello list of users, go too**Users and groups**, and then click **All users**.</span></span>

    ![Witaj, "Użytkownicy i grupy" i "Wszyscy użytkownicy" łącza](./media/active-directory-saas-workrite-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="b3510-178">Witaj tooopen **użytkownika** okno dialogowe, kliknij przycisk **Dodaj** u góry hello hello **wszyscy użytkownicy** okno dialogowe.</span><span class="sxs-lookup"><span data-stu-id="b3510-178">tooopen hello **User** dialog box, click **Add** at hello top of hello **All Users** dialog box.</span></span>

    ![przycisk Dodaj Hello](./media/active-directory-saas-workrite-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="b3510-180">W hello **użytkownika** okna dialogowego wykonaj hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="b3510-180">In hello **User** dialog box, perform hello following steps:</span></span>

    ![okno dialogowe Hello użytkownika](./media/active-directory-saas-workrite-tutorial/create_aaduser_04.png)

    <span data-ttu-id="b3510-182">a.</span><span class="sxs-lookup"><span data-stu-id="b3510-182">a.</span></span> <span data-ttu-id="b3510-183">W hello **nazwa** wpisz **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="b3510-183">In hello **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="b3510-184">b.</span><span class="sxs-lookup"><span data-stu-id="b3510-184">b.</span></span> <span data-ttu-id="b3510-185">W hello **nazwy użytkownika** pole typu hello adres e-mail użytkownika Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="b3510-185">In hello **User name** box, type hello email address of user Britta Simon.</span></span>

    <span data-ttu-id="b3510-186">c.</span><span class="sxs-lookup"><span data-stu-id="b3510-186">c.</span></span> <span data-ttu-id="b3510-187">Wybierz hello **Pokaż hasło** pole wyboru, a następnie zapisz hello wartość, która jest wyświetlana w hello **hasło** pole.</span><span class="sxs-lookup"><span data-stu-id="b3510-187">Select hello **Show Password** check box, and then write down hello value that's displayed in hello **Password** box.</span></span>

    <span data-ttu-id="b3510-188">d.</span><span class="sxs-lookup"><span data-stu-id="b3510-188">d.</span></span> <span data-ttu-id="b3510-189">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="b3510-189">Click **Create**.</span></span>
 
### <a name="create-a-workrite-test-user"></a><span data-ttu-id="b3510-190">Tworzenie użytkownika testowego Workrite</span><span class="sxs-lookup"><span data-stu-id="b3510-190">Create a Workrite test user</span></span>

<span data-ttu-id="b3510-191">Celem Hello w tej sekcji jest toocreate użytkownika o nazwie Simona Britta w Workrite.</span><span class="sxs-lookup"><span data-stu-id="b3510-191">hello objective of this section is toocreate a user called Britta Simon in Workrite.</span></span>

<span data-ttu-id="b3510-192">**toocreate użytkownika o nazwie Simona Britta w Workrite, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="b3510-192">**toocreate a user called Britta Simon in Workrite, perform hello following steps:**</span></span>

1. <span data-ttu-id="b3510-193">Zaloguj się w witrynie firmy workrite tooyour jako administrator.</span><span class="sxs-lookup"><span data-stu-id="b3510-193">Sign on tooyour workrite company site as administrator.</span></span>

2. <span data-ttu-id="b3510-194">W okienku nawigacji powitania kliknij **Admin**.</span><span class="sxs-lookup"><span data-stu-id="b3510-194">In hello navigation pane, click **Admin**.</span></span>
   
    ![Administratorowi kontrolowanie][400]

3. <span data-ttu-id="b3510-196">Przejdź tooQuick łącza, a następnie kliknij przycisk **utworzyć użytkownika**.</span><span class="sxs-lookup"><span data-stu-id="b3510-196">Go tooQuick Links, and then click **Create a User**.</span></span>
   
    ![Utwórz użytkownika][401]

4. <span data-ttu-id="b3510-198">Na powitania **Tworzenie użytkownika** okna dialogowego, wykonaj następujące kroki hello:</span><span class="sxs-lookup"><span data-stu-id="b3510-198">On hello **Create User** dialog, perform hello following steps:</span></span>
   
    ![Utwórz Dailog użytkownika][402]
    
    <span data-ttu-id="b3510-200">a.</span><span class="sxs-lookup"><span data-stu-id="b3510-200">a.</span></span> <span data-ttu-id="b3510-201">W hello **E-mail** pole tekstowe, typ hello adres e-mail użytkownika, takich jak Brittasimon@contoso.com.</span><span class="sxs-lookup"><span data-stu-id="b3510-201">In hello **Email** textbox, type hello email address of user like Brittasimon@contoso.com.</span></span>

    <span data-ttu-id="b3510-202">b.</span><span class="sxs-lookup"><span data-stu-id="b3510-202">b.</span></span> <span data-ttu-id="b3510-203">W hello **imię** pole tekstowe, typ hello imię użytkownika, takich jak Britta.</span><span class="sxs-lookup"><span data-stu-id="b3510-203">In hello **First Name** textbox, type hello firstname of user like Britta.</span></span>

    <span data-ttu-id="b3510-204">c.</span><span class="sxs-lookup"><span data-stu-id="b3510-204">c.</span></span> <span data-ttu-id="b3510-205">W hello **nazwisko** pole tekstowe, typ hello nazwisko użytkownika, takich jak Simona.</span><span class="sxs-lookup"><span data-stu-id="b3510-205">In hello **Surname** textbox, type hello surname of user like Simon.</span></span>
    
    <span data-ttu-id="b3510-206">d.</span><span class="sxs-lookup"><span data-stu-id="b3510-206">d.</span></span> <span data-ttu-id="b3510-207">Wybierz **Administrator klienta** jako **wybierz rolę**.</span><span class="sxs-lookup"><span data-stu-id="b3510-207">Select **Client Administrator** as **Choose Role**.</span></span>
    
    <span data-ttu-id="b3510-208">e.</span><span class="sxs-lookup"><span data-stu-id="b3510-208">e.</span></span> <span data-ttu-id="b3510-209">Kliknij pozycję **Zapisz**.</span><span class="sxs-lookup"><span data-stu-id="b3510-209">Click **Save**.</span></span>   

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="b3510-210">Przypisz użytkownika testowego hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="b3510-210">Assign hello Azure AD test user</span></span>

<span data-ttu-id="b3510-211">W tej sekcji możesz włączyć toouse Simona Britta Azure logowania jednokrotnego za udzielanie dostępu tooWorkrite.</span><span class="sxs-lookup"><span data-stu-id="b3510-211">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooWorkrite.</span></span>

![Przypisanie roli użytkownika hello][200] 

<span data-ttu-id="b3510-213">**tooassign tooWorkrite Simona Britta wykonaj hello następujące kroki:**</span><span class="sxs-lookup"><span data-stu-id="b3510-213">**tooassign Britta Simon tooWorkrite, perform hello following steps:**</span></span>

1. <span data-ttu-id="b3510-214">W portalu Azure hello, otwórz widok aplikacji hello, a następnie przejdź do widoku katalogu toohello i przejść za**aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="b3510-214">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Przypisz użytkownika][201] 

2. <span data-ttu-id="b3510-216">Z listy aplikacji hello wybierz **Workrite**.</span><span class="sxs-lookup"><span data-stu-id="b3510-216">In hello applications list, select **Workrite**.</span></span>

    ![łącze Workrite Hello na liście aplikacji hello](./media/active-directory-saas-workrite-tutorial/tutorial_workrite_app.png)  

3. <span data-ttu-id="b3510-218">W menu powitania po lewej stronie powitania kliknij **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="b3510-218">In hello menu on hello left, click **Users and groups**.</span></span>

    ![łącze "Użytkownicy i grupy" Hello][202]

4. <span data-ttu-id="b3510-220">Kliknij przycisk **Dodaj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="b3510-220">Click **Add** button.</span></span> <span data-ttu-id="b3510-221">Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="b3510-221">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Okienko Dodaj przypisania Hello][203]

5. <span data-ttu-id="b3510-223">Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** hello listy użytkowników.</span><span class="sxs-lookup"><span data-stu-id="b3510-223">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="b3510-224">Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="b3510-224">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="b3510-225">Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="b3510-225">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="b3510-226">Test rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="b3510-226">Test single sign-on</span></span>

<span data-ttu-id="b3510-227">Celem Hello w tej sekcji jest tootest programu Azure AD SSO konfiguracji przy użyciu hello panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="b3510-227">hello objective of this section is tootest your Azure AD SSO configuration using hello Access Panel.</span></span>

<span data-ttu-id="b3510-228">Po kliknięciu kafelka Workrite hello w hello Panel dostępu, należy pobrać automatycznie zalogowane tooyour Workrite aplikacji.</span><span class="sxs-lookup"><span data-stu-id="b3510-228">When you click hello Workrite tile in hello Access Panel, you should get automatically signed-on tooyour Workrite application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="b3510-229">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="b3510-229">Additional resources</span></span>

* [<span data-ttu-id="b3510-230">Lista samouczków dotyczących tooIntegrate aplikacji SaaS w usłudze Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="b3510-230">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="b3510-231">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="b3510-231">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-workrite-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-workrite-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-workrite-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-workrite-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-workrite-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-workrite-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-workrite-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-workrite-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-workrite-tutorial/tutorial_general_203.png
[400]: ./media/active-directory-saas-workrite-tutorial/tutorial_workrite_400.png
[401]: ./media/active-directory-saas-workrite-tutorial/tutorial_workrite_401.png
[402]: ./media/active-directory-saas-workrite-tutorial/tutorial_workrite_402.png

