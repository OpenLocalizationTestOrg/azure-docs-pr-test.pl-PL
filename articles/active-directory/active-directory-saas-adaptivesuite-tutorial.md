---
title: "Samouczek: Azure Active Directory integracji z pakietem adaptacyjną | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak tooconfigure logowanie jednokrotne między usługą Azure Active Directory i adaptacyjną Suite."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 13af9d00-116a-41b8-8ca0-4870b31e224c
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/22/2017
ms.author: jeedes
ms.openlocfilehash: af309c27ab74098c1e229c80adb11c96dc2774fb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-adaptive-suite"></a><span data-ttu-id="5b961-103">Samouczek: Integracji Azure Active Directory z adaptacyjną Suite</span><span class="sxs-lookup"><span data-stu-id="5b961-103">Tutorial: Azure Active Directory integration with Adaptive Suite</span></span>

<span data-ttu-id="5b961-104">Z tego samouczka, dowiesz się, jak toointegrate adaptacyjną Suite w usłudze Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="5b961-104">In this tutorial, you learn how toointegrate Adaptive Suite with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="5b961-105">Integrowanie adaptacyjną pakiet z usługą Azure AD zapewnia hello następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="5b961-105">Integrating Adaptive Suite with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="5b961-106">Można kontrolować w usłudze Azure AD, kto ma dostęp tooAdaptive Suite</span><span class="sxs-lookup"><span data-stu-id="5b961-106">You can control in Azure AD who has access tooAdaptive Suite</span></span>
- <span data-ttu-id="5b961-107">Można włączyć użytkownika użytkownicy tooautomatically get zalogowane tooAdaptive Suite (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="5b961-107">You can enable your users tooautomatically get signed-on tooAdaptive Suite (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="5b961-108">Możesz zarządzać kont w jednej centralnej lokalizacji - hello portalu Azure</span><span class="sxs-lookup"><span data-stu-id="5b961-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="5b961-109">Jeśli chcesz tooknow więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="5b961-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="5b961-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="5b961-110">Prerequisites</span></span>

<span data-ttu-id="5b961-111">tooconfigure integracji usługi Azure AD z adaptacyjną Suite należy hello następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="5b961-111">tooconfigure Azure AD integration with Adaptive Suite, you need hello following items:</span></span>

- <span data-ttu-id="5b961-112">Subskrypcję usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="5b961-112">An Azure AD subscription</span></span>
- <span data-ttu-id="5b961-113">Pakiet adaptacyjną jednokrotnego włączone subskrypcji</span><span class="sxs-lookup"><span data-stu-id="5b961-113">An Adaptive Suite single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="5b961-114">tootest hello kroków w tym samouczku, zaleca się przy użyciu środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="5b961-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="5b961-115">tootest hello kroki opisane w tym samouczku, należy stosować te zalecenia:</span><span class="sxs-lookup"><span data-stu-id="5b961-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="5b961-116">Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="5b961-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="5b961-117">Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz pobrać miesięczna wersja próbna [tutaj](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="5b961-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="5b961-118">Opis scenariusza</span><span class="sxs-lookup"><span data-stu-id="5b961-118">Scenario description</span></span>
<span data-ttu-id="5b961-119">W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym.</span><span class="sxs-lookup"><span data-stu-id="5b961-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="5b961-120">Scenariusz Hello opisane w tym samouczku składa się z dwóch głównych elementów:</span><span class="sxs-lookup"><span data-stu-id="5b961-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="5b961-121">Dodawanie pakietu adaptacyjną z galerii hello</span><span class="sxs-lookup"><span data-stu-id="5b961-121">Adding Adaptive Suite from hello gallery</span></span>
2. <span data-ttu-id="5b961-122">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="5b961-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-adaptive-suite-from-hello-gallery"></a><span data-ttu-id="5b961-123">Dodawanie pakietu adaptacyjną z galerii hello</span><span class="sxs-lookup"><span data-stu-id="5b961-123">Adding Adaptive Suite from hello gallery</span></span>
<span data-ttu-id="5b961-124">tooconfigure hello zintegrowania pakietu adaptacyjną usługi Azure AD, należy tooadd adaptacyjną pakiet z listy tooyour galerii hello zarządzanych aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="5b961-124">tooconfigure hello integration of Adaptive Suite into Azure AD, you need tooadd Adaptive Suite from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="5b961-125">**tooadd adaptacyjną pakiet z galerii hello wykonaj hello następujące kroki:**</span><span class="sxs-lookup"><span data-stu-id="5b961-125">**tooadd Adaptive Suite from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="5b961-126">W hello  **[portalu Azure](https://portal.azure.com)**na temat hello panelu nawigacji po lewej stronie, kliknij przycisk **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="5b961-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Usługa Active Directory][1]

2. <span data-ttu-id="5b961-128">Przejdź za**aplikacje dla przedsiębiorstw**.</span><span class="sxs-lookup"><span data-stu-id="5b961-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="5b961-129">Następnie przejdź zbyt**wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="5b961-129">Then go too**All applications**.</span></span>

    ![Aplikacje][2]
    
3. <span data-ttu-id="5b961-131">tooadd nową aplikację, kliknij przycisk **nowej aplikacji** przycisk u góry hello okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="5b961-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplikacje][3]

4. <span data-ttu-id="5b961-133">W polu wyszukiwania hello wpisz **Suite adaptacyjną**.</span><span class="sxs-lookup"><span data-stu-id="5b961-133">In hello search box, type **Adaptive Suite**.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-adaptivesuite-tutorial/tutorial_adaptivesuite_search.png)

5. <span data-ttu-id="5b961-135">W panelu wyników hello, wybierz **Suite adaptacyjną**, a następnie kliknij przycisk **Dodaj** przycisk aplikacji hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="5b961-135">In hello results panel, select **Adaptive Suite**, and then click **Add** button tooadd hello application.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-adaptivesuite-tutorial/tutorial_adaptivesuite_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="5b961-137">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="5b961-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="5b961-138">W tej sekcji możesz skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z adaptacyjną pakietu na podstawie użytkownika testowego, nazywany "Britta Simona".</span><span class="sxs-lookup"><span data-stu-id="5b961-138">In this section, you configure and test Azure AD single sign-on with Adaptive Suite based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="5b961-139">Dla pojedynczego logowania jednokrotnego toowork usługi Azure AD musi tooknow hello użytkownika odpowiednikiem pakietu adaptacyjną jest tooa użytkownika w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="5b961-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Adaptive Suite is tooa user in Azure AD.</span></span> <span data-ttu-id="5b961-140">Innymi słowy relację łącza między użytkownika usługi Azure AD i hello użytkownikowi pakietu adaptacyjną musi toobe ustanowione.</span><span class="sxs-lookup"><span data-stu-id="5b961-140">In other words, a link relationship between an Azure AD user and hello related user in Adaptive Suite needs toobe established.</span></span>

<span data-ttu-id="5b961-141">Adaptacyjną pakietu, należy przypisać wartość hello hello **nazwy użytkownika** w usłudze Azure AD jako wartość hello hello **Username** tooestablish hello łącze relacji.</span><span class="sxs-lookup"><span data-stu-id="5b961-141">In Adaptive Suite, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="5b961-142">tooconfigure i test usługi Azure AD rejestracji jednokrotnej z adaptacyjną Suite należy hello toocomplete po bloków konstrukcyjnych:</span><span class="sxs-lookup"><span data-stu-id="5b961-142">tooconfigure and test Azure AD single sign-on with Adaptive Suite, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="5b961-143">**[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configuring-azure-ad-single-sign-on)**  -tooenable Twojego toouse użytkowników tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="5b961-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="5b961-144">**[Tworzenie użytkownika testowego usługi Azure AD](#creating-an-azure-ad-test-user)**  -tootest usługi Azure AD rejestracji jednokrotnej z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="5b961-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="5b961-145">**[Tworzenie użytkownika testowego adaptacyjną Suite](#creating-an-adaptive-suite-test-user)**  -toohave odpowiednikiem Simona Britta pakietu adaptacyjną, który jest połączony toohello usługi Azure AD reprezentację użytkownika.</span><span class="sxs-lookup"><span data-stu-id="5b961-145">**[Creating an Adaptive Suite test user](#creating-an-adaptive-suite-test-user)** - toohave a counterpart of Britta Simon in Adaptive Suite that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="5b961-146">**[Przypisanie użytkownika testowego hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Simona Britta toouse usługi Azure AD rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="5b961-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="5b961-147">**[Testowanie rejestracji jednokrotnej](#testing-single-sign-on)**  -tooverify czy hello konfiguracji działania.</span><span class="sxs-lookup"><span data-stu-id="5b961-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="5b961-148">Konfigurowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="5b961-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="5b961-149">W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w hello portalu Azure i skonfigurować logowanie jednokrotne adaptacyjną pakietu aplikacji.</span><span class="sxs-lookup"><span data-stu-id="5b961-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Adaptive Suite application.</span></span>

<span data-ttu-id="5b961-150">**tooconfigure usługi Azure AD rejestracji jednokrotnej z adaptacyjną pakiet, wykonaj hello następujące kroki:**</span><span class="sxs-lookup"><span data-stu-id="5b961-150">**tooconfigure Azure AD single sign-on with Adaptive Suite, perform hello following steps:**</span></span>

1. <span data-ttu-id="5b961-151">W portalu Azure na powitania hello **Suite adaptacyjną** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.</span><span class="sxs-lookup"><span data-stu-id="5b961-151">In hello Azure portal, on hello **Adaptive Suite** application integration page, click **Single sign-on**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej][4]

2. <span data-ttu-id="5b961-153">Na powitania **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** tooenable rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="5b961-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-adaptivesuite-tutorial/tutorial_adaptivesuite_samlbase.png)

3. <span data-ttu-id="5b961-155">Na powitania **adaptacyjną domeny Suite i adres URL** sekcji, wykonaj następujące kroki hello:</span><span class="sxs-lookup"><span data-stu-id="5b961-155">On hello **Adaptive Suite Domain and URLs** section, perform hello following steps:</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-adaptivesuite-tutorial/tutorial_adaptivesuite_url.png)

    <span data-ttu-id="5b961-157">W hello **adres URL odpowiedzi** tekstowym, wpisz adres URL za pomocą hello następującego wzorca:`https://login.adaptiveinsights.com:443/samlsso/<unique-id>`</span><span class="sxs-lookup"><span data-stu-id="5b961-157">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://login.adaptiveinsights.com:443/samlsso/<unique-id>`</span></span>

    >[!NOTE]
    > <span data-ttu-id="5b961-158">Tę wartość można uzyskać od hello adaptacyjną Suite **ustawienia logowania jednokrotnego SAML** strony.</span><span class="sxs-lookup"><span data-stu-id="5b961-158">You can get this value from hello Adaptive Suite’s **SAML SSO Settings** page.</span></span>
    >  

4. <span data-ttu-id="5b961-159">Na powitania **certyfikat podpisywania SAML** kliknij **certyfikatu (Base64)** , a następnie zapisz plik certyfikatu hello na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="5b961-159">On hello **SAML Signing Certificate** section, click **Certificate (Base64)** and then save hello certificate file on your computer.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-adaptivesuite-tutorial/tutorial_adaptivesuite_certificate.png) 

