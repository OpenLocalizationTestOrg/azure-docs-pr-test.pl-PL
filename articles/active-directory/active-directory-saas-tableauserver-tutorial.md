---
title: "Samouczek: Azure Active Directory integrację z serwerem Tableau | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak tooconfigure logowanie jednokrotne między usługą Azure Active Directory i serwera Tableau."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: c1917375-08aa-445c-a444-e22e23fa19e0
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/18/2017
ms.author: jeedes
ms.openlocfilehash: feb2087bd6ae6ddcb920901e6719688fc95ae287
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-tableau-server"></a><span data-ttu-id="d0c84-103">Samouczek: Azure Active Directory integrację z serwerem Tableau</span><span class="sxs-lookup"><span data-stu-id="d0c84-103">Tutorial: Azure Active Directory integration with Tableau Server</span></span>

<span data-ttu-id="d0c84-104">Z tego samouczka, dowiesz się, jak toointegrate Tableau serwera z usługą Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="d0c84-104">In this tutorial, you learn how toointegrate Tableau Server with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="d0c84-105">Integrowanie Tableau serwera z usługą Azure AD zapewnia hello następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="d0c84-105">Integrating Tableau Server with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="d0c84-106">Można kontrolować w usłudze Azure AD, kto ma dostęp do tooTableau serwera</span><span class="sxs-lookup"><span data-stu-id="d0c84-106">You can control in Azure AD who has access tooTableau Server</span></span>
- <span data-ttu-id="d0c84-107">Można włączyć użytkownika użytkownicy tooautomatically get zalogowane tooTableau serwera (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="d0c84-107">You can enable your users tooautomatically get signed-on tooTableau Server (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="d0c84-108">Możesz zarządzać kont w jednej centralnej lokalizacji - hello portalu Azure</span><span class="sxs-lookup"><span data-stu-id="d0c84-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="d0c84-109">Jeśli chcesz tooknow więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="d0c84-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d0c84-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="d0c84-110">Prerequisites</span></span>

<span data-ttu-id="d0c84-111">tooconfigure integracji usługi Azure AD z serwerem Tableau należy hello następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="d0c84-111">tooconfigure Azure AD integration with Tableau Server, you need hello following items:</span></span>

- <span data-ttu-id="d0c84-112">Subskrypcję usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="d0c84-112">An Azure AD subscription</span></span>
- <span data-ttu-id="d0c84-113">Serwer Tableau logowanie jednokrotne włączone subskrypcji</span><span class="sxs-lookup"><span data-stu-id="d0c84-113">A Tableau Server single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="d0c84-114">tootest hello kroków w tym samouczku, zaleca się przy użyciu środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="d0c84-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="d0c84-115">tootest hello kroki opisane w tym samouczku, należy stosować te zalecenia:</span><span class="sxs-lookup"><span data-stu-id="d0c84-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="d0c84-116">Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="d0c84-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="d0c84-117">Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz pobrać miesięczna wersja próbna [tutaj](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="d0c84-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="d0c84-118">Opis scenariusza</span><span class="sxs-lookup"><span data-stu-id="d0c84-118">Scenario description</span></span>
<span data-ttu-id="d0c84-119">W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym.</span><span class="sxs-lookup"><span data-stu-id="d0c84-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="d0c84-120">Scenariusz Hello opisane w tym samouczku składa się z dwóch głównych elementów:</span><span class="sxs-lookup"><span data-stu-id="d0c84-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="d0c84-121">Dodanie serwera Tableau z galerii hello</span><span class="sxs-lookup"><span data-stu-id="d0c84-121">Adding Tableau Server from hello gallery</span></span>
2. <span data-ttu-id="d0c84-122">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="d0c84-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-tableau-server-from-hello-gallery"></a><span data-ttu-id="d0c84-123">Dodanie serwera Tableau z galerii hello</span><span class="sxs-lookup"><span data-stu-id="d0c84-123">Adding Tableau Server from hello gallery</span></span>
<span data-ttu-id="d0c84-124">tooconfigure hello integrację Tableau serwera usługi Azure AD, należy tooadd Tableau serwera z hello galerii tooyour listę zarządzanych aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="d0c84-124">tooconfigure hello integration of Tableau Server into Azure AD, you need tooadd Tableau Server from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="d0c84-125">**tooadd Tableau serwera z galerii hello wykonaj hello następujące kroki:**</span><span class="sxs-lookup"><span data-stu-id="d0c84-125">**tooadd Tableau Server from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="d0c84-126">W hello  **[portalu Azure](https://portal.azure.com)**na temat hello panelu nawigacji po lewej stronie, kliknij przycisk **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="d0c84-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Usługa Active Directory][1]

2. <span data-ttu-id="d0c84-128">Przejdź za**aplikacje dla przedsiębiorstw**.</span><span class="sxs-lookup"><span data-stu-id="d0c84-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="d0c84-129">Następnie przejdź zbyt**wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="d0c84-129">Then go too**All applications**.</span></span>

    ![Aplikacje][2]
    
3. <span data-ttu-id="d0c84-131">tooadd nową aplikację, kliknij przycisk **nowej aplikacji** przycisk u góry hello okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="d0c84-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplikacje][3]

4. <span data-ttu-id="d0c84-133">W polu wyszukiwania hello wpisz **serwera Tableau**.</span><span class="sxs-lookup"><span data-stu-id="d0c84-133">In hello search box, type **Tableau Server**.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-tableauserver-tutorial/tutorial_tableauserver_search.png)

5. <span data-ttu-id="d0c84-135">W panelu wyników hello, wybierz **serwera Tableau**, a następnie kliknij przycisk **Dodaj** przycisk aplikacji hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="d0c84-135">In hello results panel, select **Tableau Server**, and then click **Add** button tooadd hello application.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-tableauserver-tutorial/tutorial_tableauserver_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="d0c84-137">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="d0c84-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="d0c84-138">W tej sekcji możesz skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z serwerem Tableau oparte na koncie użytkownika testu o nazwie "Britta Simona".</span><span class="sxs-lookup"><span data-stu-id="d0c84-138">In this section, you configure and test Azure AD single sign-on with Tableau Server based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="d0c84-139">Dla pojedynczego logowania jednokrotnego toowork usługi Azure AD musi tooknow hello odpowiednikiem użytkownika na serwerze Tableau jest tooa użytkownika w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="d0c84-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Tableau Server is tooa user in Azure AD.</span></span> <span data-ttu-id="d0c84-140">Innymi słowy relację łącza między użytkownika usługi Azure AD i hello użytkownikowi na serwerze Tableau musi toobe ustanowione.</span><span class="sxs-lookup"><span data-stu-id="d0c84-140">In other words, a link relationship between an Azure AD user and hello related user in Tableau Server needs toobe established.</span></span>

<span data-ttu-id="d0c84-141">Na serwerze Tableau, należy przypisać wartość hello hello **nazwy użytkownika** w usłudze Azure AD jako wartość hello hello **Username** tooestablish hello łącze relacji.</span><span class="sxs-lookup"><span data-stu-id="d0c84-141">In Tableau Server, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="d0c84-142">tooconfigure i testowych usługi Azure AD rejestracji jednokrotnej z serwerem Tableau, należy po bloków konstrukcyjnych hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="d0c84-142">tooconfigure and test Azure AD single sign-on with Tableau Server, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="d0c84-143">**[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configuring-azure-ad-single-sign-on)**  -tooenable Twojego toouse użytkowników tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="d0c84-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="d0c84-144">**[Tworzenie użytkownika testowego usługi Azure AD](#creating-an-azure-ad-test-user)**  -tootest usługi Azure AD rejestracji jednokrotnej z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="d0c84-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="d0c84-145">**[Tworzenie użytkownika testowego serwera Tableau](#creating-a-tableau-server-test-user)**  -toohave odpowiednikiem Simona Britta w Tableau serwera, który jest połączony toohello usługi Azure AD reprezentację użytkownika.</span><span class="sxs-lookup"><span data-stu-id="d0c84-145">**[Creating a Tableau Server test user](#creating-a-tableau-server-test-user)** - toohave a counterpart of Britta Simon in Tableau Server that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="d0c84-146">**[Przypisanie użytkownika testowego hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Simona Britta toouse usługi Azure AD rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="d0c84-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="d0c84-147">**[Testowanie rejestracji jednokrotnej](#testing-single-sign-on)**  -tooverify czy hello konfiguracji działania.</span><span class="sxs-lookup"><span data-stu-id="d0c84-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="d0c84-148">Konfigurowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="d0c84-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="d0c84-149">W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w hello portalu Azure i skonfigurować rejestracji jednokrotnej w aplikacji serwera Tableau.</span><span class="sxs-lookup"><span data-stu-id="d0c84-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Tableau Server application.</span></span>

<span data-ttu-id="d0c84-150">**tooconfigure usługi Azure AD rejestracji jednokrotnej z serwerem Tableau, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="d0c84-150">**tooconfigure Azure AD single sign-on with Tableau Server, perform hello following steps:**</span></span>

1. <span data-ttu-id="d0c84-151">W portalu Azure na powitania hello **serwera Tableau** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.</span><span class="sxs-lookup"><span data-stu-id="d0c84-151">In hello Azure portal, on hello **Tableau Server** application integration page, click **Single sign-on**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej][4]

2. <span data-ttu-id="d0c84-153">Na powitania **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** tooenable rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="d0c84-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-tableauserver-tutorial/tutorial_tableauserver_samlbase.png)

3. <span data-ttu-id="d0c84-155">Na powitania **adresy URL i domeną serwera Tableau** sekcji, wykonaj następujące kroki hello:</span><span class="sxs-lookup"><span data-stu-id="d0c84-155">On hello **Tableau Server Domain and URLs** section, perform hello following steps:</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-tableauserver-tutorial/tutorial_tableauserver_url.png)

    <span data-ttu-id="d0c84-157">a.</span><span class="sxs-lookup"><span data-stu-id="d0c84-157">a.</span></span> <span data-ttu-id="d0c84-158">W hello **adres URL logowania** tekstowym, wpisz adres URL za pomocą hello następującego wzorca:`https://azure.<domain name>.link`</span><span class="sxs-lookup"><span data-stu-id="d0c84-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://azure.<domain name>.link`</span></span>
    
    <span data-ttu-id="d0c84-159">b.</span><span class="sxs-lookup"><span data-stu-id="d0c84-159">b.</span></span> <span data-ttu-id="d0c84-160">W hello **identyfikator** tekstowym, wpisz adres URL za pomocą hello następującego wzorca:`https://azure.<domain name>.link`</span><span class="sxs-lookup"><span data-stu-id="d0c84-160">In hello **Identifier** textbox, type a URL using hello following pattern: `https://azure.<domain name>.link`</span></span>

    <span data-ttu-id="d0c84-161">c.</span><span class="sxs-lookup"><span data-stu-id="d0c84-161">c.</span></span> <span data-ttu-id="d0c84-162">W hello **adres URL odpowiedzi** tekstowym, wpisz adres URL za pomocą hello następującego wzorca:`https://azure.<domain name>.link/wg/saml/SSO/index.html`</span><span class="sxs-lookup"><span data-stu-id="d0c84-162">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://azure.<domain name>.link/wg/saml/SSO/index.html`</span></span>
     
    > [!NOTE] 
    > <span data-ttu-id="d0c84-163">Witaj poprzedniej wartości nie są wartości rzeczywistych.</span><span class="sxs-lookup"><span data-stu-id="d0c84-163">hello preceding values are not real values.</span></span> <span data-ttu-id="d0c84-164">Później należy zaktualizować wartości hello hello rzeczywisty adres URL i identyfikator ze strony konfiguracji serwera Tableau hello.</span><span class="sxs-lookup"><span data-stu-id="d0c84-164">Later, you update hello values with hello actual URL and identifier from hello Tableau Server configuration page.</span></span> 

4. <span data-ttu-id="d0c84-165">Aplikacja serwera TABLEAU oczekuje potwierdzenia SAML hello w określonym formacie.</span><span class="sxs-lookup"><span data-stu-id="d0c84-165">Tableau Server application expects hello SAML assertions in a specific format.</span></span> <span data-ttu-id="d0c84-166">Skonfiguruj powitania po oświadczeń dla tej aplikacji.</span><span class="sxs-lookup"><span data-stu-id="d0c84-166">Configure hello following claims for this application.</span></span> <span data-ttu-id="d0c84-167">Można zarządzać hello wartości tych atrybutów z hello **"Atrybuty użytkownika"** sekcji na stronie integracji aplikacji.</span><span class="sxs-lookup"><span data-stu-id="d0c84-167">You can manage hello values of these attributes from hello **"User Attributes"** section on application integration page.</span></span> <span data-ttu-id="d0c84-168">Witaj Poniższy zrzut ekranu przedstawia przykład hello tego samego.</span><span class="sxs-lookup"><span data-stu-id="d0c84-168">hello following screenshot shows an example for hello same.</span></span>
    
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-tableauserver-tutorial/3.png)
    
