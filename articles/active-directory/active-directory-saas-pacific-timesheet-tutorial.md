---
title: 'Samouczek: Integracji Azure Active Directory z grafik pacyficzny | Dokumentacja firmy Microsoft'
description: "Dowiedz się, jak tooconfigure logowanie jednokrotne między usługą Azure Active Directory i grafik Pacyfiku."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: e546e8ba-821a-4942-9545-c84b0670beab
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/28/2017
ms.author: jeedes
ms.openlocfilehash: 5fd57ff78a3a64c135f2de9895f4643b39e33bb2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-pacific-timesheet"></a><span data-ttu-id="d19ac-103">Samouczek: Integracji Azure Active Directory z grafik i Pacyfik</span><span class="sxs-lookup"><span data-stu-id="d19ac-103">Tutorial: Azure Active Directory integration with Pacific Timesheet</span></span>

<span data-ttu-id="d19ac-104">Z tego samouczka, dowiesz się, jak toointegrate grafiku Pacyfiku w usłudze Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="d19ac-104">In this tutorial, you learn how toointegrate Pacific Timesheet with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="d19ac-105">Integrowanie grafiku Pacyfiku z usługą Azure AD zapewnia hello następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="d19ac-105">Integrating Pacific Timesheet with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="d19ac-106">Można kontrolować w usłudze Azure AD, kto ma dostęp do tooPacific grafiku</span><span class="sxs-lookup"><span data-stu-id="d19ac-106">You can control in Azure AD who has access tooPacific Timesheet</span></span>
- <span data-ttu-id="d19ac-107">Można włączyć użytkownika użytkownicy tooautomatically get zalogowane tooPacific grafiku (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="d19ac-107">You can enable your users tooautomatically get signed-on tooPacific Timesheet (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="d19ac-108">Możesz zarządzać kont w jednej centralnej lokalizacji - hello portalu Azure</span><span class="sxs-lookup"><span data-stu-id="d19ac-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="d19ac-109">Jeśli chcesz tooknow więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="d19ac-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d19ac-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="d19ac-110">Prerequisites</span></span>

<span data-ttu-id="d19ac-111">tooconfigure integracji usługi Azure AD z grafik pacyficzny należy hello następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="d19ac-111">tooconfigure Azure AD integration with Pacific Timesheet, you need hello following items:</span></span>

- <span data-ttu-id="d19ac-112">Subskrypcję usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="d19ac-112">An Azure AD subscription</span></span>
- <span data-ttu-id="d19ac-113">Grafiku pacyficzny logowanie jednokrotne włączone subskrypcji</span><span class="sxs-lookup"><span data-stu-id="d19ac-113">A Pacific Timesheet single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="d19ac-114">tootest hello kroków w tym samouczku, zaleca się przy użyciu środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="d19ac-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="d19ac-115">tootest hello kroki opisane w tym samouczku, należy stosować te zalecenia:</span><span class="sxs-lookup"><span data-stu-id="d19ac-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="d19ac-116">Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="d19ac-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="d19ac-117">Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz pobrać miesięczna wersja próbna [tutaj](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="d19ac-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="d19ac-118">Opis scenariusza</span><span class="sxs-lookup"><span data-stu-id="d19ac-118">Scenario description</span></span>
<span data-ttu-id="d19ac-119">W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym.</span><span class="sxs-lookup"><span data-stu-id="d19ac-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="d19ac-120">Scenariusz Hello opisane w tym samouczku składa się z dwóch głównych elementów:</span><span class="sxs-lookup"><span data-stu-id="d19ac-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="d19ac-121">Dodawanie z galerii hello grafiku i Pacyfik</span><span class="sxs-lookup"><span data-stu-id="d19ac-121">Adding Pacific Timesheet from hello gallery</span></span>
2. <span data-ttu-id="d19ac-122">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="d19ac-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-pacific-timesheet-from-hello-gallery"></a><span data-ttu-id="d19ac-123">Dodawanie z galerii hello grafiku i Pacyfik</span><span class="sxs-lookup"><span data-stu-id="d19ac-123">Adding Pacific Timesheet from hello gallery</span></span>
<span data-ttu-id="d19ac-124">tooconfigure hello integracji grafiku Pacyfiku w usłudze Azure Active Directory, należy tooadd grafiku Pacyfiku z hello galerii tooyour listę zarządzanych aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="d19ac-124">tooconfigure hello integration of Pacific Timesheet into Azure AD, you need tooadd Pacific Timesheet from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="d19ac-125">**tooadd grafiku Pacyfiku z galerii hello wykonaj hello następujące kroki:**</span><span class="sxs-lookup"><span data-stu-id="d19ac-125">**tooadd Pacific Timesheet from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="d19ac-126">W hello  **[portalu Azure](https://portal.azure.com)**na temat hello panelu nawigacji po lewej stronie, kliknij przycisk **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="d19ac-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Usługa Active Directory][1]

2. <span data-ttu-id="d19ac-128">Przejdź za**aplikacje dla przedsiębiorstw**.</span><span class="sxs-lookup"><span data-stu-id="d19ac-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="d19ac-129">Następnie przejdź zbyt**wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="d19ac-129">Then go too**All applications**.</span></span>

    ![Aplikacje][2]
    
3. <span data-ttu-id="d19ac-131">tooadd nową aplikację, kliknij przycisk **nowej aplikacji** przycisk u góry hello okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="d19ac-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplikacje][3]

4. <span data-ttu-id="d19ac-133">W polu wyszukiwania hello wpisz **grafiku pacyficzny**.</span><span class="sxs-lookup"><span data-stu-id="d19ac-133">In hello search box, type **Pacific Timesheet**.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-pacific-timesheet-tutorial/tutorial_pacifictimesheet_search.png)

5. <span data-ttu-id="d19ac-135">W panelu wyników hello, wybierz **grafiku pacyficzny**, a następnie kliknij przycisk **Dodaj** przycisk aplikacji hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="d19ac-135">In hello results panel, select **Pacific Timesheet**, and then click **Add** button tooadd hello application.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-pacific-timesheet-tutorial/tutorial_pacifictimesheet_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="d19ac-137">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="d19ac-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="d19ac-138">W tej sekcji skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z grafik Pacyfiku w oparciu o nazwie "Britta Simona" użytkownika testowego.</span><span class="sxs-lookup"><span data-stu-id="d19ac-138">In this section, you configure and test Azure AD single sign-on with Pacific Timesheet based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="d19ac-139">Dla pojedynczego logowania jednokrotnego toowork usługi Azure AD musi tooknow użytkownika odpowiednikiem hello w grafiku pacyficzny jest tooa użytkownika w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="d19ac-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Pacific Timesheet is tooa user in Azure AD.</span></span> <span data-ttu-id="d19ac-140">Innymi słowy relację łącza między użytkownika usługi Azure AD i hello użytkownikowi w grafiku pacyficzny musi toobe ustanowione.</span><span class="sxs-lookup"><span data-stu-id="d19ac-140">In other words, a link relationship between an Azure AD user and hello related user in Pacific Timesheet needs toobe established.</span></span>

<span data-ttu-id="d19ac-141">W grafiku pacyficzny przypisać wartość hello hello **nazwy użytkownika** w usłudze Azure AD jako wartość hello hello **Username** tooestablish hello łącze relacji.</span><span class="sxs-lookup"><span data-stu-id="d19ac-141">In Pacific Timesheet, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="d19ac-142">tooconfigure i test usługi Azure AD rejestracji jednokrotnej z grafik pacyficzny należy hello toocomplete po bloków konstrukcyjnych:</span><span class="sxs-lookup"><span data-stu-id="d19ac-142">tooconfigure and test Azure AD single sign-on with Pacific Timesheet, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="d19ac-143">**[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configuring-azure-ad-single-sign-on)**  -tooenable Twojego toouse użytkowników tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="d19ac-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="d19ac-144">**[Tworzenie użytkownika testowego usługi Azure AD](#creating-an-azure-ad-test-user)**  -tootest usługi Azure AD rejestracji jednokrotnej z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="d19ac-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="d19ac-145">**[Tworzenie użytkownika testowego i Pacyfik grafiku](#creating-a-pacific-timesheet-test-user)**  -toohave odpowiednikiem Simona Britta w grafiku Pacyfiku, który jest połączony toohello usługi Azure AD reprezentację użytkownika.</span><span class="sxs-lookup"><span data-stu-id="d19ac-145">**[Creating a Pacific Timesheet test user](#creating-a-pacific-timesheet-test-user)** - toohave a counterpart of Britta Simon in Pacific Timesheet that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="d19ac-146">**[Przypisanie użytkownika testowego hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Simona Britta toouse usługi Azure AD rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="d19ac-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="d19ac-147">**[Testowanie rejestracji jednokrotnej](#testing-single-sign-on)**  -tooverify czy hello konfiguracji działania.</span><span class="sxs-lookup"><span data-stu-id="d19ac-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="d19ac-148">Konfigurowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="d19ac-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="d19ac-149">W tej sekcji włączyć usługi Azure AD rejestracji jednokrotnej w hello portalu Azure i skonfigurować logowanie jednokrotne w aplikacji grafiku Pacyfiku.</span><span class="sxs-lookup"><span data-stu-id="d19ac-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Pacific Timesheet application.</span></span>

<span data-ttu-id="d19ac-150">**tooconfigure usługi Azure AD rejestracji jednokrotnej z grafik pacyficzny wykonaj hello następujące kroki:**</span><span class="sxs-lookup"><span data-stu-id="d19ac-150">**tooconfigure Azure AD single sign-on with Pacific Timesheet, perform hello following steps:**</span></span>

1. <span data-ttu-id="d19ac-151">W portalu Azure na powitania hello **grafiku pacyficzny** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.</span><span class="sxs-lookup"><span data-stu-id="d19ac-151">In hello Azure portal, on hello **Pacific Timesheet** application integration page, click **Single sign-on**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej][4]

2. <span data-ttu-id="d19ac-153">Na powitania **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** tooenable rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="d19ac-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-pacific-timesheet-tutorial/tutorial_pacifictimesheet_samlbase.png)

3. <span data-ttu-id="d19ac-155">Na powitania **pacyficzny grafiku domeny i adres URL** sekcji, wykonaj następujące kroki hello:</span><span class="sxs-lookup"><span data-stu-id="d19ac-155">On hello **Pacific Timesheet Domain and URLs** section, perform hello following steps:</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-pacific-timesheet-tutorial/tutorial_pacifictimesheet_url.png)

    <span data-ttu-id="d19ac-157">a.</span><span class="sxs-lookup"><span data-stu-id="d19ac-157">a.</span></span> <span data-ttu-id="d19ac-158">W hello **identyfikator** tekstowym, wpisz adres URL za pomocą hello następującego wzorca:`https://<InstanceID>.pacifictimesheet.com/timesheet/home.do`</span><span class="sxs-lookup"><span data-stu-id="d19ac-158">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<InstanceID>.pacifictimesheet.com/timesheet/home.do`</span></span>

    <span data-ttu-id="d19ac-159">b.</span><span class="sxs-lookup"><span data-stu-id="d19ac-159">b.</span></span> <span data-ttu-id="d19ac-160">W hello **adres URL odpowiedzi** tekstowym, wpisz adres URL za pomocą hello następującego wzorca:`https://<InstanceID>.pacifictimesheet.com/timesheet/home.do`</span><span class="sxs-lookup"><span data-stu-id="d19ac-160">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://<InstanceID>.pacifictimesheet.com/timesheet/home.do`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="d19ac-161">Wartości te nie są prawdziwe.</span><span class="sxs-lookup"><span data-stu-id="d19ac-161">These values are not real.</span></span> <span data-ttu-id="d19ac-162">Witaj rzeczywisty identyfikator i odpowiedzi adresu URL, należy zaktualizować te wartości.</span><span class="sxs-lookup"><span data-stu-id="d19ac-162">Update these values with hello actual Identifier and Reply URL.</span></span> <span data-ttu-id="d19ac-163">Skontaktuj się z [zespołem pomocy technicznej grafiku pacyficzny](http://www.pacifictimesheet.com/support) tooget tych wartości.</span><span class="sxs-lookup"><span data-stu-id="d19ac-163">Contact [Pacific Timesheet support team](http://www.pacifictimesheet.com/support) tooget these values.</span></span>
 
4. <span data-ttu-id="d19ac-164">Na powitania **certyfikat podpisywania SAML** kliknij **certyfikatu (Base64)** , a następnie zapisz plik certyfikatu hello na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="d19ac-164">On hello **SAML Signing Certificate** section, click **Certificate (Base64)** and then save hello certificate file on your computer.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-pacific-timesheet-tutorial/tutorial_pacifictimesheet_certificate.png) 

