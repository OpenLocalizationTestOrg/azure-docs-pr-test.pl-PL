---
title: 'Samouczek: Integracji Azure Active Directory z Agile analiz biznesowych Birst | Dokumentacja firmy Microsoft'
description: "Dowiedz się, jak tooconfigure logowanie jednokrotne między usługą Azure Active Directory i Birst Agile analiz biznesowych."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 677183b1-5348-4302-88cc-5c8ab63a3c6c
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/09/2017
ms.author: jeedes
ms.openlocfilehash: f007edcec0fb8ece215ab69f7ec7ca59ca34bddc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-birst-agile-business-analytics"></a><span data-ttu-id="eb41a-103">Samouczek: Integracji Azure Active Directory z Birst Agile analiz biznesowych</span><span class="sxs-lookup"><span data-stu-id="eb41a-103">Tutorial: Azure Active Directory integration with Birst Agile Business Analytics</span></span>

<span data-ttu-id="eb41a-104">Z tego samouczka, dowiesz się, jak toointegrate Birst Agile analiz biznesowych w usłudze Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="eb41a-104">In this tutorial, you learn how toointegrate Birst Agile Business Analytics with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="eb41a-105">Integrowanie Birst Agile analiz biznesowych z usługą Azure AD zapewnia hello następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="eb41a-105">Integrating Birst Agile Business Analytics with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="eb41a-106">Można kontrolować w usłudze Azure AD, kto ma dostęp tooBirst Agile analiz biznesowych</span><span class="sxs-lookup"><span data-stu-id="eb41a-106">You can control in Azure AD who has access tooBirst Agile Business Analytics</span></span>
- <span data-ttu-id="eb41a-107">Można włączyć użytkownika użytkownicy tooautomatically get zalogowane tooBirst Agile analiz biznesowych (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="eb41a-107">You can enable your users tooautomatically get signed-on tooBirst Agile Business Analytics (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="eb41a-108">Możesz zarządzać kont w jednej centralnej lokalizacji - hello portalu Azure</span><span class="sxs-lookup"><span data-stu-id="eb41a-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="eb41a-109">Jeśli chcesz tooknow więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="eb41a-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="eb41a-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="eb41a-110">Prerequisites</span></span>

<span data-ttu-id="eb41a-111">tooconfigure integracji usługi Azure AD z Birst Agile analiz biznesowych, należy hello następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="eb41a-111">tooconfigure Azure AD integration with Birst Agile Business Analytics, you need hello following items:</span></span>

- <span data-ttu-id="eb41a-112">Subskrypcję usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="eb41a-112">An Azure AD subscription</span></span>
- <span data-ttu-id="eb41a-113">Elastyczne analiz biznesowych Birst jednokrotnego włączone subskrypcji</span><span class="sxs-lookup"><span data-stu-id="eb41a-113">A Birst Agile Business Analytics single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="eb41a-114">tootest hello kroków w tym samouczku, zaleca się przy użyciu środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="eb41a-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="eb41a-115">tootest hello kroki opisane w tym samouczku, należy stosować te zalecenia:</span><span class="sxs-lookup"><span data-stu-id="eb41a-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="eb41a-116">Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="eb41a-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="eb41a-117">Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz pobrać miesięczna wersja próbna [tutaj](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="eb41a-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="eb41a-118">Opis scenariusza</span><span class="sxs-lookup"><span data-stu-id="eb41a-118">Scenario description</span></span>
<span data-ttu-id="eb41a-119">W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym.</span><span class="sxs-lookup"><span data-stu-id="eb41a-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="eb41a-120">Scenariusz Hello opisane w tym samouczku składa się z dwóch głównych elementów:</span><span class="sxs-lookup"><span data-stu-id="eb41a-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="eb41a-121">Dodawanie Birst Agile analiz biznesowych z galerii hello</span><span class="sxs-lookup"><span data-stu-id="eb41a-121">Adding Birst Agile Business Analytics from hello gallery</span></span>
2. <span data-ttu-id="eb41a-122">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="eb41a-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-birst-agile-business-analytics-from-hello-gallery"></a><span data-ttu-id="eb41a-123">Dodawanie Birst Agile analiz biznesowych z galerii hello</span><span class="sxs-lookup"><span data-stu-id="eb41a-123">Adding Birst Agile Business Analytics from hello gallery</span></span>
<span data-ttu-id="eb41a-124">tooconfigure hello integracji Birst Agile analiz biznesowych do usługi Azure AD, należy tooadd Birst Agile analiz biznesowych z hello galerii tooyour listę zarządzanych aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="eb41a-124">tooconfigure hello integration of Birst Agile Business Analytics into Azure AD, you need tooadd Birst Agile Business Analytics from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="eb41a-125">**tooadd Birst Agile analiz biznesowych z galerii hello wykonaj hello następujące kroki:**</span><span class="sxs-lookup"><span data-stu-id="eb41a-125">**tooadd Birst Agile Business Analytics from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="eb41a-126">W hello  **[portalu Azure](https://portal.azure.com)**na temat hello panelu nawigacji po lewej stronie, kliknij przycisk **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="eb41a-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Usługa Active Directory][1]

2. <span data-ttu-id="eb41a-128">Przejdź za**aplikacje dla przedsiębiorstw**.</span><span class="sxs-lookup"><span data-stu-id="eb41a-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="eb41a-129">Następnie przejdź zbyt**wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="eb41a-129">Then go too**All applications**.</span></span>

    ![Aplikacje][2]
    
3. <span data-ttu-id="eb41a-131">tooadd nową aplikację, kliknij przycisk **nowej aplikacji** przycisk u góry hello okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="eb41a-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplikacje][3]

4. <span data-ttu-id="eb41a-133">W polu wyszukiwania hello wpisz **Birst Agile analiz biznesowych**.</span><span class="sxs-lookup"><span data-stu-id="eb41a-133">In hello search box, type **Birst Agile Business Analytics**.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-birst-tutorial/tutorial_birst_search.png)

5. <span data-ttu-id="eb41a-135">W panelu wyników hello, wybierz **Birst Agile analiz biznesowych**, a następnie kliknij przycisk **Dodaj** przycisk aplikacji hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="eb41a-135">In hello results panel, select **Birst Agile Business Analytics**, and then click **Add** button tooadd hello application.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-birst-tutorial/tutorial_birst_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="eb41a-137">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="eb41a-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="eb41a-138">W tej sekcji możesz skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z Birst Agile analiz biznesowych na podstawie użytkownika testowego, nazywany "Britta Simona".</span><span class="sxs-lookup"><span data-stu-id="eb41a-138">In this section, you configure and test Azure AD single sign-on with Birst Agile Business Analytics based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="eb41a-139">Dla pojedynczego logowania jednokrotnego toowork usługi Azure AD musi tooknow użytkownika odpowiednikiem hello w Birst Agile analiz biznesowych jest tooa użytkownika w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="eb41a-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Birst Agile Business Analytics is tooa user in Azure AD.</span></span> <span data-ttu-id="eb41a-140">Innymi słowy relację łącza między użytkownika usługi Azure AD i hello użytkownikowi w Birst Agile analiz biznesowych musi toobe ustanowione.</span><span class="sxs-lookup"><span data-stu-id="eb41a-140">In other words, a link relationship between an Azure AD user and hello related user in Birst Agile Business Analytics needs toobe established.</span></span>

<span data-ttu-id="eb41a-141">W Birst Agile analiz biznesowych, należy przypisać wartość hello hello **nazwy użytkownika** w usłudze Azure AD jako wartość hello hello **Username** tooestablish hello łącze relacji.</span><span class="sxs-lookup"><span data-stu-id="eb41a-141">In Birst Agile Business Analytics, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="eb41a-142">tooconfigure i testowych usługi Azure AD rejestracji jednokrotnej z Birst Agile analiz biznesowych, należy po bloków konstrukcyjnych hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="eb41a-142">tooconfigure and test Azure AD single sign-on with Birst Agile Business Analytics, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="eb41a-143">**[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configuring-azure-ad-single-sign-on)**  -tooenable Twojego toouse użytkowników tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="eb41a-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="eb41a-144">**[Tworzenie użytkownika testowego usługi Azure AD](#creating-an-azure-ad-test-user)**  -tootest usługi Azure AD rejestracji jednokrotnej z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="eb41a-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="eb41a-145">**[Tworzenie użytkownika testowego analiz biznesowych Agile Birst](#creating-a-birst-agile-business-analytics-test-user)**  -toohave odpowiednikiem Simona Britta w Birst Agile analiz biznesowych, który jest odpowiednikiem połączonych toohello usługi Azure AD użytkownika.</span><span class="sxs-lookup"><span data-stu-id="eb41a-145">**[Creating a Birst Agile Business Analytics test user](#creating-a-birst-agile-business-analytics-test-user)** - toohave a counterpart of Britta Simon in Birst Agile Business Analytics that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="eb41a-146">**[Przypisanie użytkownika testowego hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Simona Britta toouse usługi Azure AD rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="eb41a-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="eb41a-147">**[Testowanie rejestracji jednokrotnej](#testing-single-sign-on)**  -tooverify czy hello konfiguracji działania.</span><span class="sxs-lookup"><span data-stu-id="eb41a-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="eb41a-148">Konfigurowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="eb41a-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="eb41a-149">W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w portalu Azure hello i skonfigurować logowanie jednokrotne w aplikacji Birst Agile analiz biznesowych.</span><span class="sxs-lookup"><span data-stu-id="eb41a-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Birst Agile Business Analytics application.</span></span>

<span data-ttu-id="eb41a-150">**tooconfigure usługi Azure AD rejestracji jednokrotnej z Birst Agile analiz biznesowych, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="eb41a-150">**tooconfigure Azure AD single sign-on with Birst Agile Business Analytics, perform hello following steps:**</span></span>

1. <span data-ttu-id="eb41a-151">W portalu Azure na powitania hello **Birst Agile analiz biznesowych** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.</span><span class="sxs-lookup"><span data-stu-id="eb41a-151">In hello Azure portal, on hello **Birst Agile Business Analytics** application integration page, click **Single sign-on**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej][4]

2. <span data-ttu-id="eb41a-153">Na powitania **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** tooenable rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="eb41a-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-birst-tutorial/tutorial_birst_samlbase.png)

3. <span data-ttu-id="eb41a-155">Na powitania **Birst Agile domeny analizy biznesowej i adres URL** sekcji, wykonaj następujące kroki hello:</span><span class="sxs-lookup"><span data-stu-id="eb41a-155">On hello **Birst Agile Business Analytics Domain and URLs** section, perform hello following steps:</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-birst-tutorial/tutorial_birst_url.png)

     <span data-ttu-id="eb41a-157">W hello **adres URL logowania** tekstowym, wpisz adres URL za pomocą hello następującego wzorca:`https://login.bws.birst.com/SAMLSSO/Services.aspx?birst.idpid=TENANTIDPID`</span><span class="sxs-lookup"><span data-stu-id="eb41a-157">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://login.bws.birst.com/SAMLSSO/Services.aspx?birst.idpid=TENANTIDPID`</span></span>

     <span data-ttu-id="eb41a-158">adres URL Hello jest zależna od hello centrum danych znajduje się konto Birst:</span><span class="sxs-lookup"><span data-stu-id="eb41a-158">hello URL depends on hello datacenter that your Birst account is located:</span></span> 

     * <span data-ttu-id="eb41a-159">Do użytku w USA datacenter następującego wzorca hello:`https://login.bws.birst.com/SAMLSSO/Services.aspx?birst.idpid=TENANTIDPID`</span><span class="sxs-lookup"><span data-stu-id="eb41a-159">For US datacenter use following hello pattern: `https://login.bws.birst.com/SAMLSSO/Services.aspx?birst.idpid=TENANTIDPID`</span></span> 

     * <span data-ttu-id="eb41a-160">Dla Europy centrum danych, użyj następującego wzorca hello:`https://login.eu1.birst.com/SAMLSSO/Services.aspx?birst.idpid=TENANTIDPID`</span><span class="sxs-lookup"><span data-stu-id="eb41a-160">For Europe datacenter use hello following pattern: `https://login.eu1.birst.com/SAMLSSO/Services.aspx?birst.idpid=TENANTIDPID`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="eb41a-161">Ta wartość nie jest prawdziwe.</span><span class="sxs-lookup"><span data-stu-id="eb41a-161">This value is not real.</span></span> <span data-ttu-id="eb41a-162">Wartość hello aktualizacji z hello rzeczywisty adres URL logowania.</span><span class="sxs-lookup"><span data-stu-id="eb41a-162">Update hello value with hello actual Sign-On URL.</span></span> <span data-ttu-id="eb41a-163">Skontaktuj się z [zespołem pomocy technicznej klienta analizy biznesowej Agile Birst](mailto:info@birst.com) tooget hello wartość.</span><span class="sxs-lookup"><span data-stu-id="eb41a-163">Contact [Birst Agile Business Analytics Client support team](mailto:info@birst.com) tooget hello value.</span></span> 
 
4. <span data-ttu-id="eb41a-164">Na powitania **certyfikat podpisywania SAML** kliknij **certyfikatu (Base64)** , a następnie zapisz plik certyfikatu hello na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="eb41a-164">On hello **SAML Signing Certificate** section, click **Certificate (Base64)** and then save hello certificate file on your computer.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-birst-tutorial/tutorial_birst_certificate.png) 

