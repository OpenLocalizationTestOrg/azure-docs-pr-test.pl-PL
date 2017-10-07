---
title: 'Samouczek: Azure Active Directory integracji z logowaniem Jednokrotnym Kantega dla zlewiska | Dokumentacja firmy Microsoft'
description: "Dowiedz się, jak tooconfigure logowanie jednokrotne między usługą Azure Active Directory i logowania jednokrotnego Kantega dla zlewiska."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: d0d99c14-a6ca-45f2-bb84-633126095e7a
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: jeedes
ms.openlocfilehash: b35eb8757e41e86228a3a9ee10869086cc801c9b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-kantega-sso-for-confluence"></a><span data-ttu-id="8b813-103">Samouczek: Azure Active Directory integracji z logowaniem Jednokrotnym Kantega dla zlewiska</span><span class="sxs-lookup"><span data-stu-id="8b813-103">Tutorial: Azure Active Directory integration with Kantega SSO for Confluence</span></span>

<span data-ttu-id="8b813-104">Z tego samouczka, dowiesz się, jak toointegrate Kantega Usługa rejestracji Jednokrotnej dla zlewiska z usługi Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="8b813-104">In this tutorial, you learn how toointegrate Kantega SSO for Confluence with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="8b813-105">Integracja z usługą Azure AD Kantega Usługa rejestracji Jednokrotnej dla zlewiska zapewnia hello następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="8b813-105">Integrating Kantega SSO for Confluence with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="8b813-106">Można kontrolować w usłudze Azure AD, kto ma dostęp tooKantega logowania jednokrotnego dla zlewiska</span><span class="sxs-lookup"><span data-stu-id="8b813-106">You can control in Azure AD who has access tooKantega SSO for Confluence</span></span>
- <span data-ttu-id="8b813-107">Można włączyć użytkownika użytkownicy tooautomatically get zalogowane tooKantega logowania jednokrotnego dla zlewiska (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="8b813-107">You can enable your users tooautomatically get signed-on tooKantega SSO for Confluence (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="8b813-108">Możesz zarządzać kont w jednej centralnej lokalizacji - hello portalu Azure</span><span class="sxs-lookup"><span data-stu-id="8b813-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="8b813-109">Jeśli chcesz tooknow więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="8b813-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="8b813-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="8b813-110">Prerequisites</span></span>

<span data-ttu-id="8b813-111">tooconfigure integracji usługi Azure AD z logowania jednokrotnego Kantega dla zlewiska należy hello następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="8b813-111">tooconfigure Azure AD integration with Kantega SSO for Confluence, you need hello following items:</span></span>

- <span data-ttu-id="8b813-112">Subskrypcję usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="8b813-112">An Azure AD subscription</span></span>
- <span data-ttu-id="8b813-113">Kantega Usługa rejestracji Jednokrotnej dla zlewiska logowanie jednokrotne włączone subskrypcji</span><span class="sxs-lookup"><span data-stu-id="8b813-113">A Kantega SSO for Confluence single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="8b813-114">tootest hello kroków w tym samouczku, zaleca się przy użyciu środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="8b813-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="8b813-115">tootest hello kroki opisane w tym samouczku, należy stosować te zalecenia:</span><span class="sxs-lookup"><span data-stu-id="8b813-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="8b813-116">Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="8b813-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="8b813-117">Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz pobrać miesięczna wersja próbna [tutaj](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="8b813-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="8b813-118">Opis scenariusza</span><span class="sxs-lookup"><span data-stu-id="8b813-118">Scenario description</span></span>
<span data-ttu-id="8b813-119">W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym.</span><span class="sxs-lookup"><span data-stu-id="8b813-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="8b813-120">Scenariusz Hello opisane w tym samouczku składa się z dwóch głównych elementów:</span><span class="sxs-lookup"><span data-stu-id="8b813-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="8b813-121">Dodawanie logowania jednokrotnego Kantega dla zlewiska z galerii hello</span><span class="sxs-lookup"><span data-stu-id="8b813-121">Adding Kantega SSO for Confluence from hello gallery</span></span>
2. <span data-ttu-id="8b813-122">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="8b813-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-kantega-sso-for-confluence-from-hello-gallery"></a><span data-ttu-id="8b813-123">Dodawanie logowania jednokrotnego Kantega dla zlewiska z galerii hello</span><span class="sxs-lookup"><span data-stu-id="8b813-123">Adding Kantega SSO for Confluence from hello gallery</span></span>
<span data-ttu-id="8b813-124">Integracja hello tooconfigure Kantega sesji rejestracji jednokrotnej dla zlewiska do usługi Azure AD, należy tooadd Kantega logowania jednokrotnego dla zlewiska z hello galerii tooyour listę zarządzanych aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="8b813-124">tooconfigure hello integration of Kantega SSO for Confluence into Azure AD, you need tooadd Kantega SSO for Confluence from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="8b813-125">**tooadd Kantega Usługa rejestracji Jednokrotnej dla zlewiska z galerii hello wykonaj hello następujące kroki:**</span><span class="sxs-lookup"><span data-stu-id="8b813-125">**tooadd Kantega SSO for Confluence from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="8b813-126">W hello  **[portalu Azure](https://portal.azure.com)**na temat hello panelu nawigacji po lewej stronie, kliknij przycisk **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="8b813-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Usługa Active Directory][1]

2. <span data-ttu-id="8b813-128">Przejdź za**aplikacje dla przedsiębiorstw**.</span><span class="sxs-lookup"><span data-stu-id="8b813-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="8b813-129">Następnie przejdź zbyt**wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="8b813-129">Then go too**All applications**.</span></span>

    ![Aplikacje][2]
    
3. <span data-ttu-id="8b813-131">tooadd nową aplikację, kliknij przycisk **nowej aplikacji** przycisk u góry hello okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="8b813-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplikacje][3]

4. <span data-ttu-id="8b813-133">W polu wyszukiwania hello wpisz **Kantega Usługa rejestracji Jednokrotnej dla zlewiska**.</span><span class="sxs-lookup"><span data-stu-id="8b813-133">In hello search box, type **Kantega SSO for Confluence**.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-kantegassoforconfluence-tutorial/tutorial_kantegassoforconfluence_search.png)

5. <span data-ttu-id="8b813-135">W panelu wyników hello, wybierz **Kantega Usługa rejestracji Jednokrotnej dla zlewiska**, a następnie kliknij przycisk **Dodaj** przycisk aplikacji hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="8b813-135">In hello results panel, select **Kantega SSO for Confluence**, and then click **Add** button tooadd hello application.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-kantegassoforconfluence-tutorial/tutorial_kantegassoforconfluence_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="8b813-137">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="8b813-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="8b813-138">W tej sekcji skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z logowania jednokrotnego Kantega dla zlewiska w oparciu o nazwie "Britta Simona" użytkownika testowego.</span><span class="sxs-lookup"><span data-stu-id="8b813-138">In this section, you configure and test Azure AD single sign-on with Kantega SSO for Confluence based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="8b813-139">Dla pojedynczego logowania jednokrotnego toowork usługi Azure AD musi tooknow użytkownika odpowiednikiem hello w rejestracji Jednokrotnej Kantega dla zlewiska jest tooa użytkownika w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="8b813-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Kantega SSO for Confluence is tooa user in Azure AD.</span></span> <span data-ttu-id="8b813-140">Innymi słowy relację łącza między użytkownika usługi Azure AD i hello użytkownikowi w rejestracji Jednokrotnej Kantega dla zlewiska musi toobe ustanowione.</span><span class="sxs-lookup"><span data-stu-id="8b813-140">In other words, a link relationship between an Azure AD user and hello related user in Kantega SSO for Confluence needs toobe established.</span></span>

<span data-ttu-id="8b813-141">W Kantega logowania jednokrotnego dla zlewiska, należy przypisać wartość hello hello **nazwy użytkownika** w usłudze Azure AD jako wartość hello hello **Username** tooestablish hello łącze relacji.</span><span class="sxs-lookup"><span data-stu-id="8b813-141">In Kantega SSO for Confluence, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="8b813-142">tooconfigure i testowanie usługi Azure AD rejestracji jednokrotnej z logowania jednokrotnego Kantega zlewiska, należy po bloków konstrukcyjnych hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="8b813-142">tooconfigure and test Azure AD single sign-on with Kantega SSO for Confluence, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="8b813-143">**[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configuring-azure-ad-single-sign-on)**  -tooenable Twojego toouse użytkowników tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="8b813-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="8b813-144">**[Tworzenie użytkownika testowego usługi Azure AD](#creating-an-azure-ad-test-user)**  -tootest usługi Azure AD rejestracji jednokrotnej z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="8b813-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="8b813-145">**[Tworzenie Kantega Usługa rejestracji Jednokrotnej dla użytkownika testowego zlewiska](#creating-a-kantega-sso-for-confluence-test-user)**  -toohave odpowiednikiem Simona Britta w rejestracji Jednokrotnej Kantega dla zlewiska, który jest połączony toohello usługi Azure AD reprezentację użytkownika.</span><span class="sxs-lookup"><span data-stu-id="8b813-145">**[Creating a Kantega SSO for Confluence test user](#creating-a-kantega-sso-for-confluence-test-user)** - toohave a counterpart of Britta Simon in Kantega SSO for Confluence that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="8b813-146">**[Przypisanie użytkownika testowego hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Simona Britta toouse usługi Azure AD rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="8b813-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="8b813-147">**[Testowanie rejestracji jednokrotnej](#testing-single-sign-on)**  -tooverify czy hello konfiguracji działania.</span><span class="sxs-lookup"><span data-stu-id="8b813-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="8b813-148">Konfigurowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="8b813-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="8b813-149">W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w hello portalu Azure i skonfigurować rejestracji jednokrotnej w Twojej rejestracji Jednokrotnej Kantega zlewiska aplikacji.</span><span class="sxs-lookup"><span data-stu-id="8b813-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Kantega SSO for Confluence application.</span></span>

<span data-ttu-id="8b813-150">**tooconfigure usługi Azure AD rejestracji jednokrotnej z logowania jednokrotnego Kantega dla zlewiska, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="8b813-150">**tooconfigure Azure AD single sign-on with Kantega SSO for Confluence, perform hello following steps:**</span></span>

1. <span data-ttu-id="8b813-151">W portalu Azure na powitania hello **Kantega Usługa rejestracji Jednokrotnej dla zlewiska** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.</span><span class="sxs-lookup"><span data-stu-id="8b813-151">In hello Azure portal, on hello **Kantega SSO for Confluence** application integration page, click **Single sign-on**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej][4]

2. <span data-ttu-id="8b813-153">Na powitania **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** tooenable rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="8b813-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-kantegassoforconfluence-tutorial/tutorial_kantegassoforconfluence_samlbase.png)

3. <span data-ttu-id="8b813-155">W **IDP** inicjowane tryb na powitania **logowania jednokrotnego Kantega zlewiska domeny i adresów URL** sekcji wykonać powitania po kroku:</span><span class="sxs-lookup"><span data-stu-id="8b813-155">In **IDP** initiated mode, on hello **Kantega SSO for Confluence Domain and URLs** section perform hello following step:</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-kantegassoforconfluence-tutorial/tutorial_kantegassoforconfluence_url1.png)

    <span data-ttu-id="8b813-157">a.</span><span class="sxs-lookup"><span data-stu-id="8b813-157">a.</span></span> <span data-ttu-id="8b813-158">W hello **identyfikator** tekstowym, wpisz adres URL za pomocą hello następującego wzorca:`https://<server-base-url>/plugins/servlet/no.kantega.saml/sp/<uniqueid>/login`</span><span class="sxs-lookup"><span data-stu-id="8b813-158">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<server-base-url>/plugins/servlet/no.kantega.saml/sp/<uniqueid>/login`</span></span>

    <span data-ttu-id="8b813-159">b.</span><span class="sxs-lookup"><span data-stu-id="8b813-159">b.</span></span> <span data-ttu-id="8b813-160">W hello **adres URL odpowiedzi** tekstowym, wpisz adres URL za pomocą hello następującego wzorca:`https://<server-base-url>/plugins/servlet/no.kantega.saml/sp/<uniqueid>/login`</span><span class="sxs-lookup"><span data-stu-id="8b813-160">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://<server-base-url>/plugins/servlet/no.kantega.saml/sp/<uniqueid>/login`</span></span>

4. <span data-ttu-id="8b813-161">W **SP** inicjowane trybie wyboru **Pokaż zaawansowane ustawienia adresu URL** i wykonywać powitania po kroku:</span><span class="sxs-lookup"><span data-stu-id="8b813-161">In **SP** initiated mode, check **Show advanced URL settings** and perform hello following step:</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-kantegassoforconfluence-tutorial/tutorial_kantegassoforconfluence_url2.png)

    <span data-ttu-id="8b813-163">W hello **adres URL logowania** tekstowym, wpisz adres URL za pomocą hello następującego wzorca:`https://<server-base-url>/plugins/servlet/no.kantega.saml/sp/<uniqueid>/login`</span><span class="sxs-lookup"><span data-stu-id="8b813-163">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<server-base-url>/plugins/servlet/no.kantega.saml/sp/<uniqueid>/login`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="8b813-164">Wartości te nie są prawdziwe.</span><span class="sxs-lookup"><span data-stu-id="8b813-164">These values are not real.</span></span> <span data-ttu-id="8b813-165">Zaktualizować te wartości z hello rzeczywisty identyfikator, adres URL odpowiedzi i adres URL logowania.</span><span class="sxs-lookup"><span data-stu-id="8b813-165">Update these values with hello actual Identifier, Reply URL, and Sign-On URL.</span></span> <span data-ttu-id="8b813-166">Te wartości są odbierane podczas konfigurowania hello zlewiska wtyczki, który znajduje się w dalszej części samouczka hello.</span><span class="sxs-lookup"><span data-stu-id="8b813-166">These values are received during hello configuration of Confluence plugin, which is explained later in hello tutorial.</span></span>

5. <span data-ttu-id="8b813-167">Na powitania **certyfikat podpisywania SAML** kliknij **XML metadanych** , a następnie zapisz plik metadanych hello na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="8b813-167">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-kantegassoforconfluence-tutorial/tutorial_kantegassoforconfluence_certificate.png) 

6. <span data-ttu-id="8b813-169">Kliknij przycisk **zapisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="8b813-169">Click **Save** button.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-kantegassoforconfluence-tutorial/tutorial_general_400.png)
    
7. <span data-ttu-id="8b813-171">W oknie przeglądarki innej witryny sieci web, zaloguj się za tooyour **portalu administracyjnego zlewiska** jako administrator.</span><span class="sxs-lookup"><span data-stu-id="8b813-171">In a different web browser window, log in tooyour **Confluence admin portal** as an administrator.</span></span>

8. <span data-ttu-id="8b813-172">Umieść kursor na koło zębate, a następnie kliknij przycisk hello **dodatki**.</span><span class="sxs-lookup"><span data-stu-id="8b813-172">Hover on cog and click hello **Add-ons**.</span></span>
    
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-kantegassoforconfluence-tutorial/addon1.png)

9. <span data-ttu-id="8b813-174">W obszarze **ATLASSIAN MARKETPLACE** , kliknij pozycję **znaleźć nowe dodatki**.</span><span class="sxs-lookup"><span data-stu-id="8b813-174">Under **ATLASSIAN MARKETPLACE** tab, click **Find new add-ons**.</span></span> 

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-kantegassoforconfluence-tutorial/addon.png)

10. <span data-ttu-id="8b813-176">Wyszukiwanie **Kantega Usługa rejestracji Jednokrotnej dla protokołu Kerberos SAML zlewiska** i kliknij przycisk **zainstalować** tooinstall przycisk hello nowej wtyczki SAML.</span><span class="sxs-lookup"><span data-stu-id="8b813-176">Search **Kantega SSO for Confluence SAML Kerberos** and click **Install** button tooinstall hello new SAML plugin.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-kantegassoforconfluence-tutorial/addon2.png)

11. <span data-ttu-id="8b813-178">rozpoczyna się instalacja dodatku Hello.</span><span class="sxs-lookup"><span data-stu-id="8b813-178">hello plugin installation starts.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-kantegassoforconfluence-tutorial/addon3.png)

12. <span data-ttu-id="8b813-180">Po zakończeniu instalacji hello.</span><span class="sxs-lookup"><span data-stu-id="8b813-180">Once hello installation is complete.</span></span> <span data-ttu-id="8b813-181">Kliknij przycisk **Zamknij**.</span><span class="sxs-lookup"><span data-stu-id="8b813-181">Click **Close**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-kantegassoforconfluence-tutorial/addon33.png)

13. <span data-ttu-id="8b813-183">Kliknij pozycję **Zarządzaj**.</span><span class="sxs-lookup"><span data-stu-id="8b813-183">Click **Manage**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-kantegassoforconfluence-tutorial/addon34.png)
    
14. <span data-ttu-id="8b813-185">Kliknij przycisk **Konfiguruj** tooconfigure hello nowej wtyczki.</span><span class="sxs-lookup"><span data-stu-id="8b813-185">Click **Configure** tooconfigure hello new plugin.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-kantegassoforconfluence-tutorial/addon35.png)

15. <span data-ttu-id="8b813-187">Tej nowej wtyczki można także znaleźć w obszarze **użytkowników i zabezpieczenia** kartę.</span><span class="sxs-lookup"><span data-stu-id="8b813-187">This new plugin can also be found under **USERS & SECURITY** tab.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-kantegassoforconfluence-tutorial/addon36.png)
    
16. <span data-ttu-id="8b813-189">W hello **SAML** sekcji.</span><span class="sxs-lookup"><span data-stu-id="8b813-189">In hello **SAML** section.</span></span> <span data-ttu-id="8b813-190">Wybierz **usługi Azure Active Directory (Azure AD)** z hello **dostawcy tożsamości Dodaj** listy rozwijanej.</span><span class="sxs-lookup"><span data-stu-id="8b813-190">Select **Azure Active Directory (Azure AD)** from hello **Add identity provider** dropdown.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-kantegassoforconfluence-tutorial/addon4.png)

17. <span data-ttu-id="8b813-192">Wybierz poziom subskrypcji jako **podstawowe**.</span><span class="sxs-lookup"><span data-stu-id="8b813-192">Select subscription level as **Basic**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-kantegassoforconfluence-tutorial/addon5.png)       

18. <span data-ttu-id="8b813-194">Na powitania **właściwości aplikacji** sekcji, wykonaj następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="8b813-194">On hello **App properties** section, perform following steps:</span></span> 

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-kantegassoforconfluence-tutorial/addon6.png)

    <span data-ttu-id="8b813-196">a.</span><span class="sxs-lookup"><span data-stu-id="8b813-196">a.</span></span> <span data-ttu-id="8b813-197">Kopiuj hello **identyfikator URI aplikacji** wartości i używać go jako **identyfikator, adres URL odpowiedzi i adres URL logowania** na powitania **logowania jednokrotnego Kantega zlewiska domeny i adresów URL** sekcji w portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="8b813-197">Copy hello **App ID URI** value and use it as **Identifier, Reply URL, and Sign-On URL** on hello **Kantega SSO for Confluence Domain and URLs** section in Azure portal.</span></span>

    <span data-ttu-id="8b813-198">b.</span><span class="sxs-lookup"><span data-stu-id="8b813-198">b.</span></span> <span data-ttu-id="8b813-199">Kliknij przycisk **Dalej**.</span><span class="sxs-lookup"><span data-stu-id="8b813-199">Click **Next**.</span></span>

19. <span data-ttu-id="8b813-200">Na powitania **importu metadanych** sekcji, wykonaj następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="8b813-200">On hello **Metadata import** section, perform following steps:</span></span> 

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-kantegassoforconfluence-tutorial/addon7.png)

    <span data-ttu-id="8b813-202">a.</span><span class="sxs-lookup"><span data-stu-id="8b813-202">a.</span></span> <span data-ttu-id="8b813-203">Wybierz **pliku metadanych na tym komputerze**i przekazywanie pliku metadanych, który został pobrany z portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="8b813-203">Select **Metadata file on my computer**, and upload metadata file, which you have downloaded from Azure portal.</span></span>

    <span data-ttu-id="8b813-204">b.</span><span class="sxs-lookup"><span data-stu-id="8b813-204">b.</span></span> <span data-ttu-id="8b813-205">Kliknij przycisk **Dalej**.</span><span class="sxs-lookup"><span data-stu-id="8b813-205">Click **Next**.</span></span>

20. <span data-ttu-id="8b813-206">Na powitania **nazwę i logowania jednokrotnego lokalizację** sekcji, wykonaj następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="8b813-206">On hello **Name and SSO location** section, perform following steps:</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-kantegassoforconfluence-tutorial/addon8.png)
    
    <span data-ttu-id="8b813-208">a.</span><span class="sxs-lookup"><span data-stu-id="8b813-208">a.</span></span> <span data-ttu-id="8b813-209">Dodaj nazwę hello dostawcy tożsamości w **Nazwa dostawcy tożsamości** pola tekstowego (np. usługi Azure AD).</span><span class="sxs-lookup"><span data-stu-id="8b813-209">Add Name of hello Identity Provider in **Identity provider name** textbox (e.g Azure AD).</span></span>

    <span data-ttu-id="8b813-210">b.</span><span class="sxs-lookup"><span data-stu-id="8b813-210">b.</span></span> <span data-ttu-id="8b813-211">Kliknij przycisk **Dalej**.</span><span class="sxs-lookup"><span data-stu-id="8b813-211">Click **Next**.</span></span>

21. <span data-ttu-id="8b813-212">Sprawdź hello certyfikatu podpisywania, a następnie kliknij przycisk **dalej**.</span><span class="sxs-lookup"><span data-stu-id="8b813-212">Verify hello Signing certificate and click **Next**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-kantegassoforconfluence-tutorial/addon9.png)

22. <span data-ttu-id="8b813-214">Na powitania **kont użytkowników zlewiska** sekcji, wykonaj następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="8b813-214">On hello **Confluence user accounts** section, perform following steps:</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-kantegassoforconfluence-tutorial/addon10.png)

    <span data-ttu-id="8b813-216">a.</span><span class="sxs-lookup"><span data-stu-id="8b813-216">a.</span></span> <span data-ttu-id="8b813-217">Wybierz **tworzenie użytkowników w katalogu wewnętrzny zlewiska firmy, w razie potrzeby** , a następnie wprowadź odpowiednią nazwę hello hello grupy użytkowników (może być wiele nie.</span><span class="sxs-lookup"><span data-stu-id="8b813-217">Select **Create users in Confluence's internal Directory if needed** and enter hello appropriate name of hello group for users (can be multiple no.</span></span> <span data-ttu-id="8b813-218">grup rozdzielone przecinkami).</span><span class="sxs-lookup"><span data-stu-id="8b813-218">of groups separated by comma).</span></span>

    <span data-ttu-id="8b813-219">b.</span><span class="sxs-lookup"><span data-stu-id="8b813-219">b.</span></span> <span data-ttu-id="8b813-220">Kliknij przycisk **Dalej**.</span><span class="sxs-lookup"><span data-stu-id="8b813-220">Click **Next**.</span></span>

23. <span data-ttu-id="8b813-221">Kliknij przycisk **Zakończ**.</span><span class="sxs-lookup"><span data-stu-id="8b813-221">Click **Finish**.</span></span>   

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-kantegassoforconfluence-tutorial/addon11.png)

24. <span data-ttu-id="8b813-223">Na powitania **znanych domeny dla usługi Azure AD** sekcji, wykonaj następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="8b813-223">On hello **Known domains for Azure AD** section, perform following steps:</span></span> 

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-kantegassoforconfluence-tutorial/addon12.png)

    <span data-ttu-id="8b813-225">a.</span><span class="sxs-lookup"><span data-stu-id="8b813-225">a.</span></span> <span data-ttu-id="8b813-226">Wybierz **znane domen** z lewego panelu hello hello strony.</span><span class="sxs-lookup"><span data-stu-id="8b813-226">Select **Known domains** from hello left panel of hello page.</span></span>

    <span data-ttu-id="8b813-227">b.</span><span class="sxs-lookup"><span data-stu-id="8b813-227">b.</span></span> <span data-ttu-id="8b813-228">Wprowadź nazwę domeny w hello **znane domen** pola tekstowego.</span><span class="sxs-lookup"><span data-stu-id="8b813-228">Enter domain name in hello **Known domains** textbox.</span></span>

    <span data-ttu-id="8b813-229">c.</span><span class="sxs-lookup"><span data-stu-id="8b813-229">c.</span></span> <span data-ttu-id="8b813-230">Kliknij pozycję **Zapisz**.</span><span class="sxs-lookup"><span data-stu-id="8b813-230">Click **Save**.</span></span> 

> [!TIP]
> <span data-ttu-id="8b813-231">Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz hello [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji hello!</span><span class="sxs-lookup"><span data-stu-id="8b813-231">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="8b813-232">Po dodaniu tej aplikacji z hello **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij hello **rejestracji jednokrotnej** hello kartę i dostępu do osadzonych dokumentacji za pośrednictwem hello  **Konfiguracja** sekcji u dołu hello.</span><span class="sxs-lookup"><span data-stu-id="8b813-232">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="8b813-233">Więcej o hello osadzonych dokumentacji funkcji w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="8b813-233">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="8b813-234">Tworzenie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="8b813-234">Creating an Azure AD test user</span></span>
<span data-ttu-id="8b813-235">Celem Hello w tej sekcji jest toocreate użytkownika testowego, w portalu Azure o nazwie Simona Britta hello.</span><span class="sxs-lookup"><span data-stu-id="8b813-235">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Tworzenie użytkowników usługi Azure AD][100]

<span data-ttu-id="8b813-237">**toocreate użytkownika testowego w usłudze Azure AD, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="8b813-237">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="8b813-238">W hello **portalu Azure**na temat hello w lewym okienku nawigacji, kliknij przycisk **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="8b813-238">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-kantegassoforconfluence-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="8b813-240">toodisplay hello listę użytkowników, przejdź zbyt**użytkowników i grup** i kliknij przycisk **wszyscy użytkownicy**.</span><span class="sxs-lookup"><span data-stu-id="8b813-240">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-kantegassoforconfluence-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="8b813-242">Witaj tooopen **użytkownika** okna dialogowego, kliknij przycisk **Dodaj** u góry hello hello okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="8b813-242">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-kantegassoforconfluence-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="8b813-244">Na powitania **użytkownika** okna dialogowego wykonaj hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="8b813-244">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-kantegassoforconfluence-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="8b813-246">a.</span><span class="sxs-lookup"><span data-stu-id="8b813-246">a.</span></span> <span data-ttu-id="8b813-247">W hello **nazwa** pole tekstowe, typ **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="8b813-247">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="8b813-248">b.</span><span class="sxs-lookup"><span data-stu-id="8b813-248">b.</span></span> <span data-ttu-id="8b813-249">W hello **nazwy użytkownika** pole tekstowe, hello typu **adres e-mail** z BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="8b813-249">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="8b813-250">c.</span><span class="sxs-lookup"><span data-stu-id="8b813-250">c.</span></span> <span data-ttu-id="8b813-251">Wybierz **Pokaż hasło** i zanotuj wartość hello hello **hasło**.</span><span class="sxs-lookup"><span data-stu-id="8b813-251">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="8b813-252">d.</span><span class="sxs-lookup"><span data-stu-id="8b813-252">d.</span></span> <span data-ttu-id="8b813-253">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="8b813-253">Click **Create**.</span></span>
 
### <a name="creating-a-kantega-sso-for-confluence-test-user"></a><span data-ttu-id="8b813-254">Tworzenie Kantega Usługa rejestracji Jednokrotnej dla użytkownika testowego zlewiska</span><span class="sxs-lookup"><span data-stu-id="8b813-254">Creating a Kantega SSO for Confluence test user</span></span>

<span data-ttu-id="8b813-255">toolog użytkowników tooenable usługi Azure AD w tooConfluence, muszą mieć przydzielone do zlewiska.</span><span class="sxs-lookup"><span data-stu-id="8b813-255">tooenable Azure AD users toolog in tooConfluence, they must be provisioned into Confluence.</span></span> <span data-ttu-id="8b813-256">W przypadku hello Kantega sesji rejestracji jednokrotnej dla zlewiska Inicjowanie obsługi to zadanie ręczne.</span><span class="sxs-lookup"><span data-stu-id="8b813-256">In hello case of Kantega SSO for Confluence, provisioning is a manual task.</span></span>

<span data-ttu-id="8b813-257">**tooprovision konta użytkownika, należy wykonać hello następujące kroki:**</span><span class="sxs-lookup"><span data-stu-id="8b813-257">**tooprovision a user account, perform hello following steps:**</span></span>

1. <span data-ttu-id="8b813-258">Zaloguj się za tooyour logowania jednokrotnego Kantega zlewiska witryny firmy jako administrator.</span><span class="sxs-lookup"><span data-stu-id="8b813-258">Log in tooyour Kantega SSO for Confluence company site as an administrator.</span></span>

2. <span data-ttu-id="8b813-259">Umieść kursor na koło zębate, a następnie kliknij przycisk hello **Zarządzanie użytkownikami**.</span><span class="sxs-lookup"><span data-stu-id="8b813-259">Hover on cog and click hello **User management**.</span></span>

    ![Dodawanie pracownika](./media/active-directory-saas-kantegassoforconfluence-tutorial/user1.png) 

3. <span data-ttu-id="8b813-261">W sekcji Użytkownicy kliknij **Dodaj użytkowników** kartę. Na powitania **"Dodaj użytkownika"** okna dialogowego wykonaj hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="8b813-261">Under Users section, click **Add Users** tab. On hello **“Add a User”** dialog page, perform hello following steps:</span></span>

    ![Dodawanie pracownika](./media/active-directory-saas-kantegassoforconfluence-tutorial/user2.png) 

    <span data-ttu-id="8b813-263">a.</span><span class="sxs-lookup"><span data-stu-id="8b813-263">a.</span></span> <span data-ttu-id="8b813-264">W hello **Username** pole tekstowe, powitalne wiadomości e-mail użytkownika, takich jak Brittasimon@contoso.com.</span><span class="sxs-lookup"><span data-stu-id="8b813-264">In hello **Username** textbox, type hello email of user like Brittasimon@contoso.com.</span></span>

    <span data-ttu-id="8b813-265">b.</span><span class="sxs-lookup"><span data-stu-id="8b813-265">b.</span></span> <span data-ttu-id="8b813-266">W hello **imię i nazwisko** pole tekstowe, typ hello pełną nazwę użytkownika, takich jak Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="8b813-266">In hello **Full Name** textbox, type hello full name of user like Britta Simon.</span></span>

    <span data-ttu-id="8b813-267">c.</span><span class="sxs-lookup"><span data-stu-id="8b813-267">c.</span></span> <span data-ttu-id="8b813-268">W hello **E-mail** pole tekstowe, typ hello adres e-mail użytkownika, takich jak Brittasimon@contoso.com.</span><span class="sxs-lookup"><span data-stu-id="8b813-268">In hello **Email** textbox, type hello email address of user like Brittasimon@contoso.com.</span></span>

    <span data-ttu-id="8b813-269">d.</span><span class="sxs-lookup"><span data-stu-id="8b813-269">d.</span></span> <span data-ttu-id="8b813-270">W hello **hasło** tekstowym, wpisz hello hasło dla użytkownika.</span><span class="sxs-lookup"><span data-stu-id="8b813-270">In hello **Password** textbox, type hello password for user.</span></span>

    <span data-ttu-id="8b813-271">e.</span><span class="sxs-lookup"><span data-stu-id="8b813-271">e.</span></span> <span data-ttu-id="8b813-272">Kliknij przycisk **Potwierdź hasło** ponownie hello hasła.</span><span class="sxs-lookup"><span data-stu-id="8b813-272">Click **Confirm Password** reenter hello password.</span></span>
    
    <span data-ttu-id="8b813-273">f.</span><span class="sxs-lookup"><span data-stu-id="8b813-273">f.</span></span> <span data-ttu-id="8b813-274">Kliknij przycisk **Dodaj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="8b813-274">Click **Add** button.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="8b813-275">Przypisanie użytkownika testowego hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="8b813-275">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="8b813-276">W tej sekcji możesz włączyć toouse Simona Britta Azure logowania jednokrotnego za udzielanie dostępu tooKantega logowania jednokrotnego dla zlewiska.</span><span class="sxs-lookup"><span data-stu-id="8b813-276">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooKantega SSO for Confluence.</span></span>

![Przypisz użytkownika][200] 

<span data-ttu-id="8b813-278">**tooassign tooKantega Simona Britta logowania jednokrotnego dla zlewiska, wykonaj hello następujące kroki:**</span><span class="sxs-lookup"><span data-stu-id="8b813-278">**tooassign Britta Simon tooKantega SSO for Confluence, perform hello following steps:**</span></span>

1. <span data-ttu-id="8b813-279">W portalu Azure hello, otwórz widok aplikacji hello, a następnie przejdź do widoku katalogu toohello i przejść za**aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="8b813-279">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Przypisz użytkownika][201] 

2. <span data-ttu-id="8b813-281">Z listy aplikacji hello wybierz **Kantega Usługa rejestracji Jednokrotnej dla zlewiska**.</span><span class="sxs-lookup"><span data-stu-id="8b813-281">In hello applications list, select **Kantega SSO for Confluence**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-kantegassoforconfluence-tutorial/tutorial_kantegassoforconfluence_app.png) 

3. <span data-ttu-id="8b813-283">W menu powitania po lewej stronie powitania kliknij **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="8b813-283">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Przypisz użytkownika][202] 

4. <span data-ttu-id="8b813-285">Kliknij przycisk **Dodaj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="8b813-285">Click **Add** button.</span></span> <span data-ttu-id="8b813-286">Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="8b813-286">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Przypisz użytkownika][203]

5. <span data-ttu-id="8b813-288">Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** hello listy użytkowników.</span><span class="sxs-lookup"><span data-stu-id="8b813-288">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="8b813-289">Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="8b813-289">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="8b813-290">Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="8b813-290">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="8b813-291">Testowanie rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="8b813-291">Testing single sign-on</span></span>

<span data-ttu-id="8b813-292">W tej sekcji można przetestować konfiguracji usługi Azure AD pojedynczego logowania jednokrotnego przy użyciu hello panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="8b813-292">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="8b813-293">Po kliknięciu hello Kantega logowania jednokrotnego dla zlewiska kafelka w hello Panel dostępu, należy pobrać automatycznie zalogowane tooyour Kantega logowania jednokrotnego dla aplikacji zlewiska.</span><span class="sxs-lookup"><span data-stu-id="8b813-293">When you click hello Kantega SSO for Confluence tile in hello Access Panel, you should get automatically signed-on tooyour Kantega SSO for Confluence application.</span></span>
<span data-ttu-id="8b813-294">Aby uzyskać więcej informacji na temat panelu dostępu, zobacz [toohello wprowadzenie panelu dostępu](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="8b813-294">For more information about the Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="8b813-295">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="8b813-295">Additional resources</span></span>

* [<span data-ttu-id="8b813-296">Lista samouczków dotyczących tooIntegrate aplikacji SaaS w usłudze Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="8b813-296">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="8b813-297">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="8b813-297">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-kantegassoforconfluence-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-kantegassoforconfluence-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-kantegassoforconfluence-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-kantegassoforconfluence-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-kantegassoforconfluence-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-kantegassoforconfluence-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-kantegassoforconfluence-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-kantegassoforconfluence-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-kantegassoforconfluence-tutorial/tutorial_general_203.png

