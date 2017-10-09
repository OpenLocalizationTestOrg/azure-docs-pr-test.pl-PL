---
title: 'Samouczek: Integracji Azure Active Directory z DocuSign | Dokumentacja firmy Microsoft'
description: "Dowiedz się, jak tooconfigure logowanie jednokrotne między usługą Azure Active Directory i DocuSign."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: a691288b-84c1-40fb-84bd-5b06878865f0
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/10/2017
ms.author: jeedes
ms.openlocfilehash: e4ef40b8f5af20d811d8d806d2bd7e2039c55052
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-docusign"></a><span data-ttu-id="44efc-103">Samouczek: Integracji Azure Active Directory z DocuSign</span><span class="sxs-lookup"><span data-stu-id="44efc-103">Tutorial: Azure Active Directory integration with DocuSign</span></span>

<span data-ttu-id="44efc-104">Z tego samouczka, dowiesz się, jak toointegrate DocuSign w usłudze Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="44efc-104">In this tutorial, you learn how toointegrate DocuSign with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="44efc-105">Integracja z usługą Azure AD DocuSign zapewnia hello następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="44efc-105">Integrating DocuSign with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="44efc-106">Można kontrolować w usłudze Azure AD, kto ma dostęp do tooDocuSign</span><span class="sxs-lookup"><span data-stu-id="44efc-106">You can control in Azure AD who has access tooDocuSign</span></span>
- <span data-ttu-id="44efc-107">Można włączyć użytkownika użytkownicy tooautomatically get zalogowane tooDocuSign (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="44efc-107">You can enable your users tooautomatically get signed-on tooDocuSign (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="44efc-108">Możesz zarządzać kont w jednej centralnej lokalizacji - hello portalu Azure</span><span class="sxs-lookup"><span data-stu-id="44efc-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="44efc-109">Jeśli chcesz tooknow więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="44efc-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="44efc-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="44efc-110">Prerequisites</span></span>

<span data-ttu-id="44efc-111">tooconfigure integracji z usługą Azure AD z DocuSign należy hello następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="44efc-111">tooconfigure Azure AD integration with DocuSign, you need hello following items:</span></span>

- <span data-ttu-id="44efc-112">Subskrypcję usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="44efc-112">An Azure AD subscription</span></span>
- <span data-ttu-id="44efc-113">DocuSign logowanie jednokrotne włączone subskrypcji</span><span class="sxs-lookup"><span data-stu-id="44efc-113">A DocuSign single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="44efc-114">tootest hello kroków w tym samouczku, zaleca się przy użyciu środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="44efc-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="44efc-115">tootest hello kroki opisane w tym samouczku, należy stosować te zalecenia:</span><span class="sxs-lookup"><span data-stu-id="44efc-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="44efc-116">Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="44efc-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="44efc-117">Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz pobrać miesięczna wersja próbna [tutaj](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="44efc-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="44efc-118">Opis scenariusza</span><span class="sxs-lookup"><span data-stu-id="44efc-118">Scenario description</span></span>
<span data-ttu-id="44efc-119">W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym.</span><span class="sxs-lookup"><span data-stu-id="44efc-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="44efc-120">Scenariusz Hello opisane w tym samouczku składa się z dwóch głównych elementów:</span><span class="sxs-lookup"><span data-stu-id="44efc-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="44efc-121">Dodawanie DocuSign z galerii hello</span><span class="sxs-lookup"><span data-stu-id="44efc-121">Adding DocuSign from hello gallery</span></span>
2. <span data-ttu-id="44efc-122">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="44efc-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-docusign-from-hello-gallery"></a><span data-ttu-id="44efc-123">Dodawanie DocuSign z galerii hello</span><span class="sxs-lookup"><span data-stu-id="44efc-123">Adding DocuSign from hello gallery</span></span>
<span data-ttu-id="44efc-124">tooconfigure hello integracji DocuSign do usługi Azure AD, należy tooadd DocuSign z hello galerii tooyour listę zarządzanych aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="44efc-124">tooconfigure hello integration of DocuSign into Azure AD, you need tooadd DocuSign from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="44efc-125">**tooadd DocuSign z galerii hello, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="44efc-125">**tooadd DocuSign from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="44efc-126">W hello  **[portalu Azure](https://portal.azure.com)**na temat hello panelu nawigacji po lewej stronie, kliknij przycisk **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="44efc-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Usługa Active Directory][1]

2. <span data-ttu-id="44efc-128">Przejdź za**aplikacje dla przedsiębiorstw**.</span><span class="sxs-lookup"><span data-stu-id="44efc-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="44efc-129">Następnie przejdź zbyt**wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="44efc-129">Then go too**All applications**.</span></span>

    ![Aplikacje][2]
    
3. <span data-ttu-id="44efc-131">Kliknij przycisk **nowej aplikacji** przycisk u góry hello hello okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="44efc-131">Click **New application** button on hello top of hello dialog.</span></span>

    ![Aplikacje][3]

4. <span data-ttu-id="44efc-133">W polu wyszukiwania hello wpisz **DocuSign**.</span><span class="sxs-lookup"><span data-stu-id="44efc-133">In hello search box, type **DocuSign**.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-docusign-tutorial/tutorial_docusign_search.png)

5. <span data-ttu-id="44efc-135">W panelu wyników hello zaznacz **DocuSign**, a następnie kliknij przycisk **Dodaj** przycisk aplikacji hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="44efc-135">In hello results panel, select **DocuSign**, and then click **Add** button tooadd hello application.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-docusign-tutorial/tutorial_docusign_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="44efc-137">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="44efc-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="44efc-138">W tej sekcji możesz skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z DocuSign na podstawie użytkownika testowego, nazywany "Britta Simona".</span><span class="sxs-lookup"><span data-stu-id="44efc-138">In this section, you configure and test Azure AD single sign-on with DocuSign based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="44efc-139">Dla pojedynczego logowania jednokrotnego toowork usługi Azure AD musi tooknow użytkownika odpowiednikiem hello w DocuSign jest tooa użytkownika w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="44efc-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in DocuSign is tooa user in Azure AD.</span></span> <span data-ttu-id="44efc-140">Innymi słowy relację łącza między użytkownika usługi Azure AD i hello użytkownikowi w DocuSign musi toobe ustanowione.</span><span class="sxs-lookup"><span data-stu-id="44efc-140">In other words, a link relationship between an Azure AD user and hello related user in DocuSign needs toobe established.</span></span>

<span data-ttu-id="44efc-141">Ta relacja łącza zostanie nawiązane, przypisując wartość hello hello **nazwy użytkownika** w usłudze Azure AD jako wartość hello hello **Username** w DocuSign.</span><span class="sxs-lookup"><span data-stu-id="44efc-141">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in DocuSign.</span></span>

<span data-ttu-id="44efc-142">tooconfigure i testowych usługi Azure AD rejestracji jednokrotnej z DocuSign, należy po bloków konstrukcyjnych hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="44efc-142">tooconfigure and test Azure AD single sign-on with DocuSign, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="44efc-143">**[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configuring-azure-ad-single-sign-on)**  -tooenable Twojego toouse użytkowników tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="44efc-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="44efc-144">**[Tworzenie użytkownika testowego usługi Azure AD](#creating-an-azure-ad-test-user)**  -tootest usługi Azure AD rejestracji jednokrotnej z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="44efc-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="44efc-145">**[Tworzenie użytkownika testowego DocuSign](#creating-a-docusign-test-user)**  -toohave odpowiednikiem Simona Britta w DocuSign, który jest połączony toohello usługi Azure AD reprezentację użytkownika.</span><span class="sxs-lookup"><span data-stu-id="44efc-145">**[Creating a DocuSign test user](#creating-a-docusign-test-user)** - toohave a counterpart of Britta Simon in DocuSign that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="44efc-146">**[Przypisanie użytkownika testowego hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Simona Britta toouse usługi Azure AD rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="44efc-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="44efc-147">**[Testowanie rejestracji jednokrotnej](#testing-single-sign-on)**  -tooverify czy hello konfiguracji działania.</span><span class="sxs-lookup"><span data-stu-id="44efc-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="44efc-148">Konfigurowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="44efc-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="44efc-149">W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w portalu Azure hello i skonfigurować logowanie jednokrotne w aplikacji DocuSign.</span><span class="sxs-lookup"><span data-stu-id="44efc-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your DocuSign application.</span></span>

<span data-ttu-id="44efc-150">**tooconfigure usługi Azure AD rejestracji jednokrotnej z DocuSign, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="44efc-150">**tooconfigure Azure AD single sign-on with DocuSign, perform hello following steps:**</span></span>

1. <span data-ttu-id="44efc-151">W portalu Azure na powitania hello **DocuSign** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.</span><span class="sxs-lookup"><span data-stu-id="44efc-151">In hello Azure portal, on hello **DocuSign** application integration page, click **Single sign-on**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej][4]

2. <span data-ttu-id="44efc-153">Na powitania **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** tooenable rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="44efc-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-docusign-tutorial/tutorial_docusign_samlbase.png)

3. <span data-ttu-id="44efc-155">Na powitania **certyfikat podpisywania SAML** kliknij **certyfikatu (Base 64)** , a następnie zapisz plik certyfikatu na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="44efc-155">On hello **SAML Signing Certificate** section, click **Certificate(Base 64)** and then save certificate file on your computer.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-docusign-tutorial/tutorial_docusign_certificate.png) 

4. <span data-ttu-id="44efc-157">Na powitania **konfiguracji DocuSign** części portalu Azure, kliknij przycisk **skonfigurować DocuSign** okna tooopen Konfigurowanie logowania jednokrotnego.</span><span class="sxs-lookup"><span data-stu-id="44efc-157">On hello **DocuSign Configuration** section of Azure portal, Click **Configure DocuSign** tooopen Configure sign-on window.</span></span> <span data-ttu-id="44efc-158">Kopiuj hello **Sign-Out adres URL, identyfikator jednostki SAML i SAML pojedynczy znak na adres URL usługi** z hello **sekcji krótkimi opisami.**</span><span class="sxs-lookup"><span data-stu-id="44efc-158">Copy hello **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>
    
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-docusign-tutorial/tutorial_docusign_configure.png)

