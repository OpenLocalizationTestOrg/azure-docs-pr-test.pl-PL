---
title: "Samouczek: Integracji Azure Active Directory z logowania jednokrotnego SAML zlewiska przez firmę Microsoft | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak tooconfigure logowanie jednokrotne między usługą Azure Active Directory i logowania jednokrotnego SAML zlewiska przez firmę Microsoft."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 1ad1cf90-52bc-4b71-ab2b-9a5a1280fb2d
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/19/2017
ms.author: jeedes
ms.openlocfilehash: ace23800e3908c8125052b4a2edcaae71f19935d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-confluence-saml-sso-by-microsoft"></a><span data-ttu-id="38eb5-103">Samouczek: Integracji Azure Active Directory z logowania jednokrotnego SAML zlewiska przez firmę Microsoft</span><span class="sxs-lookup"><span data-stu-id="38eb5-103">Tutorial: Azure Active Directory integration with Confluence SAML SSO by Microsoft</span></span>

<span data-ttu-id="38eb5-104">Z tego samouczka, dowiesz się, jak toointegrate logowania jednokrotnego SAML zlewiska przez firmę Microsoft w usłudze Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="38eb5-104">In this tutorial, you learn how toointegrate Confluence SAML SSO by Microsoft with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="38eb5-105">Integracja z usługą Azure AD logowania jednokrotnego SAML zlewiska przez firmę Microsoft udostępnia hello następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="38eb5-105">Integrating Confluence SAML SSO by Microsoft with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="38eb5-106">Można kontrolować w usłudze Azure AD, kto ma dostęp do tooConfluence logowania jednokrotnego SAML przez firmę Microsoft</span><span class="sxs-lookup"><span data-stu-id="38eb5-106">You can control in Azure AD who has access tooConfluence SAML SSO by Microsoft</span></span>
- <span data-ttu-id="38eb5-107">Można włączyć użytkownika użytkownicy tooautomatically get zalogowane tooConfluence logowania jednokrotnego SAML przez firmę Microsoft (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="38eb5-107">You can enable your users tooautomatically get signed-on tooConfluence SAML SSO by Microsoft (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="38eb5-108">Możesz zarządzać kont w jednej centralnej lokalizacji - hello portalu Azure</span><span class="sxs-lookup"><span data-stu-id="38eb5-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="38eb5-109">Jeśli chcesz tooknow więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="38eb5-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="38eb5-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="38eb5-110">Prerequisites</span></span>

<span data-ttu-id="38eb5-111">tooconfigure integracji z usługą Azure AD z logowania jednokrotnego SAML zlewiska przez firmę Microsoft, należy hello następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="38eb5-111">tooconfigure Azure AD integration with Confluence SAML SSO by Microsoft, you need hello following items:</span></span>

- <span data-ttu-id="38eb5-112">Subskrypcję usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="38eb5-112">An Azure AD subscription</span></span>
- <span data-ttu-id="38eb5-113">Aplikacja serwera zlewiska zainstalowany na serwerze Windows 64-bitowych (lokalnie lub w chmurze hello infrastrukturą IaaS)</span><span class="sxs-lookup"><span data-stu-id="38eb5-113">Confluence server application installed on a Windows 64-bit server (on premise or on hello cloud IaaS infrastructure)</span></span>
- <span data-ttu-id="38eb5-114">Serwer zlewiska jest obsługujące protokół HTTPS</span><span class="sxs-lookup"><span data-stu-id="38eb5-114">Confluence server is HTTPS enabled</span></span>
- <span data-ttu-id="38eb5-115">Uwaga hello obsługiwane wersje dla wtyczki zlewiska są wymienione w poniższej sekcji.</span><span class="sxs-lookup"><span data-stu-id="38eb5-115">Note hello supported versions for Confluence Plugin are mentioned in below section.</span></span>
- <span data-ttu-id="38eb5-116">Zlewiska serwer jest dostępny w Internecie szczególnie tooAzure dla uwierzytelniania strony logowania usługi AD i powinien tooreceive stanie hello tokenu z usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="38eb5-116">Confluence server is reachable on internet particularly tooAzure AD Login page for authentication and should able tooreceive hello token from Azure AD</span></span>
- <span data-ttu-id="38eb5-117">Poświadczenia administratora są konfigurowane w zlewiska</span><span class="sxs-lookup"><span data-stu-id="38eb5-117">Admin credentials are set up in Confluence</span></span>
- <span data-ttu-id="38eb5-118">WebSudo jest wyłączona w zlewiska</span><span class="sxs-lookup"><span data-stu-id="38eb5-118">WebSudo is disabled in Confluence</span></span>
- <span data-ttu-id="38eb5-119">Testowanie użytkowników utworzone w hello zlewiska serwera aplikacji</span><span class="sxs-lookup"><span data-stu-id="38eb5-119">Test user created in hello Confluence server application</span></span>

> [!NOTE]
> <span data-ttu-id="38eb5-120">tootest hello kroków w tym samouczku, zaleca się przy użyciu środowiska produkcyjnego programu zlewiska.</span><span class="sxs-lookup"><span data-stu-id="38eb5-120">tootest hello steps in this tutorial, we do not recommend using a production environment of Confluence.</span></span> <span data-ttu-id="38eb5-121">Testowanie integracji hello najpierw w rozwoju lub przemieszczania środowisko aplikacji hello, a następnie środowiska produkcyjnego hello użycia.</span><span class="sxs-lookup"><span data-stu-id="38eb5-121">Test hello integration first in development or staging environment of hello application and then use hello production environment.</span></span>

<span data-ttu-id="38eb5-122">tootest hello kroki opisane w tym samouczku, należy stosować te zalecenia:</span><span class="sxs-lookup"><span data-stu-id="38eb5-122">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="38eb5-123">Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="38eb5-123">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="38eb5-124">Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz pobrać miesięczna wersja próbna tutaj: [oferta wersji próbnej](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="38eb5-124">If you don't have an Azure AD trial environment, you can get a one-month trial here: [Trial offer](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="supported-versions-of-confluence"></a><span data-ttu-id="38eb5-125">Obsługiwane wersje zlewiska</span><span class="sxs-lookup"><span data-stu-id="38eb5-125">Supported versions of Confluence</span></span> 

<span data-ttu-id="38eb5-126">Od tej chwili obsługiwane są następujące wersje zlewiska:</span><span class="sxs-lookup"><span data-stu-id="38eb5-126">As of now, following versions of Confluence are supported:</span></span>

- <span data-ttu-id="38eb5-127">Zlewiska: too5.10 5.0</span><span class="sxs-lookup"><span data-stu-id="38eb5-127">Confluence: 5.0 too5.10</span></span>

## <a name="scenario-description"></a><span data-ttu-id="38eb5-128">Opis scenariusza</span><span class="sxs-lookup"><span data-stu-id="38eb5-128">Scenario description</span></span>
<span data-ttu-id="38eb5-129">W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym.</span><span class="sxs-lookup"><span data-stu-id="38eb5-129">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="38eb5-130">Scenariusz Hello opisane w tym samouczku składa się z dwóch głównych elementów:</span><span class="sxs-lookup"><span data-stu-id="38eb5-130">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="38eb5-131">Dodawanie z galerii hello logowania jednokrotnego SAML zlewiska przez firmę Microsoft</span><span class="sxs-lookup"><span data-stu-id="38eb5-131">Adding Confluence SAML SSO by Microsoft from hello gallery</span></span>
2. <span data-ttu-id="38eb5-132">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="38eb5-132">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-confluence-saml-sso-by-microsoft-from-hello-gallery"></a><span data-ttu-id="38eb5-133">Dodawanie z galerii hello logowania jednokrotnego SAML zlewiska przez firmę Microsoft</span><span class="sxs-lookup"><span data-stu-id="38eb5-133">Adding Confluence SAML SSO by Microsoft from hello gallery</span></span>
<span data-ttu-id="38eb5-134">tooconfigure hello włączenia logowania jednokrotnego SAML zlewiska przez firmę Microsoft do usługi Azure AD, należy tooadd logowania jednokrotnego SAML zlewiska przez firmę Microsoft z hello galerii tooyour listę zarządzanych aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="38eb5-134">tooconfigure hello integration of Confluence SAML SSO by Microsoft into Azure AD, you need tooadd Confluence SAML SSO by Microsoft from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="38eb5-135">**tooadd logowania jednokrotnego SAML zlewiska przez firmę Microsoft z galerii hello wykonaj hello następujące kroki:**</span><span class="sxs-lookup"><span data-stu-id="38eb5-135">**tooadd Confluence SAML SSO by Microsoft from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="38eb5-136">W hello  **[portalu Azure](https://portal.azure.com)**na temat hello panelu nawigacji po lewej stronie, kliknij przycisk **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="38eb5-136">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Usługa Active Directory][1]

2. <span data-ttu-id="38eb5-138">Przejdź za**aplikacje dla przedsiębiorstw**.</span><span class="sxs-lookup"><span data-stu-id="38eb5-138">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="38eb5-139">Następnie przejdź zbyt**wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="38eb5-139">Then go too**All applications**.</span></span>

    ![Aplikacje][2]
    
3. <span data-ttu-id="38eb5-141">tooadd nową aplikację, kliknij przycisk **nowej aplikacji** przycisk u góry hello okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="38eb5-141">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplikacje][3]

4. <span data-ttu-id="38eb5-143">W polu wyszukiwania hello wpisz **logowania jednokrotnego SAML zlewiska przez firmę Microsoft**.</span><span class="sxs-lookup"><span data-stu-id="38eb5-143">In hello search box, type **Confluence SAML SSO by Microsoft**.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-confluencemicrosoft-tutorial/tutorial_confluencemicrosoft_search.png)

5. <span data-ttu-id="38eb5-145">W panelu wyników hello, wybierz **logowania jednokrotnego SAML zlewiska przez firmę Microsoft**, a następnie kliknij przycisk **Dodaj** przycisk tooadd hello aplikacji.</span><span class="sxs-lookup"><span data-stu-id="38eb5-145">In hello results panel, select **Confluence SAML SSO by Microsoft**, and then click **Add** button tooadd hello application.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-confluencemicrosoft-tutorial/tutorial_confluencemicrosoft_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="38eb5-147">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="38eb5-147">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="38eb5-148">W tej sekcji skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z logowania jednokrotnego SAML zlewiska przez firmę Microsoft, w oparciu o nazwie "Britta Simona" użytkownika testowego.</span><span class="sxs-lookup"><span data-stu-id="38eb5-148">In this section, you configure and test Azure AD single sign-on with Confluence SAML SSO by Microsoft based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="38eb5-149">Dla pojedynczego logowania jednokrotnego toowork usługi Azure AD musi tooknow użytkownika odpowiednikiem hello w logowania jednokrotnego SAML zlewiska przez firmę Microsoft jest tooa użytkownika w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="38eb5-149">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Confluence SAML SSO by Microsoft is tooa user in Azure AD.</span></span> <span data-ttu-id="38eb5-150">Innymi słowy łącze relację między użytkownika usługi Azure AD i powiązane użytkownika logowania jednokrotnego SAML zlewiska przez firmę Microsoft hello musi toobe ustanowione.</span><span class="sxs-lookup"><span data-stu-id="38eb5-150">In other words, a link relationship between an Azure AD user and hello related user in Confluence SAML SSO by Microsoft needs toobe established.</span></span>

<span data-ttu-id="38eb5-151">W logowania jednokrotnego SAML zlewiska przez firmę Microsoft, należy przypisać wartość hello hello **nazwy użytkownika** w usłudze Azure AD jako wartość hello hello **Username** tooestablish hello łącze relacji.</span><span class="sxs-lookup"><span data-stu-id="38eb5-151">In Confluence SAML SSO by Microsoft, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="38eb5-152">tooconfigure i testowych usługi Azure AD rejestracji jednokrotnej z logowania jednokrotnego SAML zlewiska przez firmę Microsoft, należy po bloków konstrukcyjnych hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="38eb5-152">tooconfigure and test Azure AD single sign-on with Confluence SAML SSO by Microsoft, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="38eb5-153">**[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configuring-azure-ad-single-sign-on)**  -tooenable Twojego toouse użytkowników tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="38eb5-153">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="38eb5-154">**[Tworzenie użytkownika testowego usługi Azure AD](#creating-an-azure-ad-test-user)**  -tootest usługi Azure AD rejestracji jednokrotnej z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="38eb5-154">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="38eb5-155">**[Tworzenie logowania jednokrotnego SAML zlewiska przez użytkownika testowego Microsoft](#creating-a-confluence-saml-sso-by-microsoft-test-user)**  -toohave odpowiednikiem Simona Britta w logowania jednokrotnego SAML zlewiska przez firmę Microsoft, który jest połączony toohello usługi Azure AD reprezentację użytkownika.</span><span class="sxs-lookup"><span data-stu-id="38eb5-155">**[Creating a Confluence SAML SSO by Microsoft test user](#creating-a-confluence-saml-sso-by-microsoft-test-user)** - toohave a counterpart of Britta Simon in Confluence SAML SSO by Microsoft that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="38eb5-156">**[Przypisanie użytkownika testowego hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Simona Britta toouse usługi Azure AD rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="38eb5-156">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="38eb5-157">**[Testowanie rejestracji jednokrotnej](#testing-single-sign-on)**  -tooverify czy hello konfiguracji działania.</span><span class="sxs-lookup"><span data-stu-id="38eb5-157">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="38eb5-158">Konfigurowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="38eb5-158">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="38eb5-159">W tej sekcji włączyć usługi Azure AD rejestracji jednokrotnej w hello portalu Azure i skonfigurować logowanie jednokrotne w sieci logowania jednokrotnego SAML zlewiska przez aplikację Microsoft.</span><span class="sxs-lookup"><span data-stu-id="38eb5-159">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Confluence SAML SSO by Microsoft application.</span></span>

<span data-ttu-id="38eb5-160">**tooconfigure usługi Azure AD rejestracji jednokrotnej z logowania jednokrotnego SAML zlewiska przez firmę Microsoft, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="38eb5-160">**tooconfigure Azure AD single sign-on with Confluence SAML SSO by Microsoft, perform hello following steps:**</span></span>

1. <span data-ttu-id="38eb5-161">W portalu Azure na powitania hello **logowania jednokrotnego SAML zlewiska przez firmę Microsoft** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.</span><span class="sxs-lookup"><span data-stu-id="38eb5-161">In hello Azure portal, on hello **Confluence SAML SSO by Microsoft** application integration page, click **Single sign-on**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej][4]

2. <span data-ttu-id="38eb5-163">Na powitania **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** tooenable rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="38eb5-163">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-confluencemicrosoft-tutorial/tutorial_confluencemicrosoft_samlbase.png)

3. <span data-ttu-id="38eb5-165">Na powitania **logowania jednokrotnego SAML zlewiska Domain firmy Microsoft i adresy URL** sekcji, wykonaj następujące kroki hello:</span><span class="sxs-lookup"><span data-stu-id="38eb5-165">On hello **Confluence SAML SSO by Microsoft Domain and URLs** section, perform hello following steps:</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-confluencemicrosoft-tutorial/tutorial_confluencemicrosoft_url.png)

    <span data-ttu-id="38eb5-167">a.</span><span class="sxs-lookup"><span data-stu-id="38eb5-167">a.</span></span> <span data-ttu-id="38eb5-168">W hello **adres URL logowania** tekstowym, wpisz adres URL za pomocą hello następującego wzorca:`https://<domain:port>/plugins/servlet/saml/auth`</span><span class="sxs-lookup"><span data-stu-id="38eb5-168">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<domain:port>/plugins/servlet/saml/auth`</span></span>

    <span data-ttu-id="38eb5-169">b.</span><span class="sxs-lookup"><span data-stu-id="38eb5-169">b.</span></span> <span data-ttu-id="38eb5-170">W hello **identyfikator** tekstowym, wpisz adres URL za pomocą hello następującego wzorca:`https://<domain:port>/`</span><span class="sxs-lookup"><span data-stu-id="38eb5-170">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<domain:port>/`</span></span>

    <span data-ttu-id="38eb5-171">c.</span><span class="sxs-lookup"><span data-stu-id="38eb5-171">c.</span></span> <span data-ttu-id="38eb5-172">W hello **adres URL odpowiedzi** tekstowym, wpisz adres URL za pomocą hello następującego wzorca:`https://<domain:port>/plugins/servlet/saml/auth`</span><span class="sxs-lookup"><span data-stu-id="38eb5-172">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://<domain:port>/plugins/servlet/saml/auth`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="38eb5-173">Wartości te nie są prawdziwe.</span><span class="sxs-lookup"><span data-stu-id="38eb5-173">These values are not real.</span></span> <span data-ttu-id="38eb5-174">Zaktualizować te wartości z hello rzeczywisty identyfikator, adres URL odpowiedzi i adres URL logowania.</span><span class="sxs-lookup"><span data-stu-id="38eb5-174">Update these values with hello actual Identifier, Reply URL, and Sign-On URL.</span></span> <span data-ttu-id="38eb5-175">Port jest opcjonalny w przypadku, gdy jest nazwane adres URL.</span><span class="sxs-lookup"><span data-stu-id="38eb5-175">Port is optional in case it’s a named URL.</span></span> <span data-ttu-id="38eb5-176">Te wartości są odbierane podczas konfigurowania hello zlewiska wtyczki, który znajduje się w dalszej części samouczka hello.</span><span class="sxs-lookup"><span data-stu-id="38eb5-176">These values are received during hello configuration of Confluence plugin, which is explained later in hello tutorial.</span></span>
 

