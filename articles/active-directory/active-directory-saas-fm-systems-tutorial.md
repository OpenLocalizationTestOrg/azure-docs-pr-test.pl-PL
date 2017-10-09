---
title: 'Samouczek: Integracji Azure Active Directory z FM:Systems | Dokumentacja firmy Microsoft'
description: "Dowiedz się, jak tooconfigure logowanie jednokrotne między usługą Azure Active Directory i FM:Systems."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: f78c58c5-6e98-458b-8991-78624a245665
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/17/2017
ms.author: jeedes
ms.openlocfilehash: 677ef74dac663a43835d65a4d4f4fd031a0078cd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-fmsystems"></a><span data-ttu-id="72b6e-103">Samouczek: Integracji Azure Active Directory z FM:Systems</span><span class="sxs-lookup"><span data-stu-id="72b6e-103">Tutorial: Azure Active Directory integration with FM:Systems</span></span>

<span data-ttu-id="72b6e-104">Z tego samouczka, dowiesz się, jak toointegrate FM:Systems w usłudze Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="72b6e-104">In this tutorial, you learn how toointegrate FM:Systems with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="72b6e-105">Integracja z usługą Azure AD FM:Systems zapewnia hello następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="72b6e-105">Integrating FM:Systems with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="72b6e-106">Można kontrolować w usłudze Azure AD, kto ma dostęp do tooFM:Systems</span><span class="sxs-lookup"><span data-stu-id="72b6e-106">You can control in Azure AD who has access tooFM:Systems</span></span>
- <span data-ttu-id="72b6e-107">Można włączyć użytkownika użytkownicy tooautomatically get zalogowane tooFM:Systems (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="72b6e-107">You can enable your users tooautomatically get signed-on tooFM:Systems (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="72b6e-108">Możesz zarządzać kont w jednej centralnej lokalizacji - hello portalu Azure</span><span class="sxs-lookup"><span data-stu-id="72b6e-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="72b6e-109">Jeśli chcesz tooknow więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="72b6e-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="72b6e-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="72b6e-110">Prerequisites</span></span>

<span data-ttu-id="72b6e-111">tooconfigure integracji z usługą Azure AD z FM:Systems należy hello następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="72b6e-111">tooconfigure Azure AD integration with FM:Systems, you need hello following items:</span></span>

- <span data-ttu-id="72b6e-112">Subskrypcję usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="72b6e-112">An Azure AD subscription</span></span>
- <span data-ttu-id="72b6e-113">FM:Systems logowanie jednokrotne włączone subskrypcji</span><span class="sxs-lookup"><span data-stu-id="72b6e-113">An FM:Systems single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="72b6e-114">tootest hello kroków w tym samouczku, zaleca się przy użyciu środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="72b6e-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="72b6e-115">tootest hello kroki opisane w tym samouczku, należy stosować te zalecenia:</span><span class="sxs-lookup"><span data-stu-id="72b6e-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="72b6e-116">Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="72b6e-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="72b6e-117">Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz pobrać miesięczna wersja próbna [tutaj](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="72b6e-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="72b6e-118">Opis scenariusza</span><span class="sxs-lookup"><span data-stu-id="72b6e-118">Scenario description</span></span>
<span data-ttu-id="72b6e-119">W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym.</span><span class="sxs-lookup"><span data-stu-id="72b6e-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="72b6e-120">Scenariusz Hello opisane w tym samouczku składa się z dwóch głównych elementów:</span><span class="sxs-lookup"><span data-stu-id="72b6e-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="72b6e-121">Dodawanie FM:Systems z galerii hello</span><span class="sxs-lookup"><span data-stu-id="72b6e-121">Adding FM:Systems from hello gallery</span></span>
2. <span data-ttu-id="72b6e-122">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="72b6e-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-fmsystems-from-hello-gallery"></a><span data-ttu-id="72b6e-123">Dodawanie FM:Systems z galerii hello</span><span class="sxs-lookup"><span data-stu-id="72b6e-123">Adding FM:Systems from hello gallery</span></span>
<span data-ttu-id="72b6e-124">tooconfigure hello integracji FM:Systems do usługi Azure AD, należy tooadd FM:Systems z hello galerii tooyour listę zarządzanych aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="72b6e-124">tooconfigure hello integration of FM:Systems into Azure AD, you need tooadd FM:Systems from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="72b6e-125">**tooadd FM:Systems z galerii hello, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="72b6e-125">**tooadd FM:Systems from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="72b6e-126">W hello  **[portalu Azure](https://portal.azure.com)**na temat hello panelu nawigacji po lewej stronie, kliknij przycisk **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="72b6e-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Usługa Active Directory][1]

2. <span data-ttu-id="72b6e-128">Przejdź za**aplikacje dla przedsiębiorstw**.</span><span class="sxs-lookup"><span data-stu-id="72b6e-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="72b6e-129">Następnie przejdź zbyt**wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="72b6e-129">Then go too**All applications**.</span></span>

    ![Aplikacje][2]
    
3. <span data-ttu-id="72b6e-131">tooadd nową aplikację, kliknij przycisk **nowej aplikacji** przycisk u góry hello okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="72b6e-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplikacje][3]

4. <span data-ttu-id="72b6e-133">W polu wyszukiwania hello wpisz **FM:Systems**.</span><span class="sxs-lookup"><span data-stu-id="72b6e-133">In hello search box, type **FM:Systems**.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-fm-systems-tutorial/tutorial_fmsystems_search.png)

5. <span data-ttu-id="72b6e-135">W panelu wyników hello zaznacz **FM:Systems**, a następnie kliknij przycisk **Dodaj** przycisk aplikacji hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="72b6e-135">In hello results panel, select **FM:Systems**, and then click **Add** button tooadd hello application.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-fm-systems-tutorial/tutorial_fmsystems_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="72b6e-137">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="72b6e-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="72b6e-138">W tej sekcji skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z FM:Systems w oparciu o nazwie "Britta Simona" użytkownika testowego.</span><span class="sxs-lookup"><span data-stu-id="72b6e-138">In this section, you configure and test Azure AD single sign-on with FM:Systems based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="72b6e-139">Dla pojedynczego logowania jednokrotnego toowork usługi Azure AD musi tooknow użytkownika odpowiednikiem hello w FM:Systems jest tooa użytkownika w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="72b6e-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in FM:Systems is tooa user in Azure AD.</span></span> <span data-ttu-id="72b6e-140">Innymi słowy relację łącza między użytkownika usługi Azure AD i hello użytkownikowi w FM:Systems musi toobe ustanowione.</span><span class="sxs-lookup"><span data-stu-id="72b6e-140">In other words, a link relationship between an Azure AD user and hello related user in FM:Systems needs toobe established.</span></span>

<span data-ttu-id="72b6e-141">W FM:Systems, należy przypisać wartość hello hello **nazwy użytkownika** w usłudze Azure AD jako wartość hello hello **Username** tooestablish hello łącze relacji.</span><span class="sxs-lookup"><span data-stu-id="72b6e-141">In FM:Systems, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="72b6e-142">tooconfigure i testowych usługi Azure AD rejestracji jednokrotnej z FM:Systems, należy po bloków konstrukcyjnych hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="72b6e-142">tooconfigure and test Azure AD single sign-on with FM:Systems, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="72b6e-143">**[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configuring-azure-ad-single-sign-on)**  -tooenable Twojego toouse użytkowników tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="72b6e-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="72b6e-144">**[Tworzenie użytkownika testowego usługi Azure AD](#creating-an-azure-ad-test-user)**  -tootest usługi Azure AD rejestracji jednokrotnej z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="72b6e-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="72b6e-145">**[Tworzenie użytkownika testowego FM:Systems](#creating-an-fmsystems-test-user)**  -toohave odpowiednikiem Simona Britta w FM:Systems, który jest połączony toohello usługi Azure AD reprezentację użytkownika.</span><span class="sxs-lookup"><span data-stu-id="72b6e-145">**[Creating an FM:Systems test user](#creating-an-fmsystems-test-user)** - toohave a counterpart of Britta Simon in FM:Systems that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="72b6e-146">**[Przypisanie użytkownika testowego hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Simona Britta toouse usługi Azure AD rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="72b6e-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="72b6e-147">**[Testowanie rejestracji jednokrotnej](#testing-single-sign-on)**  -tooverify czy hello konfiguracji działania.</span><span class="sxs-lookup"><span data-stu-id="72b6e-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="72b6e-148">Konfigurowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="72b6e-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="72b6e-149">W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w portalu Azure hello i skonfigurować logowanie jednokrotne w aplikacji FM:Systems.</span><span class="sxs-lookup"><span data-stu-id="72b6e-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your FM:Systems application.</span></span>

<span data-ttu-id="72b6e-150">**tooconfigure usługi Azure AD rejestracji jednokrotnej z FM:Systems, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="72b6e-150">**tooconfigure Azure AD single sign-on with FM:Systems, perform hello following steps:**</span></span>

1. <span data-ttu-id="72b6e-151">W portalu Azure na powitania hello **FM:Systems** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.</span><span class="sxs-lookup"><span data-stu-id="72b6e-151">In hello Azure portal, on hello **FM:Systems** application integration page, click **Single sign-on**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej][4]

2. <span data-ttu-id="72b6e-153">Na powitania **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** tooenable rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="72b6e-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-fm-systems-tutorial/tutorial_fmsystems_samlbase.png)

3. <span data-ttu-id="72b6e-155">Na powitania **FM:Systems domeny i adres URL** sekcji, wykonaj następujące kroki hello:</span><span class="sxs-lookup"><span data-stu-id="72b6e-155">On hello **FM:Systems Domain and URLs** section, perform hello following steps:</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-fm-systems-tutorial/tutorial_fmsystems_url.png)

    <span data-ttu-id="72b6e-157">W hello **adres URL odpowiedzi** pole tekstowe, wpisz FM:Systems Twojego **adres URL odpowiedzi**, wprowadź adres URL hello przy użyciu hello następującego wzorca:`https://<companyname>.fmshosted.com/fminteract/ConsumerService2.aspx`</span><span class="sxs-lookup"><span data-stu-id="72b6e-157">In hello **Reply URL** textbox, type your FM:Systems **Reply URL**, type hello URL using hello following pattern: `https://<companyname>.fmshosted.com/fminteract/ConsumerService2.aspx`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="72b6e-158">Ta wartość nie jest prawdziwe.</span><span class="sxs-lookup"><span data-stu-id="72b6e-158">This value is not real.</span></span> <span data-ttu-id="72b6e-159">Zaktualizuj tę wartość przy hello rzeczywisty adres URL odpowiedzi służący.</span><span class="sxs-lookup"><span data-stu-id="72b6e-159">Update this value with hello actual Reply URL.</span></span> <span data-ttu-id="72b6e-160">Skontaktuj się z [zespołem pomocy technicznej FM:Systems](https://fmsystems.com/ask-us/) tooget tej wartości.</span><span class="sxs-lookup"><span data-stu-id="72b6e-160">Contact [FM:Systems support team](https://fmsystems.com/ask-us/) tooget this value.</span></span>
 
4. <span data-ttu-id="72b6e-161">Na powitania **certyfikat podpisywania SAML** kliknij **XML metadanych** , a następnie zapisz plik metadanych hello na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="72b6e-161">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-fm-systems-tutorial/tutorial_fmsystems_certificate.png) 

5. <span data-ttu-id="72b6e-163">Kliknij przycisk **zapisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="72b6e-163">Click **Save** button.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-fm-systems-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="72b6e-165">tooconfigure rejestracji jednokrotnej w **FM:Systems** strony, należy pobrać hello toosend **XML metadanych** za[zespołem pomocy technicznej FM:Systems](https://fmsystems.com/ask-us/).</span><span class="sxs-lookup"><span data-stu-id="72b6e-165">tooconfigure single sign-on on **FM:Systems** side, you need toosend hello downloaded **Metadata XML** too[FM:Systems support team](https://fmsystems.com/ask-us/).</span></span> <span data-ttu-id="72b6e-166">To ustawienie toohave hello prawidłowo po obu stronach połączenia logowania jednokrotnego SAML one ustawić.</span><span class="sxs-lookup"><span data-stu-id="72b6e-166">They set this setting toohave hello SAML SSO connection set properly on both sides.</span></span> <span data-ttu-id="72b6e-167">Otrzymasz powiadomienie podczas logowania jednokrotnego została włączona dla Twojej subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="72b6e-167">You will get a notification when SSO has been enabled for your subscription.</span></span>

> [!TIP]
> <span data-ttu-id="72b6e-168">Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz hello [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji hello!</span><span class="sxs-lookup"><span data-stu-id="72b6e-168">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="72b6e-169">Po dodaniu tej aplikacji z hello **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij hello **rejestracji jednokrotnej** hello kartę i dostępu do osadzonych dokumentacji za pośrednictwem hello  **Konfiguracja** sekcji u dołu hello.</span><span class="sxs-lookup"><span data-stu-id="72b6e-169">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="72b6e-170">Więcej o hello osadzonych dokumentacji funkcji w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="72b6e-170">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="72b6e-171">Tworzenie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="72b6e-171">Creating an Azure AD test user</span></span>
<span data-ttu-id="72b6e-172">Celem Hello w tej sekcji jest toocreate użytkownika testowego, w portalu Azure o nazwie Simona Britta hello.</span><span class="sxs-lookup"><span data-stu-id="72b6e-172">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Tworzenie użytkowników usługi Azure AD][100]

<span data-ttu-id="72b6e-174">**toocreate użytkownika testowego w usłudze Azure AD, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="72b6e-174">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="72b6e-175">W hello **portalu Azure**na temat hello w lewym okienku nawigacji, kliknij przycisk **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="72b6e-175">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-fm-systems-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="72b6e-177">toodisplay hello listę użytkowników, przejdź zbyt**użytkowników i grup** i kliknij przycisk **wszyscy użytkownicy**.</span><span class="sxs-lookup"><span data-stu-id="72b6e-177">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-fm-systems-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="72b6e-179">Witaj tooopen **użytkownika** okna dialogowego, kliknij przycisk **Dodaj** u góry hello hello okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="72b6e-179">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-fm-systems-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="72b6e-181">Na powitania **użytkownika** okna dialogowego wykonaj hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="72b6e-181">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-fm-systems-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="72b6e-183">a.</span><span class="sxs-lookup"><span data-stu-id="72b6e-183">a.</span></span> <span data-ttu-id="72b6e-184">W hello **nazwa** pole tekstowe, typ **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="72b6e-184">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="72b6e-185">b.</span><span class="sxs-lookup"><span data-stu-id="72b6e-185">b.</span></span> <span data-ttu-id="72b6e-186">W hello **nazwy użytkownika** pole tekstowe, hello typu **adres e-mail** z BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="72b6e-186">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="72b6e-187">c.</span><span class="sxs-lookup"><span data-stu-id="72b6e-187">c.</span></span> <span data-ttu-id="72b6e-188">Wybierz **Pokaż hasło** i zanotuj wartość hello hello **hasło**.</span><span class="sxs-lookup"><span data-stu-id="72b6e-188">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="72b6e-189">d.</span><span class="sxs-lookup"><span data-stu-id="72b6e-189">d.</span></span> <span data-ttu-id="72b6e-190">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="72b6e-190">Click **Create**.</span></span>
 
### <a name="creating-an-fmsystems-test-user"></a><span data-ttu-id="72b6e-191">Tworzenie użytkownika testowego FM:Systems</span><span class="sxs-lookup"><span data-stu-id="72b6e-191">Creating an FM:Systems test user</span></span>

1. <span data-ttu-id="72b6e-192">W oknie przeglądarki sieci web Zaloguj się do witryny firmy FM:Systems jako administrator.</span><span class="sxs-lookup"><span data-stu-id="72b6e-192">In a web browser window, log into your FM:Systems company site as an administrator.</span></span>

2. <span data-ttu-id="72b6e-193">Przejdź za**Administracja systemu \> Zarządzanie zabezpieczeń \> użytkowników \> listy użytkowników**.</span><span class="sxs-lookup"><span data-stu-id="72b6e-193">Go too**System Administration \> Manage Security \> Users \> User list**.</span></span>
   
    <span data-ttu-id="72b6e-194">![Administrowanie systemem](./media/active-directory-saas-fm-systems-tutorial/ic795905.png "administracji systemu")</span><span class="sxs-lookup"><span data-stu-id="72b6e-194">![System Administration](./media/active-directory-saas-fm-systems-tutorial/ic795905.png "System Administration")</span></span>

3. <span data-ttu-id="72b6e-195">Kliknij przycisk **Tworzenie nowego użytkownika**.</span><span class="sxs-lookup"><span data-stu-id="72b6e-195">Click **Create new user**.</span></span>
   
    <span data-ttu-id="72b6e-196">![Utwórz nowego użytkownika](./media/active-directory-saas-fm-systems-tutorial/ic795906.png "Utwórz nowego użytkownika")</span><span class="sxs-lookup"><span data-stu-id="72b6e-196">![Create New User](./media/active-directory-saas-fm-systems-tutorial/ic795906.png "Create New User")</span></span>

4. <span data-ttu-id="72b6e-197">W hello **Tworzenie użytkownika** sekcji, wykonaj następujące kroki hello:</span><span class="sxs-lookup"><span data-stu-id="72b6e-197">In hello **Create User** section, perform hello following steps:</span></span>
   
    <span data-ttu-id="72b6e-198">![Utwórz użytkownika](./media/active-directory-saas-fm-systems-tutorial/ic795907.png "Tworzenie użytkownika")</span><span class="sxs-lookup"><span data-stu-id="72b6e-198">![Create User](./media/active-directory-saas-fm-systems-tutorial/ic795907.png "Create User")</span></span>
   
    <span data-ttu-id="72b6e-199">a.</span><span class="sxs-lookup"><span data-stu-id="72b6e-199">a.</span></span> <span data-ttu-id="72b6e-200">Hello typu **UserName**, hello **hasło**, **Potwierdź hasło**, **E-mail** i hello **identyfikator**prawidłowy Azure związanych z kontem usługi Active Directory, mają tooprovision w hello pól tekstowych.</span><span class="sxs-lookup"><span data-stu-id="72b6e-200">Type hello **UserName**, hello **Password**, **Confirm Password**, **E-mail** and hello **Employee ID** of a valid Azure Active Directory account you want tooprovision into hello related textboxes.</span></span>
   
    <span data-ttu-id="72b6e-201">b.</span><span class="sxs-lookup"><span data-stu-id="72b6e-201">b.</span></span> <span data-ttu-id="72b6e-202">Kliknij przycisk **Dalej**.</span><span class="sxs-lookup"><span data-stu-id="72b6e-202">Click **Next**.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="72b6e-203">Przypisanie użytkownika testowego hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="72b6e-203">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="72b6e-204">W tej sekcji możesz włączyć toouse Simona Britta Azure logowania jednokrotnego za udzielanie dostępu tooFM:Systems.</span><span class="sxs-lookup"><span data-stu-id="72b6e-204">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooFM:Systems.</span></span>

![Przypisz użytkownika][200] 

<span data-ttu-id="72b6e-206">**tooassign tooFM:Systems Simona Britta wykonaj hello następujące kroki:**</span><span class="sxs-lookup"><span data-stu-id="72b6e-206">**tooassign Britta Simon tooFM:Systems, perform hello following steps:**</span></span>

1. <span data-ttu-id="72b6e-207">W portalu Azure hello, otwórz widok aplikacji hello, a następnie przejdź do widoku katalogu toohello i przejść za**aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="72b6e-207">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Przypisz użytkownika][201] 

2. <span data-ttu-id="72b6e-209">Z listy aplikacji hello wybierz **FM:Systems**.</span><span class="sxs-lookup"><span data-stu-id="72b6e-209">In hello applications list, select **FM:Systems**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-fm-systems-tutorial/tutorial_fmsystems_app.png) 

