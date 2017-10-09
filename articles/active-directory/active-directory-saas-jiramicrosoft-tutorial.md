---
title: "Samouczek: Integracji Azure Active Directory z logowania jednokrotnego SAML JIRA przez firmę Microsoft | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak tooconfigure logowanie jednokrotne między usługą Azure Active Directory i logowania jednokrotnego SAML JIRA przez firmę Microsoft."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 0dc847b9-eec4-4c31-845e-0144ddedc4a7
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/19/2017
ms.author: jeedes
ms.openlocfilehash: 178c4c040d9939bca271ac185ca5c2feb14f1247
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-jira-saml-sso-by-microsoft"></a><span data-ttu-id="794fa-103">Samouczek: Integracji Azure Active Directory z logowania jednokrotnego SAML JIRA przez firmę Microsoft</span><span class="sxs-lookup"><span data-stu-id="794fa-103">Tutorial: Azure Active Directory integration with JIRA SAML SSO by Microsoft</span></span>

<span data-ttu-id="794fa-104">Z tego samouczka, dowiesz się, jak toointegrate logowania jednokrotnego SAML JIRA przez firmę Microsoft w usłudze Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="794fa-104">In this tutorial, you learn how toointegrate JIRA SAML SSO by Microsoft with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="794fa-105">Integracja z usługą Azure AD logowania jednokrotnego SAML JIRA przez firmę Microsoft udostępnia hello następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="794fa-105">Integrating JIRA SAML SSO by Microsoft with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="794fa-106">Można kontrolować w usłudze Azure AD, kto ma dostęp do tooJIRA logowania jednokrotnego SAML przez firmę Microsoft</span><span class="sxs-lookup"><span data-stu-id="794fa-106">You can control in Azure AD who has access tooJIRA SAML SSO by Microsoft</span></span>
- <span data-ttu-id="794fa-107">Można włączyć użytkownika użytkownicy tooautomatically get zalogowane tooJIRA logowania jednokrotnego SAML przez firmę Microsoft (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="794fa-107">You can enable your users tooautomatically get signed-on tooJIRA SAML SSO by Microsoft (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="794fa-108">Możesz zarządzać kont w jednej centralnej lokalizacji - hello portalu Azure</span><span class="sxs-lookup"><span data-stu-id="794fa-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="794fa-109">Jeśli chcesz tooknow więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="794fa-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="794fa-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="794fa-110">Prerequisites</span></span>

<span data-ttu-id="794fa-111">tooconfigure integracji z usługą Azure AD z logowania jednokrotnego SAML JIRA przez firmę Microsoft, należy hello następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="794fa-111">tooconfigure Azure AD integration with JIRA SAML SSO by Microsoft, you need hello following items:</span></span>

- <span data-ttu-id="794fa-112">Subskrypcję usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="794fa-112">An Azure AD subscription</span></span>
- <span data-ttu-id="794fa-113">Aplikacja serwera JIRA zainstalowany na serwerze Windows 64-bitowych (lokalnie lub w chmurze hello infrastrukturą IaaS)</span><span class="sxs-lookup"><span data-stu-id="794fa-113">JIRA server application installed on a Windows 64-bit server (on premise or on hello cloud IaaS infrastructure)</span></span>
- <span data-ttu-id="794fa-114">Serwer JIRA jest obsługujące protokół HTTPS</span><span class="sxs-lookup"><span data-stu-id="794fa-114">JIRA server is HTTPS enabled</span></span>
- <span data-ttu-id="794fa-115">Uwaga hello obsługiwane wersje dla wtyczki JIRA są wymienione w poniższej sekcji.</span><span class="sxs-lookup"><span data-stu-id="794fa-115">Note hello supported versions for JIRA Plugin are mentioned in below section.</span></span>
- <span data-ttu-id="794fa-116">JIRA serwer jest dostępny w Internecie szczególnie tooAzure dla uwierzytelniania strony logowania usługi AD i powinien tooreceive stanie hello tokenu z usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="794fa-116">JIRA server is reachable on internet particularly tooAzure AD Login page for authentication and should able tooreceive hello token from Azure AD</span></span>
- <span data-ttu-id="794fa-117">Poświadczenia administratora są konfigurowane w JIRA</span><span class="sxs-lookup"><span data-stu-id="794fa-117">Admin credentials are set up in JIRA</span></span>
- <span data-ttu-id="794fa-118">WebSudo jest wyłączona w JIRA</span><span class="sxs-lookup"><span data-stu-id="794fa-118">WebSudo is disabled in JIRA</span></span>
- <span data-ttu-id="794fa-119">Testowanie użytkowników utworzone w hello JIRA serwera aplikacji</span><span class="sxs-lookup"><span data-stu-id="794fa-119">Test user created in hello JIRA server application</span></span>

> [!NOTE]
> <span data-ttu-id="794fa-120">tootest hello kroków w tym samouczku, zaleca się przy użyciu środowiska produkcyjnego programu JIRA.</span><span class="sxs-lookup"><span data-stu-id="794fa-120">tootest hello steps in this tutorial, we do not recommend using a production environment of JIRA.</span></span> <span data-ttu-id="794fa-121">Testowanie integracji hello najpierw w rozwoju lub przemieszczania środowisko aplikacji hello, a następnie środowiska produkcyjnego hello użycia.</span><span class="sxs-lookup"><span data-stu-id="794fa-121">Test hello integration first in development or staging environment of hello application and then use hello production environment.</span></span>

<span data-ttu-id="794fa-122">tootest hello kroki opisane w tym samouczku, należy stosować te zalecenia:</span><span class="sxs-lookup"><span data-stu-id="794fa-122">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="794fa-123">Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="794fa-123">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="794fa-124">Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz pobrać miesięczna wersja próbna tutaj: [oferta wersji próbnej](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="794fa-124">If you don't have an Azure AD trial environment, you can get a one-month trial here: [Trial offer](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="supported-versions-of-jira"></a><span data-ttu-id="794fa-125">Obsługiwane wersje JIRA</span><span class="sxs-lookup"><span data-stu-id="794fa-125">Supported versions of JIRA</span></span> 

<span data-ttu-id="794fa-126">Od tej chwili obsługiwane są następujące wersje JIRA:</span><span class="sxs-lookup"><span data-stu-id="794fa-126">As of now, following versions of JIRA are supported:</span></span>

- <span data-ttu-id="794fa-127">Podstawowe JIRA i oprogramowania: 6.0 too7.2.0</span><span class="sxs-lookup"><span data-stu-id="794fa-127">JIRA Core and Software: 6.0 too7.2.0</span></span>
- <span data-ttu-id="794fa-128">JIRA działu: 3.0 too3.2</span><span class="sxs-lookup"><span data-stu-id="794fa-128">JIRA Service Desk: 3.0 too3.2</span></span>

## <a name="scenario-description"></a><span data-ttu-id="794fa-129">Opis scenariusza</span><span class="sxs-lookup"><span data-stu-id="794fa-129">Scenario description</span></span>
<span data-ttu-id="794fa-130">W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym.</span><span class="sxs-lookup"><span data-stu-id="794fa-130">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="794fa-131">Scenariusz Hello opisane w tym samouczku składa się z dwóch głównych elementów:</span><span class="sxs-lookup"><span data-stu-id="794fa-131">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="794fa-132">Dodawanie z galerii hello logowania jednokrotnego SAML JIRA przez firmę Microsoft</span><span class="sxs-lookup"><span data-stu-id="794fa-132">Adding JIRA SAML SSO by Microsoft from hello gallery</span></span>
2. <span data-ttu-id="794fa-133">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="794fa-133">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-jira-saml-sso-by-microsoft-from-hello-gallery"></a><span data-ttu-id="794fa-134">Dodawanie z galerii hello logowania jednokrotnego SAML JIRA przez firmę Microsoft</span><span class="sxs-lookup"><span data-stu-id="794fa-134">Adding JIRA SAML SSO by Microsoft from hello gallery</span></span>
<span data-ttu-id="794fa-135">tooconfigure hello włączenia logowania jednokrotnego SAML JIRA przez firmę Microsoft do usługi Azure AD, należy tooadd logowania jednokrotnego SAML JIRA przez firmę Microsoft z hello galerii tooyour listę zarządzanych aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="794fa-135">tooconfigure hello integration of JIRA SAML SSO by Microsoft into Azure AD, you need tooadd JIRA SAML SSO by Microsoft from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="794fa-136">**tooadd logowania jednokrotnego SAML JIRA przez firmę Microsoft z galerii hello wykonaj hello następujące kroki:**</span><span class="sxs-lookup"><span data-stu-id="794fa-136">**tooadd JIRA SAML SSO by Microsoft from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="794fa-137">W hello  **[portalu Azure](https://portal.azure.com)**na temat hello panelu nawigacji po lewej stronie, kliknij przycisk **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="794fa-137">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Usługa Active Directory][1]

2. <span data-ttu-id="794fa-139">Przejdź za**aplikacje dla przedsiębiorstw**.</span><span class="sxs-lookup"><span data-stu-id="794fa-139">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="794fa-140">Następnie przejdź zbyt**wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="794fa-140">Then go too**All applications**.</span></span>

    ![Aplikacje][2]
    
3. <span data-ttu-id="794fa-142">tooadd nową aplikację, kliknij przycisk **nowej aplikacji** przycisk u góry hello okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="794fa-142">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplikacje][3]

4. <span data-ttu-id="794fa-144">W polu wyszukiwania hello wpisz **logowania jednokrotnego SAML JIRA przez firmę Microsoft**.</span><span class="sxs-lookup"><span data-stu-id="794fa-144">In hello search box, type **JIRA SAML SSO by Microsoft**.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-jiramicrosoft-tutorial/tutorial_jiramicrosoft_search.png)

5. <span data-ttu-id="794fa-146">W panelu wyników hello, wybierz **logowania jednokrotnego SAML JIRA przez firmę Microsoft**, a następnie kliknij przycisk **Dodaj** przycisk tooadd hello aplikacji.</span><span class="sxs-lookup"><span data-stu-id="794fa-146">In hello results panel, select **JIRA SAML SSO by Microsoft**, and then click **Add** button tooadd hello application.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-jiramicrosoft-tutorial/tutorial_jiramicrosoft_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="794fa-148">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="794fa-148">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="794fa-149">W tej sekcji możesz skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z logowania jednokrotnego SAML JIRA przez firmę Microsoft na podstawie użytkownika testowego, nazywany "Britta Simona".</span><span class="sxs-lookup"><span data-stu-id="794fa-149">In this section, you configure and test Azure AD single sign-on with JIRA SAML SSO by Microsoft based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="794fa-150">Dla pojedynczego logowania jednokrotnego toowork usługi Azure AD musi tooknow użytkownika odpowiednikiem hello w logowania jednokrotnego SAML JIRA przez firmę Microsoft jest tooa użytkownika w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="794fa-150">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in JIRA SAML SSO by Microsoft is tooa user in Azure AD.</span></span> <span data-ttu-id="794fa-151">Innymi słowy łącze relację między użytkownika usługi Azure AD i powiązane użytkownika logowania jednokrotnego SAML JIRA przez firmę Microsoft hello musi toobe ustanowione.</span><span class="sxs-lookup"><span data-stu-id="794fa-151">In other words, a link relationship between an Azure AD user and hello related user in JIRA SAML SSO by Microsoft needs toobe established.</span></span>

<span data-ttu-id="794fa-152">W JIRA logowania jednokrotnego SAML przez firmę Microsoft, należy przypisać wartość hello hello **nazwy użytkownika** w usłudze Azure AD jako wartość hello hello **Username** tooestablish hello łącze relacji.</span><span class="sxs-lookup"><span data-stu-id="794fa-152">In JIRA SAML SSO by Microsoft, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="794fa-153">tooconfigure i testowych usługi Azure AD rejestracji jednokrotnej z logowania jednokrotnego SAML JIRA przez firmę Microsoft, należy po bloków konstrukcyjnych hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="794fa-153">tooconfigure and test Azure AD single sign-on with JIRA SAML SSO by Microsoft, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="794fa-154">**[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configuring-azure-ad-single-sign-on)**  -tooenable Twojego toouse użytkowników tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="794fa-154">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="794fa-155">**[Tworzenie użytkownika testowego usługi Azure AD](#creating-an-azure-ad-test-user)**  -tootest usługi Azure AD rejestracji jednokrotnej z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="794fa-155">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="794fa-156">**[Tworzenie logowania jednokrotnego SAML JIRA przez użytkownika testowego Microsoft](#creating-a-jira-saml-sso-by-microsoft-test-user)**  -toohave odpowiednikiem Simona Britta w logowania jednokrotnego SAML JIRA przez firmę Microsoft, który jest połączony toohello usługi Azure AD reprezentację użytkownika.</span><span class="sxs-lookup"><span data-stu-id="794fa-156">**[Creating a JIRA SAML SSO by Microsoft test user](#creating-a-jira-saml-sso-by-microsoft-test-user)** - toohave a counterpart of Britta Simon in JIRA SAML SSO by Microsoft that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="794fa-157">**[Przypisanie użytkownika testowego hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Simona Britta toouse usługi Azure AD rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="794fa-157">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="794fa-158">**[Testowanie rejestracji jednokrotnej](#testing-single-sign-on)**  -tooverify czy hello konfiguracji działania.</span><span class="sxs-lookup"><span data-stu-id="794fa-158">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="794fa-159">Konfigurowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="794fa-159">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="794fa-160">W tej sekcji włączyć usługi Azure AD rejestracji jednokrotnej w hello portalu Azure i skonfigurować logowanie jednokrotne w sieci logowania jednokrotnego SAML JIRA przez aplikację Microsoft.</span><span class="sxs-lookup"><span data-stu-id="794fa-160">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your JIRA SAML SSO by Microsoft application.</span></span>

<span data-ttu-id="794fa-161">**tooconfigure usługi Azure AD rejestracji jednokrotnej z logowania jednokrotnego SAML JIRA przez firmę Microsoft, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="794fa-161">**tooconfigure Azure AD single sign-on with JIRA SAML SSO by Microsoft, perform hello following steps:**</span></span>

1. <span data-ttu-id="794fa-162">W portalu Azure na powitania hello **logowania jednokrotnego SAML JIRA przez firmę Microsoft** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.</span><span class="sxs-lookup"><span data-stu-id="794fa-162">In hello Azure portal, on hello **JIRA SAML SSO by Microsoft** application integration page, click **Single sign-on**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej][4]

2. <span data-ttu-id="794fa-164">Na powitania **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** tooenable rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="794fa-164">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-jiramicrosoft-tutorial/tutorial_jiramicrosoft_samlbase.png)

3. <span data-ttu-id="794fa-166">Na powitania **logowania jednokrotnego SAML JIRA Domain firmy Microsoft i adresy URL** sekcji, wykonaj następujące kroki hello:</span><span class="sxs-lookup"><span data-stu-id="794fa-166">On hello **JIRA SAML SSO by Microsoft Domain and URLs** section, perform hello following steps:</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-jiramicrosoft-tutorial/tutorial_jiramicrosoft_url.png)

    <span data-ttu-id="794fa-168">a.</span><span class="sxs-lookup"><span data-stu-id="794fa-168">a.</span></span> <span data-ttu-id="794fa-169">W hello **adres URL logowania** tekstowym, wpisz adres URL za pomocą hello następującego wzorca:`https://<domain:port>/plugins/servlet/saml/auth`</span><span class="sxs-lookup"><span data-stu-id="794fa-169">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<domain:port>/plugins/servlet/saml/auth`</span></span>

    <span data-ttu-id="794fa-170">b.</span><span class="sxs-lookup"><span data-stu-id="794fa-170">b.</span></span> <span data-ttu-id="794fa-171">W hello **identyfikator** tekstowym, wpisz adres URL za pomocą hello następującego wzorca:`https://<domain:port>/`</span><span class="sxs-lookup"><span data-stu-id="794fa-171">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<domain:port>/`</span></span>

    <span data-ttu-id="794fa-172">c.</span><span class="sxs-lookup"><span data-stu-id="794fa-172">c.</span></span> <span data-ttu-id="794fa-173">W hello **adres URL odpowiedzi** tekstowym, wpisz adres URL za pomocą hello następującego wzorca:`https://<domain:port>/plugins/servlet/saml/auth`</span><span class="sxs-lookup"><span data-stu-id="794fa-173">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://<domain:port>/plugins/servlet/saml/auth`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="794fa-174">Wartości te nie są prawdziwe.</span><span class="sxs-lookup"><span data-stu-id="794fa-174">These values are not real.</span></span> <span data-ttu-id="794fa-175">Zaktualizować te wartości z hello rzeczywisty identyfikator, adres URL odpowiedzi i adres URL logowania.</span><span class="sxs-lookup"><span data-stu-id="794fa-175">Update these values with hello actual Identifier, Reply URL, and Sign-On URL.</span></span> <span data-ttu-id="794fa-176">Port jest opcjonalny w przypadku, gdy jest nazwane adres URL.</span><span class="sxs-lookup"><span data-stu-id="794fa-176">Port is optional in case it’s a named URL.</span></span> <span data-ttu-id="794fa-177">Te wartości są odbierane podczas konfigurowania hello Jira wtyczki, który znajduje się w dalszej części samouczka hello.</span><span class="sxs-lookup"><span data-stu-id="794fa-177">These values are received during hello configuration of Jira plugin, which is explained later in hello tutorial.</span></span>
 
