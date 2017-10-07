---
title: 'Samouczek: Integracji Azure Active Directory z PolicyStat | Dokumentacja firmy Microsoft'
description: "Dowiedz się, jak tooconfigure logowanie jednokrotne między usługą Azure Active Directory i PolicyStat."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: af5eb0f1-1c8e-4809-b0c4-8ccfb915ca42
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: jeedes
ms.openlocfilehash: 868053cd0d37359fd9b4aeb93dba42cbbaa09845
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-policystat"></a><span data-ttu-id="79a97-103">Samouczek: Integracji Azure Active Directory z PolicyStat</span><span class="sxs-lookup"><span data-stu-id="79a97-103">Tutorial: Azure Active Directory integration with PolicyStat</span></span>

<span data-ttu-id="79a97-104">Z tego samouczka, dowiesz się, jak toointegrate PolicyStat w usłudze Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="79a97-104">In this tutorial, you learn how toointegrate PolicyStat with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="79a97-105">Integracja z usługą Azure AD PolicyStat zapewnia hello następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="79a97-105">Integrating PolicyStat with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="79a97-106">Można kontrolować w usłudze Azure AD, kto ma dostęp do tooPolicyStat</span><span class="sxs-lookup"><span data-stu-id="79a97-106">You can control in Azure AD who has access tooPolicyStat</span></span>
- <span data-ttu-id="79a97-107">Można włączyć użytkownika użytkownicy tooautomatically get zalogowane tooPolicyStat (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="79a97-107">You can enable your users tooautomatically get signed-on tooPolicyStat (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="79a97-108">Możesz zarządzać kont w jednej centralnej lokalizacji - hello portalu Azure</span><span class="sxs-lookup"><span data-stu-id="79a97-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="79a97-109">Jeśli chcesz tooknow więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="79a97-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="79a97-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="79a97-110">Prerequisites</span></span>

<span data-ttu-id="79a97-111">tooconfigure integracji z usługą Azure AD z PolicyStat należy hello następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="79a97-111">tooconfigure Azure AD integration with PolicyStat, you need hello following items:</span></span>

- <span data-ttu-id="79a97-112">Subskrypcję usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="79a97-112">An Azure AD subscription</span></span>
- <span data-ttu-id="79a97-113">PolicyStat logowanie jednokrotne włączone subskrypcji</span><span class="sxs-lookup"><span data-stu-id="79a97-113">A PolicyStat single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="79a97-114">tootest hello kroków w tym samouczku, zaleca się przy użyciu środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="79a97-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="79a97-115">tootest hello kroki opisane w tym samouczku, należy stosować te zalecenia:</span><span class="sxs-lookup"><span data-stu-id="79a97-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="79a97-116">Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="79a97-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="79a97-117">Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz pobrać miesięczna wersja próbna [tutaj](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="79a97-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="79a97-118">Opis scenariusza</span><span class="sxs-lookup"><span data-stu-id="79a97-118">Scenario description</span></span>
<span data-ttu-id="79a97-119">W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym.</span><span class="sxs-lookup"><span data-stu-id="79a97-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="79a97-120">Scenariusz Hello opisane w tym samouczku składa się z dwóch głównych elementów:</span><span class="sxs-lookup"><span data-stu-id="79a97-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="79a97-121">Dodawanie PolicyStat z galerii hello</span><span class="sxs-lookup"><span data-stu-id="79a97-121">Adding PolicyStat from hello gallery</span></span>
2. <span data-ttu-id="79a97-122">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="79a97-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-policystat-from-hello-gallery"></a><span data-ttu-id="79a97-123">Dodawanie PolicyStat z galerii hello</span><span class="sxs-lookup"><span data-stu-id="79a97-123">Adding PolicyStat from hello gallery</span></span>
<span data-ttu-id="79a97-124">tooconfigure hello integracji PolicyStat do usługi Azure AD, należy tooadd PolicyStat z hello galerii tooyour listę zarządzanych aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="79a97-124">tooconfigure hello integration of PolicyStat into Azure AD, you need tooadd PolicyStat from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="79a97-125">**tooadd PolicyStat z galerii hello, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="79a97-125">**tooadd PolicyStat from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="79a97-126">W hello  **[portalu Azure](https://portal.azure.com)**na temat hello panelu nawigacji po lewej stronie, kliknij przycisk **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="79a97-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Usługa Active Directory][1]

2. <span data-ttu-id="79a97-128">Przejdź za**aplikacje dla przedsiębiorstw**.</span><span class="sxs-lookup"><span data-stu-id="79a97-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="79a97-129">Następnie przejdź zbyt**wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="79a97-129">Then go too**All applications**.</span></span>

    ![Aplikacje][2]
    
3. <span data-ttu-id="79a97-131">tooadd nową aplikację, kliknij przycisk **nowej aplikacji** przycisk u góry hello okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="79a97-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplikacje][3]

4. <span data-ttu-id="79a97-133">W polu wyszukiwania hello wpisz **PolicyStat**.</span><span class="sxs-lookup"><span data-stu-id="79a97-133">In hello search box, type **PolicyStat**.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-policystat-tutorial/tutorial_policystat_search.png)

5. <span data-ttu-id="79a97-135">W panelu wyników hello zaznacz **PolicyStat**, a następnie kliknij przycisk **Dodaj** przycisk aplikacji hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="79a97-135">In hello results panel, select **PolicyStat**, and then click **Add** button tooadd hello application.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-policystat-tutorial/tutorial_policystat_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="79a97-137">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="79a97-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="79a97-138">W tej sekcji skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z PolicyStat w oparciu o nazwie "Britta Simona" użytkownika testowego.</span><span class="sxs-lookup"><span data-stu-id="79a97-138">In this section, you configure and test Azure AD single sign-on with PolicyStat based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="79a97-139">Dla pojedynczego logowania jednokrotnego toowork usługi Azure AD musi tooknow użytkownika odpowiednikiem hello w PolicyStat jest tooa użytkownika w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="79a97-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in PolicyStat is tooa user in Azure AD.</span></span> <span data-ttu-id="79a97-140">Innymi słowy relację łącza między użytkownika usługi Azure AD i hello użytkownikowi w PolicyStat musi toobe ustanowione.</span><span class="sxs-lookup"><span data-stu-id="79a97-140">In other words, a link relationship between an Azure AD user and hello related user in PolicyStat needs toobe established.</span></span>

<span data-ttu-id="79a97-141">W PolicyStat, należy przypisać wartość hello hello **nazwy użytkownika** w usłudze Azure AD jako wartość hello hello **Username** tooestablish hello łącze relacji.</span><span class="sxs-lookup"><span data-stu-id="79a97-141">In PolicyStat, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="79a97-142">tooconfigure i testowych usługi Azure AD rejestracji jednokrotnej z PolicyStat, należy po bloków konstrukcyjnych hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="79a97-142">tooconfigure and test Azure AD single sign-on with PolicyStat, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="79a97-143">**[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configuring-azure-ad-single-sign-on)**  -tooenable Twojego toouse użytkowników tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="79a97-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="79a97-144">**[Tworzenie użytkownika testowego usługi Azure AD](#creating-an-azure-ad-test-user)**  -tootest usługi Azure AD rejestracji jednokrotnej z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="79a97-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="79a97-145">**[Tworzenie użytkownika testowego PolicyStat](#creating-a-policystat-test-user)**  -toohave odpowiednikiem Simona Britta w PolicyStat, który jest połączony toohello usługi Azure AD reprezentację użytkownika.</span><span class="sxs-lookup"><span data-stu-id="79a97-145">**[Creating a PolicyStat test user](#creating-a-policystat-test-user)** - toohave a counterpart of Britta Simon in PolicyStat that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="79a97-146">**[Przypisanie użytkownika testowego hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Simona Britta toouse usługi Azure AD rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="79a97-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="79a97-147">**[Testowanie rejestracji jednokrotnej](#testing-single-sign-on)**  -tooverify czy hello konfiguracji działania.</span><span class="sxs-lookup"><span data-stu-id="79a97-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="79a97-148">Konfigurowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="79a97-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="79a97-149">W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w portalu Azure hello i skonfigurować logowanie jednokrotne w aplikacji PolicyStat.</span><span class="sxs-lookup"><span data-stu-id="79a97-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your PolicyStat application.</span></span>

<span data-ttu-id="79a97-150">**tooconfigure usługi Azure AD rejestracji jednokrotnej z PolicyStat, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="79a97-150">**tooconfigure Azure AD single sign-on with PolicyStat, perform hello following steps:**</span></span>

1. <span data-ttu-id="79a97-151">W portalu Azure na powitania hello **PolicyStat** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.</span><span class="sxs-lookup"><span data-stu-id="79a97-151">In hello Azure portal, on hello **PolicyStat** application integration page, click **Single sign-on**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej][4]

2. <span data-ttu-id="79a97-153">Na powitania **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** tooenable rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="79a97-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-policystat-tutorial/tutorial_policystat_samlbase.png)

3. <span data-ttu-id="79a97-155">Na powitania **PolicyStat domeny i adres URL** sekcji, wykonaj następujące kroki hello:</span><span class="sxs-lookup"><span data-stu-id="79a97-155">On hello **PolicyStat Domain and URLs** section, perform hello following steps:</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-policystat-tutorial/tutorial_policystat_url.png)

    <span data-ttu-id="79a97-157">a.</span><span class="sxs-lookup"><span data-stu-id="79a97-157">a.</span></span> <span data-ttu-id="79a97-158">W hello **adres URL logowania** tekstowym, wpisz adres URL za pomocą hello następującego wzorca:`https://<companyname>.policystat.com`</span><span class="sxs-lookup"><span data-stu-id="79a97-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<companyname>.policystat.com`</span></span>

    <span data-ttu-id="79a97-159">b.</span><span class="sxs-lookup"><span data-stu-id="79a97-159">b.</span></span> <span data-ttu-id="79a97-160">W hello **identyfikator** tekstowym, wpisz adres URL za pomocą hello następującego wzorca:`https://<companyname>.policystat.com/saml2/metadata/`</span><span class="sxs-lookup"><span data-stu-id="79a97-160">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<companyname>.policystat.com/saml2/metadata/`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="79a97-161">Wartości te nie są prawdziwe.</span><span class="sxs-lookup"><span data-stu-id="79a97-161">These values are not real.</span></span> <span data-ttu-id="79a97-162">Zaktualizować te wartości z hello rzeczywisty adres URL logowania i identyfikator.</span><span class="sxs-lookup"><span data-stu-id="79a97-162">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="79a97-163">Skontaktuj się z [zespołem pomocy technicznej klienta PolicyStat](http://www.policystat.com/support/) tooget tych wartości.</span><span class="sxs-lookup"><span data-stu-id="79a97-163">Contact [PolicyStat Client support team](http://www.policystat.com/support/) tooget these values.</span></span> 
 
4. <span data-ttu-id="79a97-164">Na powitania **certyfikat podpisywania SAML** kliknij **XML metadanych** , a następnie zapisz plik metadanych hello na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="79a97-164">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-policystat-tutorial/tutorial_policystat_certificate.png) 

5. <span data-ttu-id="79a97-166">Celem Hello w tej sekcji jest toooutline jak tooenable użytkowników tooauthenticate tooPolicyStat do swojego konta w usłudze Azure AD przy użyciu Federacji oparte na powitania protokołu SAML.</span><span class="sxs-lookup"><span data-stu-id="79a97-166">hello objective of this section is toooutline how tooenable users tooauthenticate tooPolicyStat with their account in Azure AD using federation based on hello SAML protocol.</span></span>

    <span data-ttu-id="79a97-167">PolicyStat aplikacji Hello oczekuje potwierdzenia SAML hello w określonym formacie wymaga tooyour mapowań atrybutów niestandardowych tooadd **atrybuty tokenu SAML** konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="79a97-167">hello PolicyStat application expects hello SAML assertions in a specific format, which requires you tooadd custom attribute mappings tooyour **SAML Token Attributes** configuration.</span></span>  

     <span data-ttu-id="79a97-168">powitania po zrzut ekranu przedstawia przykład.</span><span class="sxs-lookup"><span data-stu-id="79a97-168">hello following screenshot shows an example of this.</span></span>

     <span data-ttu-id="79a97-169">![Atrybuty](./media/active-directory-saas-policystat-tutorial/tutorial_policystat_attribute.png "atrybutów")</span><span class="sxs-lookup"><span data-stu-id="79a97-169">![Attributes](./media/active-directory-saas-policystat-tutorial/tutorial_policystat_attribute.png "Attributes")</span></span>

6. <span data-ttu-id="79a97-170">Mapowanie atrybutów hello wymagane tooadd, wykonaj hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="79a97-170">tooadd hello required attribute mappings, perform hello following steps:</span></span>

    | <span data-ttu-id="79a97-171">Nazwa atrybutu</span><span class="sxs-lookup"><span data-stu-id="79a97-171">Attribute Name</span></span>    |   <span data-ttu-id="79a97-172">Wartość atrybutu</span><span class="sxs-lookup"><span data-stu-id="79a97-172">Attribute Value</span></span> |
    |------------------- | -------------------- |
    | <span data-ttu-id="79a97-173">Identyfikator UID</span><span class="sxs-lookup"><span data-stu-id="79a97-173">uid</span></span> | <span data-ttu-id="79a97-174">ExtractMailPrefix([mail])</span><span class="sxs-lookup"><span data-stu-id="79a97-174">ExtractMailPrefix([mail])</span></span> |
    
    <span data-ttu-id="79a97-175">a.</span><span class="sxs-lookup"><span data-stu-id="79a97-175">a.</span></span> <span data-ttu-id="79a97-176">Kliknij przycisk **Dodaj atrybut** tooopen hello **Dodawanie atrybutu** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="79a97-176">Click **Add attribute** tooopen hello **Add Attribute** dialog.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-policystat-tutorial/tutorial_policystat_04.png)

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-policystat-tutorial/tutorial_policystat_addatribute.png)
    
    <span data-ttu-id="79a97-179">b.</span><span class="sxs-lookup"><span data-stu-id="79a97-179">b.</span></span> <span data-ttu-id="79a97-180">W hello **nazwa atrybutu** pole tekstowe, typ **uid**.</span><span class="sxs-lookup"><span data-stu-id="79a97-180">In hello **Attribute Name** textbox, type **uid**.</span></span>

    <span data-ttu-id="79a97-181">c.</span><span class="sxs-lookup"><span data-stu-id="79a97-181">c.</span></span> <span data-ttu-id="79a97-182">W hello **wartość atrybutu** pole tekstowe, wybierz opcję **ExtractMailPrefix()**.</span><span class="sxs-lookup"><span data-stu-id="79a97-182">In hello **Attribute Value** textbox, select **ExtractMailPrefix()**.</span></span>    
   
    <span data-ttu-id="79a97-183">d.</span><span class="sxs-lookup"><span data-stu-id="79a97-183">d.</span></span> <span data-ttu-id="79a97-184">Z hello **poczty** listy, wybierz **User.mail**.</span><span class="sxs-lookup"><span data-stu-id="79a97-184">From hello **Mail** list, select **User.mail**.</span></span>
    
    <span data-ttu-id="79a97-185">e.</span><span class="sxs-lookup"><span data-stu-id="79a97-185">e.</span></span> <span data-ttu-id="79a97-186">Kliknij przycisk **Ok**</span><span class="sxs-lookup"><span data-stu-id="79a97-186">Click **Ok**</span></span>

7. <span data-ttu-id="79a97-187">Kliknij przycisk **zapisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="79a97-187">Click **Save** button.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-policystat-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="79a97-189">W oknie przeglądarki innej witryny sieci web Zaloguj się do witryny firmy PolicyStat jako administrator.</span><span class="sxs-lookup"><span data-stu-id="79a97-189">In a different web browser window, log into your PolicyStat company site as an administrator.</span></span>

9. <span data-ttu-id="79a97-190">Kliknij przycisk hello **Admin** , a następnie kliknij pozycję **konfiguracji rejestracji jednokrotnej** w lewym okienku nawigacji.</span><span class="sxs-lookup"><span data-stu-id="79a97-190">Click hello **Admin** tab, and then click **Single Sign-On Configuration** in left navigation pane.</span></span>
   
    <span data-ttu-id="79a97-191">![Menu administratora](./media/active-directory-saas-policystat-tutorial/ic808633.png "Menu administratora")</span><span class="sxs-lookup"><span data-stu-id="79a97-191">![Administrator Menu](./media/active-directory-saas-policystat-tutorial/ic808633.png "Administrator Menu")</span></span>

10. <span data-ttu-id="79a97-192">W hello **Instalator** zaznacz **włączyć pojedynczego logowania jednokrotnego integracji**.</span><span class="sxs-lookup"><span data-stu-id="79a97-192">In hello **Setup** section, select **Enable Single Sign-on Integration**.</span></span>
   
    <span data-ttu-id="79a97-193">![Pojedynczy konfiguracji logowania jednokrotnego](./media/active-directory-saas-policystat-tutorial/ic808634.png "pojedynczy konfiguracji logowania jednokrotnego")</span><span class="sxs-lookup"><span data-stu-id="79a97-193">![Single Sign-On Configuration](./media/active-directory-saas-policystat-tutorial/ic808634.png "Single Sign-On Configuration")</span></span>

11. <span data-ttu-id="79a97-194">Kliknij przycisk **Konfigurowanie atrybutów**, a następnie na powitania **Konfigurowanie atrybutów** sekcji, wykonaj następujące kroki hello:</span><span class="sxs-lookup"><span data-stu-id="79a97-194">Click **Configure Attributes**, and then, in hello **Configure Attributes** section, perform hello following steps:</span></span>
   
    <span data-ttu-id="79a97-195">![Pojedynczy konfiguracji logowania jednokrotnego](./media/active-directory-saas-policystat-tutorial/ic808635.png "pojedynczy konfiguracji logowania jednokrotnego")</span><span class="sxs-lookup"><span data-stu-id="79a97-195">![Single Sign-On Configuration](./media/active-directory-saas-policystat-tutorial/ic808635.png "Single Sign-On Configuration")</span></span>
   
    <span data-ttu-id="79a97-196">a.</span><span class="sxs-lookup"><span data-stu-id="79a97-196">a.</span></span> <span data-ttu-id="79a97-197">W hello **atrybutu Username** pole tekstowe, typ **uid**.</span><span class="sxs-lookup"><span data-stu-id="79a97-197">In hello **Username Attribute** textbox, type **uid**.</span></span>

    <span data-ttu-id="79a97-198">b.</span><span class="sxs-lookup"><span data-stu-id="79a97-198">b.</span></span> <span data-ttu-id="79a97-199">W hello **atrybutu imię** pole tekstowe, typ **imię** użytkownika **Britta**.</span><span class="sxs-lookup"><span data-stu-id="79a97-199">In hello **First Name Attribute** textbox, type **firstname** of user **Britta**.</span></span>

    <span data-ttu-id="79a97-200">c.</span><span class="sxs-lookup"><span data-stu-id="79a97-200">c.</span></span> <span data-ttu-id="79a97-201">W hello **ostatniego atrybutu Name** pole tekstowe, typ **nazwisko** użytkownika **Simona**.</span><span class="sxs-lookup"><span data-stu-id="79a97-201">In hello **Last Name Attribute** textbox, type **lastname** of user **Simon**.</span></span>

    <span data-ttu-id="79a97-202">d.</span><span class="sxs-lookup"><span data-stu-id="79a97-202">d.</span></span> <span data-ttu-id="79a97-203">W hello **atrybut poczty E-mail** pole tekstowe, typ **emailaddress** użytkownika  **BrittaSimon@contoso.com** .</span><span class="sxs-lookup"><span data-stu-id="79a97-203">In hello **Email Attribute** textbox, type **emailaddress** of user **BrittaSimon@contoso.com**.</span></span>

    <span data-ttu-id="79a97-204">e.</span><span class="sxs-lookup"><span data-stu-id="79a97-204">e.</span></span> <span data-ttu-id="79a97-205">Kliknij przycisk **zapisać zmiany**.</span><span class="sxs-lookup"><span data-stu-id="79a97-205">Click **Save Changes**.</span></span>

12. <span data-ttu-id="79a97-206">Kliknij przycisk **Your metadanych IDP**, a następnie na powitania **Your metadanych IDP** sekcji, wykonaj następujące kroki hello:</span><span class="sxs-lookup"><span data-stu-id="79a97-206">Click **Your IDP Metadata**, and then, in hello **Your IDP Metadata** section, perform hello following steps:</span></span>
   
    <span data-ttu-id="79a97-207">![Pojedynczy konfiguracji logowania jednokrotnego](./media/active-directory-saas-policystat-tutorial/ic808636.png "pojedynczy konfiguracji logowania jednokrotnego")</span><span class="sxs-lookup"><span data-stu-id="79a97-207">![Single Sign-On Configuration](./media/active-directory-saas-policystat-tutorial/ic808636.png "Single Sign-On Configuration")</span></span>
   
    <span data-ttu-id="79a97-208">a.</span><span class="sxs-lookup"><span data-stu-id="79a97-208">a.</span></span> <span data-ttu-id="79a97-209">Otwórz z pliku metadanych pobranych, hello kopiowania zawartości, a następnie wklej go do hello **Your metadanych dostawcy tożsamości** pola tekstowego.</span><span class="sxs-lookup"><span data-stu-id="79a97-209">Open your downloaded metadata file, copy hello content, and  then paste it into hello **Your Identity Provider Metadata** textbox.</span></span>

    <span data-ttu-id="79a97-210">b.</span><span class="sxs-lookup"><span data-stu-id="79a97-210">b.</span></span> <span data-ttu-id="79a97-211">Kliknij przycisk **zapisać zmiany**.</span><span class="sxs-lookup"><span data-stu-id="79a97-211">Click **Save Changes**.</span></span>

> [!TIP]
> <span data-ttu-id="79a97-212">Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz hello [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji hello!</span><span class="sxs-lookup"><span data-stu-id="79a97-212">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="79a97-213">Po dodaniu tej aplikacji z hello **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij hello **rejestracji jednokrotnej** hello kartę i dostępu do osadzonych dokumentacji za pośrednictwem hello  **Konfiguracja** sekcji u dołu hello.</span><span class="sxs-lookup"><span data-stu-id="79a97-213">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="79a97-214">Więcej o hello osadzonych dokumentacji funkcji w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="79a97-214">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="79a97-215">Tworzenie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="79a97-215">Creating an Azure AD test user</span></span>
<span data-ttu-id="79a97-216">Celem Hello w tej sekcji jest toocreate użytkownika testowego, w portalu Azure o nazwie Simona Britta hello.</span><span class="sxs-lookup"><span data-stu-id="79a97-216">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Tworzenie użytkowników usługi Azure AD][100]

<span data-ttu-id="79a97-218">**toocreate użytkownika testowego w usłudze Azure AD, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="79a97-218">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="79a97-219">W hello **portalu Azure**na temat hello w lewym okienku nawigacji, kliknij przycisk **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="79a97-219">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-policystat-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="79a97-221">toodisplay hello listę użytkowników, przejdź zbyt**użytkowników i grup** i kliknij przycisk **wszyscy użytkownicy**.</span><span class="sxs-lookup"><span data-stu-id="79a97-221">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-policystat-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="79a97-223">Witaj tooopen **użytkownika** okna dialogowego, kliknij przycisk **Dodaj** u góry hello hello okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="79a97-223">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-policystat-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="79a97-225">Na powitania **użytkownika** okna dialogowego wykonaj hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="79a97-225">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-policystat-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="79a97-227">a.</span><span class="sxs-lookup"><span data-stu-id="79a97-227">a.</span></span> <span data-ttu-id="79a97-228">W hello **nazwa** pole tekstowe, typ **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="79a97-228">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="79a97-229">b.</span><span class="sxs-lookup"><span data-stu-id="79a97-229">b.</span></span> <span data-ttu-id="79a97-230">W hello **nazwy użytkownika** pole tekstowe, hello typu **adres e-mail** z BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="79a97-230">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="79a97-231">c.</span><span class="sxs-lookup"><span data-stu-id="79a97-231">c.</span></span> <span data-ttu-id="79a97-232">Wybierz **Pokaż hasło** i zanotuj wartość hello hello **hasło**.</span><span class="sxs-lookup"><span data-stu-id="79a97-232">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="79a97-233">d.</span><span class="sxs-lookup"><span data-stu-id="79a97-233">d.</span></span> <span data-ttu-id="79a97-234">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="79a97-234">Click **Create**.</span></span>
 
### <a name="creating-a-policystat-test-user"></a><span data-ttu-id="79a97-235">Tworzenie użytkownika testowego PolicyStat</span><span class="sxs-lookup"><span data-stu-id="79a97-235">Creating a PolicyStat test user</span></span>

<span data-ttu-id="79a97-236">W przypadku użytkowników usługi Azure AD toolog kolejności tooenable do PolicyStat muszą mieć przydzielone do PolicyStat.</span><span class="sxs-lookup"><span data-stu-id="79a97-236">In order tooenable Azure AD users toolog into PolicyStat, they must be provisioned into PolicyStat.</span></span>  

<span data-ttu-id="79a97-237">PolicyStat obsługuje tylko w czasie Inicjowanie obsługi użytkowników.</span><span class="sxs-lookup"><span data-stu-id="79a97-237">PolicyStat supports just in time user provisioning.</span></span> <span data-ttu-id="79a97-238">Oznacza to, że nie ma potrzeby użytkowników hello tooadd ręcznie tooPolicyStat.</span><span class="sxs-lookup"><span data-stu-id="79a97-238">This means, you do not need tooadd hello users manually tooPolicyStat.</span></span> <span data-ttu-id="79a97-239">Użytkownicy Hello będzie zostaną dodane automatycznie na ich pierwsze logowanie za pomocą logowania jednokrotnego.</span><span class="sxs-lookup"><span data-stu-id="79a97-239">hello users will get added automatically on their first login through SSO.</span></span>

>[!NOTE]
><span data-ttu-id="79a97-240">Możesz użyć innych PolicyStat użytkownika konta tworzenia narzędzi lub interfejsów API dostarczonych przez PolicyStat tooprovision kont użytkowników usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="79a97-240">You can use any other PolicyStat user account creation tools or APIs provided by PolicyStat tooprovision Azure AD user accounts.</span></span>
> 

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="79a97-241">Przypisanie użytkownika testowego hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="79a97-241">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="79a97-242">W tej sekcji możesz włączyć toouse Simona Britta Azure logowania jednokrotnego za udzielanie dostępu tooPolicyStat.</span><span class="sxs-lookup"><span data-stu-id="79a97-242">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooPolicyStat.</span></span>

![Przypisz użytkownika][200] 

<span data-ttu-id="79a97-244">**tooassign tooPolicyStat Simona Britta wykonaj hello następujące kroki:**</span><span class="sxs-lookup"><span data-stu-id="79a97-244">**tooassign Britta Simon tooPolicyStat, perform hello following steps:**</span></span>

1. <span data-ttu-id="79a97-245">W portalu Azure hello, otwórz widok aplikacji hello, a następnie przejdź do widoku katalogu toohello i przejść za**aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="79a97-245">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Przypisz użytkownika][201] 

2. <span data-ttu-id="79a97-247">Z listy aplikacji hello wybierz **PolicyStat**.</span><span class="sxs-lookup"><span data-stu-id="79a97-247">In hello applications list, select **PolicyStat**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-policystat-tutorial/tutorial_policystat_app.png) 

3. <span data-ttu-id="79a97-249">W menu powitania po lewej stronie powitania kliknij **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="79a97-249">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Przypisz użytkownika][202] 

4. <span data-ttu-id="79a97-251">Kliknij przycisk **Dodaj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="79a97-251">Click **Add** button.</span></span> <span data-ttu-id="79a97-252">Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="79a97-252">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Przypisz użytkownika][203]

5. <span data-ttu-id="79a97-254">Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** hello listy użytkowników.</span><span class="sxs-lookup"><span data-stu-id="79a97-254">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="79a97-255">Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="79a97-255">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="79a97-256">Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="79a97-256">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="79a97-257">Testowanie rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="79a97-257">Testing single sign-on</span></span>

<span data-ttu-id="79a97-258">W tej sekcji można przetestować konfiguracji usługi Azure AD pojedynczego logowania jednokrotnego przy użyciu hello panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="79a97-258">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="79a97-259">Po kliknięciu kafelka PolicyStat hello w hello Panel dostępu, należy pobrać automatycznie zalogowane tooyour PolicyStat aplikacji.</span><span class="sxs-lookup"><span data-stu-id="79a97-259">When you click hello PolicyStat tile in hello Access Panel, you should get automatically signed-on tooyour PolicyStat application.</span></span>
<span data-ttu-id="79a97-260">Aby uzyskać więcej informacji na temat hello Panel dostępu, zobacz [toohello wprowadzenie panelu dostępu](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="79a97-260">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="79a97-261">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="79a97-261">Additional resources</span></span>

* [<span data-ttu-id="79a97-262">Lista samouczków dotyczących tooIntegrate aplikacji SaaS w usłudze Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="79a97-262">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="79a97-263">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="79a97-263">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-policystat-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-policystat-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-policystat-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-policystat-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-policystat-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-policystat-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-policystat-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-policystat-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-policystat-tutorial/tutorial_general_203.png