4. <span data-ttu-id="38eb5-177">Witaj toogenerate **metadanych** adres url, wykonaj następujące kroki hello:</span><span class="sxs-lookup"><span data-stu-id="38eb5-177">toogenerate hello **Metadata** url, perform hello following steps:</span></span>

    <span data-ttu-id="38eb5-178">a.</span><span class="sxs-lookup"><span data-stu-id="38eb5-178">a.</span></span> <span data-ttu-id="38eb5-179">Kliknij przycisk **rejestracji aplikacji**.</span><span class="sxs-lookup"><span data-stu-id="38eb5-179">Click **App registrations**.</span></span>
    
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-Confluencemicrosoft-tutorial/appregistrations.png)
   
    <span data-ttu-id="38eb5-181">b.</span><span class="sxs-lookup"><span data-stu-id="38eb5-181">b.</span></span> <span data-ttu-id="38eb5-182">Kliknij przycisk **punkty końcowe** tooopen **punkty końcowe** okno dialogowe.</span><span class="sxs-lookup"><span data-stu-id="38eb5-182">Click **Endpoints** tooopen **Endpoints** dialog box.</span></span>  
    
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-Confluencemicrosoft-tutorial/endpointicon.png)

    <span data-ttu-id="38eb5-184">c.</span><span class="sxs-lookup"><span data-stu-id="38eb5-184">c.</span></span> <span data-ttu-id="38eb5-185">Kliknij przycisk toocopy przycisku Kopiuj hello **dokument METADANYCH usług FEDERACYJNYCH** adresu url i wklej go do Notatnika.</span><span class="sxs-lookup"><span data-stu-id="38eb5-185">Click hello copy button toocopy **FEDERATION METADATA DOCUMENT** url and paste it into notepad.</span></span>
    
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-Confluencemicrosoft-tutorial/endpoint.png)
     
    <span data-ttu-id="38eb5-187">d.</span><span class="sxs-lookup"><span data-stu-id="38eb5-187">d.</span></span> <span data-ttu-id="38eb5-188">Teraz przejdź strony właściwości toohello **logowania jednokrotnego SAML zlewiska przez firmę Microsoft** i hello kopiowania **identyfikator aplikacji** przy użyciu **kopiowania** przycisk i wklej go do Notatnika.</span><span class="sxs-lookup"><span data-stu-id="38eb5-188">Now go toohello property page of **Confluence SAML SSO by Microsoft** and copy hello **Application Id** using **Copy** button and paste it into notepad.</span></span>
 
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-Confluencemicrosoft-tutorial/appid.png)

    <span data-ttu-id="38eb5-190">e.</span><span class="sxs-lookup"><span data-stu-id="38eb5-190">e.</span></span> <span data-ttu-id="38eb5-191">Generowanie hello **adres URL metadanych** przy użyciu hello następującego wzorca: `<FEDERATION METADATA DOCUMENT url>?appid=<application id>` i skopiuj tę wartość w programie Notatnik, ponieważ jest później używany dla konfiguracji hello hello wtyczki.</span><span class="sxs-lookup"><span data-stu-id="38eb5-191">Generate hello **Metadata URL** using hello following pattern: `<FEDERATION METADATA DOCUMENT url>?appid=<application id>` and copy this value in notepad as it is used later for hello configuration of hello plugin.</span></span>