4. <span data-ttu-id="794fa-178">Witaj toogenerate **metadanych** adres url, wykonaj następujące kroki hello:</span><span class="sxs-lookup"><span data-stu-id="794fa-178">toogenerate hello **Metadata** url, perform hello following steps:</span></span>

    <span data-ttu-id="794fa-179">a.</span><span class="sxs-lookup"><span data-stu-id="794fa-179">a.</span></span> <span data-ttu-id="794fa-180">Kliknij przycisk **rejestracji aplikacji**.</span><span class="sxs-lookup"><span data-stu-id="794fa-180">Click **App registrations**.</span></span>
    
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-jiramicrosoft-tutorial/appregistrations.png)
   
    <span data-ttu-id="794fa-182">b.</span><span class="sxs-lookup"><span data-stu-id="794fa-182">b.</span></span> <span data-ttu-id="794fa-183">Kliknij przycisk **punkty końcowe** tooopen **punkty końcowe** okno dialogowe.</span><span class="sxs-lookup"><span data-stu-id="794fa-183">Click **Endpoints** tooopen **Endpoints** dialog box.</span></span>  
    
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-jiramicrosoft-tutorial/endpointicon.png)

    <span data-ttu-id="794fa-185">c.</span><span class="sxs-lookup"><span data-stu-id="794fa-185">c.</span></span> <span data-ttu-id="794fa-186">Kliknij przycisk toocopy przycisku Kopiuj hello **dokument METADANYCH usług FEDERACYJNYCH** adresu url i wklej go do Notatnika.</span><span class="sxs-lookup"><span data-stu-id="794fa-186">Click hello copy button toocopy **FEDERATION METADATA DOCUMENT** url and paste it into notepad.</span></span>
    
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-jiramicrosoft-tutorial/endpoint.png)
     
    <span data-ttu-id="794fa-188">d.</span><span class="sxs-lookup"><span data-stu-id="794fa-188">d.</span></span> <span data-ttu-id="794fa-189">Teraz przejdź strony właściwości toohello **logowania jednokrotnego SAML JIRA przez firmę Microsoft** i hello kopiowania **identyfikator aplikacji** przy użyciu **kopiowania** przycisk i wklej go do Notatnika.</span><span class="sxs-lookup"><span data-stu-id="794fa-189">Now go toohello property page of **JIRA SAML SSO by Microsoft** and copy hello **Application Id** using **Copy** button and paste it into notepad.</span></span>
 
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-jiramicrosoft-tutorial/appid.png)

    <span data-ttu-id="794fa-191">e.</span><span class="sxs-lookup"><span data-stu-id="794fa-191">e.</span></span> <span data-ttu-id="794fa-192">Generowanie hello **adres URL metadanych** przy użyciu hello następującego wzorca: `<FEDERATION METADATA DOCUMENT url>?appid=<application id>` i skopiuj tę wartość w programie Notatnik, ponieważ jest później używany dla konfiguracji hello hello wtyczki.</span><span class="sxs-lookup"><span data-stu-id="794fa-192">Generate hello **Metadata URL** using hello following pattern: `<FEDERATION METADATA DOCUMENT url>?appid=<application id>` and copy this value in notepad as it is used later for hello configuration of hello plugin.</span></span>