5. <span data-ttu-id="d19ac-166">Kliknij przycisk **zapisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="d19ac-166">Click **Save** button.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-pacific-timesheet-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="d19ac-168">Na powitania **konfiguracji grafiku Pacyfiku** kliknij pozycję **skonfigurować grafiku Pacyfiku** tooopen **Konfigurowanie logowania jednokrotnego** okna.</span><span class="sxs-lookup"><span data-stu-id="d19ac-168">On hello **Pacific Timesheet Configuration** section, click **Configure Pacific Timesheet** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="d19ac-169">Kopiuj hello **identyfikator jednostki SAML i SAML pojedynczy znak na adres URL usługi** z hello **sekcji krótkimi opisami.**</span><span class="sxs-lookup"><span data-stu-id="d19ac-169">Copy hello **SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-pacific-timesheet-tutorial/tutorial_pacifictimesheet_configure.png) 

7. <span data-ttu-id="d19ac-171">tooconfigure rejestracji jednokrotnej w **grafiku pacyficzny** strony, należy pobrać hello toosend **certyfikatu (Base64)**, **SAML pojedynczy znak na adres URL usługi**i  **Identyfikator jednostki SAML** za[zespołem pomocy technicznej grafiku pacyficzny](http://www.pacifictimesheet.com/support).</span><span class="sxs-lookup"><span data-stu-id="d19ac-171">tooconfigure single sign-on on **Pacific Timesheet** side, you need toosend hello downloaded **Certificate (Base64)**, **SAML Single Sign-On Service URL**, and **SAML Entity ID** too[Pacific Timesheet support team](http://www.pacifictimesheet.com/support).</span></span> <span data-ttu-id="d19ac-172">To ustawienie toohave hello prawidłowo po obu stronach połączenia logowania jednokrotnego SAML one ustawić.</span><span class="sxs-lookup"><span data-stu-id="d19ac-172">They set this setting toohave hello SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="d19ac-173">Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz hello [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji hello!</span><span class="sxs-lookup"><span data-stu-id="d19ac-173">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="d19ac-174">Po dodaniu tej aplikacji z hello **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij hello **rejestracji jednokrotnej** hello kartę i dostępu do osadzonych dokumentacji za pośrednictwem hello  **Konfiguracja** sekcji u dołu hello.</span><span class="sxs-lookup"><span data-stu-id="d19ac-174">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="d19ac-175">Więcej o hello osadzonych dokumentacji funkcji w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="d19ac-175">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="d19ac-176">Tworzenie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="d19ac-176">Creating an Azure AD test user</span></span>
<span data-ttu-id="d19ac-177">Celem Hello w tej sekcji jest toocreate użytkownika testowego, w portalu Azure o nazwie Simona Britta hello.</span><span class="sxs-lookup"><span data-stu-id="d19ac-177">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Tworzenie użytkowników usługi Azure AD][100]

