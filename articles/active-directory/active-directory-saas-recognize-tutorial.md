---
title: 'Samouczek: Integracji Azure Active Directory z rozpoznawanie | Dokumentacja firmy Microsoft'
description: "Dowiedz się, jak tooconfigure logowanie jednokrotne między usługą Azure Active Directory i rozpoznawanie."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: cfad939e-c8f4-45a0-bd25-c4eb9701acaa
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/10/2017
ms.author: jeedes
ms.openlocfilehash: f33fc3959f72f875b8c5c4f0abd4e9b6737ca615
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-recognize"></a><span data-ttu-id="4b598-103">Samouczek: Integracji Azure Active Directory z rozpoznawanie</span><span class="sxs-lookup"><span data-stu-id="4b598-103">Tutorial: Azure Active Directory integration with Recognize</span></span>

<span data-ttu-id="4b598-104">Z tego samouczka, dowiesz się, jak rozpoznać toointegrate w usłudze Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="4b598-104">In this tutorial, you learn how toointegrate Recognize with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="4b598-105">Integracja z usługą Azure AD rozpoznawanie zapewnia hello następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="4b598-105">Integrating Recognize with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="4b598-106">Można kontrolować w usłudze Azure AD, kto ma dostęp do tooRecognize</span><span class="sxs-lookup"><span data-stu-id="4b598-106">You can control in Azure AD who has access tooRecognize</span></span>
- <span data-ttu-id="4b598-107">Można włączyć użytkownika użytkownicy tooautomatically get zalogowane tooRecognize (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="4b598-107">You can enable your users tooautomatically get signed-on tooRecognize (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="4b598-108">Możesz zarządzać kont w jednej centralnej lokalizacji - hello portalu Azure</span><span class="sxs-lookup"><span data-stu-id="4b598-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="4b598-109">Jeśli chcesz tooknow więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="4b598-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="4b598-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="4b598-110">Prerequisites</span></span>

<span data-ttu-id="4b598-111">Integracja tooconfigure usługi Azure AD z rozpoznawanie, potrzebujesz hello następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="4b598-111">tooconfigure Azure AD integration with Recognize, you need hello following items:</span></span>

- <span data-ttu-id="4b598-112">Subskrypcję usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="4b598-112">An Azure AD subscription</span></span>
- <span data-ttu-id="4b598-113">Rozpoznaj logowanie jednokrotne włączone subskrypcji</span><span class="sxs-lookup"><span data-stu-id="4b598-113">A Recognize single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="4b598-114">tootest hello kroków w tym samouczku, zaleca się przy użyciu środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="4b598-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="4b598-115">tootest hello kroki opisane w tym samouczku, należy stosować te zalecenia:</span><span class="sxs-lookup"><span data-stu-id="4b598-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="4b598-116">Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="4b598-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="4b598-117">Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz pobrać miesięczna wersja próbna tutaj: [oferta wersji próbnej](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="4b598-117">If you don't have an Azure AD trial environment, you can get a one-month trial here: [Trial offer](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="4b598-118">Opis scenariusza</span><span class="sxs-lookup"><span data-stu-id="4b598-118">Scenario description</span></span>
<span data-ttu-id="4b598-119">W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym.</span><span class="sxs-lookup"><span data-stu-id="4b598-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="4b598-120">Scenariusz Hello opisane w tym samouczku składa się z dwóch głównych elementów:</span><span class="sxs-lookup"><span data-stu-id="4b598-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="4b598-121">Dodawanie rozpoznawaj z galerii hello</span><span class="sxs-lookup"><span data-stu-id="4b598-121">Adding Recognize from hello gallery</span></span>
2. <span data-ttu-id="4b598-122">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="4b598-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-recognize-from-hello-gallery"></a><span data-ttu-id="4b598-123">Dodawanie rozpoznawaj z galerii hello</span><span class="sxs-lookup"><span data-stu-id="4b598-123">Adding Recognize from hello gallery</span></span>
<span data-ttu-id="4b598-124">tooconfigure hello integracji rozpoznawanie do usługi Azure AD, należy tooadd rozpoznawaj z galerii hello tooyour listę zarządzanych aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="4b598-124">tooconfigure hello integration of Recognize into Azure AD, you need tooadd Recognize from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="4b598-125">**tooadd rozpoznawaj z galerii hello, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="4b598-125">**tooadd Recognize from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="4b598-126">W hello  **[portalu Azure](https://portal.azure.com)**na temat hello panelu nawigacji po lewej stronie, kliknij przycisk **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="4b598-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Usługa Active Directory][1]

2. <span data-ttu-id="4b598-128">Przejdź za**aplikacje dla przedsiębiorstw**.</span><span class="sxs-lookup"><span data-stu-id="4b598-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="4b598-129">Następnie przejdź zbyt**wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="4b598-129">Then go too**All applications**.</span></span>

    ![Aplikacje][2]
    
3. <span data-ttu-id="4b598-131">tooadd nową aplikację, kliknij przycisk **nowej aplikacji** przycisk u góry hello okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="4b598-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplikacje][3]

4. <span data-ttu-id="4b598-133">W polu wyszukiwania hello wpisz **rozpoznawanie**.</span><span class="sxs-lookup"><span data-stu-id="4b598-133">In hello search box, type **Recognize**.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-recognize-tutorial/tutorial_recognize_search.png)

5. <span data-ttu-id="4b598-135">W panelu wyników hello, wybierz **rozpoznawanie**, a następnie kliknij przycisk **Dodaj** przycisk aplikacji hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="4b598-135">In hello results panel, select **Recognize**, and then click **Add** button tooadd hello application.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-recognize-tutorial/tutorial_recognize_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="4b598-137">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="4b598-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="4b598-138">W tej sekcji skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z rozpoznawanie w oparciu o nazwie "Britta Simona" użytkownika testowego.</span><span class="sxs-lookup"><span data-stu-id="4b598-138">In this section, you configure and test Azure AD single sign-on with Recognize based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="4b598-139">Dla pojedynczego logowania jednokrotnego toowork usługi Azure AD musi tooknow użytkownika odpowiednikiem hello w rozpoznawanie jest tooa użytkownika w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="4b598-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Recognize is tooa user in Azure AD.</span></span> <span data-ttu-id="4b598-140">Innymi słowy relację łącza między użytkownika usługi Azure AD i hello użytkownikowi w rozpoznawanie musi toobe ustanowione.</span><span class="sxs-lookup"><span data-stu-id="4b598-140">In other words, a link relationship between an Azure AD user and hello related user in Recognize needs toobe established.</span></span>

<span data-ttu-id="4b598-141">Rozpoznaj, przypisywanie wartości hello hello **nazwy użytkownika** w usłudze Azure AD jako wartość hello hello **Username** tooestablish hello łącze relacji.</span><span class="sxs-lookup"><span data-stu-id="4b598-141">In Recognize, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="4b598-142">tooconfigure i testowych usługi Azure AD logowanie jednokrotne z rozpoznawanie, należy po bloków konstrukcyjnych hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="4b598-142">tooconfigure and test Azure AD single sign-on with Recognize, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="4b598-143">**[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configuring-azure-ad-single-sign-on)**  -tooenable Twojego toouse użytkowników tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="4b598-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="4b598-144">**[Tworzenie użytkownika testowego usługi Azure AD](#creating-an-azure-ad-test-user)**  -tootest usługi Azure AD rejestracji jednokrotnej z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="4b598-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="4b598-145">**[Tworzenie użytkownika testowego rozpoznawanie](#creating-a-recognize-test-user)**  -toohave odpowiednikiem Simona Britta w rozpoznawanie, który jest połączony toohello usługi Azure AD reprezentację użytkownika.</span><span class="sxs-lookup"><span data-stu-id="4b598-145">**[Creating a Recognize test user](#creating-a-recognize-test-user)** - toohave a counterpart of Britta Simon in Recognize that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="4b598-146">**[Przypisanie użytkownika testowego hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Simona Britta toouse usługi Azure AD rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="4b598-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="4b598-147">**[Testowanie rejestracji jednokrotnej](#testing-single-sign-on)**  -tooverify czy hello konfiguracji działania.</span><span class="sxs-lookup"><span data-stu-id="4b598-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="4b598-148">Konfigurowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="4b598-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="4b598-149">W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w portalu Azure hello i skonfigurować logowanie jednokrotne w aplikacji rozpoznawanie.</span><span class="sxs-lookup"><span data-stu-id="4b598-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Recognize application.</span></span>

<span data-ttu-id="4b598-150">**tooconfigure usługi Azure AD rejestracji jednokrotnej z rozpoznawanie, wykonaj hello następujące kroki:**</span><span class="sxs-lookup"><span data-stu-id="4b598-150">**tooconfigure Azure AD single sign-on with Recognize, perform hello following steps:**</span></span>

1. <span data-ttu-id="4b598-151">W portalu Azure na powitania hello **rozpoznawanie** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.</span><span class="sxs-lookup"><span data-stu-id="4b598-151">In hello Azure portal, on hello **Recognize** application integration page, click **Single sign-on**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej][4]

2. <span data-ttu-id="4b598-153">Na powitania **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** tooenable rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="4b598-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-recognize-tutorial/tutorial_recognize_samlbase.png)

3. <span data-ttu-id="4b598-155">Na powitania **adresy URL i rozpoznać domeny** sekcji, wykonaj następujące kroki hello:</span><span class="sxs-lookup"><span data-stu-id="4b598-155">On hello **Recognize Domain and URLs** section, perform hello following steps:</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-recognize-tutorial/tutorial_recognize_url.png)

    <span data-ttu-id="4b598-157">a.</span><span class="sxs-lookup"><span data-stu-id="4b598-157">a.</span></span> <span data-ttu-id="4b598-158">W hello **adres URL logowania** tekstowym, wpisz adres URL za pomocą hello następującego wzorca:`https://recognizeapp.com/<your-domain>/saml/sso`</span><span class="sxs-lookup"><span data-stu-id="4b598-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://recognizeapp.com/<your-domain>/saml/sso`</span></span>

    <span data-ttu-id="4b598-159">b.</span><span class="sxs-lookup"><span data-stu-id="4b598-159">b.</span></span> <span data-ttu-id="4b598-160">W hello **identyfikator** tekstowym, wpisz adres URL za pomocą hello następującego wzorca:`https://recognizeapp.com/<your-domain>`</span><span class="sxs-lookup"><span data-stu-id="4b598-160">In hello **Identifier** textbox, type a URL using hello following pattern: `https://recognizeapp.com/<your-domain>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="4b598-161">Wartości te nie są prawdziwe.</span><span class="sxs-lookup"><span data-stu-id="4b598-161">These values are not real.</span></span> <span data-ttu-id="4b598-162">Zaktualizować te wartości z hello rzeczywisty adres URL logowania i identyfikator.</span><span class="sxs-lookup"><span data-stu-id="4b598-162">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="4b598-163">Skontaktuj się z [zespołem pomocy technicznej klienta rozpoznaje](mailto:support@recognizeapp.com) uzyskać adres URL logowania i można uzyskać wartość identyfikatora otwierając hello sekcja Ustawienia logowania jednokrotnego, która znajduje się w dalszej części samouczka hello hello adres URL metadanych dostawcy usługi.</span><span class="sxs-lookup"><span data-stu-id="4b598-163">Contact [Recognize Client support team](mailto:support@recognizeapp.com) to get Sign-On URL and you can get Identifier value by opening hello Service Provider Metadata URL from hello SSO Settings section that is explained later in hello tutorial.</span></span> <span data-ttu-id="4b598-164">.</span><span class="sxs-lookup"><span data-stu-id="4b598-164">.</span></span> 
 
4. <span data-ttu-id="4b598-165">Na powitania **certyfikat podpisywania SAML** kliknij **certyfikatu (Base64)** , a następnie zapisz plik certyfikatu hello na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="4b598-165">On hello **SAML Signing Certificate** section, click **Certificate (Base64)** and then save hello certificate file on your computer.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-recognize-tutorial/tutorial_recognize_certificate.png) 

5. <span data-ttu-id="4b598-167">Kliknij przycisk **zapisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="4b598-167">Click **Save** button.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-recognize-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="4b598-169">Na powitania **rozpoznaje konfiguracji** kliknij **skonfigurować rozpoznaje** tooopen **Konfigurowanie logowania jednokrotnego** okna.</span><span class="sxs-lookup"><span data-stu-id="4b598-169">On hello **Recognize Configuration** section, click **Configure Recognize** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="4b598-170">Kopiuj hello **Sign-Out adres URL, identyfikator jednostki SAML i SAML pojedynczy znak na adres URL usługi** z hello **sekcji krótkimi opisami.**</span><span class="sxs-lookup"><span data-stu-id="4b598-170">Copy hello **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-recognize-tutorial/tutorial_recognize_configure.png) 

7. <span data-ttu-id="4b598-172">W oknie przeglądarki innej witryny sieci web, logowania jednokrotnego tooyour rozpoznawanie dzierżawy z uprawnieniami administratora.</span><span class="sxs-lookup"><span data-stu-id="4b598-172">In a different web browser window, sign-on tooyour Recognize tenant as an administrator.</span></span>

8. <span data-ttu-id="4b598-173">Na powitania prawym górnym rogu kliknij **Menu**.</span><span class="sxs-lookup"><span data-stu-id="4b598-173">On hello upper right corner, click **Menu**.</span></span> <span data-ttu-id="4b598-174">Przejdź za**administrator firmy**.</span><span class="sxs-lookup"><span data-stu-id="4b598-174">Go too**Company Admin**.</span></span>
   
    ![Konfigurowanie jednej logowania w aplikacji po stronie](./media/active-directory-saas-recognize-tutorial/tutorial_recognize_000.png)

9. <span data-ttu-id="4b598-176">W okienku nawigacji po lewej stronie powitania kliknij **ustawienia**.</span><span class="sxs-lookup"><span data-stu-id="4b598-176">On hello left navigation pane, click **Settings**.</span></span>
   
    ![Konfigurowanie jednej logowania w aplikacji po stronie](./media/active-directory-saas-recognize-tutorial/tutorial_recognize_001.png)

10. <span data-ttu-id="4b598-178">Wykonaj następujące kroki powitania **ustawienia logowania jednokrotnego** sekcji.</span><span class="sxs-lookup"><span data-stu-id="4b598-178">Perform hello following steps on **SSO Settings** section.</span></span>
   
    ![Konfigurowanie jednej logowania w aplikacji po stronie](./media/active-directory-saas-recognize-tutorial/tutorial_recognize_002.png)
    
    <span data-ttu-id="4b598-180">a.</span><span class="sxs-lookup"><span data-stu-id="4b598-180">a.</span></span> <span data-ttu-id="4b598-181">Jako **włączenia logowania jednokrotnego**, wybierz pozycję **ON**.</span><span class="sxs-lookup"><span data-stu-id="4b598-181">As **Enable SSO**, select **ON**.</span></span>

    <span data-ttu-id="4b598-182">b.</span><span class="sxs-lookup"><span data-stu-id="4b598-182">b.</span></span> <span data-ttu-id="4b598-183">W hello **identyfikator jednostki IDP** pole tekstowe, Wklej wartość hello **identyfikator jednostki SAML** którego została skopiowana z portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="4b598-183">In hello **IDP Entity ID** textbox, paste hello value of **SAML Entity ID** which you have copied from Azure portal.</span></span>
    
    <span data-ttu-id="4b598-184">c.</span><span class="sxs-lookup"><span data-stu-id="4b598-184">c.</span></span> <span data-ttu-id="4b598-185">W hello **logowania jednokrotnego, docelowy adres url** pole tekstowe, Wklej wartość hello **SAML pojedynczy znak na adres URL usługi** którego została skopiowana z portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="4b598-185">In hello **Sso target url** textbox, paste hello value of **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span></span>
    
    <span data-ttu-id="4b598-186">d.</span><span class="sxs-lookup"><span data-stu-id="4b598-186">d.</span></span> <span data-ttu-id="4b598-187">W hello **Slo docelowy adres url** pole tekstowe, Wklej wartość hello **Sign-Out URL** którego została skopiowana z portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="4b598-187">In hello **Slo target url** textbox, paste hello value of **Sign-Out URL** which you have copied from Azure portal.</span></span> 
    
    <span data-ttu-id="4b598-188">e.</span><span class="sxs-lookup"><span data-stu-id="4b598-188">e.</span></span> <span data-ttu-id="4b598-189">Otwórz z pobranego **certyfikatu (Base64)** pliku w Notatniku hello kopiowania zawartości go do Schowka, a następnie wklej go toohello **certyfikatu** pola tekstowego.</span><span class="sxs-lookup"><span data-stu-id="4b598-189">Open your downloaded **Certificate (Base64)** file in notepad, copy hello content of it into your clipboard, and then paste it toohello **Certificate** textbox.</span></span>
    
    <span data-ttu-id="4b598-190">f.</span><span class="sxs-lookup"><span data-stu-id="4b598-190">f.</span></span> <span data-ttu-id="4b598-191">Kliknij przycisk hello **Zapisz ustawienia** przycisku.</span><span class="sxs-lookup"><span data-stu-id="4b598-191">Click hello **Save settings** button.</span></span> 

11. <span data-ttu-id="4b598-192">Obok hello **ustawienia logowania jednokrotnego** sekcji, skopiuj adres URL hello pod **adres url usługi dostawcy metadanych**.</span><span class="sxs-lookup"><span data-stu-id="4b598-192">Beside hello **SSO Settings** section, copy hello URL under **Service Provider Metadata url**.</span></span>
   
    ![Konfigurowanie jednej logowania w aplikacji po stronie](./media/active-directory-saas-recognize-tutorial/tutorial_recognize_003.png)

12. <span data-ttu-id="4b598-194">Otwórz hello **łącze URL metadanych** w obszarze puste przeglądarki toodownload hello metadanych dokumentu.</span><span class="sxs-lookup"><span data-stu-id="4b598-194">Open hello **Metadata URL link** under a blank browser toodownload hello metadata document.</span></span> <span data-ttu-id="4b598-195">Następnie skopiuj hello EntityDescriptor value(entityID) z pliku hello i wklej go w **identyfikator** textbox w **sekcji rozpoznać domeny i adresy URL** w portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="4b598-195">Then copy hello EntityDescriptor value(entityID) from hello file and paste it in **Identifier** textbox in **Recognize Domain and URLs section** on Azure portal.</span></span>
    
    ![Konfigurowanie jednej logowania w aplikacji po stronie](./media/active-directory-saas-recognize-tutorial/tutorial_recognize_004.png)

> [!TIP]
> <span data-ttu-id="4b598-197">Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz hello [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji hello!</span><span class="sxs-lookup"><span data-stu-id="4b598-197">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="4b598-198">Po dodaniu tej aplikacji z hello **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij hello **rejestracji jednokrotnej** hello kartę i dostępu do osadzonych dokumentacji za pośrednictwem hello  **Konfiguracja** sekcji u dołu hello.</span><span class="sxs-lookup"><span data-stu-id="4b598-198">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="4b598-199">Więcej o hello osadzonych dokumentacji funkcji w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="4b598-199">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="4b598-200">Tworzenie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="4b598-200">Creating an Azure AD test user</span></span>
<span data-ttu-id="4b598-201">Celem Hello w tej sekcji jest toocreate użytkownika testowego, w portalu Azure o nazwie Simona Britta hello.</span><span class="sxs-lookup"><span data-stu-id="4b598-201">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Tworzenie użytkowników usługi Azure AD][100]

<span data-ttu-id="4b598-203">**toocreate użytkownika testowego w usłudze Azure AD, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="4b598-203">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="4b598-204">W hello **portalu Azure**na temat hello w lewym okienku nawigacji, kliknij przycisk **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="4b598-204">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-recognize-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="4b598-206">toodisplay hello listę użytkowników, przejdź zbyt**użytkowników i grup** i kliknij przycisk **wszyscy użytkownicy**.</span><span class="sxs-lookup"><span data-stu-id="4b598-206">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-recognize-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="4b598-208">Witaj tooopen **użytkownika** okna dialogowego, kliknij przycisk **Dodaj** u góry hello hello okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="4b598-208">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-recognize-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="4b598-210">Na powitania **użytkownika** okna dialogowego wykonaj hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="4b598-210">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-recognize-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="4b598-212">a.</span><span class="sxs-lookup"><span data-stu-id="4b598-212">a.</span></span> <span data-ttu-id="4b598-213">W hello **nazwa** pole tekstowe, typ **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="4b598-213">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="4b598-214">b.</span><span class="sxs-lookup"><span data-stu-id="4b598-214">b.</span></span> <span data-ttu-id="4b598-215">W hello **nazwy użytkownika** pole tekstowe, hello typu **adres e-mail** z BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="4b598-215">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="4b598-216">c.</span><span class="sxs-lookup"><span data-stu-id="4b598-216">c.</span></span> <span data-ttu-id="4b598-217">Wybierz **Pokaż hasło** i zanotuj wartość hello hello **hasło**.</span><span class="sxs-lookup"><span data-stu-id="4b598-217">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="4b598-218">d.</span><span class="sxs-lookup"><span data-stu-id="4b598-218">d.</span></span> <span data-ttu-id="4b598-219">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="4b598-219">Click **Create**.</span></span>
 
### <a name="creating-a-recognize-test-user"></a><span data-ttu-id="4b598-220">Tworzenie użytkownika testowego rozpoznawanie</span><span class="sxs-lookup"><span data-stu-id="4b598-220">Creating a Recognize test user</span></span>

<span data-ttu-id="4b598-221">W przypadku użytkowników usługi Azure AD toolog kolejności tooenable do uznania muszą mieć przydzielone do uznania.</span><span class="sxs-lookup"><span data-stu-id="4b598-221">In order tooenable Azure AD users toolog into Recognize, they must be provisioned into Recognize.</span></span> <span data-ttu-id="4b598-222">W przypadku hello rozpoznawanie Inicjowanie obsługi to zadanie ręczne.</span><span class="sxs-lookup"><span data-stu-id="4b598-222">In hello case of Recognize, provisioning is a manual task.</span></span>

<span data-ttu-id="4b598-223">Ta aplikacja nie obsługuje udostępniania SCIM, ale ma synchronizacji alternatywny użytkownika, która udostępnia użytkownikom.</span><span class="sxs-lookup"><span data-stu-id="4b598-223">This app doesn't support SCIM provisioning but has an alternate user sync that provisions users.</span></span> 

<span data-ttu-id="4b598-224">**tooprovision konta użytkownika, należy wykonać hello następujące kroki:**</span><span class="sxs-lookup"><span data-stu-id="4b598-224">**tooprovision a user account, perform hello following steps:**</span></span>

1. <span data-ttu-id="4b598-225">Zaloguj się do witryny firmy rozpoznawanie jako administrator.</span><span class="sxs-lookup"><span data-stu-id="4b598-225">Log into your Recognize company site as an administrator.</span></span>

2. <span data-ttu-id="4b598-226">Na powitania prawym górnym rogu kliknij **Menu**.</span><span class="sxs-lookup"><span data-stu-id="4b598-226">On hello upper right corner, click **Menu**.</span></span> <span data-ttu-id="4b598-227">Przejdź za**administrator firmy**.</span><span class="sxs-lookup"><span data-stu-id="4b598-227">Go too**Company Admin**.</span></span>

3. <span data-ttu-id="4b598-228">W okienku nawigacji po lewej stronie powitania kliknij **ustawienia**.</span><span class="sxs-lookup"><span data-stu-id="4b598-228">On hello left navigation pane, click **Settings**.</span></span>

4. <span data-ttu-id="4b598-229">Wykonaj następujące kroki powitania **synchronizacji użytkownika** sekcji.</span><span class="sxs-lookup"><span data-stu-id="4b598-229">Perform hello following steps on **User Sync** section.</span></span>
   
   <span data-ttu-id="4b598-230">![Nowy użytkownik](./media/active-directory-saas-recognize-tutorial/tutorial_recognize_005.png "nowego użytkownika")</span><span class="sxs-lookup"><span data-stu-id="4b598-230">![New User](./media/active-directory-saas-recognize-tutorial/tutorial_recognize_005.png "New User")</span></span>
   
   <span data-ttu-id="4b598-231">a.</span><span class="sxs-lookup"><span data-stu-id="4b598-231">a.</span></span> <span data-ttu-id="4b598-232">Jako **włączona synchronizacja**, wybierz pozycję **ON**.</span><span class="sxs-lookup"><span data-stu-id="4b598-232">As **Sync Enabled**, select **ON**.</span></span>
   
   <span data-ttu-id="4b598-233">b.</span><span class="sxs-lookup"><span data-stu-id="4b598-233">b.</span></span> <span data-ttu-id="4b598-234">Jako **dostawcy synchronizacji wybierz**, wybierz pozycję **Microsoft / usługi Office 365**.</span><span class="sxs-lookup"><span data-stu-id="4b598-234">As **Choose sync provider**, select **Microsoft / Office 365**.</span></span>
   
   <span data-ttu-id="4b598-235">c.</span><span class="sxs-lookup"><span data-stu-id="4b598-235">c.</span></span> <span data-ttu-id="4b598-236">Kliknij przycisk **Przeprowadź synchronizację użytkownika**.</span><span class="sxs-lookup"><span data-stu-id="4b598-236">Click **Run User Sync**.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="4b598-237">Przypisanie użytkownika testowego hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="4b598-237">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="4b598-238">W tej sekcji możesz włączyć toouse Simona Britta Azure logowania jednokrotnego za udzielanie dostępu tooRecognize.</span><span class="sxs-lookup"><span data-stu-id="4b598-238">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooRecognize.</span></span>

![Przypisz użytkownika][200] 

<span data-ttu-id="4b598-240">**tooassign tooRecognize Simona Britta wykonaj hello następujące kroki:**</span><span class="sxs-lookup"><span data-stu-id="4b598-240">**tooassign Britta Simon tooRecognize, perform hello following steps:**</span></span>

1. <span data-ttu-id="4b598-241">W portalu Azure hello, otwórz widok aplikacji hello, a następnie przejdź do widoku katalogu toohello i przejść za**aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="4b598-241">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Przypisz użytkownika][201] 

2. <span data-ttu-id="4b598-243">Z listy aplikacji hello wybierz **rozpoznawanie**.</span><span class="sxs-lookup"><span data-stu-id="4b598-243">In hello applications list, select **Recognize**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-recognize-tutorial/tutorial_recognize_app.png) 

3. <span data-ttu-id="4b598-245">W menu powitania po lewej stronie powitania kliknij **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="4b598-245">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Przypisz użytkownika][202] 

4. <span data-ttu-id="4b598-247">Kliknij przycisk **Dodaj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="4b598-247">Click **Add** button.</span></span> <span data-ttu-id="4b598-248">Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="4b598-248">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Przypisz użytkownika][203]

5. <span data-ttu-id="4b598-250">Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** hello listy użytkowników.</span><span class="sxs-lookup"><span data-stu-id="4b598-250">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="4b598-251">Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="4b598-251">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="4b598-252">Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="4b598-252">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="4b598-253">Testowanie rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="4b598-253">Testing single sign-on</span></span>

<span data-ttu-id="4b598-254">Celem Hello w tej sekcji jest tootest użyciu usługi Azure AD konfiguracji rejestracji jednokrotnej hello panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="4b598-254">hello objective of this section is tootest your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="4b598-255">Po kliknięciu kafelka rozpoznawanie hello w hello Panel dostępu, należy pobrać automatycznie zalogowane tooyour rozpoznawanie aplikacji.</span><span class="sxs-lookup"><span data-stu-id="4b598-255">When you click hello Recognize tile in hello Access Panel, you should get automatically signed-on tooyour Recognize application.</span></span> <span data-ttu-id="4b598-256">Aby uzyskać więcej informacji na temat hello Panel dostępu, zobacz [toohello wprowadzenie panelu dostępu](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="4b598-256">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="4b598-257">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="4b598-257">Additional resources</span></span>

* [<span data-ttu-id="4b598-258">Lista samouczków dotyczących tooIntegrate aplikacji SaaS w usłudze Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="4b598-258">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="4b598-259">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="4b598-259">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-recognize-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-recognize-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-recognize-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-recognize-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-recognize-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-recognize-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-recognize-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-recognize-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-recognize-tutorial/tutorial_general_203.png

