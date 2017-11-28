---
title: 'Samouczek: Integracji Azure Active Directory z Mindflash | Dokumentacja firmy Microsoft'
description: "Dowiedz się, jak tooconfigure logowanie jednokrotne między usługą Azure Active Directory i Mindflash."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: bdf91993-aaaa-4598-89b7-77ef8ca065d5
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/30/2017
ms.author: jeedes
ms.openlocfilehash: a1bc327ea3867287103acbb64d30f0a8d7d4c5e9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-mindflash"></a><span data-ttu-id="48ea7-103">Samouczek: Integracji Azure Active Directory z Mindflash</span><span class="sxs-lookup"><span data-stu-id="48ea7-103">Tutorial: Azure Active Directory integration with Mindflash</span></span>

<span data-ttu-id="48ea7-104">Z tego samouczka, dowiesz się, jak toointegrate Mindflash w usłudze Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="48ea7-104">In this tutorial, you learn how toointegrate Mindflash with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="48ea7-105">Integracja z usługą Azure AD Mindflash zapewnia hello następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="48ea7-105">Integrating Mindflash with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="48ea7-106">Można kontrolować w usłudze Azure AD, kto ma dostęp do tooMindflash</span><span class="sxs-lookup"><span data-stu-id="48ea7-106">You can control in Azure AD who has access tooMindflash</span></span>
- <span data-ttu-id="48ea7-107">Można włączyć użytkownika użytkownicy tooautomatically get zalogowane tooMindflash (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="48ea7-107">You can enable your users tooautomatically get signed-on tooMindflash (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="48ea7-108">Możesz zarządzać kont w jednej centralnej lokalizacji - hello portalu Azure</span><span class="sxs-lookup"><span data-stu-id="48ea7-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="48ea7-109">Jeśli chcesz tooknow więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="48ea7-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="48ea7-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="48ea7-110">Prerequisites</span></span>

<span data-ttu-id="48ea7-111">tooconfigure integracji z usługą Azure AD z Mindflash należy hello następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="48ea7-111">tooconfigure Azure AD integration with Mindflash, you need hello following items:</span></span>

- <span data-ttu-id="48ea7-112">Subskrypcję usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="48ea7-112">An Azure AD subscription</span></span>
- <span data-ttu-id="48ea7-113">Mindflash logowanie jednokrotne włączone subskrypcji</span><span class="sxs-lookup"><span data-stu-id="48ea7-113">A Mindflash single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="48ea7-114">tootest hello kroków w tym samouczku, zaleca się przy użyciu środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="48ea7-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="48ea7-115">tootest hello kroki opisane w tym samouczku, należy stosować te zalecenia:</span><span class="sxs-lookup"><span data-stu-id="48ea7-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="48ea7-116">Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="48ea7-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="48ea7-117">Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz pobrać miesięczna wersja próbna [tutaj](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="48ea7-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="48ea7-118">Opis scenariusza</span><span class="sxs-lookup"><span data-stu-id="48ea7-118">Scenario description</span></span>
<span data-ttu-id="48ea7-119">W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym.</span><span class="sxs-lookup"><span data-stu-id="48ea7-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="48ea7-120">Scenariusz Hello opisane w tym samouczku składa się z dwóch głównych elementów:</span><span class="sxs-lookup"><span data-stu-id="48ea7-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="48ea7-121">Dodawanie Mindflash z galerii hello</span><span class="sxs-lookup"><span data-stu-id="48ea7-121">Adding Mindflash from hello gallery</span></span>
2. <span data-ttu-id="48ea7-122">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="48ea7-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-mindflash-from-hello-gallery"></a><span data-ttu-id="48ea7-123">Dodawanie Mindflash z galerii hello</span><span class="sxs-lookup"><span data-stu-id="48ea7-123">Adding Mindflash from hello gallery</span></span>
<span data-ttu-id="48ea7-124">tooconfigure hello integracji Mindflash do usługi Azure AD, należy tooadd Mindflash z hello galerii tooyour listę zarządzanych aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="48ea7-124">tooconfigure hello integration of Mindflash into Azure AD, you need tooadd Mindflash from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="48ea7-125">**tooadd Mindflash z galerii hello, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="48ea7-125">**tooadd Mindflash from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="48ea7-126">W hello  **[portalu Azure](https://portal.azure.com)**na temat hello panelu nawigacji po lewej stronie, kliknij przycisk **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="48ea7-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Usługa Active Directory][1]

2. <span data-ttu-id="48ea7-128">Przejdź za**aplikacje dla przedsiębiorstw**.</span><span class="sxs-lookup"><span data-stu-id="48ea7-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="48ea7-129">Następnie przejdź zbyt**wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="48ea7-129">Then go too**All applications**.</span></span>

    ![Aplikacje][2]
    
3. <span data-ttu-id="48ea7-131">tooadd nową aplikację, kliknij przycisk **nowej aplikacji** przycisk u góry hello okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="48ea7-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplikacje][3]

4. <span data-ttu-id="48ea7-133">W polu wyszukiwania hello wpisz **Mindflash**.</span><span class="sxs-lookup"><span data-stu-id="48ea7-133">In hello search box, type **Mindflash**.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-mindflash-tutorial/tutorial_mindflash_search.png)

5. <span data-ttu-id="48ea7-135">W panelu wyników hello zaznacz **Mindflash**, a następnie kliknij przycisk **Dodaj** przycisk aplikacji hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="48ea7-135">In hello results panel, select **Mindflash**, and then click **Add** button tooadd hello application.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-mindflash-tutorial/tutorial_mindflash_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="48ea7-137">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="48ea7-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="48ea7-138">W tej sekcji skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z Mindflash w oparciu o nazwie "Britta Simona" użytkownika testowego.</span><span class="sxs-lookup"><span data-stu-id="48ea7-138">In this section, you configure and test Azure AD single sign-on with Mindflash based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="48ea7-139">Dla pojedynczego logowania jednokrotnego toowork usługi Azure AD musi tooknow użytkownika odpowiednikiem hello w Mindflash jest tooa użytkownika w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="48ea7-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Mindflash is tooa user in Azure AD.</span></span> <span data-ttu-id="48ea7-140">Innymi słowy relację łącza między użytkownika usługi Azure AD i hello użytkownikowi w Mindflash musi toobe ustanowione.</span><span class="sxs-lookup"><span data-stu-id="48ea7-140">In other words, a link relationship between an Azure AD user and hello related user in Mindflash needs toobe established.</span></span>

<span data-ttu-id="48ea7-141">W Mindflash, należy przypisać wartość hello hello **nazwy użytkownika** w usłudze Azure AD jako wartość hello hello **Username** tooestablish hello łącze relacji.</span><span class="sxs-lookup"><span data-stu-id="48ea7-141">In Mindflash, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="48ea7-142">tooconfigure i testowych usługi Azure AD rejestracji jednokrotnej z Mindflash, należy po bloków konstrukcyjnych hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="48ea7-142">tooconfigure and test Azure AD single sign-on with Mindflash, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="48ea7-143">**[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configuring-azure-ad-single-sign-on)**  -tooenable Twojego toouse użytkowników tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="48ea7-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="48ea7-144">**[Tworzenie użytkownika testowego usługi Azure AD](#creating-an-azure-ad-test-user)**  -tootest usługi Azure AD rejestracji jednokrotnej z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="48ea7-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="48ea7-145">**[Tworzenie użytkownika testowego Mindflash](#creating-a-mindflash-test-user)**  -toohave odpowiednikiem Simona Britta w Mindflash, który jest połączony toohello usługi Azure AD reprezentację użytkownika.</span><span class="sxs-lookup"><span data-stu-id="48ea7-145">**[Creating a Mindflash test user](#creating-a-mindflash-test-user)** - toohave a counterpart of Britta Simon in Mindflash that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="48ea7-146">**[Przypisanie użytkownika testowego hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Simona Britta toouse usługi Azure AD rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="48ea7-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="48ea7-147">**[Testowanie rejestracji jednokrotnej](#testing-single-sign-on)**  -tooverify czy hello konfiguracji działania.</span><span class="sxs-lookup"><span data-stu-id="48ea7-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="48ea7-148">Konfigurowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="48ea7-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="48ea7-149">W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w portalu Azure hello i skonfigurować logowanie jednokrotne w aplikacji Mindflash.</span><span class="sxs-lookup"><span data-stu-id="48ea7-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Mindflash application.</span></span>

<span data-ttu-id="48ea7-150">**tooconfigure usługi Azure AD rejestracji jednokrotnej z Mindflash, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="48ea7-150">**tooconfigure Azure AD single sign-on with Mindflash, perform hello following steps:**</span></span>

1. <span data-ttu-id="48ea7-151">W portalu Azure na powitania hello **Mindflash** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.</span><span class="sxs-lookup"><span data-stu-id="48ea7-151">In hello Azure portal, on hello **Mindflash** application integration page, click **Single sign-on**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej][4]

2. <span data-ttu-id="48ea7-153">Na powitania **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** tooenable rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="48ea7-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-mindflash-tutorial/tutorial_mindflash_samlbase.png)

3. <span data-ttu-id="48ea7-155">Na powitania **Mindflash domeny i adres URL** sekcji, wykonaj następujące kroki hello:</span><span class="sxs-lookup"><span data-stu-id="48ea7-155">On hello **Mindflash Domain and URLs** section, perform hello following steps:</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-mindflash-tutorial/tutorial_mindflash_url.png)

    <span data-ttu-id="48ea7-157">a.</span><span class="sxs-lookup"><span data-stu-id="48ea7-157">a.</span></span> <span data-ttu-id="48ea7-158">W hello **adres URL logowania** tekstowym, wpisz adres URL za pomocą hello następującego wzorca:`https://<companyname>.mindflash.com`</span><span class="sxs-lookup"><span data-stu-id="48ea7-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<companyname>.mindflash.com`</span></span>

    <span data-ttu-id="48ea7-159">b.</span><span class="sxs-lookup"><span data-stu-id="48ea7-159">b.</span></span> <span data-ttu-id="48ea7-160">W hello **identyfikator** tekstowym, wpisz adres URL za pomocą hello następującego wzorca:`https://<companyname>.mindflash.com`</span><span class="sxs-lookup"><span data-stu-id="48ea7-160">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<companyname>.mindflash.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="48ea7-161">Wartości te nie są prawdziwe.</span><span class="sxs-lookup"><span data-stu-id="48ea7-161">These values are not real.</span></span> <span data-ttu-id="48ea7-162">Zaktualizować te wartości z hello rzeczywisty adres URL logowania i identyfikator.</span><span class="sxs-lookup"><span data-stu-id="48ea7-162">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="48ea7-163">Skontaktuj się z [zespołem pomocy technicznej klienta Mindflash](https://www.mindflash.com/contact/) tooget tych wartości.</span><span class="sxs-lookup"><span data-stu-id="48ea7-163">Contact [Mindflash Client support team](https://www.mindflash.com/contact/) tooget these values.</span></span> 
 


4. <span data-ttu-id="48ea7-164">Na powitania **certyfikat podpisywania SAML** kliknij **XML metadanych** , a następnie zapisz plik metadanych hello na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="48ea7-164">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-mindflash-tutorial/tutorial_mindflash_certificate.png) 

5. <span data-ttu-id="48ea7-166">Kliknij przycisk **zapisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="48ea7-166">Click **Save** button.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-mindflash-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="48ea7-168">tooconfigure rejestracji jednokrotnej w **Mindflash** strony, należy pobrać hello toosend **XML metadanych** za[zespołem pomocy technicznej Mindflash](https://www.mindflash.com/contact/).</span><span class="sxs-lookup"><span data-stu-id="48ea7-168">tooconfigure single sign-on on **Mindflash** side, you need toosend hello downloaded **Metadata XML** too[Mindflash support team](https://www.mindflash.com/contact/).</span></span>

> [!TIP]
> <span data-ttu-id="48ea7-169">Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz hello [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji hello!</span><span class="sxs-lookup"><span data-stu-id="48ea7-169">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="48ea7-170">Po dodaniu tej aplikacji z hello **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij hello **rejestracji jednokrotnej** hello kartę i dostępu do osadzonych dokumentacji za pośrednictwem hello  **Konfiguracja** sekcji u dołu hello.</span><span class="sxs-lookup"><span data-stu-id="48ea7-170">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="48ea7-171">Więcej o hello osadzonych dokumentacji funkcji w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="48ea7-171">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="48ea7-172">Tworzenie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="48ea7-172">Creating an Azure AD test user</span></span>
<span data-ttu-id="48ea7-173">Celem Hello w tej sekcji jest toocreate użytkownika testowego, w portalu Azure o nazwie Simona Britta hello.</span><span class="sxs-lookup"><span data-stu-id="48ea7-173">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Tworzenie użytkowników usługi Azure AD][100]

<span data-ttu-id="48ea7-175">**toocreate użytkownika testowego w usłudze Azure AD, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="48ea7-175">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="48ea7-176">W hello **portalu Azure**na temat hello w lewym okienku nawigacji, kliknij przycisk **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="48ea7-176">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-mindflash-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="48ea7-178">toodisplay hello listę użytkowników, przejdź zbyt**użytkowników i grup** i kliknij przycisk **wszyscy użytkownicy**.</span><span class="sxs-lookup"><span data-stu-id="48ea7-178">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-mindflash-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="48ea7-180">Witaj tooopen **użytkownika** okna dialogowego, kliknij przycisk **Dodaj** u góry hello hello okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="48ea7-180">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-mindflash-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="48ea7-182">Na powitania **użytkownika** okna dialogowego wykonaj hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="48ea7-182">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-mindflash-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="48ea7-184">a.</span><span class="sxs-lookup"><span data-stu-id="48ea7-184">a.</span></span> <span data-ttu-id="48ea7-185">W hello **nazwa** pole tekstowe, typ **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="48ea7-185">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="48ea7-186">b.</span><span class="sxs-lookup"><span data-stu-id="48ea7-186">b.</span></span> <span data-ttu-id="48ea7-187">W hello **nazwy użytkownika** pole tekstowe, hello typu **adres e-mail** z BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="48ea7-187">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="48ea7-188">c.</span><span class="sxs-lookup"><span data-stu-id="48ea7-188">c.</span></span> <span data-ttu-id="48ea7-189">Wybierz **Pokaż hasło** i zanotuj wartość hello hello **hasło**.</span><span class="sxs-lookup"><span data-stu-id="48ea7-189">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="48ea7-190">d.</span><span class="sxs-lookup"><span data-stu-id="48ea7-190">d.</span></span> <span data-ttu-id="48ea7-191">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="48ea7-191">Click **Create**.</span></span>
 
### <a name="creating-a-mindflash-test-user"></a><span data-ttu-id="48ea7-192">Tworzenie użytkownika testowego Mindflash</span><span class="sxs-lookup"><span data-stu-id="48ea7-192">Creating a Mindflash test user</span></span>

<span data-ttu-id="48ea7-193">W przypadku użytkowników usługi Azure AD toolog kolejności tooenable do Mindflash muszą mieć przydzielone do Mindflash.</span><span class="sxs-lookup"><span data-stu-id="48ea7-193">In order tooenable Azure AD users toolog into Mindflash, they must be provisioned into Mindflash.</span></span> <span data-ttu-id="48ea7-194">W przypadku hello Mindflash Inicjowanie obsługi to zadanie ręczne.</span><span class="sxs-lookup"><span data-stu-id="48ea7-194">In hello case of Mindflash, provisioning is a manual task.</span></span>

### <a name="tooprovision-a-user-accounts-perform-hello-following-steps"></a><span data-ttu-id="48ea7-195">tooprovision kont użytkowników, wykonaj hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="48ea7-195">tooprovision a user accounts, perform hello following steps:</span></span>

1. <span data-ttu-id="48ea7-196">Zaloguj się za tooyour **Mindflash** witryny firmy jako administrator.</span><span class="sxs-lookup"><span data-stu-id="48ea7-196">Log in tooyour **Mindflash** company site as an administrator.</span></span>

2. <span data-ttu-id="48ea7-197">Przejdź za**Zarządzanie użytkownikami**.</span><span class="sxs-lookup"><span data-stu-id="48ea7-197">Go too**Manage Users**.</span></span>
   
    <span data-ttu-id="48ea7-198">![Zarządzaj użytkownikami](./media/active-directory-saas-mindflash-tutorial/ic787140.png "Zarządzanie użytkownikami")</span><span class="sxs-lookup"><span data-stu-id="48ea7-198">![Manage Users](./media/active-directory-saas-mindflash-tutorial/ic787140.png "Manage Users")</span></span>

3. <span data-ttu-id="48ea7-199">Kliknij przycisk hello **Dodaj użytkowników**, a następnie kliknij przycisk **nowy**.</span><span class="sxs-lookup"><span data-stu-id="48ea7-199">Click hello **Add Users**, and then click **New**.</span></span>

4. <span data-ttu-id="48ea7-200">W hello **Dodaj nowych użytkowników** sekcji, wykonaj następujące kroki prawidłowy Azure hello konta AD ma tooprovision:</span><span class="sxs-lookup"><span data-stu-id="48ea7-200">In hello **Add New Users** section, perform hello following steps of a valid Azure AD account you want tooprovision:</span></span>
   
    <span data-ttu-id="48ea7-201">![Dodawanie nowych użytkowników](./media/active-directory-saas-mindflash-tutorial/ic787141.png "Dodawanie nowych użytkowników")</span><span class="sxs-lookup"><span data-stu-id="48ea7-201">![Add New Users](./media/active-directory-saas-mindflash-tutorial/ic787141.png "Add New Users")</span></span>
   
    <span data-ttu-id="48ea7-202">a.</span><span class="sxs-lookup"><span data-stu-id="48ea7-202">a.</span></span> <span data-ttu-id="48ea7-203">W hello **imię** pole tekstowe, typ **imię** hello użytkownika jako **Britta**.</span><span class="sxs-lookup"><span data-stu-id="48ea7-203">In hello **First name** textbox, type **First name** of hello user as **Britta**.</span></span>

    <span data-ttu-id="48ea7-204">b.</span><span class="sxs-lookup"><span data-stu-id="48ea7-204">b.</span></span> <span data-ttu-id="48ea7-205">W hello **nazwisko** pole tekstowe, typ **nazwisko** hello użytkownika jako **Simona**.</span><span class="sxs-lookup"><span data-stu-id="48ea7-205">In hello **Last name** textbox, type **Last name** of hello user as **Simon**.</span></span>
    
    <span data-ttu-id="48ea7-206">c.</span><span class="sxs-lookup"><span data-stu-id="48ea7-206">c.</span></span> <span data-ttu-id="48ea7-207">W hello **E-mail** pole tekstowe, typ **adres E-mail** hello użytkownika jako  **BrittaSimon@contoso.com** .</span><span class="sxs-lookup"><span data-stu-id="48ea7-207">In hello **Email** textbox, type **Email Address** of hello user as **BrittaSimon@contoso.com**.</span></span>

    <span data-ttu-id="48ea7-208">b.</span><span class="sxs-lookup"><span data-stu-id="48ea7-208">b.</span></span> <span data-ttu-id="48ea7-209">Kliknij pozycję **Dodaj**.</span><span class="sxs-lookup"><span data-stu-id="48ea7-209">Click **Add**.</span></span>

>[!NOTE]
><span data-ttu-id="48ea7-210">Możesz użyć innych Mindflash użytkownika konta tworzenia narzędzi lub interfejsów API dostarczonych przez Mindflash tooprovision kont użytkowników usługi AAD.</span><span class="sxs-lookup"><span data-stu-id="48ea7-210">You can use any other Mindflash user account creation tools or APIs provided by Mindflash tooprovision AAD user accounts.</span></span> 
> 

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="48ea7-211">Przypisanie użytkownika testowego hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="48ea7-211">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="48ea7-212">W tej sekcji możesz włączyć toouse Simona Britta Azure logowania jednokrotnego za udzielanie dostępu tooMindflash.</span><span class="sxs-lookup"><span data-stu-id="48ea7-212">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooMindflash.</span></span>

![Przypisz użytkownika][200] 

<span data-ttu-id="48ea7-214">**tooassign tooMindflash Simona Britta wykonaj hello następujące kroki:**</span><span class="sxs-lookup"><span data-stu-id="48ea7-214">**tooassign Britta Simon tooMindflash, perform hello following steps:**</span></span>

1. <span data-ttu-id="48ea7-215">W portalu Azure hello, otwórz widok aplikacji hello, a następnie przejdź do widoku katalogu toohello i przejść za**aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="48ea7-215">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Przypisz użytkownika][201] 

2. <span data-ttu-id="48ea7-217">Z listy aplikacji hello wybierz **Mindflash**.</span><span class="sxs-lookup"><span data-stu-id="48ea7-217">In hello applications list, select **Mindflash**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-mindflash-tutorial/tutorial_mindflash_app.png) 

