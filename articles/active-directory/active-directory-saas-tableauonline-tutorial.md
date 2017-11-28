---
title: "Samouczek: Integracja usługi Azure Active Directory z usługą Tableau Online | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak tooconfigure logowanie jednokrotne między usługą Azure Active Directory i Tableau Online."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 1d4b1149-ba3b-4f4e-8bce-9791316b730d
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/13/2017
ms.author: jeedes
ms.openlocfilehash: 590b2674270c340b4750c7b6feeaf4f0df4bf853
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-tableau-online"></a><span data-ttu-id="04f3a-103">Samouczek: Integracja usługi Azure Active Directory z usługą Tableau Online</span><span class="sxs-lookup"><span data-stu-id="04f3a-103">Tutorial: Azure Active Directory integration with Tableau Online</span></span>

<span data-ttu-id="04f3a-104">Z tego samouczka, dowiesz się, jak toointegrate Tableau Online z usługą Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="04f3a-104">In this tutorial, you learn how toointegrate Tableau Online with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="04f3a-105">Integrowanie Tableau Online z usługą Azure AD zapewnia hello następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="04f3a-105">Integrating Tableau Online with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="04f3a-106">Można kontrolować w usłudze Azure AD, kto ma dostęp tooTableau Online</span><span class="sxs-lookup"><span data-stu-id="04f3a-106">You can control in Azure AD who has access tooTableau Online</span></span>
- <span data-ttu-id="04f3a-107">Można włączyć użytkownika użytkownicy tooautomatically get zalogowane tooTableau Online (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="04f3a-107">You can enable your users tooautomatically get signed-on tooTableau Online (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="04f3a-108">Możesz zarządzać kont w jednej centralnej lokalizacji - hello portalu Azure</span><span class="sxs-lookup"><span data-stu-id="04f3a-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="04f3a-109">Jeśli chcesz tooknow więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="04f3a-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="04f3a-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="04f3a-110">Prerequisites</span></span>

<span data-ttu-id="04f3a-111">tooconfigure integracji z usługą Azure AD Tableau online należy hello następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="04f3a-111">tooconfigure Azure AD integration with Tableau Online, you need hello following items:</span></span>

- <span data-ttu-id="04f3a-112">Subskrypcję usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="04f3a-112">An Azure AD subscription</span></span>
- <span data-ttu-id="04f3a-113">Tableau Online logowanie jednokrotne włączone subskrypcji</span><span class="sxs-lookup"><span data-stu-id="04f3a-113">A Tableau Online single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="04f3a-114">tootest hello kroków w tym samouczku, zaleca się przy użyciu środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="04f3a-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="04f3a-115">tootest hello kroki opisane w tym samouczku, należy stosować te zalecenia:</span><span class="sxs-lookup"><span data-stu-id="04f3a-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="04f3a-116">Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="04f3a-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="04f3a-117">Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz pobrać miesięczna wersja próbna [tutaj](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="04f3a-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="04f3a-118">Opis scenariusza</span><span class="sxs-lookup"><span data-stu-id="04f3a-118">Scenario description</span></span>
<span data-ttu-id="04f3a-119">W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym.</span><span class="sxs-lookup"><span data-stu-id="04f3a-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="04f3a-120">Scenariusz Hello opisane w tym samouczku składa się z dwóch głównych elementów:</span><span class="sxs-lookup"><span data-stu-id="04f3a-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="04f3a-121">Dodawanie Tableau Online z galerii hello</span><span class="sxs-lookup"><span data-stu-id="04f3a-121">Adding Tableau Online from hello gallery</span></span>
2. <span data-ttu-id="04f3a-122">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="04f3a-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-tableau-online-from-hello-gallery"></a><span data-ttu-id="04f3a-123">Dodawanie Tableau Online z galerii hello</span><span class="sxs-lookup"><span data-stu-id="04f3a-123">Adding Tableau Online from hello gallery</span></span>
<span data-ttu-id="04f3a-124">tooconfigure hello integracji Tableau Online z usługą Azure AD, należy tooadd Tableau Online z hello galerii tooyour listę zarządzanych aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="04f3a-124">tooconfigure hello integration of Tableau Online into Azure AD, you need tooadd Tableau Online from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="04f3a-125">**tooadd Tableau Online z galerii hello, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="04f3a-125">**tooadd Tableau Online from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="04f3a-126">W hello  **[portalu Azure](https://portal.azure.com)**na temat hello panelu nawigacji po lewej stronie, kliknij przycisk **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="04f3a-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Usługa Active Directory][1]

2. <span data-ttu-id="04f3a-128">Przejdź za**aplikacje dla przedsiębiorstw**.</span><span class="sxs-lookup"><span data-stu-id="04f3a-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="04f3a-129">Następnie przejdź zbyt**wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="04f3a-129">Then go too**All applications**.</span></span>

    ![Aplikacje][2]
    
3. <span data-ttu-id="04f3a-131">tooadd nową aplikację, kliknij przycisk **nowej aplikacji** przycisk u góry hello okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="04f3a-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplikacje][3]

4. <span data-ttu-id="04f3a-133">W polu wyszukiwania hello wpisz **Tableau Online**.</span><span class="sxs-lookup"><span data-stu-id="04f3a-133">In hello search box, type **Tableau Online**.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-tableauonline-tutorial/tutorial_tableauonline_search.png)

5. <span data-ttu-id="04f3a-135">W panelu wyników hello, wybierz **Tableau Online**, a następnie kliknij przycisk **Dodaj** przycisk tooadd hello aplikacji.</span><span class="sxs-lookup"><span data-stu-id="04f3a-135">In hello results panel, select **Tableau Online**, and then click **Add** button tooadd hello application.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-tableauonline-tutorial/tutorial_tableauonline_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="04f3a-137">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="04f3a-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="04f3a-138">W tej sekcji można skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z Tableau Online na podstawie użytkownika testowego, nazywany "Britta Simona".</span><span class="sxs-lookup"><span data-stu-id="04f3a-138">In this section, you configure and test Azure AD single sign-on with Tableau Online based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="04f3a-139">Dla pojedynczego logowania jednokrotnego toowork usługi Azure AD musi tooknow użytkownika odpowiednikiem hello Tableau online jest tooa użytkownika w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="04f3a-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Tableau Online is tooa user in Azure AD.</span></span> <span data-ttu-id="04f3a-140">Innymi słowy relację łącza między użytkownika usługi Azure AD i hello użytkownikowi w trybie Online Tableau musi toobe ustanowione.</span><span class="sxs-lookup"><span data-stu-id="04f3a-140">In other words, a link relationship between an Azure AD user and hello related user in Tableau Online needs toobe established.</span></span>

<span data-ttu-id="04f3a-141">W Tableau w trybie Online, należy przypisać wartość hello hello **nazwy użytkownika** w usłudze Azure AD jako wartość hello hello **Username** tooestablish hello łącze relacji.</span><span class="sxs-lookup"><span data-stu-id="04f3a-141">In Tableau Online, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="04f3a-142">tooconfigure i testowych usługi Azure AD rejestracji jednokrotnej z Tableau Online, należy po bloków konstrukcyjnych hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="04f3a-142">tooconfigure and test Azure AD single sign-on with Tableau Online, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="04f3a-143">**[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configuring-azure-ad-single-sign-on)**  -tooenable Twojego toouse użytkowników tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="04f3a-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="04f3a-144">**[Tworzenie użytkownika testowego usługi Azure AD](#creating-an-azure-ad-test-user)**  -tootest usługi Azure AD rejestracji jednokrotnej z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="04f3a-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="04f3a-145">**[Tworzenie użytkownika testowego Tableau Online](#creating-a-tableau-online-test-user)**  -toohave odpowiednikiem Simona Britta w Tableau Online, które zostało połączone toohello usługi Azure AD reprezentację użytkownika.</span><span class="sxs-lookup"><span data-stu-id="04f3a-145">**[Creating a Tableau Online test user](#creating-a-tableau-online-test-user)** - toohave a counterpart of Britta Simon in Tableau Online that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="04f3a-146">**[Przypisanie użytkownika testowego hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Simona Britta toouse usługi Azure AD rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="04f3a-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="04f3a-147">**[Testowanie rejestracji jednokrotnej](#testing-single-sign-on)**  -tooverify czy hello konfiguracji działania.</span><span class="sxs-lookup"><span data-stu-id="04f3a-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="04f3a-148">Konfigurowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="04f3a-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="04f3a-149">W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w hello portalu Azure i skonfigurować rejestracji jednokrotnej w trybie Online Tableau aplikacji.</span><span class="sxs-lookup"><span data-stu-id="04f3a-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Tableau Online application.</span></span>

<span data-ttu-id="04f3a-150">**tooconfigure usługi Azure AD rejestracji jednokrotnej z Tableau Online wykonaj hello następujące kroki:**</span><span class="sxs-lookup"><span data-stu-id="04f3a-150">**tooconfigure Azure AD single sign-on with Tableau Online, perform hello following steps:**</span></span>

1. <span data-ttu-id="04f3a-151">W portalu Azure na powitania hello **Tableau Online** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.</span><span class="sxs-lookup"><span data-stu-id="04f3a-151">In hello Azure portal, on hello **Tableau Online** application integration page, click **Single sign-on**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej][4]

2. <span data-ttu-id="04f3a-153">Na powitania **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** tooenable rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="04f3a-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-tableauonline-tutorial/tutorial_tableauonline_samlbase.png)

3. <span data-ttu-id="04f3a-155">Na powitania **Tableau Online domeny i adres URL** sekcji, wykonaj następujące kroki hello:</span><span class="sxs-lookup"><span data-stu-id="04f3a-155">On hello **Tableau Online Domain and URLs** section, perform hello following steps:</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-tableauonline-tutorial/tutorial_tableauonline_url.png)
    
    <span data-ttu-id="04f3a-157">a.</span><span class="sxs-lookup"><span data-stu-id="04f3a-157">a.</span></span> <span data-ttu-id="04f3a-158">W hello **adres URL logowania** pole tekstowe, wprowadź adres URL hello:`https://sso.online.tableau.com`</span><span class="sxs-lookup"><span data-stu-id="04f3a-158">In hello **Sign-on URL** textbox, type hello URL: `https://sso.online.tableau.com`</span></span>

    <span data-ttu-id="04f3a-159">b.</span><span class="sxs-lookup"><span data-stu-id="04f3a-159">b.</span></span> <span data-ttu-id="04f3a-160">W hello **identyfikator** pole tekstowe, wprowadź adres URL hello:`https://sso.online.tableau.com/public/sp/<instancename>`</span><span class="sxs-lookup"><span data-stu-id="04f3a-160">In hello **Identifier** textbox, type hello URL: `https://sso.online.tableau.com/public/sp/<instancename>`</span></span>

4. <span data-ttu-id="04f3a-161">Na powitania **certyfikat podpisywania SAML** kliknij **XML metadanych** , a następnie zapisz plik metadanych hello na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="04f3a-161">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-tableauonline-tutorial/tutorial_tableauonline_certificate.png) 

