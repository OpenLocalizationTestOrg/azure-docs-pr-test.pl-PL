---
title: 'Samouczek: Integracji Azure Active Directory z LiquidFiles | Dokumentacja firmy Microsoft'
description: "Dowiedz się, jak tooconfigure logowanie jednokrotne między usługą Azure Active Directory i LiquidFiles."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: cb517134-0b34-4a74-b40c-5a3223ca81b6
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/14/2017
ms.author: jeedes
ms.openlocfilehash: 67eb888090f81e0ceb791ed45d564b98fe1eb6d2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-liquidfiles"></a><span data-ttu-id="83942-103">Samouczek: Integracji Azure Active Directory z LiquidFiles</span><span class="sxs-lookup"><span data-stu-id="83942-103">Tutorial: Azure Active Directory integration with LiquidFiles</span></span>

<span data-ttu-id="83942-104">Z tego samouczka, dowiesz się, jak toointegrate LiquidFiles w usłudze Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="83942-104">In this tutorial, you learn how toointegrate LiquidFiles with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="83942-105">Integracja z usługą Azure AD LiquidFiles zapewnia hello następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="83942-105">Integrating LiquidFiles with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="83942-106">Można kontrolować w usłudze Azure AD, kto ma dostęp do tooLiquidFiles</span><span class="sxs-lookup"><span data-stu-id="83942-106">You can control in Azure AD who has access tooLiquidFiles</span></span>
- <span data-ttu-id="83942-107">Można włączyć użytkownika użytkownicy tooautomatically get zalogowane tooLiquidFiles (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="83942-107">You can enable your users tooautomatically get signed-on tooLiquidFiles (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="83942-108">Możesz zarządzać kont w jednej centralnej lokalizacji - hello portalu Azure</span><span class="sxs-lookup"><span data-stu-id="83942-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="83942-109">Jeśli chcesz tooknow więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="83942-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="83942-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="83942-110">Prerequisites</span></span>

<span data-ttu-id="83942-111">tooconfigure integracji z usługą Azure AD z LiquidFiles należy hello następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="83942-111">tooconfigure Azure AD integration with LiquidFiles, you need hello following items:</span></span>

- <span data-ttu-id="83942-112">Subskrypcję usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="83942-112">An Azure AD subscription</span></span>
- <span data-ttu-id="83942-113">LiquidFiles logowanie jednokrotne włączone subskrypcji</span><span class="sxs-lookup"><span data-stu-id="83942-113">A LiquidFiles single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="83942-114">tootest hello kroków w tym samouczku, zaleca się przy użyciu środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="83942-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="83942-115">tootest hello kroki opisane w tym samouczku, należy stosować te zalecenia:</span><span class="sxs-lookup"><span data-stu-id="83942-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="83942-116">Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="83942-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="83942-117">Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz pobrać miesięczna wersja próbna [tutaj](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="83942-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="83942-118">Opis scenariusza</span><span class="sxs-lookup"><span data-stu-id="83942-118">Scenario description</span></span>
<span data-ttu-id="83942-119">W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym.</span><span class="sxs-lookup"><span data-stu-id="83942-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="83942-120">Scenariusz Hello opisane w tym samouczku składa się z dwóch głównych elementów:</span><span class="sxs-lookup"><span data-stu-id="83942-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="83942-121">Dodawanie LiquidFiles z galerii hello</span><span class="sxs-lookup"><span data-stu-id="83942-121">Adding LiquidFiles from hello gallery</span></span>
2. <span data-ttu-id="83942-122">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="83942-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-liquidfiles-from-hello-gallery"></a><span data-ttu-id="83942-123">Dodawanie LiquidFiles z galerii hello</span><span class="sxs-lookup"><span data-stu-id="83942-123">Adding LiquidFiles from hello gallery</span></span>
<span data-ttu-id="83942-124">tooconfigure hello integracji LiquidFiles do usługi Azure AD, należy tooadd LiquidFiles z hello galerii tooyour listę zarządzanych aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="83942-124">tooconfigure hello integration of LiquidFiles into Azure AD, you need tooadd LiquidFiles from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="83942-125">**tooadd LiquidFiles z galerii hello, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="83942-125">**tooadd LiquidFiles from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="83942-126">W hello  **[portalu Azure](https://portal.azure.com)**na temat hello panelu nawigacji po lewej stronie, kliknij przycisk **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="83942-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Usługa Active Directory][1]

2. <span data-ttu-id="83942-128">Przejdź za**aplikacje dla przedsiębiorstw**.</span><span class="sxs-lookup"><span data-stu-id="83942-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="83942-129">Następnie przejdź zbyt**wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="83942-129">Then go too**All applications**.</span></span>

    ![Aplikacje][2]
    
3. <span data-ttu-id="83942-131">tooadd nową aplikację, kliknij przycisk **nowej aplikacji** przycisk u góry hello okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="83942-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplikacje][3]

4. <span data-ttu-id="83942-133">W polu wyszukiwania hello wpisz **LiquidFiles**.</span><span class="sxs-lookup"><span data-stu-id="83942-133">In hello search box, type **LiquidFiles**.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-liquidfiles-tutorial/tutorial_liquidfiles_search.png)

5. <span data-ttu-id="83942-135">W panelu wyników hello zaznacz **LiquidFiles**, a następnie kliknij przycisk **Dodaj** przycisk aplikacji hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="83942-135">In hello results panel, select **LiquidFiles**, and then click **Add** button tooadd hello application.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-liquidfiles-tutorial/tutorial_liquidfiles_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="83942-137">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="83942-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="83942-138">W tej sekcji skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z LiquidFiles w oparciu o nazwie "Britta Simona" użytkownika testowego.</span><span class="sxs-lookup"><span data-stu-id="83942-138">In this section, you configure and test Azure AD single sign-on with LiquidFiles based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="83942-139">Dla pojedynczego logowania jednokrotnego toowork usługi Azure AD musi tooknow użytkownika odpowiednikiem hello w LiquidFiles jest tooa użytkownika w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="83942-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in LiquidFiles is tooa user in Azure AD.</span></span> <span data-ttu-id="83942-140">Innymi słowy relację łącza między użytkownika usługi Azure AD i hello użytkownikowi w LiquidFiles musi toobe ustanowione.</span><span class="sxs-lookup"><span data-stu-id="83942-140">In other words, a link relationship between an Azure AD user and hello related user in LiquidFiles needs toobe established.</span></span>

<span data-ttu-id="83942-141">W LiquidFiles, należy przypisać wartość hello hello **nazwy użytkownika** w usłudze Azure AD jako wartość hello hello **Username** tooestablish hello łącze relacji.</span><span class="sxs-lookup"><span data-stu-id="83942-141">In LiquidFiles, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="83942-142">tooconfigure i testowych usługi Azure AD rejestracji jednokrotnej z LiquidFiles, należy po bloków konstrukcyjnych hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="83942-142">tooconfigure and test Azure AD single sign-on with LiquidFiles, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="83942-143">**[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configuring-azure-ad-single-sign-on)**  -tooenable Twojego toouse użytkowników tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="83942-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="83942-144">**[Tworzenie użytkownika testowego usługi Azure AD](#creating-an-azure-ad-test-user)**  -tootest usługi Azure AD rejestracji jednokrotnej z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="83942-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="83942-145">**[Tworzenie użytkownika testowego LiquidFiles](#creating-a-liquidfiles-test-user)**  -toohave odpowiednikiem Simona Britta w LiquidFiles, który jest połączony toohello usługi Azure AD reprezentację użytkownika.</span><span class="sxs-lookup"><span data-stu-id="83942-145">**[Creating a LiquidFiles test user](#creating-a-liquidfiles-test-user)** - toohave a counterpart of Britta Simon in LiquidFiles that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="83942-146">**[Przypisanie użytkownika testowego hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Simona Britta toouse usługi Azure AD rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="83942-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="83942-147">**[Testowanie rejestracji jednokrotnej](#testing-single-sign-on)**  -tooverify czy hello konfiguracji działania.</span><span class="sxs-lookup"><span data-stu-id="83942-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="83942-148">Konfigurowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="83942-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="83942-149">W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w portalu Azure hello i skonfigurować logowanie jednokrotne w aplikacji LiquidFiles.</span><span class="sxs-lookup"><span data-stu-id="83942-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your LiquidFiles application.</span></span>

<span data-ttu-id="83942-150">**tooconfigure usługi Azure AD rejestracji jednokrotnej z LiquidFiles, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="83942-150">**tooconfigure Azure AD single sign-on with LiquidFiles, perform hello following steps:**</span></span>

1. <span data-ttu-id="83942-151">W portalu Azure na powitania hello **LiquidFiles** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.</span><span class="sxs-lookup"><span data-stu-id="83942-151">In hello Azure portal, on hello **LiquidFiles** application integration page, click **Single sign-on**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej][4]

2. <span data-ttu-id="83942-153">Na powitania **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** tooenable rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="83942-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-liquidfiles-tutorial/tutorial_liquidfiles_samlbase.png)

3. <span data-ttu-id="83942-155">Na powitania **LiquidFiles domeny i adres URL** sekcji, wykonaj następujące kroki hello:</span><span class="sxs-lookup"><span data-stu-id="83942-155">On hello **LiquidFiles Domain and URLs** section, perform hello following steps:</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-liquidfiles-tutorial/tutorial_liquidfiles_url.png)

    <span data-ttu-id="83942-157">a.</span><span class="sxs-lookup"><span data-stu-id="83942-157">a.</span></span> <span data-ttu-id="83942-158">W hello **adres URL logowania** tekstowym, wpisz adres URL za pomocą hello następującego wzorca:`https://<YOUR_SERVER_URL>/saml/init`</span><span class="sxs-lookup"><span data-stu-id="83942-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<YOUR_SERVER_URL>/saml/init`</span></span>

    <span data-ttu-id="83942-159">b.</span><span class="sxs-lookup"><span data-stu-id="83942-159">b.</span></span> <span data-ttu-id="83942-160">W hello **identyfikator** tekstowym, wpisz adres URL za pomocą hello następującego wzorca:`https://<YOUR_SERVER_URL>`</span><span class="sxs-lookup"><span data-stu-id="83942-160">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<YOUR_SERVER_URL>`</span></span>

    <span data-ttu-id="83942-161">c.</span><span class="sxs-lookup"><span data-stu-id="83942-161">c.</span></span> <span data-ttu-id="83942-162">b.</span><span class="sxs-lookup"><span data-stu-id="83942-162">b.</span></span> <span data-ttu-id="83942-163">W hello **adres URL odpowiedzi** tekstowym, wpisz adres URL za pomocą hello następującego wzorca:`https://<YOUR_SERVER_URL>/saml/consume`</span><span class="sxs-lookup"><span data-stu-id="83942-163">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://<YOUR_SERVER_URL>/saml/consume`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="83942-164">Wartości te nie są prawdziwe.</span><span class="sxs-lookup"><span data-stu-id="83942-164">These values are not real.</span></span> <span data-ttu-id="83942-165">Aktualizacji są wartości z hello rzeczywisty adres URL logowania, identyfikator i adres URL odpowiedzi.</span><span class="sxs-lookup"><span data-stu-id="83942-165">Update these values with hello actual Sign-On URL, Identifier and, Reply URL.</span></span> <span data-ttu-id="83942-166">Skontaktuj się z [zespołem pomocy technicznej klienta LiquidFiles](https://www.liquidfiles.com/support.html) tooget tych wartości.</span><span class="sxs-lookup"><span data-stu-id="83942-166">Contact [LiquidFiles Client support team](https://www.liquidfiles.com/support.html) tooget these values.</span></span> 
 
4. <span data-ttu-id="83942-167">Na powitania **certyfikat podpisywania SAML** hello kopiowania, sekcji **odcisk PALCA** wartości certyfikatu.</span><span class="sxs-lookup"><span data-stu-id="83942-167">On hello **SAML Signing Certificate** section, copy hello **THUMBPRINT** value of certificate.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-liquidfiles-tutorial/tutorial_liquidfiles_certificate.png) 