3. <span data-ttu-id="72b6e-211">W menu powitania po lewej stronie powitania kliknij **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="72b6e-211">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Przypisz użytkownika][202] 

4. <span data-ttu-id="72b6e-213">Kliknij przycisk **Dodaj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="72b6e-213">Click **Add** button.</span></span> <span data-ttu-id="72b6e-214">Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="72b6e-214">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Przypisz użytkownika][203]

5. <span data-ttu-id="72b6e-216">Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** hello listy użytkowników.</span><span class="sxs-lookup"><span data-stu-id="72b6e-216">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="72b6e-217">Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="72b6e-217">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="72b6e-218">Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="72b6e-218">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="72b6e-219">Testowanie rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="72b6e-219">Testing single sign-on</span></span>

<span data-ttu-id="72b6e-220">W tej sekcji można przetestować konfiguracji usługi Azure AD pojedynczego logowania jednokrotnego przy użyciu hello panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="72b6e-220">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="72b6e-221">Po kliknięciu kafelka FM:Systems hello w hello Panel dostępu, należy pobrać automatycznie zalogowane tooyour FM:Systems aplikacji.</span><span class="sxs-lookup"><span data-stu-id="72b6e-221">When you click hello FM:Systems tile in hello Access Panel, you should get automatically signed-on tooyour FM:Systems application.</span></span>
<span data-ttu-id="72b6e-222">Aby uzyskać więcej informacji na temat panelu dostępu, zobacz [toohello wprowadzenie panelu dostępu](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="72b6e-222">For more information about the Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="72b6e-223">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="72b6e-223">Additional resources</span></span>

* [<span data-ttu-id="72b6e-224">Lista samouczków dotyczących tooIntegrate aplikacji SaaS w usłudze Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="72b6e-224">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="72b6e-225">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="72b6e-225">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-fm-systems-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-fm-systems-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-fm-systems-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-fm-systems-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-fm-systems-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-fm-systems-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-fm-systems-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-fm-systems-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-fm-systems-tutorial/tutorial_general_203.png

