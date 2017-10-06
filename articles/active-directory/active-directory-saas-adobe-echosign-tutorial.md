---
title: "Samouczek: Integracji Azure Active Directory przy użyciu konta Adobe | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak tooconfigure logowanie jednokrotne między usługą Azure Active Directory i Adobe logowania."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: f9385723-8fe7-4340-8afb-1508dac3e92b
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/24/2017
ms.author: jeedes
ms.openlocfilehash: b4b07907f30a0890003554a02a76d968400b43ba
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-adobe-sign"></a><span data-ttu-id="e88d5-103">Samouczek: Integracji Azure Active Directory przy użyciu konta Adobe</span><span class="sxs-lookup"><span data-stu-id="e88d5-103">Tutorial: Azure Active Directory integration with Adobe Sign</span></span>

<span data-ttu-id="e88d5-104">Z tego samouczka, dowiesz się, jak toointegrate Adobe zarejestrować w usłudze Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="e88d5-104">In this tutorial, you learn how toointegrate Adobe Sign with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="e88d5-105">Integracji Podpisz Adobe z usługą Azure AD zapewnia hello następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="e88d5-105">Integrating Adobe Sign with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="e88d5-106">Można kontrolować w usłudze Azure AD, kto ma dostęp tooAdobe logowania</span><span class="sxs-lookup"><span data-stu-id="e88d5-106">You can control in Azure AD who has access tooAdobe Sign</span></span>
- <span data-ttu-id="e88d5-107">Można włączyć użytkownika użytkownicy tooautomatically get zalogowane tooAdobe logowania (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="e88d5-107">You can enable your users tooautomatically get signed-on tooAdobe Sign (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="e88d5-108">Możesz zarządzać kont w jednej centralnej lokalizacji - hello portalu Azure</span><span class="sxs-lookup"><span data-stu-id="e88d5-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="e88d5-109">Jeśli chcesz tooknow więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="e88d5-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e88d5-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="e88d5-110">Prerequisites</span></span>

<span data-ttu-id="e88d5-111">tooconfigure integracji usługi Azure AD przy użyciu konta Adobe należy hello następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="e88d5-111">tooconfigure Azure AD integration with Adobe Sign, you need hello following items:</span></span>

- <span data-ttu-id="e88d5-112">Subskrypcję usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="e88d5-112">An Azure AD subscription</span></span>
- <span data-ttu-id="e88d5-113">Adobe logowania jednokrotnego włączone subskrypcji</span><span class="sxs-lookup"><span data-stu-id="e88d5-113">An Adobe Sign single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="e88d5-114">tootest hello kroków w tym samouczku, zaleca się przy użyciu środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="e88d5-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="e88d5-115">tootest hello kroki opisane w tym samouczku, należy stosować te zalecenia:</span><span class="sxs-lookup"><span data-stu-id="e88d5-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="e88d5-116">Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="e88d5-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="e88d5-117">Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz pobrać miesięczna wersja próbna [tutaj](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="e88d5-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="e88d5-118">Opis scenariusza</span><span class="sxs-lookup"><span data-stu-id="e88d5-118">Scenario description</span></span>
<span data-ttu-id="e88d5-119">W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym.</span><span class="sxs-lookup"><span data-stu-id="e88d5-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="e88d5-120">Scenariusz Hello opisane w tym samouczku składa się z dwóch głównych elementów:</span><span class="sxs-lookup"><span data-stu-id="e88d5-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="e88d5-121">Dodawanie Adobe logowania z galerii hello</span><span class="sxs-lookup"><span data-stu-id="e88d5-121">Adding Adobe Sign from hello gallery</span></span>
2. <span data-ttu-id="e88d5-122">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="e88d5-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-adobe-sign-from-hello-gallery"></a><span data-ttu-id="e88d5-123">Dodawanie Adobe logowania z galerii hello</span><span class="sxs-lookup"><span data-stu-id="e88d5-123">Adding Adobe Sign from hello gallery</span></span>
<span data-ttu-id="e88d5-124">tooconfigure hello integracji Podpisz Adobe do usługi Azure AD, należy tooadd Adobe logowania z hello galerii tooyour listę zarządzanych aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="e88d5-124">tooconfigure hello integration of Adobe Sign into Azure AD, you need tooadd Adobe Sign from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="e88d5-125">**tooadd Adobe logowania z galerii hello wykonaj hello następujące kroki:**</span><span class="sxs-lookup"><span data-stu-id="e88d5-125">**tooadd Adobe Sign from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="e88d5-126">W hello  **[portalu Azure](https://portal.azure.com)**na temat hello panelu nawigacji po lewej stronie, kliknij przycisk **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="e88d5-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Usługa Active Directory][1]

2. <span data-ttu-id="e88d5-128">Przejdź za**aplikacje dla przedsiębiorstw**.</span><span class="sxs-lookup"><span data-stu-id="e88d5-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="e88d5-129">Następnie przejdź zbyt**wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="e88d5-129">Then go too**All applications**.</span></span>

    ![Aplikacje][2]
    
3. <span data-ttu-id="e88d5-131">tooadd nową aplikację, kliknij przycisk **nowej aplikacji** przycisk u góry hello okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="e88d5-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplikacje][3]

4. <span data-ttu-id="e88d5-133">W polu wyszukiwania hello wpisz **znak Adobe**.</span><span class="sxs-lookup"><span data-stu-id="e88d5-133">In hello search box, type **Adobe Sign**.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-adobe-echosign-tutorial/tutorial_adobesign_search.png)

5. <span data-ttu-id="e88d5-135">W panelu wyników hello, wybierz **znak Adobe**, a następnie kliknij przycisk **Dodaj** przycisk aplikacji hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="e88d5-135">In hello results panel, select **Adobe Sign**, and then click **Add** button tooadd hello application.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-adobe-echosign-tutorial/tutorial_adobesign_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="e88d5-137">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="e88d5-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="e88d5-138">W tej sekcji możesz skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej znakiem Adobe oparte na koncie użytkownika testu o nazwie "Britta Simona".</span><span class="sxs-lookup"><span data-stu-id="e88d5-138">In this section, you configure and test Azure AD single sign-on with Adobe Sign based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="e88d5-139">Dla pojedynczego logowania jednokrotnego toowork usługi Azure AD musi tooknow użytkownika odpowiednikiem hello Adobe rejestracja jest tooa użytkownika w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="e88d5-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Adobe Sign is tooa user in Azure AD.</span></span> <span data-ttu-id="e88d5-140">Innymi słowy relację łącza między użytkownika usługi Azure AD i hello użytkownikowi rejestracja Adobe musi toobe ustanowione.</span><span class="sxs-lookup"><span data-stu-id="e88d5-140">In other words, a link relationship between an Azure AD user and hello related user in Adobe Sign needs toobe established.</span></span>

<span data-ttu-id="e88d5-141">W Adobe logowania, należy przypisać wartość hello hello **nazwy użytkownika** w usłudze Azure AD jako wartość hello hello **Username** tooestablish hello łącze relacji.</span><span class="sxs-lookup"><span data-stu-id="e88d5-141">In Adobe Sign, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="e88d5-142">tooconfigure i test usługi Azure AD logowania jednokrotnego przy użyciu konta Adobe należy hello toocomplete po bloków konstrukcyjnych:</span><span class="sxs-lookup"><span data-stu-id="e88d5-142">tooconfigure and test Azure AD single sign-on with Adobe Sign, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="e88d5-143">**[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configuring-azure-ad-single-sign-on)**  -tooenable Twojego toouse użytkowników tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="e88d5-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="e88d5-144">**[Tworzenie użytkownika testowego usługi Azure AD](#creating-an-azure-ad-test-user)**  -tootest usługi Azure AD rejestracji jednokrotnej z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="e88d5-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="e88d5-145">**[Tworzenie użytkownika testowego znak Adobe](#creating-an-adobe-sign-test-user)**  -toohave odpowiednikiem Simona Britta w Adobe znaku, który jest odpowiednikiem połączonych toohello usługi Azure AD użytkownika.</span><span class="sxs-lookup"><span data-stu-id="e88d5-145">**[Creating an Adobe Sign test user](#creating-an-adobe-sign-test-user)** - toohave a counterpart of Britta Simon in Adobe Sign that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="e88d5-146">**[Przypisanie użytkownika testowego hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Simona Britta toouse usługi Azure AD rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="e88d5-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="e88d5-147">**[Testowanie rejestracji jednokrotnej](#testing-single-sign-on)**  -tooverify czy hello konfiguracji działania.</span><span class="sxs-lookup"><span data-stu-id="e88d5-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="e88d5-148">Konfigurowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="e88d5-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="e88d5-149">W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w hello portalu Azure i skonfigurować rejestracji jednokrotnej w aplikacji Adobe logowania.</span><span class="sxs-lookup"><span data-stu-id="e88d5-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Adobe Sign application.</span></span>

<span data-ttu-id="e88d5-150">**tooconfigure usługi Azure AD logowania jednokrotnego przy użyciu konta Adobe wykonaj hello następujące kroki:**</span><span class="sxs-lookup"><span data-stu-id="e88d5-150">**tooconfigure Azure AD single sign-on with Adobe Sign, perform hello following steps:**</span></span>

1. <span data-ttu-id="e88d5-151">W portalu Azure na powitania hello **znak Adobe** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.</span><span class="sxs-lookup"><span data-stu-id="e88d5-151">In hello Azure portal, on hello **Adobe Sign** application integration page, click **Single sign-on**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej][4]

2. <span data-ttu-id="e88d5-153">Na powitania **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** tooenable rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="e88d5-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-adobe-echosign-tutorial/tutorial_adobesign_samlbase.png)

3. <span data-ttu-id="e88d5-155">Na powitania **Adobe logowania domeny i adres URL** sekcji, wykonaj następujące kroki hello:</span><span class="sxs-lookup"><span data-stu-id="e88d5-155">On hello **Adobe Sign Domain and URLs** section, perform hello following steps:</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-adobe-echosign-tutorial/tutorial_adobesign_url.png)

    <span data-ttu-id="e88d5-157">a.</span><span class="sxs-lookup"><span data-stu-id="e88d5-157">a.</span></span> <span data-ttu-id="e88d5-158">W hello **adres URL logowania** tekstowym, wpisz adres URL za pomocą hello następującego wzorca:`https://<companyname>.echosign.com/`</span><span class="sxs-lookup"><span data-stu-id="e88d5-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<companyname>.echosign.com/`</span></span>

    <span data-ttu-id="e88d5-159">b.</span><span class="sxs-lookup"><span data-stu-id="e88d5-159">b.</span></span> <span data-ttu-id="e88d5-160">W hello **identyfikator** tekstowym, wpisz adres URL za pomocą hello następującego wzorca:`https://<companyname>.echosign.com`</span><span class="sxs-lookup"><span data-stu-id="e88d5-160">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<companyname>.echosign.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="e88d5-161">Wartości te nie są prawdziwe.</span><span class="sxs-lookup"><span data-stu-id="e88d5-161">These values are not real.</span></span> <span data-ttu-id="e88d5-162">Zaktualizować te wartości z hello rzeczywisty adres URL logowania i identyfikator.</span><span class="sxs-lookup"><span data-stu-id="e88d5-162">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="e88d5-163">Skontaktuj się z [zespołem pomocy technicznej klienta logowania Adobe](https://helpx.adobe.com/in/contact/support.html) tooget tych wartości.</span><span class="sxs-lookup"><span data-stu-id="e88d5-163">Contact [Adobe Sign Client support team](https://helpx.adobe.com/in/contact/support.html) tooget these values.</span></span> 
 
4. <span data-ttu-id="e88d5-164">Na powitania **certyfikat podpisywania SAML** kliknij **Certificate(Base64)** , a następnie zapisz plik certyfikatu hello na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="e88d5-164">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-adobe-echosign-tutorial/tutorial_adobesign_certificate.png) 

5. <span data-ttu-id="e88d5-166">Kliknij przycisk **zapisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="e88d5-166">Click **Save** button.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-adobe-echosign-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="e88d5-168">Na powitania **konfiguracji logowania Adobe** kliknij **Konfigurowanie rejestrowania programu Adobe** tooopen **Konfigurowanie logowania jednokrotnego** okna.</span><span class="sxs-lookup"><span data-stu-id="e88d5-168">On hello **Adobe Sign Configuration** section, click **Configure Adobe Sign** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="e88d5-169">Kopiuj hello **Sign-Out adres URL, identyfikator jednostki SAML i SAML pojedynczy znak na adres URL usługi** z hello **sekcji krótkimi opisami.**</span><span class="sxs-lookup"><span data-stu-id="e88d5-169">Copy hello **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-adobe-echosign-tutorial/tutorial_adobesign_configure.png) 