5. <span data-ttu-id="38eb5-192">Kliknij przycisk **zapisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="38eb5-192">Click **Save** button.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-Confluencemicrosoft-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="38eb5-194">Skontaktuj się z [Microsoft](mailto:waadpartners@microsoft.com) z następujących informacji dla wtyczki zlewiska hello hello.</span><span class="sxs-lookup"><span data-stu-id="38eb5-194">Contact [Microsoft](mailto:waadpartners@microsoft.com) with hello following information for hello Confluence plugin.</span></span>
    
    *   <span data-ttu-id="38eb5-195">Nazwa klienta:</span><span class="sxs-lookup"><span data-stu-id="38eb5-195">Customer Name:</span></span>
    *   <span data-ttu-id="38eb5-196">Nazwa domeny głównej:</span><span class="sxs-lookup"><span data-stu-id="38eb5-196">Primary domain name:</span></span>
    *   <span data-ttu-id="38eb5-197">Azure AD Premium: Tak/nie (wtyczka będzie, dostępne tooall powitania klienta wolne, Basic i warstwy Premium)</span><span class="sxs-lookup"><span data-stu-id="38eb5-197">Azure AD Premium: Yes/No (Plugin will be available tooall     hello customer Free, Basic, and Premium SKU)</span></span>
    *   <span data-ttu-id="38eb5-198">Liczba użytkowników, którzy będą używać tej integracji:</span><span class="sxs-lookup"><span data-stu-id="38eb5-198">Number of users who will be using this integration:</span></span>
    *   <span data-ttu-id="38eb5-199">Wersja zlewiska:</span><span class="sxs-lookup"><span data-stu-id="38eb5-199">Confluence Version:</span></span>
    *   <span data-ttu-id="38eb5-200">Uwagi:</span><span class="sxs-lookup"><span data-stu-id="38eb5-200">Comments:</span></span>

