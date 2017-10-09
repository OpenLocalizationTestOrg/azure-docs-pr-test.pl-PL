---
title: 'Samouczek: Integracji Azure Active Directory z PagerDuty | Dokumentacja firmy Microsoft'
description: "Dowiedz się, jak tooconfigure logowanie jednokrotne między usługą Azure Active Directory i PagerDuty."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 0410456a-76f7-42a7-9bb5-f767de75a0e0
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/19/2017
ms.author: jeedes
ms.openlocfilehash: c3cfbedac3bf075e2d8cd833d5de7ca0bc9468b6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-pagerduty"></a><span data-ttu-id="87dc2-103">Samouczek: Integracji Azure Active Directory z PagerDuty</span><span class="sxs-lookup"><span data-stu-id="87dc2-103">Tutorial: Azure Active Directory integration with PagerDuty</span></span>

<span data-ttu-id="87dc2-104">Z tego samouczka, dowiesz się, jak toointegrate PagerDuty w usłudze Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="87dc2-104">In this tutorial, you learn how toointegrate PagerDuty with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="87dc2-105">Integracja z usługą Azure AD PagerDuty zapewnia hello następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="87dc2-105">Integrating PagerDuty with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="87dc2-106">Można kontrolować w usłudze Azure AD, kto ma dostęp do tooPagerDuty</span><span class="sxs-lookup"><span data-stu-id="87dc2-106">You can control in Azure AD who has access tooPagerDuty</span></span>
- <span data-ttu-id="87dc2-107">Można włączyć użytkownika użytkownicy tooautomatically get zalogowane tooPagerDuty (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="87dc2-107">You can enable your users tooautomatically get signed-on tooPagerDuty (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="87dc2-108">Możesz zarządzać kont w jednej centralnej lokalizacji - hello portalu Azure</span><span class="sxs-lookup"><span data-stu-id="87dc2-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="87dc2-109">Jeśli chcesz tooknow więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="87dc2-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="87dc2-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="87dc2-110">Prerequisites</span></span>

<span data-ttu-id="87dc2-111">tooconfigure integracji z usługą Azure AD z PagerDuty należy hello następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="87dc2-111">tooconfigure Azure AD integration with PagerDuty, you need hello following items:</span></span>

- <span data-ttu-id="87dc2-112">Subskrypcję usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="87dc2-112">An Azure AD subscription</span></span>
- <span data-ttu-id="87dc2-113">PagerDuty logowanie jednokrotne włączone subskrypcji</span><span class="sxs-lookup"><span data-stu-id="87dc2-113">A PagerDuty single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="87dc2-114">tootest hello kroków w tym samouczku, zaleca się przy użyciu środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="87dc2-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="87dc2-115">tootest hello kroki opisane w tym samouczku, należy stosować te zalecenia:</span><span class="sxs-lookup"><span data-stu-id="87dc2-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="87dc2-116">Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="87dc2-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="87dc2-117">Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz [uzyskać miesięczna wersja próbna](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="87dc2-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="87dc2-118">Opis scenariusza</span><span class="sxs-lookup"><span data-stu-id="87dc2-118">Scenario description</span></span>
<span data-ttu-id="87dc2-119">W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym.</span><span class="sxs-lookup"><span data-stu-id="87dc2-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="87dc2-120">Scenariusz Hello opisane w tym samouczku składa się z dwóch głównych elementów:</span><span class="sxs-lookup"><span data-stu-id="87dc2-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="87dc2-121">Dodawanie PagerDuty z galerii hello</span><span class="sxs-lookup"><span data-stu-id="87dc2-121">Adding PagerDuty from hello gallery</span></span>
2. <span data-ttu-id="87dc2-122">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="87dc2-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-pagerduty-from-hello-gallery"></a><span data-ttu-id="87dc2-123">Dodawanie PagerDuty z galerii hello</span><span class="sxs-lookup"><span data-stu-id="87dc2-123">Adding PagerDuty from hello gallery</span></span>
<span data-ttu-id="87dc2-124">tooconfigure hello integracji PagerDuty do usługi Azure AD, należy tooadd PagerDuty z hello galerii tooyour listę zarządzanych aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="87dc2-124">tooconfigure hello integration of PagerDuty into Azure AD, you need tooadd PagerDuty from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="87dc2-125">**tooadd PagerDuty z galerii hello, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="87dc2-125">**tooadd PagerDuty from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="87dc2-126">W hello  **[portalu Azure](https://portal.azure.com)**na temat hello panelu nawigacji po lewej stronie, kliknij przycisk **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="87dc2-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![przycisk usługi Azure Active Directory Hello][1]

2. <span data-ttu-id="87dc2-128">Przejdź za**aplikacje dla przedsiębiorstw**.</span><span class="sxs-lookup"><span data-stu-id="87dc2-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="87dc2-129">Następnie przejdź zbyt**wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="87dc2-129">Then go too**All applications**.</span></span>

    ![Blok aplikacje przedsiębiorstwa Hello][2]
    
3. <span data-ttu-id="87dc2-131">tooadd nową aplikację, kliknij przycisk **nowej aplikacji** przycisk u góry hello okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="87dc2-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Nowy przycisk aplikacji Hello][3]

4. <span data-ttu-id="87dc2-133">W polu wyszukiwania hello wpisz **PagerDuty**, wybierz pozycję **PagerDuty** z panelu wyników następnie kliknij przycisk **Dodaj** przycisk aplikacji hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="87dc2-133">In hello search box, type **PagerDuty**, select  **PagerDuty**  from result panel then click **Add** button tooadd hello application.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-pagerduty-tutorial/tutorial_pagerduty_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="87dc2-135">Konfiguracja i testowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="87dc2-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="87dc2-136">W tej sekcji skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z PagerDuty w oparciu o nazwie "Britta Simona" użytkownika testowego.</span><span class="sxs-lookup"><span data-stu-id="87dc2-136">In this section, you configure and test Azure AD single sign-on with PagerDuty based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="87dc2-137">Dla pojedynczego logowania jednokrotnego toowork usługi Azure AD musi tooknow użytkownika odpowiednikiem hello w PagerDuty jest tooa użytkownika w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="87dc2-137">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in PagerDuty is tooa user in Azure AD.</span></span> <span data-ttu-id="87dc2-138">Innymi słowy relację łącza między użytkownika usługi Azure AD i hello użytkownikowi w PagerDuty musi toobe ustanowione.</span><span class="sxs-lookup"><span data-stu-id="87dc2-138">In other words, a link relationship between an Azure AD user and hello related user in PagerDuty needs toobe established.</span></span>

<span data-ttu-id="87dc2-139">W PagerDuty, należy przypisać wartość hello hello **nazwy użytkownika** w usłudze Azure AD jako wartość hello hello **Username** tooestablish hello łącze relacji.</span><span class="sxs-lookup"><span data-stu-id="87dc2-139">In PagerDuty, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="87dc2-140">tooconfigure i testowych usługi Azure AD rejestracji jednokrotnej z PagerDuty, należy po bloków konstrukcyjnych hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="87dc2-140">tooconfigure and test Azure AD single sign-on with PagerDuty, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="87dc2-141">**[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configure-azure-ad-single-sign-on)**  -tooenable Twojego toouse użytkowników tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="87dc2-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="87dc2-142">**[Tworzenie użytkownika testowego usługi Azure AD](#create-an-azure-ad-test-user)**  -tootest usługi Azure AD rejestracji jednokrotnej z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="87dc2-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="87dc2-143">**[Tworzenie użytkownika testowego PagerDuty](#create-a-pagerduty-test-user)**  -toohave odpowiednikiem Simona Britta w PagerDuty, który jest połączony toohello usługi Azure AD reprezentację użytkownika.</span><span class="sxs-lookup"><span data-stu-id="87dc2-143">**[Create a PagerDuty test user](#create-a-pagerduty-test-user)** - toohave a counterpart of Britta Simon in PagerDuty that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="87dc2-144">**[Przypisz użytkownika testowego hello Azure AD](#assign-the-azure-ad-test-user)**  -tooenable Simona Britta toouse usługi Azure AD rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="87dc2-144">**[Assign hello Azure AD test user](#assign-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="87dc2-145">**[Test rejestracji jednokrotnej](#test-single-sign-on)**  -tooverify czy hello konfiguracji działania.</span><span class="sxs-lookup"><span data-stu-id="87dc2-145">**[Test Single Sign-On](#test-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="87dc2-146">Konfigurowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="87dc2-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="87dc2-147">W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w portalu Azure hello i skonfigurować logowanie jednokrotne w aplikacji PagerDuty.</span><span class="sxs-lookup"><span data-stu-id="87dc2-147">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your PagerDuty application.</span></span>

<span data-ttu-id="87dc2-148">**tooconfigure usługi Azure AD rejestracji jednokrotnej z PagerDuty, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="87dc2-148">**tooconfigure Azure AD single sign-on with PagerDuty, perform hello following steps:**</span></span>

1. <span data-ttu-id="87dc2-149">W portalu Azure na powitania hello **PagerDuty** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.</span><span class="sxs-lookup"><span data-stu-id="87dc2-149">In hello Azure portal, on hello **PagerDuty** application integration page, click **Single sign-on**.</span></span>

    ![Skonfigurować łącze rejestracji jednokrotnej][4]

2. <span data-ttu-id="87dc2-151">Na powitania **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** tooenable rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="87dc2-151">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Okno dialogowe rejestracji jednokrotnej](./media/active-directory-saas-pagerduty-tutorial/tutorial_pagerduty_samlbase.png)

3. <span data-ttu-id="87dc2-153">Na powitania **PagerDuty domeny i adres URL** sekcji, wykonaj następujące kroki hello:</span><span class="sxs-lookup"><span data-stu-id="87dc2-153">On hello **PagerDuty Domain and URLs** section, perform hello following steps:</span></span>

    ![Adresy URL i domeny PagerDuty pojedynczy informacje logowania jednokrotnego](./media/active-directory-saas-pagerduty-tutorial/tutorial_pagerduty_url.png)

    <span data-ttu-id="87dc2-155">a.</span><span class="sxs-lookup"><span data-stu-id="87dc2-155">a.</span></span> <span data-ttu-id="87dc2-156">W hello **adres URL logowania** tekstowym, wpisz adres URL za pomocą hello następującego wzorca:`https://<tenant-name>.pagerduty.com`</span><span class="sxs-lookup"><span data-stu-id="87dc2-156">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<tenant-name>.pagerduty.com`</span></span>

    <span data-ttu-id="87dc2-157">b.</span><span class="sxs-lookup"><span data-stu-id="87dc2-157">b.</span></span> <span data-ttu-id="87dc2-158">W hello **identyfikator** tekstowym, wpisz adres URL za pomocą hello następującego wzorca:`https://<tenant-name>.pagerduty.com`</span><span class="sxs-lookup"><span data-stu-id="87dc2-158">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<tenant-name>.pagerduty.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="87dc2-159">Wartości te nie są prawdziwe.</span><span class="sxs-lookup"><span data-stu-id="87dc2-159">These values are not real.</span></span> <span data-ttu-id="87dc2-160">Zaktualizować te wartości z hello rzeczywisty adres URL logowania i identyfikator.</span><span class="sxs-lookup"><span data-stu-id="87dc2-160">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="87dc2-161">Skontaktuj się z [zespołem pomocy technicznej klienta PagerDuty](https://www.pagerduty.com/support/) tooget tych wartości.</span><span class="sxs-lookup"><span data-stu-id="87dc2-161">Contact [PagerDuty Client support team](https://www.pagerduty.com/support/) tooget these values.</span></span> 

4. <span data-ttu-id="87dc2-162">Na powitania **certyfikat podpisywania SAML** kliknij **Certificate(Base64)** , a następnie zapisz plik certyfikatu hello na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="87dc2-162">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![link do pobierania certyfikatu Hello](./media/active-directory-saas-pagerduty-tutorial/tutorial_pagerduty_certificate.png) 

5. <span data-ttu-id="87dc2-164">Kliknij przycisk **zapisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="87dc2-164">Click **Save** button.</span></span>

    ![Skonfiguruj przycisk pojedynczego logowania jednokrotnego Zapisz](./media/active-directory-saas-pagerduty-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="87dc2-166">Na powitania **konfiguracji PagerDuty** kliknij **skonfigurować PagerDuty** tooopen **Konfigurowanie logowania jednokrotnego** okna.</span><span class="sxs-lookup"><span data-stu-id="87dc2-166">On hello **PagerDuty Configuration** section, click **Configure PagerDuty** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="87dc2-167">Kopiuj hello **Sign-Out adresu URL i SAML pojedynczy znak na adres URL usługi** z hello **sekcji krótkimi opisami.**</span><span class="sxs-lookup"><span data-stu-id="87dc2-167">Copy hello **Sign-Out URL and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Konfiguracja PagerDuty](./media/active-directory-saas-pagerduty-tutorial/tutorial_pagerduty_configure.png) 

7. <span data-ttu-id="87dc2-169">W oknie przeglądarki innej witryny sieci web Zaloguj się do witryny firmy Pagerduty jako administrator.</span><span class="sxs-lookup"><span data-stu-id="87dc2-169">In a different web browser window, log into your Pagerduty company site as an administrator.</span></span>

8. <span data-ttu-id="87dc2-170">W menu hello na górze hello, kliknij przycisk **ustawienia konta**.</span><span class="sxs-lookup"><span data-stu-id="87dc2-170">In hello menu on hello top, click **Account Settings**.</span></span>
   
    <span data-ttu-id="87dc2-171">![Ustawienia konta](./media/active-directory-saas-pagerduty-tutorial/ic778535.png "ustawienia konta")</span><span class="sxs-lookup"><span data-stu-id="87dc2-171">![Account Settings](./media/active-directory-saas-pagerduty-tutorial/ic778535.png "Account Settings")</span></span>

9. <span data-ttu-id="87dc2-172">Kliknij przycisk **logowanie jednokrotne**.</span><span class="sxs-lookup"><span data-stu-id="87dc2-172">Click **Single Sign-on**.</span></span>
   
    <span data-ttu-id="87dc2-173">![Logowanie jednokrotne](./media/active-directory-saas-pagerduty-tutorial/ic778536.png "logowanie jednokrotne")</span><span class="sxs-lookup"><span data-stu-id="87dc2-173">![Single sign-on](./media/active-directory-saas-pagerduty-tutorial/ic778536.png "Single sign-on")</span></span>

10. <span data-ttu-id="87dc2-174">Na powitania **włączyć logowanie jednokrotne (SSO)** wykonaj hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="87dc2-174">On hello **Enable Single Sign-on (SSO)** page, perform hello following steps:</span></span>
   
    <span data-ttu-id="87dc2-175">![Włącz rejestrację jednokrotną](./media/active-directory-saas-pagerduty-tutorial/ic778537.png "Włącz rejestrację jednokrotną")</span><span class="sxs-lookup"><span data-stu-id="87dc2-175">![Enable single sign-on](./media/active-directory-saas-pagerduty-tutorial/ic778537.png "Enable single sign-on")</span></span>
   
    <span data-ttu-id="87dc2-176">a.</span><span class="sxs-lookup"><span data-stu-id="87dc2-176">a.</span></span> <span data-ttu-id="87dc2-177">Otwórz base-64 zakodowany certyfikat pobrany z portalu Azure w programie Notatnik hello kopiowania zawartości go do Schowka, a następnie wklej go toohello **certyfikatu X.509** pole tekstowe</span><span class="sxs-lookup"><span data-stu-id="87dc2-177">Open your base-64 encoded certificate downloaded from Azure portal in notepad, copy hello content of it into your clipboard, and then paste it toohello **X.509 Certificate** textbox</span></span>
  
    <span data-ttu-id="87dc2-178">b.</span><span class="sxs-lookup"><span data-stu-id="87dc2-178">b.</span></span> <span data-ttu-id="87dc2-179">W hello **adres URL logowania** pole tekstowe, Wklej **SAML pojedynczy znak na adres URL usługi** którego została skopiowana z portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="87dc2-179">In hello **Login URL** textbox, paste **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span></span>
  
    <span data-ttu-id="87dc2-180">c.</span><span class="sxs-lookup"><span data-stu-id="87dc2-180">c.</span></span> <span data-ttu-id="87dc2-181">W hello **adresu URL wylogowania** pole tekstowe, Wklej **Sign-Out URL** którego została skopiowana z portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="87dc2-181">In hello **Logout URL** textbox, paste **Sign-Out URL** which you have copied from Azure portal.</span></span>
 
    <span data-ttu-id="87dc2-182">d.</span><span class="sxs-lookup"><span data-stu-id="87dc2-182">d.</span></span> <span data-ttu-id="87dc2-183">Wybierz **włączyć pojedynczego logowania jednokrotnego**.</span><span class="sxs-lookup"><span data-stu-id="87dc2-183">Select **Turn on Single Sign-on**.</span></span>
 
    <span data-ttu-id="87dc2-184">e.</span><span class="sxs-lookup"><span data-stu-id="87dc2-184">e.</span></span> <span data-ttu-id="87dc2-185">Kliknij przycisk **zapisać zmiany**.</span><span class="sxs-lookup"><span data-stu-id="87dc2-185">Click **Save Changes**.</span></span>

> [!TIP]
> <span data-ttu-id="87dc2-186">Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz hello [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji hello!</span><span class="sxs-lookup"><span data-stu-id="87dc2-186">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="87dc2-187">Po dodaniu tej aplikacji z hello **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij hello **rejestracji jednokrotnej** hello kartę i dostępu do osadzonych dokumentacji za pośrednictwem hello  **Konfiguracja** sekcji u dołu hello.</span><span class="sxs-lookup"><span data-stu-id="87dc2-187">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="87dc2-188">Więcej o hello osadzonych dokumentacji funkcji w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="87dc2-188">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="87dc2-189">Tworzenie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="87dc2-189">Create an Azure AD test user</span></span>

<span data-ttu-id="87dc2-190">Celem Hello w tej sekcji jest toocreate użytkownika testowego, w portalu Azure o nazwie Simona Britta hello.</span><span class="sxs-lookup"><span data-stu-id="87dc2-190">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Tworzenie użytkownika testowego usługi Azure AD][100]

<span data-ttu-id="87dc2-192">**toocreate użytkownika testowego w usłudze Azure AD, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="87dc2-192">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="87dc2-193">W hello **portalu Azure**na temat hello w lewym okienku nawigacji, kliknij przycisk **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="87dc2-193">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![przycisk usługi Azure Active Directory Hello](./media/active-directory-saas-pagerduty-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="87dc2-195">toodisplay hello listę użytkowników, przejdź zbyt**użytkowników i grup** i kliknij przycisk **wszyscy użytkownicy**.</span><span class="sxs-lookup"><span data-stu-id="87dc2-195">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Witaj, "Użytkownicy i grupy" i "Wszyscy użytkownicy" łącza](./media/active-directory-saas-pagerduty-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="87dc2-197">Witaj tooopen **użytkownika** okna dialogowego, kliknij przycisk **Dodaj** u góry hello hello okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="87dc2-197">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![przycisk Dodaj Hello](./media/active-directory-saas-pagerduty-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="87dc2-199">Na powitania **użytkownika** okna dialogowego wykonaj hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="87dc2-199">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![okno dialogowe Hello użytkownika](./media/active-directory-saas-pagerduty-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="87dc2-201">a.</span><span class="sxs-lookup"><span data-stu-id="87dc2-201">a.</span></span> <span data-ttu-id="87dc2-202">W hello **nazwa** pole tekstowe, typ **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="87dc2-202">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="87dc2-203">b.</span><span class="sxs-lookup"><span data-stu-id="87dc2-203">b.</span></span> <span data-ttu-id="87dc2-204">W hello **nazwy użytkownika** pole tekstowe, hello typu **adres e-mail** z BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="87dc2-204">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="87dc2-205">c.</span><span class="sxs-lookup"><span data-stu-id="87dc2-205">c.</span></span> <span data-ttu-id="87dc2-206">Wybierz **Pokaż hasło** i zanotuj wartość hello hello **hasło**.</span><span class="sxs-lookup"><span data-stu-id="87dc2-206">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="87dc2-207">d.</span><span class="sxs-lookup"><span data-stu-id="87dc2-207">d.</span></span> <span data-ttu-id="87dc2-208">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="87dc2-208">Click **Create**.</span></span>
 
### <a name="create-a-pagerduty-test-user"></a><span data-ttu-id="87dc2-209">Tworzenie użytkownika testowego PagerDuty</span><span class="sxs-lookup"><span data-stu-id="87dc2-209">Create a PagerDuty test user</span></span>

<span data-ttu-id="87dc2-210">toolog użytkowników tooenable usługi Azure AD w tooPagerDuty, muszą mieć przydzielone do PagerDuty.</span><span class="sxs-lookup"><span data-stu-id="87dc2-210">tooenable Azure AD users toolog in tooPagerDuty, they must be provisioned into PagerDuty.</span></span>  
<span data-ttu-id="87dc2-211">W przypadku hello PagerDuty Inicjowanie obsługi to zadanie ręczne.</span><span class="sxs-lookup"><span data-stu-id="87dc2-211">In hello case of PagerDuty, provisioning is a manual task.</span></span>

>[!NOTE]
><span data-ttu-id="87dc2-212">Możesz użyć innych Pagerduty użytkownika konta tworzenia narzędzi lub interfejsów API dostarczonych przez tooprovision Pagerduty usługi Azure Active Directory kont użytkowników.</span><span class="sxs-lookup"><span data-stu-id="87dc2-212">You can use any other Pagerduty user account creation tools or APIs provided by Pagerduty tooprovision Azure Active Directory user accounts.</span></span>

<span data-ttu-id="87dc2-213">**tooprovision konta użytkownika, należy wykonać hello następujące kroki:**</span><span class="sxs-lookup"><span data-stu-id="87dc2-213">**tooprovision a user account, perform hello following steps:**</span></span>

1. <span data-ttu-id="87dc2-214">Zaloguj się za tooyour **Pagerduty** dzierżawy.</span><span class="sxs-lookup"><span data-stu-id="87dc2-214">Log in tooyour **Pagerduty** tenant.</span></span>

2. <span data-ttu-id="87dc2-215">W menu hello na górze hello, kliknij przycisk **użytkowników**.</span><span class="sxs-lookup"><span data-stu-id="87dc2-215">In hello menu on hello top, click **Users**.</span></span>

3. <span data-ttu-id="87dc2-216">Kliknij przycisk **dodawania użytkowników**.</span><span class="sxs-lookup"><span data-stu-id="87dc2-216">Click **Add Users**.</span></span>
   
    <span data-ttu-id="87dc2-217">![Dodawanie użytkowników](./media/active-directory-saas-pagerduty-tutorial/ic778539.png "Dodawanie użytkowników")</span><span class="sxs-lookup"><span data-stu-id="87dc2-217">![Add Users](./media/active-directory-saas-pagerduty-tutorial/ic778539.png "Add Users")</span></span>

4.  <span data-ttu-id="87dc2-218">Na powitania **zaprosić zespołu** okna dialogowego, wykonaj następujące kroki hello:</span><span class="sxs-lookup"><span data-stu-id="87dc2-218">On hello **Invite your team** dialog, perform hello following steps:</span></span>
   
    <span data-ttu-id="87dc2-219">![Zaproś zespołu](./media/active-directory-saas-pagerduty-tutorial/ic778540.png "zaprosić Twojego zespołu")</span><span class="sxs-lookup"><span data-stu-id="87dc2-219">![Invite your team](./media/active-directory-saas-pagerduty-tutorial/ic778540.png "Invite your team")</span></span>

    <span data-ttu-id="87dc2-220">a.</span><span class="sxs-lookup"><span data-stu-id="87dc2-220">a.</span></span> <span data-ttu-id="87dc2-221">Typ hello **pierwszy i nazwisko** użytkownika, takich jak **Simona Britta**.</span><span class="sxs-lookup"><span data-stu-id="87dc2-221">Type hello **First and Last Name** of user like **Britta Simon**.</span></span> 
   
    <span data-ttu-id="87dc2-222">b.</span><span class="sxs-lookup"><span data-stu-id="87dc2-222">b.</span></span> <span data-ttu-id="87dc2-223">Wprowadź **E-mail** adres użytkownika, takich jak  **brittasimon@contoso.com** .</span><span class="sxs-lookup"><span data-stu-id="87dc2-223">Enter **Email** address of user like **brittasimon@contoso.com**.</span></span>
   
    <span data-ttu-id="87dc2-224">c.</span><span class="sxs-lookup"><span data-stu-id="87dc2-224">c.</span></span> <span data-ttu-id="87dc2-225">Kliknij przycisk **Dodaj**, a następnie kliknij przycisk **wysyłania zaprasza**.</span><span class="sxs-lookup"><span data-stu-id="87dc2-225">Click **Add**, and then click **Send Invites**.</span></span>
   
    >[!NOTE]
    ><span data-ttu-id="87dc2-226">Wszystkie dodano użytkownicy otrzymają zaproszenie toocreate konta PagerDuty.</span><span class="sxs-lookup"><span data-stu-id="87dc2-226">All added users will receive an invite toocreate a PagerDuty account.</span></span>

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="87dc2-227">Przypisz użytkownika testowego hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="87dc2-227">Assign hello Azure AD test user</span></span>

<span data-ttu-id="87dc2-228">W tej sekcji możesz włączyć toouse Simona Britta Azure logowania jednokrotnego za udzielanie dostępu tooPagerDuty.</span><span class="sxs-lookup"><span data-stu-id="87dc2-228">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooPagerDuty.</span></span>

![Przypisanie roli użytkownika hello][200]

<span data-ttu-id="87dc2-230">**tooassign tooPagerDuty Simona Britta wykonaj hello następujące kroki:**</span><span class="sxs-lookup"><span data-stu-id="87dc2-230">**tooassign Britta Simon tooPagerDuty, perform hello following steps:**</span></span>

1. <span data-ttu-id="87dc2-231">W portalu Azure hello, otwórz widok aplikacji hello, a następnie przejdź do widoku katalogu toohello i przejść za**aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="87dc2-231">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Przypisz użytkownika][201] 

2. <span data-ttu-id="87dc2-233">Z listy aplikacji hello wybierz **PagerDuty**.</span><span class="sxs-lookup"><span data-stu-id="87dc2-233">In hello applications list, select **PagerDuty**.</span></span>

    ![łącze PagerDuty Hello na liście aplikacji hello](./media/active-directory-saas-pagerduty-tutorial/tutorial_pagerduty_app.png) 

3. <span data-ttu-id="87dc2-235">W menu powitania po lewej stronie powitania kliknij **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="87dc2-235">In hello menu on hello left, click **Users and groups**.</span></span>

    ![łącze "Użytkownicy i grupy" Hello][202]

4. <span data-ttu-id="87dc2-237">Kliknij przycisk **Dodaj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="87dc2-237">Click **Add** button.</span></span> <span data-ttu-id="87dc2-238">Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="87dc2-238">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Okienko Dodaj przypisania Hello][203]

5. <span data-ttu-id="87dc2-240">Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** hello listy użytkowników.</span><span class="sxs-lookup"><span data-stu-id="87dc2-240">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="87dc2-241">Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="87dc2-241">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="87dc2-242">Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="87dc2-242">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="87dc2-243">Test rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="87dc2-243">Test single sign-on</span></span>

<span data-ttu-id="87dc2-244">W tej sekcji można przetestować konfiguracji usługi Azure AD pojedynczego logowania jednokrotnego przy użyciu hello panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="87dc2-244">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="87dc2-245">Po kliknięciu kafelka PagerDuty hello w hello Panelyou dostępu należy uzyskać automatycznie zalogowane tooyour PagerDuty aplikacji.</span><span class="sxs-lookup"><span data-stu-id="87dc2-245">When you click hello PagerDuty tile in hello Access Panelyou should get automatically signed-on tooyour PagerDuty application.</span></span>

<span data-ttu-id="87dc2-246">Aby uzyskać więcej informacji na temat hello Panel dostępu, zobacz [toohello wprowadzenie panelu dostępu](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="87dc2-246">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="87dc2-247">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="87dc2-247">Additional resources</span></span>

* [<span data-ttu-id="87dc2-248">Lista samouczków dotyczących tooIntegrate aplikacji SaaS w usłudze Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="87dc2-248">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="87dc2-249">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="87dc2-249">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-pagerduty-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-pagerduty-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-pagerduty-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-pagerduty-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-pagerduty-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-pagerduty-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-pagerduty-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-pagerduty-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-pagerduty-tutorial/tutorial_general_203.png

