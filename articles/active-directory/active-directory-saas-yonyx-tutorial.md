---
title: "Samouczek: Integracji Azure Active Directory z przewodników interaktywnych Yonyx | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak tooconfigure logowanie jednokrotne między usługą Azure Active Directory i przewodników interaktywnych Yonyx."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 07db4e01-319b-4cb6-9b93-4577bffd3cbc
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/16/2017
ms.author: jeedes
ms.openlocfilehash: 24e30d243143651b8d32535c76dc300931ae5746
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-yonyx-interactive-guides"></a><span data-ttu-id="585ff-103">Samouczek: Integracji Azure Active Directory z przewodników interaktywnych Yonyx</span><span class="sxs-lookup"><span data-stu-id="585ff-103">Tutorial: Azure Active Directory integration with Yonyx Interactive Guides</span></span>

<span data-ttu-id="585ff-104">Z tego samouczka, dowiesz się, jak toointegrate Yonyx Interactive prowadzi w usłudze Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="585ff-104">In this tutorial, you learn how toointegrate Yonyx Interactive Guides with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="585ff-105">Integracja z usługą Azure AD przewodników interaktywnych Yonyx zapewnia hello następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="585ff-105">Integrating Yonyx Interactive Guides with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="585ff-106">Można kontrolować w usłudze Azure AD, kto ma dostęp tooYonyx przewodników interaktywnych</span><span class="sxs-lookup"><span data-stu-id="585ff-106">You can control in Azure AD who has access tooYonyx Interactive Guides</span></span>
- <span data-ttu-id="585ff-107">Można włączyć użytkownika użytkownicy tooautomatically get zalogowane tooYonyx przewodników interaktywnych (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="585ff-107">You can enable your users tooautomatically get signed-on tooYonyx Interactive Guides (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="585ff-108">Możesz zarządzać kont w jednej centralnej lokalizacji - hello portalu Azure</span><span class="sxs-lookup"><span data-stu-id="585ff-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="585ff-109">Jeśli chcesz tooknow więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="585ff-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="585ff-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="585ff-110">Prerequisites</span></span>

<span data-ttu-id="585ff-111">tooconfigure integracji usługi Azure AD z przewodników interaktywnych Yonyx należy hello następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="585ff-111">tooconfigure Azure AD integration with Yonyx Interactive Guides, you need hello following items:</span></span>

- <span data-ttu-id="585ff-112">Subskrypcję usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="585ff-112">An Azure AD subscription</span></span>
- <span data-ttu-id="585ff-113">Yonyx przewodniki interakcyjne logowanie jednokrotne włączone subskrypcji</span><span class="sxs-lookup"><span data-stu-id="585ff-113">A Yonyx Interactive Guides single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="585ff-114">tootest hello kroków w tym samouczku, zaleca się przy użyciu środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="585ff-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="585ff-115">tootest hello kroki opisane w tym samouczku, należy stosować te zalecenia:</span><span class="sxs-lookup"><span data-stu-id="585ff-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="585ff-116">Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="585ff-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="585ff-117">Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz [uzyskać miesięczna wersja próbna](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="585ff-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="585ff-118">Opis scenariusza</span><span class="sxs-lookup"><span data-stu-id="585ff-118">Scenario description</span></span>
<span data-ttu-id="585ff-119">W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym.</span><span class="sxs-lookup"><span data-stu-id="585ff-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="585ff-120">Scenariusz Hello opisane w tym samouczku składa się z dwóch głównych elementów:</span><span class="sxs-lookup"><span data-stu-id="585ff-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="585ff-121">Dodawanie przewodników interaktywnych Yonyx z galerii hello</span><span class="sxs-lookup"><span data-stu-id="585ff-121">Adding Yonyx Interactive Guides from hello gallery</span></span>
2. <span data-ttu-id="585ff-122">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="585ff-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-yonyx-interactive-guides-from-hello-gallery"></a><span data-ttu-id="585ff-123">Dodawanie przewodników interaktywnych Yonyx z galerii hello</span><span class="sxs-lookup"><span data-stu-id="585ff-123">Adding Yonyx Interactive Guides from hello gallery</span></span>
<span data-ttu-id="585ff-124">tooconfigure hello integracji przewodników interaktywnych Yonyx do usługi Azure AD, należy tooadd Yonyx przewodników interaktywnych z hello galerii tooyour listę zarządzanych aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="585ff-124">tooconfigure hello integration of Yonyx Interactive Guides into Azure AD, you need tooadd Yonyx Interactive Guides from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="585ff-125">**tooadd Yonyx przewodników interaktywnych z galerii hello wykonaj hello następujące kroki:**</span><span class="sxs-lookup"><span data-stu-id="585ff-125">**tooadd Yonyx Interactive Guides from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="585ff-126">W hello  **[portalu Azure](https://portal.azure.com)**na temat hello panelu nawigacji po lewej stronie, kliknij przycisk **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="585ff-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![przycisk usługi Azure Active Directory Hello][1]

2. <span data-ttu-id="585ff-128">Przejdź za**aplikacje dla przedsiębiorstw**.</span><span class="sxs-lookup"><span data-stu-id="585ff-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="585ff-129">Następnie przejdź zbyt**wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="585ff-129">Then go too**All applications**.</span></span>

    ![Blok aplikacje przedsiębiorstwa Hello][2]
    
3. <span data-ttu-id="585ff-131">tooadd nową aplikację, kliknij przycisk **nowej aplikacji** przycisk u góry hello okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="585ff-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Nowy przycisk aplikacji Hello][3]

4. <span data-ttu-id="585ff-133">W polu wyszukiwania hello wpisz **przewodników interaktywnych Yonyx**, wybierz pozycję **przewodników interaktywnych Yonyx** z panelu wyników następnie kliknij przycisk **Dodaj** przycisk aplikacji hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="585ff-133">In hello search box, type **Yonyx Interactive Guides**, select  **Yonyx Interactive Guides**  from result panel then click **Add** button tooadd hello application.</span></span>

    ![Yonyx przewodników interaktywnych hello listy wyników](./media/active-directory-saas-yonyx-tutorial/tutorial_yonyxinteractiveguides_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="585ff-135">Konfiguracja i testowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="585ff-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="585ff-136">W tej sekcji skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z przewodników interaktywnych Yonyx w oparciu o nazwie "Britta Simona" użytkownika testowego.</span><span class="sxs-lookup"><span data-stu-id="585ff-136">In this section, you configure and test Azure AD single sign-on with Yonyx Interactive Guides based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="585ff-137">Dla pojedynczego logowania jednokrotnego toowork usługi Azure AD musi tooknow użytkownika odpowiednikiem hello w przewodnikach interakcyjne Yonyx jest tooa użytkownika w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="585ff-137">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Yonyx Interactive Guides is tooa user in Azure AD.</span></span> <span data-ttu-id="585ff-138">Innymi słowy relację łącza między użytkownika usługi Azure AD i hello użytkownikowi w przewodnikach interakcyjne Yonyx musi toobe ustanowione.</span><span class="sxs-lookup"><span data-stu-id="585ff-138">In other words, a link relationship between an Azure AD user and hello related user in Yonyx Interactive Guides needs toobe established.</span></span>

<span data-ttu-id="585ff-139">W przewodnikach interakcyjne Yonyx, należy przypisać wartość hello hello **nazwy użytkownika** w usłudze Azure AD jako wartość hello hello **Username** tooestablish hello łącze relacji.</span><span class="sxs-lookup"><span data-stu-id="585ff-139">In Yonyx Interactive Guides, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="585ff-140">tooconfigure i testowych usługi Azure AD rejestracji jednokrotnej z przewodników interaktywnych Yonyx, należy po bloków konstrukcyjnych hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="585ff-140">tooconfigure and test Azure AD single sign-on with Yonyx Interactive Guides, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="585ff-141">**[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configure-azure-ad-single-sign-on)**  -tooenable Twojego toouse użytkowników tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="585ff-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="585ff-142">**[Tworzenie użytkownika testowego usługi Azure AD](#create-an-azure-ad-test-user)**  -tootest usługi Azure AD rejestracji jednokrotnej z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="585ff-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="585ff-143">**[Tworzenie użytkownika testowego przewodników interaktywnych Yonyx](#create-a-yonyx-interactive-guides-test-user)**  -toohave odpowiednikiem Simona Britta w Yonyx przewodników interaktywnych, który jest połączony toohello usługi Azure AD reprezentację użytkownika.</span><span class="sxs-lookup"><span data-stu-id="585ff-143">**[Create a Yonyx Interactive Guides test user](#create-a-yonyx-interactive-guides-test-user)** - toohave a counterpart of Britta Simon in Yonyx Interactive Guides that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="585ff-144">**[Przypisz użytkownika testowego hello Azure AD](#assign-the-azure-ad-test-user)**  -tooenable Simona Britta toouse usługi Azure AD rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="585ff-144">**[Assign hello Azure AD test user](#assign-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="585ff-145">**[Test rejestracji jednokrotnej](#test-single-sign-on)**  -tooverify czy hello konfiguracji działania.</span><span class="sxs-lookup"><span data-stu-id="585ff-145">**[Test single sign-on](#test-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="585ff-146">Konfigurowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="585ff-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="585ff-147">W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w portalu Azure hello i skonfigurować logowanie jednokrotne w aplikacji przewodników interaktywnych Yonyx.</span><span class="sxs-lookup"><span data-stu-id="585ff-147">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Yonyx Interactive Guides application.</span></span>

<span data-ttu-id="585ff-148">**tooconfigure usługi Azure AD rejestracji jednokrotnej z przewodników interaktywnych Yonyx, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="585ff-148">**tooconfigure Azure AD single sign-on with Yonyx Interactive Guides, perform hello following steps:**</span></span>

1. <span data-ttu-id="585ff-149">W portalu Azure na powitania hello **przewodników interaktywnych Yonyx** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.</span><span class="sxs-lookup"><span data-stu-id="585ff-149">In hello Azure portal, on hello **Yonyx Interactive Guides** application integration page, click **Single sign-on**.</span></span>

    ![Skonfigurować łącze rejestracji jednokrotnej][4]

2. <span data-ttu-id="585ff-151">Na powitania **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** tooenable rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="585ff-151">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Okno dialogowe rejestracji jednokrotnej](./media/active-directory-saas-yonyx-tutorial/tutorial_yonyxinteractiveguides_samlbase.png)

3. <span data-ttu-id="585ff-153">Na powitania **Yonyx interakcyjne przewodniki domeny i adres URL** sekcji, wykonaj następujące kroki hello:</span><span class="sxs-lookup"><span data-stu-id="585ff-153">On hello **Yonyx Interactive Guides Domain and URLs** section, perform hello following steps:</span></span>

    ![Yonyx interakcyjne przewodniki domeny i adres URL z jednym informacje logowania jednokrotnego](./media/active-directory-saas-yonyx-tutorial/tutorial_yonyxinteractiveguides_url.png)

    <span data-ttu-id="585ff-155">a.</span><span class="sxs-lookup"><span data-stu-id="585ff-155">a.</span></span> <span data-ttu-id="585ff-156">W hello **adres URL logowania** tekstowym, wpisz adres URL za pomocą hello następującego wzorca:`https://<company name>.yonyx.com/y/conversation/?id=<guid number>`</span><span class="sxs-lookup"><span data-stu-id="585ff-156">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<company name>.yonyx.com/y/conversation/?id=<guid number>`</span></span>

    <span data-ttu-id="585ff-157">b.</span><span class="sxs-lookup"><span data-stu-id="585ff-157">b.</span></span> <span data-ttu-id="585ff-158">W hello **identyfikator** tekstowym, wpisz adres URL za pomocą hello następującego wzorca:`https://<company name>.yonyx.com`</span><span class="sxs-lookup"><span data-stu-id="585ff-158">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<company name>.yonyx.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="585ff-159">Wartości te nie są prawdziwe.</span><span class="sxs-lookup"><span data-stu-id="585ff-159">These values are not real.</span></span> <span data-ttu-id="585ff-160">Zaktualizować te wartości z hello rzeczywisty adres URL logowania i identyfikator.</span><span class="sxs-lookup"><span data-stu-id="585ff-160">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="585ff-161">Skontaktuj się z [zespołem pomocy technicznej Yonyx interakcyjne przewodników klienta](mailto:support@yonyx.com) tooget tych wartości.</span><span class="sxs-lookup"><span data-stu-id="585ff-161">Contact [Yonyx Interactive Guides Client support team](mailto:support@yonyx.com) tooget these values.</span></span> 
 
4. <span data-ttu-id="585ff-162">Na powitania **certyfikat podpisywania SAML** kliknij **Certificate(Base64)** , a następnie zapisz plik certyfikatu hello na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="585ff-162">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![link do pobierania certyfikatu Hello](./media/active-directory-saas-yonyx-tutorial/tutorial_yonyxinteractiveguides_certificate.png) 

5. <span data-ttu-id="585ff-164">Kliknij przycisk **zapisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="585ff-164">Click **Save** button.</span></span>

    ![Skonfiguruj przycisk pojedynczego logowania jednokrotnego Zapisz](./media/active-directory-saas-yonyx-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="585ff-166">Na powitania **Yonyx interakcyjne przewodniki konfiguracji** kliknij **skonfigurować przewodników interaktywnych Yonyx** tooopen **Konfigurowanie logowania jednokrotnego** okna.</span><span class="sxs-lookup"><span data-stu-id="585ff-166">On hello **Yonyx Interactive Guides Configuration** section, click **Configure Yonyx Interactive Guides** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="585ff-167">Kopiuj hello **Sign-Out adres URL, identyfikator jednostki SAML i SAML pojedynczy znak na adres URL usługi** z hello **sekcji krótkimi opisami.**</span><span class="sxs-lookup"><span data-stu-id="585ff-167">Copy hello **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Yonyx interakcyjne przewodniki konfiguracji](./media/active-directory-saas-yonyx-tutorial/tutorial_yonyxinteractiveguides_configure.png) 

7. <span data-ttu-id="585ff-169">tooconfigure rejestracji jednokrotnej w **przewodników interaktywnych Yonyx** strony, należy pobrać hello toosend **Certificate(Base64)**, **Sign-Out URL**, **SAML Pojedynczy adres URL logowania jednokrotnego usługi** **identyfikator jednostki SAML** za[zespołu obsługi przewodników interaktywnych Yonyx](mailto:support@yonyx.com).</span><span class="sxs-lookup"><span data-stu-id="585ff-169">tooconfigure single sign-on on **Yonyx Interactive Guides** side, you need toosend hello downloaded **Certificate(Base64)**, **Sign-Out URL**, **SAML Single Sign-On Service URL** **SAML Entity ID** too[Yonyx Interactive Guides support team](mailto:support@yonyx.com).</span></span> <span data-ttu-id="585ff-170">To ustawienie toohave hello prawidłowo po obu stronach połączenia logowania jednokrotnego SAML one ustawić.</span><span class="sxs-lookup"><span data-stu-id="585ff-170">They set this setting toohave hello SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="585ff-171">Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz hello [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji hello!</span><span class="sxs-lookup"><span data-stu-id="585ff-171">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="585ff-172">Po dodaniu tej aplikacji z hello **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij hello **rejestracji jednokrotnej** hello kartę i dostępu do osadzonych dokumentacji za pośrednictwem hello  **Konfiguracja** sekcji u dołu hello.</span><span class="sxs-lookup"><span data-stu-id="585ff-172">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="585ff-173">Więcej o hello osadzonych dokumentacji funkcji w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="585ff-173">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>


### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="585ff-174">Tworzenie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="585ff-174">Create an Azure AD test user</span></span>

<span data-ttu-id="585ff-175">Celem Hello w tej sekcji jest toocreate użytkownika testowego, w portalu Azure o nazwie Simona Britta hello.</span><span class="sxs-lookup"><span data-stu-id="585ff-175">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

  ![Tworzenie użytkownika testowego usługi Azure AD][100]

<span data-ttu-id="585ff-177">**toocreate użytkownika testowego w usłudze Azure AD, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="585ff-177">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="585ff-178">W hello **portalu Azure**na temat hello w lewym okienku nawigacji, kliknij przycisk **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="585ff-178">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![przycisk usługi Azure Active Directory Hello](./media/active-directory-saas-yonyx-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="585ff-180">toodisplay hello listę użytkowników, przejdź zbyt**użytkowników i grup** i kliknij przycisk **wszyscy użytkownicy**.</span><span class="sxs-lookup"><span data-stu-id="585ff-180">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Witaj, "Użytkownicy i grupy" i "Wszyscy użytkownicy" łącza](./media/active-directory-saas-yonyx-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="585ff-182">Witaj tooopen **użytkownika** okna dialogowego, kliknij przycisk **Dodaj** u góry hello hello okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="585ff-182">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![przycisk Dodaj Hello](./media/active-directory-saas-yonyx-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="585ff-184">Na powitania **użytkownika** okna dialogowego wykonaj hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="585ff-184">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![okno dialogowe Hello użytkownika](./media/active-directory-saas-yonyx-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="585ff-186">a.</span><span class="sxs-lookup"><span data-stu-id="585ff-186">a.</span></span> <span data-ttu-id="585ff-187">W hello **nazwa** pole tekstowe, typ **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="585ff-187">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="585ff-188">b.</span><span class="sxs-lookup"><span data-stu-id="585ff-188">b.</span></span> <span data-ttu-id="585ff-189">W hello **nazwy użytkownika** pole tekstowe, hello typu **adres e-mail** z BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="585ff-189">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="585ff-190">c.</span><span class="sxs-lookup"><span data-stu-id="585ff-190">c.</span></span> <span data-ttu-id="585ff-191">Wybierz **Pokaż hasło** i zanotuj wartość hello hello **hasło**.</span><span class="sxs-lookup"><span data-stu-id="585ff-191">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="585ff-192">d.</span><span class="sxs-lookup"><span data-stu-id="585ff-192">d.</span></span> <span data-ttu-id="585ff-193">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="585ff-193">Click **Create**.</span></span>
 
### <a name="create-a-yonyx-interactive-guides-test-user"></a><span data-ttu-id="585ff-194">Tworzenie użytkownika testowego przewodników interaktywnych Yonyx</span><span class="sxs-lookup"><span data-stu-id="585ff-194">Create a Yonyx Interactive Guides test user</span></span>

<span data-ttu-id="585ff-195">Celem Hello w tej sekcji jest toocreate użytkownika o nazwie Simona Britta Yonyx przewodników interakcyjne.</span><span class="sxs-lookup"><span data-stu-id="585ff-195">hello objective of this section is toocreate a user called Britta Simon in Yonyx Interactive Guides.</span></span> <span data-ttu-id="585ff-196">Przewodniki interakcyjne Yonyx obsługę w czasie, który jest domyślnie włączone.</span><span class="sxs-lookup"><span data-stu-id="585ff-196">Yonyx Interactive Guides supports just-in-time provisioning, which is by default enabled.</span></span>

<span data-ttu-id="585ff-197">Nie ma elementu akcji można w tej sekcji.</span><span class="sxs-lookup"><span data-stu-id="585ff-197">There is no action item for you in this section.</span></span> <span data-ttu-id="585ff-198">Nowy użytkownik został utworzony podczas tooaccess próba Yonyx przewodników interaktywnych, jeśli go jeszcze nie istnieje.</span><span class="sxs-lookup"><span data-stu-id="585ff-198">A new user is created during an attempt tooaccess Yonyx Interactive Guides if it doesn't exist yet.</span></span>

>[!NOTE]
><span data-ttu-id="585ff-199">Jeśli należy ręcznie toocreate użytkownika, należy hello toocontact przewodników interaktywnych Yonyx obsługuje zespołu za pomocą < mailto:support@yonyx.com >.</span><span class="sxs-lookup"><span data-stu-id="585ff-199">If you need toocreate a user manually, you need toocontact hello Yonyx Interactive Guides support team via <mailto:support@yonyx.com>.</span></span> 

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="585ff-200">Przypisz użytkownika testowego hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="585ff-200">Assign hello Azure AD test user</span></span>

<span data-ttu-id="585ff-201">W tej sekcji możesz włączyć toouse Simona Britta Azure logowania jednokrotnego za udzielanie dostępu tooYonyx przewodników interaktywnych.</span><span class="sxs-lookup"><span data-stu-id="585ff-201">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooYonyx Interactive Guides.</span></span>

![Przypisanie roli użytkownika hello][200]

<span data-ttu-id="585ff-203">**tooassign Simona Britta tooYonyx przewodników interaktywnych, wykonaj hello następujące kroki:**</span><span class="sxs-lookup"><span data-stu-id="585ff-203">**tooassign Britta Simon tooYonyx Interactive Guides, perform hello following steps:**</span></span>

1. <span data-ttu-id="585ff-204">W portalu Azure hello, otwórz widok aplikacji hello, a następnie przejdź do widoku katalogu toohello i przejść za**aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="585ff-204">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Przypisz użytkownika][201] 

2. <span data-ttu-id="585ff-206">Z listy aplikacji hello wybierz **przewodników interaktywnych Yonyx**.</span><span class="sxs-lookup"><span data-stu-id="585ff-206">In hello applications list, select **Yonyx Interactive Guides**.</span></span>

    ![łącze przewodników interaktywnych Yonyx Hello na liście aplikacji hello](./media/active-directory-saas-yonyx-tutorial/tutorial_yonyxinteractiveguides_app.png) 

3. <span data-ttu-id="585ff-208">W menu powitania po lewej stronie powitania kliknij **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="585ff-208">In hello menu on hello left, click **Users and groups**.</span></span>

    ![łącze "Użytkownicy i grupy" Hello][202]

4. <span data-ttu-id="585ff-210">Kliknij przycisk **Dodaj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="585ff-210">Click **Add** button.</span></span> <span data-ttu-id="585ff-211">Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="585ff-211">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Okienko Dodaj przypisania Hello][203]

5. <span data-ttu-id="585ff-213">Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** hello listy użytkowników.</span><span class="sxs-lookup"><span data-stu-id="585ff-213">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="585ff-214">Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="585ff-214">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="585ff-215">Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="585ff-215">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="585ff-216">Test rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="585ff-216">Test single sign-on</span></span>

<span data-ttu-id="585ff-217">W tej sekcji można przetestować konfiguracji usługi Azure AD pojedynczego logowania jednokrotnego przy użyciu hello panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="585ff-217">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="585ff-218">Po kliknięciu powitalne przewodników interaktywnych Yonyx kafelka w hello Panel dostępu, należy pobrać automatycznie zalogowane tooyour przewodników interaktywnych Yonyx aplikacji.</span><span class="sxs-lookup"><span data-stu-id="585ff-218">When you click hello Yonyx Interactive Guides tile in hello Access Panel, you should get automatically signed-on tooyour Yonyx Interactive Guides application.</span></span>

<span data-ttu-id="585ff-219">Aby uzyskać więcej informacji na temat hello Panel dostępu, zobacz [toohello wprowadzenie panelu dostępu](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="585ff-219">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="585ff-220">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="585ff-220">Additional resources</span></span>

* [<span data-ttu-id="585ff-221">Lista samouczków dotyczących tooIntegrate aplikacji SaaS w usłudze Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="585ff-221">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="585ff-222">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="585ff-222">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-yonyx-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-yonyx-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-yonyx-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-yonyx-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-yonyx-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-yonyx-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-yonyx-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-yonyx-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-yonyx-tutorial/tutorial_general_203.png

