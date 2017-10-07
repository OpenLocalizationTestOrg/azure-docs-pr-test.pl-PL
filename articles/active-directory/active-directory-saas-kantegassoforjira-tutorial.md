---
title: 'Samouczek: Azure Active Directory integracji z logowaniem Jednokrotnym Kantega dla JIRA | Dokumentacja firmy Microsoft'
description: "Dowiedz się, jak tooconfigure logowanie jednokrotne między usługą Azure Active Directory i logowania jednokrotnego Kantega dla JIRA."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: e2af4891-e3c8-43b3-bdcb-0500c493e9b4
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: jeedes
ms.openlocfilehash: 67894cc55ef91d0991c62e0e4f1be712723cb474
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-kantega-sso-for-jira"></a><span data-ttu-id="e924d-103">Samouczek: Azure Active Directory integracji z logowaniem Jednokrotnym Kantega dla JIRA</span><span class="sxs-lookup"><span data-stu-id="e924d-103">Tutorial: Azure Active Directory integration with Kantega SSO for JIRA</span></span>

<span data-ttu-id="e924d-104">Z tego samouczka, dowiesz się, jak toointegrate logowania jednokrotnego Kantega dla JIRA w usłudze Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="e924d-104">In this tutorial, you learn how toointegrate Kantega SSO for JIRA with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="e924d-105">Integracja z usługą Azure AD logowania jednokrotnego Kantega dla JIRA zapewnia hello następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="e924d-105">Integrating Kantega SSO for JIRA with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="e924d-106">Można kontrolować w usłudze Azure AD, kto ma dostęp tooKantega logowania jednokrotnego dla JIRA</span><span class="sxs-lookup"><span data-stu-id="e924d-106">You can control in Azure AD who has access tooKantega SSO for JIRA</span></span>
- <span data-ttu-id="e924d-107">Można włączyć użytkownika użytkownicy tooautomatically get zalogowane tooKantega logowania jednokrotnego dla JIRA (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="e924d-107">You can enable your users tooautomatically get signed-on tooKantega SSO for JIRA (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="e924d-108">Możesz zarządzać kont w jednej centralnej lokalizacji - hello portalu Azure</span><span class="sxs-lookup"><span data-stu-id="e924d-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="e924d-109">Jeśli chcesz tooknow więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="e924d-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e924d-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="e924d-110">Prerequisites</span></span>

<span data-ttu-id="e924d-111">tooconfigure integracji usługi Azure AD z logowania jednokrotnego Kantega dla JIRA należy hello następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="e924d-111">tooconfigure Azure AD integration with Kantega SSO for JIRA, you need hello following items:</span></span>

- <span data-ttu-id="e924d-112">Subskrypcję usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="e924d-112">An Azure AD subscription</span></span>
- <span data-ttu-id="e924d-113">Kantega Usługa rejestracji Jednokrotnej dla JIRA logowanie jednokrotne włączone subskrypcji</span><span class="sxs-lookup"><span data-stu-id="e924d-113">A Kantega SSO for JIRA single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="e924d-114">tootest hello kroków w tym samouczku, zaleca się przy użyciu środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="e924d-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="e924d-115">tootest hello kroki opisane w tym samouczku, należy stosować te zalecenia:</span><span class="sxs-lookup"><span data-stu-id="e924d-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="e924d-116">Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="e924d-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="e924d-117">Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz pobrać miesięczna wersja próbna [tutaj](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="e924d-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="e924d-118">Opis scenariusza</span><span class="sxs-lookup"><span data-stu-id="e924d-118">Scenario description</span></span>
<span data-ttu-id="e924d-119">W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym.</span><span class="sxs-lookup"><span data-stu-id="e924d-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="e924d-120">Scenariusz Hello opisane w tym samouczku składa się z dwóch głównych elementów:</span><span class="sxs-lookup"><span data-stu-id="e924d-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="e924d-121">Dodawanie logowania jednokrotnego Kantega dla JIRA z galerii hello</span><span class="sxs-lookup"><span data-stu-id="e924d-121">Adding Kantega SSO for JIRA from hello gallery</span></span>
2. <span data-ttu-id="e924d-122">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="e924d-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-kantega-sso-for-jira-from-hello-gallery"></a><span data-ttu-id="e924d-123">Dodawanie logowania jednokrotnego Kantega dla JIRA z galerii hello</span><span class="sxs-lookup"><span data-stu-id="e924d-123">Adding Kantega SSO for JIRA from hello gallery</span></span>
<span data-ttu-id="e924d-124">tooconfigure hello włączenia logowania jednokrotnego Kantega dla JIRA do usługi Azure AD, należy tooadd Kantega logowania jednokrotnego dla JIRA z hello galerii tooyour listę zarządzanych aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="e924d-124">tooconfigure hello integration of Kantega SSO for JIRA into Azure AD, you need tooadd Kantega SSO for JIRA from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="e924d-125">**tooadd Kantega Usługa rejestracji Jednokrotnej dla JIRA z galerii hello wykonaj hello następujące kroki:**</span><span class="sxs-lookup"><span data-stu-id="e924d-125">**tooadd Kantega SSO for JIRA from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="e924d-126">W hello  **[portalu Azure](https://portal.azure.com)**na temat hello panelu nawigacji po lewej stronie, kliknij przycisk **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="e924d-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Usługa Active Directory][1]

2. <span data-ttu-id="e924d-128">Przejdź za**aplikacje dla przedsiębiorstw**.</span><span class="sxs-lookup"><span data-stu-id="e924d-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="e924d-129">Następnie przejdź zbyt**wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="e924d-129">Then go too**All applications**.</span></span>

    ![Aplikacje][2]
    
3. <span data-ttu-id="e924d-131">tooadd nową aplikację, kliknij przycisk **nowej aplikacji** przycisk u góry hello okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="e924d-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplikacje][3]

4. <span data-ttu-id="e924d-133">W polu wyszukiwania hello wpisz **Kantega Usługa rejestracji Jednokrotnej dla JIRA**.</span><span class="sxs-lookup"><span data-stu-id="e924d-133">In hello search box, type **Kantega SSO for JIRA**.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-kantegassoforjira-tutorial/tutorial_kantegassoforjira_search.png)

5. <span data-ttu-id="e924d-135">W panelu wyników hello, wybierz **Kantega Usługa rejestracji Jednokrotnej dla JIRA**, a następnie kliknij przycisk **Dodaj** przycisk aplikacji hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="e924d-135">In hello results panel, select **Kantega SSO for JIRA**, and then click **Add** button tooadd hello application.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-kantegassoforjira-tutorial/tutorial_kantegassoforjira_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="e924d-137">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="e924d-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="e924d-138">W tej sekcji skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z logowania jednokrotnego Kantega dla JIRA w oparciu o nazwie "Britta Simona" użytkownika testowego.</span><span class="sxs-lookup"><span data-stu-id="e924d-138">In this section, you configure and test Azure AD single sign-on with Kantega SSO for JIRA based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="e924d-139">Dla pojedynczego logowania jednokrotnego toowork usługi Azure AD musi tooknow użytkownika odpowiednikiem hello w rejestracji Jednokrotnej Kantega dla JIRA jest tooa użytkownika w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="e924d-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Kantega SSO for JIRA is tooa user in Azure AD.</span></span> <span data-ttu-id="e924d-140">Innymi słowy relację łącza między użytkownika usługi Azure AD i hello użytkownikowi w rejestracji Jednokrotnej Kantega dla JIRA musi toobe ustanowione.</span><span class="sxs-lookup"><span data-stu-id="e924d-140">In other words, a link relationship between an Azure AD user and hello related user in Kantega SSO for JIRA needs toobe established.</span></span>

<span data-ttu-id="e924d-141">W Kantega logowania jednokrotnego dla JIRA, należy przypisać wartość hello hello **nazwy użytkownika** w usłudze Azure AD jako wartość hello hello **Username** tooestablish hello łącze relacji.</span><span class="sxs-lookup"><span data-stu-id="e924d-141">In Kantega SSO for JIRA, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="e924d-142">tooconfigure i testowanie usługi Azure AD rejestracji jednokrotnej z logowania jednokrotnego Kantega JIRA, należy po bloków konstrukcyjnych hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="e924d-142">tooconfigure and test Azure AD single sign-on with Kantega SSO for JIRA, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="e924d-143">**[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configuring-azure-ad-single-sign-on)**  -tooenable Twojego toouse użytkowników tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="e924d-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="e924d-144">**[Tworzenie użytkownika testowego usługi Azure AD](#creating-an-azure-ad-test-user)**  -tootest usługi Azure AD rejestracji jednokrotnej z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="e924d-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="e924d-145">**[Tworzenie Kantega Usługa rejestracji Jednokrotnej dla użytkownika testowego JIRA](#creating-a-kantega-sso-for-jira-test-user)**  -toohave odpowiednikiem Simona Britta w rejestracji Jednokrotnej Kantega dla JIRA, który jest połączony toohello usługi Azure AD reprezentację użytkownika.</span><span class="sxs-lookup"><span data-stu-id="e924d-145">**[Creating a Kantega SSO for JIRA test user](#creating-a-kantega-sso-for-jira-test-user)** - toohave a counterpart of Britta Simon in Kantega SSO for JIRA that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="e924d-146">**[Przypisanie użytkownika testowego hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Simona Britta toouse usługi Azure AD rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="e924d-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="e924d-147">**[Testowanie rejestracji jednokrotnej](#testing-single-sign-on)**  -tooverify czy hello konfiguracji działania.</span><span class="sxs-lookup"><span data-stu-id="e924d-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="e924d-148">Konfigurowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="e924d-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="e924d-149">W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w hello portalu Azure i skonfigurować rejestracji jednokrotnej w Twojej rejestracji Jednokrotnej Kantega JIRA aplikacji.</span><span class="sxs-lookup"><span data-stu-id="e924d-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Kantega SSO for JIRA application.</span></span>

<span data-ttu-id="e924d-150">**tooconfigure usługi Azure AD rejestracji jednokrotnej z logowania jednokrotnego Kantega dla JIRA, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="e924d-150">**tooconfigure Azure AD single sign-on with Kantega SSO for JIRA, perform hello following steps:**</span></span>

1. <span data-ttu-id="e924d-151">W portalu Azure na powitania hello **Kantega Usługa rejestracji Jednokrotnej dla JIRA** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.</span><span class="sxs-lookup"><span data-stu-id="e924d-151">In hello Azure portal, on hello **Kantega SSO for JIRA** application integration page, click **Single sign-on**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej][4]

2. <span data-ttu-id="e924d-153">Na powitania **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** tooenable rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="e924d-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-kantegassoforjira-tutorial/tutorial_kantegassoforjira_samlbase.png)

3. <span data-ttu-id="e924d-155">W **IDP** inicjowane tryb na powitania **logowania jednokrotnego Kantega JIRA domeny i adresów URL** sekcji wykonać powitania po kroku:</span><span class="sxs-lookup"><span data-stu-id="e924d-155">In **IDP** initiated mode, on hello **Kantega SSO for JIRA Domain and URLs** section perform hello following step:</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-kantegassoforjira-tutorial/tutorial_kantegassoforjira_url1.png)

    <span data-ttu-id="e924d-157">a.</span><span class="sxs-lookup"><span data-stu-id="e924d-157">a.</span></span> <span data-ttu-id="e924d-158">W hello **identyfikator** tekstowym, wpisz adres URL za pomocą hello następującego wzorca:`https://<server-base-url>/plugins/servlet/no.kantega.saml/sp/<uniqueid>/login`</span><span class="sxs-lookup"><span data-stu-id="e924d-158">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<server-base-url>/plugins/servlet/no.kantega.saml/sp/<uniqueid>/login`</span></span>

    <span data-ttu-id="e924d-159">b.</span><span class="sxs-lookup"><span data-stu-id="e924d-159">b.</span></span> <span data-ttu-id="e924d-160">W hello **adres URL odpowiedzi** tekstowym, wpisz adres URL za pomocą hello następującego wzorca:`https://<server-base-url>/plugins/servlet/no.kantega.saml/sp/<uniqueid>/login`</span><span class="sxs-lookup"><span data-stu-id="e924d-160">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://<server-base-url>/plugins/servlet/no.kantega.saml/sp/<uniqueid>/login`</span></span>

4. <span data-ttu-id="e924d-161">W **SP** inicjowane trybie wyboru **Pokaż zaawansowane ustawienia adresu URL** i wykonywać powitania po kroku:</span><span class="sxs-lookup"><span data-stu-id="e924d-161">In **SP** initiated mode, check **Show advanced URL settings** and  perform hello following step:</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-kantegassoforjira-tutorial/tutorial_kantegassoforjira_url2.png)

    <span data-ttu-id="e924d-163">W hello **adres URL logowania** tekstowym, wpisz adres URL za pomocą hello następującego wzorca:`https://<server-base-url>/plugins/servlet/no.kantega.saml/sp/<uniqueid>/login`</span><span class="sxs-lookup"><span data-stu-id="e924d-163">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<server-base-url>/plugins/servlet/no.kantega.saml/sp/<uniqueid>/login`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="e924d-164">Wartości te nie są prawdziwe.</span><span class="sxs-lookup"><span data-stu-id="e924d-164">These values are not real.</span></span> <span data-ttu-id="e924d-165">Zaktualizować te wartości z hello rzeczywisty identyfikator, adres URL odpowiedzi i adres URL logowania.</span><span class="sxs-lookup"><span data-stu-id="e924d-165">Update these values with hello actual Identifier, Reply URL, and Sign-On URL.</span></span> <span data-ttu-id="e924d-166">Te wartości są odbierane podczas konfigurowania hello Jira wtyczki, który znajduje się w dalszej części samouczka hello.</span><span class="sxs-lookup"><span data-stu-id="e924d-166">These values are received during hello configuration of Jira plugin, which is explained later in hello tutorial.</span></span>

5. <span data-ttu-id="e924d-167">Na powitania **certyfikat podpisywania SAML** kliknij **XML metadanych** , a następnie zapisz plik metadanych hello na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="e924d-167">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-kantegassoforjira-tutorial/tutorial_kantegassoforjira_certificate.png) 

6. <span data-ttu-id="e924d-169">Kliknij przycisk **zapisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="e924d-169">Click **Save** button.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-kantegassoforjira-tutorial/tutorial_general_400.png)
    
7. <span data-ttu-id="e924d-171">W oknie przeglądarki innej witryny sieci web Zaloguj się za tooyour JIRA na lokalnym serwerze jako administrator.</span><span class="sxs-lookup"><span data-stu-id="e924d-171">In a different web browser window, log in tooyour JIRA on premise server as an administrator.</span></span>

8. <span data-ttu-id="e924d-172">Umieść kursor na koło zębate, a następnie kliknij przycisk hello **dodatki**.</span><span class="sxs-lookup"><span data-stu-id="e924d-172">Hover on cog and click hello **Add-ons**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-kantegassoforjira-tutorial/addon1.png)

9. <span data-ttu-id="e924d-174">W sekcji Karta dodatki, kliknij przycisk **znaleźć nowe dodatki**.</span><span class="sxs-lookup"><span data-stu-id="e924d-174">Under Add-ons tab section, click **Find new add-ons**.</span></span> <span data-ttu-id="e924d-175">Wyszukiwanie **Kantega Usługa rejestracji Jednokrotnej dla JIRA (SAML i protokołu Kerberos)** i kliknij przycisk **zainstalować** tooinstall przycisk hello nowej wtyczki SAML.</span><span class="sxs-lookup"><span data-stu-id="e924d-175">Search **Kantega SSO for JIRA (SAML & Kerberos)** and click **Install** button tooinstall hello new SAML plugin.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-kantegassoforjira-tutorial/addon2.png)

10. <span data-ttu-id="e924d-177">rozpoczyna się instalacja dodatku Hello.</span><span class="sxs-lookup"><span data-stu-id="e924d-177">hello plugin installation starts.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-kantegassoforjira-tutorial/addon3.png)

11. <span data-ttu-id="e924d-179">Po zakończeniu instalacji hello.</span><span class="sxs-lookup"><span data-stu-id="e924d-179">Once hello installation is complete.</span></span> <span data-ttu-id="e924d-180">Kliknij przycisk **Zamknij**.</span><span class="sxs-lookup"><span data-stu-id="e924d-180">Click **Close**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-kantegassoforjira-tutorial/addon33.png)

12. <span data-ttu-id="e924d-182">Kliknij pozycję **Zarządzaj**.</span><span class="sxs-lookup"><span data-stu-id="e924d-182">Click **Manage**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-kantegassoforjira-tutorial/addon34.png)
    
13. <span data-ttu-id="e924d-184">Nowej wtyczki znajduje się w obszarze **integracji**.</span><span class="sxs-lookup"><span data-stu-id="e924d-184">New plugin is listed under **INTEGRATIONS**.</span></span> <span data-ttu-id="e924d-185">Kliknij przycisk **Konfiguruj** tooconfigure hello nowej wtyczki.</span><span class="sxs-lookup"><span data-stu-id="e924d-185">Click **Configure** tooconfigure hello new plugin.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-kantegassoforjira-tutorial/addon35.png)

14. <span data-ttu-id="e924d-187">W hello **SAML** sekcji.</span><span class="sxs-lookup"><span data-stu-id="e924d-187">In hello **SAML** section.</span></span> <span data-ttu-id="e924d-188">Wybierz **usługi Azure Active Directory (Azure AD)** z hello **dostawcy tożsamości Dodaj** listy rozwijanej.</span><span class="sxs-lookup"><span data-stu-id="e924d-188">Select **Azure Active Directory (Azure AD)** from hello **Add identity provider** dropdown.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-kantegassoforjira-tutorial/addon4.png)

15. <span data-ttu-id="e924d-190">Wybierz poziom subskrypcji jako **podstawowe**.</span><span class="sxs-lookup"><span data-stu-id="e924d-190">Select subscription level as **Basic**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-kantegassoforjira-tutorial/addon5.png)     

16. <span data-ttu-id="e924d-192">Na powitania **właściwości aplikacji** sekcji, wykonaj następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="e924d-192">On hello **App properties** section, perform following steps:</span></span> 

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-kantegassoforjira-tutorial/addon6.png)

    <span data-ttu-id="e924d-194">a.</span><span class="sxs-lookup"><span data-stu-id="e924d-194">a.</span></span> <span data-ttu-id="e924d-195">Kopiuj hello **identyfikator URI aplikacji** wartości i używać go jako **identyfikator, adres URL odpowiedzi i adres URL logowania** na powitania **logowania jednokrotnego Kantega JIRA domeny i adresów URL** sekcji w portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="e924d-195">Copy hello **App ID URI** value and use it as **Identifier, Reply URL, and Sign-On URL** on hello **Kantega SSO for JIRA Domain and URLs** section in Azure portal.</span></span>

    <span data-ttu-id="e924d-196">b.</span><span class="sxs-lookup"><span data-stu-id="e924d-196">b.</span></span> <span data-ttu-id="e924d-197">Kliknij przycisk **Dalej**.</span><span class="sxs-lookup"><span data-stu-id="e924d-197">Click **Next**.</span></span>

17. <span data-ttu-id="e924d-198">Na powitania **importu metadanych** sekcji, wykonaj następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="e924d-198">On hello **Metadata import** section, perform following steps:</span></span> 

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-kantegassoforjira-tutorial/addon7.png)

    <span data-ttu-id="e924d-200">a.</span><span class="sxs-lookup"><span data-stu-id="e924d-200">a.</span></span> <span data-ttu-id="e924d-201">Wybierz **pliku metadanych na tym komputerze**i przekazywanie pliku metadanych, który został pobrany z portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="e924d-201">Select **Metadata file on my computer**, and upload metadata file, which you have downloaded from Azure portal.</span></span>

    <span data-ttu-id="e924d-202">b.</span><span class="sxs-lookup"><span data-stu-id="e924d-202">b.</span></span> <span data-ttu-id="e924d-203">Kliknij przycisk **Dalej**.</span><span class="sxs-lookup"><span data-stu-id="e924d-203">Click **Next**.</span></span>

18. <span data-ttu-id="e924d-204">Na powitania **nazwę i logowania jednokrotnego lokalizację** sekcji, wykonaj następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="e924d-204">On hello **Name and SSO location** section, perform following steps:</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-kantegassoforjira-tutorial/addon8.png)
    
    <span data-ttu-id="e924d-206">a.</span><span class="sxs-lookup"><span data-stu-id="e924d-206">a.</span></span> <span data-ttu-id="e924d-207">Dodaj nazwę hello dostawcy tożsamości w **Nazwa dostawcy tożsamości** pola tekstowego (np. usługi Azure AD).</span><span class="sxs-lookup"><span data-stu-id="e924d-207">Add Name of hello Identity Provider in **Identity provider name** textbox (e.g Azure AD).</span></span>

    <span data-ttu-id="e924d-208">b.</span><span class="sxs-lookup"><span data-stu-id="e924d-208">b.</span></span> <span data-ttu-id="e924d-209">Kliknij przycisk **Dalej**.</span><span class="sxs-lookup"><span data-stu-id="e924d-209">Click **Next**.</span></span>

19. <span data-ttu-id="e924d-210">Sprawdź hello certyfikatu podpisywania, a następnie kliknij przycisk **dalej**.</span><span class="sxs-lookup"><span data-stu-id="e924d-210">Verify hello Signing certificate and click **Next**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-kantegassoforjira-tutorial/addon9.png)

20. <span data-ttu-id="e924d-212">Na powitania **kont użytkowników JIRA** sekcji, wykonaj następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="e924d-212">On hello **JIRA user accounts** section, perform following steps:</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-kantegassoforjira-tutorial/addon10.png)

    <span data-ttu-id="e924d-214">a.</span><span class="sxs-lookup"><span data-stu-id="e924d-214">a.</span></span> <span data-ttu-id="e924d-215">Wybierz **tworzenie użytkowników w katalogu wewnętrzny JIRA firmy, w razie potrzeby** , a następnie wprowadź odpowiednią nazwę hello hello grupy użytkowników (może być wiele nie.</span><span class="sxs-lookup"><span data-stu-id="e924d-215">Select **Create users in JIRA's internal Directory if needed** and enter hello appropriate name of hello group for users (can be multiple no.</span></span> <span data-ttu-id="e924d-216">grup rozdzielone przecinkami).</span><span class="sxs-lookup"><span data-stu-id="e924d-216">of groups separated by comma).</span></span>

    <span data-ttu-id="e924d-217">b.</span><span class="sxs-lookup"><span data-stu-id="e924d-217">b.</span></span> <span data-ttu-id="e924d-218">Kliknij przycisk **Dalej**.</span><span class="sxs-lookup"><span data-stu-id="e924d-218">Click **Next**.</span></span>

21. <span data-ttu-id="e924d-219">Kliknij przycisk **Zakończ**.</span><span class="sxs-lookup"><span data-stu-id="e924d-219">Click **Finish**.</span></span>   

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-kantegassoforjira-tutorial/addon11.png)

22. <span data-ttu-id="e924d-221">Na powitania **znanych domeny dla usługi Azure AD** sekcji, wykonaj następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="e924d-221">On hello **Known domains for Azure AD** section, perform following steps:</span></span> 

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-kantegassoforjira-tutorial/addon12.png)

    <span data-ttu-id="e924d-223">a.</span><span class="sxs-lookup"><span data-stu-id="e924d-223">a.</span></span> <span data-ttu-id="e924d-224">Wybierz **znane domen** z lewego panelu hello hello strony.</span><span class="sxs-lookup"><span data-stu-id="e924d-224">Select **Known domains** from hello left panel of hello page.</span></span>

    <span data-ttu-id="e924d-225">b.</span><span class="sxs-lookup"><span data-stu-id="e924d-225">b.</span></span> <span data-ttu-id="e924d-226">Wprowadź nazwę domeny w hello **znane domen** pola tekstowego.</span><span class="sxs-lookup"><span data-stu-id="e924d-226">Enter domain name in hello **Known domains** textbox.</span></span>

    <span data-ttu-id="e924d-227">c.</span><span class="sxs-lookup"><span data-stu-id="e924d-227">c.</span></span> <span data-ttu-id="e924d-228">Kliknij pozycję **Zapisz**.</span><span class="sxs-lookup"><span data-stu-id="e924d-228">Click **Save**.</span></span> 

> [!TIP]
> <span data-ttu-id="e924d-229">Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz hello [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji hello!</span><span class="sxs-lookup"><span data-stu-id="e924d-229">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="e924d-230">Po dodaniu tej aplikacji z hello **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij hello **rejestracji jednokrotnej** hello kartę i dostępu do osadzonych dokumentacji za pośrednictwem hello  **Konfiguracja** sekcji u dołu hello.</span><span class="sxs-lookup"><span data-stu-id="e924d-230">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="e924d-231">Więcej o hello osadzonych dokumentacji funkcji w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="e924d-231">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="e924d-232">Tworzenie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="e924d-232">Creating an Azure AD test user</span></span>
<span data-ttu-id="e924d-233">Celem Hello w tej sekcji jest toocreate użytkownika testowego, w portalu Azure o nazwie Simona Britta hello.</span><span class="sxs-lookup"><span data-stu-id="e924d-233">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Tworzenie użytkowników usługi Azure AD][100]

<span data-ttu-id="e924d-235">**toocreate użytkownika testowego w usłudze Azure AD, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="e924d-235">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="e924d-236">W hello **portalu Azure**na temat hello w lewym okienku nawigacji, kliknij przycisk **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="e924d-236">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-kantegassoforjira-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="e924d-238">toodisplay hello listę użytkowników, przejdź zbyt**użytkowników i grup** i kliknij przycisk **wszyscy użytkownicy**.</span><span class="sxs-lookup"><span data-stu-id="e924d-238">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-kantegassoforjira-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="e924d-240">Witaj tooopen **użytkownika** okna dialogowego, kliknij przycisk **Dodaj** u góry hello hello okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="e924d-240">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-kantegassoforjira-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="e924d-242">Na powitania **użytkownika** okna dialogowego wykonaj hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="e924d-242">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-kantegassoforjira-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="e924d-244">a.</span><span class="sxs-lookup"><span data-stu-id="e924d-244">a.</span></span> <span data-ttu-id="e924d-245">W hello **nazwa** pole tekstowe, typ **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="e924d-245">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="e924d-246">b.</span><span class="sxs-lookup"><span data-stu-id="e924d-246">b.</span></span> <span data-ttu-id="e924d-247">W hello **nazwy użytkownika** pole tekstowe, hello typu **adres e-mail** z BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="e924d-247">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="e924d-248">c.</span><span class="sxs-lookup"><span data-stu-id="e924d-248">c.</span></span> <span data-ttu-id="e924d-249">Wybierz **Pokaż hasło** i zanotuj wartość hello hello **hasło**.</span><span class="sxs-lookup"><span data-stu-id="e924d-249">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="e924d-250">d.</span><span class="sxs-lookup"><span data-stu-id="e924d-250">d.</span></span> <span data-ttu-id="e924d-251">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="e924d-251">Click **Create**.</span></span>
 
### <a name="creating-a-kantega-sso-for-jira-test-user"></a><span data-ttu-id="e924d-252">Tworzenie Kantega Usługa rejestracji Jednokrotnej dla użytkownika testowego JIRA</span><span class="sxs-lookup"><span data-stu-id="e924d-252">Creating a Kantega SSO for JIRA test user</span></span>

<span data-ttu-id="e924d-253">toolog użytkowników tooenable usługi Azure AD w tooJIRA, muszą mieć przydzielone do JIRA.</span><span class="sxs-lookup"><span data-stu-id="e924d-253">tooenable Azure AD users toolog in tooJIRA, they must be provisioned into JIRA.</span></span> <span data-ttu-id="e924d-254">W Kantega logowania jednokrotnego dla JIRA Inicjowanie obsługi to zadanie ręczne.</span><span class="sxs-lookup"><span data-stu-id="e924d-254">In Kantega SSO for JIRA, provisioning is a manual task.</span></span>

<span data-ttu-id="e924d-255">**tooprovision konta użytkownika, należy wykonać hello następujące kroki:**</span><span class="sxs-lookup"><span data-stu-id="e924d-255">**tooprovision a user account, perform hello following steps:**</span></span>

1. <span data-ttu-id="e924d-256">Zaloguj się za tooyour JIRA na lokalnym serwerze jako administrator.</span><span class="sxs-lookup"><span data-stu-id="e924d-256">Log in tooyour JIRA on premise server as an administrator.</span></span>

2. <span data-ttu-id="e924d-257">Umieść kursor na koło zębate, a następnie kliknij przycisk hello **Zarządzanie użytkownikami**.</span><span class="sxs-lookup"><span data-stu-id="e924d-257">Hover on cog and click hello **User management**.</span></span>

    ![Dodawanie pracownika](./media/active-directory-saas-kantegassoforjira-tutorial/user1.png) 

3. <span data-ttu-id="e924d-259">W obszarze **Zarządzanie użytkownikami** sekcji, kliknij pozycję **tworzenia użytkownika**.</span><span class="sxs-lookup"><span data-stu-id="e924d-259">Under **User management** tab section, click **Create user**.</span></span>

    ![Dodawanie pracownika](./media/active-directory-saas-kantegassoforjira-tutorial/user2.png) 

4. <span data-ttu-id="e924d-261">Na powitania **"Tworzenie nowego użytkownika"** okna dialogowego wykonaj hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="e924d-261">On hello **“Create new user”** dialog page, perform hello following steps:</span></span>

    ![Dodawanie pracownika](./media/active-directory-saas-kantegassoforjira-tutorial/user3.png) 

    <span data-ttu-id="e924d-263">a.</span><span class="sxs-lookup"><span data-stu-id="e924d-263">a.</span></span> <span data-ttu-id="e924d-264">W hello **adres E-mail** pole tekstowe, typ hello adres e-mail użytkownika, takich jak Brittasimon@contoso.com.</span><span class="sxs-lookup"><span data-stu-id="e924d-264">In hello **Email address** textbox, type hello email address of user like Brittasimon@contoso.com.</span></span>

    <span data-ttu-id="e924d-265">b.</span><span class="sxs-lookup"><span data-stu-id="e924d-265">b.</span></span> <span data-ttu-id="e924d-266">W hello **imię i nazwisko** tekstowym, wpisz pełną nazwę użytkownika hello jak Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="e924d-266">In hello **Full Name** textbox, type full name of hello user like Britta Simon.</span></span>

    <span data-ttu-id="e924d-267">c.</span><span class="sxs-lookup"><span data-stu-id="e924d-267">c.</span></span> <span data-ttu-id="e924d-268">W hello **Username** pole tekstowe, powitalne wiadomości e-mail użytkownika, takich jak Brittasimon@contoso.com.</span><span class="sxs-lookup"><span data-stu-id="e924d-268">In hello **Username** textbox, type hello email of user like Brittasimon@contoso.com.</span></span>

    <span data-ttu-id="e924d-269">d.</span><span class="sxs-lookup"><span data-stu-id="e924d-269">d.</span></span> <span data-ttu-id="e924d-270">W hello **hasło** tekstowym, wpisz hello hasło użytkownika.</span><span class="sxs-lookup"><span data-stu-id="e924d-270">In hello **Password** textbox, type hello password of user.</span></span>

    <span data-ttu-id="e924d-271">e.</span><span class="sxs-lookup"><span data-stu-id="e924d-271">e.</span></span> <span data-ttu-id="e924d-272">Kliknij przycisk **tworzenia użytkownika**.</span><span class="sxs-lookup"><span data-stu-id="e924d-272">Click **Create user**.</span></span>   

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="e924d-273">Przypisanie użytkownika testowego hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="e924d-273">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="e924d-274">W tej sekcji możesz włączyć toouse Simona Britta Azure logowania jednokrotnego za udzielanie dostępu tooKantega logowania jednokrotnego dla JIRA.</span><span class="sxs-lookup"><span data-stu-id="e924d-274">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooKantega SSO for JIRA.</span></span>

![Przypisz użytkownika][200] 

<span data-ttu-id="e924d-276">**tooassign tooKantega Simona Britta logowania jednokrotnego dla JIRA, wykonaj hello następujące kroki:**</span><span class="sxs-lookup"><span data-stu-id="e924d-276">**tooassign Britta Simon tooKantega SSO for JIRA, perform hello following steps:**</span></span>

1. <span data-ttu-id="e924d-277">W portalu Azure hello, otwórz widok aplikacji hello, a następnie przejdź do widoku katalogu toohello i przejść za**aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="e924d-277">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Przypisz użytkownika][201] 

2. <span data-ttu-id="e924d-279">Z listy aplikacji hello wybierz **Kantega Usługa rejestracji Jednokrotnej dla JIRA**.</span><span class="sxs-lookup"><span data-stu-id="e924d-279">In hello applications list, select **Kantega SSO for JIRA**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-kantegassoforjira-tutorial/tutorial_kantegassoforjira_app.png) 

3. <span data-ttu-id="e924d-281">W menu powitania po lewej stronie powitania kliknij **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="e924d-281">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Przypisz użytkownika][202] 

4. <span data-ttu-id="e924d-283">Kliknij przycisk **Dodaj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="e924d-283">Click **Add** button.</span></span> <span data-ttu-id="e924d-284">Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="e924d-284">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Przypisz użytkownika][203]

5. <span data-ttu-id="e924d-286">Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** hello listy użytkowników.</span><span class="sxs-lookup"><span data-stu-id="e924d-286">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="e924d-287">Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="e924d-287">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="e924d-288">Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="e924d-288">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="e924d-289">Testowanie rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="e924d-289">Testing single sign-on</span></span>

<span data-ttu-id="e924d-290">W tej sekcji można przetestować konfiguracji usługi Azure AD pojedynczego logowania jednokrotnego przy użyciu hello panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="e924d-290">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="e924d-291">Po kliknięciu hello Kantega logowania jednokrotnego dla JIRA kafelka w hello Panel dostępu, należy pobrać automatycznie zalogowane tooyour Kantega logowania jednokrotnego dla aplikacji JIRA.</span><span class="sxs-lookup"><span data-stu-id="e924d-291">When you click hello Kantega SSO for JIRA tile in hello Access Panel, you should get automatically signed-on tooyour Kantega SSO for JIRA application.</span></span>
<span data-ttu-id="e924d-292">Aby uzyskać więcej informacji na temat panelu dostępu, zobacz [toohello wprowadzenie panelu dostępu](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="e924d-292">For more information about the Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="e924d-293">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="e924d-293">Additional resources</span></span>

* [<span data-ttu-id="e924d-294">Lista samouczków dotyczących tooIntegrate aplikacji SaaS w usłudze Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="e924d-294">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="e924d-295">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="e924d-295">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-kantegassoforjira-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-kantegassoforjira-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-kantegassoforjira-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-kantegassoforjira-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-kantegassoforjira-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-kantegassoforjira-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-kantegassoforjira-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-kantegassoforjira-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-kantegassoforjira-tutorial/tutorial_general_203.png