5. <span data-ttu-id="5b961-161">Kliknij przycisk **zapisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="5b961-161">Click **Save** button.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-adaptivesuite-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="5b961-163">Na powitania **adaptacyjną konfiguracji pakietu** kliknij **skonfigurować pakiet adaptacyjną** tooopen **Konfigurowanie logowania jednokrotnego** okna.</span><span class="sxs-lookup"><span data-stu-id="5b961-163">On hello **Adaptive Suite Configuration** section, click **Configure Adaptive Suite** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="5b961-164">Kopiuj hello **identyfikator jednostki SAML i SAML pojedynczy znak na adres URL usługi** z hello **sekcji krótkimi opisami.**</span><span class="sxs-lookup"><span data-stu-id="5b961-164">Copy hello **SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-adaptivesuite-tutorial/tutorial_adaptivesuite_configure.png) 

7. <span data-ttu-id="5b961-166">W oknie przeglądarki innej witryny sieci web Zaloguj się w witrynie firmy adaptacyjną Suite tooyour jako administrator.</span><span class="sxs-lookup"><span data-stu-id="5b961-166">In a different web browser window, log in tooyour Adaptive Suite company site as an administrator.</span></span>

8. <span data-ttu-id="5b961-167">Przejdź za**Admin**.</span><span class="sxs-lookup"><span data-stu-id="5b961-167">Go too**Admin**.</span></span>
   
    <span data-ttu-id="5b961-168">![Administrator](./media/active-directory-saas-adaptivesuite-tutorial/IC805644.png "administratora")</span><span class="sxs-lookup"><span data-stu-id="5b961-168">![Admin](./media/active-directory-saas-adaptivesuite-tutorial/IC805644.png "Admin")</span></span>