5. <span data-ttu-id="44efc-160">W oknie przeglądarki innej witryny sieci web, logowania tooyour **portalu administracyjnego DocuSign** jako administrator.</span><span class="sxs-lookup"><span data-stu-id="44efc-160">In a different web browser window, login tooyour **DocuSign admin portal** as an administrator.</span></span>

6. <span data-ttu-id="44efc-161">W menu nawigacji powitania po lewej stronie powitania kliknij **domen**.</span><span class="sxs-lookup"><span data-stu-id="44efc-161">In hello navigation menu on hello left, click **Domains**.</span></span>
   
    ![Konfigurowanie rejestracji jednokrotnej][51]

7. <span data-ttu-id="44efc-163">W okienku po prawej stronie powitania, kliknij polecenie **oświadczenia domeny**.</span><span class="sxs-lookup"><span data-stu-id="44efc-163">On hello right pane, click **Claim Domain**.</span></span>
   
    ![Konfigurowanie rejestracji jednokrotnej][52]

8. <span data-ttu-id="44efc-165">Na powitania **oświadczenia domeny** okna dialogowego, w hello **nazwy domeny** pole tekstowe, wpisz domenę firmy, a następnie kliknij przycisk **oświadczeń**.</span><span class="sxs-lookup"><span data-stu-id="44efc-165">On hello **Claim a domain** dialog, in hello **Domain Name** textbox, type your company domain, and then click **Claim**.</span></span> <span data-ttu-id="44efc-166">Upewnij się, że Sprawdź hello domeny i hello stan jest aktywny.</span><span class="sxs-lookup"><span data-stu-id="44efc-166">Make sure that you verify hello domain and hello status is active.</span></span>
   
    ![Konfigurowanie rejestracji jednokrotnej][53]

