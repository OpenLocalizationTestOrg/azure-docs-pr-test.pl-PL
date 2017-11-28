---
title: 'Samouczek: Integracji Azure Active Directory z Learning w miejscu pracy | Dokumentacja firmy Microsoft'
description: "Dowiedz się, jak tooconfigure logowanie jednokrotne między usługą Azure Active Directory i uczenie się w miejscu pracy."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 1d607174-bea1-4f40-8233-54cabe02c66a
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/02/2017
ms.author: jeedes
ms.openlocfilehash: fa09d585d57932a95cadba9a66029765d7df3694
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-learning-at-work"></a><span data-ttu-id="71063-103">Samouczek: Integracji Azure Active Directory z Learning w miejscu pracy</span><span class="sxs-lookup"><span data-stu-id="71063-103">Tutorial: Azure Active Directory integration with Learning at Work</span></span>

<span data-ttu-id="71063-104">Z tego samouczka, dowiesz się, jak toointegrate uczenia w pracy z usługą Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="71063-104">In this tutorial, you learn how toointegrate Learning at Work with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="71063-105">Integrowanie Learning w pracy z usługą Azure AD zapewnia hello następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="71063-105">Integrating Learning at Work with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="71063-106">Można kontrolować w usłudze Azure AD, który ma tooLearning dostęp w miejscu pracy</span><span class="sxs-lookup"><span data-stu-id="71063-106">You can control in Azure AD who has access tooLearning at Work</span></span>
- <span data-ttu-id="71063-107">Można włączyć użytkownika użytkownicy tooautomatically get zalogowane tooLearning w miejscu pracy (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="71063-107">You can enable your users tooautomatically get signed-on tooLearning at Work (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="71063-108">Możesz zarządzać kont w jednej centralnej lokalizacji - hello portalu Azure</span><span class="sxs-lookup"><span data-stu-id="71063-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="71063-109">Jeśli chcesz tooknow więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="71063-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="71063-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="71063-110">Prerequisites</span></span>

<span data-ttu-id="71063-111">tooconfigure integracji usługi Azure AD przy użyciu Learning w miejscu pracy, należy hello następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="71063-111">tooconfigure Azure AD integration with Learning at Work, you need hello following items:</span></span>

- <span data-ttu-id="71063-112">Subskrypcję usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="71063-112">An Azure AD subscription</span></span>
- <span data-ttu-id="71063-113">Learning w pracy jednokrotnego włączone subskrypcji</span><span class="sxs-lookup"><span data-stu-id="71063-113">A Learning at Work single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="71063-114">tootest hello kroków w tym samouczku, zaleca się przy użyciu środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="71063-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="71063-115">tootest hello kroki opisane w tym samouczku, należy stosować te zalecenia:</span><span class="sxs-lookup"><span data-stu-id="71063-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="71063-116">Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="71063-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="71063-117">Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz pobrać miesięczna wersja próbna [tutaj](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="71063-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="71063-118">Opis scenariusza</span><span class="sxs-lookup"><span data-stu-id="71063-118">Scenario description</span></span>
<span data-ttu-id="71063-119">W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym.</span><span class="sxs-lookup"><span data-stu-id="71063-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="71063-120">Scenariusz Hello opisane w tym samouczku składa się z dwóch głównych elementów:</span><span class="sxs-lookup"><span data-stu-id="71063-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="71063-121">Dodawanie Learning w pracy z galerii hello</span><span class="sxs-lookup"><span data-stu-id="71063-121">Adding Learning at Work from hello gallery</span></span>
2. <span data-ttu-id="71063-122">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="71063-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-learning-at-work-from-hello-gallery"></a><span data-ttu-id="71063-123">Dodawanie Learning w pracy z galerii hello</span><span class="sxs-lookup"><span data-stu-id="71063-123">Adding Learning at Work from hello gallery</span></span>
<span data-ttu-id="71063-124">integracji hello tooconfigure Learning w pracy z usługą Azure AD, należy tooadd uczenia w pracy z hello galerii tooyour listę zarządzanych aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="71063-124">tooconfigure hello integration of Learning at Work into Azure AD, you need tooadd Learning at Work from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="71063-125">**tooadd uczenia w pracy z galerii hello, wykonaj hello następujące kroki:**</span><span class="sxs-lookup"><span data-stu-id="71063-125">**tooadd Learning at Work from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="71063-126">W hello  **[portalu Azure](https://portal.azure.com)**na temat hello panelu nawigacji po lewej stronie, kliknij przycisk **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="71063-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Usługa Active Directory][1]

2. <span data-ttu-id="71063-128">Przejdź za**aplikacje dla przedsiębiorstw**.</span><span class="sxs-lookup"><span data-stu-id="71063-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="71063-129">Następnie przejdź zbyt**wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="71063-129">Then go too**All applications**.</span></span>

    ![Aplikacje][2]
    
3. <span data-ttu-id="71063-131">tooadd nową aplikację, kliknij przycisk **nowej aplikacji** przycisk u góry hello okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="71063-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplikacje][3]

4. <span data-ttu-id="71063-133">W polu wyszukiwania hello wpisz **uczenia w miejscu pracy**.</span><span class="sxs-lookup"><span data-stu-id="71063-133">In hello search box, type **Learning at Work**.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-learning-at-work-tutorial/tutorial_learningatwork_search.png)

5. <span data-ttu-id="71063-135">W panelu wyników hello, wybierz **uczenia w miejscu pracy**, a następnie kliknij przycisk **Dodaj** przycisk aplikacji hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="71063-135">In hello results panel, select **Learning at Work**, and then click **Add** button tooadd hello application.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-learning-at-work-tutorial/tutorial_learningatwork_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="71063-137">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="71063-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="71063-138">W tej sekcji możesz skonfigurować i przetestować usługi Azure AD logowania jednokrotnego przy użyciu Learning w miejscu pracy na podstawie użytkownika testowego, nazywany "Britta Simona".</span><span class="sxs-lookup"><span data-stu-id="71063-138">In this section, you configure and test Azure AD single sign-on with Learning at Work based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="71063-139">Dla pojedynczego logowania jednokrotnego toowork usługi Azure AD musi tooknow użytkownika odpowiednikiem hello w uczeniu w miejscu pracy jest tooa użytkownika w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="71063-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Learning at Work is tooa user in Azure AD.</span></span> <span data-ttu-id="71063-140">Innymi słowy relację łącza między użytkownika usługi Azure AD i hello użytkownikowi w uczeniu w miejscu pracy musi toobe ustanowione.</span><span class="sxs-lookup"><span data-stu-id="71063-140">In other words, a link relationship between an Azure AD user and hello related user in Learning at Work needs toobe established.</span></span>

<span data-ttu-id="71063-141">Ta relacja łącza zostanie nawiązane, przypisując wartość hello hello **nazwy użytkownika** w usłudze Azure AD jako wartość hello hello **Username** w uczeniu w miejscu pracy.</span><span class="sxs-lookup"><span data-stu-id="71063-141">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in Learning at Work.</span></span>

<span data-ttu-id="71063-142">tooconfigure i testowych usługi Azure AD logowania jednokrotnego przy użyciu Learning w miejscu pracy, należy po bloków konstrukcyjnych hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="71063-142">tooconfigure and test Azure AD single sign-on with Learning at Work, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="71063-143">**[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configuring-azure-ad-single-sign-on)**  -tooenable Twojego toouse użytkowników tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="71063-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="71063-144">**[Tworzenie użytkownika testowego usługi Azure AD](#creating-an-azure-ad-test-user)**  -tootest usługi Azure AD rejestracji jednokrotnej z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="71063-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="71063-145">**[Tworzenie uczenie na pracę użytkownika testowego](#creating-a-learning-at-work-test-user)**  -toohave odpowiednikiem Simona Britta w uczeniu w miejscu pracy, który jest połączony toohello usługi Azure AD reprezentację użytkownika.</span><span class="sxs-lookup"><span data-stu-id="71063-145">**[Creating a Learning at Work test user](#creating-a-learning-at-work-test-user)** - toohave a counterpart of Britta Simon in Learning at Work that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="71063-146">**[Przypisanie użytkownika testowego hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Simona Britta toouse usługi Azure AD rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="71063-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="71063-147">**[Testowanie rejestracji jednokrotnej](#testing-single-sign-on)**  -tooverify czy hello konfiguracji działania.</span><span class="sxs-lookup"><span data-stu-id="71063-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="71063-148">Konfigurowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="71063-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="71063-149">W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w hello portalu Azure i skonfigurować logowanie jednokrotne zapoznanie się w pracy aplikacji.</span><span class="sxs-lookup"><span data-stu-id="71063-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Learning at Work application.</span></span>

<span data-ttu-id="71063-150">**tooconfigure usługi Azure AD logowania jednokrotnego przy użyciu Learning w miejscu pracy, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="71063-150">**tooconfigure Azure AD single sign-on with Learning at Work, perform hello following steps:**</span></span>

1. <span data-ttu-id="71063-151">W portalu Azure na powitania hello **uczenia w miejscu pracy** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.</span><span class="sxs-lookup"><span data-stu-id="71063-151">In hello Azure portal, on hello **Learning at Work** application integration page, click **Single sign-on**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej][4]

2. <span data-ttu-id="71063-153">Na powitania **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** tooenable rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="71063-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-learning-at-work-tutorial/tutorial_learningatwork_samlbase.png)

3. <span data-ttu-id="71063-155">Na powitania **uczenia domeny pracy i adresy URL** sekcji, wykonaj następujące kroki hello:</span><span class="sxs-lookup"><span data-stu-id="71063-155">On hello **Learning at Work Domain and URLs** section, perform hello following steps:</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-learning-at-work-tutorial/tutorial_learningatwork_url.png)

    <span data-ttu-id="71063-157">a.</span><span class="sxs-lookup"><span data-stu-id="71063-157">a.</span></span> <span data-ttu-id="71063-158">W hello **adres URL logowania** tekstowym, wpisz adres URL za pomocą hello następującego wzorca:`https://<subdomain>.sabacloud.com/Saba/Web/<company code>`</span><span class="sxs-lookup"><span data-stu-id="71063-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<subdomain>.sabacloud.com/Saba/Web/<company code>`</span></span>

    <span data-ttu-id="71063-159">b.</span><span class="sxs-lookup"><span data-stu-id="71063-159">b.</span></span> <span data-ttu-id="71063-160">W hello **identyfikator** tekstowym, wpisz adres URL za pomocą hello następującego wzorca:`https://<subdomain>.sabacloud.com/Saba/saml/SSO/alias/<company name>`</span><span class="sxs-lookup"><span data-stu-id="71063-160">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<subdomain>.sabacloud.com/Saba/saml/SSO/alias/<company name>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="71063-161">Wartości te nie są hello prawdziwe.</span><span class="sxs-lookup"><span data-stu-id="71063-161">These values are not hello real.</span></span> <span data-ttu-id="71063-162">Zaktualizować te wartości z hello rzeczywisty adres URL logowania i identyfikator.</span><span class="sxs-lookup"><span data-stu-id="71063-162">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="71063-163">Skontaktuj się z [uczenia w zespół obsługi klienta pracy](https://www.learninga-z.com/site/contact/support) tooget tych wartości.</span><span class="sxs-lookup"><span data-stu-id="71063-163">Contact [Learning at Work Client support team](https://www.learninga-z.com/site/contact/support) tooget these values.</span></span> 
 
4. <span data-ttu-id="71063-164">Na powitania **certyfikat podpisywania SAML** kliknij **XML metadanych** , a następnie zapisz plik metadanych hello na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="71063-164">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-learning-at-work-tutorial/tutorial_learningatwork_certificate.png) 

5. <span data-ttu-id="71063-166">Kliknij przycisk **zapisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="71063-166">Click **Save** button.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-learning-at-work-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="71063-168">Na powitania **uczenia w konfiguracji pracy** kliknij **skonfigurować Learning w miejscu pracy** tooopen **Konfigurowanie logowania jednokrotnego** okna.</span><span class="sxs-lookup"><span data-stu-id="71063-168">On hello **Learning at Work Configuration** section, click **Configure Learning at Work** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="71063-169">Kopiuj hello **Sign-Out adres URL, identyfikator jednostki SAML i SAML pojedynczy znak na adres URL usługi** z hello **sekcji krótkimi opisami.**</span><span class="sxs-lookup"><span data-stu-id="71063-169">Copy hello **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-learning-at-work-tutorial/tutorial_learningatwork_configure.png) 

