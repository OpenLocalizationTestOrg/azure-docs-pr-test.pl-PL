---
title: 'Samouczek: Integracji Azure Active Directory z eDigitalResearch | Dokumentacja firmy Microsoft'
description: "Dowiedz się, jak tooconfigure logowanie jednokrotne między usługą Azure Active Directory i eDigitalResearch."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: c6b66ea0-16ba-45b4-b550-e81c56262b1f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/20/2017
ms.author: jeedes
ms.openlocfilehash: 6dd3cafb25ef8ede3a4c16902ed8da69cb7b715f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-edigitalresearch"></a><span data-ttu-id="5fa4c-103">Samouczek: Integracji Azure Active Directory z eDigitalResearch</span><span class="sxs-lookup"><span data-stu-id="5fa4c-103">Tutorial: Azure Active Directory integration with eDigitalResearch</span></span>

<span data-ttu-id="5fa4c-104">Z tego samouczka, dowiesz się, jak eDigitalResearch toointegrate w usłudze Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="5fa4c-104">In this tutorial, you learn how toointegrate eDigitalResearch with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="5fa4c-105">Integracja z usługą Azure AD eDigitalResearch zapewnia hello następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="5fa4c-105">Integrating eDigitalResearch with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="5fa4c-106">Można kontrolować w usłudze Azure AD, kto ma dostęp do tooeDigitalResearch.</span><span class="sxs-lookup"><span data-stu-id="5fa4c-106">You can control in Azure AD who has access tooeDigitalResearch.</span></span>
- <span data-ttu-id="5fa4c-107">Można włączyć użytkownika użytkownicy tooautomatically get zalogowane tooeDigitalResearch (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="5fa4c-107">You can enable your users tooautomatically get signed-on tooeDigitalResearch (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="5fa4c-108">Możesz zarządzać kont w jednej centralnej lokalizacji - hello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="5fa4c-108">You can manage your accounts in one central location - hello Azure portal.</span></span>

<span data-ttu-id="5fa4c-109">Jeśli chcesz tooknow więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="5fa4c-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="5fa4c-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="5fa4c-110">Prerequisites</span></span>

<span data-ttu-id="5fa4c-111">tooconfigure integracji z usługą Azure AD z eDigitalResearch należy hello następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="5fa4c-111">tooconfigure Azure AD integration with eDigitalResearch, you need hello following items:</span></span>

- <span data-ttu-id="5fa4c-112">Subskrypcję usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="5fa4c-112">An Azure AD subscription</span></span>
- <span data-ttu-id="5fa4c-113">EDigitalResearch logowanie jednokrotne włączone subskrypcji</span><span class="sxs-lookup"><span data-stu-id="5fa4c-113">A eDigitalResearch single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="5fa4c-114">tootest hello kroków w tym samouczku, zaleca się przy użyciu środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="5fa4c-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="5fa4c-115">tootest hello kroki opisane w tym samouczku, należy stosować te zalecenia:</span><span class="sxs-lookup"><span data-stu-id="5fa4c-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="5fa4c-116">Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="5fa4c-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="5fa4c-117">Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz [uzyskać miesięczna wersja próbna](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="5fa4c-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="5fa4c-118">Opis scenariusza</span><span class="sxs-lookup"><span data-stu-id="5fa4c-118">Scenario description</span></span>
<span data-ttu-id="5fa4c-119">W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym.</span><span class="sxs-lookup"><span data-stu-id="5fa4c-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="5fa4c-120">Scenariusz Hello opisane w tym samouczku składa się z dwóch głównych elementów:</span><span class="sxs-lookup"><span data-stu-id="5fa4c-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="5fa4c-121">Dodawanie eDigitalResearch z galerii hello</span><span class="sxs-lookup"><span data-stu-id="5fa4c-121">Adding eDigitalResearch from hello gallery</span></span>
2. <span data-ttu-id="5fa4c-122">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="5fa4c-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-edigitalresearch-from-hello-gallery"></a><span data-ttu-id="5fa4c-123">Dodawanie eDigitalResearch z galerii hello</span><span class="sxs-lookup"><span data-stu-id="5fa4c-123">Adding eDigitalResearch from hello gallery</span></span>
<span data-ttu-id="5fa4c-124">tooconfigure hello integracji eDigitalResearch do usługi Azure AD, należy eDigitalResearch tooadd z hello galerii tooyour listę zarządzanych aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="5fa4c-124">tooconfigure hello integration of eDigitalResearch into Azure AD, you need tooadd eDigitalResearch from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="5fa4c-125">**eDigitalResearch tooadd z galerii hello wykonaj hello następujące kroki:**</span><span class="sxs-lookup"><span data-stu-id="5fa4c-125">**tooadd eDigitalResearch from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="5fa4c-126">W hello  **[portalu Azure](https://portal.azure.com)**na temat hello panelu nawigacji po lewej stronie, kliknij przycisk **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="5fa4c-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![przycisk usługi Azure Active Directory Hello][1]

2. <span data-ttu-id="5fa4c-128">Przejdź za**aplikacje dla przedsiębiorstw**.</span><span class="sxs-lookup"><span data-stu-id="5fa4c-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="5fa4c-129">Następnie przejdź zbyt**wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="5fa4c-129">Then go too**All applications**.</span></span>

    ![Blok aplikacje przedsiębiorstwa Hello][2]
    
3. <span data-ttu-id="5fa4c-131">tooadd nową aplikację, kliknij przycisk **nowej aplikacji** przycisk u góry hello okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="5fa4c-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Nowy przycisk aplikacji Hello][3]

4. <span data-ttu-id="5fa4c-133">W polu wyszukiwania hello wpisz **eDigitalResearch**, wybierz pozycję **eDigitalResearch** z panelu wyników następnie kliknij przycisk **Dodaj** przycisk aplikacji hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="5fa4c-133">In hello search box, type **eDigitalResearch**, select **eDigitalResearch** from result panel then click **Add** button tooadd hello application.</span></span>

    ![eDigitalResearch hello listy wyników](./media/active-directory-saas-edigitalresearch-tutorial/tutorial_edigitalresearch_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="5fa4c-135">Konfiguracja i testowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="5fa4c-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="5fa4c-136">W tej sekcji skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z eDigitalResearch w oparciu o nazwie "Britta Simona" użytkownika testowego.</span><span class="sxs-lookup"><span data-stu-id="5fa4c-136">In this section, you configure and test Azure AD single sign-on with eDigitalResearch based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="5fa4c-137">Dla pojedynczego logowania jednokrotnego toowork usługi Azure AD musi tooknow użytkownika odpowiednikiem hello w eDigitalResearch jest tooa użytkownika w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="5fa4c-137">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in eDigitalResearch is tooa user in Azure AD.</span></span> <span data-ttu-id="5fa4c-138">Innymi słowy relację łącza między użytkownika usługi Azure AD i hello użytkownikowi w eDigitalResearch musi toobe ustanowione.</span><span class="sxs-lookup"><span data-stu-id="5fa4c-138">In other words, a link relationship between an Azure AD user and hello related user in eDigitalResearch needs toobe established.</span></span>

<span data-ttu-id="5fa4c-139">W eDigitalResearch, należy przypisać wartość hello hello **nazwy użytkownika** w usłudze Azure AD jako wartość hello hello **Username** tooestablish hello łącze relacji.</span><span class="sxs-lookup"><span data-stu-id="5fa4c-139">In eDigitalResearch, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="5fa4c-140">tooconfigure i testowych usługi Azure AD rejestracji jednokrotnej z eDigitalResearch, należy po bloków konstrukcyjnych hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="5fa4c-140">tooconfigure and test Azure AD single sign-on with eDigitalResearch, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="5fa4c-141">**[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configure-azure-ad-single-sign-on)**  -tooenable Twojego toouse użytkowników tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="5fa4c-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="5fa4c-142">**[Tworzenie użytkownika testowego usługi Azure AD](#create-an-azure-ad-test-user)**  -tootest usługi Azure AD rejestracji jednokrotnej z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="5fa4c-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="5fa4c-143">**[Tworzenie użytkownika testowego eDigitalResearch](#create-a-edigitalresearch-test-user)**  -toohave odpowiednikiem Simona Britta w eDigitalResearch, który jest połączony toohello usługi Azure AD reprezentację użytkownika.</span><span class="sxs-lookup"><span data-stu-id="5fa4c-143">**[Create a eDigitalResearch test user](#create-a-edigitalresearch-test-user)** - toohave a counterpart of Britta Simon in eDigitalResearch that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="5fa4c-144">**[Przypisz użytkownika testowego hello Azure AD](#assign-the-azure-ad-test-user)**  -tooenable Simona Britta toouse usługi Azure AD rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="5fa4c-144">**[Assign hello Azure AD test user](#assign-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="5fa4c-145">**[Test rejestracji jednokrotnej](#test-single-sign-on)**  tooverify czy hello konfiguracji działania.</span><span class="sxs-lookup"><span data-stu-id="5fa4c-145">**[Test single sign-on](#test-single-sign-on)**  tooverify whether hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="5fa4c-146">Konfigurowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="5fa4c-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="5fa4c-147">W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w portalu Azure hello i skonfigurować logowanie jednokrotne w aplikacji eDigitalResearch.</span><span class="sxs-lookup"><span data-stu-id="5fa4c-147">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your eDigitalResearch application.</span></span>

<span data-ttu-id="5fa4c-148">**tooconfigure usługi Azure AD rejestracji jednokrotnej z eDigitalResearch, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="5fa4c-148">**tooconfigure Azure AD single sign-on with eDigitalResearch, perform hello following steps:**</span></span>

1. <span data-ttu-id="5fa4c-149">W portalu Azure na powitania hello **eDigitalResearch** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.</span><span class="sxs-lookup"><span data-stu-id="5fa4c-149">In hello Azure portal, on hello **eDigitalResearch** application integration page, click **Single sign-on**.</span></span>

    ![Skonfigurować łącze rejestracji jednokrotnej][4]

2. <span data-ttu-id="5fa4c-151">Na powitania **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** tooenable rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="5fa4c-151">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Okno dialogowe rejestracji jednokrotnej](./media/active-directory-saas-edigitalresearch-tutorial/tutorial_edigitalresearch_samlbase.png)

3. <span data-ttu-id="5fa4c-153">Na powitania **eDigitalResearch domeny i adres URL** sekcji, wykonaj następujące kroki hello:</span><span class="sxs-lookup"><span data-stu-id="5fa4c-153">On hello **eDigitalResearch Domain and URLs** section, perform hello following steps:</span></span>

    ![eDigitalResearch domeny i adres URL pojedynczego logowania jednokrotnego informacji](./media/active-directory-saas-edigitalresearch-tutorial/tutorial_edigitalresearch_url.png)

    <span data-ttu-id="5fa4c-155">a.</span><span class="sxs-lookup"><span data-stu-id="5fa4c-155">a.</span></span> <span data-ttu-id="5fa4c-156">W hello **identyfikator** tekstowym, wpisz adres URL za pomocą hello następującego wzorca:`https://<company-name>.edigitalresearch.com`</span><span class="sxs-lookup"><span data-stu-id="5fa4c-156">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<company-name>.edigitalresearch.com`</span></span>

    <span data-ttu-id="5fa4c-157">b.</span><span class="sxs-lookup"><span data-stu-id="5fa4c-157">b.</span></span> <span data-ttu-id="5fa4c-158">W hello **adres URL odpowiedzi** tekstowym, wpisz adres URL za pomocą hello następującego wzorca:`https://<company-name>.edigitalresearch.com/login/consume`</span><span class="sxs-lookup"><span data-stu-id="5fa4c-158">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://<company-name>.edigitalresearch.com/login/consume`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="5fa4c-159">Wartości te nie są prawdziwe.</span><span class="sxs-lookup"><span data-stu-id="5fa4c-159">These values are not real.</span></span> <span data-ttu-id="5fa4c-160">Witaj rzeczywisty identyfikator i odpowiedzi adresu URL, należy zaktualizować te wartości.</span><span class="sxs-lookup"><span data-stu-id="5fa4c-160">Update these values with hello actual Identifier and Reply URL.</span></span> <span data-ttu-id="5fa4c-161">Skontaktuj się z [zespołem pomocy technicznej eDigitalResearch](http://www.maruedr.com/contact) tooget tych wartości.</span><span class="sxs-lookup"><span data-stu-id="5fa4c-161">Contact [eDigitalResearch support team](http://www.maruedr.com/contact) tooget these values.</span></span>
 


4. <span data-ttu-id="5fa4c-162">Na powitania **certyfikat podpisywania SAML** kliknij **Base(64) certyfikatu** , a następnie zapisz plik certyfikatu hello na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="5fa4c-162">On hello **SAML Signing Certificate** section, click **Certificate Base(64)** and then save hello certificate file on your computer.</span></span>

    <span data-ttu-id="5fa4c-163">!</span><span class="sxs-lookup"><span data-stu-id="5fa4c-163">!</span></span>![link do pobierania certyfikatu Hello](./media/active-directory-saas-edigitalresearch-tutorial/tutorial_edigitalresearch_certificate.png) 

5. <span data-ttu-id="5fa4c-165">Kliknij przycisk **zapisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="5fa4c-165">Click **Save** button.</span></span>

    ![Skonfiguruj przycisk pojedynczego logowania jednokrotnego Zapisz](./media/active-directory-saas-edigitalresearch-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="5fa4c-167">Na powitania **eDigitalResearch konfiguracji** kliknij **skonfigurować eDigitalResearch** tooopen **Konfigurowanie logowania jednokrotnego** okna.</span><span class="sxs-lookup"><span data-stu-id="5fa4c-167">On hello **eDigitalResearch Configuration** section, click **Configure eDigitalResearch** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="5fa4c-168">Kopiuj hello **Sign-Out adres URL, identyfikator jednostki SAML** z hello **sekcji krótkimi opisami.**</span><span class="sxs-lookup"><span data-stu-id="5fa4c-168">Copy hello **Sign-Out URL, SAML Entity ID** from hello **Quick Reference section.**</span></span>

    ![eDigitalResearch konfiguracji](./media/active-directory-saas-edigitalresearch-tutorial/tutorial_edigitalresearch_configure.png) 

7. <span data-ttu-id="5fa4c-170">tooconfigure rejestracji jednokrotnej w **eDigitalResearch** strony, należy pobrać hello toosend **plik certyfikatu (Base64)**, **identyfikator jednostki SAML**, i  **Adres URL wylogowania** za[zespołem pomocy technicznej eDigitalResearch](http://www.maruedr.com/contact).</span><span class="sxs-lookup"><span data-stu-id="5fa4c-170">tooconfigure single sign-on on **eDigitalResearch** side, you need toosend hello downloaded **Certificate (Base64) File**, **SAML Entity ID**, and **Sign-Out URL** too[eDigitalResearch support team](http://www.maruedr.com/contact).</span></span> <span data-ttu-id="5fa4c-171">To ustawienie toohave hello prawidłowo po obu stronach połączenia logowania jednokrotnego SAML one ustawić.</span><span class="sxs-lookup"><span data-stu-id="5fa4c-171">They set this setting toohave hello SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="5fa4c-172">Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz hello [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji hello!</span><span class="sxs-lookup"><span data-stu-id="5fa4c-172">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="5fa4c-173">Po dodaniu tej aplikacji z hello **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij hello **rejestracji jednokrotnej** hello kartę i dostępu do osadzonych dokumentacji za pośrednictwem hello  **Konfiguracja** sekcji u dołu hello.</span><span class="sxs-lookup"><span data-stu-id="5fa4c-173">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="5fa4c-174">Więcej o hello osadzonych dokumentacji funkcji w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="5fa4c-174">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="5fa4c-175">Tworzenie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="5fa4c-175">Create an Azure AD test user</span></span>

<span data-ttu-id="5fa4c-176">Celem Hello w tej sekcji jest toocreate użytkownika testowego, w portalu Azure o nazwie Simona Britta hello.</span><span class="sxs-lookup"><span data-stu-id="5fa4c-176">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

   ![Tworzenie użytkownika testowego usługi Azure AD][100]

<span data-ttu-id="5fa4c-178">**toocreate użytkownika testowego w usłudze Azure AD, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="5fa4c-178">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="5fa4c-179">W portalu Azure, w okienku po lewej stronie powitania hello kliknij hello **usługi Azure Active Directory** przycisku.</span><span class="sxs-lookup"><span data-stu-id="5fa4c-179">In hello Azure portal, in hello left pane, click hello **Azure Active Directory** button.</span></span>

    ![przycisk usługi Azure Active Directory Hello](./media/active-directory-saas-edigitalresearch-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="5fa4c-181">toodisplay hello listę użytkowników, przejdź zbyt**użytkowników i grup**, a następnie kliknij przycisk **wszyscy użytkownicy**.</span><span class="sxs-lookup"><span data-stu-id="5fa4c-181">toodisplay hello list of users, go too**Users and groups**, and then click **All users**.</span></span>

    ![Witaj, "Użytkownicy i grupy" i "Wszyscy użytkownicy" łącza](./media/active-directory-saas-edigitalresearch-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="5fa4c-183">Witaj tooopen **użytkownika** okno dialogowe, kliknij przycisk **Dodaj** u góry hello hello **wszyscy użytkownicy** okno dialogowe.</span><span class="sxs-lookup"><span data-stu-id="5fa4c-183">tooopen hello **User** dialog box, click **Add** at hello top of hello **All Users** dialog box.</span></span>

    ![przycisk Dodaj Hello](./media/active-directory-saas-edigitalresearch-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="5fa4c-185">W hello **użytkownika** okna dialogowego wykonaj hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="5fa4c-185">In hello **User** dialog box, perform hello following steps:</span></span>

    ![okno dialogowe Hello użytkownika](./media/active-directory-saas-edigitalresearch-tutorial/create_aaduser_04.png)

    <span data-ttu-id="5fa4c-187">a.</span><span class="sxs-lookup"><span data-stu-id="5fa4c-187">a.</span></span> <span data-ttu-id="5fa4c-188">W hello **nazwa** wpisz **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="5fa4c-188">In hello **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="5fa4c-189">b.</span><span class="sxs-lookup"><span data-stu-id="5fa4c-189">b.</span></span> <span data-ttu-id="5fa4c-190">W hello **nazwy użytkownika** pole typu hello adres e-mail użytkownika Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="5fa4c-190">In hello **User name** box, type hello email address of user Britta Simon.</span></span>

    <span data-ttu-id="5fa4c-191">c.</span><span class="sxs-lookup"><span data-stu-id="5fa4c-191">c.</span></span> <span data-ttu-id="5fa4c-192">Wybierz hello **Pokaż hasło** pole wyboru, a następnie zapisz hello wartość, która jest wyświetlana w hello **hasło** pole.</span><span class="sxs-lookup"><span data-stu-id="5fa4c-192">Select hello **Show Password** check box, and then write down hello value that's displayed in hello **Password** box.</span></span>

    <span data-ttu-id="5fa4c-193">d.</span><span class="sxs-lookup"><span data-stu-id="5fa4c-193">d.</span></span> <span data-ttu-id="5fa4c-194">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="5fa4c-194">Click **Create**.</span></span>
  
### <a name="create-a-edigitalresearch-test-user"></a><span data-ttu-id="5fa4c-195">Tworzenie użytkownika testowego eDigitalResearch</span><span class="sxs-lookup"><span data-stu-id="5fa4c-195">Create a eDigitalResearch test user</span></span>

<span data-ttu-id="5fa4c-196">Celem Hello w tej sekcji jest toocreate użytkownika o nazwie Simona Britta w eDigitalResearch.</span><span class="sxs-lookup"><span data-stu-id="5fa4c-196">hello objective of this section is toocreate a user called Britta Simon in eDigitalResearch.</span></span> 

<span data-ttu-id="5fa4c-197">Praca z hello [zespołem pomocy technicznej eDigitalResearch](http://www.maruedr.com/contact) tooget użytkownicy utworzeni.</span><span class="sxs-lookup"><span data-stu-id="5fa4c-197">Work with hello [eDigitalResearch support team](http://www.maruedr.com/contact) tooget users created.</span></span>       
    
 > [!NOTE]
 > <span data-ttu-id="5fa4c-198">Właściciel konta usługi Azure Active Directory Hello otrzymuje wiadomość e-mail i następuje tooconfirm łącze swojego konta, zanim staje się aktywny.</span><span class="sxs-lookup"><span data-stu-id="5fa4c-198">hello Azure Active Directory account holder receives an email and follows a link tooconfirm their account before it becomes active.</span></span>

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="5fa4c-199">Przypisz użytkownika testowego hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="5fa4c-199">Assign hello Azure AD test user</span></span>

<span data-ttu-id="5fa4c-200">W tej sekcji możesz włączyć toouse Simona Britta Azure logowania jednokrotnego za udzielanie dostępu tooeDigitalResearch.</span><span class="sxs-lookup"><span data-stu-id="5fa4c-200">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooeDigitalResearch.</span></span>

![Przypisanie roli użytkownika hello][200] 

<span data-ttu-id="5fa4c-202">**tooassign tooeDigitalResearch Simona Britta wykonaj hello następujące kroki:**</span><span class="sxs-lookup"><span data-stu-id="5fa4c-202">**tooassign Britta Simon tooeDigitalResearch, perform hello following steps:**</span></span>

1. <span data-ttu-id="5fa4c-203">W portalu Azure hello, otwórz widok aplikacji hello, a następnie przejdź do widoku katalogu toohello i przejść za**aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="5fa4c-203">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Przypisz użytkownika][201] 

2. <span data-ttu-id="5fa4c-205">Z listy aplikacji hello wybierz **eDigitalResearch**.</span><span class="sxs-lookup"><span data-stu-id="5fa4c-205">In hello applications list, select **eDigitalResearch**.</span></span>

    ![łącze eDigitalResearch Hello na liście aplikacji hello](./media/active-directory-saas-edigitalresearch-tutorial/tutorial_edigitalresearch_app.png)  

3. <span data-ttu-id="5fa4c-207">W menu powitania po lewej stronie powitania kliknij **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="5fa4c-207">In hello menu on hello left, click **Users and groups**.</span></span>

    ![łącze "Użytkownicy i grupy" Hello][202]

4. <span data-ttu-id="5fa4c-209">Kliknij przycisk **Dodaj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="5fa4c-209">Click **Add** button.</span></span> <span data-ttu-id="5fa4c-210">Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="5fa4c-210">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Okienko Dodaj przypisania Hello][203]

5. <span data-ttu-id="5fa4c-212">Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** hello listy użytkowników.</span><span class="sxs-lookup"><span data-stu-id="5fa4c-212">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="5fa4c-213">Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="5fa4c-213">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="5fa4c-214">Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="5fa4c-214">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="5fa4c-215">Test rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="5fa4c-215">Test single sign-on</span></span>

<span data-ttu-id="5fa4c-216">W tej sekcji można przetestować konfiguracji usługi Azure AD pojedynczego logowania jednokrotnego przy użyciu hello panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="5fa4c-216">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="5fa4c-217">Po kliknięciu kafelka eDigitalResearch hello w hello Panel dostępu, należy pobrać automatycznie zalogowane tooyour eDigitalResearch aplikacji.</span><span class="sxs-lookup"><span data-stu-id="5fa4c-217">When you click hello eDigitalResearch tile in hello Access Panel, you should get automatically signed-on tooyour eDigitalResearch application.</span></span>
<span data-ttu-id="5fa4c-218">Aby uzyskać więcej informacji na temat panelu dostępu, zobacz [toohello wprowadzenie panelu dostępu](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="5fa4c-218">For more information about the Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="5fa4c-219">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="5fa4c-219">Additional resources</span></span>

* [<span data-ttu-id="5fa4c-220">Lista samouczków dotyczących tooIntegrate aplikacji SaaS w usłudze Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="5fa4c-220">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="5fa4c-221">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="5fa4c-221">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-edigitalresearch-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-edigitalresearch-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-edigitalresearch-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-edigitalresearch-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-edigitalresearch-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-edigitalresearch-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-edigitalresearch-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-edigitalresearch-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-edigitalresearch-tutorial/tutorial_general_203.png

