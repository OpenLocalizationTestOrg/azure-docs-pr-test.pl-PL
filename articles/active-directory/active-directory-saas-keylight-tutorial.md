---
title: 'Samouczek: Integracji Azure Active Directory z LockPath Keylight | Dokumentacja firmy Microsoft'
description: "Dowiedz się, jak tooconfigure logowanie jednokrotne między usługą Azure Active Directory i LockPath Keylight."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 234a32f1-9f56-4650-9e31-7b38ad734b1a
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/05/2017
ms.author: jeedes
ms.openlocfilehash: 5485aeb068ba6fbdb4ea9bfc89d401e00c5b1d29
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-lockpath-keylight"></a><span data-ttu-id="f4ff1-103">Samouczek: Integracji Azure Active Directory z LockPath Keylight</span><span class="sxs-lookup"><span data-stu-id="f4ff1-103">Tutorial: Azure Active Directory integration with LockPath Keylight</span></span>

<span data-ttu-id="f4ff1-104">Z tego samouczka, dowiesz się, jak toointegrate LockPath Keylight w usłudze Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="f4ff1-104">In this tutorial, you learn how toointegrate LockPath Keylight with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="f4ff1-105">Integracja z usługą Azure AD LockPath Keylight zapewnia hello następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="f4ff1-105">Integrating LockPath Keylight with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="f4ff1-106">Można kontrolować w usłudze Azure AD, kto ma dostęp do tooLockPath Keylight</span><span class="sxs-lookup"><span data-stu-id="f4ff1-106">You can control in Azure AD who has access tooLockPath Keylight</span></span>
- <span data-ttu-id="f4ff1-107">Można włączyć użytkownika użytkownicy tooautomatically get zalogowane tooLockPath Keylight (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="f4ff1-107">You can enable your users tooautomatically get signed-on tooLockPath Keylight (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="f4ff1-108">Możesz zarządzać kont w jednej centralnej lokalizacji - hello portalu Azure</span><span class="sxs-lookup"><span data-stu-id="f4ff1-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="f4ff1-109">Jeśli chcesz tooknow więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="f4ff1-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f4ff1-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="f4ff1-110">Prerequisites</span></span>

<span data-ttu-id="f4ff1-111">tooconfigure integracji usługi Azure AD z LockPath Keylight należy hello następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="f4ff1-111">tooconfigure Azure AD integration with LockPath Keylight, you need hello following items:</span></span>

- <span data-ttu-id="f4ff1-112">Subskrypcję usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="f4ff1-112">An Azure AD subscription</span></span>
- <span data-ttu-id="f4ff1-113">LockPath Keylight jednokrotnego włączone subskrypcji</span><span class="sxs-lookup"><span data-stu-id="f4ff1-113">A LockPath Keylight single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="f4ff1-114">tootest hello kroków w tym samouczku, zaleca się przy użyciu środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="f4ff1-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="f4ff1-115">tootest hello kroki opisane w tym samouczku, należy stosować te zalecenia:</span><span class="sxs-lookup"><span data-stu-id="f4ff1-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="f4ff1-116">Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="f4ff1-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="f4ff1-117">Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz pobrać miesięczna wersja próbna [tutaj](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="f4ff1-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="f4ff1-118">Opis scenariusza</span><span class="sxs-lookup"><span data-stu-id="f4ff1-118">Scenario description</span></span>
<span data-ttu-id="f4ff1-119">W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym.</span><span class="sxs-lookup"><span data-stu-id="f4ff1-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="f4ff1-120">Scenariusz Hello opisane w tym samouczku składa się z dwóch głównych elementów:</span><span class="sxs-lookup"><span data-stu-id="f4ff1-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="f4ff1-121">Dodawanie LockPath Keylight z galerii hello</span><span class="sxs-lookup"><span data-stu-id="f4ff1-121">Adding LockPath Keylight from hello gallery</span></span>
2. <span data-ttu-id="f4ff1-122">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="f4ff1-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-lockpath-keylight-from-hello-gallery"></a><span data-ttu-id="f4ff1-123">Dodawanie LockPath Keylight z galerii hello</span><span class="sxs-lookup"><span data-stu-id="f4ff1-123">Adding LockPath Keylight from hello gallery</span></span>
<span data-ttu-id="f4ff1-124">tooconfigure hello integracji LockPath Keylight do usługi Azure AD, należy tooadd LockPath Keylight z hello galerii tooyour listę zarządzanych aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="f4ff1-124">tooconfigure hello integration of LockPath Keylight into Azure AD, you need tooadd LockPath Keylight from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="f4ff1-125">**tooadd LockPath Keylight z galerii hello wykonaj hello następujące kroki:**</span><span class="sxs-lookup"><span data-stu-id="f4ff1-125">**tooadd LockPath Keylight from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="f4ff1-126">W hello  **[portalu Azure](https://portal.azure.com)**na temat hello panelu nawigacji po lewej stronie, kliknij przycisk **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="f4ff1-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Usługa Active Directory][1]

2. <span data-ttu-id="f4ff1-128">Przejdź za**aplikacje dla przedsiębiorstw**.</span><span class="sxs-lookup"><span data-stu-id="f4ff1-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="f4ff1-129">Następnie przejdź zbyt**wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="f4ff1-129">Then go too**All applications**.</span></span>

    ![Aplikacje][2]
    
3. <span data-ttu-id="f4ff1-131">tooadd nową aplikację, kliknij przycisk **nowej aplikacji** przycisk u góry hello okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="f4ff1-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplikacje][3]

4. <span data-ttu-id="f4ff1-133">W polu wyszukiwania hello wpisz **LockPath Keylight**.</span><span class="sxs-lookup"><span data-stu-id="f4ff1-133">In hello search box, type **LockPath Keylight**.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-keylight-tutorial/tutorial_keylight_search.png)

5. <span data-ttu-id="f4ff1-135">W panelu wyników hello, wybierz **LockPath Keylight**, a następnie kliknij przycisk **Dodaj** przycisk tooadd hello aplikacji.</span><span class="sxs-lookup"><span data-stu-id="f4ff1-135">In hello results panel, select **LockPath Keylight**, and then click **Add** button tooadd hello application.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-keylight-tutorial/tutorial_keylight_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="f4ff1-137">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="f4ff1-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="f4ff1-138">W tej sekcji możesz skonfigurować i test usługi Azure AD rejestracji jednokrotnej z LockPath Keylight oparte na użytkownika testowego o nazwie "Britta Simona".</span><span class="sxs-lookup"><span data-stu-id="f4ff1-138">In this section, you configure and test Azure AD single sign-on with LockPath Keylight based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="f4ff1-139">Dla pojedynczego logowania jednokrotnego toowork usługi Azure AD musi tooknow użytkownika odpowiednikiem hello w LockPath Keylight jest tooa użytkownika w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="f4ff1-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in LockPath Keylight is tooa user in Azure AD.</span></span> <span data-ttu-id="f4ff1-140">Innymi słowy relację łącza między użytkownika usługi Azure AD i hello użytkownikowi w LockPath Keylight musi toobe ustanowione.</span><span class="sxs-lookup"><span data-stu-id="f4ff1-140">In other words, a link relationship between an Azure AD user and hello related user in LockPath Keylight needs toobe established.</span></span>

<span data-ttu-id="f4ff1-141">W LockPath Keylight, należy przypisać wartość hello hello **nazwy użytkownika** w usłudze Azure AD jako wartość hello hello **Username** tooestablish hello łącze relacji.</span><span class="sxs-lookup"><span data-stu-id="f4ff1-141">In LockPath Keylight, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="f4ff1-142">tooconfigure i testowych usługi Azure AD rejestracji jednokrotnej z LockPath Keylight, należy po bloków konstrukcyjnych hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="f4ff1-142">tooconfigure and test Azure AD single sign-on with LockPath Keylight, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="f4ff1-143">**[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configuring-azure-ad-single-sign-on)**  -tooenable Twojego toouse użytkowników tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="f4ff1-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="f4ff1-144">**[Tworzenie użytkownika testowego usługi Azure AD](#creating-an-azure-ad-test-user)**  -tootest usługi Azure AD rejestracji jednokrotnej z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="f4ff1-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="f4ff1-145">**[Tworzenie użytkownika testowego LockPath Keylight](#creating-a-lockpath-keylight-test-user)**  -toohave odpowiednikiem Simona Britta w LockPath Keylight, który jest połączony toohello usługi Azure AD reprezentację użytkownika.</span><span class="sxs-lookup"><span data-stu-id="f4ff1-145">**[Creating a LockPath Keylight test user](#creating-a-lockpath-keylight-test-user)** - toohave a counterpart of Britta Simon in LockPath Keylight that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="f4ff1-146">**[Przypisanie użytkownika testowego hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Simona Britta toouse usługi Azure AD rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="f4ff1-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="f4ff1-147">**[Testowanie rejestracji jednokrotnej](#testing-single-sign-on)**  -tooverify czy hello konfiguracji działania.</span><span class="sxs-lookup"><span data-stu-id="f4ff1-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="f4ff1-148">Konfigurowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="f4ff1-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="f4ff1-149">W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w hello portalu Azure i skonfigurować logowanie jednokrotne w aplikacji LockPath Keylight.</span><span class="sxs-lookup"><span data-stu-id="f4ff1-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your LockPath Keylight application.</span></span>

<span data-ttu-id="f4ff1-150">**tooconfigure usługi Azure AD rejestracji jednokrotnej z LockPath Keylight wykonaj hello następujące kroki:**</span><span class="sxs-lookup"><span data-stu-id="f4ff1-150">**tooconfigure Azure AD single sign-on with LockPath Keylight, perform hello following steps:**</span></span>

1. <span data-ttu-id="f4ff1-151">W portalu Azure na powitania hello **LockPath Keylight** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.</span><span class="sxs-lookup"><span data-stu-id="f4ff1-151">In hello Azure portal, on hello **LockPath Keylight** application integration page, click **Single sign-on**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej][4]

2. <span data-ttu-id="f4ff1-153">Na powitania **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** tooenable rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="f4ff1-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-keylight-tutorial/tutorial_keylight_samlbase.png)

3. <span data-ttu-id="f4ff1-155">Na powitania **LockPath Keylight domeny i adres URL** sekcji, wykonaj następujące kroki hello::</span><span class="sxs-lookup"><span data-stu-id="f4ff1-155">On hello **LockPath Keylight Domain and URLs** section, perform hello following steps::</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-keylight-tutorial/tutorial_keylight_url.png)

    <span data-ttu-id="f4ff1-157">a.</span><span class="sxs-lookup"><span data-stu-id="f4ff1-157">a.</span></span> <span data-ttu-id="f4ff1-158">W hello **adres URL logowania** tekstowym, wpisz adres URL za pomocą hello następującego wzorca:`https://<company name>.keylightgrc.com/`</span><span class="sxs-lookup"><span data-stu-id="f4ff1-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<company name>.keylightgrc.com/`</span></span>

    <span data-ttu-id="f4ff1-159">b.</span><span class="sxs-lookup"><span data-stu-id="f4ff1-159">b.</span></span> <span data-ttu-id="f4ff1-160">W hello **identyfikator** tekstowym, wpisz adres URL za pomocą hello następującego wzorca:`https://<company name>.keylightgrc.com`</span><span class="sxs-lookup"><span data-stu-id="f4ff1-160">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<company name>.keylightgrc.com`</span></span>

    <span data-ttu-id="f4ff1-161">c.</span><span class="sxs-lookup"><span data-stu-id="f4ff1-161">c.</span></span> <span data-ttu-id="f4ff1-162">W hello **adres URL odpowiedzi** tekstowym, wpisz adres URL za pomocą hello następującego wzorca:`https://<company name>.keylightgrc.com/Login.aspx`</span><span class="sxs-lookup"><span data-stu-id="f4ff1-162">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://<company name>.keylightgrc.com/Login.aspx`</span></span>
    
    > [!NOTE] 
    > <span data-ttu-id="f4ff1-163">Wartości te nie są prawdziwe.</span><span class="sxs-lookup"><span data-stu-id="f4ff1-163">These values are not real.</span></span> <span data-ttu-id="f4ff1-164">Zaktualizować te wartości z hello rzeczywisty identyfikator, adres URL odpowiedzi i adres URL logowania.</span><span class="sxs-lookup"><span data-stu-id="f4ff1-164">Update these values with hello actual Identifier, Reply URL, and Sign-On URL.</span></span> <span data-ttu-id="f4ff1-165">Skontaktuj się z [zespołem pomocy technicznej klienta Keylight LockPath](https://www.lockpath.com/contact/) tooget tych wartości.</span><span class="sxs-lookup"><span data-stu-id="f4ff1-165">Contact [LockPath Keylight Client support team](https://www.lockpath.com/contact/) tooget these values.</span></span> 

4. <span data-ttu-id="f4ff1-166">Na powitania **certyfikat podpisywania SAML** kliknij **Certificate(Raw)** , a następnie zapisz plik certyfikatu hello na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="f4ff1-166">On hello **SAML Signing Certificate** section, click **Certificate(Raw)** and then save hello certificate file on your computer.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-keylight-tutorial/tutorial_keylight_certificate.png) 

5. <span data-ttu-id="f4ff1-168">Kliknij przycisk **zapisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="f4ff1-168">Click **Save** button.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-keylight-tutorial/tutorial_general_400.png)
    