5. <span data-ttu-id="83942-169">Kliknij przycisk **zapisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="83942-169">Click **Save** button.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-liquidfiles-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="83942-171">Na powitania **konfiguracji LiquidFiles** kliknij **skonfigurować LiquidFiles** tooopen **Konfigurowanie logowania jednokrotnego** okna.</span><span class="sxs-lookup"><span data-stu-id="83942-171">On hello **LiquidFiles Configuration** section, click **Configure LiquidFiles** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="83942-172">Witaj kopii **Sign-Out adresu URL i SAML pojedynczy znak na adres URL usługi** z hello **sekcji krótkimi opisami.**</span><span class="sxs-lookup"><span data-stu-id="83942-172">Copy hello **Sign-Out URL, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-liquidfiles-tutorial/tutorial_liquidfiles_configure.png)
 
7. <span data-ttu-id="83942-174">Logowania jednokrotnego tooyour LiquidFiles witryna firmy jako administrator.</span><span class="sxs-lookup"><span data-stu-id="83942-174">Sign-on tooyour LiquidFiles company site as administrator.</span></span>

8. <span data-ttu-id="83942-175">Kliknij przycisk **rejestracji jednokrotnej** w hello **Administracja > konfiguracji** hello menu.</span><span class="sxs-lookup"><span data-stu-id="83942-175">Click **Single Sign-On** in hello **Admin > Configuration** from hello menu.</span></span>

