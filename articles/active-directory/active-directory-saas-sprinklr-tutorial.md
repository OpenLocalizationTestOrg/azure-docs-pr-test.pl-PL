---
title: 'Samouczek: Integracji Azure Active Directory z Sprinklr | Dokumentacja firmy Microsoft'
description: "Dowiedz się, jak tooconfigure logowanie jednokrotne między usługą Azure Active Directory i Sprinklr."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: b33938a1-25a5-484c-8e75-7dc6de2d534d
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/10/2017
ms.author: jeedes
ms.openlocfilehash: 14b467c72d4a453ed7ad248eadcdade710f105af
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-sprinklr"></a><span data-ttu-id="8452b-103">Samouczek: Integracji Azure Active Directory z Sprinklr</span><span class="sxs-lookup"><span data-stu-id="8452b-103">Tutorial: Azure Active Directory integration with Sprinklr</span></span>

<span data-ttu-id="8452b-104">Z tego samouczka, dowiesz się, jak toointegrate Sprinklr w usłudze Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="8452b-104">In this tutorial, you learn how toointegrate Sprinklr with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="8452b-105">Integracja z usługą Azure AD Sprinklr zapewnia hello następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="8452b-105">Integrating Sprinklr with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="8452b-106">Można kontrolować w usłudze Azure AD, kto ma dostęp do tooSprinklr</span><span class="sxs-lookup"><span data-stu-id="8452b-106">You can control in Azure AD who has access tooSprinklr</span></span>
- <span data-ttu-id="8452b-107">Można włączyć użytkownika użytkownicy tooautomatically get zalogowane tooSprinklr (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="8452b-107">You can enable your users tooautomatically get signed-on tooSprinklr (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="8452b-108">Możesz zarządzać kont w jednej centralnej lokalizacji - hello portalu Azure</span><span class="sxs-lookup"><span data-stu-id="8452b-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="8452b-109">Jeśli chcesz tooknow więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="8452b-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="8452b-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="8452b-110">Prerequisites</span></span>

<span data-ttu-id="8452b-111">tooconfigure integracji z usługą Azure AD z Sprinklr należy hello następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="8452b-111">tooconfigure Azure AD integration with Sprinklr, you need hello following items:</span></span>

- <span data-ttu-id="8452b-112">Subskrypcję usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="8452b-112">An Azure AD subscription</span></span>
- <span data-ttu-id="8452b-113">Sprinklr jednokrotnego włączone subskrypcji</span><span class="sxs-lookup"><span data-stu-id="8452b-113">A Sprinklr single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="8452b-114">tootest hello kroków w tym samouczku, zaleca się przy użyciu środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="8452b-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="8452b-115">tootest hello kroki opisane w tym samouczku, należy stosować te zalecenia:</span><span class="sxs-lookup"><span data-stu-id="8452b-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="8452b-116">Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="8452b-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="8452b-117">Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz pobrać miesięczna wersja próbna [tutaj](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="8452b-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="8452b-118">Opis scenariusza</span><span class="sxs-lookup"><span data-stu-id="8452b-118">Scenario description</span></span>
<span data-ttu-id="8452b-119">W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym.</span><span class="sxs-lookup"><span data-stu-id="8452b-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="8452b-120">Scenariusz Hello opisane w tym samouczku składa się z dwóch głównych elementów:</span><span class="sxs-lookup"><span data-stu-id="8452b-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="8452b-121">Dodawanie Sprinklr z galerii hello</span><span class="sxs-lookup"><span data-stu-id="8452b-121">Adding Sprinklr from hello gallery</span></span>
2. <span data-ttu-id="8452b-122">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="8452b-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-sprinklr-from-hello-gallery"></a><span data-ttu-id="8452b-123">Dodawanie Sprinklr z galerii hello</span><span class="sxs-lookup"><span data-stu-id="8452b-123">Adding Sprinklr from hello gallery</span></span>
<span data-ttu-id="8452b-124">tooconfigure hello integracji Sprinklr do usługi Azure AD, należy tooadd Sprinklr z hello galerii tooyour listę zarządzanych aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="8452b-124">tooconfigure hello integration of Sprinklr into Azure AD, you need tooadd Sprinklr from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="8452b-125">**tooadd Sprinklr z galerii hello, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="8452b-125">**tooadd Sprinklr from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="8452b-126">W hello  **[portalu Azure](https://portal.azure.com)**na temat hello panelu nawigacji po lewej stronie, kliknij przycisk **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="8452b-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Usługa Active Directory][1]

2. <span data-ttu-id="8452b-128">Przejdź za**aplikacje dla przedsiębiorstw**.</span><span class="sxs-lookup"><span data-stu-id="8452b-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="8452b-129">Następnie przejdź zbyt**wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="8452b-129">Then go too**All applications**.</span></span>

    ![Aplikacje][2]
    
3. <span data-ttu-id="8452b-131">tooadd nową aplikację, kliknij przycisk **nowej aplikacji** przycisk u góry hello okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="8452b-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplikacje][3]

4. <span data-ttu-id="8452b-133">W polu wyszukiwania hello wpisz **Sprinklr**.</span><span class="sxs-lookup"><span data-stu-id="8452b-133">In hello search box, type **Sprinklr**.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-sprinklr-tutorial/tutorial_sprinklr_search.png)

5. <span data-ttu-id="8452b-135">W panelu wyników hello zaznacz **Sprinklr**, a następnie kliknij przycisk **Dodaj** przycisk aplikacji hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="8452b-135">In hello results panel, select **Sprinklr**, and then click **Add** button tooadd hello application.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-sprinklr-tutorial/tutorial_sprinklr_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="8452b-137">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="8452b-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="8452b-138">W tej sekcji możesz skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z Sprinklr na podstawie użytkownika testowego, nazywany "Britta Simona".</span><span class="sxs-lookup"><span data-stu-id="8452b-138">In this section, you configure and test Azure AD single sign-on with Sprinklr based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="8452b-139">Dla pojedynczego logowania jednokrotnego toowork usługi Azure AD musi tooknow użytkownika odpowiednikiem hello w Sprinklr jest tooa użytkownika w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="8452b-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Sprinklr is tooa user in Azure AD.</span></span> <span data-ttu-id="8452b-140">Innymi słowy relację łącza między użytkownika usługi Azure AD i hello użytkownikowi w Sprinklr musi toobe ustanowione.</span><span class="sxs-lookup"><span data-stu-id="8452b-140">In other words, a link relationship between an Azure AD user and hello related user in Sprinklr needs toobe established.</span></span>

<span data-ttu-id="8452b-141">W Sprinklr, należy przypisać wartość hello hello **nazwy użytkownika** w usłudze Azure AD jako wartość hello hello **Username** tooestablish hello łącze relacji.</span><span class="sxs-lookup"><span data-stu-id="8452b-141">In Sprinklr, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="8452b-142">tooconfigure i testowych usługi Azure AD rejestracji jednokrotnej z Sprinklr, należy po bloków konstrukcyjnych hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="8452b-142">tooconfigure and test Azure AD single sign-on with Sprinklr, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="8452b-143">**[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configuring-azure-ad-single-sign-on)**  -tooenable Twojego toouse użytkowników tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="8452b-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="8452b-144">**[Tworzenie użytkownika testowego usługi Azure AD](#creating-an-azure-ad-test-user)**  -tootest usługi Azure AD rejestracji jednokrotnej z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="8452b-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="8452b-145">**[Tworzenie użytkownika testowego Sprinklr](#creating-a-sprinklr-test-user)**  -toohave odpowiednikiem Simona Britta w Sprinklr, który jest połączony toohello usługi Azure AD reprezentację użytkownika.</span><span class="sxs-lookup"><span data-stu-id="8452b-145">**[Creating a Sprinklr test user](#creating-a-sprinklr-test-user)** - toohave a counterpart of Britta Simon in Sprinklr that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="8452b-146">**[Przypisanie użytkownika testowego hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Simona Britta toouse usługi Azure AD rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="8452b-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="8452b-147">**[Testowanie rejestracji jednokrotnej](#testing-single-sign-on)**  -tooverify czy hello konfiguracji działania.</span><span class="sxs-lookup"><span data-stu-id="8452b-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="8452b-148">Konfigurowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="8452b-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="8452b-149">W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w portalu Azure hello i skonfigurować logowanie jednokrotne w aplikacji Sprinklr.</span><span class="sxs-lookup"><span data-stu-id="8452b-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Sprinklr application.</span></span>

<span data-ttu-id="8452b-150">**tooconfigure usługi Azure AD rejestracji jednokrotnej z Sprinklr, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="8452b-150">**tooconfigure Azure AD single sign-on with Sprinklr, perform hello following steps:**</span></span>

1. <span data-ttu-id="8452b-151">W portalu Azure na powitania hello **Sprinklr** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.</span><span class="sxs-lookup"><span data-stu-id="8452b-151">In hello Azure portal, on hello **Sprinklr** application integration page, click **Single sign-on**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej][4]

2. <span data-ttu-id="8452b-153">Na powitania **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** tooenable rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="8452b-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-sprinklr-tutorial/tutorial_sprinklr_samlbase.png)

3. <span data-ttu-id="8452b-155">Na powitania **Sprinklr domeny i adres URL** sekcji, wykonaj następujące kroki hello:</span><span class="sxs-lookup"><span data-stu-id="8452b-155">On hello **Sprinklr Domain and URLs** section, perform hello following steps:</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-sprinklr-tutorial/tutorial_sprinklr_url.png)

    <span data-ttu-id="8452b-157">a.</span><span class="sxs-lookup"><span data-stu-id="8452b-157">a.</span></span> <span data-ttu-id="8452b-158">W hello **adres URL logowania** tekstowym, wpisz adres URL za pomocą hello następującego wzorca:`https://<subdomain>.sprinklr.com`</span><span class="sxs-lookup"><span data-stu-id="8452b-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<subdomain>.sprinklr.com`</span></span>

    <span data-ttu-id="8452b-159">b.</span><span class="sxs-lookup"><span data-stu-id="8452b-159">b.</span></span> <span data-ttu-id="8452b-160">W hello **identyfikator** tekstowym, wpisz adres URL za pomocą hello następującego wzorca:`https://<subdomain>.sprinklr.com`</span><span class="sxs-lookup"><span data-stu-id="8452b-160">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<subdomain>.sprinklr.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="8452b-161">Wartości te nie są prawdziwe.</span><span class="sxs-lookup"><span data-stu-id="8452b-161">These values are not real.</span></span> <span data-ttu-id="8452b-162">Zaktualizuj wartość hello z hello rzeczywisty adres URL logowania i identyfikator.</span><span class="sxs-lookup"><span data-stu-id="8452b-162">Update hello value with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="8452b-163">Skontaktuj się z [zespołem pomocy technicznej klienta Sprinklr](https://www.sprinklr.com/contact-us/) tooget tych wartości.</span><span class="sxs-lookup"><span data-stu-id="8452b-163">Contact [Sprinklr Client support team](https://www.sprinklr.com/contact-us/) tooget these values.</span></span> 
 
4. <span data-ttu-id="8452b-164">Na powitania **certyfikat podpisywania SAML** kliknij **certyfikatu (Base64)** , a następnie zapisz plik certyfikatu hello na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="8452b-164">On hello **SAML Signing Certificate** section, click **Certificate (Base64)** and then save hello certificate file on your computer.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-sprinklr-tutorial/tutorial_sprinklr_certificate.png) 

5. <span data-ttu-id="8452b-166">Kliknij przycisk **zapisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="8452b-166">Click **Save** button.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-sprinklr-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="8452b-168">Na powitania **konfiguracji Sprinklr** kliknij **skonfigurować Sprinklr** tooopen **Konfigurowanie logowania jednokrotnego** okna.</span><span class="sxs-lookup"><span data-stu-id="8452b-168">On hello **Sprinklr Configuration** section, click **Configure Sprinklr** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="8452b-169">Kopiuj hello **Sign-Out adres URL, identyfikator jednostki SAML i SAML pojedynczy znak na adres URL usługi** z hello **sekcji krótkimi opisami.**</span><span class="sxs-lookup"><span data-stu-id="8452b-169">Copy hello **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

7. <span data-ttu-id="8452b-170">W oknie przeglądarki innej witryny sieci web Zaloguj się w witrynie firmy Sprinklr tooyour jako administrator.</span><span class="sxs-lookup"><span data-stu-id="8452b-170">In a different web browser window, log in tooyour Sprinklr company site as an administrator.</span></span>

8. <span data-ttu-id="8452b-171">Przejdź za**administracji \> ustawienia**.</span><span class="sxs-lookup"><span data-stu-id="8452b-171">Go too**Administration \> Settings**.</span></span>
   
    <span data-ttu-id="8452b-172">![Administracja](./media/active-directory-saas-sprinklr-tutorial/ic782907.png "administracji")</span><span class="sxs-lookup"><span data-stu-id="8452b-172">![Administration](./media/active-directory-saas-sprinklr-tutorial/ic782907.png "Administration")</span></span>

9. <span data-ttu-id="8452b-173">Przejdź za**Zarządzanie partnera \> jednokrotnego** na w okienku po lewej stronie powitania.</span><span class="sxs-lookup"><span data-stu-id="8452b-173">Go too**Manage Partner \> Single Sign** on from hello left pane.</span></span>
   
    <span data-ttu-id="8452b-174">![Zarządzanie partnerem](./media/active-directory-saas-sprinklr-tutorial/ic782908.png "Zarządzanie partnera")</span><span class="sxs-lookup"><span data-stu-id="8452b-174">![Manage Partner](./media/active-directory-saas-sprinklr-tutorial/ic782908.png "Manage Partner")</span></span>

10. <span data-ttu-id="8452b-175">Kliknij przycisk **+ dodatki jednokrotnego**.</span><span class="sxs-lookup"><span data-stu-id="8452b-175">Click **+Add Single Sign Ons**.</span></span>
   
    <span data-ttu-id="8452b-176">![Pojedynczy prób logowania](./media/active-directory-saas-sprinklr-tutorial/ic782909.png "pojedynczy prób logowania")</span><span class="sxs-lookup"><span data-stu-id="8452b-176">![Single Sign-Ons](./media/active-directory-saas-sprinklr-tutorial/ic782909.png "Single Sign-Ons")</span></span>

11. <span data-ttu-id="8452b-177">Na powitania **logowania jednokrotnego** wykonaj hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="8452b-177">On hello **Single Sign on** page, perform hello following steps:</span></span>
   
    <span data-ttu-id="8452b-178">![Pojedynczy prób logowania](./media/active-directory-saas-sprinklr-tutorial/ic782910.png "pojedynczy prób logowania")</span><span class="sxs-lookup"><span data-stu-id="8452b-178">![Single Sign-Ons](./media/active-directory-saas-sprinklr-tutorial/ic782910.png "Single Sign-Ons")</span></span>

    <span data-ttu-id="8452b-179">a.</span><span class="sxs-lookup"><span data-stu-id="8452b-179">a.</span></span> <span data-ttu-id="8452b-180">W hello **nazwa** tekstowym, wpisz nazwę konfiguracji (na przykład: *WAADSSOTest*).</span><span class="sxs-lookup"><span data-stu-id="8452b-180">In hello **Name** textbox, type a name for your configuration (for example: *WAADSSOTest*).</span></span>

    <span data-ttu-id="8452b-181">b.</span><span class="sxs-lookup"><span data-stu-id="8452b-181">b.</span></span> <span data-ttu-id="8452b-182">Wybierz **włączone**.</span><span class="sxs-lookup"><span data-stu-id="8452b-182">Select **Enabled**.</span></span>

    <span data-ttu-id="8452b-183">c.</span><span class="sxs-lookup"><span data-stu-id="8452b-183">c.</span></span> <span data-ttu-id="8452b-184">Wybierz **korzystania z nowego certyfikatu logowania jednokrotnego**.</span><span class="sxs-lookup"><span data-stu-id="8452b-184">Select **Use new SSO Certificate**.</span></span>
             
    <span data-ttu-id="8452b-185">e.</span><span class="sxs-lookup"><span data-stu-id="8452b-185">e.</span></span> <span data-ttu-id="8452b-186">Otwieranie certyfikatu zakodowanego base-64 w Notatniku hello kopiowania zawartości go do Schowka, a następnie wklej go toohello **certyfikat dostawcy tożsamości** pola tekstowego.</span><span class="sxs-lookup"><span data-stu-id="8452b-186">Open your base-64 encoded certificate in notepad, copy hello content of it into your clipboard, and then paste it toohello **Identity Provider Certificate** textbox.</span></span>

    <span data-ttu-id="8452b-187">f.</span><span class="sxs-lookup"><span data-stu-id="8452b-187">f.</span></span> <span data-ttu-id="8452b-188">Wklej hello **identyfikator jednostki SAML** wartość, która została skopiowana z portalu Azure do hello **identyfikator jednostki** pola tekstowego.</span><span class="sxs-lookup"><span data-stu-id="8452b-188">Paste hello **SAML Entity ID** value which you have copied from Azure Portal into hello **Entity Id** textbox.</span></span>

    <span data-ttu-id="8452b-189">g.</span><span class="sxs-lookup"><span data-stu-id="8452b-189">g.</span></span> <span data-ttu-id="8452b-190">Wklej hello **SAML pojedynczy znak na adres URL usługi** wartość, która została skopiowana z portalu Azure do hello **adresu URL logowania do dostawcy tożsamości** pola tekstowego.</span><span class="sxs-lookup"><span data-stu-id="8452b-190">Paste hello **SAML Single Sign-On Service URL** value which you have copied from Azure Portal into hello **Identity Provider Login URL** textbox.</span></span>

    <span data-ttu-id="8452b-191">h.</span><span class="sxs-lookup"><span data-stu-id="8452b-191">h.</span></span> <span data-ttu-id="8452b-192">Wklej hello **Sign-Out URL** wartość, która została skopiowana z portalu Azure do hello **adres URL wylogowania dostawcy tożsamości** pola tekstowego.</span><span class="sxs-lookup"><span data-stu-id="8452b-192">Paste hello **Sign-Out URL** value which you have copied from Azure Portal into hello **Identity Provider Logout URL** textbox.</span></span>
     
    <span data-ttu-id="8452b-193">i.</span><span class="sxs-lookup"><span data-stu-id="8452b-193">i.</span></span> <span data-ttu-id="8452b-194">Jako **typ Identyfikatora użytkownika SAML**, wybierz pozycję **potwierdzenia zawiera użytkownika "s sprinklr.com username**.</span><span class="sxs-lookup"><span data-stu-id="8452b-194">As **SAML User ID Type**, select **Assertion contains User”s sprinklr.com username**.</span></span>

    <span data-ttu-id="8452b-195">j.</span><span class="sxs-lookup"><span data-stu-id="8452b-195">j.</span></span> <span data-ttu-id="8452b-196">Jako **lokalizacji identyfikator użytkownika SAML**, wybierz pozycję **identyfikator użytkownika jest w elemencie identyfikator nazwy hello hello instrukcji podmiotu**.</span><span class="sxs-lookup"><span data-stu-id="8452b-196">As **SAML User ID Location**, select **User ID is in hello Name Identifier element of hello Subject statement**.</span></span>

    <span data-ttu-id="8452b-197">k.</span><span class="sxs-lookup"><span data-stu-id="8452b-197">k.</span></span> <span data-ttu-id="8452b-198">Kliknij pozycję **Zapisz**.</span><span class="sxs-lookup"><span data-stu-id="8452b-198">Click **Save**.</span></span>
       
    <span data-ttu-id="8452b-199">![SAML](./media/active-directory-saas-sprinklr-tutorial/ic782911.png "SAML")</span><span class="sxs-lookup"><span data-stu-id="8452b-199">![SAML](./media/active-directory-saas-sprinklr-tutorial/ic782911.png "SAML")</span></span>

> [!TIP]
> <span data-ttu-id="8452b-200">Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz hello [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji hello!</span><span class="sxs-lookup"><span data-stu-id="8452b-200">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="8452b-201">Po dodaniu tej aplikacji z hello **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij hello **rejestracji jednokrotnej** hello kartę i dostępu do osadzonych dokumentacji za pośrednictwem hello  **Konfiguracja** sekcji u dołu hello.</span><span class="sxs-lookup"><span data-stu-id="8452b-201">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="8452b-202">Więcej o hello osadzonych dokumentacji funkcji w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="8452b-202">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="8452b-203">Tworzenie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="8452b-203">Creating an Azure AD test user</span></span>
<span data-ttu-id="8452b-204">Celem Hello w tej sekcji jest toocreate użytkownika testowego, w portalu Azure o nazwie Simona Britta hello.</span><span class="sxs-lookup"><span data-stu-id="8452b-204">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Tworzenie użytkowników usługi Azure AD][100]

<span data-ttu-id="8452b-206">**toocreate użytkownika testowego w usłudze Azure AD, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="8452b-206">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="8452b-207">W hello **portalu Azure**na temat hello w lewym okienku nawigacji, kliknij przycisk **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="8452b-207">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-sprinklr-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="8452b-209">toodisplay hello listę użytkowników, przejdź zbyt**użytkowników i grup** i kliknij przycisk **wszyscy użytkownicy**.</span><span class="sxs-lookup"><span data-stu-id="8452b-209">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-sprinklr-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="8452b-211">Witaj tooopen **użytkownika** okna dialogowego, kliknij przycisk **Dodaj** u góry hello hello okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="8452b-211">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-sprinklr-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="8452b-213">Na powitania **użytkownika** okna dialogowego wykonaj hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="8452b-213">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-sprinklr-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="8452b-215">a.</span><span class="sxs-lookup"><span data-stu-id="8452b-215">a.</span></span> <span data-ttu-id="8452b-216">W hello **nazwa** pole tekstowe, typ **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="8452b-216">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="8452b-217">b.</span><span class="sxs-lookup"><span data-stu-id="8452b-217">b.</span></span> <span data-ttu-id="8452b-218">W hello **nazwy użytkownika** pole tekstowe, hello typu **adres e-mail** z BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="8452b-218">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="8452b-219">c.</span><span class="sxs-lookup"><span data-stu-id="8452b-219">c.</span></span> <span data-ttu-id="8452b-220">Wybierz **Pokaż hasło** i zanotuj wartość hello hello **hasło**.</span><span class="sxs-lookup"><span data-stu-id="8452b-220">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="8452b-221">d.</span><span class="sxs-lookup"><span data-stu-id="8452b-221">d.</span></span> <span data-ttu-id="8452b-222">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="8452b-222">Click **Create**.</span></span>
 
### <a name="creating-a-sprinklr-test-user"></a><span data-ttu-id="8452b-223">Tworzenie użytkownika testowego Sprinklr</span><span class="sxs-lookup"><span data-stu-id="8452b-223">Creating a Sprinklr test user</span></span>

1. <span data-ttu-id="8452b-224">Zaloguj się za tooyour Sprinklr witryny firmy jako administrator.</span><span class="sxs-lookup"><span data-stu-id="8452b-224">Log in tooyour Sprinklr company site as an administrator.</span></span>

2. <span data-ttu-id="8452b-225">Przejdź za**administracji \> ustawienia**.</span><span class="sxs-lookup"><span data-stu-id="8452b-225">Go too**Administration \> Settings**.</span></span>
   
    <span data-ttu-id="8452b-226">![Administracja](./media/active-directory-saas-sprinklr-tutorial/ic782907.png "administracji")</span><span class="sxs-lookup"><span data-stu-id="8452b-226">![Administration](./media/active-directory-saas-sprinklr-tutorial/ic782907.png "Administration")</span></span>

3. <span data-ttu-id="8452b-227">Przejdź za**klienta zarządzania \> użytkowników** w okienku po lewej stronie powitania.</span><span class="sxs-lookup"><span data-stu-id="8452b-227">Go too**Manage Client \> Users** from hello left pane.</span></span>
   
    <span data-ttu-id="8452b-228">![Ustawienia](./media/active-directory-saas-sprinklr-tutorial/ic782914.png "ustawienia")</span><span class="sxs-lookup"><span data-stu-id="8452b-228">![Settings](./media/active-directory-saas-sprinklr-tutorial/ic782914.png "Settings")</span></span>

4. <span data-ttu-id="8452b-229">Kliknij przycisk **dodać użytkownika**.</span><span class="sxs-lookup"><span data-stu-id="8452b-229">Click **Add User**.</span></span>
   
    <span data-ttu-id="8452b-230">![Ustawienia](./media/active-directory-saas-sprinklr-tutorial/ic782915.png "ustawienia")</span><span class="sxs-lookup"><span data-stu-id="8452b-230">![Settings](./media/active-directory-saas-sprinklr-tutorial/ic782915.png "Settings")</span></span>

5. <span data-ttu-id="8452b-231">Na powitania **Edycja użytkownika** okna dialogowego, wykonaj następujące kroki hello:</span><span class="sxs-lookup"><span data-stu-id="8452b-231">On hello **Edit user** dialog, perform hello following steps:</span></span>
   
    <span data-ttu-id="8452b-232">![Edytowanie użytkownika](./media/active-directory-saas-sprinklr-tutorial/ic782916.png "Edycja użytkownika")</span><span class="sxs-lookup"><span data-stu-id="8452b-232">![Edit user](./media/active-directory-saas-sprinklr-tutorial/ic782916.png "Edit user")</span></span> 

    <span data-ttu-id="8452b-233">a.</span><span class="sxs-lookup"><span data-stu-id="8452b-233">a.</span></span> <span data-ttu-id="8452b-234">W hello **E-mail**, **imię** i **nazwisko** pól tekstowych, informacje o typie hello ma tooprovision konta użytkownika usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="8452b-234">In hello **Email**, **First Name** and **Last Name** textboxes, type hello information of an Azure AD user account you want tooprovision.</span></span>

    <span data-ttu-id="8452b-235">b.</span><span class="sxs-lookup"><span data-stu-id="8452b-235">b.</span></span> <span data-ttu-id="8452b-236">Wybierz **wyłączone hasło**.</span><span class="sxs-lookup"><span data-stu-id="8452b-236">Select **Password Disabled**.</span></span>

    <span data-ttu-id="8452b-237">c.</span><span class="sxs-lookup"><span data-stu-id="8452b-237">c.</span></span> <span data-ttu-id="8452b-238">Wybierz **języka**.</span><span class="sxs-lookup"><span data-stu-id="8452b-238">Select **Language**.</span></span>

    <span data-ttu-id="8452b-239">d.</span><span class="sxs-lookup"><span data-stu-id="8452b-239">d.</span></span> <span data-ttu-id="8452b-240">Wybierz **typ użytkownika**.</span><span class="sxs-lookup"><span data-stu-id="8452b-240">Select **User Type**.</span></span>

    <span data-ttu-id="8452b-241">e.</span><span class="sxs-lookup"><span data-stu-id="8452b-241">e.</span></span> <span data-ttu-id="8452b-242">Kliknij przycisk **aktualizacji**.</span><span class="sxs-lookup"><span data-stu-id="8452b-242">Click **Update**.</span></span>
   
     >[!IMPORTANT]
     ><span data-ttu-id="8452b-243">**Wyłączone hasło** musi być wybrany tooenable toolog użytkownika w za pośrednictwem dostawcy tożsamości.</span><span class="sxs-lookup"><span data-stu-id="8452b-243">**Password Disabled** must be selected tooenable a user toolog in via an Identity provider.</span></span> 
     
6. <span data-ttu-id="8452b-244">Przejdź za**roli**, a następnie wykonaj następujące kroki hello:</span><span class="sxs-lookup"><span data-stu-id="8452b-244">Go too**Role**, and then perform hello following steps:</span></span>
   
    <span data-ttu-id="8452b-245">![Partnera ról](./media/active-directory-saas-sprinklr-tutorial/ic782917.png "partnera ról")</span><span class="sxs-lookup"><span data-stu-id="8452b-245">![Partner Roles](./media/active-directory-saas-sprinklr-tutorial/ic782917.png "Partner Roles")</span></span>

    <span data-ttu-id="8452b-246">a.</span><span class="sxs-lookup"><span data-stu-id="8452b-246">a.</span></span> <span data-ttu-id="8452b-247">Z hello **Global** listy, wybierz **wszystkie\_uprawnienia**.</span><span class="sxs-lookup"><span data-stu-id="8452b-247">From hello **Global** list, select **ALL\_Permissions**.</span></span>  

    <span data-ttu-id="8452b-248">b.</span><span class="sxs-lookup"><span data-stu-id="8452b-248">b.</span></span> <span data-ttu-id="8452b-249">Kliknij przycisk **aktualizacji**.</span><span class="sxs-lookup"><span data-stu-id="8452b-249">Click **Update**.</span></span>

>[!NOTE]
><span data-ttu-id="8452b-250">Możesz użyć innych Sprinklr użytkownika konta tworzenia narzędzi lub interfejsów API dostarczonych przez Sprinklr tooprovision kont użytkowników usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="8452b-250">You can use any other Sprinklr user account creation tools or APIs provided by Sprinklr tooprovision Azure AD user accounts.</span></span> 

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="8452b-251">Przypisanie użytkownika testowego hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="8452b-251">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="8452b-252">W tej sekcji możesz włączyć toouse Simona Britta Azure logowania jednokrotnego za udzielanie dostępu tooSprinklr.</span><span class="sxs-lookup"><span data-stu-id="8452b-252">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooSprinklr.</span></span>

![Przypisz użytkownika][200] 

<span data-ttu-id="8452b-254">**tooassign tooSprinklr Simona Britta wykonaj hello następujące kroki:**</span><span class="sxs-lookup"><span data-stu-id="8452b-254">**tooassign Britta Simon tooSprinklr, perform hello following steps:**</span></span>

1. <span data-ttu-id="8452b-255">W portalu Azure hello, otwórz widok aplikacji hello, a następnie przejdź do widoku katalogu toohello i przejść za**aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="8452b-255">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Przypisz użytkownika][201] 