7. <span data-ttu-id="38eb5-201">W oknie przeglądarki innej witryny sieci web Zaloguj się w wystąpieniu zlewiska tooyour jako administrator.</span><span class="sxs-lookup"><span data-stu-id="38eb5-201">In a different web browser window, log in tooyour Confluence instance as an administrator.</span></span>

8. <span data-ttu-id="38eb5-202">Umieść kursor na koło zębate, a następnie kliknij przycisk hello **dodatki**.</span><span class="sxs-lookup"><span data-stu-id="38eb5-202">Hover on cog and click hello **Add-ons**.</span></span>
    
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-Confluencemicrosoft-tutorial/addon1.png)

9. <span data-ttu-id="38eb5-204">W sekcji Karta dodatki, kliknij przycisk **Zarządzanie dodatkami**.</span><span class="sxs-lookup"><span data-stu-id="38eb5-204">Under Add-ons tab section, click **Manage add-ons**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-Confluencemicrosoft-tutorial/addon72.png)

10. <span data-ttu-id="38eb5-206">Ręcznie przekazać wtyczki hello obsługiwane przez firmę Microsoft.</span><span class="sxs-lookup"><span data-stu-id="38eb5-206">Manually upload hello plugin provided by Microsoft.</span></span> <span data-ttu-id="38eb5-207">Po zainstalowaniu dodatku hello pojawia się w **użytkownik zainstalował** sekcji dodatki **zarządzania dodatkami** sekcji.</span><span class="sxs-lookup"><span data-stu-id="38eb5-207">Once hello plugin is installed, it appears in **User Installed** add-ons section of **Manage Add-on** section.</span></span>