5. <span data-ttu-id="d0c84-170">W hello **atrybuty użytkownika** sekcji na powitania **logowanie jednokrotne** okna dialogowego, skonfiguruj atrybut tokenu SAML, jak pokazano w powyższy obraz powitania i wykonywać hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="d0c84-170">In hello **User Attributes** section on hello **Single sign-on** dialog, configure SAML token attribute as shown in hello image above and perform hello following steps:</span></span>
    
    | <span data-ttu-id="d0c84-171">Nazwa atrybutu</span><span class="sxs-lookup"><span data-stu-id="d0c84-171">Attribute Name</span></span> | <span data-ttu-id="d0c84-172">Wartość atrybutu</span><span class="sxs-lookup"><span data-stu-id="d0c84-172">Attribute Value</span></span> |
    | ---------------| --------------- |    
    | <span data-ttu-id="d0c84-173">nazwa użytkownika</span><span class="sxs-lookup"><span data-stu-id="d0c84-173">username</span></span> | <span data-ttu-id="d0c84-174">*User.DisplayName*</span><span class="sxs-lookup"><span data-stu-id="d0c84-174">*user.displayname*</span></span> |

    <span data-ttu-id="d0c84-175">a.</span><span class="sxs-lookup"><span data-stu-id="d0c84-175">a.</span></span> <span data-ttu-id="d0c84-176">Kliknij przycisk **Dodaj atrybut** tooopen hello **Dodawanie atrybutu** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="d0c84-176">Click **Add attribute** tooopen hello **Add Attribute** dialog.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-tableauserver-tutorial/tutorial_officespace_04.png)

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-tableauserver-tutorial/tutorial_officespace_05.png)
    
    <span data-ttu-id="d0c84-179">b.</span><span class="sxs-lookup"><span data-stu-id="d0c84-179">b.</span></span> <span data-ttu-id="d0c84-180">W hello **nazwa** pole tekstowe, nazwa atrybutu hello typu wyświetlany dla danego wiersza.</span><span class="sxs-lookup"><span data-stu-id="d0c84-180">In hello **Name** textbox, type hello attribute name shown for that row.</span></span>
    
    <span data-ttu-id="d0c84-181">c.</span><span class="sxs-lookup"><span data-stu-id="d0c84-181">c.</span></span> <span data-ttu-id="d0c84-182">Z hello **wartość** listy wartości atrybutu hello typ wyświetlanego dla tego wiersza.</span><span class="sxs-lookup"><span data-stu-id="d0c84-182">From hello **Value** list, type hello attribute value shown for that row.</span></span>
    
    <span data-ttu-id="d0c84-183">d.</span><span class="sxs-lookup"><span data-stu-id="d0c84-183">d.</span></span> <span data-ttu-id="d0c84-184">Kliknij przycisk **Ok**</span><span class="sxs-lookup"><span data-stu-id="d0c84-184">Click **Ok**</span></span>


