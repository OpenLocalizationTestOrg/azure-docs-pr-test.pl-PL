---
title: 'Samouczek: Integracji Azure Active Directory z InsideView | Dokumentacja firmy Microsoft'
description: "Dowiedz się, jak tooconfigure logowanie jednokrotne między usługą Azure Active Directory i InsideView."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: c489a7ab-6b1f-4efb-8a66-8bc13bca78c3
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/29/2017
ms.author: jeedes
ms.openlocfilehash: 979c0c24f3a18a193616061b8c2e78292233a56d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-insideview"></a><span data-ttu-id="0a54f-103">Samouczek: Integracji Azure Active Directory z InsideView</span><span class="sxs-lookup"><span data-stu-id="0a54f-103">Tutorial: Azure Active Directory integration with InsideView</span></span>

<span data-ttu-id="0a54f-104">Z tego samouczka, dowiesz się, jak toointegrate InsideView w usłudze Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="0a54f-104">In this tutorial, you learn how toointegrate InsideView with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="0a54f-105">Integracja z usługą Azure AD InsideView zapewnia hello następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="0a54f-105">Integrating InsideView with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="0a54f-106">Można kontrolować w usłudze Azure AD, kto ma dostęp do tooInsideView</span><span class="sxs-lookup"><span data-stu-id="0a54f-106">You can control in Azure AD who has access tooInsideView</span></span>
- <span data-ttu-id="0a54f-107">Można włączyć użytkownika użytkownicy tooautomatically get zalogowane tooInsideView (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="0a54f-107">You can enable your users tooautomatically get signed-on tooInsideView (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="0a54f-108">Możesz zarządzać kont w jednej centralnej lokalizacji - hello portalu Azure</span><span class="sxs-lookup"><span data-stu-id="0a54f-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="0a54f-109">Jeśli chcesz tooknow więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="0a54f-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="0a54f-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="0a54f-110">Prerequisites</span></span>

<span data-ttu-id="0a54f-111">tooconfigure integracji z usługą Azure AD z InsideView należy hello następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="0a54f-111">tooconfigure Azure AD integration with InsideView, you need hello following items:</span></span>

- <span data-ttu-id="0a54f-112">Subskrypcję usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="0a54f-112">An Azure AD subscription</span></span>
- <span data-ttu-id="0a54f-113">InsideView logowanie jednokrotne włączone subskrypcji</span><span class="sxs-lookup"><span data-stu-id="0a54f-113">A InsideView single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="0a54f-114">tootest hello kroków w tym samouczku, zaleca się przy użyciu środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="0a54f-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="0a54f-115">tootest hello kroki opisane w tym samouczku, należy stosować te zalecenia:</span><span class="sxs-lookup"><span data-stu-id="0a54f-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="0a54f-116">Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="0a54f-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="0a54f-117">Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz pobrać miesięczna wersja próbna [tutaj](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="0a54f-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="0a54f-118">Opis scenariusza</span><span class="sxs-lookup"><span data-stu-id="0a54f-118">Scenario description</span></span>
<span data-ttu-id="0a54f-119">W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym.</span><span class="sxs-lookup"><span data-stu-id="0a54f-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="0a54f-120">Scenariusz Hello opisane w tym samouczku składa się z dwóch głównych elementów:</span><span class="sxs-lookup"><span data-stu-id="0a54f-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="0a54f-121">Dodawanie InsideView z galerii hello</span><span class="sxs-lookup"><span data-stu-id="0a54f-121">Adding InsideView from hello gallery</span></span>
2. <span data-ttu-id="0a54f-122">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="0a54f-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-insideview-from-hello-gallery"></a><span data-ttu-id="0a54f-123">Dodawanie InsideView z galerii hello</span><span class="sxs-lookup"><span data-stu-id="0a54f-123">Adding InsideView from hello gallery</span></span>
<span data-ttu-id="0a54f-124">tooconfigure hello integracji InsideView w tooAzure AD, należy tooadd InsideView z hello galerii tooyour listę zarządzanych aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="0a54f-124">tooconfigure hello integration of InsideView in tooAzure AD, you need tooadd InsideView from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="0a54f-125">**tooadd InsideView z galerii hello, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="0a54f-125">**tooadd InsideView from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="0a54f-126">W hello  **[portalu Azure](https://portal.azure.com)**na temat hello panelu nawigacji po lewej stronie, kliknij przycisk **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="0a54f-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Usługa Active Directory][1]

2. <span data-ttu-id="0a54f-128">Przejdź za**aplikacje dla przedsiębiorstw**.</span><span class="sxs-lookup"><span data-stu-id="0a54f-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="0a54f-129">Następnie przejdź zbyt**wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="0a54f-129">Then go too**All applications**.</span></span>

    ![Aplikacje][2]
    
3. <span data-ttu-id="0a54f-131">tooadd nową aplikację, kliknij przycisk **nowej aplikacji** przycisk u góry hello okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="0a54f-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplikacje][3]

4. <span data-ttu-id="0a54f-133">W polu wyszukiwania hello wpisz **InsideView**.</span><span class="sxs-lookup"><span data-stu-id="0a54f-133">In hello search box, type **InsideView**.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-insideview-tutorial/tutorial_insideview_search.png)

5. <span data-ttu-id="0a54f-135">W panelu wyników hello zaznacz **InsideView**, a następnie kliknij przycisk **Dodaj** przycisk aplikacji hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="0a54f-135">In hello results panel, select **InsideView**, and then click **Add** button tooadd hello application.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-insideview-tutorial/tutorial_insideview_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="0a54f-137">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="0a54f-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="0a54f-138">W tej sekcji możesz skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z InsideView na podstawie użytkownika testowego, nazywany "Britta Simona".</span><span class="sxs-lookup"><span data-stu-id="0a54f-138">In this section, you configure and test Azure AD single sign-on with InsideView based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="0a54f-139">Dla pojedynczego logowania jednokrotnego toowork usługi Azure AD musi tooknow użytkownika odpowiednikiem hello w InsideView jest tooa użytkownika w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="0a54f-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in InsideView is tooa user in Azure AD.</span></span> <span data-ttu-id="0a54f-140">Innymi słowy relację łącza między użytkownika usługi Azure AD i hello użytkownikowi w InsideView musi toobe ustanowione.</span><span class="sxs-lookup"><span data-stu-id="0a54f-140">In other words, a link relationship between an Azure AD user and hello related user in InsideView needs toobe established.</span></span>

<span data-ttu-id="0a54f-141">W InsideView, należy przypisać wartość hello hello **nazwy użytkownika** w usłudze Azure AD jako wartość hello hello **Username** tooestablish hello łącze relacji.</span><span class="sxs-lookup"><span data-stu-id="0a54f-141">In InsideView, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="0a54f-142">tooconfigure i testowych usługi Azure AD rejestracji jednokrotnej z InsideView, należy po bloków konstrukcyjnych hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="0a54f-142">tooconfigure and test Azure AD single sign-on with InsideView, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="0a54f-143">**[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configuring-azure-ad-single-sign-on)**  -tooenable Twojego toouse użytkowników tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="0a54f-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="0a54f-144">**[Tworzenie użytkownika testowego usługi Azure AD](#creating-an-azure-ad-test-user)**  -tootest usługi Azure AD rejestracji jednokrotnej z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="0a54f-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="0a54f-145">**[Tworzenie użytkownika testowego InsideView](#creating-a-insideview-test-user)**  -toohave odpowiednikiem Simona Britta w InsideView, który jest połączony toohello usługi Azure AD reprezentację użytkownika.</span><span class="sxs-lookup"><span data-stu-id="0a54f-145">**[Creating a InsideView test user](#creating-a-insideview-test-user)** - toohave a counterpart of Britta Simon in InsideView that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="0a54f-146">**[Przypisanie użytkownika testowego hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Simona Britta toouse usługi Azure AD rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="0a54f-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="0a54f-147">**[Testowanie rejestracji jednokrotnej](#testing-single-sign-on)**  -tooverify czy hello konfiguracji działania.</span><span class="sxs-lookup"><span data-stu-id="0a54f-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="0a54f-148">Konfigurowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="0a54f-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="0a54f-149">W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w portalu Azure hello i skonfigurować logowanie jednokrotne w aplikacji InsideView.</span><span class="sxs-lookup"><span data-stu-id="0a54f-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your InsideView application.</span></span>

<span data-ttu-id="0a54f-150">**tooconfigure usługi Azure AD rejestracji jednokrotnej z InsideView, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="0a54f-150">**tooconfigure Azure AD single sign-on with InsideView, perform hello following steps:**</span></span>

1. <span data-ttu-id="0a54f-151">W portalu Azure na powitania hello **InsideView** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.</span><span class="sxs-lookup"><span data-stu-id="0a54f-151">In hello Azure portal, on hello **InsideView** application integration page, click **Single sign-on**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej][4]

2. <span data-ttu-id="0a54f-153">Na powitania **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** tooenable rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="0a54f-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-insideview-tutorial/tutorial_insideview_samlbase.png)

3. <span data-ttu-id="0a54f-155">Na powitania **InsideView domeny i adres URL** sekcji, wykonaj następujące kroki hello:</span><span class="sxs-lookup"><span data-stu-id="0a54f-155">On hello **InsideView Domain and URLs** section, perform hello following steps:</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-insideview-tutorial/tutorial_insideview_url.png)
    
    <span data-ttu-id="0a54f-157">W hello **adres URL odpowiedzi** tekstowym, wpisz adres URL za pomocą hello następującego wzorca:`https://my.insideview.com/iv/<STS Name>/login.iv`</span><span class="sxs-lookup"><span data-stu-id="0a54f-157">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://my.insideview.com/iv/<STS Name>/login.iv`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="0a54f-158">Ta wartość nie jest prawdziwe.</span><span class="sxs-lookup"><span data-stu-id="0a54f-158">This value is not real.</span></span> <span data-ttu-id="0a54f-159">Zaktualizuj tę wartość przy hello rzeczywisty adres URL odpowiedzi służący.</span><span class="sxs-lookup"><span data-stu-id="0a54f-159">Update this value with hello actual Reply URL.</span></span> <span data-ttu-id="0a54f-160">Skontaktuj się z [zespołem pomocy technicznej InsideView ](mailto:support@insideview.com) tooget tej wartości.</span><span class="sxs-lookup"><span data-stu-id="0a54f-160">Contact [InsideView support team ](mailto:support@insideview.com) tooget this value.</span></span>
 
4. <span data-ttu-id="0a54f-161">Na powitania **certyfikat podpisywania SAML** kliknij **certyfikatu (Raw)** , a następnie zapisz plik certyfikatu hello na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="0a54f-161">On hello **SAML Signing Certificate** section, click **Certificate (Raw)** and then save hello certificate file on your computer.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-insideview-tutorial/tutorial_insideview_certificate.png) 