7. <span data-ttu-id="e88d5-171">W oknie przeglądarki innej witryny sieci web Zaloguj się w witrynie firmy Adobe znak tooyour jako administrator.</span><span class="sxs-lookup"><span data-stu-id="e88d5-171">In a different web browser window, log in tooyour Adobe Sign company site as an administrator.</span></span>

8. <span data-ttu-id="e88d5-172">Hello menu u góry hello, kliknij przycisk **konta**, a następnie w okienku nawigacji powitania po lewej stronie powitania kliknij **ustawienia SAML** w obszarze **ustawienia konta**.</span><span class="sxs-lookup"><span data-stu-id="e88d5-172">In hello menu on hello top, click **Account**, and then, in hello navigation pane on hello left side, click **SAML Settings** under **Account Settings**.</span></span>
   
   <span data-ttu-id="e88d5-173">![Konto](./media/active-directory-saas-adobe-echosign-tutorial/ic789520.png "konta")</span><span class="sxs-lookup"><span data-stu-id="e88d5-173">![Account](./media/active-directory-saas-adobe-echosign-tutorial/ic789520.png "Account")</span></span>

9. <span data-ttu-id="e88d5-174">W sekcji Ustawienia SAML hello wykonaj następujące kroki hello:</span><span class="sxs-lookup"><span data-stu-id="e88d5-174">In hello SAML Settings section, perform hello following steps:</span></span>
   
   <span data-ttu-id="e88d5-175">![Ustawienia SAML](./media/active-directory-saas-adobe-echosign-tutorial/ic789521.png "ustawienia SAML")</span><span class="sxs-lookup"><span data-stu-id="e88d5-175">![SAML Settings](./media/active-directory-saas-adobe-echosign-tutorial/ic789521.png "SAML Settings")</span></span>
   
   <span data-ttu-id="e88d5-176">a.</span><span class="sxs-lookup"><span data-stu-id="e88d5-176">a.</span></span> <span data-ttu-id="e88d5-177">Jako **tryb SAML**, wybierz pozycję **SAML obowiązkowe**.</span><span class="sxs-lookup"><span data-stu-id="e88d5-177">As **SAML Mode**, select **SAML Mandatory**.</span></span>
   
   <span data-ttu-id="e88d5-178">b.</span><span class="sxs-lookup"><span data-stu-id="e88d5-178">b.</span></span> <span data-ttu-id="e88d5-179">Wybierz **toolog Zezwalaj EchoSign Administratorzy konta przy użyciu swoich poświadczeń EchoSign**.</span><span class="sxs-lookup"><span data-stu-id="e88d5-179">Select **Allow EchoSign Account Administrators toolog in using their EchoSign Credentials**.</span></span>
   
   <span data-ttu-id="e88d5-180">c.</span><span class="sxs-lookup"><span data-stu-id="e88d5-180">c.</span></span> <span data-ttu-id="e88d5-181">Jako **Tworzenie użytkownika**, wybierz pozycję **automatyczne dodawanie użytkowników uwierzytelnionych za pośrednictwem SAML**.</span><span class="sxs-lookup"><span data-stu-id="e88d5-181">As **User Creation**, select **Automatically add users authenticated through SAML**.</span></span>

