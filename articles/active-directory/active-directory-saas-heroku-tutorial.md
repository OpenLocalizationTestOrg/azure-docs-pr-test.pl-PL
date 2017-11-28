---
title: 'Samouczek: Integracji Azure Active Directory z Heroku | Dokumentacja firmy Microsoft'
description: "Dowiedz się, jak tooconfigure logowanie jednokrotne między usługą Azure Active Directory i Heroku."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: d7d72ec6-4a60-4524-8634-26d8fbbcc833
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/30/2017
ms.author: jeedes
ms.openlocfilehash: ee11db647fd385140f1dbcab2586dfafffe5d912
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-heroku"></a><span data-ttu-id="32eca-103">Samouczek: Integracji Azure Active Directory z Heroku</span><span class="sxs-lookup"><span data-stu-id="32eca-103">Tutorial: Azure Active Directory integration with Heroku</span></span>

<span data-ttu-id="32eca-104">Z tego samouczka, dowiesz się, jak toointegrate Heroku w usłudze Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="32eca-104">In this tutorial, you learn how toointegrate Heroku with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="32eca-105">Integracja z usługą Azure AD Heroku zapewnia hello następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="32eca-105">Integrating Heroku with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="32eca-106">Można kontrolować w usłudze Azure AD, kto ma dostęp do tooHeroku</span><span class="sxs-lookup"><span data-stu-id="32eca-106">You can control in Azure AD who has access tooHeroku</span></span>
- <span data-ttu-id="32eca-107">Można włączyć użytkownika użytkownicy tooautomatically get zalogowane tooHeroku (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="32eca-107">You can enable your users tooautomatically get signed-on tooHeroku (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="32eca-108">Możesz zarządzać kont w jednej centralnej lokalizacji - hello portalu Azure</span><span class="sxs-lookup"><span data-stu-id="32eca-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="32eca-109">Jeśli chcesz tooknow więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="32eca-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="32eca-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="32eca-110">Prerequisites</span></span>

<span data-ttu-id="32eca-111">tooconfigure integracji z usługą Azure AD z Heroku należy hello następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="32eca-111">tooconfigure Azure AD integration with Heroku, you need hello following items:</span></span>

- <span data-ttu-id="32eca-112">Subskrypcję usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="32eca-112">An Azure AD subscription</span></span>
- <span data-ttu-id="32eca-113">Heroku logowanie jednokrotne włączone subskrypcji</span><span class="sxs-lookup"><span data-stu-id="32eca-113">A Heroku single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="32eca-114">tootest hello kroków w tym samouczku, zaleca się przy użyciu środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="32eca-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="32eca-115">tootest hello kroki opisane w tym samouczku, należy stosować te zalecenia:</span><span class="sxs-lookup"><span data-stu-id="32eca-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="32eca-116">Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="32eca-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="32eca-117">Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz pobrać miesięczna wersja próbna [tutaj](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="32eca-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="32eca-118">Opis scenariusza</span><span class="sxs-lookup"><span data-stu-id="32eca-118">Scenario description</span></span>
<span data-ttu-id="32eca-119">W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym.</span><span class="sxs-lookup"><span data-stu-id="32eca-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="32eca-120">Scenariusz Hello opisane w tym samouczku składa się z dwóch głównych elementów:</span><span class="sxs-lookup"><span data-stu-id="32eca-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="32eca-121">Dodawanie Heroku z galerii hello</span><span class="sxs-lookup"><span data-stu-id="32eca-121">Adding Heroku from hello gallery</span></span>
2. <span data-ttu-id="32eca-122">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="32eca-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-heroku-from-hello-gallery"></a><span data-ttu-id="32eca-123">Dodawanie Heroku z galerii hello</span><span class="sxs-lookup"><span data-stu-id="32eca-123">Adding Heroku from hello gallery</span></span>
<span data-ttu-id="32eca-124">tooconfigure hello integracji Heroku do usługi Azure AD, należy tooadd Heroku z hello galerii tooyour listę zarządzanych aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="32eca-124">tooconfigure hello integration of Heroku into Azure AD, you need tooadd Heroku from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="32eca-125">**tooadd Heroku z galerii hello, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="32eca-125">**tooadd Heroku from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="32eca-126">W hello  **[portalu Azure](https://portal.azure.com)**na temat hello panelu nawigacji po lewej stronie, kliknij przycisk **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="32eca-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Usługa Active Directory][1]

2. <span data-ttu-id="32eca-128">Przejdź za**aplikacje dla przedsiębiorstw**.</span><span class="sxs-lookup"><span data-stu-id="32eca-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="32eca-129">Następnie przejdź zbyt**wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="32eca-129">Then go too**All applications**.</span></span>

    ![Aplikacje][2]
    
3. <span data-ttu-id="32eca-131">tooadd nową aplikację, kliknij przycisk **nowej aplikacji** przycisk u góry hello okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="32eca-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplikacje][3]

4. <span data-ttu-id="32eca-133">W polu wyszukiwania hello wpisz **Heroku**.</span><span class="sxs-lookup"><span data-stu-id="32eca-133">In hello search box, type **Heroku**.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-heroku-tutorial/tutorial_heroku_search.png)

5. <span data-ttu-id="32eca-135">W panelu wyników hello zaznacz **Heroku**, a następnie kliknij przycisk **Dodaj** przycisk aplikacji hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="32eca-135">In hello results panel, select **Heroku**, and then click **Add** button tooadd hello application.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-heroku-tutorial/tutorial_heroku_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="32eca-137">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="32eca-137">Configuring and testing Azure AD single sign-on</span></span>

<span data-ttu-id="32eca-138">W tej sekcji możesz skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z Heroku na podstawie użytkownika testowego, nazywany "Britta Simona".</span><span class="sxs-lookup"><span data-stu-id="32eca-138">In this section, you configure and test Azure AD single sign-on with Heroku based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="32eca-139">Dla pojedynczego logowania jednokrotnego toowork usługi Azure AD musi tooknow użytkownika odpowiednikiem hello w Heroku jest tooa użytkownika w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="32eca-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Heroku is tooa user in Azure AD.</span></span> <span data-ttu-id="32eca-140">Innymi słowy relację łącza między użytkownika usługi Azure AD i hello użytkownikowi w Heroku musi toobe ustanowione.</span><span class="sxs-lookup"><span data-stu-id="32eca-140">In other words, a link relationship between an Azure AD user and hello related user in Heroku needs toobe established.</span></span>

<span data-ttu-id="32eca-141">W Heroku, należy przypisać wartość hello hello **nazwy użytkownika** w usłudze Azure AD jako wartość hello hello **Username** tooestablish hello łącze relacji.</span><span class="sxs-lookup"><span data-stu-id="32eca-141">In Heroku, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="32eca-142">tooconfigure i testowych usługi Azure AD rejestracji jednokrotnej z Heroku, należy po bloków konstrukcyjnych hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="32eca-142">tooconfigure and test Azure AD single sign-on with Heroku, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="32eca-143">**[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configuring-azure-ad-single-sign-on)**  -tooenable Twojego toouse użytkowników tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="32eca-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="32eca-144">**[Tworzenie użytkownika testowego usługi Azure AD](#creating-an-azure-ad-test-user)**  -tootest usługi Azure AD rejestracji jednokrotnej z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="32eca-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="32eca-145">**[Tworzenie użytkownika testowego Heroku](#creating-a-heroku-test-user)**  -toohave odpowiednikiem Simona Britta w Heroku, który jest połączony toohello usługi Azure AD reprezentację użytkownika.</span><span class="sxs-lookup"><span data-stu-id="32eca-145">**[Creating a Heroku test user](#creating-a-heroku-test-user)** - toohave a counterpart of Britta Simon in Heroku that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="32eca-146">**[Przypisanie użytkownika testowego hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Simona Britta toouse usługi Azure AD rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="32eca-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="32eca-147">**[Testowanie rejestracji jednokrotnej](#testing-single-sign-on)**  -tooverify czy hello konfiguracji działania.</span><span class="sxs-lookup"><span data-stu-id="32eca-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="32eca-148">Konfigurowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="32eca-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="32eca-149">W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w portalu Azure hello i skonfigurować logowanie jednokrotne w aplikacji Heroku.</span><span class="sxs-lookup"><span data-stu-id="32eca-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Heroku application.</span></span>

<span data-ttu-id="32eca-150">**tooconfigure usługi Azure AD rejestracji jednokrotnej z Heroku, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="32eca-150">**tooconfigure Azure AD single sign-on with Heroku, perform hello following steps:**</span></span>

1. <span data-ttu-id="32eca-151">W portalu Azure na powitania hello **Heroku** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.</span><span class="sxs-lookup"><span data-stu-id="32eca-151">In hello Azure portal, on hello **Heroku** application integration page, click **Single sign-on**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej][4]

2. <span data-ttu-id="32eca-153">Na powitania **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** tooenable rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="32eca-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-heroku-tutorial/tutorial_heroku_samlbase.png)

3. <span data-ttu-id="32eca-155">Na powitania **Heroku domeny i adres URL** sekcji, wykonaj następujące kroki hello:</span><span class="sxs-lookup"><span data-stu-id="32eca-155">On hello **Heroku Domain and URLs** section, perform hello following steps:</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-heroku-tutorial/tutorial_heroku_url.png)

    <span data-ttu-id="32eca-157">a.</span><span class="sxs-lookup"><span data-stu-id="32eca-157">a.</span></span> <span data-ttu-id="32eca-158">W hello **adres URL logowania** tekstowym, wpisz adres URL za pomocą hello następującego wzorca:</span><span class="sxs-lookup"><span data-stu-id="32eca-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern:</span></span>    
    `https://sso.heroku.com/saml/<company-name>/init`

    <span data-ttu-id="32eca-159">b.</span><span class="sxs-lookup"><span data-stu-id="32eca-159">b.</span></span> <span data-ttu-id="32eca-160">W hello **adres URL identyfikatora** tekstowym, wpisz adres URL za pomocą hello następującego wzorca:</span><span class="sxs-lookup"><span data-stu-id="32eca-160">In hello **Identifier URL** textbox, type a URL using hello following pattern:</span></span>            
    `https://sso.heroku.com/saml/<company-name>`

    > [!NOTE]
    ><span data-ttu-id="32eca-161">Wartości te nie są prawdziwe.</span><span class="sxs-lookup"><span data-stu-id="32eca-161">These values are not real.</span></span> <span data-ttu-id="32eca-162">Zaktualizować te wartości z hello rzeczywisty adres URL logowania i identyfikator.</span><span class="sxs-lookup"><span data-stu-id="32eca-162">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="32eca-163">Te wartości można uzyskać od zespołu Heroku, które zostało opisane w kolejnych sekcjach niniejszego artykułu.</span><span class="sxs-lookup"><span data-stu-id="32eca-163">You get these values from Heroku team, which is described in later sections of this article.</span></span> 
        
4. <span data-ttu-id="32eca-164">Na powitania **certyfikat podpisywania SAML** kliknij **XML metadanych** , a następnie zapisz plik metadanych hello na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="32eca-164">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-heroku-tutorial/tutorial_heroku_certificate.png) 