11. <span data-ttu-id="38eb5-208">Kliknij przycisk **Konfiguruj** tooconfigure hello nowej wtyczki.</span><span class="sxs-lookup"><span data-stu-id="38eb5-208">Click **Configure** tooconfigure hello new plugin.</span></span>

12. <span data-ttu-id="38eb5-209">Wykonaj następujące kroki na stronie konfiguracji:</span><span class="sxs-lookup"><span data-stu-id="38eb5-209">Perform following steps on configuration page:</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-Confluencemicrosoft-tutorial/addon5.png)
 
    <span data-ttu-id="38eb5-211">a.</span><span class="sxs-lookup"><span data-stu-id="38eb5-211">a.</span></span> <span data-ttu-id="38eb5-212">W **adres URL metadanych** Wklej hello **adres URL metadanych** generowane z usługi Azure AD i kliknij przycisk hello **rozwiązać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="38eb5-212">In **Metadata URL** paste hello **Metadata URL** generated from Azure AD and click hello **Resolve** button.</span></span> <span data-ttu-id="38eb5-213">Adres URL metadanych IdP hello odczytuje i wypełnienie wszystkich hello pól informacji.</span><span class="sxs-lookup"><span data-stu-id="38eb5-213">It reads hello IdP metadata URL and populates all hello fields information.</span></span>

    > [!Note]
    > <span data-ttu-id="38eb5-214">Domyślna lokalizacja SAML użytkownika identyfikator to identyfikator nazwy.</span><span class="sxs-lookup"><span data-stu-id="38eb5-214">Default SAML User ID location is Name Identifier.</span></span> <span data-ttu-id="38eb5-215">Można zmienić tej opcji atrybutu tooan i wprowadź nazwę atrybutu odpowiednie hello.</span><span class="sxs-lookup"><span data-stu-id="38eb5-215">You can change this tooan attribute option and enter hello appropriate attribute name.</span></span>

    > [!TIP]
    > <span data-ttu-id="38eb5-216">Upewnij się, że istnieje tylko jeden certyfikat mapowany aplikacji hello tak, aby nie było błędu rozpoznawania hello metadanych.</span><span class="sxs-lookup"><span data-stu-id="38eb5-216">Ensure that there is only one certificate mapped against hello app so that there is no error in resolving hello metadata.</span></span> <span data-ttu-id="38eb5-217">Jeśli dostępnych jest wiele certyfikatów na rozpoznawanie metadanych hello admin pobiera wystąpił błąd.</span><span class="sxs-lookup"><span data-stu-id="38eb5-217">If there are multiple certificates, upon resolving hello metadata, admin gets an error.</span></span>
    
    <span data-ttu-id="38eb5-218">b.</span><span class="sxs-lookup"><span data-stu-id="38eb5-218">b.</span></span> <span data-ttu-id="38eb5-219">Kopiuj hello **identyfikator, adres URL odpowiedzi i zaloguj się na adres URL** wartości i wklej je w **identyfikator, adres URL odpowiedzi i zaloguj się na adres URL** odpowiednio do pól tekstowych **logowania jednokrotnego SAML zlewiska Domain firmy Microsoft i adresy URL**  sekcji z portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="38eb5-219">Copy hello **Identifier, Reply URL and Sign on URL** values and paste them in **Identifier, Reply URL and Sign on URL** textboxes respectively in **Confluence SAML SSO by Microsoft Domain and URLs** section on Azure portal.</span></span>

    <span data-ttu-id="38eb5-220">c.</span><span class="sxs-lookup"><span data-stu-id="38eb5-220">c.</span></span> <span data-ttu-id="38eb5-221">W **nazwa przycisku logowania** nazwa hello typu przycisku organizacja chce hello toosee użytkowników na ekranie logowania.</span><span class="sxs-lookup"><span data-stu-id="38eb5-221">In **Login Button Name** type hello name of button your organization wants hello users toosee on login screen.</span></span>

    <span data-ttu-id="38eb5-222">d.</span><span class="sxs-lookup"><span data-stu-id="38eb5-222">d.</span></span> <span data-ttu-id="38eb5-223">W **lokalizacje identyfikator użytkownika SAML** wybierz opcję **identyfikator użytkownika jest w elemencie NameIdentifier hello hello instrukcji podmiotu** lub **identyfikator użytkownika jest w elemencie atrybutu**.</span><span class="sxs-lookup"><span data-stu-id="38eb5-223">In **SAML User ID Locations** select either **User ID is in hello NameIdentifier element of hello Subject statement** or **User ID is in an Attribute element**.</span></span>  <span data-ttu-id="38eb5-224">Ten identyfikator ma identyfikator użytkownika zlewiska hello toobe. Jeśli hello identyfikator użytkownika nie jest zgodny, następnie systemu nie zezwala na toolog użytkowników w.</span><span class="sxs-lookup"><span data-stu-id="38eb5-224">This ID has toobe hello Confluence user id. If hello user id is not matched, then system will not allow users toolog in.</span></span> 
    
    <span data-ttu-id="38eb5-225">e.</span><span class="sxs-lookup"><span data-stu-id="38eb5-225">e.</span></span> <span data-ttu-id="38eb5-226">W przypadku wybrania **identyfikator użytkownika jest w elemencie atrybutu** opcji, a następnie w **nazwa atrybutu** pole tekstowe Nazwa hello typu atrybutu hello, gdzie jest oczekiwany identyfikator użytkownika.</span><span class="sxs-lookup"><span data-stu-id="38eb5-226">If you select **User ID is in an Attribute element** option, then in **Attribute name** textbox type hello name of hello attribute where User Id is expected.</span></span> 

    <span data-ttu-id="38eb5-227">f.</span><span class="sxs-lookup"><span data-stu-id="38eb5-227">f.</span></span> <span data-ttu-id="38eb5-228">Jeśli używasz hello domeny federacyjnej (na przykład usług AD FS itp.) z usługą Azure AD, należy kliknąć opcję hello **Włączanie odnajdowania obszaru macierzystego** opcji i skonfigurować hello **nazwy domeny**.</span><span class="sxs-lookup"><span data-stu-id="38eb5-228">If you are using hello federated domain (like ADFS etc.) with Azure AD, then click on hello **Enable Home Realm Discovery** option and configure hello **Domain Name**.</span></span>
    
    <span data-ttu-id="38eb5-229">g.</span><span class="sxs-lookup"><span data-stu-id="38eb5-229">g.</span></span> <span data-ttu-id="38eb5-230">W **nazwy domeny** hello domeny tym miejscu wpisz nazwę w przypadku logowania za pomocą usług AD FS hello.</span><span class="sxs-lookup"><span data-stu-id="38eb5-230">In **Domain Name** type hello domain name here in case of hello ADFS-based login.</span></span>

    <span data-ttu-id="38eb5-231">h.</span><span class="sxs-lookup"><span data-stu-id="38eb5-231">h.</span></span> <span data-ttu-id="38eb5-232">Sprawdź **włączyć pojedynczego Wyloguj** Jeśli chcesz toolog się z usługą Azure AD, gdy użytkownik zaloguje z zlewiska.</span><span class="sxs-lookup"><span data-stu-id="38eb5-232">Check **Enable Single Sign out** if you wish toolog out from Azure AD when a user logs out from Confluence.</span></span> 

    <span data-ttu-id="38eb5-233">i.</span><span class="sxs-lookup"><span data-stu-id="38eb5-233">i.</span></span> <span data-ttu-id="38eb5-234">Kliknij przycisk **zapisać** przycisk toosave hello ustawienia.</span><span class="sxs-lookup"><span data-stu-id="38eb5-234">Click **Save** button toosave hello settings.</span></span>