6. <span data-ttu-id="f4ff1-170">Na powitania **konfiguracji Keylight LockPath** kliknij **skonfigurować LockPath Keylight** tooopen **Konfigurowanie logowania jednokrotnego** okna.</span><span class="sxs-lookup"><span data-stu-id="f4ff1-170">On hello **LockPath Keylight Configuration** section, click **Configure LockPath Keylight** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="f4ff1-171">Kopiuj hello **Sign-Out adresu URL i SAML pojedynczy znak na adres URL usługi** z hello **sekcji krótkimi opisami.**</span><span class="sxs-lookup"><span data-stu-id="f4ff1-171">Copy hello **Sign-Out URL and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-keylight-tutorial/tutorial_keylight_configure.png) 

7. <span data-ttu-id="f4ff1-173">Logowanie Jednokrotne w LockPath Keylight tooenable wykonaj hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="f4ff1-173">tooenable SSO in LockPath Keylight, perform hello following steps:</span></span>
   
    <span data-ttu-id="f4ff1-174">a.</span><span class="sxs-lookup"><span data-stu-id="f4ff1-174">a.</span></span> <span data-ttu-id="f4ff1-175">Zaloguj się na tooyour LockPath Keylight konto jako administrator.</span><span class="sxs-lookup"><span data-stu-id="f4ff1-175">Sign-on tooyour LockPath Keylight account as administrator.</span></span>
    
    <span data-ttu-id="f4ff1-176">b.</span><span class="sxs-lookup"><span data-stu-id="f4ff1-176">b.</span></span> <span data-ttu-id="f4ff1-177">W menu hello na górze hello, kliknij przycisk **osoby**i wybierz **Keylight Instalatora**.</span><span class="sxs-lookup"><span data-stu-id="f4ff1-177">In hello menu on hello top, click **Person**, and select **Keylight Setup**.</span></span>
   
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-keylight-tutorial/401.png) 

    <span data-ttu-id="f4ff1-179">c.</span><span class="sxs-lookup"><span data-stu-id="f4ff1-179">c.</span></span> <span data-ttu-id="f4ff1-180">W elemencie treeview hello powitania po lewej stronie, kliknij przycisk **SAML**.</span><span class="sxs-lookup"><span data-stu-id="f4ff1-180">In hello treeview on hello left, click **SAML**.</span></span>
   
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-keylight-tutorial/402.png) 

    <span data-ttu-id="f4ff1-182">d.</span><span class="sxs-lookup"><span data-stu-id="f4ff1-182">d.</span></span> <span data-ttu-id="f4ff1-183">Na powitania **ustawienia SAML** okna dialogowego, kliknij przycisk **Edytuj**.</span><span class="sxs-lookup"><span data-stu-id="f4ff1-183">On hello **SAML Settings** dialog, click **Edit**.</span></span>
   
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-keylight-tutorial/404.png) 