5. <span data-ttu-id="eb41a-166">Kliknij przycisk **zapisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="eb41a-166">Click **Save** button.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-birst-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="eb41a-168">Na powitania **Birst Agile konfiguracji analizy biznesowej** kliknij **skonfigurować Birst Agile analiz biznesowych** tooopen **Konfigurowanie logowania jednokrotnego** okna.</span><span class="sxs-lookup"><span data-stu-id="eb41a-168">On hello **Birst Agile Business Analytics Configuration** section, click **Configure Birst Agile Business Analytics** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="eb41a-169">Kopiuj hello **Sign-Out adres URL, identyfikator jednostki SAML i SAML pojedynczy znak na adres URL usługi** z hello **sekcji krótkimi opisami.**</span><span class="sxs-lookup"><span data-stu-id="eb41a-169">Copy hello **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-birst-tutorial/tutorial_birst_configure.png) 

7. <span data-ttu-id="eb41a-171">tooconfigure rejestracji jednokrotnej w **Birst Agile analiz biznesowych** strony, należy pobrać hello toosend **certyfikatu (Base64)**, **Sign-Out adres URL, identyfikator jednostki SAML i SAML logowania jednokrotnego Adres URL usługi** za[Birst Agile analiz biznesowych obsługuje zespołu](mailto:info@birst.com).</span><span class="sxs-lookup"><span data-stu-id="eb41a-171">tooconfigure single sign-on on **Birst Agile Business Analytics** side, you need toosend hello downloaded **Certificate (Base64)**, **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** too[Birst Agile Business Analytics support team](mailto:info@birst.com).</span></span> 

    > [!NOTE]
    > <span data-ttu-id="eb41a-172">Wspomina zespołu tooBirst, że ta integracja wymaga algorytm SHA256 (SHA1 nie będzie obsługiwana) tak, aby ich ustawiona hello logowania jednokrotnego na powitania odpowiedniego serwera, takich jak **app2101** itp.</span><span class="sxs-lookup"><span data-stu-id="eb41a-172">Mention tooBirst team that this integration needs SHA256 Algorithm (SHA1 will not be supported) so that they can set hello SSO on hello appropriate server like **app2101** etc.</span></span>
  