9. <span data-ttu-id="44efc-168">W menu po lewej stronie powitania kliknij **dostawców tożsamości**</span><span class="sxs-lookup"><span data-stu-id="44efc-168">In menu on hello left side, click **Identity Providers**</span></span>  
   
    ![Konfigurowanie rejestracji jednokrotnej][54]
10. <span data-ttu-id="44efc-170">W okienku po prawej stronie powitania, kliknij przycisk **Dodawanie dostawcy tożsamości**.</span><span class="sxs-lookup"><span data-stu-id="44efc-170">In hello right pane, click **Add Identity Provider**.</span></span> 
   
    ![Konfigurowanie rejestracji jednokrotnej][55]

11. <span data-ttu-id="44efc-172">Na powitania **ustawień dostawcy tożsamości** wykonaj hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="44efc-172">On hello **Identity Provider Settings** page, perform hello following steps:</span></span>
   
    ![Konfigurowanie rejestracji jednokrotnej][56]

    <span data-ttu-id="44efc-174">a.</span><span class="sxs-lookup"><span data-stu-id="44efc-174">a.</span></span> <span data-ttu-id="44efc-175">W hello **nazwa** tekstowym, wpisz unikatową nazwę dla danej konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="44efc-175">In hello **Name** textbox, type a unique name for your configuration.</span></span> <span data-ttu-id="44efc-176">Nie należy używać spacji.</span><span class="sxs-lookup"><span data-stu-id="44efc-176">Do not use spaces.</span></span>

    <span data-ttu-id="44efc-177">b.</span><span class="sxs-lookup"><span data-stu-id="44efc-177">b.</span></span> <span data-ttu-id="44efc-178">Wklej **identyfikator jednostki SAML** do hello **wystawcy dostawcy tożsamości** pola tekstowego.</span><span class="sxs-lookup"><span data-stu-id="44efc-178">Paste **SAML Entity ID** into hello **Identity Provider Issuer** textbox.</span></span>

    <span data-ttu-id="44efc-179">c.</span><span class="sxs-lookup"><span data-stu-id="44efc-179">c.</span></span> <span data-ttu-id="44efc-180">Wklej **SAML pojedynczy znak na adres URL usługi** do hello **adresu URL logowania do dostawcy tożsamości** pola tekstowego.</span><span class="sxs-lookup"><span data-stu-id="44efc-180">Paste **SAML Single Sign-On Service URL** into hello **Identity Provider Login URL** textbox.</span></span>

    <span data-ttu-id="44efc-181">d.</span><span class="sxs-lookup"><span data-stu-id="44efc-181">d.</span></span> <span data-ttu-id="44efc-182">Wklej **Sign-Out URL** do hello **adres URL wylogowania dostawcy tożsamości** pola tekstowego.</span><span class="sxs-lookup"><span data-stu-id="44efc-182">Paste **Sign-Out URL** into hello **Identity Provider Logout URL** textbox.</span></span>

    <span data-ttu-id="44efc-183">e.</span><span class="sxs-lookup"><span data-stu-id="44efc-183">e.</span></span> <span data-ttu-id="44efc-184">Wybierz **podpisywania żądania uwierzytelniania**.</span><span class="sxs-lookup"><span data-stu-id="44efc-184">Select **Sign AuthN Request**.</span></span>

    <span data-ttu-id="44efc-185">f.</span><span class="sxs-lookup"><span data-stu-id="44efc-185">f.</span></span> <span data-ttu-id="44efc-186">Jako **AuthN wysyłanie żądania przez**, wybierz pozycję **POST**.</span><span class="sxs-lookup"><span data-stu-id="44efc-186">As **Send AuthN request by**, select **POST**.</span></span>

    <span data-ttu-id="44efc-187">g.</span><span class="sxs-lookup"><span data-stu-id="44efc-187">g.</span></span> <span data-ttu-id="44efc-188">Jako **Wyślij żądanie wylogowania**, wybierz pozycję **UZYSKAĆ**.</span><span class="sxs-lookup"><span data-stu-id="44efc-188">As **Send logout request by**, select **GET**.</span></span>