5. <span data-ttu-id="04f3a-163">Kliknij przycisk **zapisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="04f3a-163">Click **Save** button.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-tableauonline-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="04f3a-165">W oknie innej przeglądarki, logowania jednokrotnego tooyour aplikacji Tableau Online.</span><span class="sxs-lookup"><span data-stu-id="04f3a-165">In a different browser window, sign-on tooyour Tableau Online application.</span></span> <span data-ttu-id="04f3a-166">Przejdź za**ustawienia** , a następnie **uwierzytelniania**.</span><span class="sxs-lookup"><span data-stu-id="04f3a-166">Go too**Settings** and then **Authentication**.</span></span>
   
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-tableauonline-tutorial/tutorial_tableauonline_09.png)
    
7. <span data-ttu-id="04f3a-168">tooenable SAML, w obszarze **typy uwierzytelniania** sekcji.</span><span class="sxs-lookup"><span data-stu-id="04f3a-168">tooenable SAML, Under **Authentication Types** section.</span></span> <span data-ttu-id="04f3a-169">Sprawdź hello **rejestracji jednokrotnej z SAML** wyboru.</span><span class="sxs-lookup"><span data-stu-id="04f3a-169">Check hello **Single sign-on with SAML** checkbox.</span></span>
   
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-tableauonline-tutorial/tutorial_tableauonline_12.png)