5. <span data-ttu-id="32eca-166">Kliknij przycisk **zapisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="32eca-166">Click **Save** button.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-heroku-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="32eca-168">tooenable logowania jednokrotnego w Heroku, wykonaj następujące kroki hello:</span><span class="sxs-lookup"><span data-stu-id="32eca-168">tooenable SSO in Heroku, perform hello following steps:</span></span>
   
    <span data-ttu-id="32eca-169">a.</span><span class="sxs-lookup"><span data-stu-id="32eca-169">a.</span></span> <span data-ttu-id="32eca-170">Zaloguj się za toohello Heroku konta z uprawnieniami administratora.</span><span class="sxs-lookup"><span data-stu-id="32eca-170">Log in toohello Heroku account as an administrator.</span></span>

    <span data-ttu-id="32eca-171">b.</span><span class="sxs-lookup"><span data-stu-id="32eca-171">b.</span></span> <span data-ttu-id="32eca-172">Kliknij przycisk hello **ustawienia** kartę.</span><span class="sxs-lookup"><span data-stu-id="32eca-172">Click hello **Settings** tab.</span></span>

    <span data-ttu-id="32eca-173">c.</span><span class="sxs-lookup"><span data-stu-id="32eca-173">c.</span></span> <span data-ttu-id="32eca-174">Na powitania **Zaloguj się na stronie**, kliknij przycisk **przekazać metadanych**.</span><span class="sxs-lookup"><span data-stu-id="32eca-174">On hello **Single Sign On Page**, click **Upload Metadata**.</span></span>

    <span data-ttu-id="32eca-175">d.</span><span class="sxs-lookup"><span data-stu-id="32eca-175">d.</span></span> <span data-ttu-id="32eca-176">Przekaż plik metadanych hello, który został pobrany z portalu Azure hello.</span><span class="sxs-lookup"><span data-stu-id="32eca-176">Upload hello metadata file, which you have downloaded from hello Azure portal.</span></span>

    <span data-ttu-id="32eca-177">e.</span><span class="sxs-lookup"><span data-stu-id="32eca-177">e.</span></span> <span data-ttu-id="32eca-178">Po pomyślnej instalacji hello, Administratorzy Zobacz okno dialogowe potwierdzenia i jest wyświetlany adres URL hello hello logowania jednokrotnego logowania dla użytkowników końcowych.</span><span class="sxs-lookup"><span data-stu-id="32eca-178">When hello setup is successful, administrators see a confirmation dialog and hello URL of hello SSO Login for end users is displayed.</span></span> 

    <span data-ttu-id="32eca-179">f.</span><span class="sxs-lookup"><span data-stu-id="32eca-179">f.</span></span> <span data-ttu-id="32eca-180">Hello kopii **adres URL logowania Heroku** i **identyfikator jednostki Heroku** wartości, a następnie przejść za tworzenie kopii**Heroku domeny i adres URL** sekcji w portalu Azure i Wklej te wartości do hello **Adres Url logowania** i **identyfikator** pól tekstowych odpowiednio.</span><span class="sxs-lookup"><span data-stu-id="32eca-180">Copy hello **Heroku Login URL** and **Heroku Entity ID** values and go back too**Heroku Domain and URLs** section in Azure portal and paste these values into hello **Sign-On Url** and **Identifier** textboxes respectively.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-heroku-tutorial/tutorial_heroku_52.png) 
    