> [!TIP]
> <span data-ttu-id="eb41a-173">Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz hello [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji hello!</span><span class="sxs-lookup"><span data-stu-id="eb41a-173">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="eb41a-174">Po dodaniu tej aplikacji z hello **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij hello **rejestracji jednokrotnej** hello kartę i dostępu do osadzonych dokumentacji za pośrednictwem hello  **Konfiguracja** sekcji u dołu hello.</span><span class="sxs-lookup"><span data-stu-id="eb41a-174">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="eb41a-175">Więcej o hello osadzonych dokumentacji funkcji w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="eb41a-175">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="eb41a-176">Tworzenie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="eb41a-176">Creating an Azure AD test user</span></span>
<span data-ttu-id="eb41a-177">Celem Hello w tej sekcji jest toocreate użytkownika testowego, w portalu Azure o nazwie Simona Britta hello.</span><span class="sxs-lookup"><span data-stu-id="eb41a-177">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Tworzenie użytkowników usługi Azure AD][100]

<span data-ttu-id="eb41a-179">**toocreate użytkownika testowego w usłudze Azure AD, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="eb41a-179">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="eb41a-180">W hello **portalu Azure**na temat hello w lewym okienku nawigacji, kliknij przycisk **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="eb41a-180">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-birst-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="eb41a-182">toodisplay hello listę użytkowników, przejdź zbyt**użytkowników i grup** i kliknij przycisk **wszyscy użytkownicy**.</span><span class="sxs-lookup"><span data-stu-id="eb41a-182">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-birst-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="eb41a-184">Witaj tooopen **użytkownika** okna dialogowego, kliknij przycisk **Dodaj** u góry hello hello okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="eb41a-184">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-birst-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="eb41a-186">Na powitania **użytkownika** okna dialogowego wykonaj hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="eb41a-186">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-birst-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="eb41a-188">a.</span><span class="sxs-lookup"><span data-stu-id="eb41a-188">a.</span></span> <span data-ttu-id="eb41a-189">W hello **nazwa** pole tekstowe, typ **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="eb41a-189">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="eb41a-190">b.</span><span class="sxs-lookup"><span data-stu-id="eb41a-190">b.</span></span> <span data-ttu-id="eb41a-191">W hello **nazwy użytkownika** pole tekstowe, hello typu **adres e-mail** z BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="eb41a-191">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="eb41a-192">c.</span><span class="sxs-lookup"><span data-stu-id="eb41a-192">c.</span></span> <span data-ttu-id="eb41a-193">Wybierz **Pokaż hasło** i zanotuj wartość hello hello **hasło**.</span><span class="sxs-lookup"><span data-stu-id="eb41a-193">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="eb41a-194">d.</span><span class="sxs-lookup"><span data-stu-id="eb41a-194">d.</span></span> <span data-ttu-id="eb41a-195">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="eb41a-195">Click **Create**.</span></span>
 