8. <span data-ttu-id="04f3a-171">Przewiń w dół do **Importowanie pliku metadanych do Tableau Online** sekcji.</span><span class="sxs-lookup"><span data-stu-id="04f3a-171">Scroll down until **Import metadata file into Tableau Online** section.</span></span>  <span data-ttu-id="04f3a-172">Kliknij przycisk Przeglądaj i zaimportować plik metadanych hello, które zostały pobrane z usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="04f3a-172">Click Browse and import hello metadata file you have downloaded from Azure AD.</span></span> <span data-ttu-id="04f3a-173">Następnie kliknij przycisk **Zastosuj**.</span><span class="sxs-lookup"><span data-stu-id="04f3a-173">Then, click **Apply**.</span></span>
   
   ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-tableauonline-tutorial/tutorial_tableauonline_13.png)

9. <span data-ttu-id="04f3a-175">W hello **odpowiada potwierdzenia** sekcję należy wstawić hello odpowiedniego dostawcy tożsamości potwierdzenia nazwę **adres e-mail**, **imię**, i **nazwisko** .</span><span class="sxs-lookup"><span data-stu-id="04f3a-175">In hello **Match assertions** section, insert hello corresponding Identity Provider assertion name for **email address**, **first name**, and **last name**.</span></span> <span data-ttu-id="04f3a-176">tooget te informacje z usługi Azure AD:</span><span class="sxs-lookup"><span data-stu-id="04f3a-176">tooget this information from Azure AD:</span></span> 
  
    <span data-ttu-id="04f3a-177">a.</span><span class="sxs-lookup"><span data-stu-id="04f3a-177">a.</span></span> <span data-ttu-id="04f3a-178">W portalu Azure Witaj, przejdź na powitania **Tableau Online** strony integracja aplikacji.</span><span class="sxs-lookup"><span data-stu-id="04f3a-178">In hello Azure portal, go on hello **Tableau Online** application integration page.</span></span>
    
    <span data-ttu-id="04f3a-179">b.</span><span class="sxs-lookup"><span data-stu-id="04f3a-179">b.</span></span> <span data-ttu-id="04f3a-180">W sekcji atrybuty hello, wybierz hello **"wyświetlić i edytować wszystkie atrybuty użytkowników"** pola wyboru.</span><span class="sxs-lookup"><span data-stu-id="04f3a-180">In hello attributes section, Select hello **"view and edit all other user attributes"** checkbox.</span></span> 
    
   ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-tableauonline-tutorial/attributesection.png)
      
    <span data-ttu-id="04f3a-182">c.</span><span class="sxs-lookup"><span data-stu-id="04f3a-182">c.</span></span> <span data-ttu-id="04f3a-183">Skopiuj wartość przestrzeni nazw hello tych atrybutów: givenname, poczty e-mail i nazwisko przy użyciu hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="04f3a-183">Copy hello namespace value for these attributes: givenname, email and surname by using hello following steps:</span></span>

   ![Azure AD rejestracji jednokrotnej](./media/active-directory-saas-tableauonline-tutorial/tutorial_tableauonline_10.png)
    
    <span data-ttu-id="04f3a-185">d.</span><span class="sxs-lookup"><span data-stu-id="04f3a-185">d.</span></span> <span data-ttu-id="04f3a-186">Kliknij przycisk **user.givenname** wartości</span><span class="sxs-lookup"><span data-stu-id="04f3a-186">Click **user.givenname** value</span></span> 
    
    <span data-ttu-id="04f3a-187">e.</span><span class="sxs-lookup"><span data-stu-id="04f3a-187">e.</span></span> <span data-ttu-id="04f3a-188">Skopiuj wartość hello z hello **przestrzeni nazw** pola tekstowego.</span><span class="sxs-lookup"><span data-stu-id="04f3a-188">Copy hello value from hello **namespace** textbox.</span></span>

   ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-tableauonline-tutorial/attributesection2.png)

    <span data-ttu-id="04f3a-190">f.</span><span class="sxs-lookup"><span data-stu-id="04f3a-190">f.</span></span> <span data-ttu-id="04f3a-191">toocopy hello namesapce wartości hello poczty e-mail i nazwisko wykonaj hello w poprzednich krokach.</span><span class="sxs-lookup"><span data-stu-id="04f3a-191">toocopy hello namesapce values for hello email and surname follow hello preceding steps.</span></span>

    <span data-ttu-id="04f3a-192">g.</span><span class="sxs-lookup"><span data-stu-id="04f3a-192">g.</span></span> <span data-ttu-id="04f3a-193">Przełącz toohello aplikacji Tableau Online, a następnie ustaw hello **Tableau Online atrybuty** sekcji w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="04f3a-193">Switch toohello Tableau Online application, then set hello **Tableau Online Attributes** section as follows:</span></span>
     * <span data-ttu-id="04f3a-194">Adres e-mail: **poczty** lub **userprincipalname**</span><span class="sxs-lookup"><span data-stu-id="04f3a-194">Email: **mail** or **userprincipalname**</span></span>
     * <span data-ttu-id="04f3a-195">Imię: **givenname**</span><span class="sxs-lookup"><span data-stu-id="04f3a-195">First name: **givenname**</span></span>
     * <span data-ttu-id="04f3a-196">Nazwisko: **nazwisko**</span><span class="sxs-lookup"><span data-stu-id="04f3a-196">Last name: **surname**</span></span>
   
   ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-tableauonline-tutorial/tutorial_tableauonline_14.png)