12. <span data-ttu-id="44efc-189">W hello **mapowanie atrybutu niestandardowego** sekcji, wybierz pole hello ma toomap oświadczenie, Azure AD.</span><span class="sxs-lookup"><span data-stu-id="44efc-189">In hello **Custom Attribute Mapping** section, choose hello field you want toomap with Azure AD Claim.</span></span> <span data-ttu-id="44efc-190">W tym przykładzie hello **emailaddress** oświadczenia jest zamapowana z wartością hello **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress**.</span><span class="sxs-lookup"><span data-stu-id="44efc-190">In this example, hello **emailaddress** claim is mapped with hello value of **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress**.</span></span> <span data-ttu-id="44efc-191">To nazwa oświadczenia domyślne hello z usługą Azure AD, oświadczenie adresu e-mail.</span><span class="sxs-lookup"><span data-stu-id="44efc-191">It is hello default claim name from Azure AD for email claim.</span></span> 
   
    > [!NOTE]
    > <span data-ttu-id="44efc-192">Użyj hello odpowiednie **identyfikator użytkownika** toomap hello użytkownika z usługi Azure AD tooDocuSign użytkownika mapowania.</span><span class="sxs-lookup"><span data-stu-id="44efc-192">Use hello appropriate **User identifier** toomap hello user from Azure AD tooDocuSign user mapping.</span></span> <span data-ttu-id="44efc-193">Wybierz hello odpowiednie pola, a następnie wprowadź odpowiednie wartości hello na podstawie własnych ustawień organizacji.</span><span class="sxs-lookup"><span data-stu-id="44efc-193">Select hello proper Field and enter hello appropriate value based on your organization settings.</span></span>
          
    ![Konfigurowanie rejestracji jednokrotnej][57]