5. <span data-ttu-id="0a54f-163">Kliknij przycisk **zapisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="0a54f-163">Click **Save** button.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-insideview-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="0a54f-165">Na powitania **konfiguracji InsideView** kliknij **skonfigurować InsideView** tooopen **Konfigurowanie logowania jednokrotnego** okna.</span><span class="sxs-lookup"><span data-stu-id="0a54f-165">On hello **InsideView Configuration** section, click **Configure InsideView** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="0a54f-166">Kopiuj hello **SAML pojedynczy znak na adres URL usługi** z hello **sekcji krótkimi opisami.**</span><span class="sxs-lookup"><span data-stu-id="0a54f-166">Copy hello **SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-insideview-tutorial/tutorial_insideview_configure.png) 

7. <span data-ttu-id="0a54f-168">W oknie przeglądarki innej witryny sieci web Zaloguj się w witrynie firmy InsideView tooyour jako administrator.</span><span class="sxs-lookup"><span data-stu-id="0a54f-168">In a different web browser window, log in tooyour InsideView company site as an administrator.</span></span>

8. <span data-ttu-id="0a54f-169">Hello pasku narzędzi u góry hello, kliknij przycisk **Admin**, **ustawienia SingleSignOn**, a następnie kliknij przycisk **dodać SAML**.</span><span class="sxs-lookup"><span data-stu-id="0a54f-169">In hello toolbar on hello top, click **Admin**, **SingleSignOn Settings**, and then click **Add SAML**.</span></span>
   
   <span data-ttu-id="0a54f-170">![SAML logowania jednokrotnego ustawienia](./media/active-directory-saas-insideview-tutorial/ic794135.png "SAML logowania jednokrotnego ustawienia")</span><span class="sxs-lookup"><span data-stu-id="0a54f-170">![SAML Single Sign On Settings](./media/active-directory-saas-insideview-tutorial/ic794135.png "SAML Single Sign On Settings")</span></span>