> [!TIP]
> <span data-ttu-id="04f3a-198">Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz hello [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji hello!</span><span class="sxs-lookup"><span data-stu-id="04f3a-198">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="04f3a-199">Po dodaniu tej aplikacji z hello **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij hello **rejestracji jednokrotnej** hello kartę i dostępu do osadzonych dokumentacji za pośrednictwem hello  **Konfiguracja** sekcji u dołu hello.</span><span class="sxs-lookup"><span data-stu-id="04f3a-199">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="04f3a-200">Więcej o hello osadzonych dokumentacji funkcji w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="04f3a-200">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="04f3a-201">Tworzenie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="04f3a-201">Creating an Azure AD test user</span></span>
<span data-ttu-id="04f3a-202">Celem Hello w tej sekcji jest toocreate użytkownika testowego, w portalu Azure o nazwie Simona Britta hello.</span><span class="sxs-lookup"><span data-stu-id="04f3a-202">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Tworzenie użytkowników usługi Azure AD][100]

<span data-ttu-id="04f3a-204">**toocreate użytkownika testowego w usłudze Azure AD, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="04f3a-204">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="04f3a-205">W hello **portalu Azure**na temat hello w lewym okienku nawigacji, kliknij przycisk **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="04f3a-205">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-tableauonline-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="04f3a-207">toodisplay hello listę użytkowników, przejdź zbyt**użytkowników i grup** i kliknij przycisk **wszyscy użytkownicy**.</span><span class="sxs-lookup"><span data-stu-id="04f3a-207">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-tableauonline-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="04f3a-209">Witaj tooopen **użytkownika** okna dialogowego, kliknij przycisk **Dodaj** u góry hello hello okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="04f3a-209">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-tableauonline-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="04f3a-211">Na powitania **użytkownika** okna dialogowego wykonaj hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="04f3a-211">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-tableauonline-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="04f3a-213">a.</span><span class="sxs-lookup"><span data-stu-id="04f3a-213">a.</span></span> <span data-ttu-id="04f3a-214">W hello **nazwa** pole tekstowe, typ **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="04f3a-214">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="04f3a-215">b.</span><span class="sxs-lookup"><span data-stu-id="04f3a-215">b.</span></span> <span data-ttu-id="04f3a-216">W hello **nazwy użytkownika** pole tekstowe, hello typu **adres e-mail** z BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="04f3a-216">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="04f3a-217">c.</span><span class="sxs-lookup"><span data-stu-id="04f3a-217">c.</span></span> <span data-ttu-id="04f3a-218">Wybierz **Pokaż hasło** i zanotuj wartość hello hello **hasło**.</span><span class="sxs-lookup"><span data-stu-id="04f3a-218">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="04f3a-219">d.</span><span class="sxs-lookup"><span data-stu-id="04f3a-219">d.</span></span> <span data-ttu-id="04f3a-220">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="04f3a-220">Click **Create**.</span></span>
 