9. <span data-ttu-id="5b961-169">W hello **użytkownikami i rolami** kliknij **Zarządzaj ustawieniami logowania jednokrotnego SAML**.</span><span class="sxs-lookup"><span data-stu-id="5b961-169">In hello **Users and Roles** section, click **Manage SAML SSO Settings**.</span></span>
   
    <span data-ttu-id="5b961-170">![Zarządzanie ustawieniami logowania jednokrotnego SAML](./media/active-directory-saas-adaptivesuite-tutorial/IC805645.png "Zarządzanie ustawieniami logowania jednokrotnego SAML")</span><span class="sxs-lookup"><span data-stu-id="5b961-170">![Manage SAML SSO Settings](./media/active-directory-saas-adaptivesuite-tutorial/IC805645.png "Manage SAML SSO Settings")</span></span>

10. <span data-ttu-id="5b961-171">Na powitania **ustawienia logowania jednokrotnego SAML** wykonaj hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="5b961-171">On hello **SAML SSO Settings** page, perform hello following steps:</span></span>
   
    <span data-ttu-id="5b961-172">![Ustawienia logowania jednokrotnego SAML](./media/active-directory-saas-adaptivesuite-tutorial/IC805646.png "ustawienia logowania jednokrotnego SAML")</span><span class="sxs-lookup"><span data-stu-id="5b961-172">![SAML SSO Settings](./media/active-directory-saas-adaptivesuite-tutorial/IC805646.png "SAML SSO Settings")</span></span>

    <span data-ttu-id="5b961-173">a.</span><span class="sxs-lookup"><span data-stu-id="5b961-173">a.</span></span> <span data-ttu-id="5b961-174">W hello **Nazwa dostawcy tożsamości** tekstowym, wpisz nazwę dla danej konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="5b961-174">In hello **Identity provider name** textbox, type a name for your configuration.</span></span>
    
    <span data-ttu-id="5b961-175">b.</span><span class="sxs-lookup"><span data-stu-id="5b961-175">b.</span></span> <span data-ttu-id="5b961-176">Wklej hello **identyfikator jednostki SAML** wartość skopiowany z portalu Azure do hello **dostawcy tożsamości identyfikator jednostki** pola tekstowego.</span><span class="sxs-lookup"><span data-stu-id="5b961-176">Paste hello **SAML Entity ID** value copied from Azure portal into hello **Identity provider Entity ID** textbox.</span></span>
  
    <span data-ttu-id="5b961-177">c.</span><span class="sxs-lookup"><span data-stu-id="5b961-177">c.</span></span> <span data-ttu-id="5b961-178">Wklej hello **SAML pojedynczy znak na adres URL usługi** wartość skopiowany z portalu Azure do hello **dostawcy tożsamości adresu URL logowania jednokrotnego** pola tekstowego.</span><span class="sxs-lookup"><span data-stu-id="5b961-178">Paste hello **SAML Single Sign-On Service URL** value copied from Azure portal into hello **Identity provider SSO URL** textbox.</span></span>
  
    <span data-ttu-id="5b961-179">d.</span><span class="sxs-lookup"><span data-stu-id="5b961-179">d.</span></span> <span data-ttu-id="5b961-180">Wklej hello **SAML pojedynczy znak na adres URL usługi** wartość skopiowany z portalu Azure do hello **niestandardowy adres URL wylogowania** pola tekstowego.</span><span class="sxs-lookup"><span data-stu-id="5b961-180">Paste hello **SAML Single Sign-On Service URL** value copied from Azure portal into hello **Custom logout URL** textbox.</span></span>
  
    <span data-ttu-id="5b961-181">e.</span><span class="sxs-lookup"><span data-stu-id="5b961-181">e.</span></span> <span data-ttu-id="5b961-182">tooupload pobranego certyfikatu, kliknij przycisk **wybierz plik**.</span><span class="sxs-lookup"><span data-stu-id="5b961-182">tooupload your downloaded certificate, click **Choose file**.</span></span>
  
    <span data-ttu-id="5b961-183">f.</span><span class="sxs-lookup"><span data-stu-id="5b961-183">f.</span></span> <span data-ttu-id="5b961-184">Wybierz poniżej powitania dla:</span><span class="sxs-lookup"><span data-stu-id="5b961-184">Select hello following, for:</span></span>
    * <span data-ttu-id="5b961-185">**Identyfikator użytkownika SAML**, wybierz pozycję **nazwy użytkownika adaptacyjną Insights**.</span><span class="sxs-lookup"><span data-stu-id="5b961-185">**SAML user id**, select **User’s Adaptive Insights user name**.</span></span>
    * <span data-ttu-id="5b961-186">**Lokalizacja identyfikator użytkownika SAML**, wybierz pozycję **identyfikatora użytkownika w NameID podmiotu**.</span><span class="sxs-lookup"><span data-stu-id="5b961-186">**SAML user id location**, select **User id in NameID of Subject**.</span></span>
    * <span data-ttu-id="5b961-187">**Format SAML NameID**, wybierz pozycję **adres E-mail**.</span><span class="sxs-lookup"><span data-stu-id="5b961-187">**SAML NameID format**, select **Email address**.</span></span>
    * <span data-ttu-id="5b961-188">**Włącz SAML**, wybierz pozycję **Zezwalaj logowania jednokrotnego SAML i bezpośrednie logowanie adaptacyjną Insights**.</span><span class="sxs-lookup"><span data-stu-id="5b961-188">**Enable SAML**, select **Allow SAML SSO and direct Adaptive Insights login**.</span></span>
    
    <span data-ttu-id="5b961-189">g.</span><span class="sxs-lookup"><span data-stu-id="5b961-189">g.</span></span> <span data-ttu-id="5b961-190">Kliknij pozycję **Zapisz**.</span><span class="sxs-lookup"><span data-stu-id="5b961-190">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="5b961-191">Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz hello [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji hello!</span><span class="sxs-lookup"><span data-stu-id="5b961-191">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="5b961-192">Po dodaniu tej aplikacji z hello **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij hello **rejestracji jednokrotnej** hello kartę i dostępu do osadzonych dokumentacji za pośrednictwem hello  **Konfiguracja** sekcji u dołu hello.</span><span class="sxs-lookup"><span data-stu-id="5b961-192">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="5b961-193">Więcej o hello osadzonych dokumentacji funkcji w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="5b961-193">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="5b961-194">Tworzenie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="5b961-194">Creating an Azure AD test user</span></span>
<span data-ttu-id="5b961-195">Celem Hello w tej sekcji jest toocreate użytkownika testowego, w portalu Azure o nazwie Simona Britta hello.</span><span class="sxs-lookup"><span data-stu-id="5b961-195">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Tworzenie użytkowników usługi Azure AD][100]