7. <span data-ttu-id="71063-171">tooconfigure rejestracji jednokrotnej w **uczenia w miejscu pracy** strony, należy pobrać hello toosend **XML metadanych**, **identyfikator jednostki SAML**, **SAML logowania jednokrotnego Adres URL usługi**, i **Sign-Out URL** za[uczenia w witrynie pomocy technicznej pracy](https://www.learninga-z.com/site/contact/support).</span><span class="sxs-lookup"><span data-stu-id="71063-171">tooconfigure single sign-on on **Learning at Work** side, you need toosend hello downloaded **Metadata XML**, **SAML Entity ID**, **SAML Single Sign-On Service URL**, and **Sign-Out URL** too[Learning at Work support](https://www.learninga-z.com/site/contact/support).</span></span>

> [!TIP]
> <span data-ttu-id="71063-172">Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz hello [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji hello!</span><span class="sxs-lookup"><span data-stu-id="71063-172">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="71063-173">Po dodaniu tej aplikacji z hello **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij hello **rejestracji jednokrotnej** hello kartę i dostępu do osadzonych dokumentacji za pośrednictwem hello  **Konfiguracja** sekcji u dołu hello.</span><span class="sxs-lookup"><span data-stu-id="71063-173">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="71063-174">Więcej o hello osadzonych dokumentacji funkcji w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="71063-174">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="71063-175">Tworzenie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="71063-175">Creating an Azure AD test user</span></span>
<span data-ttu-id="71063-176">Celem Hello w tej sekcji jest toocreate użytkownika testowego, w portalu Azure o nazwie Simona Britta hello.</span><span class="sxs-lookup"><span data-stu-id="71063-176">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Tworzenie użytkowników usługi Azure AD][100]

<span data-ttu-id="71063-178">**toocreate użytkownika testowego w usłudze Azure AD, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="71063-178">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="71063-179">W hello **portalu Azure**na temat hello w lewym okienku nawigacji, kliknij przycisk **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="71063-179">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-learning-at-work-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="71063-181">toodisplay hello listę użytkowników, przejdź zbyt**użytkowników i grup** i kliknij przycisk **wszyscy użytkownicy**.</span><span class="sxs-lookup"><span data-stu-id="71063-181">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-learning-at-work-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="71063-183">Witaj tooopen **użytkownika** okna dialogowego, kliknij przycisk **Dodaj** u góry hello hello okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="71063-183">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-learning-at-work-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="71063-185">Na powitania **użytkownika** okna dialogowego wykonaj hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="71063-185">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-learning-at-work-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="71063-187">a.</span><span class="sxs-lookup"><span data-stu-id="71063-187">a.</span></span> <span data-ttu-id="71063-188">W hello **nazwa** pole tekstowe, typ **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="71063-188">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="71063-189">b.</span><span class="sxs-lookup"><span data-stu-id="71063-189">b.</span></span> <span data-ttu-id="71063-190">W hello **nazwy użytkownika** pole tekstowe, hello typu **adres e-mail** z BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="71063-190">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="71063-191">c.</span><span class="sxs-lookup"><span data-stu-id="71063-191">c.</span></span> <span data-ttu-id="71063-192">Wybierz **Pokaż hasło** i zanotuj wartość hello hello **hasło**.</span><span class="sxs-lookup"><span data-stu-id="71063-192">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="71063-193">d.</span><span class="sxs-lookup"><span data-stu-id="71063-193">d.</span></span> <span data-ttu-id="71063-194">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="71063-194">Click **Create**.</span></span>
 
### <a name="creating-a-learning-at-work-test-user"></a><span data-ttu-id="71063-195">Tworzenie uczenie na pracę użytkownika testowego</span><span class="sxs-lookup"><span data-stu-id="71063-195">Creating a Learning at Work test user</span></span>

<span data-ttu-id="71063-196">W tej sekcji należy utworzyć użytkownika o nazwie Simona Britta w uczeniu w miejscu pracy.</span><span class="sxs-lookup"><span data-stu-id="71063-196">In this section, you create a user called Britta Simon in Learning at Work.</span></span> <span data-ttu-id="71063-197">Praca z [uczenia w witrynie pomocy technicznej pracy](https://www.learninga-z.com/site/contact/support) tooadd hello użytkowników w hello Learning na platformie pracy.</span><span class="sxs-lookup"><span data-stu-id="71063-197">Work with [Learning at Work support](https://www.learninga-z.com/site/contact/support) tooadd hello users in hello Learning at Work platform.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="71063-198">Przypisanie użytkownika testowego hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="71063-198">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="71063-199">W tej sekcji możesz włączyć toouse Simona Britta Azure logowania jednokrotnego za udzielanie dostępu tooLearning w miejscu pracy.</span><span class="sxs-lookup"><span data-stu-id="71063-199">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooLearning at Work.</span></span>

![Przypisz użytkownika][200] 

<span data-ttu-id="71063-201">**tooassign tooLearning Simona Britta w miejscu pracy, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="71063-201">**tooassign Britta Simon tooLearning at Work, perform hello following steps:**</span></span>

1. <span data-ttu-id="71063-202">W portalu Azure hello, otwórz widok aplikacji hello, a następnie przejdź do widoku katalogu toohello i przejść za**aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="71063-202">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Przypisz użytkownika][201] 

2. <span data-ttu-id="71063-204">Z listy aplikacji hello wybierz **uczenia w miejscu pracy**.</span><span class="sxs-lookup"><span data-stu-id="71063-204">In hello applications list, select **Learning at Work**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-learning-at-work-tutorial/tutorial_learningatwork_app.png) 