### <a name="creating-a-birst-agile-business-analytics-test-user"></a><span data-ttu-id="eb41a-196">Tworzenie użytkownika testowego Birst Agile analityka biznesowa</span><span class="sxs-lookup"><span data-stu-id="eb41a-196">Creating a Birst Agile Business Analytics test user</span></span>

<span data-ttu-id="eb41a-197">Celem Hello w tej sekcji jest toocreate użytkownika o nazwie Simona Britta w Birst Agile analiz biznesowych.</span><span class="sxs-lookup"><span data-stu-id="eb41a-197">hello objective of this section is toocreate a user called Britta Simon in Birst Agile Business Analytics.</span></span> <span data-ttu-id="eb41a-198">Praca z [Birst Agile analiz biznesowych obsługuje zespołu](mailto:info@birst.com) tooadd hello użytkowników w hello Birst konta.</span><span class="sxs-lookup"><span data-stu-id="eb41a-198">Work with [Birst Agile Business Analytics support team](mailto:info@birst.com) tooadd hello users in hello Birst account.</span></span> 

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="eb41a-199">Przypisanie użytkownika testowego hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="eb41a-199">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="eb41a-200">W tej sekcji możesz włączyć toouse Simona Britta Azure logowania jednokrotnego za udzielanie dostępu tooBirst Agile analiz biznesowych.</span><span class="sxs-lookup"><span data-stu-id="eb41a-200">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooBirst Agile Business Analytics.</span></span>