> [!TIP]
> <span data-ttu-id="38eb5-235">Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz hello [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji hello!</span><span class="sxs-lookup"><span data-stu-id="38eb5-235">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="38eb5-236">Po dodaniu tej aplikacji z hello **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij hello **rejestracji jednokrotnej** hello kartę i dostępu do osadzonych dokumentacji za pośrednictwem hello  **Konfiguracja** sekcji u dołu hello.</span><span class="sxs-lookup"><span data-stu-id="38eb5-236">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="38eb5-237">Więcej o hello osadzonych dokumentacji funkcji w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="38eb5-237">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="38eb5-238">Tworzenie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="38eb5-238">Creating an Azure AD test user</span></span>
<span data-ttu-id="38eb5-239">Celem Hello w tej sekcji jest toocreate użytkownika testowego, w portalu Azure o nazwie Simona Britta hello.</span><span class="sxs-lookup"><span data-stu-id="38eb5-239">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Tworzenie użytkowników usługi Azure AD][100]

<span data-ttu-id="38eb5-241">**toocreate użytkownika testowego w usłudze Azure AD, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="38eb5-241">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="38eb5-242">W hello **portalu Azure**na temat hello w lewym okienku nawigacji, kliknij przycisk **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="38eb5-242">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-confluencemicrosoft-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="38eb5-244">toodisplay hello listę użytkowników, przejdź zbyt**użytkowników i grup** i kliknij przycisk **wszyscy użytkownicy**.</span><span class="sxs-lookup"><span data-stu-id="38eb5-244">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-confluencemicrosoft-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="38eb5-246">Witaj tooopen **użytkownika** okna dialogowego, kliknij przycisk **Dodaj** u góry hello hello okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="38eb5-246">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-confluencemicrosoft-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="38eb5-248">Na powitania **użytkownika** okna dialogowego wykonaj hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="38eb5-248">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-confluencemicrosoft-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="38eb5-250">a.</span><span class="sxs-lookup"><span data-stu-id="38eb5-250">a.</span></span> <span data-ttu-id="38eb5-251">W hello **nazwa** pole tekstowe, typ **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="38eb5-251">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="38eb5-252">b.</span><span class="sxs-lookup"><span data-stu-id="38eb5-252">b.</span></span> <span data-ttu-id="38eb5-253">W hello **nazwy użytkownika** pole tekstowe, hello typu **adres e-mail** z BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="38eb5-253">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="38eb5-254">c.</span><span class="sxs-lookup"><span data-stu-id="38eb5-254">c.</span></span> <span data-ttu-id="38eb5-255">Wybierz **Pokaż hasło** i zanotuj wartość hello hello **hasło**.</span><span class="sxs-lookup"><span data-stu-id="38eb5-255">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="38eb5-256">d.</span><span class="sxs-lookup"><span data-stu-id="38eb5-256">d.</span></span> <span data-ttu-id="38eb5-257">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="38eb5-257">Click **Create**.</span></span>
 