5. <span data-ttu-id="794fa-193">Kliknij przycisk **zapisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="794fa-193">Click **Save** button.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-jiramicrosoft-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="794fa-195">Skontaktuj się z [Microsoft](mailto:waadpartners@microsoft.com) z następujących informacji dla wtyczki JIRA hello hello.</span><span class="sxs-lookup"><span data-stu-id="794fa-195">Contact [Microsoft](mailto:waadpartners@microsoft.com) with hello following information for hello JIRA plugin.</span></span>
    
    *   <span data-ttu-id="794fa-196">Nazwa klienta:</span><span class="sxs-lookup"><span data-stu-id="794fa-196">Customer Name:</span></span>
    *   <span data-ttu-id="794fa-197">Nazwa domeny głównej:</span><span class="sxs-lookup"><span data-stu-id="794fa-197">Primary domain name:</span></span>
    *   <span data-ttu-id="794fa-198">Azure AD Premium: Tak/nie (wtyczka będzie, dostępne tooall powitania klienta wolne, Basic i warstwy Premium)</span><span class="sxs-lookup"><span data-stu-id="794fa-198">Azure AD Premium: Yes/No (Plugin will be available tooall     hello customer Free, Basic, and Premium SKU)</span></span>
    *   <span data-ttu-id="794fa-199">Liczba użytkowników, którzy będą używać tej integracji:</span><span class="sxs-lookup"><span data-stu-id="794fa-199">Number of users who will be using this integration:</span></span>
    *   <span data-ttu-id="794fa-200">Wersja JIRA:</span><span class="sxs-lookup"><span data-stu-id="794fa-200">JIRA Version:</span></span>
    *   <span data-ttu-id="794fa-201">Uwagi:</span><span class="sxs-lookup"><span data-stu-id="794fa-201">Comments:</span></span>