8. <span data-ttu-id="32eca-182">Kliknij przycisk **Dalej**.</span><span class="sxs-lookup"><span data-stu-id="32eca-182">Click **Next**.</span></span>

> [!TIP]
> <span data-ttu-id="32eca-183">Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz hello [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji hello!</span><span class="sxs-lookup"><span data-stu-id="32eca-183">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="32eca-184">Po dodaniu tej aplikacji z hello **aplikacje przedsiębiorstwa w usłudze Active Directory** po prostu kliknij hello **rejestracji jednokrotnej** hello kartę i dostępu do osadzonych dokumentacji za pośrednictwem hello  **Konfiguracja** sekcji u dołu hello.</span><span class="sxs-lookup"><span data-stu-id="32eca-184">After adding this app from hello **Active Directory Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="32eca-185">Więcej o hello osadzonych dokumentacji funkcji w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="32eca-185">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="32eca-186">Tworzenie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="32eca-186">Creating an Azure AD test user</span></span>

<span data-ttu-id="32eca-187">Celem Hello w tej sekcji jest toocreate użytkownika testowego, w portalu Azure o nazwie Simona Britta hello.</span><span class="sxs-lookup"><span data-stu-id="32eca-187">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Tworzenie użytkowników usługi Azure AD][100]

<span data-ttu-id="32eca-189">**toocreate użytkownika testowego w usłudze Azure AD, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="32eca-189">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="32eca-190">W hello **portalu Azure**na temat hello w lewym okienku nawigacji, kliknij przycisk **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="32eca-190">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-heroku-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="32eca-192">toodisplay hello listę użytkowników, przejdź zbyt**użytkowników i grup** i kliknij przycisk **wszyscy użytkownicy**.</span><span class="sxs-lookup"><span data-stu-id="32eca-192">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-heroku-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="32eca-194">Witaj tooopen **użytkownika** okna dialogowego, kliknij przycisk **Dodaj** u góry hello hello okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="32eca-194">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-heroku-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="32eca-196">Na powitania **użytkownika** okna dialogowego wykonaj hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="32eca-196">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-heroku-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="32eca-198">a.</span><span class="sxs-lookup"><span data-stu-id="32eca-198">a.</span></span> <span data-ttu-id="32eca-199">W hello **nazwa** pole tekstowe, typ **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="32eca-199">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="32eca-200">b.</span><span class="sxs-lookup"><span data-stu-id="32eca-200">b.</span></span> <span data-ttu-id="32eca-201">W hello **nazwy użytkownika** pole tekstowe, hello typu **adres e-mail** z BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="32eca-201">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="32eca-202">c.</span><span class="sxs-lookup"><span data-stu-id="32eca-202">c.</span></span> <span data-ttu-id="32eca-203">Wybierz **Pokaż hasło** i zanotuj wartość hello hello **hasło**.</span><span class="sxs-lookup"><span data-stu-id="32eca-203">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="32eca-204">d.</span><span class="sxs-lookup"><span data-stu-id="32eca-204">d.</span></span> <span data-ttu-id="32eca-205">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="32eca-205">Click **Create**.</span></span>
 