10. <span data-ttu-id="e88d5-182">Przenieś, wykonywanie hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="e88d5-182">Move on, performing hello following steps:</span></span>

       <span data-ttu-id="e88d5-183">![Ustawienia SAML](./media/active-directory-saas-adobe-echosign-tutorial/ic789522.png "ustawienia SAML")</span><span class="sxs-lookup"><span data-stu-id="e88d5-183">![SAML Settings](./media/active-directory-saas-adobe-echosign-tutorial/ic789522.png "SAML Settings")</span></span>

    <span data-ttu-id="e88d5-184">a.</span><span class="sxs-lookup"><span data-stu-id="e88d5-184">a.</span></span> <span data-ttu-id="e88d5-185">Wklej **SAML identyfikator jednostki**, która została skopiowana z portalu Azure do hello **identyfikator jednostki IdP** pole tekstowe.</span><span class="sxs-lookup"><span data-stu-id="e88d5-185">Paste **SAML Entity ID**, which you have copied from Azure portal into hello **IdP Entity ID** textbox.</span></span>
    
    <span data-ttu-id="e88d5-186">b.</span><span class="sxs-lookup"><span data-stu-id="e88d5-186">b.</span></span> <span data-ttu-id="e88d5-187">Wklej **SAML pojedynczy znak na adres URL usługi**, która została skopiowana z portalu Azure do hello **adres URL logowania IdP** pole tekstowe.</span><span class="sxs-lookup"><span data-stu-id="e88d5-187">Paste **SAML Single Sign-On Service URL**, which you have copied from Azure portal into hello **IdP Login URL** textbox.</span></span>
   
    <span data-ttu-id="e88d5-188">c.</span><span class="sxs-lookup"><span data-stu-id="e88d5-188">c.</span></span> <span data-ttu-id="e88d5-189">Wklej **Sign-Out adres URL**, która została skopiowana z portalu Azure do hello **adresu URL wylogowania IdP** pola tekstowego.</span><span class="sxs-lookup"><span data-stu-id="e88d5-189">Paste **Sign-Out URL**, which you have copied from Azure portal into hello **IdP Logout URL** textbox.</span></span>

    <span data-ttu-id="e88d5-190">d.</span><span class="sxs-lookup"><span data-stu-id="e88d5-190">d.</span></span> <span data-ttu-id="e88d5-191">Otwórz z pobranego **Certificate(Base64)** pliku w Notatniku hello kopiowania zawartości go do Schowka, a następnie wklej go toohello **certyfikatu IdP** pole tekstowe</span><span class="sxs-lookup"><span data-stu-id="e88d5-191">Open your downloaded **Certificate(Base64)** file in notepad, copy hello content of it into your clipboard, and then paste it toohello **IdP Certificate** textbox</span></span>

    <span data-ttu-id="e88d5-192">e.</span><span class="sxs-lookup"><span data-stu-id="e88d5-192">e.</span></span> <span data-ttu-id="e88d5-193">Kliknij przycisk **zapisać zmiany**.</span><span class="sxs-lookup"><span data-stu-id="e88d5-193">Click **Save Changes**.</span></span>