![Przypisz użytkownika][200] 

<span data-ttu-id="eb41a-202">**tooassign tooBirst Simona Britta Agile analiz biznesowych, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="eb41a-202">**tooassign Britta Simon tooBirst Agile Business Analytics, perform hello following steps:**</span></span>

1. <span data-ttu-id="eb41a-203">W portalu Azure hello, otwórz widok aplikacji hello, a następnie przejdź do widoku katalogu toohello i przejść za**aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="eb41a-203">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Przypisz użytkownika][201] 

2. <span data-ttu-id="eb41a-205">Z listy aplikacji hello wybierz **Birst Agile analiz biznesowych**.</span><span class="sxs-lookup"><span data-stu-id="eb41a-205">In hello applications list, select **Birst Agile Business Analytics**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-birst-tutorial/tutorial_birst_app.png) 

3. <span data-ttu-id="eb41a-207">W menu powitania po lewej stronie powitania kliknij **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="eb41a-207">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Przypisz użytkownika][202] 

4. <span data-ttu-id="eb41a-209">Kliknij przycisk **Dodaj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="eb41a-209">Click **Add** button.</span></span> <span data-ttu-id="eb41a-210">Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="eb41a-210">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Przypisz użytkownika][203]

5. <span data-ttu-id="eb41a-212">Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** hello listy użytkowników.</span><span class="sxs-lookup"><span data-stu-id="eb41a-212">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="eb41a-213">Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="eb41a-213">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="eb41a-214">Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="eb41a-214">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="eb41a-215">Testowanie rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="eb41a-215">Testing single sign-on</span></span>

<span data-ttu-id="eb41a-216">Celem Hello w tej sekcji jest tootest programu Azure AD SSO konfiguracji przy użyciu hello panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="eb41a-216">hello objective of this section is tootest your Azure AD SSO configuration using hello Access Panel.</span></span>

<span data-ttu-id="eb41a-217">Po kliknięciu powitalne Birst Agile analiz biznesowych kafelka w hello Panel dostępu, należy pobrać zalogowane automatycznie tooyour Birst Agile analiz biznesowych aplikacji.</span><span class="sxs-lookup"><span data-stu-id="eb41a-217">When you click hello Birst Agile Business Analytics tile in hello Access Panel, you should get automatically signed-on tooyour Birst Agile Business Analytics application.</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="eb41a-218">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="eb41a-218">Additional resources</span></span>

* [<span data-ttu-id="eb41a-219">Lista samouczków dotyczących tooIntegrate aplikacji SaaS w usłudze Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="eb41a-219">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="eb41a-220">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="eb41a-220">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-birst-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-birst-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-birst-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-birst-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-birst-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-birst-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-birst-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-birst-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-birst-tutorial/tutorial_general_203.png

