---
title: 'Samouczek: Integracji Azure Active Directory z PostBeyond | Dokumentacja firmy Microsoft'
description: "Dowiedz się, jak tooconfigure logowanie jednokrotne między usługą Azure Active Directory i PostBeyond."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 09992f08-ec50-4472-997f-ccbe719039e8
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/29/2017
ms.author: jeedes
ms.openlocfilehash: 38019fd24a603732e91a1b5f7bfed5ab4edb017f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-postbeyond"></a><span data-ttu-id="f92d4-103">Samouczek: Integracji Azure Active Directory z PostBeyond</span><span class="sxs-lookup"><span data-stu-id="f92d4-103">Tutorial: Azure Active Directory integration with PostBeyond</span></span>

<span data-ttu-id="f92d4-104">Z tego samouczka, dowiesz się, jak toointegrate PostBeyond w usłudze Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="f92d4-104">In this tutorial, you learn how toointegrate PostBeyond with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="f92d4-105">Integracja z usługą Azure AD PostBeyond zapewnia hello następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="f92d4-105">Integrating PostBeyond with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="f92d4-106">Można kontrolować w usłudze Azure AD, kto ma dostęp do tooPostBeyond</span><span class="sxs-lookup"><span data-stu-id="f92d4-106">You can control in Azure AD who has access tooPostBeyond</span></span>
- <span data-ttu-id="f92d4-107">Można włączyć użytkownika użytkownicy tooautomatically get zalogowane tooPostBeyond (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="f92d4-107">You can enable your users tooautomatically get signed-on tooPostBeyond (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="f92d4-108">Możesz zarządzać kont w jednej centralnej lokalizacji - hello portalu Azure</span><span class="sxs-lookup"><span data-stu-id="f92d4-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="f92d4-109">Jeśli chcesz tooknow więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="f92d4-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f92d4-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="f92d4-110">Prerequisites</span></span>

<span data-ttu-id="f92d4-111">tooconfigure integracji z usługą Azure AD z PostBeyond należy hello następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="f92d4-111">tooconfigure Azure AD integration with PostBeyond, you need hello following items:</span></span>

- <span data-ttu-id="f92d4-112">Subskrypcję usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="f92d4-112">An Azure AD subscription</span></span>
- <span data-ttu-id="f92d4-113">PostBeyond logowanie jednokrotne włączone subskrypcji</span><span class="sxs-lookup"><span data-stu-id="f92d4-113">A PostBeyond single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="f92d4-114">tootest hello kroków w tym samouczku, zaleca się przy użyciu środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="f92d4-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="f92d4-115">tootest hello kroki opisane w tym samouczku, należy stosować te zalecenia:</span><span class="sxs-lookup"><span data-stu-id="f92d4-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="f92d4-116">Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="f92d4-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="f92d4-117">Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz pobrać miesięczna wersja próbna [tutaj](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="f92d4-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="f92d4-118">Opis scenariusza</span><span class="sxs-lookup"><span data-stu-id="f92d4-118">Scenario description</span></span>
<span data-ttu-id="f92d4-119">W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym.</span><span class="sxs-lookup"><span data-stu-id="f92d4-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="f92d4-120">Scenariusz Hello opisane w tym samouczku składa się z dwóch głównych elementów:</span><span class="sxs-lookup"><span data-stu-id="f92d4-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="f92d4-121">Dodawanie PostBeyond z galerii hello</span><span class="sxs-lookup"><span data-stu-id="f92d4-121">Adding PostBeyond from hello gallery</span></span>
2. <span data-ttu-id="f92d4-122">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="f92d4-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-postbeyond-from-hello-gallery"></a><span data-ttu-id="f92d4-123">Dodawanie PostBeyond z galerii hello</span><span class="sxs-lookup"><span data-stu-id="f92d4-123">Adding PostBeyond from hello gallery</span></span>
<span data-ttu-id="f92d4-124">integracji hello tooconfigure PostBeyond do usługi Azure AD, należy tooadd PostBeyond z hello galerii tooyour listę zarządzanych aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="f92d4-124">tooconfigure hello integration of PostBeyond into Azure AD, you need tooadd PostBeyond from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="f92d4-125">**tooadd PostBeyond z galerii hello, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="f92d4-125">**tooadd PostBeyond from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="f92d4-126">W hello  **[portalu Azure](https://portal.azure.com)**na temat hello panelu nawigacji po lewej stronie, kliknij przycisk **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="f92d4-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Usługa Active Directory][1]

2. <span data-ttu-id="f92d4-128">Przejdź za**aplikacje dla przedsiębiorstw**.</span><span class="sxs-lookup"><span data-stu-id="f92d4-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="f92d4-129">Następnie przejdź zbyt**wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="f92d4-129">Then go too**All applications**.</span></span>

    ![Aplikacje][2]
    
3. <span data-ttu-id="f92d4-131">tooadd nową aplikację, kliknij przycisk **nowej aplikacji** przycisk u góry hello okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="f92d4-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplikacje][3]

4. <span data-ttu-id="f92d4-133">W polu wyszukiwania hello wpisz **PostBeyond**.</span><span class="sxs-lookup"><span data-stu-id="f92d4-133">In hello search box, type **PostBeyond**.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-postbeyond-tutorial/tutorial_postbeyond_search.png)

5. <span data-ttu-id="f92d4-135">W panelu wyników hello zaznacz **PostBeyond**, a następnie kliknij przycisk **Dodaj** przycisk aplikacji hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="f92d4-135">In hello results panel, select **PostBeyond**, and then click **Add** button tooadd hello application.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-postbeyond-tutorial/tutorial_postbeyond_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="f92d4-137">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="f92d4-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="f92d4-138">W tej sekcji skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z PostBeyond w oparciu o nazwie "Britta Simona" użytkownika testowego.</span><span class="sxs-lookup"><span data-stu-id="f92d4-138">In this section, you configure and test Azure AD single sign-on with PostBeyond based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="f92d4-139">Dla pojedynczego logowania jednokrotnego toowork usługi Azure AD musi tooknow użytkownika odpowiednikiem hello w PostBeyond jest tooa użytkownika w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="f92d4-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in PostBeyond is tooa user in Azure AD.</span></span> <span data-ttu-id="f92d4-140">Innymi słowy relację łącza między użytkownika usługi Azure AD i hello użytkownikowi w PostBeyond musi toobe ustanowione.</span><span class="sxs-lookup"><span data-stu-id="f92d4-140">In other words, a link relationship between an Azure AD user and hello related user in PostBeyond needs toobe established.</span></span>

<span data-ttu-id="f92d4-141">W PostBeyond, należy przypisać wartość hello hello **nazwy użytkownika** w usłudze Azure AD jako wartość hello hello **Username** tooestablish hello łącze relacji.</span><span class="sxs-lookup"><span data-stu-id="f92d4-141">In PostBeyond, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="f92d4-142">tooconfigure i testowych usługi Azure AD rejestracji jednokrotnej z PostBeyond, należy po bloków konstrukcyjnych hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="f92d4-142">tooconfigure and test Azure AD single sign-on with PostBeyond, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="f92d4-143">**[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configuring-azure-ad-single-sign-on)**  -tooenable Twojego toouse użytkowników tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="f92d4-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="f92d4-144">**[Tworzenie użytkownika testowego usługi Azure AD](#creating-an-azure-ad-test-user)**  -tootest usługi Azure AD rejestracji jednokrotnej z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="f92d4-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="f92d4-145">**[Tworzenie użytkownika testowego PostBeyond](#creating-a-postbeyond-test-user)**  -toohave odpowiednikiem Simona Britta w PostBeyond, który jest połączony toohello usługi Azure AD reprezentację użytkownika.</span><span class="sxs-lookup"><span data-stu-id="f92d4-145">**[Creating a PostBeyond test user](#creating-a-postbeyond-test-user)** - toohave a counterpart of Britta Simon in PostBeyond that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="f92d4-146">**[Przypisanie użytkownika testowego hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Simona Britta toouse usługi Azure AD rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="f92d4-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="f92d4-147">**[Testowanie rejestracji jednokrotnej](#testing-single-sign-on)**  -tooverify czy hello konfiguracji działania.</span><span class="sxs-lookup"><span data-stu-id="f92d4-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="f92d4-148">Konfigurowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="f92d4-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="f92d4-149">W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w hello portalu Azure i skonfigurować logowanie jednokrotne PostBeyond aplikacji.</span><span class="sxs-lookup"><span data-stu-id="f92d4-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your PostBeyond application.</span></span>

<span data-ttu-id="f92d4-150">**tooconfigure usługi Azure AD rejestracji jednokrotnej z PostBeyond, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="f92d4-150">**tooconfigure Azure AD single sign-on with PostBeyond, perform hello following steps:**</span></span>

1. <span data-ttu-id="f92d4-151">W portalu Azure na powitania hello **PostBeyond** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.</span><span class="sxs-lookup"><span data-stu-id="f92d4-151">In hello Azure portal, on hello **PostBeyond** application integration page, click **Single sign-on**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej][4]

2. <span data-ttu-id="f92d4-153">Na powitania **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** tooenable rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="f92d4-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-postbeyond-tutorial/tutorial_postbeyond_samlbase.png)

3. <span data-ttu-id="f92d4-155">Na powitania **PostBeyond domeny i adres URL** sekcji, wykonaj następujące kroki hello:</span><span class="sxs-lookup"><span data-stu-id="f92d4-155">On hello **PostBeyond Domain and URLs** section, perform hello following steps:</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-postbeyond-tutorial/tutorial_postbeyond_url.png)

    <span data-ttu-id="f92d4-157">a.</span><span class="sxs-lookup"><span data-stu-id="f92d4-157">a.</span></span> <span data-ttu-id="f92d4-158">W hello **adres URL logowania** tekstowym, wpisz adres URL za pomocą hello następującego wzorca:`https://<subdomain>.postbeyond.com`</span><span class="sxs-lookup"><span data-stu-id="f92d4-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<subdomain>.postbeyond.com`</span></span>

    <span data-ttu-id="f92d4-159">b.</span><span class="sxs-lookup"><span data-stu-id="f92d4-159">b.</span></span> <span data-ttu-id="f92d4-160">W hello **identyfikator** tekstowym, wpisz adres URL za pomocą hello następującego wzorca:`https://<subdomain>.postbeyond.com`</span><span class="sxs-lookup"><span data-stu-id="f92d4-160">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<subdomain>.postbeyond.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="f92d4-161">Wartości te nie są prawdziwe.</span><span class="sxs-lookup"><span data-stu-id="f92d4-161">These values are not real.</span></span> <span data-ttu-id="f92d4-162">Zaktualizować te wartości z hello rzeczywisty adres URL logowania i identyfikator.</span><span class="sxs-lookup"><span data-stu-id="f92d4-162">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="f92d4-163">Skontaktuj się z [zespołem pomocy technicznej klienta PostBeyond](mailto:sso@postbeyond.com) tooget tych wartości.</span><span class="sxs-lookup"><span data-stu-id="f92d4-163">Contact [PostBeyond Client support team](mailto:sso@postbeyond.com) tooget these values.</span></span> 
 
4. <span data-ttu-id="f92d4-164">Na powitania **certyfikat podpisywania SAML** kliknij **Certificate(Base64)** , a następnie zapisz plik certyfikatu hello na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="f92d4-164">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-postbeyond-tutorial/tutorial_postbeyond_certificate.png) 