<span data-ttu-id="5b961-197">**toocreate użytkownika testowego w usłudze Azure AD, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="5b961-197">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="5b961-198">W hello **portalu Azure**na temat hello w lewym okienku nawigacji, kliknij przycisk **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="5b961-198">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-adaptivesuite-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="5b961-200">toodisplay hello listę użytkowników, przejdź zbyt**użytkowników i grup** i kliknij przycisk **wszyscy użytkownicy**.</span><span class="sxs-lookup"><span data-stu-id="5b961-200">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-adaptivesuite-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="5b961-202">Witaj tooopen **użytkownika** okna dialogowego, kliknij przycisk **Dodaj** u góry hello hello okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="5b961-202">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-adaptivesuite-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="5b961-204">Na powitania **użytkownika** okna dialogowego wykonaj hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="5b961-204">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-adaptivesuite-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="5b961-206">a.</span><span class="sxs-lookup"><span data-stu-id="5b961-206">a.</span></span> <span data-ttu-id="5b961-207">W hello **nazwa** pole tekstowe, typ **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="5b961-207">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="5b961-208">b.</span><span class="sxs-lookup"><span data-stu-id="5b961-208">b.</span></span> <span data-ttu-id="5b961-209">W hello **nazwy użytkownika** pole tekstowe, hello typu **adres e-mail** z BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="5b961-209">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="5b961-210">c.</span><span class="sxs-lookup"><span data-stu-id="5b961-210">c.</span></span> <span data-ttu-id="5b961-211">Wybierz **Pokaż hasło** i zanotuj wartość hello hello **hasło**.</span><span class="sxs-lookup"><span data-stu-id="5b961-211">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="5b961-212">d.</span><span class="sxs-lookup"><span data-stu-id="5b961-212">d.</span></span> <span data-ttu-id="5b961-213">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="5b961-213">Click **Create**.</span></span>
 