8. <span data-ttu-id="f4ff1-185">Na powitania **edytowanie ustawień SAML** okna dialogowego wykonaj hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="f4ff1-185">On hello **Edit SAML Settings** dialog page, perform hello following steps:</span></span>
   
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-keylight-tutorial/405.png) 
   
    <span data-ttu-id="f4ff1-187">a.</span><span class="sxs-lookup"><span data-stu-id="f4ff1-187">a.</span></span> <span data-ttu-id="f4ff1-188">Ustaw **uwierzytelnianie SAML** za**Active**.</span><span class="sxs-lookup"><span data-stu-id="f4ff1-188">Set **SAML authentication** too**Active**.</span></span>

    <span data-ttu-id="f4ff1-189">b.</span><span class="sxs-lookup"><span data-stu-id="f4ff1-189">b.</span></span> <span data-ttu-id="f4ff1-190">Wklej hello **SAML pojedynczy znak na adres URL usługi** wartość, która została skopiowana z hello portalu Azure do hello **adresu URL logowania do dostawcy tożsamości** pola tekstowego.</span><span class="sxs-lookup"><span data-stu-id="f4ff1-190">Paste hello **SAML Single Sign-On Service URL** value which you have copied from hello Azure portal into hello **Identity Provider Login URL** textbox.</span></span>

    <span data-ttu-id="f4ff1-191">c.</span><span class="sxs-lookup"><span data-stu-id="f4ff1-191">c.</span></span> <span data-ttu-id="f4ff1-192">Wklej hello **pojedynczy adres URL usługi Sign-Out** wartość, która została skopiowana z hello portalu Azure do hello **adres URL wylogowania dostawcy tożsamości** pola tekstowego.</span><span class="sxs-lookup"><span data-stu-id="f4ff1-192">Paste hello **Single Sign-Out Service URL** value which you have copied from hello Azure portal into hello **Identity Provider Logout URL** textbox.</span></span>

    <span data-ttu-id="f4ff1-193">d.</span><span class="sxs-lookup"><span data-stu-id="f4ff1-193">d.</span></span> <span data-ttu-id="f4ff1-194">Kliknij przycisk **wybierz plik** tooselect odcisk Twojej pobrany LockPath Keylight, a następnie kliknij przycisk **Otwórz** tooupload hello certyfikatu.</span><span class="sxs-lookup"><span data-stu-id="f4ff1-194">Click **Choose File** tooselect your downloaded LockPath Keylight certificate, and then click **Open** tooupload hello certificate.</span></span>

    <span data-ttu-id="f4ff1-195">e.</span><span class="sxs-lookup"><span data-stu-id="f4ff1-195">e.</span></span> <span data-ttu-id="f4ff1-196">Ustaw **lokalizacji identyfikator użytkownika SAML** za**elementu NameIdentifier hello podmiotu instrukcji**.</span><span class="sxs-lookup"><span data-stu-id="f4ff1-196">Set **SAML User Id location** too**NameIdentifier element of hello subject statement**.</span></span>
    
    <span data-ttu-id="f4ff1-197">f.</span><span class="sxs-lookup"><span data-stu-id="f4ff1-197">f.</span></span> <span data-ttu-id="f4ff1-198">Podaj hello **dostawcy usług Keylight** przy użyciu hello następującego wzorca: **https://&lt;NazwaFirmy&gt;. keylightgrc.com**.</span><span class="sxs-lookup"><span data-stu-id="f4ff1-198">Provide hello **Keylight Service Provider** using hello following pattern: **https://&lt;CompanyName&gt;.keylightgrc.com**.</span></span>
    
    <span data-ttu-id="f4ff1-199">g.</span><span class="sxs-lookup"><span data-stu-id="f4ff1-199">g.</span></span> <span data-ttu-id="f4ff1-200">Ustaw **automatycznego udostępniania użytkownikom** za**Active**.</span><span class="sxs-lookup"><span data-stu-id="f4ff1-200">Set **Auto-provision users** too**Active**.</span></span>

    <span data-ttu-id="f4ff1-201">h.</span><span class="sxs-lookup"><span data-stu-id="f4ff1-201">h.</span></span> <span data-ttu-id="f4ff1-202">Ustaw **typ konta Auto-provision** za**pełnej**.</span><span class="sxs-lookup"><span data-stu-id="f4ff1-202">Set **Auto-provision account type** too**Full User**.</span></span>

    <span data-ttu-id="f4ff1-203">i.</span><span class="sxs-lookup"><span data-stu-id="f4ff1-203">i.</span></span> <span data-ttu-id="f4ff1-204">Ustaw **roli zabezpieczeń Auto-provision**, wybierz pozycję **użytkowników standardowych z SAML**.</span><span class="sxs-lookup"><span data-stu-id="f4ff1-204">Set **Auto-provision security role**, select **Standard User with SAML**.</span></span>
    
    <span data-ttu-id="f4ff1-205">j.</span><span class="sxs-lookup"><span data-stu-id="f4ff1-205">j.</span></span> <span data-ttu-id="f4ff1-206">Ustaw **konfiguracji zabezpieczeń Auto-provision**, wybierz pozycję **standardowej konfiguracji użytkownika**.</span><span class="sxs-lookup"><span data-stu-id="f4ff1-206">Set **Auto-provision security config**, select **Standard User Configuration**.</span></span>
     
    <span data-ttu-id="f4ff1-207">k.</span><span class="sxs-lookup"><span data-stu-id="f4ff1-207">k.</span></span> <span data-ttu-id="f4ff1-208">W hello **atrybut poczty E-mail** pole tekstowe, typ `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress`.</span><span class="sxs-lookup"><span data-stu-id="f4ff1-208">In hello **Email attribute** textbox, type `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress`.</span></span>
    
    <span data-ttu-id="f4ff1-209">l.</span><span class="sxs-lookup"><span data-stu-id="f4ff1-209">l.</span></span> <span data-ttu-id="f4ff1-210">W hello **atrybutu imię** pole tekstowe, typ `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname`.</span><span class="sxs-lookup"><span data-stu-id="f4ff1-210">In hello **First name attribute** textbox, type `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname`.</span></span>
    
    <span data-ttu-id="f4ff1-211">m.</span><span class="sxs-lookup"><span data-stu-id="f4ff1-211">m.</span></span> <span data-ttu-id="f4ff1-212">W hello **ostatniego atrybutu name** pole tekstowe, typ `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/surname`.</span><span class="sxs-lookup"><span data-stu-id="f4ff1-212">In hello **Last name attribute** textbox, type `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/surname`.</span></span>
    
    <span data-ttu-id="f4ff1-213">n.</span><span class="sxs-lookup"><span data-stu-id="f4ff1-213">n.</span></span> <span data-ttu-id="f4ff1-214">Kliknij pozycję **Zapisz**.</span><span class="sxs-lookup"><span data-stu-id="f4ff1-214">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="f4ff1-215">Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz hello [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji hello!</span><span class="sxs-lookup"><span data-stu-id="f4ff1-215">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="f4ff1-216">Po dodaniu tej aplikacji z hello **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij hello **rejestracji jednokrotnej** hello kartę i dostępu do osadzonych dokumentacji za pośrednictwem hello  **Konfiguracja** sekcji u dołu hello.</span><span class="sxs-lookup"><span data-stu-id="f4ff1-216">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="f4ff1-217">Więcej o hello osadzonych dokumentacji funkcji w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="f4ff1-217">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="f4ff1-218">Tworzenie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="f4ff1-218">Creating an Azure AD test user</span></span>
<span data-ttu-id="f4ff1-219">Celem Hello w tej sekcji jest toocreate użytkownika testowego, w portalu Azure o nazwie Simona Britta hello.</span><span class="sxs-lookup"><span data-stu-id="f4ff1-219">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Tworzenie użytkowników usługi Azure AD][100]