5. <span data-ttu-id="f92d4-166">Kliknij przycisk **zapisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="f92d4-166">Click **Save** button.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-postbeyond-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="f92d4-168">Na powitania **konfiguracji PostBeyond** kliknij **skonfigurować PostBeyond** tooopen **Konfigurowanie logowania jednokrotnego** okna.</span><span class="sxs-lookup"><span data-stu-id="f92d4-168">On hello **PostBeyond Configuration** section, click **Configure PostBeyond** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="f92d4-169">Kopiuj hello **Sign-Out adres URL, identyfikator jednostki SAML i SAML pojedynczy znak na adres URL usługi** z hello **sekcji krótkimi opisami.**</span><span class="sxs-lookup"><span data-stu-id="f92d4-169">Copy hello **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-postbeyond-tutorial/tutorial_postbeyond_configure.png) 

7. <span data-ttu-id="f92d4-171">tooconfigure rejestracji jednokrotnej w **PostBeyond** strony, należy pobrać hello toosend **Certificate(Base64)**, **identyfikator jednostki SAML**, **SAML logowania jednokrotnego Adres URL usługi** i **Sign-Out URL** za[zespołem pomocy technicznej PostBeyond](mailto:sso@postbeyond.com).</span><span class="sxs-lookup"><span data-stu-id="f92d4-171">tooconfigure single sign-on on **PostBeyond** side, you need toosend hello downloaded **Certificate(Base64)**, **SAML Entity ID**, **SAML Single Sign-On Service URL** and **Sign-Out URL** too[PostBeyond support team](mailto:sso@postbeyond.com).</span></span> <span data-ttu-id="f92d4-172">To ustawienie toohave hello prawidłowo po obu stronach połączenia logowania jednokrotnego SAML one ustawić.</span><span class="sxs-lookup"><span data-stu-id="f92d4-172">They set this setting toohave hello SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="f92d4-173">Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz hello [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji hello!</span><span class="sxs-lookup"><span data-stu-id="f92d4-173">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="f92d4-174">Po dodaniu tej aplikacji z hello **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij hello **rejestracji jednokrotnej** hello kartę i dostępu do osadzonych dokumentacji za pośrednictwem hello  **Konfiguracja** sekcji u dołu hello.</span><span class="sxs-lookup"><span data-stu-id="f92d4-174">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="f92d4-175">Więcej o hello osadzonych dokumentacji funkcji w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="f92d4-175">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="f92d4-176">Tworzenie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="f92d4-176">Creating an Azure AD test user</span></span>
<span data-ttu-id="f92d4-177">Celem Hello w tej sekcji jest toocreate użytkownika testowego, w portalu Azure o nazwie Simona Britta hello.</span><span class="sxs-lookup"><span data-stu-id="f92d4-177">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Tworzenie użytkowników usługi Azure AD][100]