13. <span data-ttu-id="44efc-195">W hello **certyfikat dostawcy tożsamości** , kliknij przycisk **Dodaj certyfikat**, a następnie przekaż certyfikat hello został pobrany z portalu usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="44efc-195">In hello **Identity Provider Certificate** section, click **Add Certificate**, and then upload hello certificate you have downloaded from Azure AD portal.</span></span>   
   
    ![Konfigurowanie rejestracji jednokrotnej][58]

14. <span data-ttu-id="44efc-197">Kliknij pozycję **Zapisz**.</span><span class="sxs-lookup"><span data-stu-id="44efc-197">Click **Save**.</span></span>

15. <span data-ttu-id="44efc-198">W hello **dostawców tożsamości** kliknij **akcje**, a następnie kliknij przycisk **punkty końcowe**.</span><span class="sxs-lookup"><span data-stu-id="44efc-198">In hello **Identity Providers** section, click **Actions**, and then click **Endpoints**.</span></span>   
   
    ![Konfigurowanie rejestracji jednokrotnej][59]
 
16. <span data-ttu-id="44efc-200">W hello **Wyświetl SAML 2.0 punkty końcowe** sekcji na **portalu administracyjnego DocuSign**, wykonaj następujące kroki hello:</span><span class="sxs-lookup"><span data-stu-id="44efc-200">In hello **View SAML 2.0 Endpoints** section on **DocuSign admin portal**, perform hello following steps:</span></span>
   
    ![Konfigurowanie rejestracji jednokrotnej][60]
   
    <span data-ttu-id="44efc-202">a.</span><span class="sxs-lookup"><span data-stu-id="44efc-202">a.</span></span> <span data-ttu-id="44efc-203">Hello kopiowania **adres URL wystawcy dostawcy usługi**i wkleić do hello **identyfikator** textbox w **DocuSign domeny i adres URL** sekcji hello Azure hello następujące portalu Wzorzec: `https://<subdomain>.docusign.com/organization/<uniqueID>/saml2/login/sp/<uniqueID>`.</span><span class="sxs-lookup"><span data-stu-id="44efc-203">Copy hello **Service Provider Issuer URL**, and then paste into hello **Identifier** textbox on **DocuSign Domain and URLs** section of hello Azure portal following hello pattern: `https://<subdomain>.docusign.com/organization/<uniqueID>/saml2/login/sp/<uniqueID>`.</span></span>
   
    <span data-ttu-id="44efc-204">b.</span><span class="sxs-lookup"><span data-stu-id="44efc-204">b.</span></span> <span data-ttu-id="44efc-205">Hello kopiowania **adresu URL logowania do usługi dostawcy**i wkleić do hello **na adres URL logowania** textbox w **DocuSign domeny i adres URL** sekcji hello Azure hello następujące portalu Wzorzec: `https://<subdomain>.docusign.com/organization/<uniqueID>/saml2/`.</span><span class="sxs-lookup"><span data-stu-id="44efc-205">Copy hello **Service Provider Login URL**, and then paste into hello **Sign On URL** textbox on **DocuSign Domain and URLs** section of hello Azure portal following hello pattern: `https://<subdomain>.docusign.com/organization/<uniqueID>/saml2/`.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-docusign-tutorial/tutorial_docusign_url.png)
      
    <span data-ttu-id="44efc-207">c.</span><span class="sxs-lookup"><span data-stu-id="44efc-207">c.</span></span>  <span data-ttu-id="44efc-208">Kliknij przycisk **Zamknij**</span><span class="sxs-lookup"><span data-stu-id="44efc-208">Click **Close**</span></span>
    