<span data-ttu-id="f4ff1-221">**toocreate użytkownika testowego w usłudze Azure AD, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="f4ff1-221">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="f4ff1-222">W hello **portalu Azure**na temat hello w lewym okienku nawigacji, kliknij przycisk **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="f4ff1-222">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-keylight-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="f4ff1-224">toodisplay hello listę użytkowników, przejdź zbyt**użytkowników i grup** i kliknij przycisk **wszyscy użytkownicy**.</span><span class="sxs-lookup"><span data-stu-id="f4ff1-224">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-keylight-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="f4ff1-226">Witaj tooopen **użytkownika** okna dialogowego, kliknij przycisk **Dodaj** u góry hello hello okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="f4ff1-226">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-keylight-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="f4ff1-228">Na powitania **użytkownika** okna dialogowego wykonaj hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="f4ff1-228">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-keylight-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="f4ff1-230">a.</span><span class="sxs-lookup"><span data-stu-id="f4ff1-230">a.</span></span> <span data-ttu-id="f4ff1-231">W hello **nazwa** pole tekstowe, typ **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="f4ff1-231">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="f4ff1-232">b.</span><span class="sxs-lookup"><span data-stu-id="f4ff1-232">b.</span></span> <span data-ttu-id="f4ff1-233">W hello **nazwy użytkownika** pole tekstowe, hello typu **adres e-mail** z BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="f4ff1-233">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="f4ff1-234">c.</span><span class="sxs-lookup"><span data-stu-id="f4ff1-234">c.</span></span> <span data-ttu-id="f4ff1-235">Wybierz **Pokaż hasło** i zanotuj wartość hello hello **hasło**.</span><span class="sxs-lookup"><span data-stu-id="f4ff1-235">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="f4ff1-236">d.</span><span class="sxs-lookup"><span data-stu-id="f4ff1-236">d.</span></span> <span data-ttu-id="f4ff1-237">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="f4ff1-237">Click **Create**.</span></span>
 
