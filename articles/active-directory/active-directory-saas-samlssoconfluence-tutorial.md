---
title: 'Samouczek: Integracji Azure Active Directory z logowania jednokrotnego SAML dla zlewiska przez rozpoznawania GmbH | Dokumentacja firmy Microsoft'
description: "Dowiedz się, jak tooconfigure logowanie jednokrotne między usługą Azure Active Directory i logowania jednokrotnego SAML dla zlewiska przez rozpoznawania GmbH."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 6b47d483-d3a3-442d-b123-171e3f0f7486
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/18/2017
ms.author: jeedes
ms.openlocfilehash: fe50636709857ec49023e24bdc8c6cd8c58e3c7a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-saml-sso-for-confluence-by-resolution-gmbh"></a><span data-ttu-id="1bed9-103">Samouczek: Integracji Azure Active Directory z logowania jednokrotnego SAML dla zlewiska przez rozpoznawania GmbH</span><span class="sxs-lookup"><span data-stu-id="1bed9-103">Tutorial: Azure Active Directory integration with SAML SSO for Confluence by resolution GmbH</span></span>

<span data-ttu-id="1bed9-104">Z tego samouczka, dowiesz się, jak toointegrate logowania jednokrotnego SAML dla zlewiska przez rozpoznawania GmbH w usłudze Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="1bed9-104">In this tutorial, you learn how toointegrate SAML SSO for Confluence by resolution GmbH with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="1bed9-105">Integrowanie logowania jednokrotnego SAML dla zlewiska przez rozpoznawania GmbH z usługą Azure AD zapewnia hello następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="1bed9-105">Integrating SAML SSO for Confluence by resolution GmbH with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="1bed9-106">Można kontrolować w usłudze Azure AD, kto ma dostęp tooSAML logowania jednokrotnego dla zlewiska przez rozpoznawania GmbH</span><span class="sxs-lookup"><span data-stu-id="1bed9-106">You can control in Azure AD who has access tooSAML SSO for Confluence by resolution GmbH</span></span>
- <span data-ttu-id="1bed9-107">Można włączyć użytkownika użytkownicy tooautomatically get zalogowane tooSAML logowania jednokrotnego dla zlewiska przez rozpoznawania GmbH (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="1bed9-107">You can enable your users tooautomatically get signed-on tooSAML SSO for Confluence by resolution GmbH (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="1bed9-108">Możesz zarządzać kont w jednej centralnej lokalizacji - hello portalu Azure</span><span class="sxs-lookup"><span data-stu-id="1bed9-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="1bed9-109">Jeśli chcesz tooknow więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="1bed9-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="1bed9-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="1bed9-110">Prerequisites</span></span>

<span data-ttu-id="1bed9-111">tooconfigure integracji usługi Azure AD z logowania jednokrotnego SAML dla zlewiska przez rozpoznawania GmbH należy hello następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="1bed9-111">tooconfigure Azure AD integration with SAML SSO for Confluence by resolution GmbH, you need hello following items:</span></span>

- <span data-ttu-id="1bed9-112">Subskrypcję usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="1bed9-112">An Azure AD subscription</span></span>
- <span data-ttu-id="1bed9-113">Logowania jednokrotnego SAML dla zlewiska przez rozpoznawanie jednokrotnego GmbH w subskrypcji włączone</span><span class="sxs-lookup"><span data-stu-id="1bed9-113">A SAML SSO for Confluence by resolution GmbH single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="1bed9-114">tootest hello kroków w tym samouczku, zaleca się przy użyciu środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="1bed9-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="1bed9-115">tootest hello kroki opisane w tym samouczku, należy stosować te zalecenia:</span><span class="sxs-lookup"><span data-stu-id="1bed9-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="1bed9-116">Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="1bed9-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="1bed9-117">Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz pobrać miesięczna wersja próbna [tutaj](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="1bed9-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="1bed9-118">Opis scenariusza</span><span class="sxs-lookup"><span data-stu-id="1bed9-118">Scenario description</span></span>
<span data-ttu-id="1bed9-119">W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym.</span><span class="sxs-lookup"><span data-stu-id="1bed9-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="1bed9-120">Scenariusz Hello opisane w tym samouczku składa się z dwóch głównych elementów:</span><span class="sxs-lookup"><span data-stu-id="1bed9-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="1bed9-121">Dodawanie logowania jednokrotnego SAML dla zlewiska przy rozdzielczości GmbH z galerii hello</span><span class="sxs-lookup"><span data-stu-id="1bed9-121">Adding SAML SSO for Confluence by resolution GmbH from hello gallery</span></span>
2. <span data-ttu-id="1bed9-122">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="1bed9-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-saml-sso-for-confluence-by-resolution-gmbh-from-hello-gallery"></a><span data-ttu-id="1bed9-123">Dodawanie logowania jednokrotnego SAML dla zlewiska przy rozdzielczości GmbH z galerii hello</span><span class="sxs-lookup"><span data-stu-id="1bed9-123">Adding SAML SSO for Confluence by resolution GmbH from hello gallery</span></span>

<span data-ttu-id="1bed9-124">tooconfigure hello włączenia logowania jednokrotnego SAML dla zlewiska przez rozpoznawania GmbH do usługi Azure AD, należy tooadd logowania jednokrotnego SAML dla zlewiska przez rozpoznawania GmbH z hello galerii tooyour listę zarządzanych aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="1bed9-124">tooconfigure hello integration of SAML SSO for Confluence by resolution GmbH into Azure AD, you need tooadd SAML SSO for Confluence by resolution GmbH from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="1bed9-125">**tooadd logowania jednokrotnego SAML dla zlewiska przez rozpoznawania GmbH z galerii hello, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="1bed9-125">**tooadd SAML SSO for Confluence by resolution GmbH from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="1bed9-126">W hello  **[portalu Azure](https://portal.azure.com)**na temat hello panelu nawigacji po lewej stronie, kliknij przycisk **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="1bed9-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Usługa Active Directory][1]

2. <span data-ttu-id="1bed9-128">Przejdź za**aplikacje dla przedsiębiorstw**.</span><span class="sxs-lookup"><span data-stu-id="1bed9-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="1bed9-129">Następnie przejdź zbyt**wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="1bed9-129">Then go too**All applications**.</span></span>

    ![Aplikacje][2]
    
3. <span data-ttu-id="1bed9-131">tooadd nową aplikację, kliknij przycisk **nowej aplikacji** przycisk u góry hello okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="1bed9-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplikacje][3]

4. <span data-ttu-id="1bed9-133">W polu wyszukiwania hello wpisz **logowania jednokrotnego SAML dla zlewiska przez rozpoznawania GmbH**.</span><span class="sxs-lookup"><span data-stu-id="1bed9-133">In hello search box, type **SAML SSO for Confluence by resolution GmbH**.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-samlssoconfluence-tutorial/tutorial_samlssoconfluence_search.png)

5. <span data-ttu-id="1bed9-135">W panelu wyników hello, wybierz **logowania jednokrotnego SAML dla zlewiska przez rozpoznawania GmbH**, a następnie kliknij przycisk **Dodaj** przycisk aplikacji hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="1bed9-135">In hello results panel, select **SAML SSO for Confluence by resolution GmbH**, and then click **Add** button tooadd hello application.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-samlssoconfluence-tutorial/tutorial_samlssoconfluence_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="1bed9-137">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="1bed9-137">Configuring and testing Azure AD single sign-on</span></span>

<span data-ttu-id="1bed9-138">W tej sekcji możesz skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z logowania jednokrotnego SAML dla zlewiska przez rozdzielczość GmbH oparte na koncie użytkownika testu o nazwie "Britta Simona".</span><span class="sxs-lookup"><span data-stu-id="1bed9-138">In this section, you configure and test Azure AD single sign-on with SAML SSO for Confluence by resolution GmbH based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="1bed9-139">Dla pojedynczego logowania jednokrotnego toowork usługi Azure AD musi tooknow hello odpowiednikiem użytkownika używanego w logowania jednokrotnego SAML dla zlewiska przez rozpoznawania GmbH jest tooa użytkownika w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="1bed9-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in SAML SSO for Confluence by resolution GmbH is tooa user in Azure AD.</span></span> <span data-ttu-id="1bed9-140">Innymi słowy relację łącza między użytkownika usługi Azure AD i hello użytkownikowi w logowania jednokrotnego SAML dla zlewiska przez rozpoznawania GmbH musi toobe ustanowione.</span><span class="sxs-lookup"><span data-stu-id="1bed9-140">In other words, a link relationship between an Azure AD user and hello related user in SAML SSO for Confluence by resolution GmbH needs toobe established.</span></span>

<span data-ttu-id="1bed9-141">W logowania jednokrotnego SAML zlewiska przez rozpoznawania GmbH, należy przypisać wartość hello hello **nazwy użytkownika** w usłudze Azure AD jako wartość hello hello **Username** tooestablish hello łącze relacji.</span><span class="sxs-lookup"><span data-stu-id="1bed9-141">In SAML SSO for Confluence by resolution GmbH, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="1bed9-142">tooconfigure i testowanie usługi Azure AD rejestracji jednokrotnej z logowania jednokrotnego SAML zlewiska przez rozpoznawania GmbH, należy po bloków konstrukcyjnych hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="1bed9-142">tooconfigure and test Azure AD single sign-on with SAML SSO for Confluence by resolution GmbH, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="1bed9-143">**[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configuring-azure-ad-single-sign-on)**  -tooenable Twojego toouse użytkowników tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="1bed9-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="1bed9-144">**[Tworzenie użytkownika testowego usługi Azure AD](#creating-an-azure-ad-test-user)**  -tootest usługi Azure AD rejestracji jednokrotnej z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="1bed9-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="1bed9-145">**[Tworzenie logowania jednokrotnego SAML dla zlewiska przez użytkownika testowego GmbH rozpoznawania](#creating-a-saml-sso-for-confluence-by-resolution-gmbh-test-user)**  -toohave odpowiednikiem Simona Britta w logowania jednokrotnego SAML dla zlewiska przez rozpoznawania GmbH, który jest połączony toohello usługi Azure AD reprezentację użytkownika.</span><span class="sxs-lookup"><span data-stu-id="1bed9-145">**[Creating a SAML SSO for Confluence by resolution GmbH test user](#creating-a-saml-sso-for-confluence-by-resolution-gmbh-test-user)** - toohave a counterpart of Britta Simon in SAML SSO for Confluence by resolution GmbH that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="1bed9-146">**[Przypisanie użytkownika testowego hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Simona Britta toouse usługi Azure AD rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="1bed9-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="1bed9-147">**[Testowanie rejestracji jednokrotnej](#testing-single-sign-on)**  -tooverify czy hello konfiguracji działania.</span><span class="sxs-lookup"><span data-stu-id="1bed9-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="1bed9-148">Konfigurowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="1bed9-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="1bed9-149">W tej sekcji włączyć usługi Azure AD rejestracji jednokrotnej w hello portalu Azure i skonfigurować logowanie jednokrotne w sieci logowania jednokrotnego SAML dla zlewiska przy rozpoznawania GmbH aplikacji.</span><span class="sxs-lookup"><span data-stu-id="1bed9-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your SAML SSO for Confluence by resolution GmbH application.</span></span>

<span data-ttu-id="1bed9-150">**tooconfigure usługi Azure AD rejestracji jednokrotnej z logowania jednokrotnego SAML dla zlewiska przez rozpoznawania GmbH, wykonaj hello następujące kroki:**</span><span class="sxs-lookup"><span data-stu-id="1bed9-150">**tooconfigure Azure AD single sign-on with SAML SSO for Confluence by resolution GmbH, perform hello following steps:**</span></span>

1. <span data-ttu-id="1bed9-151">W portalu Azure na powitania hello **logowania jednokrotnego SAML dla zlewiska przez rozpoznawania GmbH** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.</span><span class="sxs-lookup"><span data-stu-id="1bed9-151">In hello Azure portal, on hello **SAML SSO for Confluence by resolution GmbH** application integration page, click **Single sign-on**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej][4]

2. <span data-ttu-id="1bed9-153">Na powitania **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** tooenable rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="1bed9-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-samlssoconfluence-tutorial/tutorial_samlssoconfluence_samlbase.png)

3. <span data-ttu-id="1bed9-155">Na powitania **logowania jednokrotnego SAML zlewiska przez rozpoznawania GmbH domeny i adresów URL** sekcji, jeśli chcesz, aby aplikacja hello tooconfigure w **IDP** inicjowane tryb:</span><span class="sxs-lookup"><span data-stu-id="1bed9-155">On hello **SAML SSO for Confluence by resolution GmbH Domain and URLs** section, If you wish tooconfigure hello application in **IDP** initiated mode:</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-samlssoconfluence-tutorial/tutorial_samlssoconfluence_url_1.png)

    <span data-ttu-id="1bed9-157">a.</span><span class="sxs-lookup"><span data-stu-id="1bed9-157">a.</span></span> <span data-ttu-id="1bed9-158">W hello **identyfikator** tekstowym, wpisz adres URL za pomocą hello następującego wzorca:`https://<server-base-url>/plugins/servlet/samlsso`</span><span class="sxs-lookup"><span data-stu-id="1bed9-158">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<server-base-url>/plugins/servlet/samlsso`</span></span>

    <span data-ttu-id="1bed9-159">b.</span><span class="sxs-lookup"><span data-stu-id="1bed9-159">b.</span></span> <span data-ttu-id="1bed9-160">W hello **adres URL odpowiedzi** tekstowym, wpisz adres URL za pomocą hello następującego wzorca:`https://<server-base-url>/plugins/servlet/samlsso`</span><span class="sxs-lookup"><span data-stu-id="1bed9-160">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://<server-base-url>/plugins/servlet/samlsso`</span></span>

4. <span data-ttu-id="1bed9-161">Sprawdź **Pokaż zaawansowane ustawienia adresu URL**.</span><span class="sxs-lookup"><span data-stu-id="1bed9-161">Check **Show advanced URL settings**.</span></span> <span data-ttu-id="1bed9-162">Jeśli chcesz, aby aplikacja hello tooconfigure w **SP** inicjowane tryb:</span><span class="sxs-lookup"><span data-stu-id="1bed9-162">If you wish tooconfigure hello application in **SP** initiated mode:</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-samlssoconfluence-tutorial/tutorial_samlssoconfluence_url_2.png)

    <span data-ttu-id="1bed9-164">W hello **adres URL logowania** tekstowym, wpisz adres URL za pomocą hello następującego wzorca:`https://<server-base-url>/plugins/servlet/samlsso`</span><span class="sxs-lookup"><span data-stu-id="1bed9-164">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<server-base-url>/plugins/servlet/samlsso`</span></span>
     
    > [!NOTE] 
    > <span data-ttu-id="1bed9-165">Wartości te nie są prawdziwe.</span><span class="sxs-lookup"><span data-stu-id="1bed9-165">These values are not real.</span></span> <span data-ttu-id="1bed9-166">Zaktualizować te wartości z hello rzeczywisty identyfikator, adres URL odpowiedzi i adres URL logowania.</span><span class="sxs-lookup"><span data-stu-id="1bed9-166">Update these values with hello actual Identifier, Reply URL, and Sign-On URL.</span></span> <span data-ttu-id="1bed9-167">Skontaktuj się z [zespołu obsługi logowania jednokrotnego SAML dla zlewiska przez rozpoznawania klienta GmbH](https://www.resolution.de/go/support) tooget tych wartości.</span><span class="sxs-lookup"><span data-stu-id="1bed9-167">Contact [SAML SSO for Confluence by resolution GmbH Client support team](https://www.resolution.de/go/support) tooget these values.</span></span> 

5. <span data-ttu-id="1bed9-168">Na powitania **certyfikat podpisywania SAML** kliknij **XML metadanych** , a następnie zapisz plik metadanych hello na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="1bed9-168">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-samlssoconfluence-tutorial/tutorial_samlssoconfluence_certificate.png) 

6. <span data-ttu-id="1bed9-170">Kliknij przycisk **zapisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="1bed9-170">Click **Save** button.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-samlssoconfluence-tutorial/tutorial_general_400.png)  
    
7. <span data-ttu-id="1bed9-172">W oknie przeglądarki innej witryny sieci web, zaloguj się za tooyour **logowania jednokrotnego SAML dla zlewiska przez portal administracyjny GmbH rozpoznawania** jako administrator.</span><span class="sxs-lookup"><span data-stu-id="1bed9-172">In a different web browser window, log in tooyour **SAML SSO for Confluence by resolution GmbH admin portal** as an administrator.</span></span>

8. <span data-ttu-id="1bed9-173">Umieść kursor na koło zębate, a następnie kliknij przycisk hello **dodatki**.</span><span class="sxs-lookup"><span data-stu-id="1bed9-173">Hover on cog and click hello **Add-ons**.</span></span>
    
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-samlssoconfluence-tutorial/addon1.png)

9. <span data-ttu-id="1bed9-175">Jesteś przekierowanego tooAdministrator dostępu do strony.</span><span class="sxs-lookup"><span data-stu-id="1bed9-175">You are redirected tooAdministrator Access page.</span></span> <span data-ttu-id="1bed9-176">Wprowadź hasło hello, a następnie kliknij przycisk **Potwierdź** przycisku.</span><span class="sxs-lookup"><span data-stu-id="1bed9-176">Enter hello password and click **Confirm** button.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-samlssoconfluence-tutorial/addon2.png)

10. <span data-ttu-id="1bed9-178">W obszarze **ATLASSIAN MARKETPLACE** , kliknij pozycję **znaleźć nowe dodatki**.</span><span class="sxs-lookup"><span data-stu-id="1bed9-178">Under **ATLASSIAN MARKETPLACE** tab, click **Find new add-ons**.</span></span> 

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-samlssoconfluence-tutorial/addon.png)

11. <span data-ttu-id="1bed9-180">Wyszukiwanie **SAML pojedynczy znak na rejestracji jednokrotnej (SSO) dla zlewiska** i kliknij przycisk **zainstalować** tooinstall przycisk hello nowej wtyczki SAML.</span><span class="sxs-lookup"><span data-stu-id="1bed9-180">Search **SAML Single Sign On (SSO) for Confluence** and click **Install** button tooinstall hello new SAML plugin.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-samlssoconfluence-tutorial/addon7.png)

12. <span data-ttu-id="1bed9-182">Instalacja dodatku Hello rozpocznie.</span><span class="sxs-lookup"><span data-stu-id="1bed9-182">hello plugin installation will start.</span></span> <span data-ttu-id="1bed9-183">Kliknij przycisk **Zamknij**.</span><span class="sxs-lookup"><span data-stu-id="1bed9-183">Click **Close**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-samlssoconfluence-tutorial/addon8.png)

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-samlssoconfluence-tutorial/addon9.png)

13. <span data-ttu-id="1bed9-186">Kliknij pozycję **Zarządzaj**.</span><span class="sxs-lookup"><span data-stu-id="1bed9-186">Click **Manage**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-samlssoconfluence-tutorial/addon10.png)
    
14. <span data-ttu-id="1bed9-188">Kliknij przycisk **Konfiguruj** tooconfigure hello nowej wtyczki.</span><span class="sxs-lookup"><span data-stu-id="1bed9-188">Click **Configure** tooconfigure hello new plugin.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-samlssoconfluence-tutorial/addon11.png)

15. <span data-ttu-id="1bed9-190">Tej nowej wtyczki można także znaleźć w obszarze **użytkowników i zabezpieczenia** kartę.</span><span class="sxs-lookup"><span data-stu-id="1bed9-190">This new plugin can also be found under **USERS & SECURITY** tab.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-samlssoconfluence-tutorial/addon3.png)
    
16. <span data-ttu-id="1bed9-192">Na **konfiguracji wtyczki SingleSignOn SAML** kliknij przycisk **dodać dodatkowe dostawcy tożsamości** przycisk tooconfigure hello ustawienia dostawcy tożsamości.</span><span class="sxs-lookup"><span data-stu-id="1bed9-192">On **SAML SingleSignOn Plugin Configuration** page, click **Add additional Identity Provider** button tooconfigure hello settings of Identity Provider.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-samlssoconfluence-tutorial/addon4.png)

17. <span data-ttu-id="1bed9-194">Wykonaj następujące kroki na tej stronie:</span><span class="sxs-lookup"><span data-stu-id="1bed9-194">Perform following steps on this page:</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-samlssoconfluence-tutorial/addon5.png)
 
    <span data-ttu-id="1bed9-196">a.</span><span class="sxs-lookup"><span data-stu-id="1bed9-196">a.</span></span> <span data-ttu-id="1bed9-197">Dodaj **nazwa** z hello dostawcy tożsamości (np. usługi Azure AD).</span><span class="sxs-lookup"><span data-stu-id="1bed9-197">Add **Name** of hello Identity Provider (e.g Azure AD).</span></span>
    
    <span data-ttu-id="1bed9-198">b.</span><span class="sxs-lookup"><span data-stu-id="1bed9-198">b.</span></span> <span data-ttu-id="1bed9-199">Dodaj **opis** z hello dostawcy tożsamości (np. usługi Azure AD).</span><span class="sxs-lookup"><span data-stu-id="1bed9-199">Add **Description** of hello Identity Provider (e.g Azure AD).</span></span>

    <span data-ttu-id="1bed9-200">c.</span><span class="sxs-lookup"><span data-stu-id="1bed9-200">c.</span></span> <span data-ttu-id="1bed9-201">Kliknij przycisk **XML** i wybierz hello **metadanych** pliku, który został pobrany z portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="1bed9-201">Click **XML** and select hello **Metadata** file that you have downloaded from Azure portal.</span></span>

    <span data-ttu-id="1bed9-202">d.</span><span class="sxs-lookup"><span data-stu-id="1bed9-202">d.</span></span> <span data-ttu-id="1bed9-203">Kliknij przycisk **obciążenia** przycisku.</span><span class="sxs-lookup"><span data-stu-id="1bed9-203">Click **Load** button.</span></span>

    <span data-ttu-id="1bed9-204">e.</span><span class="sxs-lookup"><span data-stu-id="1bed9-204">e.</span></span> <span data-ttu-id="1bed9-205">Odczytuje hello IdP metadanych i wypełni pola hello jak wyróżniono hello zrzucie ekranu.</span><span class="sxs-lookup"><span data-stu-id="1bed9-205">It reads hello IdP metadata and populates hello fields as highlighted in hello screenshot.</span></span>   
18. <span data-ttu-id="1bed9-206">Kliknij przycisk **Zapisz ustawienia** przycisk toosave hello ustawienia.</span><span class="sxs-lookup"><span data-stu-id="1bed9-206">Click **Save settings** button toosave hello settings.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-samlssoconfluence-tutorial/addon6.png)

> [!TIP]
> <span data-ttu-id="1bed9-208">Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz hello [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji hello!</span><span class="sxs-lookup"><span data-stu-id="1bed9-208">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="1bed9-209">Po dodaniu tej aplikacji z hello **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij hello **rejestracji jednokrotnej** hello kartę i dostępu do osadzonych dokumentacji za pośrednictwem hello  **Konfiguracja** sekcji u dołu hello.</span><span class="sxs-lookup"><span data-stu-id="1bed9-209">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="1bed9-210">Więcej o hello osadzonych dokumentacji funkcji w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="1bed9-210">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="1bed9-211">Tworzenie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="1bed9-211">Creating an Azure AD test user</span></span>
<span data-ttu-id="1bed9-212">Celem Hello w tej sekcji jest toocreate użytkownika testowego, w portalu Azure o nazwie Simona Britta hello.</span><span class="sxs-lookup"><span data-stu-id="1bed9-212">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Tworzenie użytkowników usługi Azure AD][100]

<span data-ttu-id="1bed9-214">**toocreate użytkownika testowego w usłudze Azure AD, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="1bed9-214">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="1bed9-215">W hello **portalu Azure**na temat hello w lewym okienku nawigacji, kliknij przycisk **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="1bed9-215">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-samlssoconfluence-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="1bed9-217">toodisplay hello listę użytkowników, przejdź zbyt**użytkowników i grup** i kliknij przycisk **wszyscy użytkownicy**.</span><span class="sxs-lookup"><span data-stu-id="1bed9-217">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-samlssoconfluence-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="1bed9-219">Witaj tooopen **użytkownika** okna dialogowego, kliknij przycisk **Dodaj** u góry hello hello okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="1bed9-219">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-samlssoconfluence-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="1bed9-221">Na powitania **użytkownika** okna dialogowego wykonaj hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="1bed9-221">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-samlssoconfluence-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="1bed9-223">a.</span><span class="sxs-lookup"><span data-stu-id="1bed9-223">a.</span></span> <span data-ttu-id="1bed9-224">W hello **nazwa** pole tekstowe, typ **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="1bed9-224">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="1bed9-225">b.</span><span class="sxs-lookup"><span data-stu-id="1bed9-225">b.</span></span> <span data-ttu-id="1bed9-226">W hello **nazwy użytkownika** pole tekstowe, hello typu **adres e-mail** z BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="1bed9-226">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="1bed9-227">c.</span><span class="sxs-lookup"><span data-stu-id="1bed9-227">c.</span></span> <span data-ttu-id="1bed9-228">Wybierz **Pokaż hasło** i zanotuj wartość hello hello **hasło**.</span><span class="sxs-lookup"><span data-stu-id="1bed9-228">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="1bed9-229">d.</span><span class="sxs-lookup"><span data-stu-id="1bed9-229">d.</span></span> <span data-ttu-id="1bed9-230">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="1bed9-230">Click **Create**.</span></span>
 
### <a name="creating-a-saml-sso-for-confluence-by-resolution-gmbh-test-user"></a><span data-ttu-id="1bed9-231">Tworzenie logowania jednokrotnego SAML dla zlewiska przez użytkownika testowego GmbH rozwiązania</span><span class="sxs-lookup"><span data-stu-id="1bed9-231">Creating a SAML SSO for Confluence by resolution GmbH test user</span></span>

<span data-ttu-id="1bed9-232">toolog użytkowników tooenable usługi Azure AD w tooSAML logowania jednokrotnego dla zlewiska przez rozpoznawania GmbH one muszą mieć przydzielone do logowania jednokrotnego SAML dla zlewiska przez rozpoznawania GmbH.</span><span class="sxs-lookup"><span data-stu-id="1bed9-232">tooenable Azure AD users toolog in tooSAML SSO for Confluence by resolution GmbH, they must be provisioned into SAML SSO for Confluence by resolution GmbH.</span></span>  
<span data-ttu-id="1bed9-233">W logowania jednokrotnego SAML zlewiska przez rozpoznawania GmbH Inicjowanie obsługi to zadanie ręczne.</span><span class="sxs-lookup"><span data-stu-id="1bed9-233">In SAML SSO for Confluence by resolution GmbH, provisioning is a manual task.</span></span>

<span data-ttu-id="1bed9-234">**tooprovision konta użytkownika, należy wykonać hello następujące kroki:**</span><span class="sxs-lookup"><span data-stu-id="1bed9-234">**tooprovision a user account, perform hello following steps:**</span></span>

1. <span data-ttu-id="1bed9-235">Zaloguj się za tooyour logowania jednokrotnego SAML dla zlewiska przez witrynę firmy GmbH rozpoznawania jako administrator.</span><span class="sxs-lookup"><span data-stu-id="1bed9-235">Log in tooyour SAML SSO for Confluence by resolution GmbH company site as an administrator.</span></span>

2. <span data-ttu-id="1bed9-236">Umieść kursor na koło zębate, a następnie kliknij przycisk hello **Zarządzanie użytkownikami**.</span><span class="sxs-lookup"><span data-stu-id="1bed9-236">Hover on cog and click hello **User management**.</span></span>

    ![Dodawanie pracownika](./media/active-directory-saas-samlssoconfluence-tutorial/user1.png) 

3. <span data-ttu-id="1bed9-238">W sekcji Użytkownicy kliknij **dodawania użytkowników** kartę. Na powitania **"Dodaj użytkownika"** okna dialogowego wykonaj hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="1bed9-238">Under Users section, click **Add users** tab. On hello **“Add a User”** dialog page, perform hello following steps:</span></span>

    ![Dodawanie pracownika](./media/active-directory-saas-samlssoconfluence-tutorial/user2.png) 

    <span data-ttu-id="1bed9-240">a.</span><span class="sxs-lookup"><span data-stu-id="1bed9-240">a.</span></span> <span data-ttu-id="1bed9-241">W hello **Username** pole tekstowe, typ hello adres e-mail użytkownika, takich jak Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="1bed9-241">In hello **Username** textbox, type hello email of user like Britta Simon.</span></span>

    <span data-ttu-id="1bed9-242">b.</span><span class="sxs-lookup"><span data-stu-id="1bed9-242">b.</span></span> <span data-ttu-id="1bed9-243">W hello **imię i nazwisko** pole tekstowe, typ hello pełną nazwę użytkownika, takich jak Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="1bed9-243">In hello **Full Name** textbox, type hello full name of user like Britta Simon.</span></span>

    <span data-ttu-id="1bed9-244">c.</span><span class="sxs-lookup"><span data-stu-id="1bed9-244">c.</span></span> <span data-ttu-id="1bed9-245">W hello **E-mail** pole tekstowe, typ hello adres e-mail użytkownika, takich jak Brittasimon@contoso.com.</span><span class="sxs-lookup"><span data-stu-id="1bed9-245">In hello **Email** textbox, type hello email address of user like Brittasimon@contoso.com.</span></span>

    <span data-ttu-id="1bed9-246">d.</span><span class="sxs-lookup"><span data-stu-id="1bed9-246">d.</span></span> <span data-ttu-id="1bed9-247">W hello **hasło** tekstowym, wpisz hasło powitania dla Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="1bed9-247">In hello **Password** textbox, type hello password for Britta Simon.</span></span>

    <span data-ttu-id="1bed9-248">e.</span><span class="sxs-lookup"><span data-stu-id="1bed9-248">e.</span></span> <span data-ttu-id="1bed9-249">Kliknij przycisk **Potwierdź hasło** ponownie hello hasła.</span><span class="sxs-lookup"><span data-stu-id="1bed9-249">Click **Confirm Password** reenter hello password.</span></span>
    
    <span data-ttu-id="1bed9-250">f.</span><span class="sxs-lookup"><span data-stu-id="1bed9-250">f.</span></span> <span data-ttu-id="1bed9-251">Kliknij przycisk **Dodaj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="1bed9-251">Click **Add** button.</span></span>    

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="1bed9-252">Przypisanie użytkownika testowego hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="1bed9-252">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="1bed9-253">W tej sekcji możesz włączyć toouse Simona Britta Azure logowania jednokrotnego za udzielanie dostępu tooSAML logowania jednokrotnego dla zlewiska przez rozpoznawania GmbH.</span><span class="sxs-lookup"><span data-stu-id="1bed9-253">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooSAML SSO for Confluence by resolution GmbH.</span></span>

![Przypisz użytkownika][200] 

<span data-ttu-id="1bed9-255">**tooassign Simona Britta tooSAML logowania jednokrotnego dla zlewiska przez rozpoznawania GmbH, wykonaj hello następujące kroki:**</span><span class="sxs-lookup"><span data-stu-id="1bed9-255">**tooassign Britta Simon tooSAML SSO for Confluence by resolution GmbH, perform hello following steps:**</span></span>

1. <span data-ttu-id="1bed9-256">W portalu Azure hello, otwórz widok aplikacji hello, a następnie przejdź do widoku katalogu toohello i przejść za**aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="1bed9-256">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Przypisz użytkownika][201] 

2. <span data-ttu-id="1bed9-258">Z listy aplikacji hello wybierz **logowania jednokrotnego SAML dla zlewiska przez rozpoznawania GmbH**.</span><span class="sxs-lookup"><span data-stu-id="1bed9-258">In hello applications list, select **SAML SSO for Confluence by resolution GmbH**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-samlssoconfluence-tutorial/tutorial_samlssoconfluence_app.png) 

3. <span data-ttu-id="1bed9-260">W menu powitania po lewej stronie powitania kliknij **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="1bed9-260">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Przypisz użytkownika][202] 

4. <span data-ttu-id="1bed9-262">Kliknij przycisk **Dodaj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="1bed9-262">Click **Add** button.</span></span> <span data-ttu-id="1bed9-263">Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="1bed9-263">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Przypisz użytkownika][203]

5. <span data-ttu-id="1bed9-265">Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** hello listy użytkowników.</span><span class="sxs-lookup"><span data-stu-id="1bed9-265">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="1bed9-266">Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="1bed9-266">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="1bed9-267">Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="1bed9-267">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="1bed9-268">Testowanie rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="1bed9-268">Testing single sign-on</span></span>

<span data-ttu-id="1bed9-269">W tej sekcji można przetestować konfiguracji usługi Azure AD pojedynczego logowania jednokrotnego przy użyciu hello panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="1bed9-269">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="1bed9-270">Po kliknięciu hello logowania jednokrotnego SAML dla zlewiska przez rozpoznawania GmbH kafelka w hello Panel dostępu, należy pobrać automatycznie zalogowane tooyour logowania jednokrotnego SAML dla zlewiska przez rozpoznawania GmbH aplikacji.</span><span class="sxs-lookup"><span data-stu-id="1bed9-270">When you click hello SAML SSO for Confluence by resolution GmbH tile in hello Access Panel, you should get automatically signed-on tooyour SAML SSO for Confluence by resolution GmbH application.</span></span>
<span data-ttu-id="1bed9-271">Aby uzyskać więcej informacji na temat panelu dostępu, zobacz [wprowadzenie do panelu dostępu](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="1bed9-271">For more information about the Access Panel, see [introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="1bed9-272">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="1bed9-272">Additional resources</span></span>

* [<span data-ttu-id="1bed9-273">Lista samouczków dotyczących tooIntegrate aplikacji SaaS w usłudze Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="1bed9-273">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="1bed9-274">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="1bed9-274">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-samlssoconfluence-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-samlssoconfluence-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-samlssoconfluence-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-samlssoconfluence-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-samlssoconfluence-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-samlssoconfluence-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-samlssoconfluence-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-samlssoconfluence-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-samlssoconfluence-tutorial/tutorial_general_203.png