### <a name="creating-an-adaptive-suite-test-user"></a><span data-ttu-id="5b961-214">Tworzenie użytkownika testowego adaptacyjną Suite</span><span class="sxs-lookup"><span data-stu-id="5b961-214">Creating an Adaptive Suite test user</span></span>

<span data-ttu-id="5b961-215">toolog użytkowników tooenable usługi Azure AD w tooAdaptive Suite muszą mieć przydzielone do adaptacyjnego Suite.</span><span class="sxs-lookup"><span data-stu-id="5b961-215">tooenable Azure AD users toolog in tooAdaptive Suite, they must be provisioned into Adaptive Suite.</span></span>  

* <span data-ttu-id="5b961-216">W przypadku hello pakietu adaptacyjną Inicjowanie obsługi to zadanie ręczne.</span><span class="sxs-lookup"><span data-stu-id="5b961-216">In hello case of Adaptive Suite, provisioning is a manual task.</span></span>

<span data-ttu-id="5b961-217">**tooconfigure aprowizacji użytkowników, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="5b961-217">**tooconfigure user provisioning, perform hello following steps:**</span></span> 

1. <span data-ttu-id="5b961-218">Zaloguj się za tooyour **Suite adaptacyjną** witryny firmy jako administrator.</span><span class="sxs-lookup"><span data-stu-id="5b961-218">Log in tooyour **Adaptive Suite** company site as an administrator.</span></span>
2. <span data-ttu-id="5b961-219">Przejdź za**Admin**.</span><span class="sxs-lookup"><span data-stu-id="5b961-219">Go too**Admin**.</span></span>
   
   <span data-ttu-id="5b961-220">![Administrator](./media/active-directory-saas-adaptivesuite-tutorial/IC805644.png "administratora")</span><span class="sxs-lookup"><span data-stu-id="5b961-220">![Admin](./media/active-directory-saas-adaptivesuite-tutorial/IC805644.png "Admin")</span></span>