17. <span data-ttu-id="44efc-209">Na powitania portalu Azure, kliknij przycisk **zapisać**.</span><span class="sxs-lookup"><span data-stu-id="44efc-209">On hello Azure portal, click **Save**.</span></span>
    
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-docusign-tutorial/tutorial_general_400.png)

> [!TIP]
> <span data-ttu-id="44efc-211">Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz hello [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji hello!</span><span class="sxs-lookup"><span data-stu-id="44efc-211">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="44efc-212">Po dodaniu tej aplikacji z hello **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij hello **rejestracji jednokrotnej** hello kartę i dostępu do osadzonych dokumentacji za pośrednictwem hello  **Konfiguracja** sekcji u dołu hello.</span><span class="sxs-lookup"><span data-stu-id="44efc-212">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="44efc-213">Więcej o hello osadzonych dokumentacji funkcji w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="44efc-213">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="44efc-214">Tworzenie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="44efc-214">Creating an Azure AD test user</span></span>
<span data-ttu-id="44efc-215">Celem Hello w tej sekcji jest toocreate użytkownika testowego, w portalu Azure o nazwie Simona Britta hello.</span><span class="sxs-lookup"><span data-stu-id="44efc-215">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Tworzenie użytkowników usługi Azure AD][100]

<span data-ttu-id="44efc-217">**toocreate użytkownika testowego w usłudze Azure AD, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="44efc-217">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="44efc-218">W hello **portalu Azure**na temat hello w lewym okienku nawigacji, kliknij przycisk **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="44efc-218">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-docusign-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="44efc-220">toodisplay hello listę użytkowników, przejdź zbyt**użytkowników i grup** i kliknij przycisk **wszyscy użytkownicy**.</span><span class="sxs-lookup"><span data-stu-id="44efc-220">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-docusign-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="44efc-222">U góry okna dialogowego hello hello, kliknij przycisk **Dodaj** tooopen hello **użytkownika** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="44efc-222">At hello top of hello dialog, click **Add** tooopen hello **User** dialog.</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-docusign-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="44efc-224">Na powitania **użytkownika** okna dialogowego wykonaj hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="44efc-224">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-docusign-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="44efc-226">a.</span><span class="sxs-lookup"><span data-stu-id="44efc-226">a.</span></span> <span data-ttu-id="44efc-227">W hello **nazwa** pole tekstowe, typ **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="44efc-227">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="44efc-228">b.</span><span class="sxs-lookup"><span data-stu-id="44efc-228">b.</span></span> <span data-ttu-id="44efc-229">W hello **nazwy użytkownika** pole tekstowe, hello typu **adres e-mail** z BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="44efc-229">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="44efc-230">c.</span><span class="sxs-lookup"><span data-stu-id="44efc-230">c.</span></span> <span data-ttu-id="44efc-231">Wybierz **Pokaż hasło** i zanotuj wartość hello hello **hasło**.</span><span class="sxs-lookup"><span data-stu-id="44efc-231">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="44efc-232">d.</span><span class="sxs-lookup"><span data-stu-id="44efc-232">d.</span></span> <span data-ttu-id="44efc-233">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="44efc-233">Click **Create**.</span></span>
 
### <a name="creating-a-docusign-test-user"></a><span data-ttu-id="44efc-234">Tworzenie użytkownika testowego DocuSign</span><span class="sxs-lookup"><span data-stu-id="44efc-234">Creating a DocuSign test user</span></span>

<span data-ttu-id="44efc-235">Aplikacja obsługuje **tylko w czasie Inicjowanie obsługi użytkowników** i po uwierzytelniania użytkowników są tworzone automatycznie w aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="44efc-235">Application supports **Just in time user provisioning** and after authentication users are created in hello application automatically.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="44efc-236">Przypisanie użytkownika testowego hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="44efc-236">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="44efc-237">W tej sekcji możesz włączyć toouse Simona Britta Azure logowania jednokrotnego za udzielanie jej tooDocuSign dostępu.</span><span class="sxs-lookup"><span data-stu-id="44efc-237">In this section, you enable Britta Simon toouse Azure single sign-on by granting her access tooDocuSign.</span></span>