### <a name="creating-a-tableau-online-test-user"></a><span data-ttu-id="04f3a-221">Tworzenie użytkownika testowego Tableau Online</span><span class="sxs-lookup"><span data-stu-id="04f3a-221">Creating a Tableau Online test user</span></span>

<span data-ttu-id="04f3a-222">W tej sekcji należy utworzyć użytkownika o nazwie Simona Britta Tableau online.</span><span class="sxs-lookup"><span data-stu-id="04f3a-222">In this section, you create a user called Britta Simon in Tableau Online.</span></span>

1. <span data-ttu-id="04f3a-223">Na **Tableau Online**, kliknij przycisk **ustawienia** , a następnie **uwierzytelniania** sekcji.</span><span class="sxs-lookup"><span data-stu-id="04f3a-223">On **Tableau Online**, click **Settings** and then **Authentication** section.</span></span> <span data-ttu-id="04f3a-224">Przewiń w dół za**Wybieranie: Użytkownicy** sekcji.</span><span class="sxs-lookup"><span data-stu-id="04f3a-224">Scroll down too**Select Users** section.</span></span> <span data-ttu-id="04f3a-225">Kliknij przycisk **dodawania użytkowników** , a następnie **wprowadź adresy E-mail**.</span><span class="sxs-lookup"><span data-stu-id="04f3a-225">Click **Add Users** and then **Enter Email Addresses**.</span></span>
   
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-tableauonline-tutorial/tutorial_tableauonline_15.png)
2. <span data-ttu-id="04f3a-227">Wybierz **Dodawanie użytkowników do uwierzytelniania rejestracji jednokrotnej (SSO)**.</span><span class="sxs-lookup"><span data-stu-id="04f3a-227">Select **Add users for single sign-on (SSO) authentication**.</span></span> <span data-ttu-id="04f3a-228">W hello **wprowadź adresy E-mail** Dodaj pole tekstowebritta.simon@contoso.com</span><span class="sxs-lookup"><span data-stu-id="04f3a-228">In hello **Enter Email Addresses** textbox add britta.simon@contoso.com</span></span>
   
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-tableauonline-tutorial/tutorial_tableauonline_11.png)
3. <span data-ttu-id="04f3a-230">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="04f3a-230">Click **Create**.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="04f3a-231">Przypisanie użytkownika testowego hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="04f3a-231">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="04f3a-232">W tej sekcji możesz włączyć toouse Simona Britta Azure logowania jednokrotnego za udzielanie dostępu tooTableau w trybie Online.</span><span class="sxs-lookup"><span data-stu-id="04f3a-232">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooTableau Online.</span></span>

