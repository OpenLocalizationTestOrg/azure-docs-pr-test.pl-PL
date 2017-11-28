---
title: "Samouczek: Integracja usługi Azure Active Directory z usługą Ekspresyjne Online | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak tooconfigure logowanie jednokrotne między usługą Azure Active Directory i Ekspresyjne Online."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 4fd6b29b-1b46-4fd1-9f5e-16b1c9d892cd
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/09/2017
ms.author: jeedes
ms.openlocfilehash: b728606ded7687d424a8175d0602b6b00f398497
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-bgs-online"></a><span data-ttu-id="599a8-103">Samouczek: Integracja usługi Azure Active Directory z usługą Ekspresyjne Online</span><span class="sxs-lookup"><span data-stu-id="599a8-103">Tutorial: Azure Active Directory integration with BGS Online</span></span>

<span data-ttu-id="599a8-104">Z tego samouczka, dowiesz się, jak toointegrate Ekspresyjne Online z usługą Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="599a8-104">In this tutorial, you learn how toointegrate BGS Online with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="599a8-105">Integrowanie Ekspresyjne Online z usługą Azure AD zapewnia hello następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="599a8-105">Integrating BGS Online with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="599a8-106">Można kontrolować w usłudze Azure AD, kto ma dostęp tooBGS Online</span><span class="sxs-lookup"><span data-stu-id="599a8-106">You can control in Azure AD who has access tooBGS Online</span></span>
- <span data-ttu-id="599a8-107">Można włączyć użytkownika użytkownicy tooautomatically get zalogowane tooBGS Online (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="599a8-107">You can enable your users tooautomatically get signed-on tooBGS Online (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="599a8-108">Możesz zarządzać kont w jednej centralnej lokalizacji - hello portalu Azure</span><span class="sxs-lookup"><span data-stu-id="599a8-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="599a8-109">Jeśli chcesz tooknow więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="599a8-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="599a8-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="599a8-110">Prerequisites</span></span>

<span data-ttu-id="599a8-111">tooconfigure integracji z usługą Azure AD Ekspresyjne online należy hello następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="599a8-111">tooconfigure Azure AD integration with BGS Online, you need hello following items:</span></span>

- <span data-ttu-id="599a8-112">Subskrypcję usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="599a8-112">An Azure AD subscription</span></span>
- <span data-ttu-id="599a8-113">Ekspresyjne Online jednokrotnego włączone subskrypcji</span><span class="sxs-lookup"><span data-stu-id="599a8-113">A BGS Online single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="599a8-114">tootest hello kroków w tym samouczku, zaleca się przy użyciu środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="599a8-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="599a8-115">tootest hello kroki opisane w tym samouczku, należy stosować te zalecenia:</span><span class="sxs-lookup"><span data-stu-id="599a8-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="599a8-116">Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="599a8-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="599a8-117">Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz pobrać miesięczna wersja próbna [tutaj](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="599a8-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="599a8-118">Opis scenariusza</span><span class="sxs-lookup"><span data-stu-id="599a8-118">Scenario description</span></span>
<span data-ttu-id="599a8-119">W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym.</span><span class="sxs-lookup"><span data-stu-id="599a8-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="599a8-120">Scenariusz Hello opisane w tym samouczku składa się z dwóch głównych elementów:</span><span class="sxs-lookup"><span data-stu-id="599a8-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="599a8-121">Dodawanie Ekspresyjne Online z galerii hello</span><span class="sxs-lookup"><span data-stu-id="599a8-121">Adding BGS Online from hello gallery</span></span>
2. <span data-ttu-id="599a8-122">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="599a8-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-bgs-online-from-hello-gallery"></a><span data-ttu-id="599a8-123">Dodawanie Ekspresyjne Online z galerii hello</span><span class="sxs-lookup"><span data-stu-id="599a8-123">Adding BGS Online from hello gallery</span></span>
<span data-ttu-id="599a8-124">tooconfigure hello integracji Ekspresyjne Online z usługą Azure AD, należy tooadd Ekspresyjne Online z hello galerii tooyour listę zarządzanych aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="599a8-124">tooconfigure hello integration of BGS Online into Azure AD, you need tooadd BGS Online from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="599a8-125">**tooadd Ekspresyjne Online z galerii hello, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="599a8-125">**tooadd BGS Online from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="599a8-126">W hello  **[portalu Azure](https://portal.azure.com)**na temat hello panelu nawigacji po lewej stronie, kliknij przycisk **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="599a8-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Usługa Active Directory][1]

2. <span data-ttu-id="599a8-128">Przejdź za**aplikacje dla przedsiębiorstw**.</span><span class="sxs-lookup"><span data-stu-id="599a8-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="599a8-129">Następnie przejdź zbyt**wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="599a8-129">Then go too**All applications**.</span></span>

    ![Aplikacje][2]
    
3. <span data-ttu-id="599a8-131">tooadd nową aplikację, kliknij przycisk **nowej aplikacji** przycisk u góry hello okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="599a8-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplikacje][3]

4. <span data-ttu-id="599a8-133">W polu wyszukiwania hello wpisz **Ekspresyjne Online**.</span><span class="sxs-lookup"><span data-stu-id="599a8-133">In hello search box, type **BGS Online**.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-bgsonline-tutorial/tutorial_bgsonline_search.png)

5. <span data-ttu-id="599a8-135">W panelu wyników hello, wybierz **Ekspresyjne Online**, a następnie kliknij przycisk **Dodaj** przycisk tooadd hello aplikacji.</span><span class="sxs-lookup"><span data-stu-id="599a8-135">In hello results panel, select **BGS Online**, and then click **Add** button tooadd hello application.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-bgsonline-tutorial/tutorial_bgsonline_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="599a8-137">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="599a8-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="599a8-138">W tej sekcji możesz skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej Ekspresyjne online na podstawie użytkownika testowego, nazywany "Britta Simona".</span><span class="sxs-lookup"><span data-stu-id="599a8-138">In this section, you configure and test Azure AD single sign-on with BGS Online based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="599a8-139">Dla pojedynczego logowania jednokrotnego toowork usługi Azure AD musi tooknow użytkownika odpowiednikiem hello Ekspresyjne online jest tooa użytkownika w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="599a8-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in BGS Online is tooa user in Azure AD.</span></span> <span data-ttu-id="599a8-140">Innymi słowy relację łącza między użytkownika usługi Azure AD i hello użytkownikowi w trybie Online Ekspresyjne musi toobe ustanowione.</span><span class="sxs-lookup"><span data-stu-id="599a8-140">In other words, a link relationship between an Azure AD user and hello related user in BGS Online needs toobe established.</span></span>

<span data-ttu-id="599a8-141">W trybie Online Ekspresyjne przypisać wartość hello hello **nazwy użytkownika** w usłudze Azure AD jako wartość hello hello **Username** tooestablish hello łącze relacji.</span><span class="sxs-lookup"><span data-stu-id="599a8-141">In BGS Online, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="599a8-142">tooconfigure i testowych usługi Azure AD rejestracji jednokrotnej z Ekspresyjne Online, należy po bloków konstrukcyjnych hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="599a8-142">tooconfigure and test Azure AD single sign-on with BGS Online, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="599a8-143">**[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configuring-azure-ad-single-sign-on)**  -tooenable Twojego toouse użytkowników tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="599a8-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="599a8-144">**[Tworzenie użytkownika testowego usługi Azure AD](#creating-an-azure-ad-test-user)**  -tootest usługi Azure AD rejestracji jednokrotnej z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="599a8-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="599a8-145">**[Tworzenie użytkownika testowego Ekspresyjne Online](#creating-a-bgs-online-test-user)**  -toohave odpowiednikiem Simona Britta w Ekspresyjne Online, które zostało połączone toohello usługi Azure AD reprezentację użytkownika.</span><span class="sxs-lookup"><span data-stu-id="599a8-145">**[Creating a BGS Online test user](#creating-a-bgs-online-test-user)** - toohave a counterpart of Britta Simon in BGS Online that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="599a8-146">**[Przypisanie użytkownika testowego hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Simona Britta toouse usługi Azure AD rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="599a8-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="599a8-147">**[Testowanie rejestracji jednokrotnej](#testing-single-sign-on)**  -tooverify czy hello konfiguracji działania.</span><span class="sxs-lookup"><span data-stu-id="599a8-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="599a8-148">Konfigurowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="599a8-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="599a8-149">W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w portalu Azure hello i skonfigurować logowanie jednokrotne w trybie Online Ekspresyjne aplikacji.</span><span class="sxs-lookup"><span data-stu-id="599a8-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your BGS Online application.</span></span>

<span data-ttu-id="599a8-150">**tooconfigure usługi Azure AD rejestracji jednokrotnej z Ekspresyjne Online wykonaj hello następujące kroki:**</span><span class="sxs-lookup"><span data-stu-id="599a8-150">**tooconfigure Azure AD single sign-on with BGS Online, perform hello following steps:**</span></span>

1. <span data-ttu-id="599a8-151">W portalu Azure na powitania hello **Ekspresyjne Online** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.</span><span class="sxs-lookup"><span data-stu-id="599a8-151">In hello Azure portal, on hello **BGS Online** application integration page, click **Single sign-on**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej][4]

2. <span data-ttu-id="599a8-153">Na powitania **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** tooenable rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="599a8-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-bgsonline-tutorial/tutorial_bgsonline_samlbase.png)

3. <span data-ttu-id="599a8-155">Na powitania **Ekspresyjne Online domeny i adres URL** sekcji, wykonaj następujące kroki hello:</span><span class="sxs-lookup"><span data-stu-id="599a8-155">On hello **BGS Online Domain and URLs** section, perform hello following steps:</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-bgsonline-tutorial/tutorial_bgsonline_url.png)

    <span data-ttu-id="599a8-157">a.</span><span class="sxs-lookup"><span data-stu-id="599a8-157">a.</span></span> <span data-ttu-id="599a8-158">W hello **identyfikator** tekstowym, wpisz adres URL za pomocą hello następującego wzorca:</span><span class="sxs-lookup"><span data-stu-id="599a8-158">In hello **Identifier** textbox, type a URL using hello following pattern:</span></span>

    <span data-ttu-id="599a8-159">W środowisku produkcyjnym należy używać tego wzorca`https://<company name>.millwardbrown.report`</span><span class="sxs-lookup"><span data-stu-id="599a8-159">For production environment, use this pattern `https://<company name>.millwardbrown.report`</span></span> 

    <span data-ttu-id="599a8-160">Dla środowiska testowego Użyj tego wzorca`https://millwardbrown.marketingtracker.nl/mt5/`</span><span class="sxs-lookup"><span data-stu-id="599a8-160">For test environment, use this pattern `https://millwardbrown.marketingtracker.nl/mt5/`</span></span>

    <span data-ttu-id="599a8-161">b.</span><span class="sxs-lookup"><span data-stu-id="599a8-161">b.</span></span> <span data-ttu-id="599a8-162">W hello **adres URL odpowiedzi** tekstowym, wpisz adres URL za pomocą hello następującego wzorca:</span><span class="sxs-lookup"><span data-stu-id="599a8-162">In hello **Reply URL** textbox, type a URL using hello following pattern:</span></span>
    
    <span data-ttu-id="599a8-163">W środowisku produkcyjnym należy używać tego wzorca`https://<company name>.millwardbrown.report/sso/saml/AssertionConsumerService.aspx`</span><span class="sxs-lookup"><span data-stu-id="599a8-163">For production environment, use this pattern `https://<company name>.millwardbrown.report/sso/saml/AssertionConsumerService.aspx`</span></span> 
      
    <span data-ttu-id="599a8-164">Dla środowiska testowego Użyj tego wzorca`https://millwardbrown.marketingtracker.nl/mt5/sso/saml/AssertionConsumerService.aspx`</span><span class="sxs-lookup"><span data-stu-id="599a8-164">For test environment, use this pattern `https://millwardbrown.marketingtracker.nl/mt5/sso/saml/AssertionConsumerService.aspx`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="599a8-165">Wartości te nie są prawdziwe.</span><span class="sxs-lookup"><span data-stu-id="599a8-165">These values are not real.</span></span> <span data-ttu-id="599a8-166">Witaj rzeczywisty identyfikator i odpowiedzi adresu URL, należy zaktualizować te wartości.</span><span class="sxs-lookup"><span data-stu-id="599a8-166">Update these values with hello actual Identifier and Reply URL.</span></span> <span data-ttu-id="599a8-167">Skontaktuj się z [zespół pomocy technicznej Online Ekspresyjne](mailTo:bgsdashboardteam@millwardbrown.com) tooget tych wartości.</span><span class="sxs-lookup"><span data-stu-id="599a8-167">Contact [BGS Online support team](mailTo:bgsdashboardteam@millwardbrown.com) tooget these values.</span></span>
 

4. <span data-ttu-id="599a8-168">Na powitania **certyfikat podpisywania SAML** kliknij **XML metadanych** , a następnie zapisz plik metadanych hello na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="599a8-168">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-bgsonline-tutorial/tutorial_bgsonline_certificate.png) 