7. <span data-ttu-id="794fa-202">W oknie przeglądarki innej witryny sieci web Zaloguj się w wystąpieniu JIRA tooyour jako administrator.</span><span class="sxs-lookup"><span data-stu-id="794fa-202">In a different web browser window, log in tooyour JIRA instance as an administrator.</span></span>

8. <span data-ttu-id="794fa-203">Umieść kursor na koło zębate, a następnie kliknij przycisk hello **dodatki**.</span><span class="sxs-lookup"><span data-stu-id="794fa-203">Hover on cog and click hello **Add-ons**.</span></span>
    
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-jiramicrosoft-tutorial/addon1.png)

9. <span data-ttu-id="794fa-205">W sekcji Karta dodatki, kliknij przycisk **Zarządzanie dodatkami**.</span><span class="sxs-lookup"><span data-stu-id="794fa-205">Under Add-ons tab section, click **Manage add-ons**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-jiramicrosoft-tutorial/addon7.png)

10. <span data-ttu-id="794fa-207">Ręcznie przekazać wtyczki hello obsługiwane przez firmę Microsoft.</span><span class="sxs-lookup"><span data-stu-id="794fa-207">Manually upload hello plugin provided by Microsoft.</span></span> <span data-ttu-id="794fa-208">Po zainstalowaniu dodatku hello pojawia się w **użytkownik zainstalował** sekcji dodatki **zarządzania dodatkami** sekcji.</span><span class="sxs-lookup"><span data-stu-id="794fa-208">Once hello plugin is installed, it appears in **User Installed** add-ons section of **Manage Add-on** section.</span></span>