### <a name="creating-a-heroku-test-user"></a><span data-ttu-id="32eca-206">Tworzenie użytkownika testowego Heroku</span><span class="sxs-lookup"><span data-stu-id="32eca-206">Creating a Heroku test user</span></span>

<span data-ttu-id="32eca-207">W tej sekcji należy utworzyć użytkownika o nazwie Simona Britta w Heroku.</span><span class="sxs-lookup"><span data-stu-id="32eca-207">In this section, you create a user called Britta Simon in Heroku.</span></span> <span data-ttu-id="32eca-208">Heroku obsługę w czasie, który jest domyślnie włączona.</span><span class="sxs-lookup"><span data-stu-id="32eca-208">Heroku supports just-in-time provisioning, which is enabled by default.</span></span>

<span data-ttu-id="32eca-209">Nie ma elementu akcji można w tej sekcji.</span><span class="sxs-lookup"><span data-stu-id="32eca-209">There is no action item for you in this section.</span></span> <span data-ttu-id="32eca-210">Nowy użytkownik jest tworzony podczas uzyskiwania dostępu do Heroku, jeśli jeszcze nie istnieje hello użytkownika.</span><span class="sxs-lookup"><span data-stu-id="32eca-210">A new user is created when accessing Heroku if hello user doesn't exist yet.</span></span> <span data-ttu-id="32eca-211">Po udostępnieniu hello konta hello użytkownik końcowy otrzymuje wiadomość e-mail z weryfikacji i musi połączyć tooclick hello potwierdzenia.</span><span class="sxs-lookup"><span data-stu-id="32eca-211">After hello account is provisioned, hello end user receives a verification email and needs tooclick hello acknowledgement link.</span></span>