<span data-ttu-id="d19ac-179">**toocreate użytkownika testowego w usłudze Azure AD, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="d19ac-179">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="d19ac-180">W hello **portalu Azure**na temat hello w lewym okienku nawigacji, kliknij przycisk **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="d19ac-180">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-pacific-timesheet-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="d19ac-182">toodisplay hello listę użytkowników, przejdź zbyt**użytkowników i grup** i kliknij przycisk **wszyscy użytkownicy**.</span><span class="sxs-lookup"><span data-stu-id="d19ac-182">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-pacific-timesheet-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="d19ac-184">Witaj tooopen **użytkownika** okna dialogowego, kliknij przycisk **Dodaj** u góry hello hello okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="d19ac-184">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-pacific-timesheet-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="d19ac-186">Na powitania **użytkownika** okna dialogowego wykonaj hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="d19ac-186">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-pacific-timesheet-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="d19ac-188">a.</span><span class="sxs-lookup"><span data-stu-id="d19ac-188">a.</span></span> <span data-ttu-id="d19ac-189">W hello **nazwa** pole tekstowe, typ **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="d19ac-189">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="d19ac-190">b.</span><span class="sxs-lookup"><span data-stu-id="d19ac-190">b.</span></span> <span data-ttu-id="d19ac-191">W hello **nazwy użytkownika** pole tekstowe, hello typu **adres e-mail** z BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="d19ac-191">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="d19ac-192">c.</span><span class="sxs-lookup"><span data-stu-id="d19ac-192">c.</span></span> <span data-ttu-id="d19ac-193">Wybierz **Pokaż hasło** i zanotuj wartość hello hello **hasło**.</span><span class="sxs-lookup"><span data-stu-id="d19ac-193">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="d19ac-194">d.</span><span class="sxs-lookup"><span data-stu-id="d19ac-194">d.</span></span> <span data-ttu-id="d19ac-195">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="d19ac-195">Click **Create**.</span></span>
 