11. <span data-ttu-id="794fa-209">Kliknij przycisk **Konfiguruj** tooconfigure hello nowej wtyczki.</span><span class="sxs-lookup"><span data-stu-id="794fa-209">Click **Configure** tooconfigure hello new plugin.</span></span>

12. <span data-ttu-id="794fa-210">Wykonaj następujące kroki na stronie konfiguracji:</span><span class="sxs-lookup"><span data-stu-id="794fa-210">Perform following steps on configuration page:</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-jiramicrosoft-tutorial/addon5.png)
 
    <span data-ttu-id="794fa-212">a.</span><span class="sxs-lookup"><span data-stu-id="794fa-212">a.</span></span> <span data-ttu-id="794fa-213">W **adres URL metadanych** Wklej hello **adres URL metadanych** generowane z usługi Azure AD i kliknij przycisk hello **rozwiązać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="794fa-213">In **Metadata URL** paste hello **Metadata URL** generated from Azure AD and click hello **Resolve** button.</span></span> <span data-ttu-id="794fa-214">Adres URL metadanych IdP hello odczytuje i wypełnienie wszystkich hello pól informacji.</span><span class="sxs-lookup"><span data-stu-id="794fa-214">It reads hello IdP metadata URL and populates all hello fields information.</span></span>

    > [!Note]
    > <span data-ttu-id="794fa-215">Domyślna lokalizacja SAML użytkownika identyfikator to identyfikator nazwy.</span><span class="sxs-lookup"><span data-stu-id="794fa-215">Default SAML User ID location is Name Identifier.</span></span> <span data-ttu-id="794fa-216">Można zmienić tej opcji atrybutu tooan i wprowadź nazwę atrybutu odpowiednie hello.</span><span class="sxs-lookup"><span data-stu-id="794fa-216">You can change this tooan attribute option and enter hello appropriate attribute name.</span></span>

    > [!TIP]
    > <span data-ttu-id="794fa-217">Upewnij się, że istnieje tylko jeden certyfikat mapowany aplikacji hello tak, aby nie było błędu rozpoznawania hello metadanych.</span><span class="sxs-lookup"><span data-stu-id="794fa-217">Ensure that there is only one certificate mapped against hello app so that there is no error in resolving hello metadata.</span></span> <span data-ttu-id="794fa-218">Jeśli dostępnych jest wiele certyfikatów na rozpoznawanie metadanych hello admin pobiera wystąpił błąd.</span><span class="sxs-lookup"><span data-stu-id="794fa-218">If there are multiple certificates, upon resolving hello metadata, admin gets an error.</span></span>
    
    <span data-ttu-id="794fa-219">b.</span><span class="sxs-lookup"><span data-stu-id="794fa-219">b.</span></span> <span data-ttu-id="794fa-220">Kopiuj hello **identyfikator, adres URL odpowiedzi i zaloguj się na adres URL** wartości i wklej je w **identyfikator, adres URL odpowiedzi i zaloguj się na adres URL** odpowiednio do pól tekstowych **logowania jednokrotnego SAML JIRA Domain firmy Microsoft i adresy URL** sekcji z portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="794fa-220">Copy hello **Identifier, Reply URL and Sign on URL** values and paste them in **Identifier, Reply URL and Sign on URL** textboxes respectively in **JIRA SAML SSO by Microsoft Domain and URLs** section on Azure portal.</span></span>

    <span data-ttu-id="794fa-221">c.</span><span class="sxs-lookup"><span data-stu-id="794fa-221">c.</span></span> <span data-ttu-id="794fa-222">W **nazwa przycisku logowania** nazwa hello typu przycisku organizacja chce hello toosee użytkowników na ekranie logowania.</span><span class="sxs-lookup"><span data-stu-id="794fa-222">In **Login Button Name** type hello name of button your organization wants hello users toosee on login screen.</span></span>

    <span data-ttu-id="794fa-223">d.</span><span class="sxs-lookup"><span data-stu-id="794fa-223">d.</span></span> <span data-ttu-id="794fa-224">W **lokalizacje identyfikator użytkownika SAML** wybierz opcję **identyfikator użytkownika jest w elemencie NameIdentifier hello hello instrukcji podmiotu** lub **identyfikator użytkownika jest w elemencie atrybutu**.</span><span class="sxs-lookup"><span data-stu-id="794fa-224">In **SAML User ID Locations** select either **User ID is in hello NameIdentifier element of hello Subject statement** or **User ID is in an Attribute element**.</span></span>  <span data-ttu-id="794fa-225">Ten identyfikator ma identyfikator użytkownika JIRA hello toobe. Jeśli hello identyfikator użytkownika nie jest zgodny, następnie systemu nie zezwala na toolog użytkowników w.</span><span class="sxs-lookup"><span data-stu-id="794fa-225">This ID has toobe hello JIRA user id. If hello user id is not matched, then system will not allow users toolog in.</span></span> 
    
    <span data-ttu-id="794fa-226">e.</span><span class="sxs-lookup"><span data-stu-id="794fa-226">e.</span></span> <span data-ttu-id="794fa-227">W przypadku wybrania **identyfikator użytkownika jest w elemencie atrybutu** opcji, a następnie w **nazwa atrybutu** pole tekstowe Nazwa hello typu atrybutu hello, gdzie jest oczekiwany identyfikator użytkownika.</span><span class="sxs-lookup"><span data-stu-id="794fa-227">If you select **User ID is in an Attribute element** option, then in **Attribute name** textbox type hello name of hello attribute where User Id is expected.</span></span> 

    <span data-ttu-id="794fa-228">f.</span><span class="sxs-lookup"><span data-stu-id="794fa-228">f.</span></span> <span data-ttu-id="794fa-229">Jeśli używasz hello domeny federacyjnej (na przykład usług AD FS itp.) z usługą Azure AD, należy kliknąć opcję hello **Włączanie odnajdowania obszaru macierzystego** opcji i skonfigurować hello **nazwy domeny**.</span><span class="sxs-lookup"><span data-stu-id="794fa-229">If you are using hello federated domain (like ADFS etc.) with Azure AD, then click on hello **Enable Home Realm Discovery** option and configure hello **Domain Name**.</span></span>
    
    <span data-ttu-id="794fa-230">g.</span><span class="sxs-lookup"><span data-stu-id="794fa-230">g.</span></span> <span data-ttu-id="794fa-231">W **nazwy domeny** hello domeny tym miejscu wpisz nazwę w przypadku logowania za pomocą usług AD FS hello.</span><span class="sxs-lookup"><span data-stu-id="794fa-231">In **Domain Name** type hello domain name here in case of hello ADFS-based login.</span></span>

    <span data-ttu-id="794fa-232">h.</span><span class="sxs-lookup"><span data-stu-id="794fa-232">h.</span></span> <span data-ttu-id="794fa-233">Sprawdź **włączyć pojedynczego Wyloguj** Jeśli chcesz toolog się z usługą Azure AD, gdy użytkownik zaloguje z JIRA.</span><span class="sxs-lookup"><span data-stu-id="794fa-233">Check **Enable Single Sign out** if you wish toolog out from Azure AD when a user logs out from JIRA.</span></span> 

    <span data-ttu-id="794fa-234">i.</span><span class="sxs-lookup"><span data-stu-id="794fa-234">i.</span></span> <span data-ttu-id="794fa-235">Kliknij przycisk **zapisać** przycisk toosave hello ustawienia.</span><span class="sxs-lookup"><span data-stu-id="794fa-235">Click **Save** button toosave hello settings.</span></span>