9. <span data-ttu-id="0a54f-171">W hello **Dodaj nowe SAML** sekcji, wykonaj następujące kroki hello:</span><span class="sxs-lookup"><span data-stu-id="0a54f-171">In hello **Add a New SAML** section, perform hello following steps:</span></span>

    <span data-ttu-id="0a54f-172">![Dodaj nowy SAML](./media/active-directory-saas-insideview-tutorial/ic794136.png "Dodaj nowe SAML")</span><span class="sxs-lookup"><span data-stu-id="0a54f-172">![Add a New SAML](./media/active-directory-saas-insideview-tutorial/ic794136.png "Add a New SAML")</span></span>
   
    <span data-ttu-id="0a54f-173">a.</span><span class="sxs-lookup"><span data-stu-id="0a54f-173">a.</span></span> <span data-ttu-id="0a54f-174">W hello **nazwę STS** tekstowym, wpisz nazwę dla danej konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="0a54f-174">In hello **STS Name** textbox, type a name for your configuration.</span></span>

    <span data-ttu-id="0a54f-175">b.</span><span class="sxs-lookup"><span data-stu-id="0a54f-175">b.</span></span> <span data-ttu-id="0a54f-176">W **SamlP/WS-Fed niechciane punktu końcowego** pole tekstowe, Wklej wartość hello **SAML pojedynczy znak na adres URL usługi**, które zostały skopiowane z portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="0a54f-176">In **SamlP/WS-Fed Unsolicited EndPoint** textbox, paste hello value of **SAML Single Sign-On Service URL**, which you have copied from Azure portal.</span></span>
    
    <span data-ttu-id="0a54f-177">c.</span><span class="sxs-lookup"><span data-stu-id="0a54f-177">c.</span></span> <span data-ttu-id="0a54f-178">Otwieranie certyfikatu zakodowanego base-64, które zostały pobrane z usługi Azure portalu, hello kopiowania zawartości go do Schowka, a następnie wklej go toohello **certyfikat STS** pola tekstowego.</span><span class="sxs-lookup"><span data-stu-id="0a54f-178">Open your base-64 encoded certificate, which you have downloaded from Azure portal, copy hello content of it into your clipboard, and then paste it toohello **STS Certificate** textbox.</span></span>

    <span data-ttu-id="0a54f-179">d.</span><span class="sxs-lookup"><span data-stu-id="0a54f-179">d.</span></span> <span data-ttu-id="0a54f-180">W hello **mapowanie identyfikatora użytkownika Crm** pole tekstowe, typ `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress`.</span><span class="sxs-lookup"><span data-stu-id="0a54f-180">In hello **Crm User Id Mapping** textbox, type `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress`.</span></span>
        
    <span data-ttu-id="0a54f-181">e.</span><span class="sxs-lookup"><span data-stu-id="0a54f-181">e.</span></span> <span data-ttu-id="0a54f-182">W hello **mapowania E-mail Crm** pole tekstowe, typ `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress`.</span><span class="sxs-lookup"><span data-stu-id="0a54f-182">In hello **Crm Email Mapping** textbox, type `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress`.</span></span>

    <span data-ttu-id="0a54f-183">f.</span><span class="sxs-lookup"><span data-stu-id="0a54f-183">f.</span></span> <span data-ttu-id="0a54f-184">W hello **mapowania imię Crm** pole tekstowe, typ `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname`.</span><span class="sxs-lookup"><span data-stu-id="0a54f-184">In hello **Crm First Name Mapping** textbox, type `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname`.</span></span>
    
    <span data-ttu-id="0a54f-185">g.</span><span class="sxs-lookup"><span data-stu-id="0a54f-185">g.</span></span> <span data-ttu-id="0a54f-186">W hello **nazwisko Crm mapowania** pole tekstowe, typ `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/surname`.</span><span class="sxs-lookup"><span data-stu-id="0a54f-186">In hello **Crm lastName Mapping** textbox, type `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/surname`.</span></span>  

    <span data-ttu-id="0a54f-187">h.</span><span class="sxs-lookup"><span data-stu-id="0a54f-187">h.</span></span> <span data-ttu-id="0a54f-188">Kliknij pozycję **Zapisz**.</span><span class="sxs-lookup"><span data-stu-id="0a54f-188">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="0a54f-189">Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz hello [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji hello!</span><span class="sxs-lookup"><span data-stu-id="0a54f-189">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="0a54f-190">Po dodaniu tej aplikacji z hello **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij hello **rejestracji jednokrotnej** hello kartę i dostępu do osadzonych dokumentacji za pośrednictwem hello  **Konfiguracja** sekcji u dołu hello.</span><span class="sxs-lookup"><span data-stu-id="0a54f-190">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="0a54f-191">Więcej o hello osadzonych dokumentacji funkcji w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="0a54f-191">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 
 
### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="0a54f-192">Tworzenie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="0a54f-192">Creating an Azure AD test user</span></span>
<span data-ttu-id="0a54f-193">Celem Hello w tej sekcji jest toocreate użytkownika testowego, w portalu Azure o nazwie Simona Britta hello.</span><span class="sxs-lookup"><span data-stu-id="0a54f-193">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Tworzenie użytkowników usługi Azure AD][100]