3. <span data-ttu-id="71063-206">W menu powitania po lewej stronie powitania kliknij **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="71063-206">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Przypisz użytkownika][202] 

4. <span data-ttu-id="71063-208">Kliknij przycisk **Dodaj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="71063-208">Click **Add** button.</span></span> <span data-ttu-id="71063-209">Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="71063-209">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Przypisz użytkownika][203]

5. <span data-ttu-id="71063-211">Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** hello listy użytkowników.</span><span class="sxs-lookup"><span data-stu-id="71063-211">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="71063-212">Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="71063-212">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="71063-213">Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="71063-213">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="71063-214">Testowanie rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="71063-214">Testing single sign-on</span></span>

<span data-ttu-id="71063-215">W tej sekcji można przetestować konfiguracji usługi Azure AD pojedynczego logowania jednokrotnego przy użyciu hello panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="71063-215">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="71063-216">Po kliknięciu hello uczenia na kafelku pracy w hello Panel dostępu, należy pobrać automatycznie zalogowane tooyour uczenia w pracy aplikacji.</span><span class="sxs-lookup"><span data-stu-id="71063-216">When you click hello Learning at Work tile in hello Access Panel, you should get automatically signed-on tooyour Learning at Work application.</span></span>
<span data-ttu-id="71063-217">Aby uzyskać więcej informacji na temat hello Panel dostępu, zobacz [toohello wprowadzenie panelu dostępu](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="71063-217">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="71063-218">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="71063-218">Additional resources</span></span>

* [<span data-ttu-id="71063-219">Lista samouczków dotyczących tooIntegrate aplikacji SaaS w usłudze Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="71063-219">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="71063-220">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="71063-220">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-learning-at-work-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-learning-at-work-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-learning-at-work-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-learning-at-work-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-learning-at-work-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-learning-at-work-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-learning-at-work-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-learning-at-work-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-learning-at-work-tutorial/tutorial_general_203.png