### <a name="creating-a-pacific-timesheet-test-user"></a><span data-ttu-id="d19ac-196">Tworzenie użytkownika testowego grafiku i Pacyfik</span><span class="sxs-lookup"><span data-stu-id="d19ac-196">Creating a Pacific Timesheet test user</span></span>

<span data-ttu-id="d19ac-197">W tej sekcji utworzysz użytkownika o nazwie Simona Britta w grafiku Pacyfiku.</span><span class="sxs-lookup"><span data-stu-id="d19ac-197">In this section, you create a user called Britta Simon in Pacific Timesheet.</span></span> <span data-ttu-id="d19ac-198">Praca z [zespołem pomocy technicznej grafiku pacyficzny](http://www.pacifictimesheet.com/support) toocreate użytkownika w aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="d19ac-198">Work with [Pacific Timesheet support team](http://www.pacifictimesheet.com/support) toocreate a user in hello application.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="d19ac-199">Przypisanie użytkownika testowego hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="d19ac-199">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="d19ac-200">W tej sekcji możesz włączyć toouse Simona Britta Azure logowania jednokrotnego za udzielanie dostępu tooPacific grafiku.</span><span class="sxs-lookup"><span data-stu-id="d19ac-200">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooPacific Timesheet.</span></span>

![Przypisz użytkownika][200] 

<span data-ttu-id="d19ac-202">**tooassign tooPacific Simona Britta grafik, wykonaj hello następujące kroki:**</span><span class="sxs-lookup"><span data-stu-id="d19ac-202">**tooassign Britta Simon tooPacific Timesheet, perform hello following steps:**</span></span>

1. <span data-ttu-id="d19ac-203">W portalu Azure hello, otwórz widok aplikacji hello, a następnie przejdź do widoku katalogu toohello i przejść za**aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="d19ac-203">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Przypisz użytkownika][201] 