### <a name="creating-a-lockpath-keylight-test-user"></a><span data-ttu-id="f4ff1-238">Tworzenie użytkownika testowego LockPath Keylight</span><span class="sxs-lookup"><span data-stu-id="f4ff1-238">Creating a LockPath Keylight test user</span></span>

<span data-ttu-id="f4ff1-239">W tej sekcji należy utworzyć użytkownika o nazwie Simona Britta w LockPath Keylight.</span><span class="sxs-lookup"><span data-stu-id="f4ff1-239">In this section, you create a user called Britta Simon in LockPath Keylight.</span></span> <span data-ttu-id="f4ff1-240">LockPath Keylight obsługę w czasie, który jest domyślnie włączona.</span><span class="sxs-lookup"><span data-stu-id="f4ff1-240">LockPath Keylight supports just-in-time provisioning, which is enabled by default.</span></span>

<span data-ttu-id="f4ff1-241">Nie ma elementu akcji można w tej sekcji.</span><span class="sxs-lookup"><span data-stu-id="f4ff1-241">There is no action item for you in this section.</span></span> <span data-ttu-id="f4ff1-242">Nowy użytkownik jest tworzony podczas uzyskiwania dostępu do LockPath Keylight, jeśli jeszcze nie istnieje hello użytkownika.</span><span class="sxs-lookup"><span data-stu-id="f4ff1-242">A new user is created when accessing LockPath Keylight if hello user doesn't exist yet.</span></span> 

