---
title: 'Samouczek: Integracji Azure Active Directory z Synergi | Dokumentacja firmy Microsoft'
description: "Dowiedz się, jak tooconfigure logowanie jednokrotne między usługą Azure Active Directory i Synergi."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 73c970e1-f1ba-420b-b225-414fdf93b140
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/08/2017
ms.author: jeedes
ms.openlocfilehash: 5d4a9a596db2a60dda5bcac2c86b88b460a2e2cc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-synergi"></a><span data-ttu-id="63962-103">Samouczek: Integracji Azure Active Directory z Synergi</span><span class="sxs-lookup"><span data-stu-id="63962-103">Tutorial: Azure Active Directory integration with Synergi</span></span>

<span data-ttu-id="63962-104">Z tego samouczka, dowiesz się, jak toointegrate Synergi w usłudze Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="63962-104">In this tutorial, you learn how toointegrate Synergi with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="63962-105">Integracja z usługą Azure AD Synergi zapewnia hello następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="63962-105">Integrating Synergi with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="63962-106">Można kontrolować w usłudze Azure AD, kto ma dostęp do tooSynergi.</span><span class="sxs-lookup"><span data-stu-id="63962-106">You can control in Azure AD who has access tooSynergi.</span></span>
- <span data-ttu-id="63962-107">Można włączyć użytkownika użytkownicy tooautomatically get zalogowane tooSynergi (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="63962-107">You can enable your users tooautomatically get signed-on tooSynergi (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="63962-108">Możesz zarządzać kont w jednej centralnej lokalizacji - hello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="63962-108">You can manage your accounts in one central location - hello Azure portal.</span></span>

<span data-ttu-id="63962-109">Jeśli chcesz tooknow więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="63962-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="63962-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="63962-110">Prerequisites</span></span>

<span data-ttu-id="63962-111">tooconfigure integracji z usługą Azure AD z Synergi należy hello następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="63962-111">tooconfigure Azure AD integration with Synergi, you need hello following items:</span></span>

- <span data-ttu-id="63962-112">Subskrypcję usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="63962-112">An Azure AD subscription</span></span>
- <span data-ttu-id="63962-113">Synergi logowanie jednokrotne włączone subskrypcji</span><span class="sxs-lookup"><span data-stu-id="63962-113">A Synergi single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="63962-114">tootest hello kroków w tym samouczku, zaleca się przy użyciu środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="63962-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="63962-115">tootest hello kroki opisane w tym samouczku, należy stosować te zalecenia:</span><span class="sxs-lookup"><span data-stu-id="63962-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="63962-116">Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="63962-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="63962-117">Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz [uzyskać miesięczna wersja próbna](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="63962-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="63962-118">Opis scenariusza</span><span class="sxs-lookup"><span data-stu-id="63962-118">Scenario description</span></span>
<span data-ttu-id="63962-119">W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym.</span><span class="sxs-lookup"><span data-stu-id="63962-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="63962-120">Scenariusz Hello opisane w tym samouczku składa się z dwóch głównych elementów:</span><span class="sxs-lookup"><span data-stu-id="63962-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="63962-121">Dodawanie Synergi z galerii hello</span><span class="sxs-lookup"><span data-stu-id="63962-121">Adding Synergi from hello gallery</span></span>
2. <span data-ttu-id="63962-122">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="63962-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-synergi-from-hello-gallery"></a><span data-ttu-id="63962-123">Dodawanie Synergi z galerii hello</span><span class="sxs-lookup"><span data-stu-id="63962-123">Adding Synergi from hello gallery</span></span>
<span data-ttu-id="63962-124">tooconfigure hello integracji Synergi do usługi Azure AD, należy tooadd Synergi z hello galerii tooyour listę zarządzanych aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="63962-124">tooconfigure hello integration of Synergi into Azure AD, you need tooadd Synergi from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="63962-125">**tooadd Synergi z galerii hello, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="63962-125">**tooadd Synergi from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="63962-126">W hello  **[portalu Azure](https://portal.azure.com)**na temat hello panelu nawigacji po lewej stronie, kliknij przycisk **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="63962-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![przycisk usługi Azure Active Directory Hello][1]

2. <span data-ttu-id="63962-128">Przejdź za**aplikacje dla przedsiębiorstw**.</span><span class="sxs-lookup"><span data-stu-id="63962-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="63962-129">Następnie przejdź zbyt**wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="63962-129">Then go too**All applications**.</span></span>

    ![Blok aplikacje przedsiębiorstwa Hello][2]
    
3. <span data-ttu-id="63962-131">tooadd nową aplikację, kliknij przycisk **nowej aplikacji** przycisk u góry hello okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="63962-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Nowy przycisk aplikacji Hello][3]

4. <span data-ttu-id="63962-133">W polu wyszukiwania hello wpisz **Synergi**, wybierz pozycję **Synergi** z panelu wyników następnie kliknij przycisk **Dodaj** przycisk aplikacji hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="63962-133">In hello search box, type **Synergi**, select **Synergi** from result panel then click **Add** button tooadd hello application.</span></span>

    ![Synergi hello listy wyników](./media/active-directory-saas-synergi-tutorial/tutorial_synergi_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="63962-135">Konfiguracja i testowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="63962-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="63962-136">W tej sekcji skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z Synergi w oparciu o nazwie "Britta Simona" użytkownika testowego.</span><span class="sxs-lookup"><span data-stu-id="63962-136">In this section, you configure and test Azure AD single sign-on with Synergi based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="63962-137">Dla pojedynczego logowania jednokrotnego toowork usługi Azure AD musi tooknow użytkownika odpowiednikiem hello w Synergi jest tooa użytkownika w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="63962-137">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Synergi is tooa user in Azure AD.</span></span> <span data-ttu-id="63962-138">Innymi słowy relację łącza między użytkownika usługi Azure AD i hello użytkownikowi w Synergi musi toobe ustanowione.</span><span class="sxs-lookup"><span data-stu-id="63962-138">In other words, a link relationship between an Azure AD user and hello related user in Synergi needs toobe established.</span></span>

<span data-ttu-id="63962-139">W Synergi, należy przypisać wartość hello hello **nazwy użytkownika** w usłudze Azure AD jako wartość hello hello **Username** tooestablish hello łącze relacji.</span><span class="sxs-lookup"><span data-stu-id="63962-139">In Synergi, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="63962-140">tooconfigure i testowych usługi Azure AD rejestracji jednokrotnej z Synergi, należy po bloków konstrukcyjnych hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="63962-140">tooconfigure and test Azure AD single sign-on with Synergi, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="63962-141">**[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configure-azure-ad-single-sign-on)**  -tooenable Twojego toouse użytkowników tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="63962-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="63962-142">**[Tworzenie użytkownika testowego usługi Azure AD](#create-an-azure-ad-test-user)**  -tootest usługi Azure AD rejestracji jednokrotnej z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="63962-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="63962-143">**[Tworzenie użytkownika testowego Synergi](#create-a-synergi-test-user)**  -toohave odpowiednikiem Simona Britta w Synergi, który jest połączony toohello usługi Azure AD reprezentację użytkownika.</span><span class="sxs-lookup"><span data-stu-id="63962-143">**[Create a Synergi test user](#create-a-synergi-test-user)** - toohave a counterpart of Britta Simon in Synergi that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="63962-144">**[Przypisz użytkownika testowego hello Azure AD](#assign-the-azure-ad-test-user)**  -tooenable Simona Britta toouse usługi Azure AD rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="63962-144">**[Assign hello Azure AD test user](#assign-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="63962-145">**[Test rejestracji jednokrotnej](#test-single-sign-on)**  -tooverify czy hello konfiguracji działania.</span><span class="sxs-lookup"><span data-stu-id="63962-145">**[Test single sign-on](#test-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="63962-146">Konfigurowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="63962-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="63962-147">W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w portalu Azure hello i skonfigurować logowanie jednokrotne w aplikacji Synergi.</span><span class="sxs-lookup"><span data-stu-id="63962-147">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Synergi application.</span></span>

<span data-ttu-id="63962-148">**tooconfigure usługi Azure AD rejestracji jednokrotnej z Synergi, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="63962-148">**tooconfigure Azure AD single sign-on with Synergi, perform hello following steps:**</span></span>

1. <span data-ttu-id="63962-149">W portalu Azure na powitania hello **Synergi** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.</span><span class="sxs-lookup"><span data-stu-id="63962-149">In hello Azure portal, on hello **Synergi** application integration page, click **Single sign-on**.</span></span>

    ![Skonfigurować łącze rejestracji jednokrotnej][4]

2. <span data-ttu-id="63962-151">Na powitania **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** tooenable rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="63962-151">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Okno dialogowe rejestracji jednokrotnej](./media/active-directory-saas-synergi-tutorial/tutorial_synergi_samlbase.png)

3. <span data-ttu-id="63962-153">Na powitania **Synergi domeny i adres URL** sekcji, wykonaj następujące kroki hello:</span><span class="sxs-lookup"><span data-stu-id="63962-153">On hello **Synergi Domain and URLs** section, perform hello following steps:</span></span>

    ![Adresy URL i domeny Synergi pojedynczy informacje logowania jednokrotnego](./media/active-directory-saas-synergi-tutorial/tutorial_synergi_url.png)

    <span data-ttu-id="63962-155">a.</span><span class="sxs-lookup"><span data-stu-id="63962-155">a.</span></span> <span data-ttu-id="63962-156">W hello **identyfikator** tekstowym, wpisz adres URL za pomocą hello następującego wzorca:`https://<company name>.irmsecurity.com`</span><span class="sxs-lookup"><span data-stu-id="63962-156">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<company name>.irmsecurity.com`</span></span>

    <span data-ttu-id="63962-157">b.</span><span class="sxs-lookup"><span data-stu-id="63962-157">b.</span></span> <span data-ttu-id="63962-158">W hello **adres URL odpowiedzi** tekstowym, wpisz adres URL za pomocą hello następującego wzorca:`https://<company name>.irmsecurity.com/sso/<organization id>`</span><span class="sxs-lookup"><span data-stu-id="63962-158">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://<company name>.irmsecurity.com/sso/<organization id>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="63962-159">Wartości te nie są prawdziwe.</span><span class="sxs-lookup"><span data-stu-id="63962-159">These values are not real.</span></span> <span data-ttu-id="63962-160">Witaj rzeczywisty identyfikator i odpowiedzi adresu URL, należy zaktualizować te wartości.</span><span class="sxs-lookup"><span data-stu-id="63962-160">Update these values with hello actual Identifier and Reply URL.</span></span> <span data-ttu-id="63962-161">Skontaktuj się z [zespołem pomocy technicznej Synergi](https://www.irmsecurity.com/contact/) tooget tych wartości.</span><span class="sxs-lookup"><span data-stu-id="63962-161">Contact [Synergi support team](https://www.irmsecurity.com/contact/) tooget these values.</span></span>

4. <span data-ttu-id="63962-162">Na powitania **certyfikat podpisywania SAML** kliknij **Certificate(Base64)** , a następnie zapisz plik certyfikatu hello na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="63962-162">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![link do pobierania certyfikatu Hello](./media/active-directory-saas-synergi-tutorial/tutorial_synergi_certificate.png) 

5. <span data-ttu-id="63962-164">Kliknij przycisk **zapisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="63962-164">Click **Save** button.</span></span>

    ![Skonfiguruj przycisk pojedynczego logowania jednokrotnego Zapisz](./media/active-directory-saas-synergi-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="63962-166">Na powitania **konfiguracji Synergi** kliknij **skonfigurować Synergi** tooopen **Konfigurowanie logowania jednokrotnego** okna.</span><span class="sxs-lookup"><span data-stu-id="63962-166">On hello **Synergi Configuration** section, click **Configure Synergi** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="63962-167">Witaj kopii **Sign-Out adresu URL i identyfikator jednostki SAML** z hello **sekcji krótkimi opisami.**</span><span class="sxs-lookup"><span data-stu-id="63962-167">Copy hello **Sign-Out URL and SAML Entity ID** from hello **Quick Reference section.**</span></span>

    ![Konfiguracja Synergi](./media/active-directory-saas-synergi-tutorial/tutorial_synergi_configure.png) 

7. <span data-ttu-id="63962-169">tooconfigure rejestracji jednokrotnej w **Synergi** strony, należy pobrać hello toosend **Certificate(Base64) Sign-Out adresu URL i identyfikator jednostki SAML** za[zespołem pomocy technicznej Synergi](https://www.irmsecurity.com/contact/).</span><span class="sxs-lookup"><span data-stu-id="63962-169">tooconfigure single sign-on on **Synergi** side, you need toosend hello downloaded **Certificate(Base64), Sign-Out URL, and SAML Entity ID** too[Synergi support team](https://www.irmsecurity.com/contact/).</span></span>

> [!TIP]
> <span data-ttu-id="63962-170">Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz hello [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji hello!</span><span class="sxs-lookup"><span data-stu-id="63962-170">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="63962-171">Po dodaniu tej aplikacji z hello **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij hello **rejestracji jednokrotnej** hello kartę i dostępu do osadzonych dokumentacji za pośrednictwem hello  **Konfiguracja** sekcji u dołu hello.</span><span class="sxs-lookup"><span data-stu-id="63962-171">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="63962-172">Więcej o hello osadzonych dokumentacji funkcji w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="63962-172">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="63962-173">Tworzenie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="63962-173">Create an Azure AD test user</span></span>

<span data-ttu-id="63962-174">Celem Hello w tej sekcji jest toocreate użytkownika testowego, w portalu Azure o nazwie Simona Britta hello.</span><span class="sxs-lookup"><span data-stu-id="63962-174">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

   ![Tworzenie użytkownika testowego usługi Azure AD][100]

<span data-ttu-id="63962-176">**toocreate użytkownika testowego w usłudze Azure AD, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="63962-176">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="63962-177">W portalu Azure, w okienku po lewej stronie powitania hello kliknij hello **usługi Azure Active Directory** przycisku.</span><span class="sxs-lookup"><span data-stu-id="63962-177">In hello Azure portal, in hello left pane, click hello **Azure Active Directory** button.</span></span>

    ![przycisk usługi Azure Active Directory Hello](./media/active-directory-saas-synergi-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="63962-179">toodisplay hello listę użytkowników, przejdź zbyt**użytkowników i grup**, a następnie kliknij przycisk **wszyscy użytkownicy**.</span><span class="sxs-lookup"><span data-stu-id="63962-179">toodisplay hello list of users, go too**Users and groups**, and then click **All users**.</span></span>

    ![Witaj, "Użytkownicy i grupy" i "Wszyscy użytkownicy" łącza](./media/active-directory-saas-synergi-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="63962-181">Witaj tooopen **użytkownika** okno dialogowe, kliknij przycisk **Dodaj** u góry hello hello **wszyscy użytkownicy** okno dialogowe.</span><span class="sxs-lookup"><span data-stu-id="63962-181">tooopen hello **User** dialog box, click **Add** at hello top of hello **All Users** dialog box.</span></span>

    ![przycisk Dodaj Hello](./media/active-directory-saas-synergi-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="63962-183">W hello **użytkownika** okna dialogowego wykonaj hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="63962-183">In hello **User** dialog box, perform hello following steps:</span></span>

    ![okno dialogowe Hello użytkownika](./media/active-directory-saas-synergi-tutorial/create_aaduser_04.png)

    <span data-ttu-id="63962-185">a.</span><span class="sxs-lookup"><span data-stu-id="63962-185">a.</span></span> <span data-ttu-id="63962-186">W hello **nazwa** wpisz **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="63962-186">In hello **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="63962-187">b.</span><span class="sxs-lookup"><span data-stu-id="63962-187">b.</span></span> <span data-ttu-id="63962-188">W hello **nazwy użytkownika** pole typu hello adres e-mail użytkownika Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="63962-188">In hello **User name** box, type hello email address of user Britta Simon.</span></span>

    <span data-ttu-id="63962-189">c.</span><span class="sxs-lookup"><span data-stu-id="63962-189">c.</span></span> <span data-ttu-id="63962-190">Wybierz hello **Pokaż hasło** pole wyboru, a następnie zapisz hello wartość, która jest wyświetlana w hello **hasło** pole.</span><span class="sxs-lookup"><span data-stu-id="63962-190">Select hello **Show Password** check box, and then write down hello value that's displayed in hello **Password** box.</span></span>

    <span data-ttu-id="63962-191">d.</span><span class="sxs-lookup"><span data-stu-id="63962-191">d.</span></span> <span data-ttu-id="63962-192">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="63962-192">Click **Create**.</span></span>
  
### <a name="create-a-synergi-test-user"></a><span data-ttu-id="63962-193">Tworzenie użytkownika testowego Synergi</span><span class="sxs-lookup"><span data-stu-id="63962-193">Create a Synergi test user</span></span>

<span data-ttu-id="63962-194">W tej sekcji należy utworzyć użytkownika o nazwie Simona Britta w Synergi.</span><span class="sxs-lookup"><span data-stu-id="63962-194">In this section, you create a user called Britta Simon in Synergi.</span></span> <span data-ttu-id="63962-195">Praca z [zespołem pomocy technicznej Synergi](https://www.irmsecurity.com/contact/) do dodawania użytkowników hello hello Synergi platformy.</span><span class="sxs-lookup"><span data-stu-id="63962-195">Work with [Synergi support team](https://www.irmsecurity.com/contact/) to add hello users in hello Synergi platform.</span></span> <span data-ttu-id="63962-196">Użytkownicy muszą utworzyć i aktywowana, aby użyć rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="63962-196">Users must be created and activated before you use single sign-on.</span></span>

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="63962-197">Przypisz użytkownika testowego hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="63962-197">Assign hello Azure AD test user</span></span>

<span data-ttu-id="63962-198">W tej sekcji możesz włączyć toouse Simona Britta Azure logowania jednokrotnego za udzielanie dostępu tooSynergi.</span><span class="sxs-lookup"><span data-stu-id="63962-198">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooSynergi.</span></span>

![Przypisanie roli użytkownika hello][200] 

<span data-ttu-id="63962-200">**tooassign tooSynergi Simona Britta wykonaj hello następujące kroki:**</span><span class="sxs-lookup"><span data-stu-id="63962-200">**tooassign Britta Simon tooSynergi, perform hello following steps:**</span></span>

1. <span data-ttu-id="63962-201">W portalu Azure hello, otwórz widok aplikacji hello, a następnie przejdź do widoku katalogu toohello i przejść za**aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="63962-201">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Przypisz użytkownika][201] 

2. <span data-ttu-id="63962-203">Z listy aplikacji hello wybierz **Synergi**.</span><span class="sxs-lookup"><span data-stu-id="63962-203">In hello applications list, select **Synergi**.</span></span>

    ![łącze Synergi Hello na liście aplikacji hello](./media/active-directory-saas-synergi-tutorial/tutorial_synergi_app.png)  

3. <span data-ttu-id="63962-205">W menu powitania po lewej stronie powitania kliknij **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="63962-205">In hello menu on hello left, click **Users and groups**.</span></span>

    ![łącze "Użytkownicy i grupy" Hello][202]

4. <span data-ttu-id="63962-207">Kliknij przycisk **Dodaj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="63962-207">Click **Add** button.</span></span> <span data-ttu-id="63962-208">Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="63962-208">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Okienko Dodaj przypisania Hello][203]

5. <span data-ttu-id="63962-210">Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** hello listy użytkowników.</span><span class="sxs-lookup"><span data-stu-id="63962-210">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="63962-211">Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="63962-211">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="63962-212">Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="63962-212">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="63962-213">Test rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="63962-213">Test single sign-on</span></span>

<span data-ttu-id="63962-214">W tej sekcji można przetestować konfiguracji usługi Azure AD pojedynczego logowania jednokrotnego przy użyciu hello panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="63962-214">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="63962-215">Po kliknięciu kafelka Synergi hello w hello Panel dostępu, należy pobrać automatycznie zalogowane tooyour Synergi aplikacji.</span><span class="sxs-lookup"><span data-stu-id="63962-215">When you click hello Synergi tile in hello Access Panel, you should get automatically signed-on tooyour Synergi application.</span></span>
<span data-ttu-id="63962-216">Aby uzyskać więcej informacji na temat panelu dostępu, zobacz [toohello wprowadzenie panelu dostępu](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="63962-216">For more information about the Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="63962-217">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="63962-217">Additional resources</span></span>

* [<span data-ttu-id="63962-218">Lista samouczków dotyczących tooIntegrate aplikacji SaaS w usłudze Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="63962-218">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="63962-219">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="63962-219">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-synergi-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-synergi-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-synergi-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-synergi-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-synergi-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-synergi-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-synergi-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-synergi-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-synergi-tutorial/tutorial_general_203.png

