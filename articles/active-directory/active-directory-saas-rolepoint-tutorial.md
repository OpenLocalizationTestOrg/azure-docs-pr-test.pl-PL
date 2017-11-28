---
title: 'Samouczek: Integracji Azure Active Directory z RolePoint | Dokumentacja firmy Microsoft'
description: "Dowiedz się, jak tooconfigure logowanie jednokrotne między usługą Azure Active Directory i RolePoint."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 68d37f40-15da-45f5-a9e1-d53f78e786d1
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/27/2017
ms.author: jeedes
ms.openlocfilehash: 8629dd87c17d44ab89251ebbd19156c6d6cbedc5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-rolepoint"></a><span data-ttu-id="7b2d4-103">Samouczek: Integracji Azure Active Directory z RolePoint</span><span class="sxs-lookup"><span data-stu-id="7b2d4-103">Tutorial: Azure Active Directory integration with RolePoint</span></span>

<span data-ttu-id="7b2d4-104">Z tego samouczka, dowiesz się, jak toointegrate RolePoint w usłudze Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="7b2d4-104">In this tutorial, you learn how toointegrate RolePoint with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="7b2d4-105">Integracja z usługą Azure AD RolePoint zapewnia hello następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="7b2d4-105">Integrating RolePoint with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="7b2d4-106">Można kontrolować w usłudze Azure AD, kto ma dostęp do tooRolePoint</span><span class="sxs-lookup"><span data-stu-id="7b2d4-106">You can control in Azure AD who has access tooRolePoint</span></span>
- <span data-ttu-id="7b2d4-107">Można włączyć użytkownika użytkownicy tooautomatically get zalogowane tooRolePoint (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="7b2d4-107">You can enable your users tooautomatically get signed-on tooRolePoint (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="7b2d4-108">Możesz zarządzać kont w jednej centralnej lokalizacji - hello portalu Azure</span><span class="sxs-lookup"><span data-stu-id="7b2d4-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="7b2d4-109">Jeśli chcesz tooknow więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="7b2d4-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="7b2d4-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="7b2d4-110">Prerequisites</span></span>

<span data-ttu-id="7b2d4-111">tooconfigure integracji z usługą Azure AD z RolePoint należy hello następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="7b2d4-111">tooconfigure Azure AD integration with RolePoint, you need hello following items:</span></span>

- <span data-ttu-id="7b2d4-112">Subskrypcję usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="7b2d4-112">An Azure AD subscription</span></span>
- <span data-ttu-id="7b2d4-113">RolePoint jednokrotnego włączone subskrypcji</span><span class="sxs-lookup"><span data-stu-id="7b2d4-113">A RolePoint single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="7b2d4-114">tootest hello kroków w tym samouczku, zaleca się przy użyciu środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="7b2d4-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="7b2d4-115">tootest hello kroki opisane w tym samouczku, należy stosować te zalecenia:</span><span class="sxs-lookup"><span data-stu-id="7b2d4-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="7b2d4-116">Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="7b2d4-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="7b2d4-117">Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz pobrać miesięczna wersja próbna [tutaj](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="7b2d4-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="7b2d4-118">Opis scenariusza</span><span class="sxs-lookup"><span data-stu-id="7b2d4-118">Scenario description</span></span>
<span data-ttu-id="7b2d4-119">W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym.</span><span class="sxs-lookup"><span data-stu-id="7b2d4-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="7b2d4-120">Scenariusz Hello opisane w tym samouczku składa się z dwóch głównych elementów:</span><span class="sxs-lookup"><span data-stu-id="7b2d4-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="7b2d4-121">Dodawanie RolePoint z galerii hello</span><span class="sxs-lookup"><span data-stu-id="7b2d4-121">Adding RolePoint from hello gallery</span></span>
2. <span data-ttu-id="7b2d4-122">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="7b2d4-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-rolepoint-from-hello-gallery"></a><span data-ttu-id="7b2d4-123">Dodawanie RolePoint z galerii hello</span><span class="sxs-lookup"><span data-stu-id="7b2d4-123">Adding RolePoint from hello gallery</span></span>
<span data-ttu-id="7b2d4-124">tooconfigure hello integracji RolePoint do usługi Azure AD, należy tooadd RolePoint z hello galerii tooyour listę zarządzanych aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="7b2d4-124">tooconfigure hello integration of RolePoint into Azure AD, you need tooadd RolePoint from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="7b2d4-125">**tooadd RolePoint z galerii hello, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="7b2d4-125">**tooadd RolePoint from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="7b2d4-126">W hello  **[portalu Azure](https://portal.azure.com)**na temat hello panelu nawigacji po lewej stronie, kliknij przycisk **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="7b2d4-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Usługa Active Directory][1]

2. <span data-ttu-id="7b2d4-128">Przejdź za**aplikacje dla przedsiębiorstw**.</span><span class="sxs-lookup"><span data-stu-id="7b2d4-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="7b2d4-129">Następnie przejdź zbyt**wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="7b2d4-129">Then go too**All applications**.</span></span>

    ![Aplikacje][2]
    
3. <span data-ttu-id="7b2d4-131">tooadd nową aplikację, kliknij przycisk **nowej aplikacji** przycisk u góry hello okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="7b2d4-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplikacje][3]

4. <span data-ttu-id="7b2d4-133">W polu wyszukiwania hello wpisz **RolePoint**.</span><span class="sxs-lookup"><span data-stu-id="7b2d4-133">In hello search box, type **RolePoint**.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-rolepoint-tutorial/tutorial_rolepoint_search.png)

5. <span data-ttu-id="7b2d4-135">W panelu wyników hello zaznacz **RolePoint**, a następnie kliknij przycisk **Dodaj** przycisk aplikacji hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="7b2d4-135">In hello results panel, select **RolePoint**, and then click **Add** button tooadd hello application.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-rolepoint-tutorial/tutorial_rolepoint_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="7b2d4-137">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="7b2d4-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="7b2d4-138">W tej sekcji możesz skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z RolePoint na podstawie użytkownika testowego, nazywany "Britta Simona".</span><span class="sxs-lookup"><span data-stu-id="7b2d4-138">In this section, you configure and test Azure AD single sign-on with RolePoint based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="7b2d4-139">Dla pojedynczego logowania jednokrotnego toowork usługi Azure AD musi tooknow użytkownika odpowiednikiem hello w RolePoint jest tooa użytkownika w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="7b2d4-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in RolePoint is tooa user in Azure AD.</span></span> <span data-ttu-id="7b2d4-140">Innymi słowy relację łącza między użytkownika usługi Azure AD i hello użytkownikowi w RolePoint musi toobe ustanowione.</span><span class="sxs-lookup"><span data-stu-id="7b2d4-140">In other words, a link relationship between an Azure AD user and hello related user in RolePoint needs toobe established.</span></span>

<span data-ttu-id="7b2d4-141">Ta relacja łącza zostanie nawiązane, przypisując wartość hello hello **nazwy użytkownika** w usłudze Azure AD jako wartość hello hello **Username** w RolePoint.</span><span class="sxs-lookup"><span data-stu-id="7b2d4-141">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in RolePoint.</span></span>

<span data-ttu-id="7b2d4-142">tooconfigure i testowych usługi Azure AD rejestracji jednokrotnej z RolePoint, należy po bloków konstrukcyjnych hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="7b2d4-142">tooconfigure and test Azure AD single sign-on with RolePoint, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="7b2d4-143">**[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configuring-azure-ad-single-sign-on)**  -tooenable Twojego toouse użytkowników tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="7b2d4-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="7b2d4-144">**[Tworzenie użytkownika testowego usługi Azure AD](#creating-an-azure-ad-test-user)**  -tootest usługi Azure AD rejestracji jednokrotnej z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="7b2d4-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="7b2d4-145">**[Tworzenie użytkownika testowego RolePoint](#creating-a-rolepoint-test-user)**  -toohave odpowiednikiem Simona Britta w RolePoint, który jest połączony toohello usługi Azure AD reprezentację użytkownika.</span><span class="sxs-lookup"><span data-stu-id="7b2d4-145">**[Creating a RolePoint test user](#creating-a-rolepoint-test-user)** - toohave a counterpart of Britta Simon in RolePoint that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="7b2d4-146">**[Przypisanie użytkownika testowego hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Simona Britta toouse usługi Azure AD rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="7b2d4-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="7b2d4-147">**[Testowanie rejestracji jednokrotnej](#testing-single-sign-on)**  -tooverify czy hello konfiguracji działania.</span><span class="sxs-lookup"><span data-stu-id="7b2d4-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="7b2d4-148">Konfigurowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="7b2d4-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="7b2d4-149">W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w portalu Azure hello i skonfigurować logowanie jednokrotne w aplikacji RolePoint.</span><span class="sxs-lookup"><span data-stu-id="7b2d4-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your RolePoint application.</span></span>

<span data-ttu-id="7b2d4-150">**tooconfigure usługi Azure AD rejestracji jednokrotnej z RolePoint, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="7b2d4-150">**tooconfigure Azure AD single sign-on with RolePoint, perform hello following steps:**</span></span>

1. <span data-ttu-id="7b2d4-151">W portalu Azure na powitania hello **RolePoint** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.</span><span class="sxs-lookup"><span data-stu-id="7b2d4-151">In hello Azure portal, on hello **RolePoint** application integration page, click **Single sign-on**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej][4]

2. <span data-ttu-id="7b2d4-153">Na powitania **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** tooenable rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="7b2d4-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-rolepoint-tutorial/tutorial_rolepoint_samlbase.png)

3. <span data-ttu-id="7b2d4-155">Na powitania **RolePoint domeny i adres URL** sekcji, wykonaj następujące kroki hello:</span><span class="sxs-lookup"><span data-stu-id="7b2d4-155">On hello **RolePoint Domain and URLs** section, perform hello following steps:</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-rolepoint-tutorial/tutorial_rolepoint_url.png)

    <span data-ttu-id="7b2d4-157">a.</span><span class="sxs-lookup"><span data-stu-id="7b2d4-157">a.</span></span> <span data-ttu-id="7b2d4-158">W hello **adres URL logowania** tekstowym, wpisz adres URL za pomocą hello następującego wzorca:`https://<subdomain>.rolepoint.com/login`</span><span class="sxs-lookup"><span data-stu-id="7b2d4-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<subdomain>.rolepoint.com/login`</span></span>
    
    <span data-ttu-id="7b2d4-159">b.</span><span class="sxs-lookup"><span data-stu-id="7b2d4-159">b.</span></span> <span data-ttu-id="7b2d4-160">W hello **identyfikator** tekstowym, wpisz adres URL za pomocą hello następującego wzorca:`https://app.rolepoint.com/<instancename>`</span><span class="sxs-lookup"><span data-stu-id="7b2d4-160">In hello **Identifier** textbox, type a URL using hello following pattern: `https://app.rolepoint.com/<instancename>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="7b2d4-161">Wartości te nie są hello prawdziwe.</span><span class="sxs-lookup"><span data-stu-id="7b2d4-161">These values are not hello real.</span></span> <span data-ttu-id="7b2d4-162">Zaktualizować te wartości z hello rzeczywisty adres URL logowania i identyfikator.</span><span class="sxs-lookup"><span data-stu-id="7b2d4-162">Update these values with hello actual Sign-on URL and Identifier.</span></span> <span data-ttu-id="7b2d4-163">W tym miejscu zalecamy możesz toouse hello unikatową wartość ciągu w hello Identifier.Contact [zespołem pomocy technicznej RolePoint](mailto:info@rolepoint.com) tooget hello wartość.</span><span class="sxs-lookup"><span data-stu-id="7b2d4-163">Here we suggest you toouse hello unique value of string in hello Identifier.Contact [RolePoint support team](mailto:info@rolepoint.com) tooget hello value.</span></span> 
 
4. <span data-ttu-id="7b2d4-164">Na powitania **certyfikat podpisywania SAML** kliknij **XML metadanych** , a następnie zapisz plik metadanych hello na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="7b2d4-164">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-rolepoint-tutorial/tutorial_rolepoint_certificate.png) 

5. <span data-ttu-id="7b2d4-166">Kliknij przycisk **zapisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="7b2d4-166">Click **Save** button.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-rolepoint-tutorial/tutorial_general_400.png)


6. <span data-ttu-id="7b2d4-168">tooconfigure rejestracji jednokrotnej w **RolePoint** strony, należy pobrać hello toosend **XML metadanych** za[zespołem pomocy technicznej RolePoint](mailto:info@rolepoint.com).</span><span class="sxs-lookup"><span data-stu-id="7b2d4-168">tooconfigure single sign-on on **RolePoint** side, you need toosend hello downloaded **Metadata XML** too[RolePoint support team](mailto:info@rolepoint.com).</span></span>

> [!TIP]
> <span data-ttu-id="7b2d4-169">Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz hello [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji hello!</span><span class="sxs-lookup"><span data-stu-id="7b2d4-169">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="7b2d4-170">Po dodaniu tej aplikacji z hello **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij hello **rejestracji jednokrotnej** hello kartę i dostępu do osadzonych dokumentacji za pośrednictwem hello  **Konfiguracja** sekcji u dołu hello.</span><span class="sxs-lookup"><span data-stu-id="7b2d4-170">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="7b2d4-171">Więcej o hello osadzonych dokumentacji funkcji w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="7b2d4-171">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="7b2d4-172">Tworzenie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="7b2d4-172">Creating an Azure AD test user</span></span>
<span data-ttu-id="7b2d4-173">Celem Hello w tej sekcji jest toocreate użytkownika testowego, w portalu Azure o nazwie Simona Britta hello.</span><span class="sxs-lookup"><span data-stu-id="7b2d4-173">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Tworzenie użytkowników usługi Azure AD][100]

<span data-ttu-id="7b2d4-175">**toocreate użytkownika testowego w usłudze Azure AD, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="7b2d4-175">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="7b2d4-176">W hello **portalu Azure**na temat hello w lewym okienku nawigacji, kliknij przycisk **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="7b2d4-176">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-rolepoint-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="7b2d4-178">toodisplay hello listę użytkowników, przejdź zbyt**użytkowników i grup** i kliknij przycisk **wszyscy użytkownicy**.</span><span class="sxs-lookup"><span data-stu-id="7b2d4-178">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-rolepoint-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="7b2d4-180">Witaj tooopen **użytkownika** okna dialogowego, kliknij przycisk **Dodaj** u góry hello hello okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="7b2d4-180">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-rolepoint-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="7b2d4-182">Na powitania **użytkownika** okna dialogowego wykonaj hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="7b2d4-182">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-rolepoint-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="7b2d4-184">a.</span><span class="sxs-lookup"><span data-stu-id="7b2d4-184">a.</span></span> <span data-ttu-id="7b2d4-185">W hello **nazwa** pole tekstowe, typ **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="7b2d4-185">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="7b2d4-186">b.</span><span class="sxs-lookup"><span data-stu-id="7b2d4-186">b.</span></span> <span data-ttu-id="7b2d4-187">W hello **nazwy użytkownika** pole tekstowe, hello typu **adres e-mail** z BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="7b2d4-187">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="7b2d4-188">c.</span><span class="sxs-lookup"><span data-stu-id="7b2d4-188">c.</span></span> <span data-ttu-id="7b2d4-189">Wybierz **Pokaż hasło** i zanotuj wartość hello hello **hasło**.</span><span class="sxs-lookup"><span data-stu-id="7b2d4-189">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="7b2d4-190">d.</span><span class="sxs-lookup"><span data-stu-id="7b2d4-190">d.</span></span> <span data-ttu-id="7b2d4-191">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="7b2d4-191">Click **Create**.</span></span>
 
### <a name="creating-a-rolepoint-test-user"></a><span data-ttu-id="7b2d4-192">Tworzenie użytkownika testowego RolePoint</span><span class="sxs-lookup"><span data-stu-id="7b2d4-192">Creating a RolePoint test user</span></span>

<span data-ttu-id="7b2d4-193">W tej sekcji należy utworzyć użytkownika o nazwie Simona Britta w RolePoint.</span><span class="sxs-lookup"><span data-stu-id="7b2d4-193">In this section, you create a user called Britta Simon in RolePoint.</span></span> <span data-ttu-id="7b2d4-194">Praca z [zespołem pomocy technicznej RolePoint](mailto:info@rolepoint.com) tooadd hello użytkowników hello RolePoint platformy.</span><span class="sxs-lookup"><span data-stu-id="7b2d4-194">Work with [RolePoint support team](mailto:info@rolepoint.com) tooadd hello users in hello RolePoint platform.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="7b2d4-195">Przypisanie użytkownika testowego hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="7b2d4-195">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="7b2d4-196">W tej sekcji możesz włączyć toouse Simona Britta Azure logowania jednokrotnego za udzielanie dostępu tooRolePoint.</span><span class="sxs-lookup"><span data-stu-id="7b2d4-196">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooRolePoint.</span></span>

![Przypisz użytkownika][200] 

<span data-ttu-id="7b2d4-198">**tooassign tooRolePoint Simona Britta wykonaj hello następujące kroki:**</span><span class="sxs-lookup"><span data-stu-id="7b2d4-198">**tooassign Britta Simon tooRolePoint, perform hello following steps:**</span></span>

1. <span data-ttu-id="7b2d4-199">W portalu Azure hello, otwórz widok aplikacji hello, a następnie przejdź do widoku katalogu toohello i przejść za**aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="7b2d4-199">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Przypisz użytkownika][201] 

2. <span data-ttu-id="7b2d4-201">Z listy aplikacji hello wybierz **RolePoint**.</span><span class="sxs-lookup"><span data-stu-id="7b2d4-201">In hello applications list, select **RolePoint**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-rolepoint-tutorial/tutorial_rolepoint_app.png) 

3. <span data-ttu-id="7b2d4-203">W menu powitania po lewej stronie powitania kliknij **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="7b2d4-203">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Przypisz użytkownika][202] 

4. <span data-ttu-id="7b2d4-205">Kliknij przycisk **Dodaj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="7b2d4-205">Click **Add** button.</span></span> <span data-ttu-id="7b2d4-206">Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="7b2d4-206">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Przypisz użytkownika][203]

5. <span data-ttu-id="7b2d4-208">Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** hello listy użytkowników.</span><span class="sxs-lookup"><span data-stu-id="7b2d4-208">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="7b2d4-209">Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="7b2d4-209">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="7b2d4-210">Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="7b2d4-210">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="7b2d4-211">Testowanie rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="7b2d4-211">Testing single sign-on</span></span>

<span data-ttu-id="7b2d4-212">W tej sekcji można przetestować konfiguracji usługi Azure AD pojedynczego logowania jednokrotnego przy użyciu hello panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="7b2d4-212">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="7b2d4-213">Po kliknięciu kafelka RolePoint hello w hello Panel dostępu, należy pobrać automatycznie zalogowane tooyour RolePoint aplikacji.</span><span class="sxs-lookup"><span data-stu-id="7b2d4-213">When you click hello RolePoint tile in hello Access Panel, you should get automatically signed-on tooyour RolePoint application.</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="7b2d4-214">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="7b2d4-214">Additional resources</span></span>

* [<span data-ttu-id="7b2d4-215">Lista samouczków dotyczących tooIntegrate aplikacji SaaS w usłudze Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="7b2d4-215">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="7b2d4-216">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="7b2d4-216">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-rolepoint-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-rolepoint-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-rolepoint-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-rolepoint-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-rolepoint-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-rolepoint-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-rolepoint-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-rolepoint-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-rolepoint-tutorial/tutorial_general_203.png

