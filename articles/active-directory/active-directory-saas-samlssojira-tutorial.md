---
title: 'Samouczek: Integracji Azure Active Directory z logowania jednokrotnego SAML dla Jira przez rozpoznawania GmbH | Dokumentacja firmy Microsoft'
description: "Dowiedz się, jak tooconfigure logowanie jednokrotne między usługą Azure Active Directory i logowania jednokrotnego SAML dla Jira przez rozpoznawania GmbH."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 20e18819-e330-4e40-bd8d-2ff3b98e035f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/18/2017
ms.author: jeedes
ms.openlocfilehash: a3436a9aa25640e931a61b5ba4a62611e6e07890
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-saml-sso-for-jira-by-resolution-gmbh"></a><span data-ttu-id="6319f-103">Samouczek: Integracji Azure Active Directory z logowania jednokrotnego SAML dla Jira przez rozpoznawania GmbH</span><span class="sxs-lookup"><span data-stu-id="6319f-103">Tutorial: Azure Active Directory integration with SAML SSO for Jira by resolution GmbH</span></span>

<span data-ttu-id="6319f-104">Z tego samouczka, dowiesz się, jak toointegrate logowania jednokrotnego SAML dla Jira przez rozpoznawania GmbH w usłudze Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="6319f-104">In this tutorial, you learn how toointegrate SAML SSO for Jira by resolution GmbH with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="6319f-105">Integrowanie logowania jednokrotnego SAML dla Jira przez rozpoznawania GmbH z usługą Azure AD zapewnia hello następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="6319f-105">Integrating SAML SSO for Jira by resolution GmbH with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="6319f-106">Można kontrolować w usłudze Azure AD mającego tooSAML dostępu logowania jednokrotnego dla Jira przez rozpoznawania GmbH</span><span class="sxs-lookup"><span data-stu-id="6319f-106">You can control in Azure AD who has access tooSAML SSO for Jira by resolution GmbH</span></span>
- <span data-ttu-id="6319f-107">Można włączyć użytkownika użytkownicy tooautomatically get zalogowane tooSAML logowania jednokrotnego dla Jira rozpoznawania GmbH (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="6319f-107">You can enable your users tooautomatically get signed-on tooSAML SSO for Jira by resolution GmbH (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="6319f-108">Możesz zarządzać kont w jednej centralnej lokalizacji - hello portalu Azure</span><span class="sxs-lookup"><span data-stu-id="6319f-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="6319f-109">Jeśli chcesz tooknow więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="6319f-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="6319f-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="6319f-110">Prerequisites</span></span>

<span data-ttu-id="6319f-111">tooconfigure integracji usługi Azure AD z logowania jednokrotnego SAML dla Jira przez rozpoznawania GmbH należy hello następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="6319f-111">tooconfigure Azure AD integration with SAML SSO for Jira by resolution GmbH, you need hello following items:</span></span>

- <span data-ttu-id="6319f-112">Subskrypcję usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="6319f-112">An Azure AD subscription</span></span>
- <span data-ttu-id="6319f-113">Logowania jednokrotnego SAML dla Jira przez rozpoznawanie jednokrotnego GmbH w subskrypcji włączone</span><span class="sxs-lookup"><span data-stu-id="6319f-113">A SAML SSO for Jira by resolution GmbH single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="6319f-114">tootest hello kroków w tym samouczku, zaleca się przy użyciu środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="6319f-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="6319f-115">tootest hello kroki opisane w tym samouczku, należy stosować te zalecenia:</span><span class="sxs-lookup"><span data-stu-id="6319f-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="6319f-116">Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="6319f-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="6319f-117">Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz pobrać miesięczna wersja próbna [tutaj](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="6319f-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="6319f-118">Opis scenariusza</span><span class="sxs-lookup"><span data-stu-id="6319f-118">Scenario description</span></span>
<span data-ttu-id="6319f-119">W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym.</span><span class="sxs-lookup"><span data-stu-id="6319f-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="6319f-120">Scenariusz Hello opisane w tym samouczku składa się z dwóch głównych elementów:</span><span class="sxs-lookup"><span data-stu-id="6319f-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="6319f-121">Dodawanie logowania jednokrotnego SAML dla Jira przy rozdzielczości GmbH z galerii hello</span><span class="sxs-lookup"><span data-stu-id="6319f-121">Adding SAML SSO for Jira by resolution GmbH from hello gallery</span></span>
2. <span data-ttu-id="6319f-122">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="6319f-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-saml-sso-for-jira-by-resolution-gmbh-from-hello-gallery"></a><span data-ttu-id="6319f-123">Dodawanie logowania jednokrotnego SAML dla Jira przy rozdzielczości GmbH z galerii hello</span><span class="sxs-lookup"><span data-stu-id="6319f-123">Adding SAML SSO for Jira by resolution GmbH from hello gallery</span></span>
<span data-ttu-id="6319f-124">tooconfigure hello włączenia logowania jednokrotnego SAML dla Jira przez rozpoznawania GmbH do usługi Azure AD, należy tooadd logowania jednokrotnego SAML dla Jira przez rozpoznawania GmbH z hello galerii tooyour listę zarządzanych aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="6319f-124">tooconfigure hello integration of SAML SSO for Jira by resolution GmbH into Azure AD, you need tooadd SAML SSO for Jira by resolution GmbH from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="6319f-125">**tooadd logowania jednokrotnego SAML dla Jira przez rozpoznawania GmbH z galerii hello, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="6319f-125">**tooadd SAML SSO for Jira by resolution GmbH from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="6319f-126">W hello  **[portalu Azure](https://portal.azure.com)**na temat hello panelu nawigacji po lewej stronie, kliknij przycisk **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="6319f-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Usługa Active Directory][1]

2. <span data-ttu-id="6319f-128">Przejdź za**aplikacje dla przedsiębiorstw**.</span><span class="sxs-lookup"><span data-stu-id="6319f-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="6319f-129">Następnie przejdź zbyt**wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="6319f-129">Then go too**All applications**.</span></span>

    ![Aplikacje][2]
    
3. <span data-ttu-id="6319f-131">tooadd nową aplikację, kliknij przycisk **nowej aplikacji** przycisk u góry hello okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="6319f-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplikacje][3]

4. <span data-ttu-id="6319f-133">W polu wyszukiwania hello wpisz **logowania jednokrotnego SAML dla Jira przez rozpoznawania GmbH**.</span><span class="sxs-lookup"><span data-stu-id="6319f-133">In hello search box, type **SAML SSO for Jira by resolution GmbH**.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-samlssojira-tutorial/tutorial_samlssojira_search.png)

5. <span data-ttu-id="6319f-135">W panelu wyników hello, wybierz **logowania jednokrotnego SAML dla Jira przez rozpoznawania GmbH**, a następnie kliknij przycisk **Dodaj** przycisk aplikacji hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="6319f-135">In hello results panel, select **SAML SSO for Jira by resolution GmbH**, and then click **Add** button tooadd hello application.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-samlssojira-tutorial/tutorial_samlssojira_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="6319f-137">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="6319f-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="6319f-138">W tej sekcji możesz skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z logowania jednokrotnego SAML dla Jira przez rozdzielczość GmbH oparte na koncie użytkownika testu o nazwie "Britta Simona".</span><span class="sxs-lookup"><span data-stu-id="6319f-138">In this section, you configure and test Azure AD single sign-on with SAML SSO for Jira by resolution GmbH based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="6319f-139">Dla pojedynczego logowania jednokrotnego toowork usługi Azure AD musi tooknow hello odpowiednikiem użytkownika używanego w logowania jednokrotnego SAML dla Jira przez rozpoznawania GmbH jest tooa użytkownika w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="6319f-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in SAML SSO for Jira by resolution GmbH is tooa user in Azure AD.</span></span> <span data-ttu-id="6319f-140">Innymi słowy relację łącza między użytkownika usługi Azure AD i hello użytkownikowi w logowania jednokrotnego SAML dla Jira przez rozpoznawania GmbH musi toobe ustanowione.</span><span class="sxs-lookup"><span data-stu-id="6319f-140">In other words, a link relationship between an Azure AD user and hello related user in SAML SSO for Jira by resolution GmbH needs toobe established.</span></span>

<span data-ttu-id="6319f-141">W logowania jednokrotnego SAML Jira przez rozpoznawania GmbH, należy przypisać wartość hello hello **nazwy użytkownika** w usłudze Azure AD jako wartość hello hello **Username** tooestablish hello łącze relacji.</span><span class="sxs-lookup"><span data-stu-id="6319f-141">In SAML SSO for Jira by resolution GmbH, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="6319f-142">tooconfigure i testowanie usługi Azure AD rejestracji jednokrotnej z logowania jednokrotnego SAML Jira przez rozpoznawania GmbH, należy po bloków konstrukcyjnych hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="6319f-142">tooconfigure and test Azure AD single sign-on with SAML SSO for Jira by resolution GmbH, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="6319f-143">**[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configuring-azure-ad-single-sign-on)**  -tooenable Twojego toouse użytkowników tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="6319f-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="6319f-144">**[Tworzenie użytkownika testowego usługi Azure AD](#creating-an-azure-ad-test-user)**  -tootest usługi Azure AD rejestracji jednokrotnej z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="6319f-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="6319f-145">**[Tworzenie logowania jednokrotnego SAML dla Jira przez użytkownika testowego GmbH rozpoznawania](#creating-a-saml-sso-for-jira-by-resolution-gmbh-test-user)**  -toohave odpowiednikiem Simona Britta w logowania jednokrotnego SAML dla Jira przez rozpoznawania GmbH, który jest połączony toohello usługi Azure AD reprezentację użytkownika.</span><span class="sxs-lookup"><span data-stu-id="6319f-145">**[Creating a SAML SSO for Jira by resolution GmbH test user](#creating-a-saml-sso-for-jira-by-resolution-gmbh-test-user)** - toohave a counterpart of Britta Simon in SAML SSO for Jira by resolution GmbH that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="6319f-146">**[Przypisanie użytkownika testowego hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Simona Britta toouse usługi Azure AD rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="6319f-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="6319f-147">**[Testowanie rejestracji jednokrotnej](#testing-single-sign-on)**  -tooverify czy hello konfiguracji działania.</span><span class="sxs-lookup"><span data-stu-id="6319f-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="6319f-148">Konfigurowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="6319f-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="6319f-149">W tej sekcji włączyć usługi Azure AD rejestracji jednokrotnej w hello portalu Azure i skonfigurować logowanie jednokrotne w sieci logowania jednokrotnego SAML dla Jira przy rozpoznawania GmbH aplikacji.</span><span class="sxs-lookup"><span data-stu-id="6319f-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your SAML SSO for Jira by resolution GmbH application.</span></span>

<span data-ttu-id="6319f-150">**tooconfigure usługi Azure AD rejestracji jednokrotnej z logowania jednokrotnego SAML dla Jira przez rozpoznawania GmbH, wykonaj hello następujące kroki:**</span><span class="sxs-lookup"><span data-stu-id="6319f-150">**tooconfigure Azure AD single sign-on with SAML SSO for Jira by resolution GmbH, perform hello following steps:**</span></span>

1. <span data-ttu-id="6319f-151">W portalu Azure na powitania hello **logowania jednokrotnego SAML dla Jira przez rozpoznawania GmbH** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.</span><span class="sxs-lookup"><span data-stu-id="6319f-151">In hello Azure portal, on hello **SAML SSO for Jira by resolution GmbH** application integration page, click **Single sign-on**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej][4]

2. <span data-ttu-id="6319f-153">Na powitania **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** tooenable rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="6319f-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-samlssojira-tutorial/tutorial_samlssojira_samlbase.png)

3. <span data-ttu-id="6319f-155">Na powitania **logowania jednokrotnego SAML Jira przez rozpoznawania GmbH domeny i adresów URL** sekcji, jeśli chcesz, aby aplikacja hello tooconfigure w **IDP** inicjowane tryb:</span><span class="sxs-lookup"><span data-stu-id="6319f-155">On hello **SAML SSO for Jira by resolution GmbH Domain and URLs** section, If you wish tooconfigure hello application in **IDP** initiated mode:</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-samlssojira-tutorial/tutorial_samlssojira_url_1.png)

    <span data-ttu-id="6319f-157">a.</span><span class="sxs-lookup"><span data-stu-id="6319f-157">a.</span></span> <span data-ttu-id="6319f-158">W hello **identyfikator** tekstowym, wpisz adres URL za pomocą hello następującego wzorca:`https://<server-base-url>/plugins/servlet/samlsso`</span><span class="sxs-lookup"><span data-stu-id="6319f-158">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<server-base-url>/plugins/servlet/samlsso`</span></span>

    <span data-ttu-id="6319f-159">b.</span><span class="sxs-lookup"><span data-stu-id="6319f-159">b.</span></span> <span data-ttu-id="6319f-160">W hello **adres URL odpowiedzi** tekstowym, wpisz adres URL za pomocą hello następującego wzorca:`https://<server-base-url>/plugins/servlet/samlsso`</span><span class="sxs-lookup"><span data-stu-id="6319f-160">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://<server-base-url>/plugins/servlet/samlsso`</span></span>

4. <span data-ttu-id="6319f-161">Sprawdź **Pokaż zaawansowane ustawienia adresu URL**.</span><span class="sxs-lookup"><span data-stu-id="6319f-161">Check **Show advanced URL settings**.</span></span> <span data-ttu-id="6319f-162">Jeśli chcesz, aby aplikacja hello tooconfigure w **SP** inicjowane tryb:</span><span class="sxs-lookup"><span data-stu-id="6319f-162">If you wish tooconfigure hello application in **SP** initiated mode:</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-samlssojira-tutorial/tutorial_samlssojira_url_2.png)

    <span data-ttu-id="6319f-164">W hello **adres URL logowania** tekstowym, wpisz adres URL za pomocą hello następującego wzorca:`https://<server-base-url>/plugins/servlet/samlsso`</span><span class="sxs-lookup"><span data-stu-id="6319f-164">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<server-base-url>/plugins/servlet/samlsso`</span></span>
     
    > [!NOTE] 
    > <span data-ttu-id="6319f-165">Wartości te nie są prawdziwe.</span><span class="sxs-lookup"><span data-stu-id="6319f-165">These values are not real.</span></span> <span data-ttu-id="6319f-166">Zaktualizować te wartości z hello rzeczywisty identyfikator, adres URL odpowiedzi i adres URL logowania.</span><span class="sxs-lookup"><span data-stu-id="6319f-166">Update these values with hello actual Identifier, Reply URL, and Sign-On URL.</span></span> <span data-ttu-id="6319f-167">Skontaktuj się z [zespołu obsługi logowania jednokrotnego SAML dla Jira przez rozpoznawania klienta GmbH](https://www.resolution.de/go/support) tooget tych wartości.</span><span class="sxs-lookup"><span data-stu-id="6319f-167">Contact [SAML SSO for Jira by resolution GmbH Client support team](https://www.resolution.de/go/support) tooget these values.</span></span> 

5. <span data-ttu-id="6319f-168">Na powitania **certyfikat podpisywania SAML** kliknij **XML metadanych** , a następnie zapisz plik metadanych hello na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="6319f-168">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-samlssojira-tutorial/tutorial_samlssojira_certificate.png) 

6. <span data-ttu-id="6319f-170">Kliknij przycisk **zapisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="6319f-170">Click **Save** button.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-samlssojira-tutorial/tutorial_general_400.png)
    
7. <span data-ttu-id="6319f-172">W oknie przeglądarki innej witryny sieci web, zaloguj się za tooyour **logowania jednokrotnego SAML dla Jira przez portal administracyjny GmbH rozpoznawania** jako administrator.</span><span class="sxs-lookup"><span data-stu-id="6319f-172">In a different web browser window, log in tooyour **SAML SSO for Jira by resolution GmbH admin portal** as an administrator.</span></span>

8. <span data-ttu-id="6319f-173">Umieść kursor na koło zębate, a następnie kliknij przycisk hello **dodatki**.</span><span class="sxs-lookup"><span data-stu-id="6319f-173">Hover on cog and click hello **Add-ons**.</span></span>
    
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-samlssojira-tutorial/addon1.png)

9. <span data-ttu-id="6319f-175">Jesteś przekierowanego tooAdministrator dostępu do strony.</span><span class="sxs-lookup"><span data-stu-id="6319f-175">You are redirected tooAdministrator Access page.</span></span> <span data-ttu-id="6319f-176">Wprowadź hello **hasło** i kliknij przycisk **Potwierdź** przycisku.</span><span class="sxs-lookup"><span data-stu-id="6319f-176">Enter hello **Password** and click **Confirm** button.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-samlssojira-tutorial/addon2.png)

10. <span data-ttu-id="6319f-178">W sekcji Karta dodatki, kliknij przycisk **znaleźć nowe dodatki**.</span><span class="sxs-lookup"><span data-stu-id="6319f-178">Under Add-ons tab section, click **Find new add-ons**.</span></span> <span data-ttu-id="6319f-179">Wyszukiwanie **SAML pojedynczy znak na rejestracji jednokrotnej (SSO) dla JIRA** i kliknij przycisk **zainstalować** tooinstall przycisk hello nowej wtyczki SAML.</span><span class="sxs-lookup"><span data-stu-id="6319f-179">Search **SAML Single Sign On (SSO) for JIRA** and click **Install** button tooinstall hello new SAML plugin.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-samlssojira-tutorial/addon7.png)

11. <span data-ttu-id="6319f-181">Instalacja dodatku Hello rozpocznie.</span><span class="sxs-lookup"><span data-stu-id="6319f-181">hello plugin installation will start.</span></span> <span data-ttu-id="6319f-182">Kliknij przycisk **Zamknij**.</span><span class="sxs-lookup"><span data-stu-id="6319f-182">Click **Close**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-samlssojira-tutorial/addon8.png)

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-samlssojira-tutorial/addon9.png)

12. <span data-ttu-id="6319f-185">Kliknij pozycję **Zarządzaj**.</span><span class="sxs-lookup"><span data-stu-id="6319f-185">Click **Manage**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-samlssojira-tutorial/addon10.png)
    
13. <span data-ttu-id="6319f-187">Kliknij przycisk **Konfiguruj** tooconfigure hello nowej wtyczki.</span><span class="sxs-lookup"><span data-stu-id="6319f-187">Click **Configure** tooconfigure hello new plugin.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-samlssojira-tutorial/addon11.png)

14. <span data-ttu-id="6319f-189">Na **konfiguracji wtyczki SingleSignOn SAML** kliknij przycisk **dodać dodatkowe dostawcy tożsamości** przycisk tooconfigure hello ustawienia dostawcy tożsamości.</span><span class="sxs-lookup"><span data-stu-id="6319f-189">On **SAML SingleSignOn Plugin Configuration** page, click **Add additional Identity Provider** button tooconfigure hello settings of Identity Provider.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-samlssojira-tutorial/addon4.png)

15. <span data-ttu-id="6319f-191">Wykonaj następujące kroki na tej stronie:</span><span class="sxs-lookup"><span data-stu-id="6319f-191">Perform following steps on this page:</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-samlssojira-tutorial/addon5.png)
 
    <span data-ttu-id="6319f-193">a.</span><span class="sxs-lookup"><span data-stu-id="6319f-193">a.</span></span> <span data-ttu-id="6319f-194">Dodaj **nazwa** z hello dostawcy tożsamości (np. usługi Azure AD).</span><span class="sxs-lookup"><span data-stu-id="6319f-194">Add **Name** of hello Identity Provider (e.g Azure AD).</span></span>
    
    <span data-ttu-id="6319f-195">b.</span><span class="sxs-lookup"><span data-stu-id="6319f-195">b.</span></span> <span data-ttu-id="6319f-196">Dodaj **opis** z hello dostawcy tożsamości (np. usługi Azure AD).</span><span class="sxs-lookup"><span data-stu-id="6319f-196">Add **Description** of hello Identity Provider (e.g Azure AD).</span></span>

    <span data-ttu-id="6319f-197">c.</span><span class="sxs-lookup"><span data-stu-id="6319f-197">c.</span></span> <span data-ttu-id="6319f-198">Kliknij przycisk **XML** i wybierz hello **metadanych** pliku, który został pobrany z portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="6319f-198">Click **XML** and select hello **Metadata** file, which you have downloaded from Azure portal.</span></span>

    <span data-ttu-id="6319f-199">d.</span><span class="sxs-lookup"><span data-stu-id="6319f-199">d.</span></span> <span data-ttu-id="6319f-200">Kliknij przycisk **obciążenia** przycisku.</span><span class="sxs-lookup"><span data-stu-id="6319f-200">Click **Load** button.</span></span>

    <span data-ttu-id="6319f-201">e.</span><span class="sxs-lookup"><span data-stu-id="6319f-201">e.</span></span> <span data-ttu-id="6319f-202">Odczytuje hello IdP metadanych i wypełni pola hello jak wyróżniono hello zrzucie ekranu.</span><span class="sxs-lookup"><span data-stu-id="6319f-202">It reads hello IdP metadata and populates hello fields as highlighted in hello screenshot.</span></span>   

16. <span data-ttu-id="6319f-203">Kliknij przycisk **Zapisz ustawienia** przycisk toosave hello ustawienia.</span><span class="sxs-lookup"><span data-stu-id="6319f-203">Click **Save settings** button toosave hello settings.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-samlssojira-tutorial/addon6.png)

> [!TIP]
> <span data-ttu-id="6319f-205">Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz hello [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji hello!</span><span class="sxs-lookup"><span data-stu-id="6319f-205">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="6319f-206">Po dodaniu tej aplikacji z hello **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij hello **rejestracji jednokrotnej** hello kartę i dostępu do osadzonych dokumentacji za pośrednictwem hello  **Konfiguracja** sekcji u dołu hello.</span><span class="sxs-lookup"><span data-stu-id="6319f-206">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="6319f-207">Więcej o hello osadzonych dokumentacji funkcji w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="6319f-207">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="6319f-208">Tworzenie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="6319f-208">Creating an Azure AD test user</span></span>
<span data-ttu-id="6319f-209">Celem Hello w tej sekcji jest toocreate użytkownika testowego, w portalu Azure o nazwie Simona Britta hello.</span><span class="sxs-lookup"><span data-stu-id="6319f-209">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Tworzenie użytkowników usługi Azure AD][100]

<span data-ttu-id="6319f-211">**toocreate użytkownika testowego w usłudze Azure AD, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="6319f-211">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="6319f-212">W hello **portalu Azure**na temat hello w lewym okienku nawigacji, kliknij przycisk **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="6319f-212">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-samlssojira-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="6319f-214">toodisplay hello listę użytkowników, przejdź zbyt**użytkowników i grup** i kliknij przycisk **wszyscy użytkownicy**.</span><span class="sxs-lookup"><span data-stu-id="6319f-214">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-samlssojira-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="6319f-216">Witaj tooopen **użytkownika** okna dialogowego, kliknij przycisk **Dodaj** u góry hello hello okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="6319f-216">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-samlssojira-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="6319f-218">Na powitania **użytkownika** okna dialogowego wykonaj hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="6319f-218">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-samlssojira-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="6319f-220">a.</span><span class="sxs-lookup"><span data-stu-id="6319f-220">a.</span></span> <span data-ttu-id="6319f-221">W hello **nazwa** pole tekstowe, typ **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="6319f-221">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="6319f-222">b.</span><span class="sxs-lookup"><span data-stu-id="6319f-222">b.</span></span> <span data-ttu-id="6319f-223">W hello **nazwy użytkownika** pole tekstowe, hello typu **adres e-mail** z BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="6319f-223">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="6319f-224">c.</span><span class="sxs-lookup"><span data-stu-id="6319f-224">c.</span></span> <span data-ttu-id="6319f-225">Wybierz **Pokaż hasło** i zanotuj wartość hello hello **hasło**.</span><span class="sxs-lookup"><span data-stu-id="6319f-225">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="6319f-226">d.</span><span class="sxs-lookup"><span data-stu-id="6319f-226">d.</span></span> <span data-ttu-id="6319f-227">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="6319f-227">Click **Create**.</span></span>
 
### <a name="creating-a-saml-sso-for-jira-by-resolution-gmbh-test-user"></a><span data-ttu-id="6319f-228">Tworzenie logowania jednokrotnego SAML dla Jira przez użytkownika testowego GmbH rozwiązania</span><span class="sxs-lookup"><span data-stu-id="6319f-228">Creating a SAML SSO for Jira by resolution GmbH test user</span></span>

<span data-ttu-id="6319f-229">toolog użytkowników tooenable usługi Azure AD w tooSAML logowania jednokrotnego dla Jira przez rozpoznawania GmbH one muszą mieć przydzielone do logowania jednokrotnego SAML dla Jira przez rozpoznawania GmbH.</span><span class="sxs-lookup"><span data-stu-id="6319f-229">tooenable Azure AD users toolog in tooSAML SSO for Jira by resolution GmbH, they must be provisioned into SAML SSO for Jira by resolution GmbH.</span></span>  
<span data-ttu-id="6319f-230">W logowania jednokrotnego SAML Jira przez rozpoznawania GmbH Inicjowanie obsługi to zadanie ręczne.</span><span class="sxs-lookup"><span data-stu-id="6319f-230">In SAML SSO for Jira by resolution GmbH, provisioning is a manual task.</span></span>

<span data-ttu-id="6319f-231">**tooprovision konta użytkownika, należy wykonać hello następujące kroki:**</span><span class="sxs-lookup"><span data-stu-id="6319f-231">**tooprovision a user account, perform hello following steps:**</span></span>

1. <span data-ttu-id="6319f-232">Zaloguj się za tooyour logowania jednokrotnego SAML dla Jira przez witrynę firmy GmbH rozpoznawania jako administrator.</span><span class="sxs-lookup"><span data-stu-id="6319f-232">Log in tooyour SAML SSO for Jira by resolution GmbH company site as an administrator.</span></span>

2. <span data-ttu-id="6319f-233">Umieść kursor na koło zębate, a następnie kliknij przycisk hello **Zarządzanie użytkownikami**.</span><span class="sxs-lookup"><span data-stu-id="6319f-233">Hover on cog and click hello **User management**.</span></span>

    ![Dodawanie pracownika](./media/active-directory-saas-samlssojira-tutorial/user1.png) 

3. <span data-ttu-id="6319f-235">Jesteś tooenter stronę dostępu do przekierowanych tooAdministrator **hasła** i kliknij przycisk **Potwierdź** przycisku.</span><span class="sxs-lookup"><span data-stu-id="6319f-235">You are redirected tooAdministrator Access page tooenter **Password** and click **Confirm** button.</span></span>

    ![Dodawanie pracownika](./media/active-directory-saas-samlssojira-tutorial/user2.png) 

4. <span data-ttu-id="6319f-237">W obszarze **Zarządzanie użytkownikami** sekcji, kliknij pozycję **Utwórz użytkownika**.</span><span class="sxs-lookup"><span data-stu-id="6319f-237">Under **User management** tab section, click **create user**.</span></span>

    ![Dodawanie pracownika](./media/active-directory-saas-samlssojira-tutorial/user3.png) 

5. <span data-ttu-id="6319f-239">Na powitania **"Tworzenie nowego użytkownika"** okna dialogowego wykonaj hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="6319f-239">On hello **“Create new user”** dialog page, perform hello following steps:</span></span>

    ![Dodawanie pracownika](./media/active-directory-saas-samlssojira-tutorial/user4.png) 

    <span data-ttu-id="6319f-241">a.</span><span class="sxs-lookup"><span data-stu-id="6319f-241">a.</span></span> <span data-ttu-id="6319f-242">W hello **adres E-mail** pole tekstowe, typ hello adres e-mail użytkownika, takich jak Brittasimon@contoso.com.</span><span class="sxs-lookup"><span data-stu-id="6319f-242">In hello **Email address** textbox, type hello email address of user like Brittasimon@contoso.com.</span></span>

    <span data-ttu-id="6319f-243">b.</span><span class="sxs-lookup"><span data-stu-id="6319f-243">b.</span></span> <span data-ttu-id="6319f-244">W hello **imię i nazwisko** tekstowym, wpisz pełną nazwę użytkownika hello jak Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="6319f-244">In hello **Full Name** textbox, type full name of hello user like Britta Simon.</span></span>

    <span data-ttu-id="6319f-245">c.</span><span class="sxs-lookup"><span data-stu-id="6319f-245">c.</span></span> <span data-ttu-id="6319f-246">W hello **Username** pole tekstowe, powitalne wiadomości e-mail użytkownika, takich jak Brittasimon@contoso.com.</span><span class="sxs-lookup"><span data-stu-id="6319f-246">In hello **Username** textbox, type hello email of user like Brittasimon@contoso.com.</span></span>

    <span data-ttu-id="6319f-247">d.</span><span class="sxs-lookup"><span data-stu-id="6319f-247">d.</span></span> <span data-ttu-id="6319f-248">W hello **hasło** tekstowym, wpisz hello hasło użytkownika.</span><span class="sxs-lookup"><span data-stu-id="6319f-248">In hello **Password** textbox, type hello password of user.</span></span>

    <span data-ttu-id="6319f-249">e.</span><span class="sxs-lookup"><span data-stu-id="6319f-249">e.</span></span> <span data-ttu-id="6319f-250">Kliknij przycisk **tworzenia użytkownika**.</span><span class="sxs-lookup"><span data-stu-id="6319f-250">Click **Create user**.</span></span>   

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="6319f-251">Przypisanie użytkownika testowego hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="6319f-251">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="6319f-252">W tej sekcji możesz włączyć toouse Simona Britta Azure logowania jednokrotnego za udzielanie dostępu tooSAML logowania jednokrotnego dla Jira przez rozpoznawania GmbH.</span><span class="sxs-lookup"><span data-stu-id="6319f-252">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooSAML SSO for Jira by resolution GmbH.</span></span>

![Przypisz użytkownika][200] 

<span data-ttu-id="6319f-254">**tooassign Simona Britta tooSAML logowania jednokrotnego dla Jira przez rozpoznawania GmbH, wykonaj hello następujące kroki:**</span><span class="sxs-lookup"><span data-stu-id="6319f-254">**tooassign Britta Simon tooSAML SSO for Jira by resolution GmbH, perform hello following steps:**</span></span>

1. <span data-ttu-id="6319f-255">W portalu Azure hello, otwórz widok aplikacji hello, a następnie przejdź do widoku katalogu toohello i przejść za**aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="6319f-255">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Przypisz użytkownika][201] 

2. <span data-ttu-id="6319f-257">Z listy aplikacji hello wybierz **logowania jednokrotnego SAML dla Jira przez rozpoznawania GmbH**.</span><span class="sxs-lookup"><span data-stu-id="6319f-257">In hello applications list, select **SAML SSO for Jira by resolution GmbH**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-samlssojira-tutorial/tutorial_samlssojira_app.png) 

3. <span data-ttu-id="6319f-259">W menu powitania po lewej stronie powitania kliknij **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="6319f-259">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Przypisz użytkownika][202] 

4. <span data-ttu-id="6319f-261">Kliknij przycisk **Dodaj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="6319f-261">Click **Add** button.</span></span> <span data-ttu-id="6319f-262">Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="6319f-262">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Przypisz użytkownika][203]

5. <span data-ttu-id="6319f-264">Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** hello listy użytkowników.</span><span class="sxs-lookup"><span data-stu-id="6319f-264">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="6319f-265">Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="6319f-265">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="6319f-266">Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="6319f-266">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="6319f-267">Testowanie rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="6319f-267">Testing single sign-on</span></span>

<span data-ttu-id="6319f-268">W tej sekcji można przetestować konfiguracji usługi Azure AD pojedynczego logowania jednokrotnego przy użyciu hello panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="6319f-268">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="6319f-269">Po kliknięciu hello logowania jednokrotnego SAML dla Jira przez rozpoznawania GmbH kafelka w hello Panel dostępu, należy pobrać automatycznie zalogowane tooyour logowania jednokrotnego SAML dla Jira przez rozpoznawania GmbH aplikacji.</span><span class="sxs-lookup"><span data-stu-id="6319f-269">When you click hello SAML SSO for Jira by resolution GmbH tile in hello Access Panel, you should get automatically signed-on tooyour SAML SSO for Jira by resolution GmbH application.</span></span>
<span data-ttu-id="6319f-270">Aby uzyskać więcej informacji na temat panelu dostępu, zobacz [wprowadzenie do panelu dostępu](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="6319f-270">For more information about the Access Panel, see [introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="6319f-271">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="6319f-271">Additional resources</span></span>

* [<span data-ttu-id="6319f-272">Lista samouczków dotyczących tooIntegrate aplikacji SaaS w usłudze Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="6319f-272">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="6319f-273">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="6319f-273">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-samlssojira-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-samlssojira-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-samlssojira-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-samlssojira-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-samlssojira-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-samlssojira-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-samlssojira-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-samlssojira-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-samlssojira-tutorial/tutorial_general_203.png