> [!TIP]
> <span data-ttu-id="794fa-236">Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz hello [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji hello!</span><span class="sxs-lookup"><span data-stu-id="794fa-236">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="794fa-237">Po dodaniu tej aplikacji z hello **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij hello **rejestracji jednokrotnej** hello kartę i dostępu do osadzonych dokumentacji za pośrednictwem hello  **Konfiguracja** sekcji u dołu hello.</span><span class="sxs-lookup"><span data-stu-id="794fa-237">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="794fa-238">Więcej o hello osadzonych dokumentacji funkcji w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="794fa-238">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="794fa-239">Tworzenie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="794fa-239">Creating an Azure AD test user</span></span>
<span data-ttu-id="794fa-240">Celem Hello w tej sekcji jest toocreate użytkownika testowego, w portalu Azure o nazwie Simona Britta hello.</span><span class="sxs-lookup"><span data-stu-id="794fa-240">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Tworzenie użytkowników usługi Azure AD][100]

<span data-ttu-id="794fa-242">**toocreate użytkownika testowego w usłudze Azure AD, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="794fa-242">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="794fa-243">W hello **portalu Azure**na temat hello w lewym okienku nawigacji, kliknij przycisk **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="794fa-243">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-jiramicrosoft-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="794fa-245">toodisplay hello listę użytkowników, przejdź zbyt**użytkowników i grup** i kliknij przycisk **wszyscy użytkownicy**.</span><span class="sxs-lookup"><span data-stu-id="794fa-245">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-jiramicrosoft-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="794fa-247">Witaj tooopen **użytkownika** okna dialogowego, kliknij przycisk **Dodaj** u góry hello hello okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="794fa-247">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-jiramicrosoft-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="794fa-249">Na powitania **użytkownika** okna dialogowego wykonaj hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="794fa-249">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-jiramicrosoft-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="794fa-251">a.</span><span class="sxs-lookup"><span data-stu-id="794fa-251">a.</span></span> <span data-ttu-id="794fa-252">W hello **nazwa** pole tekstowe, typ **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="794fa-252">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="794fa-253">b.</span><span class="sxs-lookup"><span data-stu-id="794fa-253">b.</span></span> <span data-ttu-id="794fa-254">W hello **nazwy użytkownika** pole tekstowe, hello typu **adres e-mail** z BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="794fa-254">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="794fa-255">c.</span><span class="sxs-lookup"><span data-stu-id="794fa-255">c.</span></span> <span data-ttu-id="794fa-256">Wybierz **Pokaż hasło** i zanotuj wartość hello hello **hasło**.</span><span class="sxs-lookup"><span data-stu-id="794fa-256">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="794fa-257">d.</span><span class="sxs-lookup"><span data-stu-id="794fa-257">d.</span></span> <span data-ttu-id="794fa-258">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="794fa-258">Click **Create**.</span></span>
 