### <a name="creating-a-confluence-saml-sso-by-microsoft-test-user"></a><span data-ttu-id="38eb5-258">Tworzenie logowania jednokrotnego SAML zlewiska przez użytkownika testowego firmy Microsoft</span><span class="sxs-lookup"><span data-stu-id="38eb5-258">Creating a Confluence SAML SSO by Microsoft test user</span></span>

<span data-ttu-id="38eb5-259">toolog użytkowników tooenable usługi Azure AD w tooConfluence na serwerze lokalnym, ich muszą mieć przydzielone do logowania jednokrotnego SAML zlewiska przez firmę Microsoft.</span><span class="sxs-lookup"><span data-stu-id="38eb5-259">tooenable Azure AD users toolog in tooConfluence on premise server, they must be provisioned into Confluence SAML SSO by Microsoft.</span></span> <span data-ttu-id="38eb5-260">W przypadku logowania jednokrotnego SAML zlewiska przez firmę Microsoft inicjowania obsługi administracyjnej jest zadanie ręczne.</span><span class="sxs-lookup"><span data-stu-id="38eb5-260">For Confluence SAML SSO by Microsoft, provisioning is a manual task.</span></span>

<span data-ttu-id="38eb5-261">**tooprovision konta użytkownika, należy wykonać hello następujące kroki:**</span><span class="sxs-lookup"><span data-stu-id="38eb5-261">**tooprovision a user account, perform hello following steps:**</span></span>

1. <span data-ttu-id="38eb5-262">Zaloguj się za tooyour zlewiska na lokalnym serwerze jako administrator.</span><span class="sxs-lookup"><span data-stu-id="38eb5-262">Log in tooyour Confluence on premise server as an administrator.</span></span>

2. <span data-ttu-id="38eb5-263">Umieść kursor na koło zębate, a następnie kliknij przycisk hello **Zarządzanie użytkownikami**.</span><span class="sxs-lookup"><span data-stu-id="38eb5-263">Hover on cog and click hello **User management**.</span></span>

    ![Dodawanie pracownika](./media/active-directory-saas-confluencemicrosoft-tutorial/user1.png) 