3. <span data-ttu-id="5b961-221">W hello **użytkownikami i rolami** kliknij **Dodaj użytkownika**.</span><span class="sxs-lookup"><span data-stu-id="5b961-221">In hello **Users and Roles** section, click **Add User**.</span></span>
   
   <span data-ttu-id="5b961-222">![Dodaj użytkownika](./media/active-directory-saas-adaptivesuite-tutorial/IC805648.png "Dodaj użytkownika")</span><span class="sxs-lookup"><span data-stu-id="5b961-222">![Add User](./media/active-directory-saas-adaptivesuite-tutorial/IC805648.png "Add User")</span></span>
4. <span data-ttu-id="5b961-223">W hello **nowego użytkownika** sekcji, wykonaj następujące kroki hello:</span><span class="sxs-lookup"><span data-stu-id="5b961-223">In hello **New User** section, perform hello following steps:</span></span>
   
   <span data-ttu-id="5b961-224">![Przedstawia](./media/active-directory-saas-adaptivesuite-tutorial/IC805649.png "przesyłania")</span><span class="sxs-lookup"><span data-stu-id="5b961-224">![Submit](./media/active-directory-saas-adaptivesuite-tutorial/IC805649.png "Submit")</span></span>   

   <span data-ttu-id="5b961-225">a.</span><span class="sxs-lookup"><span data-stu-id="5b961-225">a.</span></span> <span data-ttu-id="5b961-226">Hello typu **nazwa**, **logowania**, **E-mail**, **hasło** z prawidłowym użytkownikiem usługi Azure Active Directory ma tooprovision do hello powiązane pola tekstowe.</span><span class="sxs-lookup"><span data-stu-id="5b961-226">Type hello **Name**, **Login**, **Email**, **Password** of a valid Azure Active Directory user you want tooprovision into hello related textboxes.</span></span>
  
   <span data-ttu-id="5b961-227">b.</span><span class="sxs-lookup"><span data-stu-id="5b961-227">b.</span></span> <span data-ttu-id="5b961-228">Wybierz **roli**.</span><span class="sxs-lookup"><span data-stu-id="5b961-228">Select a **Role**.</span></span>
  
   <span data-ttu-id="5b961-229">c.</span><span class="sxs-lookup"><span data-stu-id="5b961-229">c.</span></span> <span data-ttu-id="5b961-230">Kliknij przycisk **przesłać**.</span><span class="sxs-lookup"><span data-stu-id="5b961-230">Click **Submit**.</span></span>