![Przypisz użytkownika][200] 

<span data-ttu-id="04f3a-234">**tooassign tooTableau Simona Britta w trybie Online, wykonaj hello następujące kroki:**</span><span class="sxs-lookup"><span data-stu-id="04f3a-234">**tooassign Britta Simon tooTableau Online, perform hello following steps:**</span></span>

1. <span data-ttu-id="04f3a-235">W portalu Azure hello, otwórz widok aplikacji hello, a następnie przejdź do widoku katalogu toohello i przejść za**aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="04f3a-235">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Przypisz użytkownika][201] 

2. <span data-ttu-id="04f3a-237">Z listy aplikacji hello wybierz **Tableau Online**.</span><span class="sxs-lookup"><span data-stu-id="04f3a-237">In hello applications list, select **Tableau Online**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-tableauonline-tutorial/tutorial_tableauonline_app.png) 

3. <span data-ttu-id="04f3a-239">W menu powitania po lewej stronie powitania kliknij **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="04f3a-239">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Przypisz użytkownika][202] 

4. <span data-ttu-id="04f3a-241">Kliknij przycisk **Dodaj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="04f3a-241">Click **Add** button.</span></span> <span data-ttu-id="04f3a-242">Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="04f3a-242">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Przypisz użytkownika][203]

5. <span data-ttu-id="04f3a-244">Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** hello listy użytkowników.</span><span class="sxs-lookup"><span data-stu-id="04f3a-244">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="04f3a-245">Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="04f3a-245">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="04f3a-246">Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="04f3a-246">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="04f3a-247">Testowanie rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="04f3a-247">Testing single sign-on</span></span>

<span data-ttu-id="04f3a-248">Celem Hello w tej sekcji jest tootest programu Azure AD SSO konfiguracji przy użyciu hello panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="04f3a-248">hello objective of this section is tootest your Azure AD SSO configuration using hello Access Panel.</span></span>

<span data-ttu-id="04f3a-249">Po kliknięciu kafelka Tableau Online hello w hello Panel dostępu, należy pobrać aplikacji Tableau Online tooyour zalogowane automatycznie.</span><span class="sxs-lookup"><span data-stu-id="04f3a-249">When you click hello Tableau Online tile in hello Access Panel, you should get automatically signed-on tooyour Tableau Online application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="04f3a-250">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="04f3a-250">Additional resources</span></span>

* [<span data-ttu-id="04f3a-251">Lista samouczków dotyczących tooIntegrate aplikacji SaaS w usłudze Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="04f3a-251">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="04f3a-252">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="04f3a-252">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-tableauonline-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-tableauonline-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-tableauonline-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-tableauonline-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-tableauonline-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-tableauonline-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-tableauonline-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-tableauonline-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-tableauonline-tutorial/tutorial_general_203.png