6. <span data-ttu-id="d0c84-185">Na powitania **certyfikat podpisywania SAML** kliknij **XML metadanych** , a następnie zapisz plik metadanych hello na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="d0c84-185">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-tableauserver-tutorial/tutorial_tableauserver_certificate.png) 

7. <span data-ttu-id="d0c84-187">Kliknij przycisk **zapisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="d0c84-187">Click **Save** button.</span></span>

    <span data-ttu-id="d0c84-188">![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-tableauserver-tutorial/tutorial_general_400.png)
<CS></span><span class="sxs-lookup"><span data-stu-id="d0c84-188">![Configure Single Sign-On](./media/active-directory-saas-tableauserver-tutorial/tutorial_general_400.png)
<CS></span></span>
8. <span data-ttu-id="d0c84-189">tooget logowania jednokrotnego skonfigurowane dla aplikacji, należy tooyour toosign na serwerze Tableau dzierżawy jako administrator.</span><span class="sxs-lookup"><span data-stu-id="d0c84-189">tooget SSO configured for your application, you need toosign-on tooyour Tableau Server tenant as an administrator.</span></span>
   
   <span data-ttu-id="d0c84-190">a.</span><span class="sxs-lookup"><span data-stu-id="d0c84-190">a.</span></span> <span data-ttu-id="d0c84-191">W oknie Konfiguracja serwera Tableau powitania kliknij hello **SAML** kartę.</span><span class="sxs-lookup"><span data-stu-id="d0c84-191">In hello Tableau Server configuration, click hello **SAML** tab.</span></span>
  
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-tableauserver-tutorial/tutorial_tableauserver_001.png) 
  
   <span data-ttu-id="d0c84-193">b.</span><span class="sxs-lookup"><span data-stu-id="d0c84-193">b.</span></span> <span data-ttu-id="d0c84-194">Zaznacz pole wyboru hello z **SAML używana dla logowania jednokrotnego**.</span><span class="sxs-lookup"><span data-stu-id="d0c84-194">Select hello checkbox of **Use SAML for single sign-on**.</span></span>
   
   <span data-ttu-id="d0c84-195">c.</span><span class="sxs-lookup"><span data-stu-id="d0c84-195">c.</span></span> <span data-ttu-id="d0c84-196">Serwer TABLEAU adres zwrotny URL — Witaj adres URL serwera Tableau użytkownicy będą uzyskiwać dostęp do, takich jak http://tableau_server.</span><span class="sxs-lookup"><span data-stu-id="d0c84-196">Tableau Server return URL—hello URL that Tableau Server users will be accessing, such as http://tableau_server.</span></span> <span data-ttu-id="d0c84-197">Nie zaleca się przy użyciu http://localhost.</span><span class="sxs-lookup"><span data-stu-id="d0c84-197">Using http://localhost is not recommended.</span></span> <span data-ttu-id="d0c84-198">Przy użyciu adresu URL znakiem ukośnika (na przykład http://tableau_server/) nie jest obsługiwana.</span><span class="sxs-lookup"><span data-stu-id="d0c84-198">Using a URL with a trailing slash (for example, http://tableau_server/) is not supported.</span></span> <span data-ttu-id="d0c84-199">Kopia **serwera Tableau zwrotnego adresu URL** i wklej go tooAzure AD **na adres URL logowania** textbox w **adresy URL i domeną serwera Tableau** sekcji.</span><span class="sxs-lookup"><span data-stu-id="d0c84-199">Copy **Tableau Server return URL** and paste it tooAzure AD **Sign On URL** textbox in **Tableau Server Domain and URLs** section.</span></span>
   
   <span data-ttu-id="d0c84-200">d.</span><span class="sxs-lookup"><span data-stu-id="d0c84-200">d.</span></span> <span data-ttu-id="d0c84-201">Identyfikator jednostki SAML — identyfikator jednostki hello unikatowo identyfikuje toohello instalacji z serwera Tableau dostawców tożsamości.</span><span class="sxs-lookup"><span data-stu-id="d0c84-201">SAML entity ID—hello entity ID uniquely identifies your Tableau Server installation toohello IdP.</span></span> <span data-ttu-id="d0c84-202">Możesz wprowadzić adres URL serwera Tableau ponownie, jeśli chcesz, ale nie ma toobe adres URL serwera Tableau.</span><span class="sxs-lookup"><span data-stu-id="d0c84-202">You can enter your Tableau Server URL again here, if you like, but it does not have toobe your Tableau Server URL.</span></span> <span data-ttu-id="d0c84-203">Kopiuj **SAML identyfikator jednostki** i wklej go tooAzure AD **identyfikator** textbox w **adresy URL i domeną serwera Tableau** sekcji.</span><span class="sxs-lookup"><span data-stu-id="d0c84-203">Copy **SAML entity ID** and paste it tooAzure AD **Identifier** textbox in **Tableau Server Domain and URLs** section.</span></span>
     
   <span data-ttu-id="d0c84-204">e.</span><span class="sxs-lookup"><span data-stu-id="d0c84-204">e.</span></span> <span data-ttu-id="d0c84-205">Kliknij przycisk hello **Eksportuj plik metadanych** i otwórz go w aplikacji Edytor tekstu hello.</span><span class="sxs-lookup"><span data-stu-id="d0c84-205">Click hello **Export Metadata File** and open it in hello text editor application.</span></span> <span data-ttu-id="d0c84-206">Znajdź adres URL usługi klienta potwierdzenia z indeksem 0 Http Post i URL hello kopii.</span><span class="sxs-lookup"><span data-stu-id="d0c84-206">Locate Assertion Consumer Service URL with Http Post and Index 0 and copy hello URL.</span></span> <span data-ttu-id="d0c84-207">Teraz wklej go tooAzure AD **adres URL odpowiedzi** textbox w **adresy URL i domeną serwera Tableau** sekcji.</span><span class="sxs-lookup"><span data-stu-id="d0c84-207">Now paste it tooAzure AD **Reply URL** textbox in **Tableau Server Domain and URLs** section.</span></span>
   
   <span data-ttu-id="d0c84-208">f.</span><span class="sxs-lookup"><span data-stu-id="d0c84-208">f.</span></span> <span data-ttu-id="d0c84-209">Zlokalizuj plik metadanych Federacji pobrany z portalu Azure, a następnie przekaż go w hello **pliku metadanych SAML Idp**.</span><span class="sxs-lookup"><span data-stu-id="d0c84-209">Locate your Federation Metadata file downloaded from Azure portal, and then upload it in hello **SAML Idp metadata file**.</span></span>
   
   <span data-ttu-id="d0c84-210">g.</span><span class="sxs-lookup"><span data-stu-id="d0c84-210">g.</span></span> <span data-ttu-id="d0c84-211">Kliknij przycisk hello **OK** przycisk na stronie Konfiguracja serwera Tableau hello.</span><span class="sxs-lookup"><span data-stu-id="d0c84-211">Click hello **OK** button in hello Tableau Server Configuration page.</span></span>
   
    >[!NOTE] 
    ><span data-ttu-id="d0c84-212">Odbiorca ma tooupload dowolny certyfikat w konfiguracji logowania jednokrotnego SAML serwera Tableau hello i będą uzyskać ignorowane w hello przepływu logowania jednokrotnego.</span><span class="sxs-lookup"><span data-stu-id="d0c84-212">Customer have tooupload any certificate in hello Tableau Server SAML SSO configuration and it will get ignored in hello SSO flow.</span></span>
    ><span data-ttu-id="d0c84-213">Jeśli konieczne pomoc w konfigurowaniu SAML na serwerze Tableau, można znaleźć w artykule toothis [skonfigurować SAML](http://onlinehelp.tableau.com/current/server/en-us/config_saml.htm).</span><span class="sxs-lookup"><span data-stu-id="d0c84-213">If you need help configuring SAML on Tableau Server then please refer toothis article [Configure SAML](http://onlinehelp.tableau.com/current/server/en-us/config_saml.htm).</span></span>
    >
<CE>

> [!TIP]
> <span data-ttu-id="d0c84-214">Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz hello [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji hello!</span><span class="sxs-lookup"><span data-stu-id="d0c84-214">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="d0c84-215">Po dodaniu tej aplikacji z hello **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij hello **rejestracji jednokrotnej** hello kartę i dostępu do osadzonych dokumentacji za pośrednictwem hello  **Konfiguracja** sekcji u dołu hello.</span><span class="sxs-lookup"><span data-stu-id="d0c84-215">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="d0c84-216">Więcej o hello osadzonych dokumentacji funkcji w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="d0c84-216">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="d0c84-217">Tworzenie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="d0c84-217">Creating an Azure AD test user</span></span>
<span data-ttu-id="d0c84-218">Celem Hello w tej sekcji jest toocreate użytkownika testowego, w portalu Azure o nazwie Simona Britta hello.</span><span class="sxs-lookup"><span data-stu-id="d0c84-218">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Tworzenie użytkowników usługi Azure AD][100]

<span data-ttu-id="d0c84-220">**toocreate użytkownika testowego w usłudze Azure AD, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="d0c84-220">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="d0c84-221">W hello **portalu Azure**na temat hello w lewym okienku nawigacji, kliknij przycisk **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="d0c84-221">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-tableauserver-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="d0c84-223">toodisplay hello listę użytkowników, przejdź zbyt**użytkowników i grup** i kliknij przycisk **wszyscy użytkownicy**.</span><span class="sxs-lookup"><span data-stu-id="d0c84-223">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-tableauserver-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="d0c84-225">Witaj tooopen **użytkownika** okna dialogowego, kliknij przycisk **Dodaj** u góry hello hello okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="d0c84-225">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-tableauserver-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="d0c84-227">Na powitania **użytkownika** okna dialogowego wykonaj hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="d0c84-227">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-tableauserver-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="d0c84-229">a.</span><span class="sxs-lookup"><span data-stu-id="d0c84-229">a.</span></span> <span data-ttu-id="d0c84-230">W hello **nazwa** pole tekstowe, typ **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="d0c84-230">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="d0c84-231">b.</span><span class="sxs-lookup"><span data-stu-id="d0c84-231">b.</span></span> <span data-ttu-id="d0c84-232">W hello **nazwy użytkownika** pole tekstowe, hello typu **adres e-mail** z BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="d0c84-232">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="d0c84-233">c.</span><span class="sxs-lookup"><span data-stu-id="d0c84-233">c.</span></span> <span data-ttu-id="d0c84-234">Wybierz **Pokaż hasło** i zanotuj wartość hello hello **hasło**.</span><span class="sxs-lookup"><span data-stu-id="d0c84-234">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="d0c84-235">d.</span><span class="sxs-lookup"><span data-stu-id="d0c84-235">d.</span></span> <span data-ttu-id="d0c84-236">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="d0c84-236">Click **Create**.</span></span>
 
### <a name="creating-a-tableau-server-test-user"></a><span data-ttu-id="d0c84-237">Tworzenie użytkownika testowego Tableau serwera</span><span class="sxs-lookup"><span data-stu-id="d0c84-237">Creating a Tableau Server test user</span></span>

<span data-ttu-id="d0c84-238">Celem Hello w tej sekcji jest toocreate użytkownika o nazwie Simona Britta w Tableau serwera.</span><span class="sxs-lookup"><span data-stu-id="d0c84-238">hello objective of this section is toocreate a user called Britta Simon in Tableau Server.</span></span> <span data-ttu-id="d0c84-239">Należy tooprovision wszyscy użytkownicy hello w hello Tableau serwera.</span><span class="sxs-lookup"><span data-stu-id="d0c84-239">You need tooprovision all hello users in hello Tableau server.</span></span> 

<span data-ttu-id="d0c84-240">Tej nazwy użytkownika hello użytkownika powinna być zgodna wartość hello, które zostały skonfigurowane w atrybucie niestandardowym hello Azure AD z **username**.</span><span class="sxs-lookup"><span data-stu-id="d0c84-240">That username of hello user should match hello value which you have configured in hello Azure AD custom attribute of **username**.</span></span> <span data-ttu-id="d0c84-241">Z hello poprawne mapowania integracji hello powinny działać [Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configuring-azure-ad-single-sign-on).</span><span class="sxs-lookup"><span data-stu-id="d0c84-241">With hello correct mapping hello integration should work [Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on).</span></span>

>[!NOTE]
><span data-ttu-id="d0c84-242">Należy ręcznie toocreate użytkownika, należy najpierw toocontact hello Tableau administratora w organizacji.</span><span class="sxs-lookup"><span data-stu-id="d0c84-242">If you need toocreate a user manually, you need toocontact hello Tableau Server administrator in your organization.</span></span>
> 
> 

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="d0c84-243">Przypisanie użytkownika testowego hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="d0c84-243">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="d0c84-244">W tej sekcji możesz włączyć toouse Simona Britta Azure logowania jednokrotnego za udzielanie dostępu tooTableau serwera.</span><span class="sxs-lookup"><span data-stu-id="d0c84-244">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooTableau Server.</span></span>

![Przypisz użytkownika][200] 

<span data-ttu-id="d0c84-246">**tooassign tooTableau Simona Britta serwera, wykonaj hello następujące kroki:**</span><span class="sxs-lookup"><span data-stu-id="d0c84-246">**tooassign Britta Simon tooTableau Server, perform hello following steps:**</span></span>

1. <span data-ttu-id="d0c84-247">W portalu Azure hello, otwórz widok aplikacji hello, a następnie przejdź do widoku katalogu toohello i przejść za**aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="d0c84-247">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Przypisz użytkownika][201] 