5. <span data-ttu-id="599a8-170">Kliknij przycisk **zapisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="599a8-170">Click **Save** button.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-bgsonline-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="599a8-172">Na powitania **konfiguracji Online Ekspresyjne** kliknij **skonfigurować Ekspresyjne Online** tooopen **Konfigurowanie logowania jednokrotnego** okna.</span><span class="sxs-lookup"><span data-stu-id="599a8-172">On hello **BGS Online Configuration** section, click **Configure BGS Online** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="599a8-173">Kopiuj hello **SAML pojedynczy znak na adres URL usługi** z hello **sekcji krótkimi opisami.**</span><span class="sxs-lookup"><span data-stu-id="599a8-173">Copy hello **SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-bgsonline-tutorial/tutorial_bgsonline_configure.png) 

7. <span data-ttu-id="599a8-175">tooconfigure rejestracji jednokrotnej w **Ekspresyjne Online** strony, należy pobrać hello toosend **XML metadanych** i **SAML pojedynczy znak na adres URL usługi** zbyt[Ekspresyjne Zespół pomocy technicznej online](mailto:bgsdashboardteam@millwardbrown.com).</span><span class="sxs-lookup"><span data-stu-id="599a8-175">tooconfigure single sign-on on **BGS Online** side, you need toosend hello downloaded **Metadata XML** and **SAML Single Sign-On Service URL** too[BGS Online support team](mailto:bgsdashboardteam@millwardbrown.com).</span></span> 