3. <span data-ttu-id="48ea7-219">W menu powitania po lewej stronie powitania kliknij **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="48ea7-219">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Przypisz użytkownika][202] 

4. <span data-ttu-id="48ea7-221">Kliknij przycisk **Dodaj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="48ea7-221">Click **Add** button.</span></span> <span data-ttu-id="48ea7-222">Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="48ea7-222">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Przypisz użytkownika][203]

5. <span data-ttu-id="48ea7-224">Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** hello listy użytkowników.</span><span class="sxs-lookup"><span data-stu-id="48ea7-224">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="48ea7-225">Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="48ea7-225">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="48ea7-226">Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="48ea7-226">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="48ea7-227">Testowanie rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="48ea7-227">Testing single sign-on</span></span>

<span data-ttu-id="48ea7-228">W tej sekcji można przetestować konfiguracji usługi Azure AD pojedynczego logowania jednokrotnego przy użyciu hello panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="48ea7-228">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="48ea7-229">Po kliknięciu kafelka Mindflash hello w hello Panel dostępu, należy pobrać strony logowania Mindflash aplikacji.</span><span class="sxs-lookup"><span data-stu-id="48ea7-229">When you click hello Mindflash tile in hello Access Panel, you should get login page of Mindflash application.</span></span>
<span data-ttu-id="48ea7-230">Aby uzyskać więcej informacji na temat hello Panel dostępu, zobacz [toohello wprowadzenie panelu dostępu](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="48ea7-230">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="48ea7-231">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="48ea7-231">Additional resources</span></span>

* [<span data-ttu-id="48ea7-232">Lista samouczków dotyczących tooIntegrate aplikacji SaaS w usłudze Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="48ea7-232">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="48ea7-233">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="48ea7-233">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-mindflash-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-mindflash-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-mindflash-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-mindflash-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-mindflash-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-mindflash-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-mindflash-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-mindflash-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-mindflash-tutorial/tutorial_general_203.png

