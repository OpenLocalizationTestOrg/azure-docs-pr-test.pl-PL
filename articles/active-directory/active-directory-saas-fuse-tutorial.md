---
title: 'Samouczek: Integracji Azure Active Directory z bezpiecznik | Dokumentacja firmy Microsoft'
description: "Dowiedz się, jak tooconfigure logowanie jednokrotne między usługą Azure Active Directory i bezpiecznik."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 5ef34f58-863a-4b37-875c-e8efa3e18bb3
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/27/2017
ms.author: jeedes
ms.openlocfilehash: 720ed8af0b5de1e3bee5a40353ca0ee661766864
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-fuse"></a><span data-ttu-id="89e72-103">Samouczek: Integracji Azure Active Directory z bezpiecznik</span><span class="sxs-lookup"><span data-stu-id="89e72-103">Tutorial: Azure Active Directory integration with Fuse</span></span>

<span data-ttu-id="89e72-104">Z tego samouczka, dowiesz się, jak toointegrate łączenie z usługą Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="89e72-104">In this tutorial, you learn how toointegrate Fuse with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="89e72-105">Integracja z usługą Azure AD bezpiecznik zapewnia hello następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="89e72-105">Integrating Fuse with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="89e72-106">Można kontrolować w usłudze Azure AD, kto ma dostęp do tooFuse.</span><span class="sxs-lookup"><span data-stu-id="89e72-106">You can control in Azure AD who has access tooFuse.</span></span>
- <span data-ttu-id="89e72-107">Można włączyć użytkownika użytkownicy tooautomatically get zalogowane tooFuse (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="89e72-107">You can enable your users tooautomatically get signed-on tooFuse (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="89e72-108">Możesz zarządzać kont w jednej centralnej lokalizacji - hello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="89e72-108">You can manage your accounts in one central location - hello Azure portal.</span></span>

<span data-ttu-id="89e72-109">Jeśli chcesz tooknow więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="89e72-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="89e72-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="89e72-110">Prerequisites</span></span>

<span data-ttu-id="89e72-111">Integracja tooconfigure usługi Azure AD z bezpiecznik, należy hello następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="89e72-111">tooconfigure Azure AD integration with Fuse, you need hello following items:</span></span>

- <span data-ttu-id="89e72-112">Subskrypcję usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="89e72-112">An Azure AD subscription</span></span>
- <span data-ttu-id="89e72-113">Bezpiecznik logowanie jednokrotne włączone subskrypcji</span><span class="sxs-lookup"><span data-stu-id="89e72-113">A Fuse single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="89e72-114">tootest hello kroków w tym samouczku, zaleca się przy użyciu środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="89e72-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="89e72-115">tootest hello kroki opisane w tym samouczku, należy stosować te zalecenia:</span><span class="sxs-lookup"><span data-stu-id="89e72-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="89e72-116">Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="89e72-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="89e72-117">Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz [uzyskać miesięczna wersja próbna](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="89e72-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="89e72-118">Opis scenariusza</span><span class="sxs-lookup"><span data-stu-id="89e72-118">Scenario description</span></span>
<span data-ttu-id="89e72-119">W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym.</span><span class="sxs-lookup"><span data-stu-id="89e72-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="89e72-120">Scenariusz Hello opisane w tym samouczku składa się z dwóch głównych elementów:</span><span class="sxs-lookup"><span data-stu-id="89e72-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="89e72-121">Dodaj bezpiecznik z galerii hello</span><span class="sxs-lookup"><span data-stu-id="89e72-121">Add Fuse from hello gallery</span></span>
2. <span data-ttu-id="89e72-122">Konfiguracja i testowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="89e72-122">Configure and test Azure AD single sign-on</span></span>

## <a name="add-fuse-from-hello-gallery"></a><span data-ttu-id="89e72-123">Dodaj bezpiecznik z galerii hello</span><span class="sxs-lookup"><span data-stu-id="89e72-123">Add Fuse from hello gallery</span></span>
<span data-ttu-id="89e72-124">tooconfigure hello integracja bezpieczników programu Azure AD, należy tooadd bezpiecznik z hello galerii tooyour listę zarządzanych aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="89e72-124">tooconfigure hello integration of Fuse into Azure AD, you need tooadd Fuse from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="89e72-125">**tooadd bezpiecznik z galerii hello wykonaj hello następujące kroki:**</span><span class="sxs-lookup"><span data-stu-id="89e72-125">**tooadd Fuse from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="89e72-126">W hello  **[portalu Azure](https://portal.azure.com)**na temat hello panelu nawigacji po lewej stronie, kliknij przycisk **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="89e72-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![przycisk usługi Azure Active Directory Hello][1]

2. <span data-ttu-id="89e72-128">Przejdź za**aplikacje dla przedsiębiorstw**.</span><span class="sxs-lookup"><span data-stu-id="89e72-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="89e72-129">Następnie przejdź zbyt**wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="89e72-129">Then go too**All applications**.</span></span>

    ![Blok aplikacje przedsiębiorstwa Hello][2]
    
3. <span data-ttu-id="89e72-131">tooadd nową aplikację, kliknij przycisk **nowej aplikacji** przycisk u góry hello okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="89e72-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Nowy przycisk aplikacji Hello][3]

4. <span data-ttu-id="89e72-133">W polu wyszukiwania hello wpisz **łączenie**, wybierz pozycję **łączenie** z panelu wyników następnie kliknij przycisk **Dodaj** przycisk aplikacji hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="89e72-133">In hello search box, type **Fuse**, select **Fuse** from result panel then click **Add** button tooadd hello application.</span></span>

    ![Łączenie hello listy wyników](./media/active-directory-saas-fuse-tutorial/tutorial_fuse_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="89e72-135">Konfiguracja i testowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="89e72-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="89e72-136">W tej sekcji skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z bezpiecznik w oparciu o nazwie "Britta Simona" użytkownika testowego.</span><span class="sxs-lookup"><span data-stu-id="89e72-136">In this section, you configure and test Azure AD single sign-on with Fuse based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="89e72-137">Dla pojedynczego logowania jednokrotnego toowork usługi Azure AD musi tooknow użytkownika odpowiednikiem hello w bezpiecznik jest tooa użytkownika w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="89e72-137">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Fuse is tooa user in Azure AD.</span></span> <span data-ttu-id="89e72-138">Innymi słowy link relację między użytkownika usługi Azure AD i hello użytkownikowi w toobe potrzeb bezpiecznik ustanowione.</span><span class="sxs-lookup"><span data-stu-id="89e72-138">In other words, a link relationship between an Azure AD user and hello related user in Fuse needs toobe established.</span></span>

<span data-ttu-id="89e72-139">W bezpiecznik, należy przypisać wartość hello hello **nazwy użytkownika** w usłudze Azure AD jako wartość hello hello **Username** tooestablish hello łącze relacji.</span><span class="sxs-lookup"><span data-stu-id="89e72-139">In Fuse, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="89e72-140">tooconfigure i test usługi Azure AD rejestracji jednokrotnej z bezpiecznik należy hello toocomplete po bloków konstrukcyjnych:</span><span class="sxs-lookup"><span data-stu-id="89e72-140">tooconfigure and test Azure AD single sign-on with Fuse, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="89e72-141">**[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configure-azure-ad-single-sign-on)**  -tooenable Twojego toouse użytkowników tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="89e72-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="89e72-142">**[Tworzenie użytkownika testowego usługi Azure AD](#create-an-azure-ad-test-user)**  -tootest usługi Azure AD rejestracji jednokrotnej z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="89e72-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="89e72-143">**[Tworzenie użytkownika testowego bezpiecznik](#create-a-fuse-test-user)**  -toohave odpowiednikiem Simona Britta w bezpiecznik, który jest połączony toohello usługi Azure AD reprezentację użytkownika.</span><span class="sxs-lookup"><span data-stu-id="89e72-143">**[Create a Fuse test user](#create-a-fuse-test-user)** - toohave a counterpart of Britta Simon in Fuse that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="89e72-144">**[Przypisz użytkownika testowego hello Azure AD](#assign-the-azure-ad-test-user)**  -tooenable Simona Britta toouse usługi Azure AD rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="89e72-144">**[Assign hello Azure AD test user](#assign-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="89e72-145">**[Test rejestracji jednokrotnej](#test-single-sign-on)**  -tooverify czy hello konfiguracji działania.</span><span class="sxs-lookup"><span data-stu-id="89e72-145">**[Test single sign-on](#test-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="89e72-146">Konfigurowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="89e72-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="89e72-147">W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w hello portalu Azure i skonfigurować logowanie jednokrotne w aplikacji bezpiecznik.</span><span class="sxs-lookup"><span data-stu-id="89e72-147">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Fuse application.</span></span>

<span data-ttu-id="89e72-148">**tooconfigure usługi Azure AD rejestracji jednokrotnej z bezpiecznik, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="89e72-148">**tooconfigure Azure AD single sign-on with Fuse, perform hello following steps:**</span></span>

1. <span data-ttu-id="89e72-149">W portalu Azure na powitania hello **łączenie** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.</span><span class="sxs-lookup"><span data-stu-id="89e72-149">In hello Azure portal, on hello **Fuse** application integration page, click **Single sign-on**.</span></span>

    ![Skonfigurować łącze rejestracji jednokrotnej][4]

2. <span data-ttu-id="89e72-151">Na powitania **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** tooenable rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="89e72-151">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Okno dialogowe rejestracji jednokrotnej](./media/active-directory-saas-fuse-tutorial/tutorial_fuse_samlbase.png)

3. <span data-ttu-id="89e72-153">Na powitania **adresy URL i łączenie domeny** sekcji, wykonaj następujące kroki hello:</span><span class="sxs-lookup"><span data-stu-id="89e72-153">On hello **Fuse Domain and URLs** section, perform hello following steps:</span></span>

    ![Łączenie domeny i adres URL pojedynczego logowania jednokrotnego informacji](./media/active-directory-saas-fuse-tutorial/tutorial_fuse_url.png)
    
    <span data-ttu-id="89e72-155">W hello **adres URL logowania** tekstowym, wpisz adres URL za pomocą hello następującego wzorca:`https://<tenant name>.fusion-universal.com/`</span><span class="sxs-lookup"><span data-stu-id="89e72-155">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<tenant name>.fusion-universal.com/`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="89e72-156">Ta wartość nie jest prawdziwe.</span><span class="sxs-lookup"><span data-stu-id="89e72-156">This value is not real.</span></span> <span data-ttu-id="89e72-157">Zaktualizuj tę wartość z hello rzeczywisty adres URL logowania.</span><span class="sxs-lookup"><span data-stu-id="89e72-157">Update this value with hello actual Sign-On URL.</span></span> <span data-ttu-id="89e72-158">Skontaktuj się z [zespołem pomocy technicznej klienta łączenie](mailto:support@fusion-universal.com) tooget tej wartości.</span><span class="sxs-lookup"><span data-stu-id="89e72-158">Contact [Fuse Client support team](mailto:support@fusion-universal.com) tooget this value.</span></span> 
 
4. <span data-ttu-id="89e72-159">Na powitania **certyfikat podpisywania SAML** kliknij **certyfikatu (Raw)** , a następnie zapisz plik certyfikatu hello na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="89e72-159">On hello **SAML Signing Certificate** section, click **Certificate (Raw)** and then save hello certificate file on your computer.</span></span>

    ![link do pobierania certyfikatu Hello](./media/active-directory-saas-fuse-tutorial/tutorial_fuse_certificate.png) 

5. <span data-ttu-id="89e72-161">Kliknij przycisk **zapisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="89e72-161">Click **Save** button.</span></span>

    ![Skonfiguruj przycisk pojedynczego logowania jednokrotnego Zapisz](./media/active-directory-saas-fuse-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="89e72-163">Na powitania **łączenie konfiguracji** kliknij **skonfigurować łączenie** tooopen **Konfigurowanie logowania jednokrotnego** okna.</span><span class="sxs-lookup"><span data-stu-id="89e72-163">On hello **Fuse Configuration** section, click **Configure Fuse** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="89e72-164">Kopiuj hello **Sign-Out adres URL, identyfikator jednostki SAML i SAML pojedynczy znak na adres URL usługi** z hello **sekcji krótkimi opisami.**</span><span class="sxs-lookup"><span data-stu-id="89e72-164">Copy hello **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Łączenie konfiguracji](./media/active-directory-saas-fuse-tutorial/tutorial_fuse_configure.png) 

7. <span data-ttu-id="89e72-166">tooget logowania jednokrotnego skonfigurowane dla aplikacji, skontaktuj się z [zespołem pomocy technicznej bezpiecznik](mailto:support@fusion-universal.com) i podaj następujący hello:</span><span class="sxs-lookup"><span data-stu-id="89e72-166">tooget SSO configured for your application, contact [Fuse support team](mailto:support@fusion-universal.com) and provide them with hello following:</span></span>

    * <span data-ttu-id="89e72-167">Witaj pobrane **plik certyfikatu (Raw)**</span><span class="sxs-lookup"><span data-stu-id="89e72-167">hello downloaded **Certificate (Raw) file**</span></span>
    * <span data-ttu-id="89e72-168">Witaj **SAML pojedynczy znak na adres URL usługi**</span><span class="sxs-lookup"><span data-stu-id="89e72-168">hello **SAML Single Sign-On Service URL**</span></span>
    * <span data-ttu-id="89e72-169">Witaj **identyfikator jednostki SAML**</span><span class="sxs-lookup"><span data-stu-id="89e72-169">hello **SAML Entity ID**</span></span>
    * <span data-ttu-id="89e72-170">Witaj **Sign-Out adresu URL**</span><span class="sxs-lookup"><span data-stu-id="89e72-170">hello **Sign-Out URL**</span></span>

> [!TIP]
> <span data-ttu-id="89e72-171">Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz hello [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji hello!</span><span class="sxs-lookup"><span data-stu-id="89e72-171">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="89e72-172">Po dodaniu tej aplikacji z hello **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij hello **rejestracji jednokrotnej** hello kartę i dostępu do osadzonych dokumentacji za pośrednictwem hello  **Konfiguracja** sekcji u dołu hello.</span><span class="sxs-lookup"><span data-stu-id="89e72-172">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="89e72-173">Więcej o hello osadzonych dokumentacji funkcji w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="89e72-173">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="89e72-174">Tworzenie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="89e72-174">Create an Azure AD test user</span></span>

<span data-ttu-id="89e72-175">Celem Hello w tej sekcji jest toocreate użytkownika testowego, w portalu Azure o nazwie Simona Britta hello.</span><span class="sxs-lookup"><span data-stu-id="89e72-175">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

   ![Tworzenie użytkownika testowego usługi Azure AD][100]

<span data-ttu-id="89e72-177">**toocreate użytkownika testowego w usłudze Azure AD, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="89e72-177">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="89e72-178">W portalu Azure, w okienku po lewej stronie powitania hello kliknij hello **usługi Azure Active Directory** przycisku.</span><span class="sxs-lookup"><span data-stu-id="89e72-178">In hello Azure portal, in hello left pane, click hello **Azure Active Directory** button.</span></span>

    ![przycisk usługi Azure Active Directory Hello](./media/active-directory-saas-fuse-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="89e72-180">toodisplay hello listę użytkowników, przejdź zbyt**użytkowników i grup**, a następnie kliknij przycisk **wszyscy użytkownicy**.</span><span class="sxs-lookup"><span data-stu-id="89e72-180">toodisplay hello list of users, go too**Users and groups**, and then click **All users**.</span></span>

    ![Witaj, "Użytkownicy i grupy" i "Wszyscy użytkownicy" łącza](./media/active-directory-saas-fuse-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="89e72-182">Witaj tooopen **użytkownika** okno dialogowe, kliknij przycisk **Dodaj** u góry hello hello **wszyscy użytkownicy** okno dialogowe.</span><span class="sxs-lookup"><span data-stu-id="89e72-182">tooopen hello **User** dialog box, click **Add** at hello top of hello **All Users** dialog box.</span></span>

    ![przycisk Dodaj Hello](./media/active-directory-saas-fuse-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="89e72-184">W hello **użytkownika** okna dialogowego wykonaj hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="89e72-184">In hello **User** dialog box, perform hello following steps:</span></span>

    ![okno dialogowe Hello użytkownika](./media/active-directory-saas-fuse-tutorial/create_aaduser_04.png)

    <span data-ttu-id="89e72-186">a.</span><span class="sxs-lookup"><span data-stu-id="89e72-186">a.</span></span> <span data-ttu-id="89e72-187">W hello **nazwa** wpisz **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="89e72-187">In hello **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="89e72-188">b.</span><span class="sxs-lookup"><span data-stu-id="89e72-188">b.</span></span> <span data-ttu-id="89e72-189">W hello **nazwy użytkownika** pole typu hello adres e-mail użytkownika Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="89e72-189">In hello **User name** box, type hello email address of user Britta Simon.</span></span>

    <span data-ttu-id="89e72-190">c.</span><span class="sxs-lookup"><span data-stu-id="89e72-190">c.</span></span> <span data-ttu-id="89e72-191">Wybierz hello **Pokaż hasło** pole wyboru, a następnie zapisz hello wartość, która jest wyświetlana w hello **hasło** pole.</span><span class="sxs-lookup"><span data-stu-id="89e72-191">Select hello **Show Password** check box, and then write down hello value that's displayed in hello **Password** box.</span></span>

    <span data-ttu-id="89e72-192">d.</span><span class="sxs-lookup"><span data-stu-id="89e72-192">d.</span></span> <span data-ttu-id="89e72-193">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="89e72-193">Click **Create**.</span></span>
 
### <a name="create-a-fuse-test-user"></a><span data-ttu-id="89e72-194">Tworzenie użytkownika testowego bezpiecznik</span><span class="sxs-lookup"><span data-stu-id="89e72-194">Create a Fuse test user</span></span>

<span data-ttu-id="89e72-195">W tej sekcji należy utworzyć użytkownika o nazwie Simona Britta w bezpiecznik.</span><span class="sxs-lookup"><span data-stu-id="89e72-195">In this section, you create a user called Britta Simon in Fuse.</span></span> <span data-ttu-id="89e72-196">We współpracy z [zespołem pomocy technicznej bezpiecznik](mailto:support@fusion-universal.com) użytkowników hello tooadd hello bezpiecznik platformy.</span><span class="sxs-lookup"><span data-stu-id="89e72-196">Please work with [Fuse support team](mailto:support@fusion-universal.com) tooadd hello users in hello Fuse platform.</span></span>


### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="89e72-197">Przypisz użytkownika testowego hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="89e72-197">Assign hello Azure AD test user</span></span>

<span data-ttu-id="89e72-198">W tej sekcji możesz włączyć toouse Simona Britta Azure logowania jednokrotnego za udzielanie dostępu tooFuse.</span><span class="sxs-lookup"><span data-stu-id="89e72-198">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooFuse.</span></span>

![Przypisanie roli użytkownika hello][200] 

<span data-ttu-id="89e72-200">**tooassign tooFuse Simona Britta wykonaj hello następujące kroki:**</span><span class="sxs-lookup"><span data-stu-id="89e72-200">**tooassign Britta Simon tooFuse, perform hello following steps:**</span></span>

1. <span data-ttu-id="89e72-201">W portalu Azure hello, otwórz widok aplikacji hello, a następnie przejdź do widoku katalogu toohello i przejść za**aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="89e72-201">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Przypisz użytkownika][201] 

2. <span data-ttu-id="89e72-203">Z listy aplikacji hello wybierz **łączenie**.</span><span class="sxs-lookup"><span data-stu-id="89e72-203">In hello applications list, select **Fuse**.</span></span>

    ![łącze bezpiecznik Hello na liście aplikacji hello](./media/active-directory-saas-fuse-tutorial/tutorial_fuse_app.png)  

3. <span data-ttu-id="89e72-205">W menu powitania po lewej stronie powitania kliknij **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="89e72-205">In hello menu on hello left, click **Users and groups**.</span></span>

    ![łącze "Użytkownicy i grupy" Hello][202]

4. <span data-ttu-id="89e72-207">Kliknij przycisk **Dodaj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="89e72-207">Click **Add** button.</span></span> <span data-ttu-id="89e72-208">Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="89e72-208">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Okienko Dodaj przypisania Hello][203]

5. <span data-ttu-id="89e72-210">Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** hello listy użytkowników.</span><span class="sxs-lookup"><span data-stu-id="89e72-210">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="89e72-211">Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="89e72-211">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="89e72-212">Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="89e72-212">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="89e72-213">Test rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="89e72-213">Test single sign-on</span></span>

<span data-ttu-id="89e72-214">W tej sekcji można przetestować konfiguracji usługi Azure AD pojedynczego logowania jednokrotnego przy użyciu hello panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="89e72-214">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="89e72-215">Po kliknięciu kafelka bezpiecznik hello w hello Panel dostępu, należy pobrać automatycznie zalogowane tooyour bezpiecznik aplikacji.</span><span class="sxs-lookup"><span data-stu-id="89e72-215">When you click hello Fuse tile in hello Access Panel, you should get automatically signed-on tooyour Fuse application.</span></span>
<span data-ttu-id="89e72-216">Aby uzyskać więcej informacji na temat panelu dostępu, zobacz [toohello wprowadzenie panelu dostępu](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="89e72-216">For more information about the Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="89e72-217">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="89e72-217">Additional resources</span></span>

* [<span data-ttu-id="89e72-218">Lista samouczków dotyczących tooIntegrate aplikacji SaaS w usłudze Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="89e72-218">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="89e72-219">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="89e72-219">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-fuse-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-fuse-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-fuse-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-fuse-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-fuse-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-fuse-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-fuse-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-fuse-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-fuse-tutorial/tutorial_general_203.png