> [!TIP]
> <span data-ttu-id="599a8-176">Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz hello [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji hello!</span><span class="sxs-lookup"><span data-stu-id="599a8-176">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="599a8-177">Po dodaniu tej aplikacji z hello **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij hello **rejestracji jednokrotnej** hello kartę i dostępu do osadzonych dokumentacji za pośrednictwem hello  **Konfiguracja** sekcji u dołu hello.</span><span class="sxs-lookup"><span data-stu-id="599a8-177">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="599a8-178">Więcej o hello osadzonych dokumentacji funkcji w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="599a8-178">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="599a8-179">Tworzenie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="599a8-179">Creating an Azure AD test user</span></span>
<span data-ttu-id="599a8-180">Celem Hello w tej sekcji jest toocreate użytkownika testowego, w portalu Azure o nazwie Simona Britta hello.</span><span class="sxs-lookup"><span data-stu-id="599a8-180">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Tworzenie użytkowników usługi Azure AD][100]

<span data-ttu-id="599a8-182">**toocreate użytkownika testowego w usłudze Azure AD, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="599a8-182">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="599a8-183">W hello **portalu Azure**na temat hello w lewym okienku nawigacji, kliknij przycisk **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="599a8-183">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-bgsonline-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="599a8-185">toodisplay hello listę użytkowników, przejdź zbyt**użytkowników i grup** i kliknij przycisk **wszyscy użytkownicy**.</span><span class="sxs-lookup"><span data-stu-id="599a8-185">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-bgsonline-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="599a8-187">Witaj tooopen **użytkownika** okna dialogowego, kliknij przycisk **Dodaj** u góry hello hello okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="599a8-187">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-bgsonline-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="599a8-189">Na powitania **użytkownika** okna dialogowego wykonaj hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="599a8-189">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-bgsonline-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="599a8-191">a.</span><span class="sxs-lookup"><span data-stu-id="599a8-191">a.</span></span> <span data-ttu-id="599a8-192">W hello **nazwa** pole tekstowe, typ **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="599a8-192">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="599a8-193">b.</span><span class="sxs-lookup"><span data-stu-id="599a8-193">b.</span></span> <span data-ttu-id="599a8-194">W hello **nazwy użytkownika** pole tekstowe, hello typu **adres e-mail** z BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="599a8-194">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="599a8-195">c.</span><span class="sxs-lookup"><span data-stu-id="599a8-195">c.</span></span> <span data-ttu-id="599a8-196">Wybierz **Pokaż hasło** i zanotuj wartość hello hello **hasło**.</span><span class="sxs-lookup"><span data-stu-id="599a8-196">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="599a8-197">d.</span><span class="sxs-lookup"><span data-stu-id="599a8-197">d.</span></span> <span data-ttu-id="599a8-198">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="599a8-198">Click **Create**.</span></span>
 