### <a name="creating-a-jira-saml-sso-by-microsoft-test-user"></a><span data-ttu-id="794fa-259">Tworzenie logowania jednokrotnego SAML JIRA przez użytkownika testowego firmy Microsoft</span><span class="sxs-lookup"><span data-stu-id="794fa-259">Creating a JIRA SAML SSO by Microsoft test user</span></span>

<span data-ttu-id="794fa-260">toolog użytkowników tooenable usługi Azure AD w tooJIRA na serwerze lokalnym, ich muszą mieć przydzielone do logowania jednokrotnego SAML JIRA przez firmę Microsoft.</span><span class="sxs-lookup"><span data-stu-id="794fa-260">tooenable Azure AD users toolog in tooJIRA on-premise server, they must be provisioned into JIRA SAML SSO by Microsoft.</span></span> <span data-ttu-id="794fa-261">W przypadku logowania jednokrotnego SAML JIRA przez firmę Microsoft inicjowania obsługi administracyjnej jest zadanie ręczne.</span><span class="sxs-lookup"><span data-stu-id="794fa-261">For JIRA SAML SSO by Microsoft, provisioning is a manual task.</span></span>

<span data-ttu-id="794fa-262">**tooprovision konta użytkownika, należy wykonać hello następujące kroki:**</span><span class="sxs-lookup"><span data-stu-id="794fa-262">**tooprovision a user account, perform hello following steps:**</span></span>

1. <span data-ttu-id="794fa-263">Zaloguj się za tooyour JIRA na lokalnym serwerze jako administrator.</span><span class="sxs-lookup"><span data-stu-id="794fa-263">Log in tooyour JIRA on-premise server as an administrator.</span></span>

2. <span data-ttu-id="794fa-264">Umieść kursor na koło zębate, a następnie kliknij przycisk hello **Zarządzanie użytkownikami**.</span><span class="sxs-lookup"><span data-stu-id="794fa-264">Hover on cog and click hello **User management**.</span></span>

    ![Dodawanie pracownika](./media/active-directory-saas-jiramicrosoft-tutorial/user1.png) 

3. <span data-ttu-id="794fa-266">Jesteś tooenter stronę dostępu do przekierowanych tooAdministrator **hasła** i kliknij przycisk **Potwierdź** przycisku.</span><span class="sxs-lookup"><span data-stu-id="794fa-266">You are redirected tooAdministrator Access page tooenter **Password** and click **Confirm** button.</span></span>

    ![Dodawanie pracownika](./media/active-directory-saas-jiramicrosoft-tutorial/user2.png) 

4. <span data-ttu-id="794fa-268">W obszarze **Zarządzanie użytkownikami** sekcji, kliknij pozycję **Utwórz użytkownika**.</span><span class="sxs-lookup"><span data-stu-id="794fa-268">Under **User management** tab section, click **create user**.</span></span>

    ![Dodawanie pracownika](./media/active-directory-saas-jiramicrosoft-tutorial/user3.png) 