<span data-ttu-id="0a54f-195">**toocreate użytkownika testowego w usłudze Azure AD, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="0a54f-195">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="0a54f-196">W hello **portalu Azure**na temat hello w lewym okienku nawigacji, kliknij przycisk **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="0a54f-196">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-insideview-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="0a54f-198">toodisplay hello listę użytkowników, przejdź zbyt**użytkowników i grup** i kliknij przycisk **wszyscy użytkownicy**.</span><span class="sxs-lookup"><span data-stu-id="0a54f-198">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-insideview-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="0a54f-200">Witaj tooopen **użytkownika** okna dialogowego, kliknij przycisk **Dodaj** u góry hello hello okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="0a54f-200">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-insideview-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="0a54f-202">Na powitania **użytkownika** okna dialogowego wykonaj hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="0a54f-202">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-insideview-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="0a54f-204">a.</span><span class="sxs-lookup"><span data-stu-id="0a54f-204">a.</span></span> <span data-ttu-id="0a54f-205">W hello **nazwa** pole tekstowe, typ **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="0a54f-205">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="0a54f-206">b.</span><span class="sxs-lookup"><span data-stu-id="0a54f-206">b.</span></span> <span data-ttu-id="0a54f-207">W hello **nazwy użytkownika** pole tekstowe, hello typu **adres e-mail** z BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="0a54f-207">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="0a54f-208">c.</span><span class="sxs-lookup"><span data-stu-id="0a54f-208">c.</span></span> <span data-ttu-id="0a54f-209">Wybierz **Pokaż hasło** i zanotuj wartość hello hello **hasło**.</span><span class="sxs-lookup"><span data-stu-id="0a54f-209">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="0a54f-210">d.</span><span class="sxs-lookup"><span data-stu-id="0a54f-210">d.</span></span> <span data-ttu-id="0a54f-211">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="0a54f-211">Click **Create**.</span></span>
 
