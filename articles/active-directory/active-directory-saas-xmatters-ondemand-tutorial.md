---
title: 'Samouczek: Integracji Azure Active Directory z xMatters OnDemand | Dokumentacja firmy Microsoft'
description: "Dowiedz się, jak tooconfigure logowanie jednokrotne między usługą Azure Active Directory i xMatters na żądanie."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: ca0633db-4f95-432e-b3db-0168193b5ce9
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: jeedes
ms.openlocfilehash: 7cc8f9f0d8cefc8a60b9514027437ced50c66242
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-xmatters-ondemand"></a><span data-ttu-id="fe6df-103">Samouczek: Integracji Azure Active Directory z xMatters na żądanie</span><span class="sxs-lookup"><span data-stu-id="fe6df-103">Tutorial: Azure Active Directory integration with xMatters OnDemand</span></span>

<span data-ttu-id="fe6df-104">Z tego samouczka, dowiesz się, jak xMatters toointegrate OnDemand w usłudze Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="fe6df-104">In this tutorial, you learn how toointegrate xMatters OnDemand with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="fe6df-105">Integrowanie xMatters na żądanie z usługą Azure AD zapewnia hello następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="fe6df-105">Integrating xMatters OnDemand with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="fe6df-106">Można kontrolować w usłudze Azure AD, kto ma dostęp do tooxMatters na żądanie</span><span class="sxs-lookup"><span data-stu-id="fe6df-106">You can control in Azure AD who has access tooxMatters OnDemand</span></span>
- <span data-ttu-id="fe6df-107">Można włączyć użytkownika użytkownicy tooautomatically get zalogowane tooxMatters OnDemand (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="fe6df-107">You can enable your users tooautomatically get signed-on tooxMatters OnDemand (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="fe6df-108">Możesz zarządzać kont w jednej centralnej lokalizacji - hello portalu Azure</span><span class="sxs-lookup"><span data-stu-id="fe6df-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="fe6df-109">Jeśli chcesz tooknow więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="fe6df-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="fe6df-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="fe6df-110">Prerequisites</span></span>

<span data-ttu-id="fe6df-111">tooconfigure integracji usługi Azure AD z xMatters na żądanie należy hello następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="fe6df-111">tooconfigure Azure AD integration with xMatters OnDemand, you need hello following items:</span></span>

- <span data-ttu-id="fe6df-112">Subskrypcję usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="fe6df-112">An Azure AD subscription</span></span>
- <span data-ttu-id="fe6df-113">XMatters OnDemand logowanie jednokrotne włączone subskrypcji</span><span class="sxs-lookup"><span data-stu-id="fe6df-113">A xMatters OnDemand single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="fe6df-114">tootest hello kroków w tym samouczku, zaleca się przy użyciu środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="fe6df-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="fe6df-115">tootest hello kroki opisane w tym samouczku, należy stosować te zalecenia:</span><span class="sxs-lookup"><span data-stu-id="fe6df-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="fe6df-116">Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="fe6df-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="fe6df-117">Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz pobrać miesięczna wersja próbna [tutaj](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="fe6df-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="fe6df-118">Opis scenariusza</span><span class="sxs-lookup"><span data-stu-id="fe6df-118">Scenario description</span></span>
<span data-ttu-id="fe6df-119">W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym.</span><span class="sxs-lookup"><span data-stu-id="fe6df-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="fe6df-120">Scenariusz Hello opisane w tym samouczku składa się z dwóch głównych elementów:</span><span class="sxs-lookup"><span data-stu-id="fe6df-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="fe6df-121">Dodawanie xMatters na żądanie z galerii hello</span><span class="sxs-lookup"><span data-stu-id="fe6df-121">Adding xMatters OnDemand from hello gallery</span></span>
2. <span data-ttu-id="fe6df-122">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="fe6df-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-xmatters-ondemand-from-hello-gallery"></a><span data-ttu-id="fe6df-123">Dodawanie xMatters na żądanie z galerii hello</span><span class="sxs-lookup"><span data-stu-id="fe6df-123">Adding xMatters OnDemand from hello gallery</span></span>
<span data-ttu-id="fe6df-124">tooconfigure hello integracji xMatters na żądanie do usługi Azure AD, należy tooadd xMatters na żądanie z hello galerii tooyour listę zarządzanych aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="fe6df-124">tooconfigure hello integration of xMatters OnDemand into Azure AD, you need tooadd xMatters OnDemand from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="fe6df-125">**xMatters tooadd na żądanie z galerii hello wykonaj hello następujące kroki:**</span><span class="sxs-lookup"><span data-stu-id="fe6df-125">**tooadd xMatters OnDemand from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="fe6df-126">W hello  **[portalu Azure](https://portal.azure.com)**na temat hello panelu nawigacji po lewej stronie, kliknij przycisk **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="fe6df-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Usługa Active Directory][1]

2. <span data-ttu-id="fe6df-128">Przejdź za**aplikacje dla przedsiębiorstw**.</span><span class="sxs-lookup"><span data-stu-id="fe6df-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="fe6df-129">Następnie przejdź zbyt**wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="fe6df-129">Then go too**All applications**.</span></span>

    ![Aplikacje][2]
    
3. <span data-ttu-id="fe6df-131">tooadd nową aplikację, kliknij przycisk **nowej aplikacji** przycisk u góry hello okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="fe6df-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplikacje][3]

4. <span data-ttu-id="fe6df-133">W polu wyszukiwania hello wpisz **xMatters OnDemand**.</span><span class="sxs-lookup"><span data-stu-id="fe6df-133">In hello search box, type **xMatters OnDemand**.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-xmatters-ondemand-tutorial/tutorial_xmattersondemand_search.png)

5. <span data-ttu-id="fe6df-135">W panelu wyników hello, wybierz **xMatters OnDemand**, a następnie kliknij przycisk **Dodaj** przycisk tooadd hello aplikacji.</span><span class="sxs-lookup"><span data-stu-id="fe6df-135">In hello results panel, select **xMatters OnDemand**, and then click **Add** button tooadd hello application.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-xmatters-ondemand-tutorial/tutorial_xmattersondemand_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="fe6df-137">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="fe6df-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="fe6df-138">W tej sekcji skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z xMatters OnDemand oparta na koncie użytkownika testu o nazwie "Britta Simona".</span><span class="sxs-lookup"><span data-stu-id="fe6df-138">In this section, you configure and test Azure AD single sign-on with xMatters OnDemand based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="fe6df-139">Dla pojedynczego logowania jednokrotnego toowork, usługi Azure AD musi tooknow jakie hello użytkownika odpowiednika w xMatters OnDemand jest tooa użytkownika w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="fe6df-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in xMatters OnDemand is tooa user in Azure AD.</span></span> <span data-ttu-id="fe6df-140">Innymi słowy relację łącza między użytkownika usługi Azure AD i hello użytkownikowi w xMatters OnDemand musi toobe ustanowione.</span><span class="sxs-lookup"><span data-stu-id="fe6df-140">In other words, a link relationship between an Azure AD user and hello related user in xMatters OnDemand needs toobe established.</span></span>

<span data-ttu-id="fe6df-141">W xMatters na żądanie, należy przypisać wartość hello hello **nazwy użytkownika** w usłudze Azure AD jako wartość hello hello **Username** tooestablish hello łącze relacji.</span><span class="sxs-lookup"><span data-stu-id="fe6df-141">In xMatters OnDemand, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="fe6df-142">tooconfigure i testowych usługi Azure AD rejestracji jednokrotnej z xMatters na żądanie, należy po bloków konstrukcyjnych hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="fe6df-142">tooconfigure and test Azure AD single sign-on with xMatters OnDemand, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="fe6df-143">**[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configuring-azure-ad-single-sign-on)**  -tooenable Twojego toouse użytkowników tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="fe6df-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="fe6df-144">**[Tworzenie użytkownika testowego usługi Azure AD](#creating-an-azure-ad-test-user)**  -tootest usługi Azure AD rejestracji jednokrotnej z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="fe6df-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="fe6df-145">**[Tworzenie użytkownika testowego OnDemand xMatters](#creating-a-xmatters-ondemand-test-user)**  -toohave odpowiednikiem Simona Britta w xMatters atrybutu, który jest połączony toohello usługi Azure AD reprezentację użytkownika.</span><span class="sxs-lookup"><span data-stu-id="fe6df-145">**[Creating a xMatters OnDemand test user](#creating-a-xmatters-ondemand-test-user)** - toohave a counterpart of Britta Simon in xMatters OnDemand that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="fe6df-146">**[Przypisanie użytkownika testowego hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Simona Britta toouse usługi Azure AD rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="fe6df-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="fe6df-147">**[Testowanie rejestracji jednokrotnej](#testing-single-sign-on)**  -tooverify czy hello konfiguracji działania.</span><span class="sxs-lookup"><span data-stu-id="fe6df-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="fe6df-148">Konfigurowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="fe6df-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="fe6df-149">W tej sekcji włączyć usługi Azure AD rejestracji jednokrotnej w hello portalu Azure i skonfigurować logowanie jednokrotne w sieci xMatters aplikacji na żądanie.</span><span class="sxs-lookup"><span data-stu-id="fe6df-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your xMatters OnDemand application.</span></span>

<span data-ttu-id="fe6df-150">**tooconfigure usługi Azure AD rejestracji jednokrotnej z xMatters na żądanie, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="fe6df-150">**tooconfigure Azure AD single sign-on with xMatters OnDemand, perform hello following steps:**</span></span>

1. <span data-ttu-id="fe6df-151">W portalu Azure na powitania hello **xMatters OnDemand** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.</span><span class="sxs-lookup"><span data-stu-id="fe6df-151">In hello Azure portal, on hello **xMatters OnDemand** application integration page, click **Single sign-on**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej][4]

2. <span data-ttu-id="fe6df-153">Na powitania **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** tooenable rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="fe6df-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-xmatters-ondemand-tutorial/tutorial_xmattersondemand_samlbase.png)

3. <span data-ttu-id="fe6df-155">Na powitania **xMatters OnDemand domeny i adres URL** sekcji, wykonaj następujące kroki hello:</span><span class="sxs-lookup"><span data-stu-id="fe6df-155">On hello **xMatters OnDemand Domain and URLs** section, perform hello following steps:</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-xmatters-ondemand-tutorial/tutorial_xmattersondemand_url.png)
    
    <span data-ttu-id="fe6df-157">a.</span><span class="sxs-lookup"><span data-stu-id="fe6df-157">a.</span></span> <span data-ttu-id="fe6df-158">W hello **identyfikator** tekstowym, wpisz adres URL za pomocą hello następującego wzorca:</span><span class="sxs-lookup"><span data-stu-id="fe6df-158">In hello **Identifier** textbox, type a URL using hello following pattern:</span></span>   
    | |
    |--|
    | `https://<companyname>.au1.xmatters.com.au/`|
    | `https://<companyname>.cs1.xmatters.com/`|
    | `https://<companyname>.xmatters.com/`|
    | `https://www.xmatters.com`|
    | `https://<companyname>.xmatters.com.au/`|

    <span data-ttu-id="fe6df-159">b.</span><span class="sxs-lookup"><span data-stu-id="fe6df-159">b.</span></span> <span data-ttu-id="fe6df-160">W hello **adres URL odpowiedzi** tekstowym, wpisz adres URL za pomocą hello następującego wzorca:</span><span class="sxs-lookup"><span data-stu-id="fe6df-160">In hello **Reply URL** textbox, type a URL using hello following pattern:</span></span>
    | |
    |--|
    | `https://<companyname>.au1.xmatters.com.au`|
    | `https://<companyname>.xmatters.com/sp/<instancename>`|
    | `https://<companyname>.cs1.xmatters.com/sp/<instancename>`|
    | `https://<companyname>.au1.xmatters.com.au/<instancename>`|

    > [!NOTE] 
    > <span data-ttu-id="fe6df-161">Wartości te nie są prawdziwe.</span><span class="sxs-lookup"><span data-stu-id="fe6df-161">These values are not real.</span></span> <span data-ttu-id="fe6df-162">Witaj rzeczywisty identyfikator i odpowiedzi adresu URL, należy zaktualizować te wartości.</span><span class="sxs-lookup"><span data-stu-id="fe6df-162">Update these values with hello actual Identifier and Reply URL.</span></span> <span data-ttu-id="fe6df-163">Skontaktuj się z [xMatters OnDemand obsługuje zespołu](https://www.xmatters.com/company/contact-us/) tooget tych wartości.</span><span class="sxs-lookup"><span data-stu-id="fe6df-163">Contact [xMatters OnDemand support team](https://www.xmatters.com/company/contact-us/) tooget these values.</span></span>

4. <span data-ttu-id="fe6df-164">Na powitania **certyfikat podpisywania SAML** kliknij **Certificate(Base64)** , a następnie zapisz hello plik certyfikatu lokalnie jako **c:\\XMatters OnDemand.cer**.</span><span class="sxs-lookup"><span data-stu-id="fe6df-164">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file locally as **c:\\XMatters OnDemand.cer**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-xmatters-ondemand-tutorial/tutorial_xmattersondemand_certificate.png)
    
    > [!IMPORTANT]
    > <span data-ttu-id="fe6df-166">Należy tooforward hello certyfikatu toohello [xMatters OnDemand obsługuje zespołu](https://www.xmatters.com/company/contact-us/).</span><span class="sxs-lookup"><span data-stu-id="fe6df-166">You need tooforward hello certificate toohello [xMatters OnDemand support team](https://www.xmatters.com/company/contact-us/).</span></span> <span data-ttu-id="fe6df-167">certyfikat Hello musi toobe przekazany przez zespół pomocy technicznej xMatters hello, zanim można sfinalizować hello pojedynczego logowania w konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="fe6df-167">hello certificate needs toobe uploaded by hello xMatters support team before you can finalize hello single sign-on configuration.</span></span> 

5. <span data-ttu-id="fe6df-168">Kliknij przycisk **zapisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="fe6df-168">Click **Save** button.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-xmatters-ondemand-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="fe6df-170">Na powitania **xMatters konfiguracji OnDemand** kliknij **skonfigurować xMatters OnDemand** tooopen **konfigurowania rejestracji** okna.</span><span class="sxs-lookup"><span data-stu-id="fe6df-170">On hello **xMatters OnDemand Configuration** section, click **Configure xMatters OnDemand** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="fe6df-171">Kopiuj hello **Sign-Out adres URL, identyfikator jednostki SAML i SAML pojedynczy znak na adres URL usługi** z hello **sekcji krótkimi opisami.**</span><span class="sxs-lookup"><span data-stu-id="fe6df-171">Copy hello **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-xmatters-ondemand-tutorial/tutorial_xmattersondemand_configure.png) 

7. <span data-ttu-id="fe6df-173">W oknie przeglądarki innej witryny sieci web Zaloguj się za tooyour XMatters OnDemand witryny firmy jako administrator.</span><span class="sxs-lookup"><span data-stu-id="fe6df-173">In a different web browser window, log in tooyour XMatters OnDemand company site as an administrator.</span></span>

8. <span data-ttu-id="fe6df-174">Witaj pasku narzędzi u góry hello, kliknij przycisk **administratora**, a następnie kliknij przycisk **szczegóły firmy** na pasku nawigacyjnym hello na powitania po lewej stronie.</span><span class="sxs-lookup"><span data-stu-id="fe6df-174">In hello toolbar on hello top, click **Admin**, and then click **Company Details** in hello navigation bar on hello left side.</span></span>
   
    <span data-ttu-id="fe6df-175">![Administrator](./media/active-directory-saas-xmatters-ondemand-tutorial/IC776795.png "administratora")</span><span class="sxs-lookup"><span data-stu-id="fe6df-175">![Admin](./media/active-directory-saas-xmatters-ondemand-tutorial/IC776795.png "Admin")</span></span>

9. <span data-ttu-id="fe6df-176">Na powitania **Konfiguracja SAML** wykonaj hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="fe6df-176">On hello **SAML Configuration** page, perform hello following steps:</span></span>
   
    <span data-ttu-id="fe6df-177">![Konfiguracja SAML](./media/active-directory-saas-xmatters-ondemand-tutorial/IC776796.png "Konfiguracja SAML")</span><span class="sxs-lookup"><span data-stu-id="fe6df-177">![SAML configuration](./media/active-directory-saas-xmatters-ondemand-tutorial/IC776796.png "SAML configuration")</span></span>
   
    <span data-ttu-id="fe6df-178">a.</span><span class="sxs-lookup"><span data-stu-id="fe6df-178">a.</span></span> <span data-ttu-id="fe6df-179">Wybierz **Włącz SAML**.</span><span class="sxs-lookup"><span data-stu-id="fe6df-179">Select **Enable SAML**.</span></span>
   
    <span data-ttu-id="fe6df-180">b.</span><span class="sxs-lookup"><span data-stu-id="fe6df-180">b.</span></span> <span data-ttu-id="fe6df-181">Wklej **identyfikator jednostki SAML**, która została skopiowana z hello portalu Azure do hello **identyfikator dostawcy tożsamości** pole tekstowe.</span><span class="sxs-lookup"><span data-stu-id="fe6df-181">Paste **SAML Entity ID**, which you have copied from hello Azure portal into hello **Identity Provider ID** textbox.</span></span>
   
    <span data-ttu-id="fe6df-182">c.</span><span class="sxs-lookup"><span data-stu-id="fe6df-182">c.</span></span> <span data-ttu-id="fe6df-183">Wklej **SAML pojedynczy znak na adres URL usługi**, która została skopiowana z hello portalu Azure do hello **jeden znak na adres URL** pola tekstowego.</span><span class="sxs-lookup"><span data-stu-id="fe6df-183">Paste **SAML Single Sign-On Service URL**, which you have copied from hello Azure portal into hello **Single Sign On URL** textbox.</span></span>
   
    <span data-ttu-id="fe6df-184">d.</span><span class="sxs-lookup"><span data-stu-id="fe6df-184">d.</span></span> <span data-ttu-id="fe6df-185">Wklej **Sign-Out adres URL**, która została skopiowana z hello portalu Azure do hello **pojedynczego adresu URL wylogowania** pola tekstowego.</span><span class="sxs-lookup"><span data-stu-id="fe6df-185">Paste **Sign-Out URL**, which you have copied from hello Azure portal into hello **Single Logout URL** textbox.</span></span>
   
    <span data-ttu-id="fe6df-186">e.</span><span class="sxs-lookup"><span data-stu-id="fe6df-186">e.</span></span> <span data-ttu-id="fe6df-187">Na stronie Szczegóły firmy hello u góry hello kliknij **Zapisz zmiany**.</span><span class="sxs-lookup"><span data-stu-id="fe6df-187">On hello Company Details page, at hello top, click **Save Changes**.</span></span>
    
    <span data-ttu-id="fe6df-188">![Szczegóły firmy](./media/active-directory-saas-xmatters-ondemand-tutorial/IC776797.png "firmy szczegóły")</span><span class="sxs-lookup"><span data-stu-id="fe6df-188">![Company details](./media/active-directory-saas-xmatters-ondemand-tutorial/IC776797.png "Company details")</span></span>

> [!TIP]
> <span data-ttu-id="fe6df-189">Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz hello [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji hello!</span><span class="sxs-lookup"><span data-stu-id="fe6df-189">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="fe6df-190">Po dodaniu tej aplikacji z hello **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij hello **rejestracji jednokrotnej** hello kartę i dostępu do osadzonych dokumentacji za pośrednictwem hello  **Konfiguracja** sekcji u dołu hello.</span><span class="sxs-lookup"><span data-stu-id="fe6df-190">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="fe6df-191">Więcej o hello osadzonych dokumentacji funkcji w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="fe6df-191">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="fe6df-192">Tworzenie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="fe6df-192">Creating an Azure AD test user</span></span>
<span data-ttu-id="fe6df-193">Celem Hello w tej sekcji jest toocreate użytkownika testowego, w portalu Azure o nazwie Simona Britta hello.</span><span class="sxs-lookup"><span data-stu-id="fe6df-193">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Tworzenie użytkowników usługi Azure AD][100]

<span data-ttu-id="fe6df-195">**toocreate użytkownika testowego w usłudze Azure AD, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="fe6df-195">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="fe6df-196">W hello **portalu Azure**na temat hello w lewym okienku nawigacji, kliknij przycisk **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="fe6df-196">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-xmatters-ondemand-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="fe6df-198">toodisplay hello listę użytkowników, przejdź zbyt**użytkowników i grup** i kliknij przycisk **wszyscy użytkownicy**.</span><span class="sxs-lookup"><span data-stu-id="fe6df-198">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-xmatters-ondemand-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="fe6df-200">Witaj tooopen **użytkownika** okna dialogowego, kliknij przycisk **Dodaj** u góry hello hello okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="fe6df-200">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-xmatters-ondemand-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="fe6df-202">Na powitania **użytkownika** okna dialogowego wykonaj hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="fe6df-202">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-xmatters-ondemand-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="fe6df-204">a.</span><span class="sxs-lookup"><span data-stu-id="fe6df-204">a.</span></span> <span data-ttu-id="fe6df-205">W hello **nazwa** pole tekstowe, typ **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="fe6df-205">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="fe6df-206">b.</span><span class="sxs-lookup"><span data-stu-id="fe6df-206">b.</span></span> <span data-ttu-id="fe6df-207">W hello **nazwy użytkownika** pole tekstowe, hello typu **adres e-mail** z BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="fe6df-207">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="fe6df-208">c.</span><span class="sxs-lookup"><span data-stu-id="fe6df-208">c.</span></span> <span data-ttu-id="fe6df-209">Wybierz **Pokaż hasło** i zanotuj wartość hello hello **hasło**.</span><span class="sxs-lookup"><span data-stu-id="fe6df-209">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="fe6df-210">d.</span><span class="sxs-lookup"><span data-stu-id="fe6df-210">d.</span></span> <span data-ttu-id="fe6df-211">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="fe6df-211">Click **Create**.</span></span>
 
### <a name="creating-a-xmatters-ondemand-test-user"></a><span data-ttu-id="fe6df-212">Tworzenie użytkownika testowego OnDemand xMatters</span><span class="sxs-lookup"><span data-stu-id="fe6df-212">Creating a xMatters OnDemand test user</span></span>

<span data-ttu-id="fe6df-213">W kolejności tooenable usługi Azure AD użytkownicy toolog w tooXMatters na żądanie musi być przygotowana do XMatters OnDemand.</span><span class="sxs-lookup"><span data-stu-id="fe6df-213">In order tooenable Azure AD users toolog in tooXMatters OnDemand, they must be provisioned into XMatters OnDemand.</span></span> <span data-ttu-id="fe6df-214">W przypadku hello XMatters OnDemand Inicjowanie obsługi to zadanie ręczne.</span><span class="sxs-lookup"><span data-stu-id="fe6df-214">In hello case of XMatters OnDemand, provisioning is a manual task.</span></span>

### <a name="tooprovision-a-user-accounts-perform-hello-following-steps"></a><span data-ttu-id="fe6df-215">tooprovision kont użytkowników, wykonaj hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="fe6df-215">tooprovision a user accounts, perform hello following steps:</span></span>
1. <span data-ttu-id="fe6df-216">Zaloguj się za tooyour **XMatters OnDemand** dzierżawy.</span><span class="sxs-lookup"><span data-stu-id="fe6df-216">Log in tooyour **XMatters OnDemand** tenant.</span></span>

2.  <span data-ttu-id="fe6df-217">Kliknij przycisk **użytkowników** kartę, a następnie kliknij przycisk **Dodaj użytkownika**.</span><span class="sxs-lookup"><span data-stu-id="fe6df-217">Click **Users** tab. and then click **Add User**.</span></span>
  
    <span data-ttu-id="fe6df-218">![Użytkownicy](./media/active-directory-saas-xmatters-ondemand-tutorial/IC781048.png "użytkowników")</span><span class="sxs-lookup"><span data-stu-id="fe6df-218">![Users](./media/active-directory-saas-xmatters-ondemand-tutorial/IC781048.png "Users")</span></span>

3. <span data-ttu-id="fe6df-219">W hello **dodać użytkownika** sekcji, wykonaj następujące kroki hello:</span><span class="sxs-lookup"><span data-stu-id="fe6df-219">In hello **Add a User** section, perform hello following steps:</span></span>
   
    <span data-ttu-id="fe6df-220">![Dodawanie użytkownika](./media/active-directory-saas-xmatters-ondemand-tutorial/IC781049.png "Dodawanie użytkownika")</span><span class="sxs-lookup"><span data-stu-id="fe6df-220">![Add a User](./media/active-directory-saas-xmatters-ondemand-tutorial/IC781049.png "Add a User")</span></span>

    <span data-ttu-id="fe6df-221">a.</span><span class="sxs-lookup"><span data-stu-id="fe6df-221">a.</span></span> <span data-ttu-id="fe6df-222">Wybierz **Active**.</span><span class="sxs-lookup"><span data-stu-id="fe6df-222">Select **Active**.</span></span>

    <span data-ttu-id="fe6df-223">b.</span><span class="sxs-lookup"><span data-stu-id="fe6df-223">b.</span></span> <span data-ttu-id="fe6df-224">W hello **identyfikator użytkownika** pole tekstowe, identyfikator użytkownika hello typu użytkownika, takich jak Brittasimon@contoso.com.</span><span class="sxs-lookup"><span data-stu-id="fe6df-224">In hello **User ID** textbox, type hello user id of user like Brittasimon@contoso.com.</span></span>
   
    <span data-ttu-id="fe6df-225">c.</span><span class="sxs-lookup"><span data-stu-id="fe6df-225">c.</span></span> <span data-ttu-id="fe6df-226">W hello **imię** pole tekstowe, typ imię użytkownika hello, takich jak Britta.</span><span class="sxs-lookup"><span data-stu-id="fe6df-226">In hello **First Name** textbox, type first name of hello user like Britta.</span></span>

    <span data-ttu-id="fe6df-227">d.</span><span class="sxs-lookup"><span data-stu-id="fe6df-227">d.</span></span> <span data-ttu-id="fe6df-228">W hello **nazwisko** tekstowym, wpisz nazwisko hello użytkownika, takich jak Simona.</span><span class="sxs-lookup"><span data-stu-id="fe6df-228">In hello **Last Name** textbox, type last name of hello user like Simon.</span></span>
    
    <span data-ttu-id="fe6df-229">e.</span><span class="sxs-lookup"><span data-stu-id="fe6df-229">e.</span></span> <span data-ttu-id="fe6df-230">W hello **lokacji** pole tekstowe, wprowadź hello prawidłowej lokacji prawidłowy Azure AD konta tooprovision.</span><span class="sxs-lookup"><span data-stu-id="fe6df-230">In hello **Site** textbox, Enter hello valid site of a valid Azure AD account you want tooprovision.</span></span>
    
    <span data-ttu-id="fe6df-231">f.</span><span class="sxs-lookup"><span data-stu-id="fe6df-231">f.</span></span> <span data-ttu-id="fe6df-232">Kliknij pozycję **Zapisz**.</span><span class="sxs-lookup"><span data-stu-id="fe6df-232">Click **Save**.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="fe6df-233">Przypisanie użytkownika testowego hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="fe6df-233">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="fe6df-234">W tej sekcji możesz włączyć toouse Simona Britta Azure logowania jednokrotnego za udzielanie dostępu tooxMatters na żądanie.</span><span class="sxs-lookup"><span data-stu-id="fe6df-234">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooxMatters OnDemand.</span></span>

![Przypisz użytkownika][200] 

<span data-ttu-id="fe6df-236">**tooassign tooxMatters Simona Britta na żądanie, wykonaj hello następujące kroki:**</span><span class="sxs-lookup"><span data-stu-id="fe6df-236">**tooassign Britta Simon tooxMatters OnDemand, perform hello following steps:**</span></span>

1. <span data-ttu-id="fe6df-237">W portalu Azure hello, otwórz widok aplikacji hello, a następnie przejdź do widoku katalogu toohello i przejść za**aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="fe6df-237">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Przypisz użytkownika][201] 

