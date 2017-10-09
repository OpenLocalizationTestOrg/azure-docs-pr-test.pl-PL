---
title: 'Samouczek: Azure Active Directory integracji z logowaniem Jednokrotnym Kantega dla Bitbucket | Dokumentacja firmy Microsoft'
description: "Dowiedz się, jak tooconfigure logowanie jednokrotne między usługą Azure Active Directory i logowania jednokrotnego Kantega dla Bitbucket."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: c41cdaaf-0441-493c-94c7-569615b7b1ab
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: jeedes
ms.openlocfilehash: e86a9a9a42f2f80fe83191f113f6bab46cc8a37d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-kantega-sso-for-bitbucket"></a><span data-ttu-id="2cc60-103">Samouczek: Azure Active Directory integracji z logowaniem Jednokrotnym Kantega dla Bitbucket</span><span class="sxs-lookup"><span data-stu-id="2cc60-103">Tutorial: Azure Active Directory integration with Kantega SSO for Bitbucket</span></span>

<span data-ttu-id="2cc60-104">Z tego samouczka, dowiesz się, jak toointegrate logowania jednokrotnego Kantega dla Bitbucket w usłudze Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="2cc60-104">In this tutorial, you learn how toointegrate Kantega SSO for Bitbucket with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="2cc60-105">Integracja z usługą Azure AD logowania jednokrotnego Kantega dla Bitbucket zapewnia hello następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="2cc60-105">Integrating Kantega SSO for Bitbucket with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="2cc60-106">Można kontrolować w usłudze Azure AD, kto ma dostęp tooKantega logowania jednokrotnego dla Bitbucket</span><span class="sxs-lookup"><span data-stu-id="2cc60-106">You can control in Azure AD who has access tooKantega SSO for Bitbucket</span></span>
- <span data-ttu-id="2cc60-107">Można włączyć użytkownika użytkownicy tooautomatically get zalogowane tooKantega logowania jednokrotnego dla Bitbucket (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="2cc60-107">You can enable your users tooautomatically get signed-on tooKantega SSO for Bitbucket (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="2cc60-108">Możesz zarządzać kont w jednej centralnej lokalizacji - hello portalu Azure</span><span class="sxs-lookup"><span data-stu-id="2cc60-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="2cc60-109">Jeśli chcesz tooknow więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="2cc60-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="2cc60-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="2cc60-110">Prerequisites</span></span>

<span data-ttu-id="2cc60-111">tooconfigure integracji usługi Azure AD z logowania jednokrotnego Kantega dla Bitbucket należy hello następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="2cc60-111">tooconfigure Azure AD integration with Kantega SSO for Bitbucket, you need hello following items:</span></span>

- <span data-ttu-id="2cc60-112">Subskrypcję usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="2cc60-112">An Azure AD subscription</span></span>
- <span data-ttu-id="2cc60-113">Kantega Usługa rejestracji Jednokrotnej dla Bitbucket logowanie jednokrotne włączone subskrypcji</span><span class="sxs-lookup"><span data-stu-id="2cc60-113">A Kantega SSO for Bitbucket single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="2cc60-114">tootest hello kroków w tym samouczku, zaleca się przy użyciu środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="2cc60-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="2cc60-115">tootest hello kroki opisane w tym samouczku, należy stosować te zalecenia:</span><span class="sxs-lookup"><span data-stu-id="2cc60-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="2cc60-116">Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="2cc60-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="2cc60-117">Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz pobrać miesięczna wersja próbna [tutaj](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="2cc60-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="2cc60-118">Opis scenariusza</span><span class="sxs-lookup"><span data-stu-id="2cc60-118">Scenario description</span></span>
<span data-ttu-id="2cc60-119">W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym.</span><span class="sxs-lookup"><span data-stu-id="2cc60-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="2cc60-120">Scenariusz Hello opisane w tym samouczku składa się z dwóch głównych elementów:</span><span class="sxs-lookup"><span data-stu-id="2cc60-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="2cc60-121">Dodawanie logowania jednokrotnego Kantega dla Bitbucket z galerii hello</span><span class="sxs-lookup"><span data-stu-id="2cc60-121">Adding Kantega SSO for Bitbucket from hello gallery</span></span>
2. <span data-ttu-id="2cc60-122">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="2cc60-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-kantega-sso-for-bitbucket-from-hello-gallery"></a><span data-ttu-id="2cc60-123">Dodawanie logowania jednokrotnego Kantega dla Bitbucket z galerii hello</span><span class="sxs-lookup"><span data-stu-id="2cc60-123">Adding Kantega SSO for Bitbucket from hello gallery</span></span>
<span data-ttu-id="2cc60-124">tooconfigure hello włączenia logowania jednokrotnego Kantega dla Bitbucket do usługi Azure AD, należy tooadd Kantega logowania jednokrotnego dla Bitbucket z hello galerii tooyour listę zarządzanych aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="2cc60-124">tooconfigure hello integration of Kantega SSO for Bitbucket into Azure AD, you need tooadd Kantega SSO for Bitbucket from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="2cc60-125">**tooadd Kantega Usługa rejestracji Jednokrotnej dla Bitbucket z galerii hello wykonaj hello następujące kroki:**</span><span class="sxs-lookup"><span data-stu-id="2cc60-125">**tooadd Kantega SSO for Bitbucket from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="2cc60-126">W hello  **[portalu Azure](https://portal.azure.com)**na temat hello panelu nawigacji po lewej stronie, kliknij przycisk **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="2cc60-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Usługa Active Directory][1]

2. <span data-ttu-id="2cc60-128">Przejdź za**aplikacje dla przedsiębiorstw**.</span><span class="sxs-lookup"><span data-stu-id="2cc60-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="2cc60-129">Następnie przejdź zbyt**wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="2cc60-129">Then go too**All applications**.</span></span>

    ![Aplikacje][2]
    
3. <span data-ttu-id="2cc60-131">tooadd nową aplikację, kliknij przycisk **nowej aplikacji** przycisk u góry hello okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="2cc60-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplikacje][3]

4. <span data-ttu-id="2cc60-133">W polu wyszukiwania hello wpisz **Kantega Usługa rejestracji Jednokrotnej dla Bitbucket**.</span><span class="sxs-lookup"><span data-stu-id="2cc60-133">In hello search box, type **Kantega SSO for Bitbucket**.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-kantegassoforbitbucket-tutorial/tutorial_kantegassoforbitbucket_search.png)

5. <span data-ttu-id="2cc60-135">W panelu wyników hello, wybierz **Kantega Usługa rejestracji Jednokrotnej dla Bitbucket**, a następnie kliknij przycisk **Dodaj** przycisk aplikacji hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="2cc60-135">In hello results panel, select **Kantega SSO for Bitbucket**, and then click **Add** button tooadd hello application.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-kantegassoforbitbucket-tutorial/tutorial_kantegassoforbitbucket_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="2cc60-137">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="2cc60-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="2cc60-138">W tej sekcji skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z logowania jednokrotnego Kantega dla Bitbucket w oparciu o nazwie "Britta Simona" użytkownika testowego.</span><span class="sxs-lookup"><span data-stu-id="2cc60-138">In this section, you configure and test Azure AD single sign-on with Kantega SSO for Bitbucket based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="2cc60-139">Dla pojedynczego logowania jednokrotnego toowork usługi Azure AD musi tooknow użytkownika odpowiednikiem hello w rejestracji Jednokrotnej Kantega dla Bitbucket jest tooa użytkownika w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="2cc60-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Kantega SSO for Bitbucket is tooa user in Azure AD.</span></span> <span data-ttu-id="2cc60-140">Innymi słowy relację łącza między użytkownika usługi Azure AD i hello użytkownikowi w rejestracji Jednokrotnej Kantega dla Bitbucket musi toobe ustanowione.</span><span class="sxs-lookup"><span data-stu-id="2cc60-140">In other words, a link relationship between an Azure AD user and hello related user in Kantega SSO for Bitbucket needs toobe established.</span></span>

<span data-ttu-id="2cc60-141">W Kantega logowania jednokrotnego dla Bitbucket, należy przypisać wartość hello hello **nazwy użytkownika** w usłudze Azure AD jako wartość hello hello **Username** tooestablish hello łącze relacji.</span><span class="sxs-lookup"><span data-stu-id="2cc60-141">In Kantega SSO for Bitbucket, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="2cc60-142">tooconfigure i testowanie usługi Azure AD rejestracji jednokrotnej z logowania jednokrotnego Kantega Bitbucket, należy po bloków konstrukcyjnych hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="2cc60-142">tooconfigure and test Azure AD single sign-on with Kantega SSO for Bitbucket, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="2cc60-143">**[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configuring-azure-ad-single-sign-on)**  -tooenable Twojego toouse użytkowników tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="2cc60-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="2cc60-144">**[Tworzenie użytkownika testowego usługi Azure AD](#creating-an-azure-ad-test-user)**  -tootest usługi Azure AD rejestracji jednokrotnej z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="2cc60-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="2cc60-145">**[Tworzenie Kantega Usługa rejestracji Jednokrotnej dla użytkownika testowego Bitbucket](#creating-a-kantega-sso-for-bitbucket-test-user)**  -toohave odpowiednikiem Simona Britta w rejestracji Jednokrotnej Kantega dla Bitbucket, który jest połączony toohello usługi Azure AD reprezentację użytkownika.</span><span class="sxs-lookup"><span data-stu-id="2cc60-145">**[Creating a Kantega SSO for Bitbucket test user](#creating-a-kantega-sso-for-bitbucket-test-user)** - toohave a counterpart of Britta Simon in Kantega SSO for Bitbucket that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="2cc60-146">**[Przypisanie użytkownika testowego hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Simona Britta toouse usługi Azure AD rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="2cc60-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="2cc60-147">**[Testowanie rejestracji jednokrotnej](#testing-single-sign-on)**  -tooverify czy hello konfiguracji działania.</span><span class="sxs-lookup"><span data-stu-id="2cc60-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="2cc60-148">Konfigurowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="2cc60-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="2cc60-149">W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w portalu Azure hello i skonfigurować logowanie jednokrotne w Twojej rejestracji Jednokrotnej Kantega Bitbucket aplikacji.</span><span class="sxs-lookup"><span data-stu-id="2cc60-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Kantega SSO for Bitbucket application.</span></span>

<span data-ttu-id="2cc60-150">**tooconfigure usługi Azure AD rejestracji jednokrotnej z logowania jednokrotnego Kantega dla Bitbucket, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="2cc60-150">**tooconfigure Azure AD single sign-on with Kantega SSO for Bitbucket, perform hello following steps:**</span></span>

1. <span data-ttu-id="2cc60-151">W portalu Azure na powitania hello **Kantega Usługa rejestracji Jednokrotnej dla Bitbucket** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.</span><span class="sxs-lookup"><span data-stu-id="2cc60-151">In hello Azure portal, on hello **Kantega SSO for Bitbucket** application integration page, click **Single sign-on**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej][4]

2. <span data-ttu-id="2cc60-153">Na powitania **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** tooenable rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="2cc60-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-kantegassoforbitbucket-tutorial/tutorial_kantegassoforbitbucket_samlbase.png)

3. <span data-ttu-id="2cc60-155">W **IDP** inicjowane tryb na powitania **logowania jednokrotnego Kantega Bitbucket domeny i adresów URL** sekcji wykonać powitania po kroku:</span><span class="sxs-lookup"><span data-stu-id="2cc60-155">In **IDP** initiated mode, on hello **Kantega SSO for Bitbucket Domain and URLs** section perform hello following step:</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-kantegassoforbitbucket-tutorial/tutorial_kantegassoforbitbucket_url1.png)

    <span data-ttu-id="2cc60-157">a.</span><span class="sxs-lookup"><span data-stu-id="2cc60-157">a.</span></span> <span data-ttu-id="2cc60-158">W hello **identyfikator** tekstowym, wpisz adres URL za pomocą hello następującego wzorca:`https://<server-base-url>/plugins/servlet/no.kantega.saml/sp/<uniqueid>/login`</span><span class="sxs-lookup"><span data-stu-id="2cc60-158">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<server-base-url>/plugins/servlet/no.kantega.saml/sp/<uniqueid>/login`</span></span>

    <span data-ttu-id="2cc60-159">b.</span><span class="sxs-lookup"><span data-stu-id="2cc60-159">b.</span></span> <span data-ttu-id="2cc60-160">W hello **adres URL odpowiedzi** tekstowym, wpisz adres URL za pomocą hello następującego wzorca:`https://<server-base-url>/plugins/servlet/no.kantega.saml/sp/<uniqueid>/login`</span><span class="sxs-lookup"><span data-stu-id="2cc60-160">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://<server-base-url>/plugins/servlet/no.kantega.saml/sp/<uniqueid>/login`</span></span>

4. <span data-ttu-id="2cc60-161">W **SP** inicjowane trybie wyboru **Pokaż zaawansowane ustawienia adresu URL** i wykonywać powitania po kroku:</span><span class="sxs-lookup"><span data-stu-id="2cc60-161">In **SP** initiated mode, check **Show advanced URL settings** and  perform hello following step:</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-kantegassoforbitbucket-tutorial/tutorial_kantegassoforbitbucket_url2.png)
    
    <span data-ttu-id="2cc60-163">W hello **adres URL logowania** tekstowym, wpisz adres URL za pomocą hello następującego wzorca:`https://<server-base-url>/plugins/servlet/no.kantega.saml/sp/<uniqueid>/login`</span><span class="sxs-lookup"><span data-stu-id="2cc60-163">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<server-base-url>/plugins/servlet/no.kantega.saml/sp/<uniqueid>/login`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="2cc60-164">Wartości te nie są prawdziwe.</span><span class="sxs-lookup"><span data-stu-id="2cc60-164">These values are not real.</span></span> <span data-ttu-id="2cc60-165">Zaktualizować te wartości z hello rzeczywisty identyfikator, adres URL odpowiedzi i adres URL logowania.</span><span class="sxs-lookup"><span data-stu-id="2cc60-165">Update these values with hello actual Identifier, Reply URL, and Sign-On URL.</span></span> <span data-ttu-id="2cc60-166">Te wartości są odbierane podczas konfigurowania hello wtyczki Bitbucket, który znajduje się w dalszej części samouczka hello.</span><span class="sxs-lookup"><span data-stu-id="2cc60-166">These values are recieved during hello configuration of Bitbucket plugin which is explained later in hello tutorial.</span></span>

5. <span data-ttu-id="2cc60-167">Na powitania **certyfikat podpisywania SAML** kliknij **XML metadanych** , a następnie zapisz plik metadanych hello na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="2cc60-167">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-kantegassoforbitbucket-tutorial/tutorial_kantegassoforbitbucket_certificate.png) 

6. <span data-ttu-id="2cc60-169">Kliknij przycisk **zapisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="2cc60-169">Click **Save** button.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-kantegassoforbitbucket-tutorial/tutorial_general_400.png)

7. <span data-ttu-id="2cc60-171">W oknie przeglądarki innej witryny sieci web Zaloguj się w portalu administracyjnym Bitbucket tooyour jako administrator.</span><span class="sxs-lookup"><span data-stu-id="2cc60-171">In a different web browser window, log in tooyour Bitbucket admin portal as an administrator.</span></span>

8. <span data-ttu-id="2cc60-172">Kliknij koło zębate, a następnie kliknij przycisk hello **znaleźć nowe dodatki**.</span><span class="sxs-lookup"><span data-stu-id="2cc60-172">Click cog and click hello **Find new add-ons**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-kantegassoforbitbucket-tutorial/addon1.png)

9. <span data-ttu-id="2cc60-174">Wyszukiwanie **logowania jednokrotnego Kantega Bitbucket SAML i protokołu Kerberos** i kliknij przycisk **zainstalować** tooinstall przycisk hello nowej wtyczki SAML.</span><span class="sxs-lookup"><span data-stu-id="2cc60-174">Search **Kantega SSO for Bitbucket SAML & Kerberos** and click **Install** button tooinstall hello new SAML plugin.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-kantegassoforbitbucket-tutorial/addon2.png)

10. <span data-ttu-id="2cc60-176">rozpoczyna się instalacja dodatku Hello.</span><span class="sxs-lookup"><span data-stu-id="2cc60-176">hello plugin installation starts.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-kantegassoforbitbucket-tutorial/addon31.png)

11. <span data-ttu-id="2cc60-178">Po zakończeniu instalacji hello.</span><span class="sxs-lookup"><span data-stu-id="2cc60-178">Once hello installation is complete.</span></span> <span data-ttu-id="2cc60-179">Kliknij przycisk **Zamknij**.</span><span class="sxs-lookup"><span data-stu-id="2cc60-179">Click **Close**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-kantegassoforbitbucket-tutorial/addon33.png)

12. <span data-ttu-id="2cc60-181">Kliknij pozycję **Zarządzaj**.</span><span class="sxs-lookup"><span data-stu-id="2cc60-181">Click **Manage**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-kantegassoforbitbucket-tutorial/addon34.png)
    
13. <span data-ttu-id="2cc60-183">Kliknij przycisk **Konfiguruj** tooconfigure hello nowej wtyczki.</span><span class="sxs-lookup"><span data-stu-id="2cc60-183">Click **Configure** tooconfigure hello new plugin.</span></span>  

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-kantegassoforbitbucket-tutorial/addon35.png)

14. <span data-ttu-id="2cc60-185">W hello **SAML** sekcji.</span><span class="sxs-lookup"><span data-stu-id="2cc60-185">In hello **SAML** section.</span></span> <span data-ttu-id="2cc60-186">Wybierz **usługi Azure Active Directory (Azure AD)** z hello **dostawcy tożsamości Dodaj** listy rozwijanej.</span><span class="sxs-lookup"><span data-stu-id="2cc60-186">Select **Azure Active Directory (Azure AD)** from hello **Add identity provider** dropdown.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-kantegassoforbitbucket-tutorial/addon4.png)

15. <span data-ttu-id="2cc60-188">Wybierz poziom subskrypcji jako **podstawowe**.</span><span class="sxs-lookup"><span data-stu-id="2cc60-188">Select subscription level as **Basic**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-kantegassoforbitbucket-tutorial/addon5.png)

16. <span data-ttu-id="2cc60-190">Na powitania **właściwości aplikacji** sekcji, wykonaj następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="2cc60-190">On hello **App properties** section, perform following steps:</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-kantegassoforbitbucket-tutorial/addon6.png)

    <span data-ttu-id="2cc60-192">a.</span><span class="sxs-lookup"><span data-stu-id="2cc60-192">a.</span></span> <span data-ttu-id="2cc60-193">Kopiuj hello **identyfikator URI aplikacji** wartości i używać go jako **identyfikator, adres URL odpowiedzi i adres URL logowania** na powitania **logowania jednokrotnego Kantega Bitbucket domeny i adresów URL** sekcji w portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="2cc60-193">Copy hello **App ID URI** value and use it as **Identifier, Reply URL, and Sign-On URL** on hello **Kantega SSO for Bitbucket Domain and URLs** section in Azure portal.</span></span>

    <span data-ttu-id="2cc60-194">b.</span><span class="sxs-lookup"><span data-stu-id="2cc60-194">b.</span></span> <span data-ttu-id="2cc60-195">Kliknij przycisk **Dalej**.</span><span class="sxs-lookup"><span data-stu-id="2cc60-195">Click **Next**.</span></span>

17. <span data-ttu-id="2cc60-196">Na powitania **importu metadanych** sekcji, wykonaj następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="2cc60-196">On hello **Metadata import** section, perform following steps:</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-kantegassoforbitbucket-tutorial/addon7.png)

    <span data-ttu-id="2cc60-198">a.</span><span class="sxs-lookup"><span data-stu-id="2cc60-198">a.</span></span> <span data-ttu-id="2cc60-199">Wybierz **pliku metadanych na tym komputerze**i przekazywanie pliku metadanych, który został pobrany z portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="2cc60-199">Select **Metadata file on my computer**, and upload metadata file, which you have downloaded from Azure portal.</span></span>

    <span data-ttu-id="2cc60-200">b.</span><span class="sxs-lookup"><span data-stu-id="2cc60-200">b.</span></span> <span data-ttu-id="2cc60-201">Kliknij przycisk **Dalej**.</span><span class="sxs-lookup"><span data-stu-id="2cc60-201">Click **Next**.</span></span>

18. <span data-ttu-id="2cc60-202">Na powitania **nazwę i logowania jednokrotnego lokalizację** sekcji, wykonaj następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="2cc60-202">On hello **Name and SSO location** section, perform following steps:</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-kantegassoforbitbucket-tutorial/addon8.png)

    <span data-ttu-id="2cc60-204">a.</span><span class="sxs-lookup"><span data-stu-id="2cc60-204">a.</span></span> <span data-ttu-id="2cc60-205">Dodaj nazwę hello dostawcy tożsamości w **Nazwa dostawcy tożsamości** pola tekstowego (np. usługi Azure AD).</span><span class="sxs-lookup"><span data-stu-id="2cc60-205">Add Name of hello Identity Provider in **Identity provider name** textbox (e.g Azure AD).</span></span>

    <span data-ttu-id="2cc60-206">b.</span><span class="sxs-lookup"><span data-stu-id="2cc60-206">b.</span></span> <span data-ttu-id="2cc60-207">Kliknij przycisk **Dalej**.</span><span class="sxs-lookup"><span data-stu-id="2cc60-207">Click **Next**.</span></span>

19. <span data-ttu-id="2cc60-208">Sprawdź hello certyfikatu podpisywania, a następnie kliknij przycisk **dalej**.</span><span class="sxs-lookup"><span data-stu-id="2cc60-208">Verify hello Signing certificate and click **Next**.</span></span>    

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-kantegassoforbitbucket-tutorial/addon9.png)

20. <span data-ttu-id="2cc60-210">Na powitania **kont użytkowników Bitbucket** sekcji, wykonaj następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="2cc60-210">On hello **Bitbucket user accounts** section, perform following steps:</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-kantegassoforbitbucket-tutorial/addon10.png)

    <span data-ttu-id="2cc60-212">a.</span><span class="sxs-lookup"><span data-stu-id="2cc60-212">a.</span></span> <span data-ttu-id="2cc60-213">Wybierz **tworzenie użytkowników w katalogu wewnętrznego w Bitbucket, w razie potrzeby** , a następnie wprowadź odpowiednią nazwę hello hello grupy użytkowników (może być wiele nie.</span><span class="sxs-lookup"><span data-stu-id="2cc60-213">Select **Create users in Bitbucket's internal Directory if needed** and enter hello appropriate name of hello group for users (can be multiple no.</span></span> <span data-ttu-id="2cc60-214">grup rozdzielone przecinkami).</span><span class="sxs-lookup"><span data-stu-id="2cc60-214">of groups separated by comma).</span></span>

    <span data-ttu-id="2cc60-215">b.</span><span class="sxs-lookup"><span data-stu-id="2cc60-215">b.</span></span> <span data-ttu-id="2cc60-216">Kliknij przycisk **Dalej**.</span><span class="sxs-lookup"><span data-stu-id="2cc60-216">Click **Next**.</span></span>

21. <span data-ttu-id="2cc60-217">Kliknij przycisk **Zakończ**.</span><span class="sxs-lookup"><span data-stu-id="2cc60-217">Click **Finish**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-kantegassoforbitbucket-tutorial/addon11.png)

22. <span data-ttu-id="2cc60-219">Na powitania **znanych domeny dla usługi Azure AD** sekcji, wykonaj następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="2cc60-219">On hello **Known domains for Azure AD** section, perform following steps:</span></span>   

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-kantegassoforbitbucket-tutorial/addon12.png)

    <span data-ttu-id="2cc60-221">a.</span><span class="sxs-lookup"><span data-stu-id="2cc60-221">a.</span></span> <span data-ttu-id="2cc60-222">Wybierz **znane domen** z lewego panelu hello hello strony.</span><span class="sxs-lookup"><span data-stu-id="2cc60-222">Select **Known domains** from hello left panel of hello page.</span></span>

    <span data-ttu-id="2cc60-223">b.</span><span class="sxs-lookup"><span data-stu-id="2cc60-223">b.</span></span> <span data-ttu-id="2cc60-224">Wprowadź nazwę domeny w hello **znane domen** pola tekstowego.</span><span class="sxs-lookup"><span data-stu-id="2cc60-224">Enter domain name in hello **Known domains** textbox.</span></span>

    <span data-ttu-id="2cc60-225">c.</span><span class="sxs-lookup"><span data-stu-id="2cc60-225">c.</span></span> <span data-ttu-id="2cc60-226">Kliknij pozycję **Zapisz**.</span><span class="sxs-lookup"><span data-stu-id="2cc60-226">Click **Save**.</span></span>  

> [!TIP]
> <span data-ttu-id="2cc60-227">Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz hello [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji hello!</span><span class="sxs-lookup"><span data-stu-id="2cc60-227">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="2cc60-228">Po dodaniu tej aplikacji z hello **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij hello **rejestracji jednokrotnej** hello kartę i dostępu do osadzonych dokumentacji za pośrednictwem hello  **Konfiguracja** sekcji u dołu hello.</span><span class="sxs-lookup"><span data-stu-id="2cc60-228">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="2cc60-229">Więcej o hello osadzonych dokumentacji funkcji w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="2cc60-229">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="2cc60-230">Tworzenie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="2cc60-230">Creating an Azure AD test user</span></span>
<span data-ttu-id="2cc60-231">Celem Hello w tej sekcji jest toocreate użytkownika testowego, w portalu Azure o nazwie Simona Britta hello.</span><span class="sxs-lookup"><span data-stu-id="2cc60-231">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Tworzenie użytkowników usługi Azure AD][100]

<span data-ttu-id="2cc60-233">**toocreate użytkownika testowego w usłudze Azure AD, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="2cc60-233">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="2cc60-234">W hello **portalu Azure**na temat hello w lewym okienku nawigacji, kliknij przycisk **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="2cc60-234">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-kantegassoforbitbucket-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="2cc60-236">toodisplay hello listę użytkowników, przejdź zbyt**użytkowników i grup** i kliknij przycisk **wszyscy użytkownicy**.</span><span class="sxs-lookup"><span data-stu-id="2cc60-236">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-kantegassoforbitbucket-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="2cc60-238">Witaj tooopen **użytkownika** okna dialogowego, kliknij przycisk **Dodaj** u góry hello hello okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="2cc60-238">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-kantegassoforbitbucket-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="2cc60-240">Na powitania **użytkownika** okna dialogowego wykonaj hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="2cc60-240">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-kantegassoforbitbucket-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="2cc60-242">a.</span><span class="sxs-lookup"><span data-stu-id="2cc60-242">a.</span></span> <span data-ttu-id="2cc60-243">W hello **nazwa** pole tekstowe, typ **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="2cc60-243">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="2cc60-244">b.</span><span class="sxs-lookup"><span data-stu-id="2cc60-244">b.</span></span> <span data-ttu-id="2cc60-245">W hello **nazwy użytkownika** pole tekstowe, hello typu **adres e-mail** z BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="2cc60-245">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="2cc60-246">c.</span><span class="sxs-lookup"><span data-stu-id="2cc60-246">c.</span></span> <span data-ttu-id="2cc60-247">Wybierz **Pokaż hasło** i zanotuj wartość hello hello **hasło**.</span><span class="sxs-lookup"><span data-stu-id="2cc60-247">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="2cc60-248">d.</span><span class="sxs-lookup"><span data-stu-id="2cc60-248">d.</span></span> <span data-ttu-id="2cc60-249">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="2cc60-249">Click **Create**.</span></span>
 
### <a name="creating-a-kantega-sso-for-bitbucket-test-user"></a><span data-ttu-id="2cc60-250">Tworzenie Kantega Usługa rejestracji Jednokrotnej dla użytkownika testowego Bitbucket</span><span class="sxs-lookup"><span data-stu-id="2cc60-250">Creating a Kantega SSO for Bitbucket test user</span></span>

<span data-ttu-id="2cc60-251">toolog użytkowników tooenable usługi Azure AD w tooBitbucket, muszą mieć przydzielone do Bitbucket.</span><span class="sxs-lookup"><span data-stu-id="2cc60-251">tooenable Azure AD users toolog in tooBitbucket, they must be provisioned into Bitbucket.</span></span> <span data-ttu-id="2cc60-252">W Kantega logowania jednokrotnego dla Bitbucket Inicjowanie obsługi to zadanie ręczne.</span><span class="sxs-lookup"><span data-stu-id="2cc60-252">In Kantega SSO for Bitbucket, provisioning is a manual task.</span></span>

<span data-ttu-id="2cc60-253">**tooprovision konta użytkownika, należy wykonać hello następujące kroki:**</span><span class="sxs-lookup"><span data-stu-id="2cc60-253">**tooprovision a user account, perform hello following steps:**</span></span>

1. <span data-ttu-id="2cc60-254">Zaloguj się za tooyour Bitbucket witryny firmy jako administrator.</span><span class="sxs-lookup"><span data-stu-id="2cc60-254">Log in tooyour Bitbucket company site as an administrator.</span></span>

2. <span data-ttu-id="2cc60-255">Kliknij ikonę ustawień.</span><span class="sxs-lookup"><span data-stu-id="2cc60-255">Click on settings icon.</span></span>

    ![Dodawanie pracownika](./media/active-directory-saas-kantegassoforbitbucket-tutorial/user1.png) 

3. <span data-ttu-id="2cc60-257">W obszarze **administracji** sekcji, kliknij pozycję **użytkowników**.</span><span class="sxs-lookup"><span data-stu-id="2cc60-257">Under **Administration** tab section, click **Users**.</span></span>

    ![Dodawanie pracownika](./media/active-directory-saas-kantegassoforbitbucket-tutorial/user2.png)

4. <span data-ttu-id="2cc60-259">Kliknij przycisk **tworzenia użytkownika**.</span><span class="sxs-lookup"><span data-stu-id="2cc60-259">Click **Create user**.</span></span>

    ![Dodawanie pracownika](./media/active-directory-saas-kantegassoforbitbucket-tutorial/user3.png)     

5. <span data-ttu-id="2cc60-261">Na powitania **Tworzenie użytkownika** okna dialogowego wykonaj hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="2cc60-261">On hello **Create User** dialog page, perform hello following steps:</span></span>

    ![Dodawanie pracownika](./media/active-directory-saas-kantegassoforbitbucket-tutorial/user4.png) 

    <span data-ttu-id="2cc60-263">a.</span><span class="sxs-lookup"><span data-stu-id="2cc60-263">a.</span></span> <span data-ttu-id="2cc60-264">W hello **Username** pole tekstowe, powitalne wiadomości e-mail użytkownika, takich jak Brittasimon@contoso.com.</span><span class="sxs-lookup"><span data-stu-id="2cc60-264">In hello **Username** textbox, type hello email of user like Brittasimon@contoso.com.</span></span>
    
    <span data-ttu-id="2cc60-265">b.</span><span class="sxs-lookup"><span data-stu-id="2cc60-265">b.</span></span> <span data-ttu-id="2cc60-266">W hello **imię i nazwisko** tekstowym, wpisz pełną nazwę użytkownika hello jak Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="2cc60-266">In hello **Full Name** textbox, type full name of hello user like Britta Simon.</span></span>
    
    <span data-ttu-id="2cc60-267">c.</span><span class="sxs-lookup"><span data-stu-id="2cc60-267">c.</span></span> <span data-ttu-id="2cc60-268">W hello **adres E-mail** pole tekstowe, typ hello adres e-mail użytkownika, takich jak Brittasimon@contoso.com.</span><span class="sxs-lookup"><span data-stu-id="2cc60-268">In hello **Email address** textbox, type hello email address of user like Brittasimon@contoso.com.</span></span>

    <span data-ttu-id="2cc60-269">d.</span><span class="sxs-lookup"><span data-stu-id="2cc60-269">d.</span></span> <span data-ttu-id="2cc60-270">W hello **hasło** tekstowym, wpisz hello hasło użytkownika.</span><span class="sxs-lookup"><span data-stu-id="2cc60-270">In hello **Password** textbox, type hello password of user.</span></span>  

    <span data-ttu-id="2cc60-271">e.</span><span class="sxs-lookup"><span data-stu-id="2cc60-271">e.</span></span> <span data-ttu-id="2cc60-272">W hello **Potwierdź hasło** pole tekstowe, hello ponownie wprowadź hasło użytkownika.</span><span class="sxs-lookup"><span data-stu-id="2cc60-272">In hello **Confirm Password** textbox, reenter hello password of user.</span></span>

    <span data-ttu-id="2cc60-273">f.</span><span class="sxs-lookup"><span data-stu-id="2cc60-273">f.</span></span> <span data-ttu-id="2cc60-274">Kliknij przycisk **tworzenia użytkownika**.</span><span class="sxs-lookup"><span data-stu-id="2cc60-274">Click **Create user**.</span></span>   

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="2cc60-275">Przypisanie użytkownika testowego hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="2cc60-275">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="2cc60-276">W tej sekcji możesz włączyć toouse Simona Britta Azure logowania jednokrotnego za udzielanie dostępu tooKantega logowania jednokrotnego dla Bitbucket.</span><span class="sxs-lookup"><span data-stu-id="2cc60-276">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooKantega SSO for Bitbucket.</span></span>

![Przypisz użytkownika][200] 

<span data-ttu-id="2cc60-278">**tooassign tooKantega Simona Britta logowania jednokrotnego dla Bitbucket, wykonaj hello następujące kroki:**</span><span class="sxs-lookup"><span data-stu-id="2cc60-278">**tooassign Britta Simon tooKantega SSO for Bitbucket, perform hello following steps:**</span></span>

1. <span data-ttu-id="2cc60-279">W portalu Azure hello, otwórz widok aplikacji hello, a następnie przejdź do widoku katalogu toohello i przejść za**aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="2cc60-279">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Przypisz użytkownika][201] 

2. <span data-ttu-id="2cc60-281">Z listy aplikacji hello wybierz **Kantega Usługa rejestracji Jednokrotnej dla Bitbucket**.</span><span class="sxs-lookup"><span data-stu-id="2cc60-281">In hello applications list, select **Kantega SSO for Bitbucket**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-kantegassoforbitbucket-tutorial/tutorial_kantegassoforbitbucket_app.png) 

3. <span data-ttu-id="2cc60-283">W menu powitania po lewej stronie powitania kliknij **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="2cc60-283">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Przypisz użytkownika][202] 

4. <span data-ttu-id="2cc60-285">Kliknij przycisk **Dodaj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="2cc60-285">Click **Add** button.</span></span> <span data-ttu-id="2cc60-286">Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="2cc60-286">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Przypisz użytkownika][203]

5. <span data-ttu-id="2cc60-288">Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** hello listy użytkowników.</span><span class="sxs-lookup"><span data-stu-id="2cc60-288">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="2cc60-289">Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="2cc60-289">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="2cc60-290">Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="2cc60-290">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="2cc60-291">Testowanie rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="2cc60-291">Testing single sign-on</span></span>

<span data-ttu-id="2cc60-292">W tej sekcji można przetestować konfiguracji usługi Azure AD pojedynczego logowania jednokrotnego przy użyciu hello panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="2cc60-292">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="2cc60-293">Po kliknięciu hello Kantega logowania jednokrotnego dla Bitbucket kafelka w hello Panel dostępu, należy pobrać automatycznie zalogowane tooyour Kantega logowania jednokrotnego dla aplikacji Bitbucket.</span><span class="sxs-lookup"><span data-stu-id="2cc60-293">When you click hello Kantega SSO for Bitbucket tile in hello Access Panel, you should get automatically signed-on tooyour Kantega SSO for Bitbucket application.</span></span>
<span data-ttu-id="2cc60-294">Aby uzyskać więcej informacji na temat panelu dostępu, zobacz [toohello wprowadzenie panelu dostępu](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="2cc60-294">For more information about the Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="2cc60-295">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="2cc60-295">Additional resources</span></span>

* [<span data-ttu-id="2cc60-296">Lista samouczków dotyczących tooIntegrate aplikacji SaaS w usłudze Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="2cc60-296">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="2cc60-297">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="2cc60-297">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-kantegassoforbitbucket-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-kantegassoforbitbucket-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-kantegassoforbitbucket-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-kantegassoforbitbucket-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-kantegassoforbitbucket-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-kantegassoforbitbucket-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-kantegassoforbitbucket-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-kantegassoforbitbucket-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-kantegassoforbitbucket-tutorial/tutorial_general_203.png