<span data-ttu-id="f92d4-179">**toocreate użytkownika testowego w usłudze Azure AD, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="f92d4-179">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="f92d4-180">W hello **portalu Azure**na temat hello w lewym okienku nawigacji, kliknij przycisk **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="f92d4-180">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-postbeyond-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="f92d4-182">toodisplay hello listę użytkowników, przejdź zbyt**użytkowników i grup** i kliknij przycisk **wszyscy użytkownicy**.</span><span class="sxs-lookup"><span data-stu-id="f92d4-182">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-postbeyond-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="f92d4-184">Witaj tooopen **użytkownika** okna dialogowego, kliknij przycisk **Dodaj** u góry hello hello okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="f92d4-184">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-postbeyond-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="f92d4-186">Na powitania **użytkownika** okna dialogowego wykonaj hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="f92d4-186">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-postbeyond-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="f92d4-188">a.</span><span class="sxs-lookup"><span data-stu-id="f92d4-188">a.</span></span> <span data-ttu-id="f92d4-189">W hello **nazwa** pole tekstowe, typ **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="f92d4-189">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="f92d4-190">b.</span><span class="sxs-lookup"><span data-stu-id="f92d4-190">b.</span></span> <span data-ttu-id="f92d4-191">W hello **nazwy użytkownika** pole tekstowe, hello typu **adres e-mail** z BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="f92d4-191">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="f92d4-192">c.</span><span class="sxs-lookup"><span data-stu-id="f92d4-192">c.</span></span> <span data-ttu-id="f92d4-193">Wybierz **Pokaż hasło** i zanotuj wartość hello hello **hasło**.</span><span class="sxs-lookup"><span data-stu-id="f92d4-193">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="f92d4-194">d.</span><span class="sxs-lookup"><span data-stu-id="f92d4-194">d.</span></span> <span data-ttu-id="f92d4-195">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="f92d4-195">Click **Create**.</span></span>
 