2. <span data-ttu-id="8452b-257">Z listy aplikacji hello wybierz **Sprinklr**.</span><span class="sxs-lookup"><span data-stu-id="8452b-257">In hello applications list, select **Sprinklr**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-sprinklr-tutorial/tutorial_sprinklr_app.png) 

3. <span data-ttu-id="8452b-259">W menu powitania po lewej stronie powitania kliknij **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="8452b-259">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Przypisz użytkownika][202] 

4. <span data-ttu-id="8452b-261">Kliknij przycisk **Dodaj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="8452b-261">Click **Add** button.</span></span> <span data-ttu-id="8452b-262">Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="8452b-262">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Przypisz użytkownika][203]

5. <span data-ttu-id="8452b-264">Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** hello listy użytkowników.</span><span class="sxs-lookup"><span data-stu-id="8452b-264">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="8452b-265">Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="8452b-265">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="8452b-266">Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="8452b-266">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="8452b-267">Testowanie rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="8452b-267">Testing single sign-on</span></span>

<span data-ttu-id="8452b-268">W tej sekcji można przetestować konfiguracji usługi Azure AD pojedynczego logowania jednokrotnego przy użyciu hello panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="8452b-268">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="8452b-269">Po kliknięciu kafelka Sprinklr hello w hello panelu dostępu get automatycznie zalogowane tooyour Sprinklr aplikacji, aby uzyskać więcej informacji na temat hello panelu dostępu, zobacz [toohello wprowadzenie panelu dostępu](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="8452b-269">When you click hello Sprinklr tile in hello Access Panel, you should get automatically signed-on tooyour Sprinklr application For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="8452b-270">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="8452b-270">Additional resources</span></span>

* [<span data-ttu-id="8452b-271">Lista samouczków dotyczących tooIntegrate aplikacji SaaS w usłudze Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="8452b-271">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="8452b-272">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="8452b-272">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-sprinklr-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-sprinklr-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-sprinklr-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-sprinklr-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-sprinklr-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-sprinklr-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-sprinklr-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-sprinklr-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-sprinklr-tutorial/tutorial_general_203.png