### <a name="creating-a-bgs-online-test-user"></a><span data-ttu-id="599a8-199">Tworzenie użytkownika testowego Ekspresyjne Online</span><span class="sxs-lookup"><span data-stu-id="599a8-199">Creating a BGS Online test user</span></span>

<span data-ttu-id="599a8-200">W tej sekcji należy utworzyć użytkownika o nazwie Simona Britta Ekspresyjne online.</span><span class="sxs-lookup"><span data-stu-id="599a8-200">In this section, you create a user called Britta Simon in BGS Online.</span></span> <span data-ttu-id="599a8-201">Praca z [zespół pomocy technicznej Online Ekspresyjne](mailto:bgsdashboardteam@millwardbrown.com) użytkowników hello tooadd hello Ekspresyjne Online platformy.</span><span class="sxs-lookup"><span data-stu-id="599a8-201">Work with [BGS Online support team](mailto:bgsdashboardteam@millwardbrown.com) tooadd hello users in hello BGS Online platform.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="599a8-202">Przypisanie użytkownika testowego hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="599a8-202">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="599a8-203">W tej sekcji możesz włączyć toouse Simona Britta Azure logowania jednokrotnego za udzielanie dostępu tooBGS w trybie Online.</span><span class="sxs-lookup"><span data-stu-id="599a8-203">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooBGS Online.</span></span>