> [!TIP]
> <span data-ttu-id="e88d5-194">Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz hello [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji hello!</span><span class="sxs-lookup"><span data-stu-id="e88d5-194">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="e88d5-195">Po dodaniu tej aplikacji z hello **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij hello **rejestracji jednokrotnej** hello kartę i dostępu do osadzonych dokumentacji za pośrednictwem hello  **Konfiguracja** sekcji u dołu hello.</span><span class="sxs-lookup"><span data-stu-id="e88d5-195">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="e88d5-196">Więcej o hello osadzonych dokumentacji funkcji w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="e88d5-196">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="e88d5-197">Tworzenie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="e88d5-197">Creating an Azure AD test user</span></span>
<span data-ttu-id="e88d5-198">Celem Hello w tej sekcji jest toocreate użytkownika testowego, w portalu Azure o nazwie Simona Britta hello.</span><span class="sxs-lookup"><span data-stu-id="e88d5-198">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Tworzenie użytkowników usługi Azure AD][100]

<span data-ttu-id="e88d5-200">**toocreate użytkownika testowego w usłudze Azure AD, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="e88d5-200">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="e88d5-201">W hello **portalu Azure**na temat hello w lewym okienku nawigacji, kliknij przycisk **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="e88d5-201">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-adobe-echosign-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="e88d5-203">toodisplay hello listę użytkowników, przejdź zbyt**użytkowników i grup** i kliknij przycisk **wszyscy użytkownicy**.</span><span class="sxs-lookup"><span data-stu-id="e88d5-203">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-adobe-echosign-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="e88d5-205">Witaj tooopen **użytkownika** okna dialogowego, kliknij przycisk **Dodaj** u góry hello hello okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="e88d5-205">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-adobe-echosign-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="e88d5-207">Na powitania **użytkownika** okna dialogowego wykonaj hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="e88d5-207">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-adobe-echosign-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="e88d5-209">a.</span><span class="sxs-lookup"><span data-stu-id="e88d5-209">a.</span></span> <span data-ttu-id="e88d5-210">W hello **nazwa** pole tekstowe, typ **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="e88d5-210">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="e88d5-211">b.</span><span class="sxs-lookup"><span data-stu-id="e88d5-211">b.</span></span> <span data-ttu-id="e88d5-212">W hello **nazwy użytkownika** pole tekstowe, hello typu **adres e-mail** z BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="e88d5-212">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="e88d5-213">c.</span><span class="sxs-lookup"><span data-stu-id="e88d5-213">c.</span></span> <span data-ttu-id="e88d5-214">Wybierz **Pokaż hasło** i zanotuj wartość hello hello **hasło**.</span><span class="sxs-lookup"><span data-stu-id="e88d5-214">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="e88d5-215">d.</span><span class="sxs-lookup"><span data-stu-id="e88d5-215">d.</span></span> <span data-ttu-id="e88d5-216">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="e88d5-216">Click **Create**.</span></span>
 
