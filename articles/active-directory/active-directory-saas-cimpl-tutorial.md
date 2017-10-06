---
title: 'Samouczek: Integracji Azure Active Directory z Cimpl | Dokumentacja firmy Microsoft'
description: "Dowiedz się, jak tooconfigure logowanie jednokrotne między usługą Azure Active Directory i Cimpl."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 58ee5481-ae40-4e4a-a3c9-86343851fc9a
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/14/2017
ms.author: jeedes
ms.openlocfilehash: 0b993f2b58aaeac24e657060fb31651edc847f98
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-cimpl"></a><span data-ttu-id="ea2b4-103">Samouczek: Integracji Azure Active Directory z Cimpl</span><span class="sxs-lookup"><span data-stu-id="ea2b4-103">Tutorial: Azure Active Directory integration with Cimpl</span></span>

<span data-ttu-id="ea2b4-104">Z tego samouczka, dowiesz się, jak toointegrate Cimpl w usłudze Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="ea2b4-104">In this tutorial, you learn how toointegrate Cimpl with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="ea2b4-105">Integracja z usługą Azure AD Cimpl zapewnia hello następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="ea2b4-105">Integrating Cimpl with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="ea2b4-106">Można kontrolować w usłudze Azure AD, kto ma dostęp do tooCimpl</span><span class="sxs-lookup"><span data-stu-id="ea2b4-106">You can control in Azure AD who has access tooCimpl</span></span>
- <span data-ttu-id="ea2b4-107">Można włączyć użytkownika użytkownicy tooautomatically get zalogowane tooCimpl (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="ea2b4-107">You can enable your users tooautomatically get signed-on tooCimpl (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="ea2b4-108">Możesz zarządzać kont w jednej centralnej lokalizacji - hello portalu Azure</span><span class="sxs-lookup"><span data-stu-id="ea2b4-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="ea2b4-109">Jeśli chcesz tooknow więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="ea2b4-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ea2b4-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="ea2b4-110">Prerequisites</span></span>

<span data-ttu-id="ea2b4-111">tooconfigure integracji z usługą Azure AD z Cimpl należy hello następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="ea2b4-111">tooconfigure Azure AD integration with Cimpl, you need hello following items:</span></span>

- <span data-ttu-id="ea2b4-112">Subskrypcję usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="ea2b4-112">An Azure AD subscription</span></span>
- <span data-ttu-id="ea2b4-113">Cimpl jednokrotnego włączone subskrypcji</span><span class="sxs-lookup"><span data-stu-id="ea2b4-113">A Cimpl single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="ea2b4-114">tootest hello kroków w tym samouczku, zaleca się przy użyciu środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="ea2b4-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="ea2b4-115">tootest hello kroki opisane w tym samouczku, należy stosować te zalecenia:</span><span class="sxs-lookup"><span data-stu-id="ea2b4-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="ea2b4-116">Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="ea2b4-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="ea2b4-117">Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz pobrać miesięczna wersja próbna [tutaj](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="ea2b4-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="ea2b4-118">Opis scenariusza</span><span class="sxs-lookup"><span data-stu-id="ea2b4-118">Scenario description</span></span>
<span data-ttu-id="ea2b4-119">W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym.</span><span class="sxs-lookup"><span data-stu-id="ea2b4-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="ea2b4-120">Scenariusz Hello opisane w tym samouczku składa się z dwóch głównych elementów:</span><span class="sxs-lookup"><span data-stu-id="ea2b4-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="ea2b4-121">Dodawanie Cimpl z galerii hello</span><span class="sxs-lookup"><span data-stu-id="ea2b4-121">Adding Cimpl from hello gallery</span></span>
2. <span data-ttu-id="ea2b4-122">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="ea2b4-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-cimpl-from-hello-gallery"></a><span data-ttu-id="ea2b4-123">Dodawanie Cimpl z galerii hello</span><span class="sxs-lookup"><span data-stu-id="ea2b4-123">Adding Cimpl from hello gallery</span></span>
<span data-ttu-id="ea2b4-124">tooconfigure hello integracji Cimpl do usługi Azure AD, należy tooadd Cimpl z hello galerii tooyour listę zarządzanych aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="ea2b4-124">tooconfigure hello integration of Cimpl into Azure AD, you need tooadd Cimpl from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="ea2b4-125">**tooadd Cimpl z galerii hello, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="ea2b4-125">**tooadd Cimpl from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="ea2b4-126">W hello  **[portalu Azure](https://portal.azure.com)**na temat hello panelu nawigacji po lewej stronie, kliknij przycisk **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="ea2b4-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Usługa Active Directory][1]

2. <span data-ttu-id="ea2b4-128">Przejdź za**aplikacje dla przedsiębiorstw**.</span><span class="sxs-lookup"><span data-stu-id="ea2b4-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="ea2b4-129">Następnie przejdź zbyt**wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="ea2b4-129">Then go too**All applications**.</span></span>

    ![Aplikacje][2]
    
3. <span data-ttu-id="ea2b4-131">tooadd nową aplikację, kliknij przycisk **nowej aplikacji** przycisk u góry hello okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="ea2b4-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplikacje][3]

4. <span data-ttu-id="ea2b4-133">W polu wyszukiwania hello wpisz **Cimpl**.</span><span class="sxs-lookup"><span data-stu-id="ea2b4-133">In hello search box, type **Cimpl**.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-cimpl-tutorial/tutorial_cimpl_search.png)

5. <span data-ttu-id="ea2b4-135">W panelu wyników hello zaznacz **Cimpl**, a następnie kliknij przycisk **Dodaj** przycisk aplikacji hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="ea2b4-135">In hello results panel, select **Cimpl**, and then click **Add** button tooadd hello application.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-cimpl-tutorial/tutorial_cimpl_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="ea2b4-137">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="ea2b4-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="ea2b4-138">W tej sekcji skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z Cimpl w oparciu o nazwie "Britta Simona" użytkownika testowego.</span><span class="sxs-lookup"><span data-stu-id="ea2b4-138">In this section, you configure and test Azure AD single sign-on with Cimpl based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="ea2b4-139">Dla pojedynczego logowania jednokrotnego toowork usługi Azure AD musi tooknow użytkownika odpowiednikiem hello w Cimpl jest tooa użytkownika w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="ea2b4-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Cimpl is tooa user in Azure AD.</span></span> <span data-ttu-id="ea2b4-140">Innymi słowy relację łącza między użytkownika usługi Azure AD i hello użytkownikowi w Cimpl musi toobe ustanowione.</span><span class="sxs-lookup"><span data-stu-id="ea2b4-140">In other words, a link relationship between an Azure AD user and hello related user in Cimpl needs toobe established.</span></span>

<span data-ttu-id="ea2b4-141">W Cimpl, należy przypisać wartość hello hello **nazwy użytkownika** w usłudze Azure AD jako wartość hello hello **Username** tooestablish hello łącze relacji.</span><span class="sxs-lookup"><span data-stu-id="ea2b4-141">In Cimpl, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="ea2b4-142">tooconfigure i testowych usługi Azure AD rejestracji jednokrotnej z Cimpl, należy po bloków konstrukcyjnych hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="ea2b4-142">tooconfigure and test Azure AD single sign-on with Cimpl, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="ea2b4-143">**[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configuring-azure-ad-single-sign-on)**  -tooenable Twojego toouse użytkowników tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="ea2b4-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="ea2b4-144">**[Tworzenie użytkownika testowego usługi Azure AD](#creating-an-azure-ad-test-user)**  -tootest usługi Azure AD rejestracji jednokrotnej z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="ea2b4-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="ea2b4-145">**[Tworzenie użytkownika testowego Cimpl](#creating-a-cimpl-test-user)**  -toohave odpowiednikiem Simona Britta w Cimpl, który jest połączony toohello usługi Azure AD reprezentację użytkownika.</span><span class="sxs-lookup"><span data-stu-id="ea2b4-145">**[Creating a Cimpl test user](#creating-a-cimpl-test-user)** - toohave a counterpart of Britta Simon in Cimpl that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="ea2b4-146">**[Przypisanie użytkownika testowego hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Simona Britta toouse usługi Azure AD rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="ea2b4-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="ea2b4-147">**[Testowanie rejestracji jednokrotnej](#testing-single-sign-on)**  -tooverify czy hello konfiguracji działania.</span><span class="sxs-lookup"><span data-stu-id="ea2b4-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="ea2b4-148">Konfigurowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="ea2b4-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="ea2b4-149">W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w portalu Azure hello i skonfigurować logowanie jednokrotne w aplikacji Cimpl.</span><span class="sxs-lookup"><span data-stu-id="ea2b4-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Cimpl application.</span></span>

<span data-ttu-id="ea2b4-150">**tooconfigure usługi Azure AD rejestracji jednokrotnej z Cimpl, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="ea2b4-150">**tooconfigure Azure AD single sign-on with Cimpl, perform hello following steps:**</span></span>

1. <span data-ttu-id="ea2b4-151">W portalu Azure na powitania hello **Cimpl** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.</span><span class="sxs-lookup"><span data-stu-id="ea2b4-151">In hello Azure portal, on hello **Cimpl** application integration page, click **Single sign-on**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej][4]

2. <span data-ttu-id="ea2b4-153">Na powitania **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** tooenable rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="ea2b4-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-cimpl-tutorial/tutorial_cimpl_samlbase.png)

3. <span data-ttu-id="ea2b4-155">Na powitania **Cimpl domeny i adres URL** sekcji, wykonaj następujące kroki hello:</span><span class="sxs-lookup"><span data-stu-id="ea2b4-155">On hello **Cimpl Domain and URLs** section, perform hello following steps:</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-cimpl-tutorial/tutorial_cimpl_url.png)

    <span data-ttu-id="ea2b4-157">a.</span><span class="sxs-lookup"><span data-stu-id="ea2b4-157">a.</span></span> <span data-ttu-id="ea2b4-158">W hello **adres URL logowania** tekstowym, wpisz adres URL za pomocą hello następującego wzorca:`https://sso.etelesolv.com/<TENANTNAME>`</span><span class="sxs-lookup"><span data-stu-id="ea2b4-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://sso.etelesolv.com/<TENANTNAME>`</span></span>

    <span data-ttu-id="ea2b4-159">b.</span><span class="sxs-lookup"><span data-stu-id="ea2b4-159">b.</span></span> <span data-ttu-id="ea2b4-160">W hello **identyfikator** tekstowym, wpisz adres URL za pomocą hello następującego wzorca:`https://sso.etelesolv.com/<TENANTNAME>`</span><span class="sxs-lookup"><span data-stu-id="ea2b4-160">In hello **Identifier** textbox, type a URL using hello following pattern: `https://sso.etelesolv.com/<TENANTNAME>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="ea2b4-161">Wartości te nie są prawdziwe.</span><span class="sxs-lookup"><span data-stu-id="ea2b4-161">These values are not real.</span></span> <span data-ttu-id="ea2b4-162">Zaktualizować te wartości z hello rzeczywisty adres URL logowania i identyfikator.</span><span class="sxs-lookup"><span data-stu-id="ea2b4-162">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="ea2b4-163">Skontaktuj się z zespołem Cimpl w **+1 866-982-8250** tooget tych wartości.</span><span class="sxs-lookup"><span data-stu-id="ea2b4-163">Contact Cimpl team at **+1 866-982-8250** tooget these values.</span></span> 
 
4. <span data-ttu-id="ea2b4-164">Na powitania **certyfikat podpisywania SAML** kliknij **certyfikatu (Base64)** , a następnie zapisz plik certyfikatu hello na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="ea2b4-164">On hello **SAML Signing Certificate** section, click **Certificate (Base64)** and then save hello certificate file on your computer.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-cimpl-tutorial/tutorial_cimpl_certificate.png) 

5. <span data-ttu-id="ea2b4-166">Kliknij przycisk **zapisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="ea2b4-166">Click **Save** button.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-cimpl-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="ea2b4-168">Na powitania **konfiguracji Cimpl** kliknij **skonfigurować Cimpl** tooopen **Konfigurowanie logowania jednokrotnego** okna.</span><span class="sxs-lookup"><span data-stu-id="ea2b4-168">On hello **Cimpl Configuration** section, click **Configure Cimpl** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="ea2b4-169">Kopiuj hello **identyfikator jednostki SAML i SAML pojedynczy znak na adres URL usługi** z hello **sekcji krótkimi opisami.**</span><span class="sxs-lookup"><span data-stu-id="ea2b4-169">Copy hello **SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-cimpl-tutorial/tutorial_cimpl_configure.png) 

7. <span data-ttu-id="ea2b4-171">tooconfigure rejestracji jednokrotnej w **Cimpl** strony, należy pobrać hello toosend **certyfikatu (Base64)**, **identyfikator jednostki SAML i SAML pojedynczy znak na adres URL usługi** tooCimpl Obsługa w **+1 866-982-8250**.</span><span class="sxs-lookup"><span data-stu-id="ea2b4-171">tooconfigure single sign-on on **Cimpl** side, you need toosend hello downloaded **Certificate (Base64)**, **SAML Entity ID, and SAML Single Sign-On Service URL** tooCimpl support at **+1 866-982-8250**.</span></span>


> [!TIP]
> <span data-ttu-id="ea2b4-172">Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz hello [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji hello!</span><span class="sxs-lookup"><span data-stu-id="ea2b4-172">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="ea2b4-173">Po dodaniu tej aplikacji z hello **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij hello **rejestracji jednokrotnej** hello kartę i dostępu do osadzonych dokumentacji za pośrednictwem hello  **Konfiguracja** sekcji u dołu hello.</span><span class="sxs-lookup"><span data-stu-id="ea2b4-173">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="ea2b4-174">Więcej o hello osadzonych dokumentacji funkcji w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="ea2b4-174">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="ea2b4-175">Tworzenie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="ea2b4-175">Creating an Azure AD test user</span></span>
<span data-ttu-id="ea2b4-176">Celem Hello w tej sekcji jest toocreate użytkownika testowego, w portalu Azure o nazwie Simona Britta hello.</span><span class="sxs-lookup"><span data-stu-id="ea2b4-176">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Tworzenie użytkowników usługi Azure AD][100]

<span data-ttu-id="ea2b4-178">**toocreate użytkownika testowego w usłudze Azure AD, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="ea2b4-178">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="ea2b4-179">W hello **portalu Azure**na temat hello w lewym okienku nawigacji, kliknij przycisk **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="ea2b4-179">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-cimpl-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="ea2b4-181">toodisplay hello listę użytkowników, przejdź zbyt**użytkowników i grup** i kliknij przycisk **wszyscy użytkownicy**.</span><span class="sxs-lookup"><span data-stu-id="ea2b4-181">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-cimpl-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="ea2b4-183">Witaj tooopen **użytkownika** okna dialogowego, kliknij przycisk **Dodaj** u góry hello hello okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="ea2b4-183">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-cimpl-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="ea2b4-185">Na powitania **użytkownika** okna dialogowego wykonaj hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="ea2b4-185">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-cimpl-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="ea2b4-187">a.</span><span class="sxs-lookup"><span data-stu-id="ea2b4-187">a.</span></span> <span data-ttu-id="ea2b4-188">W hello **nazwa** pole tekstowe, typ **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="ea2b4-188">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="ea2b4-189">b.</span><span class="sxs-lookup"><span data-stu-id="ea2b4-189">b.</span></span> <span data-ttu-id="ea2b4-190">W hello **nazwy użytkownika** pole tekstowe, hello typu **adres e-mail** z BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="ea2b4-190">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="ea2b4-191">c.</span><span class="sxs-lookup"><span data-stu-id="ea2b4-191">c.</span></span> <span data-ttu-id="ea2b4-192">Wybierz **Pokaż hasło** i zanotuj wartość hello hello **hasło**.</span><span class="sxs-lookup"><span data-stu-id="ea2b4-192">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="ea2b4-193">d.</span><span class="sxs-lookup"><span data-stu-id="ea2b4-193">d.</span></span> <span data-ttu-id="ea2b4-194">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="ea2b4-194">Click **Create**.</span></span>
 
### <a name="creating-a-cimpl-test-user"></a><span data-ttu-id="ea2b4-195">Tworzenie użytkownika testowego Cimpl</span><span class="sxs-lookup"><span data-stu-id="ea2b4-195">Creating a Cimpl test user</span></span>

<span data-ttu-id="ea2b4-196">Celem Hello w tej sekcji jest toocreate użytkownika o nazwie Simona Britta w Cimpl.</span><span class="sxs-lookup"><span data-stu-id="ea2b4-196">hello objective of this section is toocreate a user called Britta Simon in Cimpl.</span></span> <span data-ttu-id="ea2b4-197">Praca z obsługą Cimpl w **+1 866-982-8250** tooadd hello użytkowników w hello Cimpl konta.</span><span class="sxs-lookup"><span data-stu-id="ea2b4-197">Work with Cimpl support at **+1 866-982-8250** tooadd hello users in hello Cimpl account.</span></span> 

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="ea2b4-198">Przypisanie użytkownika testowego hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="ea2b4-198">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="ea2b4-199">W tej sekcji możesz włączyć toouse Simona Britta Azure logowania jednokrotnego za udzielanie dostępu tooCimpl.</span><span class="sxs-lookup"><span data-stu-id="ea2b4-199">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooCimpl.</span></span>

![Przypisz użytkownika][200] 

<span data-ttu-id="ea2b4-201">**tooassign tooCimpl Simona Britta wykonaj hello następujące kroki:**</span><span class="sxs-lookup"><span data-stu-id="ea2b4-201">**tooassign Britta Simon tooCimpl, perform hello following steps:**</span></span>

1. <span data-ttu-id="ea2b4-202">W portalu Azure hello, otwórz widok aplikacji hello, a następnie przejdź do widoku katalogu toohello i przejść za**aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="ea2b4-202">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Przypisz użytkownika][201] 

2. <span data-ttu-id="ea2b4-204">Z listy aplikacji hello wybierz **Cimpl**.</span><span class="sxs-lookup"><span data-stu-id="ea2b4-204">In hello applications list, select **Cimpl**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-cimpl-tutorial/tutorial_cimpl_app.png) 

3. <span data-ttu-id="ea2b4-206">W menu powitania po lewej stronie powitania kliknij **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="ea2b4-206">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Przypisz użytkownika][202] 

4. <span data-ttu-id="ea2b4-208">Kliknij przycisk **Dodaj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="ea2b4-208">Click **Add** button.</span></span> <span data-ttu-id="ea2b4-209">Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="ea2b4-209">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Przypisz użytkownika][203]

5. <span data-ttu-id="ea2b4-211">Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** hello listy użytkowników.</span><span class="sxs-lookup"><span data-stu-id="ea2b4-211">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="ea2b4-212">Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="ea2b4-212">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="ea2b4-213">Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="ea2b4-213">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="ea2b4-214">Testowanie rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="ea2b4-214">Testing single sign-on</span></span>

<span data-ttu-id="ea2b4-215">Celem Hello w tej sekcji jest tootest programu Azure AD SSO konfiguracji przy użyciu hello panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="ea2b4-215">hello objective of this section is tootest your Azure AD SSO configuration using hello Access Panel.</span></span>  <span data-ttu-id="ea2b4-216">Po kliknięciu kafelka Cimpl hello w hello Panel dostępu, należy pobrać automatycznie zalogowane tooyour Cimpl aplikacji.</span><span class="sxs-lookup"><span data-stu-id="ea2b4-216">When you click hello Cimpl tile in hello Access Panel, you should get automatically signed-on tooyour Cimpl application.</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="ea2b4-217">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="ea2b4-217">Additional resources</span></span>

* [<span data-ttu-id="ea2b4-218">Lista samouczków dotyczących tooIntegrate aplikacji SaaS w usłudze Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="ea2b4-218">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="ea2b4-219">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="ea2b4-219">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-cimpl-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-cimpl-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-cimpl-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-cimpl-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-cimpl-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-cimpl-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-cimpl-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-cimpl-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-cimpl-tutorial/tutorial_general_203.png