9. <span data-ttu-id="83942-176">Na powitania **konfiguracji rejestracji jednokrotnej** wykonaj następujące kroki hello</span><span class="sxs-lookup"><span data-stu-id="83942-176">On hello **Single Sign-On Configuration** page, perform hello following steps</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-liquidfiles-tutorial/tutorial_single_01.png)

    <span data-ttu-id="83942-178">a.</span><span class="sxs-lookup"><span data-stu-id="83942-178">a.</span></span> <span data-ttu-id="83942-179">Jako **pojedynczy znak na metodę**, wybierz pozycję **SAML 2**.</span><span class="sxs-lookup"><span data-stu-id="83942-179">As **Single Sign On Method**, select **SAML 2**.</span></span>

    <span data-ttu-id="83942-180">b.</span><span class="sxs-lookup"><span data-stu-id="83942-180">b.</span></span> <span data-ttu-id="83942-181">W hello **adres URL logowania IDP** pole tekstowe, Wklej wartość hello **SAML pojedynczy znak na adres URL usługi**, które zostały skopiowane z portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="83942-181">In hello **IDP Login URL** textbox, paste hello value of **SAML Single Sign-On Service URL**, which you have copied from Azure portal.</span></span>

    <span data-ttu-id="83942-182">c.</span><span class="sxs-lookup"><span data-stu-id="83942-182">c.</span></span> <span data-ttu-id="83942-183">W hello **adresu URL wylogowania IDP** pole tekstowe, Wklej hello wartość **Sign-Out URL**, które zostały skopiowane z portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="83942-183">In hello **IDP Logout URL** textbox, paste hello value of **Sign-Out URL**, which you have copied from Azure portal.</span></span>

    <span data-ttu-id="83942-184">d.</span><span class="sxs-lookup"><span data-stu-id="83942-184">d.</span></span> <span data-ttu-id="83942-185">W hello **odcisk palca certyfikatu IDP** pole tekstowe, Wklej hello **odcisk PALCA** wartość, która została skopiowana z portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="83942-185">In hello **IDP Cert Fingerprint** textbox, paste hello **THUMBPRINT** value which you have copied from Azure portal..</span></span>

    <span data-ttu-id="83942-186">e.</span><span class="sxs-lookup"><span data-stu-id="83942-186">e.</span></span> <span data-ttu-id="83942-187">W polu tekstowym Format identyfikatora nazwy hello, wpisz wartość hello **urn: oasis: nazwy: tc: SAML:1.1:nameid-format: emailAddress**.</span><span class="sxs-lookup"><span data-stu-id="83942-187">In hello Name Identifier Format textbox, type hello value **urn:oasis:names:tc:SAML:1.1:nameid-format:emailAddress**.</span></span>

    <span data-ttu-id="83942-188">f.</span><span class="sxs-lookup"><span data-stu-id="83942-188">f.</span></span> <span data-ttu-id="83942-189">W hello textbox kontekstu uwierzytelniania, wpisz wartość hello **urn: oasis: nazwy: tc: SAML:2.0:ac:classes:PasswordProtectedTransport**.</span><span class="sxs-lookup"><span data-stu-id="83942-189">In hello Authn Context textbox, type hello value **urn:oasis:names:tc:SAML:2.0:ac:classes:PasswordProtectedTransport**.</span></span>

    <span data-ttu-id="83942-190">g.</span><span class="sxs-lookup"><span data-stu-id="83942-190">g.</span></span> <span data-ttu-id="83942-191">Kliknij pozycję **Zapisz**.</span><span class="sxs-lookup"><span data-stu-id="83942-191">Click **Save**.</span></span>  