2. <span data-ttu-id="fe6df-239">Z listy aplikacji hello wybierz **xMatters OnDemand**.</span><span class="sxs-lookup"><span data-stu-id="fe6df-239">In hello applications list, select **xMatters OnDemand**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-xmatters-ondemand-tutorial/tutorial_xmattersondemand_app.png) 

3. <span data-ttu-id="fe6df-241">W menu powitania po lewej stronie powitania kliknij **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="fe6df-241">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Przypisz użytkownika][202] 

4. <span data-ttu-id="fe6df-243">Kliknij przycisk **Dodaj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="fe6df-243">Click **Add** button.</span></span> <span data-ttu-id="fe6df-244">Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="fe6df-244">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Przypisz użytkownika][203]

5. <span data-ttu-id="fe6df-246">Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** hello listy użytkowników.</span><span class="sxs-lookup"><span data-stu-id="fe6df-246">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="fe6df-247">Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="fe6df-247">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="fe6df-248">Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="fe6df-248">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="fe6df-249">Testowanie rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="fe6df-249">Testing single sign-on</span></span>

<span data-ttu-id="fe6df-250">W tej sekcji można przetestować konfiguracji usługi Azure AD pojedynczego logowania jednokrotnego przy użyciu hello panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="fe6df-250">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="fe6df-251">Po kliknięciu xMatters hello kafelka na żądanie w panelu dostępu hello, należy pobrać xMatters automatycznie zalogowane tooyour aplikacji na żądanie.</span><span class="sxs-lookup"><span data-stu-id="fe6df-251">When you click hello xMatters OnDemand tile in hello Access Panel, you should get automatically signed-on tooyour xMatters OnDemand application.</span></span>
<span data-ttu-id="fe6df-252">Aby uzyskać więcej informacji na temat panelu dostępu, zobacz [toohello wprowadzenie panelu dostępu](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="fe6df-252">For more information about the Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="fe6df-253">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="fe6df-253">Additional resources</span></span>

* [<span data-ttu-id="fe6df-254">Lista samouczków dotyczących tooIntegrate aplikacji SaaS w usłudze Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="fe6df-254">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="fe6df-255">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="fe6df-255">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-xmatters-ondemand-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-xmatters-ondemand-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-xmatters-ondemand-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-xmatters-ondemand-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-xmatters-ondemand-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-xmatters-ondemand-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-xmatters-ondemand-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-xmatters-ondemand-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-xmatters-ondemand-tutorial/tutorial_general_203.png