### <a name="creating-a-postbeyond-test-user"></a><span data-ttu-id="f92d4-196">Tworzenie użytkownika testowego PostBeyond</span><span class="sxs-lookup"><span data-stu-id="f92d4-196">Creating a PostBeyond test user</span></span>

<span data-ttu-id="f92d4-197">W tej sekcji należy utworzyć użytkownika o nazwie Simona Britta w PostBeyond.</span><span class="sxs-lookup"><span data-stu-id="f92d4-197">In this section, you create a user called Britta Simon in PostBeyond.</span></span> <span data-ttu-id="f92d4-198">Jeśli nie znasz jak tooadd Simona Britta w PostBeyond, współpracy z [zespołem pomocy technicznej PostBeyond](mailto:sso@postbeyond.com) tooadd hello użytkownika testowego i włączenia funkcji logowania jednokrotnego.</span><span class="sxs-lookup"><span data-stu-id="f92d4-198">If you don't know how tooadd Britta Simon in PostBeyond, please work with [PostBeyond support team](mailto:sso@postbeyond.com) tooadd hello test user and enable SSO.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="f92d4-199">Przypisanie użytkownika testowego hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="f92d4-199">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="f92d4-200">W tej sekcji możesz włączyć toouse Simona Britta Azure logowania jednokrotnego za udzielanie dostępu tooPostBeyond.</span><span class="sxs-lookup"><span data-stu-id="f92d4-200">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooPostBeyond.</span></span>