5. <span data-ttu-id="794fa-270">Na powitania **"Tworzenie nowego użytkownika"** okna dialogowego wykonaj hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="794fa-270">On hello **“Create new user”** dialog page, perform hello following steps:</span></span>

    ![Dodawanie pracownika](./media/active-directory-saas-jiramicrosoft-tutorial/user4.png) 

    <span data-ttu-id="794fa-272">a.</span><span class="sxs-lookup"><span data-stu-id="794fa-272">a.</span></span> <span data-ttu-id="794fa-273">W hello **adres E-mail** pole tekstowe, typ hello adres e-mail użytkownika, takich jak Brittasimon@contoso.com.</span><span class="sxs-lookup"><span data-stu-id="794fa-273">In hello **Email address** textbox, type hello email address of user like Brittasimon@contoso.com.</span></span>

    <span data-ttu-id="794fa-274">b.</span><span class="sxs-lookup"><span data-stu-id="794fa-274">b.</span></span> <span data-ttu-id="794fa-275">W hello **imię i nazwisko** tekstowym, wpisz pełną nazwę użytkownika hello jak Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="794fa-275">In hello **Full Name** textbox, type full name of hello user like Britta Simon.</span></span>

    <span data-ttu-id="794fa-276">c.</span><span class="sxs-lookup"><span data-stu-id="794fa-276">c.</span></span> <span data-ttu-id="794fa-277">W hello **Username** pole tekstowe, powitalne wiadomości e-mail użytkownika, takich jak Brittasimon@contoso.com.</span><span class="sxs-lookup"><span data-stu-id="794fa-277">In hello **Username** textbox, type hello email of user like Brittasimon@contoso.com.</span></span>

    <span data-ttu-id="794fa-278">d.</span><span class="sxs-lookup"><span data-stu-id="794fa-278">d.</span></span> <span data-ttu-id="794fa-279">W hello **hasło** tekstowym, wpisz hello hasło użytkownika.</span><span class="sxs-lookup"><span data-stu-id="794fa-279">In hello **Password** textbox, type hello password of user.</span></span>

    <span data-ttu-id="794fa-280">e.</span><span class="sxs-lookup"><span data-stu-id="794fa-280">e.</span></span> <span data-ttu-id="794fa-281">Kliknij przycisk **tworzenia użytkownika**.</span><span class="sxs-lookup"><span data-stu-id="794fa-281">Click **Create user**.</span></span>   

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="794fa-282">Przypisanie użytkownika testowego hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="794fa-282">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="794fa-283">W tej sekcji możesz włączyć toouse Simona Britta Azure logowania jednokrotnego za udzielanie dostępu tooJIRA logowania jednokrotnego SAML przez firmę Microsoft.</span><span class="sxs-lookup"><span data-stu-id="794fa-283">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooJIRA SAML SSO by Microsoft.</span></span>

![Przypisz użytkownika][200] 

<span data-ttu-id="794fa-285">**tooassign tooJIRA Simona Britta logowania jednokrotnego SAML przez firmę Microsoft, należy wykonać hello następujące kroki:**</span><span class="sxs-lookup"><span data-stu-id="794fa-285">**tooassign Britta Simon tooJIRA SAML SSO by Microsoft, perform hello following steps:**</span></span>

1. <span data-ttu-id="794fa-286">W portalu Azure hello, otwórz widok aplikacji hello, a następnie przejdź do widoku katalogu toohello i przejść za**aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="794fa-286">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Przypisz użytkownika][201] 

2. <span data-ttu-id="794fa-288">Z listy aplikacji hello wybierz **logowania jednokrotnego SAML JIRA przez firmę Microsoft**.</span><span class="sxs-lookup"><span data-stu-id="794fa-288">In hello applications list, select **JIRA SAML SSO by Microsoft**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-jiramicrosoft-tutorial/tutorial_jiramicrosoft_app.png) 

3. <span data-ttu-id="794fa-290">W menu powitania po lewej stronie powitania kliknij **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="794fa-290">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Przypisz użytkownika][202] 

4. <span data-ttu-id="794fa-292">Kliknij przycisk **Dodaj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="794fa-292">Click **Add** button.</span></span> <span data-ttu-id="794fa-293">Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="794fa-293">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Przypisz użytkownika][203]

5. <span data-ttu-id="794fa-295">Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** hello listy użytkowników.</span><span class="sxs-lookup"><span data-stu-id="794fa-295">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="794fa-296">Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="794fa-296">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="794fa-297">Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="794fa-297">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="794fa-298">Testowanie rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="794fa-298">Testing single sign-on</span></span>

<span data-ttu-id="794fa-299">W tej sekcji można przetestować konfiguracji usługi Azure AD pojedynczego logowania jednokrotnego przy użyciu hello panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="794fa-299">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="794fa-300">Po kliknięciu hello logowania jednokrotnego SAML JIRA przez Microsoft kafelka w hello Panel dostępu, należy pobrać automatycznie zalogowane tooyour logowania jednokrotnego SAML JIRA przez aplikację Microsoft.</span><span class="sxs-lookup"><span data-stu-id="794fa-300">When you click hello JIRA SAML SSO by Microsoft tile in hello Access Panel, you should get automatically signed-on tooyour JIRA SAML SSO by Microsoft application.</span></span>
<span data-ttu-id="794fa-301">Aby uzyskać więcej informacji na temat hello Panel dostępu, zobacz [toohello wprowadzenie panelu dostępu](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="794fa-301">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="794fa-302">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="794fa-302">Additional resources</span></span>

* [<span data-ttu-id="794fa-303">Lista samouczków dotyczących tooIntegrate aplikacji SaaS w usłudze Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="794fa-303">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="794fa-304">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="794fa-304">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-jiramicrosoft-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-jiramicrosoft-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-jiramicrosoft-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-jiramicrosoft-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-jiramicrosoft-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-jiramicrosoft-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-jiramicrosoft-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-jiramicrosoft-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-jiramicrosoft-tutorial/tutorial_general_203.png

