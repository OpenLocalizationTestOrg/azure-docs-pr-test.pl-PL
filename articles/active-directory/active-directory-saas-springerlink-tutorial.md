---
title: "Samouczek: Integracji Azure Active Directory z łączem Springer | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak tooconfigure logowanie jednokrotne między usługą Azure Active Directory i Springer łącza."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 58cdf029-bdc0-43c4-a469-b921c2a669bd
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/03/2017
ms.author: jeedes
ms.openlocfilehash: dabd2f72b3a195fc359826a4863a197e5019f5c1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-springer-link"></a><span data-ttu-id="d85b4-103">Samouczek: Integracji Azure Active Directory z łączem Springer</span><span class="sxs-lookup"><span data-stu-id="d85b4-103">Tutorial: Azure Active Directory integration with Springer Link</span></span>

<span data-ttu-id="d85b4-104">Z tego samouczka, dowiesz się, jak toointegrate Springer połączyć z usługą Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="d85b4-104">In this tutorial, you learn how toointegrate Springer Link with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="d85b4-105">Integrowanie Springer łącza z usługą Azure AD zapewnia hello następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="d85b4-105">Integrating Springer Link with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="d85b4-106">Można kontrolować w usłudze Azure AD, kto ma dostęp tooSpringer łącza.</span><span class="sxs-lookup"><span data-stu-id="d85b4-106">You can control in Azure AD who has access tooSpringer Link.</span></span>
- <span data-ttu-id="d85b4-107">Można włączyć użytkownika użytkownicy tooautomatically get zalogowane tooSpringer łącza (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="d85b4-107">You can enable your users tooautomatically get signed-on tooSpringer Link (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="d85b4-108">Możesz zarządzać kont w jednej centralnej lokalizacji - hello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="d85b4-108">You can manage your accounts in one central location - hello Azure portal.</span></span>

<span data-ttu-id="d85b4-109">Jeśli chcesz tooknow więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="d85b4-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d85b4-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="d85b4-110">Prerequisites</span></span>

<span data-ttu-id="d85b4-111">tooconfigure integracji usługi Azure AD z łączem Springer należy hello następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="d85b4-111">tooconfigure Azure AD integration with Springer Link, you need hello following items:</span></span>

- <span data-ttu-id="d85b4-112">Subskrypcję usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="d85b4-112">An Azure AD subscription</span></span>
- <span data-ttu-id="d85b4-113">Łącze Springer logowanie jednokrotne włączone subskrypcji</span><span class="sxs-lookup"><span data-stu-id="d85b4-113">A Springer Link single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="d85b4-114">tootest hello kroków w tym samouczku, zaleca się przy użyciu środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="d85b4-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="d85b4-115">tootest hello kroki opisane w tym samouczku, należy stosować te zalecenia:</span><span class="sxs-lookup"><span data-stu-id="d85b4-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="d85b4-116">Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="d85b4-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="d85b4-117">Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz [uzyskać miesięczna wersja próbna](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="d85b4-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="d85b4-118">Opis scenariusza</span><span class="sxs-lookup"><span data-stu-id="d85b4-118">Scenario description</span></span>
<span data-ttu-id="d85b4-119">W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym.</span><span class="sxs-lookup"><span data-stu-id="d85b4-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="d85b4-120">Scenariusz Hello opisane w tym samouczku składa się z dwóch głównych elementów:</span><span class="sxs-lookup"><span data-stu-id="d85b4-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="d85b4-121">Dodanie Springer łącza z galerii hello</span><span class="sxs-lookup"><span data-stu-id="d85b4-121">Adding Springer Link from hello gallery</span></span>
2. <span data-ttu-id="d85b4-122">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="d85b4-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-springer-link-from-hello-gallery"></a><span data-ttu-id="d85b4-123">Dodanie Springer łącza z galerii hello</span><span class="sxs-lookup"><span data-stu-id="d85b4-123">Adding Springer Link from hello gallery</span></span>
<span data-ttu-id="d85b4-124">tooconfigure hello integracji Springer łącze do usługi Azure AD, należy tooadd Springer łącza z hello galerii tooyour listę zarządzanych aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="d85b4-124">tooconfigure hello integration of Springer Link into Azure AD, you need tooadd Springer Link from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="d85b4-125">**tooadd Springer łącza z galerii hello wykonaj hello następujące kroki:**</span><span class="sxs-lookup"><span data-stu-id="d85b4-125">**tooadd Springer Link from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="d85b4-126">W hello  **[portalu Azure](https://portal.azure.com)**na temat hello panelu nawigacji po lewej stronie, kliknij przycisk **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="d85b4-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![przycisk usługi Azure Active Directory Hello][1]

2. <span data-ttu-id="d85b4-128">Przejdź za**aplikacje dla przedsiębiorstw**.</span><span class="sxs-lookup"><span data-stu-id="d85b4-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="d85b4-129">Następnie przejdź zbyt**wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="d85b4-129">Then go too**All applications**.</span></span>

    ![Blok aplikacje przedsiębiorstwa Hello][2]
    
3. <span data-ttu-id="d85b4-131">tooadd nową aplikację, kliknij przycisk **nowej aplikacji** przycisk u góry hello okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="d85b4-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Nowy przycisk aplikacji Hello][3]

4. <span data-ttu-id="d85b4-133">W hello wyszukiwania wpisz **Springer łącze**, wybierz pozycję **Springer łącze** z panelu wyników kliknięcie **Dodaj** przycisk aplikacji hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="d85b4-133">In hello search box, type **Springer Link**, select **Springer Link** from result panel then click **Add** button tooadd hello application.</span></span>

    ![Łącze Springer hello listy wyników](./media/active-directory-saas-springerlink-tutorial/tutorial_springerlink_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="d85b4-135">Konfiguracja i testowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="d85b4-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="d85b4-136">W tej sekcji skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z łączem Springer w oparciu o nazwie "Britta Simona" użytkownika testowego.</span><span class="sxs-lookup"><span data-stu-id="d85b4-136">In this section, you configure and test Azure AD single sign-on with Springer Link based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="d85b4-137">Dla pojedynczego logowania jednokrotnego toowork usługi Azure AD musi tooknow użytkownika odpowiednikiem hello Springer łącza jest tooa użytkownika w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="d85b4-137">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Springer Link is tooa user in Azure AD.</span></span> <span data-ttu-id="d85b4-138">Innymi słowy relację łącza między użytkownika usługi Azure AD i hello użytkownikowi łącza Springer musi toobe ustanowione.</span><span class="sxs-lookup"><span data-stu-id="d85b4-138">In other words, a link relationship between an Azure AD user and hello related user in Springer Link needs toobe established.</span></span>

<span data-ttu-id="d85b4-139">Łącza Springer przypisać wartość hello hello **nazwy użytkownika** w usłudze Azure AD jako wartość hello hello **Username** tooestablish hello łącze relacji.</span><span class="sxs-lookup"><span data-stu-id="d85b4-139">In Springer Link, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="d85b4-140">tooconfigure i testowych usługi Azure AD rejestracji jednokrotnej z łączem Springer, należy po bloków konstrukcyjnych hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="d85b4-140">tooconfigure and test Azure AD single sign-on with Springer Link, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="d85b4-141">**[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configure-azure-ad-single-sign-on)**  -tooenable Twojego toouse użytkowników tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="d85b4-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="d85b4-142">**[Tworzenie użytkownika testowego usługi Azure AD](#create-an-azure-ad-test-user)**  -tootest usługi Azure AD rejestracji jednokrotnej z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="d85b4-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="d85b4-143">**[Przypisz użytkownika testowego hello Azure AD](#assign-the-azure-ad-test-user)**  -tooenable Simona Britta toouse usługi Azure AD rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="d85b4-143">**[Assign hello Azure AD test user](#assign-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
4. <span data-ttu-id="d85b4-144">**[Test rejestracji jednokrotnej](#test-single-sign-on)**  -tooverify czy hello konfiguracji działania.</span><span class="sxs-lookup"><span data-stu-id="d85b4-144">**[Test single sign-on](#test-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="d85b4-145">Konfigurowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="d85b4-145">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="d85b4-146">W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w hello portalu Azure i skonfigurować rejestracji jednokrotnej w aplikacji Springer łącza.</span><span class="sxs-lookup"><span data-stu-id="d85b4-146">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Springer Link application.</span></span>

<span data-ttu-id="d85b4-147">**tooconfigure usługi Azure AD rejestracji jednokrotnej z łączem Springer wykonaj hello następujące kroki:**</span><span class="sxs-lookup"><span data-stu-id="d85b4-147">**tooconfigure Azure AD single sign-on with Springer Link, perform hello following steps:**</span></span>

1. <span data-ttu-id="d85b4-148">W portalu Azure na powitania hello **łącze Springer** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.</span><span class="sxs-lookup"><span data-stu-id="d85b4-148">In hello Azure portal, on hello **Springer Link** application integration page, click **Single sign-on**.</span></span>

    ![Skonfigurować łącze rejestracji jednokrotnej][4]

2. <span data-ttu-id="d85b4-150">Na powitania **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** tooenable rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="d85b4-150">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Okno dialogowe rejestracji jednokrotnej](./media/active-directory-saas-springerlink-tutorial/tutorial_springerlink_samlbase.png)

3. <span data-ttu-id="d85b4-152">Na powitania **Springer łącze domeny i adres URL** sekcji, jeśli chcesz, aby aplikacja hello tooconfigure w **IDP** inicjowane tryb:</span><span class="sxs-lookup"><span data-stu-id="d85b4-152">On hello **Springer Link Domain and URLs** section,  If you wish tooconfigure hello application in **IDP** initiated mode:</span></span>

    ![Adresy URL i Springer łącze domeny pojedynczy informacje logowania jednokrotnego](./media/active-directory-saas-springerlink-tutorial/tutorial_springerlink_url1.png)

    <span data-ttu-id="d85b4-154">a.</span><span class="sxs-lookup"><span data-stu-id="d85b4-154">a.</span></span> <span data-ttu-id="d85b4-155">W hello **identyfikator** pole tekstowe, wprowadź adres URL hello:`https://fsso.springer.com`</span><span class="sxs-lookup"><span data-stu-id="d85b4-155">In hello **Identifier** textbox, type hello URL: `https://fsso.springer.com`</span></span>

    <span data-ttu-id="d85b4-156">b.</span><span class="sxs-lookup"><span data-stu-id="d85b4-156">b.</span></span> <span data-ttu-id="d85b4-157">W hello **adres URL odpowiedzi** pole tekstowe, wprowadź adres URL hello:`https://fsso-qa1.springer.com/federation/Consumer/metaAlias/SpringerServiceProvider`</span><span class="sxs-lookup"><span data-stu-id="d85b4-157">In hello **Reply URL** textbox, type hello URL: `https://fsso-qa1.springer.com/federation/Consumer/metaAlias/SpringerServiceProvider`</span></span>    

4. <span data-ttu-id="d85b4-158">Sprawdź **Pokaż zaawansowane ustawienia adresu URL**.</span><span class="sxs-lookup"><span data-stu-id="d85b4-158">Check **Show advanced URL settings**.</span></span> <span data-ttu-id="d85b4-159">Jeśli chcesz, aby aplikacja hello tooconfigure w **SP** inicjowane tryb:</span><span class="sxs-lookup"><span data-stu-id="d85b4-159">If you wish tooconfigure hello application in **SP** initiated mode:</span></span>

    ![Adresy URL i Springer łącze domeny pojedynczy informacje logowania jednokrotnego](./media/active-directory-saas-springerlink-tutorial/tutorial_springerlink_url.png)

    <span data-ttu-id="d85b4-161">W hello **adres URL logowania** pole tekstowe, wprowadź adres URL hello:`https://fsso.springer.com/federation/Consumer/metaAlias/SpringerServiceProvider`</span><span class="sxs-lookup"><span data-stu-id="d85b4-161">In hello **Sign-on URL** textbox, type hello URL : `https://fsso.springer.com/federation/Consumer/metaAlias/SpringerServiceProvider`</span></span>    

5. <span data-ttu-id="d85b4-162">Kliknij przycisk **zapisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="d85b4-162">Click **Save** button.</span></span>

    ![Skonfiguruj przycisk pojedynczego logowania jednokrotnego Zapisz](./media/active-directory-saas-springerlink-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="d85b4-164">Witaj toogenerate **metadanych** adres url, wykonaj następujące kroki hello:</span><span class="sxs-lookup"><span data-stu-id="d85b4-164">toogenerate hello **Metadata** url, perform hello following steps:</span></span>

    <span data-ttu-id="d85b4-165">a.</span><span class="sxs-lookup"><span data-stu-id="d85b4-165">a.</span></span> <span data-ttu-id="d85b4-166">Kliknij przycisk **rejestracji aplikacji**.</span><span class="sxs-lookup"><span data-stu-id="d85b4-166">Click **App registrations**.</span></span>
    
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-springerlink-tutorial/tutorial_springerlink_appregistrations.png)
   
    <span data-ttu-id="d85b4-168">b.</span><span class="sxs-lookup"><span data-stu-id="d85b4-168">b.</span></span> <span data-ttu-id="d85b4-169">Kliknij przycisk **punkty końcowe** tooopen **punkty końcowe** okno dialogowe.</span><span class="sxs-lookup"><span data-stu-id="d85b4-169">Click **Endpoints** tooopen **Endpoints** dialog box.</span></span>  
    
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-springerlink-tutorial/tutorial_springerlink_endpointicon.png)

    <span data-ttu-id="d85b4-171">c.</span><span class="sxs-lookup"><span data-stu-id="d85b4-171">c.</span></span> <span data-ttu-id="d85b4-172">Kliknij przycisk toocopy przycisku Kopiuj hello **dokument METADANYCH usług FEDERACYJNYCH** adresu url i wklej go do Notatnika.</span><span class="sxs-lookup"><span data-stu-id="d85b4-172">Click hello copy button toocopy **FEDERATION METADATA DOCUMENT** url and paste it into notepad.</span></span>
    
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-springerlink-tutorial/tutorial_springerlink_endpoint.png)
     
    <span data-ttu-id="d85b4-174">d.</span><span class="sxs-lookup"><span data-stu-id="d85b4-174">d.</span></span> <span data-ttu-id="d85b4-175">Teraz przejdź strony właściwości toohello **Springer łącze** i hello kopii **identyfikator aplikacji** przy użyciu **kopiowania** przycisk i wklej go do Notatnika.</span><span class="sxs-lookup"><span data-stu-id="d85b4-175">Now go toohello property page of **Springer Link** and copy hello **Application Id** using **Copy** button and paste it into notepad.</span></span>
 
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-springerlink-tutorial/tutorial_springerlink_appid.png)

    <span data-ttu-id="d85b4-177">e.</span><span class="sxs-lookup"><span data-stu-id="d85b4-177">e.</span></span> <span data-ttu-id="d85b4-178">Generowanie hello **adres URL metadanych** przy użyciu hello następującego wzorca:`<FEDERATION METADATA DOCUMENT url>?appid=<application id>`</span><span class="sxs-lookup"><span data-stu-id="d85b4-178">Generate hello **Metadata URL** using hello following pattern: `<FEDERATION METADATA DOCUMENT url>?appid=<application id>`</span></span>

7. <span data-ttu-id="d85b4-179">tooconfigure rejestracji jednokrotnej w **Springer łącze** strony, należy hello toosend wygenerowany **adres URL metadanych** za[zespołem pomocy technicznej Springer łącze](mailto:identity@springernature.com).</span><span class="sxs-lookup"><span data-stu-id="d85b4-179">tooconfigure single sign-on on **Springer Link** side, you need toosend hello generated **Metadata URL** too[Springer Link support team](mailto:identity@springernature.com).</span></span>

> [!TIP]
> <span data-ttu-id="d85b4-180">Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz hello [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji hello!</span><span class="sxs-lookup"><span data-stu-id="d85b4-180">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="d85b4-181">Po dodaniu tej aplikacji z hello **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij hello **rejestracji jednokrotnej** hello kartę i dostępu do osadzonych dokumentacji za pośrednictwem hello  **Konfiguracja** sekcji u dołu hello.</span><span class="sxs-lookup"><span data-stu-id="d85b4-181">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="d85b4-182">Więcej o hello osadzonych dokumentacji funkcji w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="d85b4-182">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>


### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="d85b4-183">Tworzenie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="d85b4-183">Create an Azure AD test user</span></span>

<span data-ttu-id="d85b4-184">Celem Hello w tej sekcji jest toocreate użytkownika testowego, w portalu Azure o nazwie Simona Britta hello.</span><span class="sxs-lookup"><span data-stu-id="d85b4-184">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

   ![Tworzenie użytkownika testowego usługi Azure AD][100]

<span data-ttu-id="d85b4-186">**toocreate użytkownika testowego w usłudze Azure AD, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="d85b4-186">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="d85b4-187">W portalu Azure, w okienku po lewej stronie powitania hello kliknij hello **usługi Azure Active Directory** przycisku.</span><span class="sxs-lookup"><span data-stu-id="d85b4-187">In hello Azure portal, in hello left pane, click hello **Azure Active Directory** button.</span></span>

    ![przycisk usługi Azure Active Directory Hello](./media/active-directory-saas-springerlink-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="d85b4-189">toodisplay hello listę użytkowników, przejdź zbyt**użytkowników i grup**, a następnie kliknij przycisk **wszyscy użytkownicy**.</span><span class="sxs-lookup"><span data-stu-id="d85b4-189">toodisplay hello list of users, go too**Users and groups**, and then click **All users**.</span></span>

    ![Witaj, "Użytkownicy i grupy" i "Wszyscy użytkownicy" łącza](./media/active-directory-saas-springerlink-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="d85b4-191">Witaj tooopen **użytkownika** okno dialogowe, kliknij przycisk **Dodaj** u góry hello hello **wszyscy użytkownicy** okno dialogowe.</span><span class="sxs-lookup"><span data-stu-id="d85b4-191">tooopen hello **User** dialog box, click **Add** at hello top of hello **All Users** dialog box.</span></span>

    ![przycisk Dodaj Hello](./media/active-directory-saas-springerlink-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="d85b4-193">W hello **użytkownika** okna dialogowego wykonaj hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="d85b4-193">In hello **User** dialog box, perform hello following steps:</span></span>

    ![okno dialogowe Hello użytkownika](./media/active-directory-saas-springerlink-tutorial/create_aaduser_04.png)

    <span data-ttu-id="d85b4-195">a.</span><span class="sxs-lookup"><span data-stu-id="d85b4-195">a.</span></span> <span data-ttu-id="d85b4-196">W hello **nazwa** wpisz **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="d85b4-196">In hello **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="d85b4-197">b.</span><span class="sxs-lookup"><span data-stu-id="d85b4-197">b.</span></span> <span data-ttu-id="d85b4-198">W hello **nazwy użytkownika** pole typu hello adres e-mail użytkownika Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="d85b4-198">In hello **User name** box, type hello email address of user Britta Simon.</span></span>

    <span data-ttu-id="d85b4-199">c.</span><span class="sxs-lookup"><span data-stu-id="d85b4-199">c.</span></span> <span data-ttu-id="d85b4-200">Wybierz hello **Pokaż hasło** pole wyboru, a następnie zapisz hello wartość, która jest wyświetlana w hello **hasło** pole.</span><span class="sxs-lookup"><span data-stu-id="d85b4-200">Select hello **Show Password** check box, and then write down hello value that's displayed in hello **Password** box.</span></span>

    <span data-ttu-id="d85b4-201">d.</span><span class="sxs-lookup"><span data-stu-id="d85b4-201">d.</span></span> <span data-ttu-id="d85b4-202">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="d85b4-202">Click **Create**.</span></span>
 
### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="d85b4-203">Przypisz użytkownika testowego hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="d85b4-203">Assign hello Azure AD test user</span></span>

<span data-ttu-id="d85b4-204">W tej sekcji możesz włączyć toouse Simona Britta Azure logowania jednokrotnego za udzielanie dostępu tooSpringer łącza.</span><span class="sxs-lookup"><span data-stu-id="d85b4-204">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooSpringer Link.</span></span>

![Przypisanie roli użytkownika hello][200] 

<span data-ttu-id="d85b4-206">**tooassign tooSpringer Simona Britta łącza, należy wykonać hello następujące kroki:**</span><span class="sxs-lookup"><span data-stu-id="d85b4-206">**tooassign Britta Simon tooSpringer Link, perform hello following steps:**</span></span>

1. <span data-ttu-id="d85b4-207">W portalu Azure hello, otwórz widok aplikacji hello, a następnie przejdź do widoku katalogu toohello i przejść za**aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="d85b4-207">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Przypisz użytkownika][201] 

2. <span data-ttu-id="d85b4-209">Z listy aplikacji hello wybierz **łącze Springer**.</span><span class="sxs-lookup"><span data-stu-id="d85b4-209">In hello applications list, select **Springer Link**.</span></span>

    ![Witaj Springer łącza na liście aplikacji hello](./media/active-directory-saas-springerlink-tutorial/tutorial_springerlink_app.png)  

3. <span data-ttu-id="d85b4-211">W menu powitania po lewej stronie powitania kliknij **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="d85b4-211">In hello menu on hello left, click **Users and groups**.</span></span>

    ![łącze "Użytkownicy i grupy" Hello][202]

4. <span data-ttu-id="d85b4-213">Kliknij przycisk **Dodaj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="d85b4-213">Click **Add** button.</span></span> <span data-ttu-id="d85b4-214">Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="d85b4-214">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Okienko Dodaj przypisania Hello][203]

5. <span data-ttu-id="d85b4-216">Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** hello listy użytkowników.</span><span class="sxs-lookup"><span data-stu-id="d85b4-216">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="d85b4-217">Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="d85b4-217">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="d85b4-218">Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="d85b4-218">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="d85b4-219">Test rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="d85b4-219">Test single sign-on</span></span>

<span data-ttu-id="d85b4-220">W tej sekcji można przetestować konfiguracji usługi Azure AD pojedynczego logowania jednokrotnego przy użyciu hello panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="d85b4-220">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="d85b4-221">Po kliknięciu kafelka łącze Springer hello w hello Panel dostępu, należy pobrać automatycznie zalogowane tooyour łącze Springer aplikacji.</span><span class="sxs-lookup"><span data-stu-id="d85b4-221">When you click hello Springer Link tile in hello Access Panel, you should get automatically signed-on tooyour Springer Link application.</span></span>
<span data-ttu-id="d85b4-222">Aby uzyskać więcej informacji na temat hello Panel dostępu, zobacz [toohello wprowadzenie panelu dostępu](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="d85b4-222">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="d85b4-223">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="d85b4-223">Additional resources</span></span>

* [<span data-ttu-id="d85b4-224">Lista samouczków dotyczących tooIntegrate aplikacji SaaS w usłudze Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="d85b4-224">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="d85b4-225">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="d85b4-225">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-springerlink-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-springerlink-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-springerlink-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-springerlink-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-springerlink-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-springerlink-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-springerlink-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-springerlink-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-springerlink-tutorial/tutorial_general_203.png

