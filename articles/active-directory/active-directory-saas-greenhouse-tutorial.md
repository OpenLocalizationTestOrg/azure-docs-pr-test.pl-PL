---
title: 'Samouczek: Integracji Azure Active Directory z cieplarnianych | Dokumentacja firmy Microsoft'
description: "Dowiedz się, jak tooconfigure logowanie jednokrotne między usługą Azure Active Directory i cieplarnianych."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 78ec1766-4f79-4f16-9a66-d5584c4b6151
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/19/2017
ms.author: jeedes
ms.openlocfilehash: 1a7cdd00c4f2b15a1afc89522d79af22f4c5d866
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-greenhouse"></a><span data-ttu-id="d179d-103">Samouczek: Integracji Azure Active Directory z cieplarnianych</span><span class="sxs-lookup"><span data-stu-id="d179d-103">Tutorial: Azure Active Directory integration with Greenhouse</span></span>

<span data-ttu-id="d179d-104">Z tego samouczka, dowiesz się, jak toointegrate cieplarnianych w usłudze Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="d179d-104">In this tutorial, you learn how toointegrate Greenhouse with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="d179d-105">Integracja z usługą Azure AD cieplarnianych zapewnia hello następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="d179d-105">Integrating Greenhouse with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="d179d-106">Można kontrolować w usłudze Azure AD, kto ma dostęp do tooGreenhouse.</span><span class="sxs-lookup"><span data-stu-id="d179d-106">You can control in Azure AD who has access tooGreenhouse.</span></span>
- <span data-ttu-id="d179d-107">Można włączyć użytkownika użytkownicy tooautomatically get zalogowane tooGreenhouse (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="d179d-107">You can enable your users tooautomatically get signed-on tooGreenhouse (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="d179d-108">Możesz zarządzać kont w jednej centralnej lokalizacji - hello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="d179d-108">You can manage your accounts in one central location - hello Azure portal.</span></span>

<span data-ttu-id="d179d-109">Jeśli chcesz tooknow więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="d179d-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d179d-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="d179d-110">Prerequisites</span></span>

<span data-ttu-id="d179d-111">tooconfigure integracji usługi Azure AD z cieplarnianych należy hello następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="d179d-111">tooconfigure Azure AD integration with Greenhouse, you need hello following items:</span></span>

- <span data-ttu-id="d179d-112">Subskrypcję usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="d179d-112">An Azure AD subscription</span></span>
- <span data-ttu-id="d179d-113">Cieplarnianych logowanie jednokrotne włączone subskrypcji</span><span class="sxs-lookup"><span data-stu-id="d179d-113">A Greenhouse single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="d179d-114">tootest hello kroków w tym samouczku, zaleca się przy użyciu środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="d179d-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="d179d-115">tootest hello kroki opisane w tym samouczku, należy stosować te zalecenia:</span><span class="sxs-lookup"><span data-stu-id="d179d-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="d179d-116">Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="d179d-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="d179d-117">Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz [uzyskać miesięczna wersja próbna](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="d179d-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="d179d-118">Opis scenariusza</span><span class="sxs-lookup"><span data-stu-id="d179d-118">Scenario description</span></span>
<span data-ttu-id="d179d-119">W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym.</span><span class="sxs-lookup"><span data-stu-id="d179d-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="d179d-120">Scenariusz Hello opisane w tym samouczku składa się z dwóch głównych elementów:</span><span class="sxs-lookup"><span data-stu-id="d179d-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="d179d-121">Dodawanie cieplarnianych z galerii hello</span><span class="sxs-lookup"><span data-stu-id="d179d-121">Adding Greenhouse from hello gallery</span></span>
2. <span data-ttu-id="d179d-122">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="d179d-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-greenhouse-from-hello-gallery"></a><span data-ttu-id="d179d-123">Dodawanie cieplarnianych z galerii hello</span><span class="sxs-lookup"><span data-stu-id="d179d-123">Adding Greenhouse from hello gallery</span></span>
<span data-ttu-id="d179d-124">tooconfigure hello integracji cieplarnianych do usługi Azure AD, należy tooadd cieplarnianych z hello galerii tooyour listę zarządzanych aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="d179d-124">tooconfigure hello integration of Greenhouse into Azure AD, you need tooadd Greenhouse from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="d179d-125">**tooadd cieplarnianych z galerii hello wykonaj hello następujące kroki:**</span><span class="sxs-lookup"><span data-stu-id="d179d-125">**tooadd Greenhouse from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="d179d-126">W hello  **[portalu Azure](https://portal.azure.com)**na temat hello panelu nawigacji po lewej stronie, kliknij przycisk **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="d179d-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![przycisk usługi Azure Active Directory Hello][1]

2. <span data-ttu-id="d179d-128">Przejdź za**aplikacje dla przedsiębiorstw**.</span><span class="sxs-lookup"><span data-stu-id="d179d-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="d179d-129">Następnie przejdź zbyt**wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="d179d-129">Then go too**All applications**.</span></span>

    ![Blok aplikacje przedsiębiorstwa Hello][2]
    
3. <span data-ttu-id="d179d-131">tooadd nową aplikację, kliknij przycisk **nowej aplikacji** przycisk u góry hello okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="d179d-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Nowy przycisk aplikacji Hello][3]

4. <span data-ttu-id="d179d-133">W polu wyszukiwania hello wpisz **cieplarnianych**, wybierz pozycję **cieplarnianych** z panelu wyników następnie kliknij przycisk **Dodaj** przycisk aplikacji hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="d179d-133">In hello search box, type **Greenhouse**, select **Greenhouse** from result panel then click **Add** button tooadd hello application.</span></span>

    ![Cieplarnianych hello listy wyników](./media/active-directory-saas-greenhouse-tutorial/tutorial_greenhouse_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="d179d-135">Konfiguracja i testowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="d179d-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="d179d-136">W tej sekcji skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z cieplarnianych w oparciu o nazwie "Britta Simona" użytkownika testowego.</span><span class="sxs-lookup"><span data-stu-id="d179d-136">In this section, you configure and test Azure AD single sign-on with Greenhouse based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="d179d-137">Dla pojedynczego logowania jednokrotnego toowork usługi Azure AD musi tooknow użytkownika odpowiednikiem hello w cieplarnianych jest tooa użytkownika w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="d179d-137">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Greenhouse is tooa user in Azure AD.</span></span> <span data-ttu-id="d179d-138">Innymi słowy relację łącza między użytkownika usługi Azure AD i hello użytkownikowi w cieplarnianych musi toobe ustanowione.</span><span class="sxs-lookup"><span data-stu-id="d179d-138">In other words, a link relationship between an Azure AD user and hello related user in Greenhouse needs toobe established.</span></span>

<span data-ttu-id="d179d-139">W szklarni, należy przypisać wartość hello hello **nazwy użytkownika** w usłudze Azure AD jako wartość hello hello **Username** tooestablish hello łącze relacji.</span><span class="sxs-lookup"><span data-stu-id="d179d-139">In Greenhouse, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="d179d-140">tooconfigure i testowych usługi Azure AD rejestracji jednokrotnej z cieplarnianych, należy po bloków konstrukcyjnych hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="d179d-140">tooconfigure and test Azure AD single sign-on with Greenhouse, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="d179d-141">**[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configure-azure-ad-single-sign-on)**  -tooenable Twojego toouse użytkowników tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="d179d-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="d179d-142">**[Tworzenie użytkownika testowego usługi Azure AD](#create-an-azure-ad-test-user)**  -tootest usługi Azure AD rejestracji jednokrotnej z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="d179d-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="d179d-143">**[Tworzenie użytkownika testowego cieplarnianych](#create-a-greenhouse-test-user)**  -toohave odpowiednikiem Simona Britta w cieplarnianych, który jest połączony toohello usługi Azure AD reprezentację użytkownika.</span><span class="sxs-lookup"><span data-stu-id="d179d-143">**[Create a Greenhouse test user](#create-a-greenhouse-test-user)** - toohave a counterpart of Britta Simon in Greenhouse that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="d179d-144">**[Przypisz użytkownika testowego hello Azure AD](#assign-the-azure-ad-test-user)**  -tooenable Simona Britta toouse usługi Azure AD rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="d179d-144">**[Assign hello Azure AD test user](#assign-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="d179d-145">**[Test rejestracji jednokrotnej](#test-single-sign-on)**  -tooverify czy hello konfiguracji działania.</span><span class="sxs-lookup"><span data-stu-id="d179d-145">**[Test single sign-on](#test-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="d179d-146">Konfigurowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="d179d-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="d179d-147">W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w hello portalu Azure i skonfigurować logowanie jednokrotne w aplikacji cieplarnianych.</span><span class="sxs-lookup"><span data-stu-id="d179d-147">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Greenhouse application.</span></span>

<span data-ttu-id="d179d-148">**tooconfigure usługi Azure AD rejestracji jednokrotnej z cieplarnianych, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="d179d-148">**tooconfigure Azure AD single sign-on with Greenhouse, perform hello following steps:**</span></span>

1. <span data-ttu-id="d179d-149">W portalu Azure na powitania hello **cieplarnianych** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.</span><span class="sxs-lookup"><span data-stu-id="d179d-149">In hello Azure portal, on hello **Greenhouse** application integration page, click **Single sign-on**.</span></span>

    ![Skonfigurować łącze rejestracji jednokrotnej][4]

2. <span data-ttu-id="d179d-151">Na powitania **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** tooenable rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="d179d-151">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Okno dialogowe rejestracji jednokrotnej](./media/active-directory-saas-greenhouse-tutorial/tutorial_greenhouse_samlbase.png)

3. <span data-ttu-id="d179d-153">Na powitania **cieplarnianych domeny i adres URL** sekcji, wykonaj następujące kroki hello:</span><span class="sxs-lookup"><span data-stu-id="d179d-153">On hello **Greenhouse Domain and URLs** section, perform hello following steps:</span></span>

    ![Adresy URL i domeny cieplarnianych pojedynczy informacje logowania jednokrotnego](./media/active-directory-saas-greenhouse-tutorial/tutorial_greenhouse_url.png)

    <span data-ttu-id="d179d-155">a.</span><span class="sxs-lookup"><span data-stu-id="d179d-155">a.</span></span> <span data-ttu-id="d179d-156">W hello **adres URL logowania** tekstowym, wpisz adres URL za pomocą hello następującego wzorca:`https://<companyname>.greenhouse.io`</span><span class="sxs-lookup"><span data-stu-id="d179d-156">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<companyname>.greenhouse.io`</span></span>

    <span data-ttu-id="d179d-157">b.</span><span class="sxs-lookup"><span data-stu-id="d179d-157">b.</span></span> <span data-ttu-id="d179d-158">W hello **identyfikator** tekstowym, wpisz adres URL za pomocą hello następującego wzorca:`https://<companyname>.greenhouse.io`</span><span class="sxs-lookup"><span data-stu-id="d179d-158">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<companyname>.greenhouse.io`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="d179d-159">Wartości te nie są prawdziwe.</span><span class="sxs-lookup"><span data-stu-id="d179d-159">These values are not real.</span></span> <span data-ttu-id="d179d-160">Zaktualizować te wartości z hello rzeczywisty adres URL logowania i identyfikator.</span><span class="sxs-lookup"><span data-stu-id="d179d-160">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="d179d-161">Skontaktuj się z [zespołem pomocy technicznej klienta cieplarnianych](https://www.greenhouse.io/contact) tooget tych wartości.</span><span class="sxs-lookup"><span data-stu-id="d179d-161">Contact [Greenhouse Client support team](https://www.greenhouse.io/contact) tooget these values.</span></span> 
 


4. <span data-ttu-id="d179d-162">Na powitania **certyfikat podpisywania SAML** kliknij **XML metadanych** , a następnie zapisz plik metadanych hello na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="d179d-162">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![link do pobierania certyfikatu Hello](./media/active-directory-saas-greenhouse-tutorial/tutorial_greenhouse_certificate.png) 

5. <span data-ttu-id="d179d-164">Kliknij przycisk **zapisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="d179d-164">Click **Save** button.</span></span>

    ![Skonfiguruj przycisk pojedynczego logowania jednokrotnego Zapisz](./media/active-directory-saas-greenhouse-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="d179d-166">tooconfigure rejestracji jednokrotnej w **cieplarnianych** strony, należy pobrać hello toosend **XML metadanych** za[zespołem pomocy technicznej cieplarnianych](http://www.greenhouse.io/contact).</span><span class="sxs-lookup"><span data-stu-id="d179d-166">tooconfigure single sign-on on **Greenhouse** side, you need toosend hello downloaded **Metadata XML** too[Greenhouse support team](http://www.greenhouse.io/contact).</span></span>

> [!TIP]
> <span data-ttu-id="d179d-167">Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz hello [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji hello!</span><span class="sxs-lookup"><span data-stu-id="d179d-167">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="d179d-168">Po dodaniu tej aplikacji z hello **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij hello **rejestracji jednokrotnej** hello kartę i dostępu do osadzonych dokumentacji za pośrednictwem hello  **Konfiguracja** sekcji u dołu hello.</span><span class="sxs-lookup"><span data-stu-id="d179d-168">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="d179d-169">Więcej o hello osadzonych dokumentacji funkcji w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="d179d-169">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="d179d-170">Tworzenie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="d179d-170">Create an Azure AD test user</span></span>

<span data-ttu-id="d179d-171">Celem Hello w tej sekcji jest toocreate użytkownika testowego, w portalu Azure o nazwie Simona Britta hello.</span><span class="sxs-lookup"><span data-stu-id="d179d-171">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

   ![Tworzenie użytkownika testowego usługi Azure AD][100]

<span data-ttu-id="d179d-173">**toocreate użytkownika testowego w usłudze Azure AD, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="d179d-173">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="d179d-174">W portalu Azure, w okienku po lewej stronie powitania hello kliknij hello **usługi Azure Active Directory** przycisku.</span><span class="sxs-lookup"><span data-stu-id="d179d-174">In hello Azure portal, in hello left pane, click hello **Azure Active Directory** button.</span></span>

    ![przycisk usługi Azure Active Directory Hello](./media/active-directory-saas-greenhouse-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="d179d-176">toodisplay hello listę użytkowników, przejdź zbyt**użytkowników i grup**, a następnie kliknij przycisk **wszyscy użytkownicy**.</span><span class="sxs-lookup"><span data-stu-id="d179d-176">toodisplay hello list of users, go too**Users and groups**, and then click **All users**.</span></span>

    ![Witaj, "Użytkownicy i grupy" i "Wszyscy użytkownicy" łącza](./media/active-directory-saas-greenhouse-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="d179d-178">Witaj tooopen **użytkownika** okno dialogowe, kliknij przycisk **Dodaj** u góry hello hello **wszyscy użytkownicy** okno dialogowe.</span><span class="sxs-lookup"><span data-stu-id="d179d-178">tooopen hello **User** dialog box, click **Add** at hello top of hello **All Users** dialog box.</span></span>

    ![przycisk Dodaj Hello](./media/active-directory-saas-greenhouse-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="d179d-180">W hello **użytkownika** okna dialogowego wykonaj hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="d179d-180">In hello **User** dialog box, perform hello following steps:</span></span>

    ![okno dialogowe Hello użytkownika](./media/active-directory-saas-greenhouse-tutorial/create_aaduser_04.png)

    <span data-ttu-id="d179d-182">a.</span><span class="sxs-lookup"><span data-stu-id="d179d-182">a.</span></span> <span data-ttu-id="d179d-183">W hello **nazwa** wpisz **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="d179d-183">In hello **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="d179d-184">b.</span><span class="sxs-lookup"><span data-stu-id="d179d-184">b.</span></span> <span data-ttu-id="d179d-185">W hello **nazwy użytkownika** pole typu hello adres e-mail użytkownika Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="d179d-185">In hello **User name** box, type hello email address of user Britta Simon.</span></span>

    <span data-ttu-id="d179d-186">c.</span><span class="sxs-lookup"><span data-stu-id="d179d-186">c.</span></span> <span data-ttu-id="d179d-187">Wybierz hello **Pokaż hasło** pole wyboru, a następnie zapisz hello wartość, która jest wyświetlana w hello **hasło** pole.</span><span class="sxs-lookup"><span data-stu-id="d179d-187">Select hello **Show Password** check box, and then write down hello value that's displayed in hello **Password** box.</span></span>

    <span data-ttu-id="d179d-188">d.</span><span class="sxs-lookup"><span data-stu-id="d179d-188">d.</span></span> <span data-ttu-id="d179d-189">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="d179d-189">Click **Create**.</span></span>
 
### <a name="create-a-greenhouse-test-user"></a><span data-ttu-id="d179d-190">Tworzenie użytkownika testowego cieplarnianych</span><span class="sxs-lookup"><span data-stu-id="d179d-190">Create a Greenhouse test user</span></span>

<span data-ttu-id="d179d-191">W przypadku użytkowników usługi Azure AD toolog kolejności tooenable do cieplarnianych muszą mieć przydzielone do cieplarnianych.</span><span class="sxs-lookup"><span data-stu-id="d179d-191">In order tooenable Azure AD users toolog into Greenhouse, they must be provisioned into Greenhouse.</span></span> <span data-ttu-id="d179d-192">W przypadku hello cieplarnianych Inicjowanie obsługi to zadanie ręczne.</span><span class="sxs-lookup"><span data-stu-id="d179d-192">In hello case of Greenhouse, provisioning is a manual task.</span></span>

>[!NOTE]
><span data-ttu-id="d179d-193">Możesz użyć innych cieplarnianych użytkownika konta tworzenia narzędzi lub interfejsów API dostarczonych przez tooprovision cieplarnianych kont użytkowników usługi AAD.</span><span class="sxs-lookup"><span data-stu-id="d179d-193">You can use any other Greenhouse user account creation tools or APIs provided by Greenhouse tooprovision AAD user accounts.</span></span> 

<span data-ttu-id="d179d-194">**tooprovision kont użytkowników, wykonaj hello następujące kroki:**</span><span class="sxs-lookup"><span data-stu-id="d179d-194">**tooprovision a user accounts, perform hello following steps:**</span></span>

1. <span data-ttu-id="d179d-195">Zaloguj się za tooyour **cieplarnianych** witryny firmy jako administrator.</span><span class="sxs-lookup"><span data-stu-id="d179d-195">Log in tooyour **Greenhouse** company site as an administrator.</span></span>

2. <span data-ttu-id="d179d-196">Witaj menu u góry hello, kliknij przycisk **Konfiguruj**, a następnie kliknij przycisk **użytkowników**.</span><span class="sxs-lookup"><span data-stu-id="d179d-196">In hello menu on hello top, click **Configure**, and then click **Users**.</span></span>
   
   <span data-ttu-id="d179d-197">![Użytkownicy](./media/active-directory-saas-greenhouse-tutorial/ic790791.png "użytkowników")</span><span class="sxs-lookup"><span data-stu-id="d179d-197">![Users](./media/active-directory-saas-greenhouse-tutorial/ic790791.png "Users")</span></span>

3. <span data-ttu-id="d179d-198">Kliknij przycisk **nowych użytkowników**.</span><span class="sxs-lookup"><span data-stu-id="d179d-198">Click **New Users**.</span></span>
   
   <span data-ttu-id="d179d-199">![Nowy użytkownik](./media/active-directory-saas-greenhouse-tutorial/ic790792.png "nowego użytkownika")</span><span class="sxs-lookup"><span data-stu-id="d179d-199">![New User](./media/active-directory-saas-greenhouse-tutorial/ic790792.png "New User")</span></span>

4. <span data-ttu-id="d179d-200">W hello **Dodaj nowego użytkownika** sekcji, wykonaj następujące kroki hello:</span><span class="sxs-lookup"><span data-stu-id="d179d-200">In hello **Add New User** section, perform hello following steps:</span></span>
   
   <span data-ttu-id="d179d-201">![Dodaj nowego użytkownika](./media/active-directory-saas-greenhouse-tutorial/ic790793.png "Dodaj nowego użytkownika")</span><span class="sxs-lookup"><span data-stu-id="d179d-201">![Add New User](./media/active-directory-saas-greenhouse-tutorial/ic790793.png "Add New User")</span></span>

   <span data-ttu-id="d179d-202">a.</span><span class="sxs-lookup"><span data-stu-id="d179d-202">a.</span></span> <span data-ttu-id="d179d-203">W hello **wprowadź wiadomości e-mail użytkownika** pole tekstowe, typ hello adres e-mail ma tooprovision prawidłowe konto usługi Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="d179d-203">In hello **Enter user emails** textbox, type hello email address of a valid Azure Active Directory account you want tooprovision.</span></span>

   <span data-ttu-id="d179d-204">b.</span><span class="sxs-lookup"><span data-stu-id="d179d-204">b.</span></span> <span data-ttu-id="d179d-205">Kliknij pozycję **Zapisz**.</span><span class="sxs-lookup"><span data-stu-id="d179d-205">Click **Save**.</span></span>    
   
      >[!NOTE]
      ><span data-ttu-id="d179d-206">posiadaczy konta usługi Azure Active Directory Hello otrzymają wiadomość e-mail, w tym kontem hello tooconfirm łącze zanim staje się aktywny.</span><span class="sxs-lookup"><span data-stu-id="d179d-206">hello Azure Active Directory account holders will receive an email including a link tooconfirm hello account before it becomes active.</span></span>

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="d179d-207">Przypisz użytkownika testowego hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="d179d-207">Assign hello Azure AD test user</span></span>

<span data-ttu-id="d179d-208">W tej sekcji możesz włączyć toouse Simona Britta Azure logowania jednokrotnego za udzielanie dostępu tooGreenhouse.</span><span class="sxs-lookup"><span data-stu-id="d179d-208">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooGreenhouse.</span></span>

![Przypisanie roli użytkownika hello][200] 

<span data-ttu-id="d179d-210">**tooassign tooGreenhouse Simona Britta wykonaj hello następujące kroki:**</span><span class="sxs-lookup"><span data-stu-id="d179d-210">**tooassign Britta Simon tooGreenhouse, perform hello following steps:**</span></span>

1. <span data-ttu-id="d179d-211">W portalu Azure hello, otwórz widok aplikacji hello, a następnie przejdź do widoku katalogu toohello i przejść za**aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="d179d-211">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Przypisz użytkownika][201] 

2. <span data-ttu-id="d179d-213">Z listy aplikacji hello wybierz **cieplarnianych**.</span><span class="sxs-lookup"><span data-stu-id="d179d-213">In hello applications list, select **Greenhouse**.</span></span>

    ![łącze cieplarnianych Hello na liście aplikacji hello](./media/active-directory-saas-greenhouse-tutorial/tutorial_greenhouse_app.png)  

3. <span data-ttu-id="d179d-215">W menu powitania po lewej stronie powitania kliknij **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="d179d-215">In hello menu on hello left, click **Users and groups**.</span></span>

    ![łącze "Użytkownicy i grupy" Hello][202]

4. <span data-ttu-id="d179d-217">Kliknij przycisk **Dodaj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="d179d-217">Click **Add** button.</span></span> <span data-ttu-id="d179d-218">Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="d179d-218">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Okienko Dodaj przypisania Hello][203]

5. <span data-ttu-id="d179d-220">Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** hello listy użytkowników.</span><span class="sxs-lookup"><span data-stu-id="d179d-220">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="d179d-221">Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="d179d-221">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="d179d-222">Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="d179d-222">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="d179d-223">Test rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="d179d-223">Test single sign-on</span></span>

<span data-ttu-id="d179d-224">W tej sekcji można przetestować konfiguracji usługi Azure AD pojedynczego logowania jednokrotnego przy użyciu hello panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="d179d-224">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="d179d-225">Po kliknięciu kafelka cieplarnianych hello w hello Panel dostępu, należy pobrać automatycznie zalogowane tooyour cieplarnianych aplikacji.</span><span class="sxs-lookup"><span data-stu-id="d179d-225">When you click hello Greenhouse tile in hello Access Panel, you should get automatically signed-on tooyour Greenhouse application.</span></span>
<span data-ttu-id="d179d-226">Aby uzyskać więcej informacji na temat hello Panel dostępu, zobacz [toohello wprowadzenie panelu dostępu](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="d179d-226">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="d179d-227">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="d179d-227">Additional resources</span></span>

* [<span data-ttu-id="d179d-228">Lista samouczków dotyczących tooIntegrate aplikacji SaaS w usłudze Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="d179d-228">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="d179d-229">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="d179d-229">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-greenhouse-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-greenhouse-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-greenhouse-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-greenhouse-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-greenhouse-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-greenhouse-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-greenhouse-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-greenhouse-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-greenhouse-tutorial/tutorial_general_203.png