![Przypisz użytkownika][200] 

<span data-ttu-id="f92d4-202">**tooassign tooPostBeyond Simona Britta wykonaj hello następujące kroki:**</span><span class="sxs-lookup"><span data-stu-id="f92d4-202">**tooassign Britta Simon tooPostBeyond, perform hello following steps:**</span></span>

1. <span data-ttu-id="f92d4-203">W portalu Azure hello, otwórz widok aplikacji hello, a następnie przejdź do widoku katalogu toohello i przejść za**aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="f92d4-203">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Przypisz użytkownika][201] 

2. <span data-ttu-id="f92d4-205">Z listy aplikacji hello wybierz **PostBeyond**.</span><span class="sxs-lookup"><span data-stu-id="f92d4-205">In hello applications list, select **PostBeyond**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-postbeyond-tutorial/tutorial_postbeyond_app.png) 

3. <span data-ttu-id="f92d4-207">W menu powitania po lewej stronie powitania kliknij **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="f92d4-207">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Przypisz użytkownika][202] 

4. <span data-ttu-id="f92d4-209">Kliknij przycisk **Dodaj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="f92d4-209">Click **Add** button.</span></span> <span data-ttu-id="f92d4-210">Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="f92d4-210">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Przypisz użytkownika][203]

5. <span data-ttu-id="f92d4-212">Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** hello listy użytkowników.</span><span class="sxs-lookup"><span data-stu-id="f92d4-212">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="f92d4-213">Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="f92d4-213">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="f92d4-214">Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="f92d4-214">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="f92d4-215">Testowanie rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="f92d4-215">Testing single sign-on</span></span>

<span data-ttu-id="f92d4-216">Celem Hello w tej sekcji jest tootest programu Azure AD SSO konfiguracji przy użyciu hello panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="f92d4-216">hello objective of this section is tootest your Azure AD SSO configuration using hello Access Panel.</span></span>

<span data-ttu-id="f92d4-217">Po kliknięciu kafelka PostBeyond hello w hello Panel dostępu, należy pobrać toohello PostBeyond Zaloguj się na stronie.</span><span class="sxs-lookup"><span data-stu-id="f92d4-217">When you click hello PostBeyond tile in hello Access Panel, you should get toohello PostBeyond sign in page.</span></span> <span data-ttu-id="f92d4-218">Polecenie **Zaloguj się przy użyciu usługi Office 365**, wprowadź swoje poświadczenia usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="f92d4-218">Click on **Sign in with Office 365**, enter your Azure AD credentials.</span></span> <span data-ttu-id="f92d4-219">Następnie możesz należy zalogować się do PostBeyond.</span><span class="sxs-lookup"><span data-stu-id="f92d4-219">Then, you should be logged in into PostBeyond.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="f92d4-220">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="f92d4-220">Additional resources</span></span>

* [<span data-ttu-id="f92d4-221">Lista samouczków dotyczących tooIntegrate aplikacji SaaS w usłudze Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="f92d4-221">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="f92d4-222">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="f92d4-222">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-postbeyond-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-postbeyond-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-postbeyond-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-postbeyond-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-postbeyond-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-postbeyond-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-postbeyond-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-postbeyond-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-postbeyond-tutorial/tutorial_general_203.png