3. <span data-ttu-id="38eb5-265">W sekcji Użytkownicy kliknij **dodawania użytkowników** kartę. Na powitania **"Dodaj użytkownika"** okna dialogowego wykonaj hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="38eb5-265">Under Users section, click **Add users** tab. On hello **“Add a User”** dialog page, perform hello following steps:</span></span>

    ![Dodawanie pracownika](./media/active-directory-saas-confluencemicrosoft-tutorial/user2.png) 

    <span data-ttu-id="38eb5-267">a.</span><span class="sxs-lookup"><span data-stu-id="38eb5-267">a.</span></span> <span data-ttu-id="38eb5-268">W hello **Username** pole tekstowe, typ hello adres e-mail użytkownika, takich jak Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="38eb5-268">In hello **Username** textbox, type hello email of user like Britta Simon.</span></span>

    <span data-ttu-id="38eb5-269">b.</span><span class="sxs-lookup"><span data-stu-id="38eb5-269">b.</span></span> <span data-ttu-id="38eb5-270">W hello **imię i nazwisko** pole tekstowe, typ hello pełną nazwę użytkownika, takich jak Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="38eb5-270">In hello **Full Name** textbox, type hello full name of user like Britta Simon.</span></span>

    <span data-ttu-id="38eb5-271">c.</span><span class="sxs-lookup"><span data-stu-id="38eb5-271">c.</span></span> <span data-ttu-id="38eb5-272">W hello **E-mail** pole tekstowe, typ hello adres e-mail użytkownika, takich jak Brittasimon@contoso.com.</span><span class="sxs-lookup"><span data-stu-id="38eb5-272">In hello **Email** textbox, type hello email address of user like Brittasimon@contoso.com.</span></span>

    <span data-ttu-id="38eb5-273">d.</span><span class="sxs-lookup"><span data-stu-id="38eb5-273">d.</span></span> <span data-ttu-id="38eb5-274">W hello **hasło** tekstowym, wpisz hasło powitania dla Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="38eb5-274">In hello **Password** textbox, type hello password for Britta Simon.</span></span>

    <span data-ttu-id="38eb5-275">e.</span><span class="sxs-lookup"><span data-stu-id="38eb5-275">e.</span></span> <span data-ttu-id="38eb5-276">Kliknij przycisk **Potwierdź hasło** ponownie hello hasła.</span><span class="sxs-lookup"><span data-stu-id="38eb5-276">Click **Confirm Password** reenter hello password.</span></span>
    
    <span data-ttu-id="38eb5-277">f.</span><span class="sxs-lookup"><span data-stu-id="38eb5-277">f.</span></span> <span data-ttu-id="38eb5-278">Kliknij przycisk **Dodaj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="38eb5-278">Click **Add** button.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="38eb5-279">Przypisanie użytkownika testowego hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="38eb5-279">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="38eb5-280">W tej sekcji możesz włączyć toouse Simona Britta Azure logowania jednokrotnego za udzielanie dostępu tooConfluence logowania jednokrotnego SAML przez firmę Microsoft.</span><span class="sxs-lookup"><span data-stu-id="38eb5-280">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooConfluence SAML SSO by Microsoft.</span></span>

![Przypisz użytkownika][200] 

<span data-ttu-id="38eb5-282">**tooassign tooConfluence Simona Britta logowania jednokrotnego SAML przez firmę Microsoft, należy wykonać hello następujące kroki:**</span><span class="sxs-lookup"><span data-stu-id="38eb5-282">**tooassign Britta Simon tooConfluence SAML SSO by Microsoft, perform hello following steps:**</span></span>

1. <span data-ttu-id="38eb5-283">W portalu Azure hello, otwórz widok aplikacji hello, a następnie przejdź do widoku katalogu toohello i przejść za**aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="38eb5-283">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Przypisz użytkownika][201] 

2. <span data-ttu-id="38eb5-285">Z listy aplikacji hello wybierz **logowania jednokrotnego SAML zlewiska przez firmę Microsoft**.</span><span class="sxs-lookup"><span data-stu-id="38eb5-285">In hello applications list, select **Confluence SAML SSO by Microsoft**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-confluencemicrosoft-tutorial/tutorial_confluencemicrosoft_app.png) 

3. <span data-ttu-id="38eb5-287">W menu powitania po lewej stronie powitania kliknij **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="38eb5-287">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Przypisz użytkownika][202] 

4. <span data-ttu-id="38eb5-289">Kliknij przycisk **Dodaj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="38eb5-289">Click **Add** button.</span></span> <span data-ttu-id="38eb5-290">Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="38eb5-290">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Przypisz użytkownika][203]

5. <span data-ttu-id="38eb5-292">Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** hello listy użytkowników.</span><span class="sxs-lookup"><span data-stu-id="38eb5-292">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="38eb5-293">Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="38eb5-293">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="38eb5-294">Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="38eb5-294">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="38eb5-295">Testowanie rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="38eb5-295">Testing single sign-on</span></span>

<span data-ttu-id="38eb5-296">W tej sekcji można przetestować konfiguracji usługi Azure AD pojedynczego logowania jednokrotnego przy użyciu hello panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="38eb5-296">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="38eb5-297">Po kliknięciu hello logowania jednokrotnego SAML zlewiska przez Microsoft kafelka w hello Panel dostępu, należy pobrać automatycznie zalogowane tooyour logowania jednokrotnego SAML zlewiska przez aplikację Microsoft.</span><span class="sxs-lookup"><span data-stu-id="38eb5-297">When you click hello Confluence SAML SSO by Microsoft tile in hello Access Panel, you should get automatically signed-on tooyour Confluence SAML SSO by Microsoft application.</span></span>
<span data-ttu-id="38eb5-298">Aby uzyskać więcej informacji na temat hello Panel dostępu, zobacz [toohello wprowadzenie panelu dostępu](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="38eb5-298">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="38eb5-299">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="38eb5-299">Additional resources</span></span>

* [<span data-ttu-id="38eb5-300">Lista samouczków dotyczących tooIntegrate aplikacji SaaS w usłudze Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="38eb5-300">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="38eb5-301">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="38eb5-301">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-confluencemicrosoft-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-confluencemicrosoft-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-confluencemicrosoft-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-confluencemicrosoft-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-confluencemicrosoft-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-confluencemicrosoft-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-confluencemicrosoft-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-confluencemicrosoft-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-confluencemicrosoft-tutorial/tutorial_general_203.png