### <a name="creating-a-insideview-test-user"></a><span data-ttu-id="0a54f-212">Tworzenie użytkownika testowego InsideView</span><span class="sxs-lookup"><span data-stu-id="0a54f-212">Creating a InsideView test user</span></span>

<span data-ttu-id="0a54f-213">toolog użytkowników tooenable usługi Azure AD w tooInsideView, muszą mieć przydzielone w tooInsideView.</span><span class="sxs-lookup"><span data-stu-id="0a54f-213">tooenable Azure AD users toolog in tooInsideView, they must be provisioned in tooInsideView.</span></span> <span data-ttu-id="0a54f-214">W przypadku hello InsideView Inicjowanie obsługi to zadanie ręczne.</span><span class="sxs-lookup"><span data-stu-id="0a54f-214">In hello case of InsideView, provisioning is a manual task.</span></span>

<span data-ttu-id="0a54f-215">Użytkownicy tooget lub kontakty utworzone w InsideView, skontaktuj się z [zespołem pomocy technicznej InsideView](mailto:support@insideview.com).</span><span class="sxs-lookup"><span data-stu-id="0a54f-215">tooget users or contacts created in InsideView, Contact [InsideView support team](mailto:support@insideview.com).</span></span>

>[!NOTE]
><span data-ttu-id="0a54f-216">Możesz użyć innych InsideView użytkownika konta tworzenia narzędzi lub interfejsów API dostarczonych przez InsideView tooprovision kont użytkowników usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="0a54f-216">You can use any other InsideView user account creation tools or APIs provided by InsideView tooprovision Azure AD user accounts.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="0a54f-217">Przypisanie użytkownika testowego hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="0a54f-217">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="0a54f-218">W tej sekcji możesz włączyć toouse Simona Britta Azure logowania jednokrotnego za udzielanie dostępu tooInsideView.</span><span class="sxs-lookup"><span data-stu-id="0a54f-218">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooInsideView.</span></span>