![Przypisz użytkownika][200] 

<span data-ttu-id="599a8-205">**tooassign tooBGS Simona Britta w trybie Online, wykonaj hello następujące kroki:**</span><span class="sxs-lookup"><span data-stu-id="599a8-205">**tooassign Britta Simon tooBGS Online, perform hello following steps:**</span></span>

1. <span data-ttu-id="599a8-206">W portalu Azure hello, otwórz widok aplikacji hello, a następnie przejdź do widoku katalogu toohello i przejść za**aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="599a8-206">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Przypisz użytkownika][201] 

2. <span data-ttu-id="599a8-208">Z listy aplikacji hello wybierz **Ekspresyjne Online**.</span><span class="sxs-lookup"><span data-stu-id="599a8-208">In hello applications list, select **BGS Online**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-bgsonline-tutorial/tutorial_bgsonline_app.png) 

3. <span data-ttu-id="599a8-210">W menu powitania po lewej stronie powitania kliknij **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="599a8-210">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Przypisz użytkownika][202] 

4. <span data-ttu-id="599a8-212">Kliknij przycisk **Dodaj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="599a8-212">Click **Add** button.</span></span> <span data-ttu-id="599a8-213">Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="599a8-213">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Przypisz użytkownika][203]

5. <span data-ttu-id="599a8-215">Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** hello listy użytkowników.</span><span class="sxs-lookup"><span data-stu-id="599a8-215">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="599a8-216">Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="599a8-216">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="599a8-217">Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="599a8-217">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="599a8-218">Testowanie rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="599a8-218">Testing single sign-on</span></span>

<span data-ttu-id="599a8-219">W tej sekcji można przetestować konfigurację usługi Azure AD z logowania jednokrotnego za pomocą hello panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="599a8-219">In this section, you test your Azure AD SSO configuration using hello Access Panel.</span></span>

<span data-ttu-id="599a8-220">Po kliknięciu kafelka Ekspresyjne Online hello w hello Panel dostępu, należy pobrać aplikacji Online Ekspresyjne tooyour zalogowane automatycznie.</span><span class="sxs-lookup"><span data-stu-id="599a8-220">When you click hello BGS Online tile in hello Access Panel, you should get automatically signed-on tooyour BGS Online application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="599a8-221">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="599a8-221">Additional resources</span></span>

* [<span data-ttu-id="599a8-222">Lista samouczków dotyczących tooIntegrate aplikacji SaaS w usłudze Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="599a8-222">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="599a8-223">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="599a8-223">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-bgsonline-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-bgsonline-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-bgsonline-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-bgsonline-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-bgsonline-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-bgsonline-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-bgsonline-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-bgsonline-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-bgsonline-tutorial/tutorial_general_203.png