### <a name="creating-an-adobe-sign-test-user"></a><span data-ttu-id="e88d5-217">Tworzenie użytkownika testowego Adobe logowania</span><span class="sxs-lookup"><span data-stu-id="e88d5-217">Creating an Adobe Sign test user</span></span>

<span data-ttu-id="e88d5-218">toolog użytkowników tooenable usługi Azure AD w tooAdobe logowania, muszą mieć przydzielone do programu Adobe logowania.</span><span class="sxs-lookup"><span data-stu-id="e88d5-218">tooenable Azure AD users toolog in tooAdobe Sign, they must be provisioned into Adobe Sign.</span></span> <span data-ttu-id="e88d5-219">W przypadku hello Adobe logowania Inicjowanie obsługi to zadanie ręczne.</span><span class="sxs-lookup"><span data-stu-id="e88d5-219">In hello case of Adobe Sign, provisioning is a manual task.</span></span>

>[!NOTE]
><span data-ttu-id="e88d5-220">Możesz użyć innych Adobe logowania użytkownika konta tworzenia narzędzi lub interfejsów API dostarczonych przez tooprovision Adobe logowania konta użytkownika usługi AAD.</span><span class="sxs-lookup"><span data-stu-id="e88d5-220">You can use any other Adobe Sign user account creation tools or APIs provided by Adobe Sign tooprovision AAD user accounts.</span></span> 