> [!TIP]
> <span data-ttu-id="83942-192">Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz hello [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji hello!</span><span class="sxs-lookup"><span data-stu-id="83942-192">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="83942-193">Po dodaniu tej aplikacji z hello **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij hello **rejestracji jednokrotnej** hello kartę i dostępu do osadzonych dokumentacji za pośrednictwem hello  **Konfiguracja** sekcji u dołu hello.</span><span class="sxs-lookup"><span data-stu-id="83942-193">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="83942-194">Więcej o hello osadzonych dokumentacji funkcji w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="83942-194">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="83942-195">Tworzenie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="83942-195">Creating an Azure AD test user</span></span>
<span data-ttu-id="83942-196">Celem Hello w tej sekcji jest toocreate użytkownika testowego, w portalu Azure o nazwie Simona Britta hello.</span><span class="sxs-lookup"><span data-stu-id="83942-196">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Tworzenie użytkowników usługi Azure AD][100]

<span data-ttu-id="83942-198">**toocreate użytkownika testowego w usłudze Azure AD, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="83942-198">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="83942-199">W hello **portalu Azure**na temat hello w lewym okienku nawigacji, kliknij przycisk **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="83942-199">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-liquidfiles-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="83942-201">toodisplay hello listę użytkowników, przejdź zbyt**użytkowników i grup** i kliknij przycisk **wszyscy użytkownicy**.</span><span class="sxs-lookup"><span data-stu-id="83942-201">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-liquidfiles-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="83942-203">Witaj tooopen **użytkownika** okna dialogowego, kliknij przycisk **Dodaj** u góry hello hello okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="83942-203">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-liquidfiles-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="83942-205">Na powitania **użytkownika** okna dialogowego wykonaj hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="83942-205">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-liquidfiles-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="83942-207">a.</span><span class="sxs-lookup"><span data-stu-id="83942-207">a.</span></span> <span data-ttu-id="83942-208">W hello **nazwa** pole tekstowe, typ **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="83942-208">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="83942-209">b.</span><span class="sxs-lookup"><span data-stu-id="83942-209">b.</span></span> <span data-ttu-id="83942-210">W hello **nazwy użytkownika** pole tekstowe, hello typu **adres e-mail** z BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="83942-210">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="83942-211">c.</span><span class="sxs-lookup"><span data-stu-id="83942-211">c.</span></span> <span data-ttu-id="83942-212">Wybierz **Pokaż hasło** i zanotuj wartość hello hello **hasło**.</span><span class="sxs-lookup"><span data-stu-id="83942-212">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="83942-213">d.</span><span class="sxs-lookup"><span data-stu-id="83942-213">d.</span></span> <span data-ttu-id="83942-214">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="83942-214">Click **Create**.</span></span>
 