![Przypisz użytkownika][200] 

<span data-ttu-id="0a54f-220">**tooassign tooInsideView Simona Britta wykonaj hello następujące kroki:**</span><span class="sxs-lookup"><span data-stu-id="0a54f-220">**tooassign Britta Simon tooInsideView, perform hello following steps:**</span></span>

1. <span data-ttu-id="0a54f-221">W portalu Azure hello, otwórz widok aplikacji hello, a następnie przejdź do widoku katalogu toohello i przejść za**aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="0a54f-221">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Przypisz użytkownika][201] 

2. <span data-ttu-id="0a54f-223">Z listy aplikacji hello wybierz **InsideView**.</span><span class="sxs-lookup"><span data-stu-id="0a54f-223">In hello applications list, select **InsideView**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-insideview-tutorial/tutorial_insideview_app.png) 

3. <span data-ttu-id="0a54f-225">W menu powitania po lewej stronie powitania kliknij **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="0a54f-225">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Przypisz użytkownika][202] 

4. <span data-ttu-id="0a54f-227">Kliknij przycisk **Dodaj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="0a54f-227">Click **Add** button.</span></span> <span data-ttu-id="0a54f-228">Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="0a54f-228">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Przypisz użytkownika][203]

5. <span data-ttu-id="0a54f-230">Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** hello listy użytkowników.</span><span class="sxs-lookup"><span data-stu-id="0a54f-230">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="0a54f-231">Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="0a54f-231">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="0a54f-232">Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="0a54f-232">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="0a54f-233">Testowanie rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="0a54f-233">Testing single sign-on</span></span>

<span data-ttu-id="0a54f-234">W tej sekcji można przetestować konfiguracji usługi Azure AD pojedynczego logowania jednokrotnego przy użyciu hello panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="0a54f-234">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="0a54f-235">Po kliknięciu kafelka InsideView hello w hello Panel dostępu, należy pobrać automatycznie zalogowane tooyour InsideView aplikacji.</span><span class="sxs-lookup"><span data-stu-id="0a54f-235">When you click hello InsideView tile in hello Access Panel, you should get automatically signed-on tooyour InsideView application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="0a54f-236">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="0a54f-236">Additional resources</span></span>

* [<span data-ttu-id="0a54f-237">Lista samouczków dotyczących tooIntegrate aplikacji SaaS w usłudze Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="0a54f-237">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="0a54f-238">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="0a54f-238">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-insideview-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-insideview-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-insideview-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-insideview-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-insideview-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-insideview-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-insideview-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-insideview-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-insideview-tutorial/tutorial_general_203.png