<span data-ttu-id="e88d5-221">**tooprovision konta użytkownika, należy wykonać hello następujące kroki:**</span><span class="sxs-lookup"><span data-stu-id="e88d5-221">**tooprovision a user account, perform hello following steps:**</span></span>

1. <span data-ttu-id="e88d5-222">Zaloguj się za tooyour **znak Adobe** witryny firmy jako administrator.</span><span class="sxs-lookup"><span data-stu-id="e88d5-222">Log in tooyour **Adobe Sign** company site as administrator.</span></span>

2. <span data-ttu-id="e88d5-223">Hello menu u góry hello, kliknij przycisk **konta**, a następnie w okienku nawigacji powitania po lewej stronie powitania kliknij **użytkownicy i grupy**, a następnie kliknij przycisk **utworzenie nowego użytkownika**.</span><span class="sxs-lookup"><span data-stu-id="e88d5-223">In hello menu on hello top, click **Account**, and then, in hello navigation pane on hello left side, click **Users & Groups**, and then, click **Create a new user**.</span></span>
   
   <span data-ttu-id="e88d5-224">![Konto](./media/active-directory-saas-adobe-echosign-tutorial/ic789524.png "konta")</span><span class="sxs-lookup"><span data-stu-id="e88d5-224">![Account](./media/active-directory-saas-adobe-echosign-tutorial/ic789524.png "Account")</span></span>
   
3. <span data-ttu-id="e88d5-225">W hello **Tworzenie nowego użytkownika** sekcji, wykonaj następujące kroki hello:</span><span class="sxs-lookup"><span data-stu-id="e88d5-225">In hello **Create New User** section, perform hello following steps:</span></span>
   
   <span data-ttu-id="e88d5-226">![Utwórz użytkownika](./media/active-directory-saas-adobe-echosign-tutorial/ic789525.png "Tworzenie użytkownika")</span><span class="sxs-lookup"><span data-stu-id="e88d5-226">![Create User](./media/active-directory-saas-adobe-echosign-tutorial/ic789525.png "Create User")</span></span>
   
   <span data-ttu-id="e88d5-227">a.</span><span class="sxs-lookup"><span data-stu-id="e88d5-227">a.</span></span> <span data-ttu-id="e88d5-228">Typ hello **adres E-mail**, **imię**, i **nazwisko** z prawidłowego konta usługi AAD mają tooprovision w hello związane z pól tekstowych.</span><span class="sxs-lookup"><span data-stu-id="e88d5-228">Type hello **Email Address**, **First Name**, and **Last Name** of a valid AAD account you want tooprovision into hello related textboxes.</span></span>
   
   <span data-ttu-id="e88d5-229">b.</span><span class="sxs-lookup"><span data-stu-id="e88d5-229">b.</span></span> <span data-ttu-id="e88d5-230">Kliknij przycisk **Utwórz użytkownika**.</span><span class="sxs-lookup"><span data-stu-id="e88d5-230">Click **Create User**.</span></span>