![Przypisz użytkownika][200] 

<span data-ttu-id="44efc-239">**tooassign tooDocuSign Simona Britta wykonaj hello następujące kroki:**</span><span class="sxs-lookup"><span data-stu-id="44efc-239">**tooassign Britta Simon tooDocuSign, perform hello following steps:**</span></span>

1. <span data-ttu-id="44efc-240">W portalu Azure hello, otwórz widok aplikacji hello, a następnie przejdź do widoku katalogu toohello i przejść za**aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="44efc-240">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Przypisz użytkownika][201] 

2. <span data-ttu-id="44efc-242">Z listy aplikacji hello wybierz **DocuSign**.</span><span class="sxs-lookup"><span data-stu-id="44efc-242">In hello applications list, select **DocuSign**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-docusign-tutorial/tutorial_docusign_app.png) 

3. <span data-ttu-id="44efc-244">W menu powitania po lewej stronie powitania kliknij **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="44efc-244">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Przypisz użytkownika][202] 

4. <span data-ttu-id="44efc-246">Kliknij przycisk **Dodaj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="44efc-246">Click **Add** button.</span></span> <span data-ttu-id="44efc-247">Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="44efc-247">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Przypisz użytkownika][203]

5. <span data-ttu-id="44efc-249">Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** hello listy użytkowników.</span><span class="sxs-lookup"><span data-stu-id="44efc-249">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="44efc-250">Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="44efc-250">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="44efc-251">Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="44efc-251">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="44efc-252">Testowanie rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="44efc-252">Testing single sign-on</span></span>

<span data-ttu-id="44efc-253">W tej sekcji można przetestować konfiguracji usługi Azure AD pojedynczego logowania jednokrotnego przy użyciu hello panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="44efc-253">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="44efc-254">Po kliknięciu kafelka DocuSign hello w hello Panel dostępu, należy pobrać automatycznie zalogowane tooyour DocuSign aplikacji.</span><span class="sxs-lookup"><span data-stu-id="44efc-254">When you click hello DocuSign tile in hello Access Panel, you should get automatically signed-on tooyour DocuSign application.</span></span>
<span data-ttu-id="44efc-255">Aby uzyskać więcej informacji na temat hello Panel dostępu, zobacz [toohello wprowadzenie panelu dostępu](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="44efc-255">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="44efc-256">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="44efc-256">Additional resources</span></span>

* [<span data-ttu-id="44efc-257">Lista samouczków dotyczących tooIntegrate aplikacji SaaS w usłudze Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="44efc-257">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="44efc-258">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="44efc-258">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)
* [<span data-ttu-id="44efc-259">Skonfiguruj Inicjowanie obsługi użytkowników</span><span class="sxs-lookup"><span data-stu-id="44efc-259">Configure User Provisioning</span></span>](active-directory-saas-docusign-provisioning-tutorial.md)


<!--Image references-->

[1]: ./media/active-directory-saas-docusign-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-docusign-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-docusign-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-docusign-tutorial/tutorial_general_04.png
[51]: ./media/active-directory-saas-docusign-tutorial/tutorial_docusign_21.png
[52]: ./media/active-directory-saas-docusign-tutorial/tutorial_docusign_22.png
[53]: ./media/active-directory-saas-docusign-tutorial/tutorial_docusign_23.png
[54]: ./media/active-directory-saas-docusign-tutorial/tutorial_docusign_19.png
[55]: ./media/active-directory-saas-docusign-tutorial/tutorial_docusign_20.png
[56]: ./media/active-directory-saas-docusign-tutorial/tutorial_docusign_24.png
[57]: ./media/active-directory-saas-docusign-tutorial/tutorial_docusign_25.png
[58]: ./media/active-directory-saas-docusign-tutorial/tutorial_docusign_26.png
[59]: ./media/active-directory-saas-docusign-tutorial/tutorial_docusign_27.png
[60]: ./media/active-directory-saas-docusign-tutorial/tutorial_docusign_28.png
[61]: ./media/active-directory-saas-docusign-tutorial/tutorial_docusign_29.png
[100]: ./media/active-directory-saas-docusign-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-docusign-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-docusign-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-docusign-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-docusign-tutorial/tutorial_general_203.png