>[!NOTE]
><span data-ttu-id="f4ff1-243">Jeśli potrzebujesz ręcznie toocreate użytkownika, należy toocontact hello [zespołem pomocy technicznej klienta Keylight LockPath](https://www.lockpath.com/contact/).</span><span class="sxs-lookup"><span data-stu-id="f4ff1-243">If you need toocreate a user manually, you need toocontact hello [LockPath Keylight Client support team](https://www.lockpath.com/contact/).</span></span> 

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="f4ff1-244">Przypisanie użytkownika testowego hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="f4ff1-244">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="f4ff1-245">W tej sekcji możesz włączyć toouse Simona Britta Azure logowania jednokrotnego za udzielanie dostępu tooLockPath Keylight.</span><span class="sxs-lookup"><span data-stu-id="f4ff1-245">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooLockPath Keylight.</span></span>

![Przypisz użytkownika][200] 

<span data-ttu-id="f4ff1-247">**tooassign tooLockPath Simona Britta Keylight, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="f4ff1-247">**tooassign Britta Simon tooLockPath Keylight, perform hello following steps:**</span></span>

1. <span data-ttu-id="f4ff1-248">W portalu Azure hello, otwórz widok aplikacji hello, a następnie przejdź do widoku katalogu toohello i przejść za**aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="f4ff1-248">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Przypisz użytkownika][201] 