2. <span data-ttu-id="d19ac-205">Z listy aplikacji hello wybierz **grafiku pacyficzny**.</span><span class="sxs-lookup"><span data-stu-id="d19ac-205">In hello applications list, select **Pacific Timesheet**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-pacific-timesheet-tutorial/tutorial_pacifictimesheet_app.png) 

3. <span data-ttu-id="d19ac-207">W menu powitania po lewej stronie powitania kliknij **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="d19ac-207">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Przypisz użytkownika][202] 

4. <span data-ttu-id="d19ac-209">Kliknij przycisk **Dodaj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="d19ac-209">Click **Add** button.</span></span> <span data-ttu-id="d19ac-210">Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="d19ac-210">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Przypisz użytkownika][203]

5. <span data-ttu-id="d19ac-212">Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** hello listy użytkowników.</span><span class="sxs-lookup"><span data-stu-id="d19ac-212">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="d19ac-213">Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="d19ac-213">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="d19ac-214">Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="d19ac-214">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="d19ac-215">Testowanie rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="d19ac-215">Testing single sign-on</span></span>

<span data-ttu-id="d19ac-216">Celem Hello w tej sekcji jest tootest użyciu usługi Azure AD konfiguracji rejestracji jednokrotnej hello panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="d19ac-216">hello objective of this section is tootest your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="d19ac-217">Po kliknięciu kafelka grafiku pacyficzny hello w hello panelu dostępu, należy pobrać aplikację grafiku pacyficzny tooyour zalogowane automatycznie.</span><span class="sxs-lookup"><span data-stu-id="d19ac-217">When you click hello Pacific Timesheet tile in hello Access Panel, you should get automatically signed-on tooyour Pacific Timesheet application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="d19ac-218">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="d19ac-218">Additional resources</span></span>

* [<span data-ttu-id="d19ac-219">Lista samouczków dotyczących tooIntegrate aplikacji SaaS w usłudze Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="d19ac-219">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="d19ac-220">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="d19ac-220">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-pacific-timesheet-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-pacific-timesheet-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-pacific-timesheet-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-pacific-timesheet-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-pacific-timesheet-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-pacific-timesheet-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-pacific-timesheet-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-pacific-timesheet-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-pacific-timesheet-tutorial/tutorial_general_203.png