>[!NOTE]
><span data-ttu-id="32eca-212">Jeśli potrzebujesz ręcznie toocreate użytkownika, należy toocontact hello [zespołem pomocy technicznej klienta Heroku](https://www.heroku.com/support).</span><span class="sxs-lookup"><span data-stu-id="32eca-212">If you need toocreate a user manually, you need toocontact hello [Heroku Client support team](https://www.heroku.com/support).</span></span>
>  

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="32eca-213">Przypisanie użytkownika testowego hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="32eca-213">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="32eca-214">W tej sekcji możesz włączyć toouse Simona Britta Azure logowania jednokrotnego za udzielanie dostępu tooHeroku.</span><span class="sxs-lookup"><span data-stu-id="32eca-214">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooHeroku.</span></span>

![Przypisz użytkownika][200] 

<span data-ttu-id="32eca-216">**tooassign tooHeroku Simona Britta wykonaj hello następujące kroki:**</span><span class="sxs-lookup"><span data-stu-id="32eca-216">**tooassign Britta Simon tooHeroku, perform hello following steps:**</span></span>

1. <span data-ttu-id="32eca-217">W portalu Azure hello, otwórz widok aplikacji hello, a następnie przejdź do widoku katalogu toohello i przejść za**aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="32eca-217">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Przypisz użytkownika][201] 

2. <span data-ttu-id="32eca-219">Z listy aplikacji hello wybierz **Heroku**.</span><span class="sxs-lookup"><span data-stu-id="32eca-219">In hello applications list, select **Heroku**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-heroku-tutorial/tutorial_heroku_app.png) 

3. <span data-ttu-id="32eca-221">W menu powitania po lewej stronie powitania kliknij **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="32eca-221">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Przypisz użytkownika][202] 

4. <span data-ttu-id="32eca-223">Kliknij przycisk **Dodaj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="32eca-223">Click **Add** button.</span></span> <span data-ttu-id="32eca-224">Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="32eca-224">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Przypisz użytkownika][203]

5. <span data-ttu-id="32eca-226">Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** hello listy użytkowników.</span><span class="sxs-lookup"><span data-stu-id="32eca-226">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="32eca-227">Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="32eca-227">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="32eca-228">Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="32eca-228">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="32eca-229">Testowanie rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="32eca-229">Testing single sign-on</span></span>

<span data-ttu-id="32eca-230">W tej sekcji można przetestować konfiguracji usługi Azure AD pojedynczego logowania jednokrotnego przy użyciu hello panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="32eca-230">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="32eca-231">Po kliknięciu kafelka Heroku hello w hello Panel dostępu, należy pobrać automatycznie zalogowane tooyour Heroku aplikacji.</span><span class="sxs-lookup"><span data-stu-id="32eca-231">When you click hello Heroku tile in hello Access Panel, you should get automatically signed-on tooyour Heroku application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="32eca-232">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="32eca-232">Additional resources</span></span>

* [<span data-ttu-id="32eca-233">Lista samouczków dotyczących tooIntegrate aplikacji SaaS w usłudze Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="32eca-233">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="32eca-234">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="32eca-234">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-heroku-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-heroku-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-heroku-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-heroku-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-heroku-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-heroku-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-heroku-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-heroku-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-heroku-tutorial/tutorial_general_203.png