### <a name="creating-a-liquidfiles-test-user"></a><span data-ttu-id="83942-215">Tworzenie użytkownika testowego LiquidFiles</span><span class="sxs-lookup"><span data-stu-id="83942-215">Creating a LiquidFiles test user</span></span>

<span data-ttu-id="83942-216">Celem Hello w tej sekcji jest toocreate użytkownika o nazwie Simona Britta w LiquidFiles.</span><span class="sxs-lookup"><span data-stu-id="83942-216">hello objective of this section is toocreate a user called Britta Simon in LiquidFiles.</span></span> <span data-ttu-id="83942-217">Współpraca z Twojej tooget administratora serwera LiquidFiles samodzielnie dodany jako użytkownik przed zalogowaniem się tooyour LiquidFiles aplikacji.</span><span class="sxs-lookup"><span data-stu-id="83942-217">Work with your LiquidFiles server administrator tooget yourself added as a user before logging in tooyour LiquidFiles application.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="83942-218">Przypisanie użytkownika testowego hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="83942-218">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="83942-219">W tej sekcji możesz włączyć toouse Simona Britta Azure logowania jednokrotnego za udzielanie dostępu tooLiquidFiles.</span><span class="sxs-lookup"><span data-stu-id="83942-219">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooLiquidFiles.</span></span>