2. <span data-ttu-id="d0c84-249">Z listy aplikacji hello wybierz **serwera Tableau**.</span><span class="sxs-lookup"><span data-stu-id="d0c84-249">In hello applications list, select **Tableau Server**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-tableauserver-tutorial/tutorial_tableauserver_app.png) 

3. <span data-ttu-id="d0c84-251">W menu powitania po lewej stronie powitania kliknij **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="d0c84-251">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Przypisz użytkownika][202] 

4. <span data-ttu-id="d0c84-253">Kliknij przycisk **Dodaj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="d0c84-253">Click **Add** button.</span></span> <span data-ttu-id="d0c84-254">Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="d0c84-254">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Przypisz użytkownika][203]

5. <span data-ttu-id="d0c84-256">Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** hello listy użytkowników.</span><span class="sxs-lookup"><span data-stu-id="d0c84-256">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="d0c84-257">Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="d0c84-257">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="d0c84-258">Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="d0c84-258">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="d0c84-259">Testowanie rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="d0c84-259">Testing single sign-on</span></span>

<span data-ttu-id="d0c84-260">W tej sekcji można przetestować konfiguracji usługi Azure AD pojedynczego logowania jednokrotnego przy użyciu hello panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="d0c84-260">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="d0c84-261">Po kliknięciu kafelka serwera Tableau hello w hello Panel dostępu, należy pobrać automatycznie zalogowane tooyour Tableau serwera aplikacji.</span><span class="sxs-lookup"><span data-stu-id="d0c84-261">When you click hello Tableau Server tile in hello Access Panel, you should get automatically signed-on tooyour Tableau Server application.</span></span>
<span data-ttu-id="d0c84-262">Aby uzyskać więcej informacji na temat panelu dostępu, zobacz [wprowadzenie do panelu dostępu](https://msdn.microsoft.com/library/dn308586).</span><span class="sxs-lookup"><span data-stu-id="d0c84-262">For more information about the Access Panel, see [introduction to the Access Panel](https://msdn.microsoft.com/library/dn308586).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="d0c84-263">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="d0c84-263">Additional resources</span></span>

* [<span data-ttu-id="d0c84-264">Lista samouczków dotyczących tooIntegrate aplikacji SaaS w usłudze Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="d0c84-264">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="d0c84-265">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="d0c84-265">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-tableauserver-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-tableauserver-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-tableauserver-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-tableauserver-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-tableauserver-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-tableauserver-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-tableauserver-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-tableauserver-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-tableauserver-tutorial/tutorial_general_203.png