2. <span data-ttu-id="f4ff1-250">Z listy aplikacji hello wybierz **LockPath Keylight**.</span><span class="sxs-lookup"><span data-stu-id="f4ff1-250">In hello applications list, select **LockPath Keylight**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-keylight-tutorial/tutorial_keylight_app.png) 

3. <span data-ttu-id="f4ff1-252">W menu powitania po lewej stronie powitania kliknij **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="f4ff1-252">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Przypisz użytkownika][202] 

4. <span data-ttu-id="f4ff1-254">Kliknij przycisk **Dodaj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="f4ff1-254">Click **Add** button.</span></span> <span data-ttu-id="f4ff1-255">Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="f4ff1-255">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Przypisz użytkownika][203]

5. <span data-ttu-id="f4ff1-257">Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** hello listy użytkowników.</span><span class="sxs-lookup"><span data-stu-id="f4ff1-257">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="f4ff1-258">Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="f4ff1-258">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="f4ff1-259">Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="f4ff1-259">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="f4ff1-260">Testowanie rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="f4ff1-260">Testing single sign-on</span></span>

<span data-ttu-id="f4ff1-261">W tej sekcji można przetestować konfiguracji usługi Azure AD pojedynczego logowania jednokrotnego przy użyciu hello panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="f4ff1-261">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="f4ff1-262">Po kliknięciu hello LockPath Keylight kafelka w hello Panel dostępu, należy pobrać zalogowane automatycznie tooyour LockPath Keylight aplikacji.</span><span class="sxs-lookup"><span data-stu-id="f4ff1-262">When you click hello LockPath Keylight tile in hello Access Panel, you should get automatically signed-on tooyour LockPath Keylight application.</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="f4ff1-263">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="f4ff1-263">Additional resources</span></span>

* [<span data-ttu-id="f4ff1-264">Lista samouczków dotyczących tooIntegrate aplikacji SaaS w usłudze Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="f4ff1-264">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="f4ff1-265">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="f4ff1-265">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-keylight-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-keylight-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-keylight-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-keylight-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-keylight-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-keylight-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-keylight-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-keylight-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-keylight-tutorial/tutorial_general_203.png