![Przypisz użytkownika][200] 

<span data-ttu-id="83942-221">**tooassign tooLiquidFiles Simona Britta wykonaj hello następujące kroki:**</span><span class="sxs-lookup"><span data-stu-id="83942-221">**tooassign Britta Simon tooLiquidFiles, perform hello following steps:**</span></span>

1. <span data-ttu-id="83942-222">W portalu Azure hello, otwórz widok aplikacji hello, a następnie przejdź do widoku katalogu toohello i przejść za**aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="83942-222">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Przypisz użytkownika][201] 

2. <span data-ttu-id="83942-224">Z listy aplikacji hello wybierz **LiquidFiles**.</span><span class="sxs-lookup"><span data-stu-id="83942-224">In hello applications list, select **LiquidFiles**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-liquidfiles-tutorial/tutorial_liquidfiles_app.png) 

3. <span data-ttu-id="83942-226">W menu powitania po lewej stronie powitania kliknij **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="83942-226">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Przypisz użytkownika][202] 

4. <span data-ttu-id="83942-228">Kliknij przycisk **Dodaj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="83942-228">Click **Add** button.</span></span> <span data-ttu-id="83942-229">Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="83942-229">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Przypisz użytkownika][203]

5. <span data-ttu-id="83942-231">Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** hello listy użytkowników.</span><span class="sxs-lookup"><span data-stu-id="83942-231">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="83942-232">Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="83942-232">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="83942-233">Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="83942-233">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="83942-234">Testowanie rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="83942-234">Testing single sign-on</span></span>

<span data-ttu-id="83942-235">Celem Hello w tej sekcji jest tootest użyciu usługi Azure AD konfiguracji rejestracji jednokrotnej hello panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="83942-235">hello objective of this section is tootest your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="83942-236">Po kliknięciu powitalne LiquidFiles kafelka w hello Panel dostępu, należy pobrać automatycznie zalogowane tooyour LiquidFiles aplikacji.</span><span class="sxs-lookup"><span data-stu-id="83942-236">When you click hello LiquidFiles tile in hello Access Panel, you should get automatically signed-on tooyour LiquidFiles application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="83942-237">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="83942-237">Additional resources</span></span>

* [<span data-ttu-id="83942-238">Lista samouczków dotyczących tooIntegrate aplikacji SaaS w usłudze Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="83942-238">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="83942-239">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="83942-239">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-liquidfiles-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-liquidfiles-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-liquidfiles-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-liquidfiles-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-liquidfiles-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-liquidfiles-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-liquidfiles-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-liquidfiles-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-liquidfiles-tutorial/tutorial_general_203.png