>[!NOTE]
><span data-ttu-id="e88d5-231">Właściciel konta usługi Azure Active Directory Hello otrzymuje wiadomość e-mail zawierającą łącze tooconfirm hello konta, zanim staje się aktywny.</span><span class="sxs-lookup"><span data-stu-id="e88d5-231">hello Azure Active Directory account holder receives an email that includes a link tooconfirm hello account before it becomes active.</span></span> 

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="e88d5-232">Przypisanie użytkownika testowego hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="e88d5-232">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="e88d5-233">W tej sekcji możesz włączyć toouse Simona Britta Azure logowania jednokrotnego za udzielanie dostępu tooAdobe logowania.</span><span class="sxs-lookup"><span data-stu-id="e88d5-233">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooAdobe Sign.</span></span>

![Przypisz użytkownika][200] 

<span data-ttu-id="e88d5-235">**tooassign tooAdobe Simona Britta logowania, należy wykonać hello następujące kroki:**</span><span class="sxs-lookup"><span data-stu-id="e88d5-235">**tooassign Britta Simon tooAdobe Sign, perform hello following steps:**</span></span>

1. <span data-ttu-id="e88d5-236">W portalu Azure hello, otwórz widok aplikacji hello, a następnie przejdź do widoku katalogu toohello i przejść za**aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="e88d5-236">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Przypisz użytkownika][201] 

2. <span data-ttu-id="e88d5-238">Z listy aplikacji hello wybierz **znak Adobe**.</span><span class="sxs-lookup"><span data-stu-id="e88d5-238">In hello applications list, select **Adobe Sign**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-adobe-echosign-tutorial/tutorial_adobesign_app.png) 

3. <span data-ttu-id="e88d5-240">W menu powitania po lewej stronie powitania kliknij **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="e88d5-240">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Przypisz użytkownika][202] 

4. <span data-ttu-id="e88d5-242">Kliknij przycisk **Dodaj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="e88d5-242">Click **Add** button.</span></span> <span data-ttu-id="e88d5-243">Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="e88d5-243">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Przypisz użytkownika][203]

5. <span data-ttu-id="e88d5-245">Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** hello listy użytkowników.</span><span class="sxs-lookup"><span data-stu-id="e88d5-245">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="e88d5-246">Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="e88d5-246">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="e88d5-247">Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="e88d5-247">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="e88d5-248">Testowanie rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="e88d5-248">Testing single sign-on</span></span>

<span data-ttu-id="e88d5-249">Po kliknięciu powitalne znak Adobe kafelka w hello Panel dostępu, należy pobrać automatycznie zalogowane tooyour Adobe logowania aplikacji.</span><span class="sxs-lookup"><span data-stu-id="e88d5-249">When you click hello Adobe Sign tile in hello Access Panel, you should get automatically signed-on tooyour Adobe Sign application.</span></span>
<span data-ttu-id="e88d5-250">Aby uzyskać więcej informacji na temat hello Panel dostępu, zobacz [toohello wprowadzenie panelu dostępu](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="e88d5-250">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="e88d5-251">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="e88d5-251">Additional resources</span></span>

* [<span data-ttu-id="e88d5-252">Lista samouczków dotyczących tooIntegrate aplikacji SaaS w usłudze Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="e88d5-252">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="e88d5-253">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="e88d5-253">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-adobe-echosign-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-adobe-echosign-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-adobe-echosign-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-adobe-echosign-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-adobe-echosign-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-adobe-echosign-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-adobe-echosign-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-adobe-echosign-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-adobe-echosign-tutorial/tutorial_general_203.png