>[!NOTE]
><span data-ttu-id="5b961-231">Możesz użyć innych adaptacyjną Suite użytkownika konta tworzenia narzędzi lub interfejsów API dostarczonych przez tooprovision Suite adaptacyjną kont użytkowników usługi AAD.</span><span class="sxs-lookup"><span data-stu-id="5b961-231">You can use any other Adaptive Suite user account creation tools or APIs provided by Adaptive Suite tooprovision AAD user accounts.</span></span>
>  

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="5b961-232">Przypisanie użytkownika testowego hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="5b961-232">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="5b961-233">W tej sekcji możesz włączyć toouse Simona Britta Azure logowania jednokrotnego za udzielanie dostępu tooAdaptive Suite.</span><span class="sxs-lookup"><span data-stu-id="5b961-233">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooAdaptive Suite.</span></span>

![Przypisz użytkownika][200] 

<span data-ttu-id="5b961-235">**tooassign tooAdaptive Simona Britta pakiet, wykonaj hello następujące kroki:**</span><span class="sxs-lookup"><span data-stu-id="5b961-235">**tooassign Britta Simon tooAdaptive Suite, perform hello following steps:**</span></span>

1. <span data-ttu-id="5b961-236">W portalu Azure hello, otwórz widok aplikacji hello, a następnie przejdź do widoku katalogu toohello i przejść za**aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="5b961-236">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Przypisz użytkownika][201] 

2. <span data-ttu-id="5b961-238">Z listy aplikacji hello wybierz **Suite adaptacyjną**.</span><span class="sxs-lookup"><span data-stu-id="5b961-238">In hello applications list, select **Adaptive Suite**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-adaptivesuite-tutorial/tutorial_adaptivesuite_app.png) 

3. <span data-ttu-id="5b961-240">W menu powitania po lewej stronie powitania kliknij **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="5b961-240">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Przypisz użytkownika][202] 

4. <span data-ttu-id="5b961-242">Kliknij przycisk **Dodaj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="5b961-242">Click **Add** button.</span></span> <span data-ttu-id="5b961-243">Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="5b961-243">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Przypisz użytkownika][203]

5. <span data-ttu-id="5b961-245">Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** hello listy użytkowników.</span><span class="sxs-lookup"><span data-stu-id="5b961-245">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="5b961-246">Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="5b961-246">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="5b961-247">Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="5b961-247">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="5b961-248">Testowanie rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="5b961-248">Testing single sign-on</span></span>

<span data-ttu-id="5b961-249">Celem Hello w tej sekcji jest tootest z usługi Microsoft Azure AD rejestracji jednokrotnej konfiguracji przy użyciu hello panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="5b961-249">hello objective of this section is tootest your Microsoft Azure AD Single Sign-On configuration using hello Access Panel.</span></span>

<span data-ttu-id="5b961-250">Po kliknięciu kafelka adaptacyjną Suite hello w hello Panel dostępu, należy pobrać automatycznie zalogowane tooyour adaptacyjną pakietu aplikacji.</span><span class="sxs-lookup"><span data-stu-id="5b961-250">When you click hello Adaptive Suite tile in hello Access Panel, you should get automatically signed-on tooyour Adaptive Suite application.</span></span>


## <a name="additional-resources"></a><span data-ttu-id="5b961-251">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="5b961-251">Additional resources</span></span>

* [<span data-ttu-id="5b961-252">Lista samouczków dotyczących tooIntegrate aplikacji SaaS w usłudze Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="5b961-252">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="5b961-253">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="5b961-253">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-adaptivesuite-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-adaptivesuite-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-adaptivesuite-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-adaptivesuite-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-adaptivesuite-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-adaptivesuite-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-adaptivesuite-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-adaptivesuite-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-adaptivesuite-tutorial/tutorial_general_203.png

