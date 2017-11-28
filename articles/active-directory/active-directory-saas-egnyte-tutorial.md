---
title: 'Samouczek: Integracji Azure Active Directory z Egnyte | Dokumentacja firmy Microsoft'
description: "Dowiedz się, jak tooconfigure logowanie jednokrotne między usługą Azure Active Directory i Egnyte."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 8c2101d4-1779-4b36-8464-5c1ff780da18
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/18/2017
ms.author: jeedes
ms.openlocfilehash: d86fa28a1e7b23474cb76c08aef8539acadaf24d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-egnyte"></a><span data-ttu-id="6fe8e-103">Samouczek: Integracji Azure Active Directory z Egnyte</span><span class="sxs-lookup"><span data-stu-id="6fe8e-103">Tutorial: Azure Active Directory integration with Egnyte</span></span>

<span data-ttu-id="6fe8e-104">Z tego samouczka, dowiesz się, jak toointegrate Egnyte w usłudze Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="6fe8e-104">In this tutorial, you learn how toointegrate Egnyte with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="6fe8e-105">Integracja z usługą Azure AD Egnyte zapewnia hello następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="6fe8e-105">Integrating Egnyte with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="6fe8e-106">Można kontrolować w usłudze Azure AD, kto ma dostęp do tooEgnyte</span><span class="sxs-lookup"><span data-stu-id="6fe8e-106">You can control in Azure AD who has access tooEgnyte</span></span>
- <span data-ttu-id="6fe8e-107">Można włączyć użytkownika użytkownicy tooautomatically get zalogowane tooEgnyte (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="6fe8e-107">You can enable your users tooautomatically get signed-on tooEgnyte (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="6fe8e-108">Możesz zarządzać kont w jednej centralnej lokalizacji - hello portalu Azure</span><span class="sxs-lookup"><span data-stu-id="6fe8e-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="6fe8e-109">Jeśli chcesz tooknow więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="6fe8e-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="6fe8e-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="6fe8e-110">Prerequisites</span></span>

<span data-ttu-id="6fe8e-111">tooconfigure integracji z usługą Azure AD z Egnyte należy hello następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="6fe8e-111">tooconfigure Azure AD integration with Egnyte, you need hello following items:</span></span>

- <span data-ttu-id="6fe8e-112">Subskrypcję usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="6fe8e-112">An Azure AD subscription</span></span>
- <span data-ttu-id="6fe8e-113">Egnyte logowanie jednokrotne włączone subskrypcji</span><span class="sxs-lookup"><span data-stu-id="6fe8e-113">An Egnyte single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="6fe8e-114">tootest hello kroków w tym samouczku, zaleca się przy użyciu środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="6fe8e-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="6fe8e-115">tootest hello kroki opisane w tym samouczku, należy stosować te zalecenia:</span><span class="sxs-lookup"><span data-stu-id="6fe8e-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="6fe8e-116">Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="6fe8e-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="6fe8e-117">Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz pobrać miesięczna wersja próbna [tutaj](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="6fe8e-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="6fe8e-118">Opis scenariusza</span><span class="sxs-lookup"><span data-stu-id="6fe8e-118">Scenario description</span></span>
<span data-ttu-id="6fe8e-119">W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym.</span><span class="sxs-lookup"><span data-stu-id="6fe8e-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="6fe8e-120">Scenariusz Hello opisane w tym samouczku składa się z dwóch głównych elementów:</span><span class="sxs-lookup"><span data-stu-id="6fe8e-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="6fe8e-121">Dodawanie Egnyte z galerii hello</span><span class="sxs-lookup"><span data-stu-id="6fe8e-121">Adding Egnyte from hello gallery</span></span>
2. <span data-ttu-id="6fe8e-122">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="6fe8e-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-egnyte-from-hello-gallery"></a><span data-ttu-id="6fe8e-123">Dodawanie Egnyte z galerii hello</span><span class="sxs-lookup"><span data-stu-id="6fe8e-123">Adding Egnyte from hello gallery</span></span>
<span data-ttu-id="6fe8e-124">tooconfigure hello integracji Egnyte do usługi Azure AD, należy tooadd Egnyte z hello galerii tooyour listę zarządzanych aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="6fe8e-124">tooconfigure hello integration of Egnyte into Azure AD, you need tooadd Egnyte from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="6fe8e-125">**tooadd Egnyte z galerii hello, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="6fe8e-125">**tooadd Egnyte from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="6fe8e-126">W hello  **[portalu Azure](https://portal.azure.com)**na temat hello panelu nawigacji po lewej stronie, kliknij przycisk **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="6fe8e-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Usługa Active Directory][1]

2. <span data-ttu-id="6fe8e-128">Przejdź za**aplikacje dla przedsiębiorstw**.</span><span class="sxs-lookup"><span data-stu-id="6fe8e-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="6fe8e-129">Następnie przejdź zbyt**wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="6fe8e-129">Then go too**All applications**.</span></span>

    ![Aplikacje][2]
    
3. <span data-ttu-id="6fe8e-131">tooadd nową aplikację, kliknij przycisk **nowej aplikacji** przycisk u góry hello okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="6fe8e-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplikacje][3]

4. <span data-ttu-id="6fe8e-133">W polu wyszukiwania hello wpisz **Egnyte**.</span><span class="sxs-lookup"><span data-stu-id="6fe8e-133">In hello search box, type **Egnyte**.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-egnyte-tutorial/tutorial_egnyte_search.png)

5. <span data-ttu-id="6fe8e-135">W panelu wyników hello zaznacz **Egnyte**, a następnie kliknij przycisk **Dodaj** przycisk aplikacji hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="6fe8e-135">In hello results panel, select **Egnyte**, and then click **Add** button tooadd hello application.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-egnyte-tutorial/tutorial_egnyte_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="6fe8e-137">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="6fe8e-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="6fe8e-138">W tej sekcji możesz skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z Egnyte na podstawie użytkownika testowego, nazywany "Britta Simona".</span><span class="sxs-lookup"><span data-stu-id="6fe8e-138">In this section, you configure and test Azure AD single sign-on with Egnyte based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="6fe8e-139">Dla pojedynczego logowania jednokrotnego toowork usługi Azure AD musi tooknow użytkownika odpowiednikiem hello w Egnyte jest tooa użytkownika w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="6fe8e-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Egnyte is tooa user in Azure AD.</span></span> <span data-ttu-id="6fe8e-140">Innymi słowy relację łącza między użytkownika usługi Azure AD i hello użytkownikowi w Egnyte musi toobe ustanowione.</span><span class="sxs-lookup"><span data-stu-id="6fe8e-140">In other words, a link relationship between an Azure AD user and hello related user in Egnyte needs toobe established.</span></span>

<span data-ttu-id="6fe8e-141">W Egnyte, należy przypisać wartość hello hello **nazwy użytkownika** w usłudze Azure AD jako wartość hello hello **Username** tooestablish hello łącze relacji.</span><span class="sxs-lookup"><span data-stu-id="6fe8e-141">In Egnyte, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="6fe8e-142">tooconfigure i testowych usługi Azure AD rejestracji jednokrotnej z Egnyte, należy po bloków konstrukcyjnych hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="6fe8e-142">tooconfigure and test Azure AD single sign-on with Egnyte, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="6fe8e-143">**[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configuring-azure-ad-single-sign-on)**  -tooenable Twojego toouse użytkowników tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="6fe8e-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="6fe8e-144">**[Tworzenie użytkownika testowego usługi Azure AD](#creating-an-azure-ad-test-user)**  -tootest usługi Azure AD rejestracji jednokrotnej z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="6fe8e-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="6fe8e-145">**[Tworzenie użytkownika testowego Egnyte](#creating-an-egnyte-test-user)**  -toohave odpowiednikiem Simona Britta w Egnyte, który jest połączony toohello usługi Azure AD reprezentację użytkownika.</span><span class="sxs-lookup"><span data-stu-id="6fe8e-145">**[Creating an Egnyte test user](#creating-an-egnyte-test-user)** - toohave a counterpart of Britta Simon in Egnyte that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="6fe8e-146">**[Przypisanie użytkownika testowego hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Simona Britta toouse usługi Azure AD rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="6fe8e-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="6fe8e-147">**[Testowanie rejestracji jednokrotnej](#testing-single-sign-on)**  -tooverify czy hello konfiguracji działania.</span><span class="sxs-lookup"><span data-stu-id="6fe8e-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="6fe8e-148">Konfigurowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="6fe8e-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="6fe8e-149">W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w portalu Azure hello i skonfigurować logowanie jednokrotne w aplikacji Egnyte.</span><span class="sxs-lookup"><span data-stu-id="6fe8e-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Egnyte application.</span></span>

<span data-ttu-id="6fe8e-150">**tooconfigure usługi Azure AD rejestracji jednokrotnej z Egnyte, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="6fe8e-150">**tooconfigure Azure AD single sign-on with Egnyte, perform hello following steps:**</span></span>

1. <span data-ttu-id="6fe8e-151">W portalu Azure na powitania hello **Egnyte** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.</span><span class="sxs-lookup"><span data-stu-id="6fe8e-151">In hello Azure portal, on hello **Egnyte** application integration page, click **Single sign-on**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej][4]

2. <span data-ttu-id="6fe8e-153">Na powitania **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** tooenable rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="6fe8e-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-egnyte-tutorial/tutorial_egnyte_samlbase.png)

3. <span data-ttu-id="6fe8e-155">Na powitania **Egnyte domeny i adres URL** sekcji, wykonaj następujące kroki hello:</span><span class="sxs-lookup"><span data-stu-id="6fe8e-155">On hello **Egnyte Domain and URLs** section, perform hello following steps:</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-egnyte-tutorial/tutorial_egnyte_url.png)

    <span data-ttu-id="6fe8e-157">W hello **adres URL logowania** tekstowym, wpisz adres URL za pomocą hello następującego wzorca:`https://<companyname>.egnyte.com`</span><span class="sxs-lookup"><span data-stu-id="6fe8e-157">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<companyname>.egnyte.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="6fe8e-158">Ta wartość nie jest prawdziwe.</span><span class="sxs-lookup"><span data-stu-id="6fe8e-158">This value is not real.</span></span> <span data-ttu-id="6fe8e-159">Zaktualizuj tę wartość z hello rzeczywisty adres URL logowania.</span><span class="sxs-lookup"><span data-stu-id="6fe8e-159">Update this value with hello actual Sign-On URL.</span></span> <span data-ttu-id="6fe8e-160">Skontaktuj się z [zespołem pomocy technicznej klienta Egnyte](https://www.egnyte.com/corp/contact_egnyte.html) tooget tej wartości.</span><span class="sxs-lookup"><span data-stu-id="6fe8e-160">Contact [Egnyte Client support team](https://www.egnyte.com/corp/contact_egnyte.html) tooget this value.</span></span> 
 
4. <span data-ttu-id="6fe8e-161">Na powitania **certyfikat podpisywania SAML** kliknij **Certificate(Base64)** , a następnie zapisz plik certyfikatu hello na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="6fe8e-161">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-egnyte-tutorial/tutorial_egnyte_certificate.png) 

5. <span data-ttu-id="6fe8e-163">Kliknij przycisk **zapisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="6fe8e-163">Click **Save** button.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-egnyte-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="6fe8e-165">Na powitania **konfiguracji Egnyte** kliknij **skonfigurować Egnyte** tooopen **Konfigurowanie logowania jednokrotnego** okna.</span><span class="sxs-lookup"><span data-stu-id="6fe8e-165">On hello **Egnyte Configuration** section, click **Configure Egnyte** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="6fe8e-166">Kopiuj hello **identyfikator jednostki SAML i SAML pojedynczy znak na adres URL usługi** z hello **sekcji krótkimi opisami.**</span><span class="sxs-lookup"><span data-stu-id="6fe8e-166">Copy hello **SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-egnyte-tutorial/tutorial_egnyte_configure.png) 

7. <span data-ttu-id="6fe8e-168">W oknie przeglądarki innej witryny sieci web Zaloguj się w witrynie firmy Egnyte tooyour jako administrator.</span><span class="sxs-lookup"><span data-stu-id="6fe8e-168">In a different web browser window, log in tooyour Egnyte company site as an administrator.</span></span>

8. <span data-ttu-id="6fe8e-169">Kliknij przycisk **ustawienia**.</span><span class="sxs-lookup"><span data-stu-id="6fe8e-169">Click **Settings**.</span></span>
   
   <span data-ttu-id="6fe8e-170">![Ustawienia](./media/active-directory-saas-egnyte-tutorial/ic787819.png "ustawienia")</span><span class="sxs-lookup"><span data-stu-id="6fe8e-170">![Settings](./media/active-directory-saas-egnyte-tutorial/ic787819.png "Settings")</span></span>

9. <span data-ttu-id="6fe8e-171">W menu powitania kliknij **ustawienia**.</span><span class="sxs-lookup"><span data-stu-id="6fe8e-171">In hello menu, click **Settings**.</span></span>

   <span data-ttu-id="6fe8e-172">![Ustawienia](./media/active-directory-saas-egnyte-tutorial/ic787820.png "ustawienia")</span><span class="sxs-lookup"><span data-stu-id="6fe8e-172">![Settings](./media/active-directory-saas-egnyte-tutorial/ic787820.png "Settings")</span></span>

10. <span data-ttu-id="6fe8e-173">Kliknij przycisk hello **konfiguracji** , a następnie kliknij pozycję **zabezpieczeń**.</span><span class="sxs-lookup"><span data-stu-id="6fe8e-173">Click hello **Configuration** tab, and then click **Security**.</span></span>

    <span data-ttu-id="6fe8e-174">![Zabezpieczenia](./media/active-directory-saas-egnyte-tutorial/ic787821.png "zabezpieczeń")</span><span class="sxs-lookup"><span data-stu-id="6fe8e-174">![Security](./media/active-directory-saas-egnyte-tutorial/ic787821.png "Security")</span></span>

11. <span data-ttu-id="6fe8e-175">W hello **uwierzytelniania rejestracji jednokrotnej** sekcji, wykonaj następujące kroki hello:</span><span class="sxs-lookup"><span data-stu-id="6fe8e-175">In hello **Single Sign-On Authentication** section, perform hello following steps:</span></span>

    <span data-ttu-id="6fe8e-176">![Rejestracja jednokrotna na uwierzytelnianie](./media/active-directory-saas-egnyte-tutorial/ic787822.png "Rejestracja jednokrotna dotyczących uwierzytelniania")</span><span class="sxs-lookup"><span data-stu-id="6fe8e-176">![Single Sign On Authentication](./media/active-directory-saas-egnyte-tutorial/ic787822.png "Single Sign On Authentication")</span></span>   
    
    <span data-ttu-id="6fe8e-177">a.</span><span class="sxs-lookup"><span data-stu-id="6fe8e-177">a.</span></span> <span data-ttu-id="6fe8e-178">Jako **uwierzytelniania rejestracji jednokrotnej**, wybierz pozycję **SAML 2.0**.</span><span class="sxs-lookup"><span data-stu-id="6fe8e-178">As **Single sign-on authentication**, select **SAML 2.0**.</span></span>
   
    <span data-ttu-id="6fe8e-179">b.</span><span class="sxs-lookup"><span data-stu-id="6fe8e-179">b.</span></span> <span data-ttu-id="6fe8e-180">Jako **dostawcy tożsamości**, wybierz pozycję **AzureAD**.</span><span class="sxs-lookup"><span data-stu-id="6fe8e-180">As **Identity provider**, select **AzureAD**.</span></span>
   
    <span data-ttu-id="6fe8e-181">c.</span><span class="sxs-lookup"><span data-stu-id="6fe8e-181">c.</span></span> <span data-ttu-id="6fe8e-182">Wklej **SAML pojedynczy znak na adres URL usługi** skopiowany z portalu Azure do hello **adresu URL logowania do dostawcy tożsamości** pola tekstowego.</span><span class="sxs-lookup"><span data-stu-id="6fe8e-182">Paste **SAML Single Sign-On Service URL** copied from Azure portal into hello **Identity provider login URL** textbox.</span></span>
   
    <span data-ttu-id="6fe8e-183">d.</span><span class="sxs-lookup"><span data-stu-id="6fe8e-183">d.</span></span> <span data-ttu-id="6fe8e-184">Wklej **identyfikator jednostki SAML** którego została skopiowana z portalu Azure do hello **identyfikator jednostki dostawcy tożsamości** pola tekstowego.</span><span class="sxs-lookup"><span data-stu-id="6fe8e-184">Paste **SAML Entity ID** which you have copied from Azure portal into hello **Identity provider entity ID** textbox.</span></span>
      
    <span data-ttu-id="6fe8e-185">e.</span><span class="sxs-lookup"><span data-stu-id="6fe8e-185">e.</span></span> <span data-ttu-id="6fe8e-186">Otwieranie certyfikatu zakodowanego base-64 w Notatniku pobrany z portalu Azure, hello kopiowania zawartości go do Schowka, a następnie wklej go toohello **certyfikat dostawcy tożsamości** pola tekstowego.</span><span class="sxs-lookup"><span data-stu-id="6fe8e-186">Open your base-64 encoded certificate in notepad downloaded from Azure portal, copy hello content of it into your clipboard, and then paste it toohello **Identity provider certificate** textbox.</span></span>
   
    <span data-ttu-id="6fe8e-187">f.</span><span class="sxs-lookup"><span data-stu-id="6fe8e-187">f.</span></span> <span data-ttu-id="6fe8e-188">Jako **domyślne mapowanie użytkownika**, wybierz pozycję **adres E-mail**.</span><span class="sxs-lookup"><span data-stu-id="6fe8e-188">As **Default user mapping**, select **Email address**.</span></span>
   
    <span data-ttu-id="6fe8e-189">g.</span><span class="sxs-lookup"><span data-stu-id="6fe8e-189">g.</span></span> <span data-ttu-id="6fe8e-190">Jako **Użyj wartości wystawcy specyficznego dla domeny**, wybierz pozycję **wyłączone**.</span><span class="sxs-lookup"><span data-stu-id="6fe8e-190">As **Use domain-specific issuer value**, select **disabled**.</span></span>
   
    <span data-ttu-id="6fe8e-191">h.</span><span class="sxs-lookup"><span data-stu-id="6fe8e-191">h.</span></span> <span data-ttu-id="6fe8e-192">Kliknij pozycję **Zapisz**.</span><span class="sxs-lookup"><span data-stu-id="6fe8e-192">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="6fe8e-193">Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz hello [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji hello!</span><span class="sxs-lookup"><span data-stu-id="6fe8e-193">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="6fe8e-194">Po dodaniu tej aplikacji z hello **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij hello **rejestracji jednokrotnej** hello kartę i dostępu do osadzonych dokumentacji za pośrednictwem hello  **Konfiguracja** sekcji u dołu hello.</span><span class="sxs-lookup"><span data-stu-id="6fe8e-194">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="6fe8e-195">Więcej o hello osadzonych dokumentacji funkcji w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="6fe8e-195">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="6fe8e-196">Tworzenie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="6fe8e-196">Creating an Azure AD test user</span></span>
<span data-ttu-id="6fe8e-197">Celem Hello w tej sekcji jest toocreate użytkownika testowego, w portalu Azure o nazwie Simona Britta hello.</span><span class="sxs-lookup"><span data-stu-id="6fe8e-197">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Tworzenie użytkowników usługi Azure AD][100]

<span data-ttu-id="6fe8e-199">**toocreate użytkownika testowego w usłudze Azure AD, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="6fe8e-199">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="6fe8e-200">W hello **portalu Azure**na temat hello w lewym okienku nawigacji, kliknij przycisk **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="6fe8e-200">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-egnyte-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="6fe8e-202">toodisplay hello listę użytkowników, przejdź zbyt**użytkowników i grup** i kliknij przycisk **wszyscy użytkownicy**.</span><span class="sxs-lookup"><span data-stu-id="6fe8e-202">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-egnyte-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="6fe8e-204">Witaj tooopen **użytkownika** okna dialogowego, kliknij przycisk **Dodaj** u góry hello hello okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="6fe8e-204">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-egnyte-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="6fe8e-206">Na powitania **użytkownika** okna dialogowego wykonaj hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="6fe8e-206">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-egnyte-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="6fe8e-208">a.</span><span class="sxs-lookup"><span data-stu-id="6fe8e-208">a.</span></span> <span data-ttu-id="6fe8e-209">W hello **nazwa** pole tekstowe, typ **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="6fe8e-209">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="6fe8e-210">b.</span><span class="sxs-lookup"><span data-stu-id="6fe8e-210">b.</span></span> <span data-ttu-id="6fe8e-211">W hello **nazwy użytkownika** pole tekstowe, hello typu **adres e-mail** z BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="6fe8e-211">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="6fe8e-212">c.</span><span class="sxs-lookup"><span data-stu-id="6fe8e-212">c.</span></span> <span data-ttu-id="6fe8e-213">Wybierz **Pokaż hasło** i zanotuj wartość hello hello **hasło**.</span><span class="sxs-lookup"><span data-stu-id="6fe8e-213">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="6fe8e-214">d.</span><span class="sxs-lookup"><span data-stu-id="6fe8e-214">d.</span></span> <span data-ttu-id="6fe8e-215">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="6fe8e-215">Click **Create**.</span></span>
 
### <a name="creating-an-egnyte-test-user"></a><span data-ttu-id="6fe8e-216">Tworzenie użytkownika testowego Egnyte</span><span class="sxs-lookup"><span data-stu-id="6fe8e-216">Creating an Egnyte test user</span></span>

<span data-ttu-id="6fe8e-217">toolog użytkowników tooenable usługi Azure AD w tooEgnyte, muszą mieć przydzielone do Egnyte.</span><span class="sxs-lookup"><span data-stu-id="6fe8e-217">tooenable Azure AD users toolog in tooEgnyte, they must be provisioned into Egnyte.</span></span> <span data-ttu-id="6fe8e-218">W przypadku hello Egnyte Inicjowanie obsługi to zadanie ręczne.</span><span class="sxs-lookup"><span data-stu-id="6fe8e-218">In hello case of Egnyte, provisioning is a manual task.</span></span>

<span data-ttu-id="6fe8e-219">**tooprovision kont użytkowników, wykonaj hello następujące kroki:**</span><span class="sxs-lookup"><span data-stu-id="6fe8e-219">**tooprovision a user accounts, perform hello following steps:**</span></span>

1. <span data-ttu-id="6fe8e-220">Zaloguj się za tooyour **Egnyte** witryny firmy jako administrator.</span><span class="sxs-lookup"><span data-stu-id="6fe8e-220">Log in tooyour **Egnyte** company site as administrator.</span></span>

2. <span data-ttu-id="6fe8e-221">Przejdź za**ustawienia \> użytkownicy i grupy**.</span><span class="sxs-lookup"><span data-stu-id="6fe8e-221">Go too**Settings \> Users & Groups**.</span></span>

3. <span data-ttu-id="6fe8e-222">Kliknij przycisk **Dodaj nowego użytkownika**, a następnie wybierz typ hello użytkownika ma tooadd.</span><span class="sxs-lookup"><span data-stu-id="6fe8e-222">Click **Add New User**, and then select hello type of user you want tooadd.</span></span>
   
   <span data-ttu-id="6fe8e-223">![Użytkownicy](./media/active-directory-saas-egnyte-tutorial/ic787824.png "użytkowników")</span><span class="sxs-lookup"><span data-stu-id="6fe8e-223">![Users](./media/active-directory-saas-egnyte-tutorial/ic787824.png "Users")</span></span>

4. <span data-ttu-id="6fe8e-224">W hello **nowego użytkownika standardowego** sekcji, wykonaj następujące kroki hello:</span><span class="sxs-lookup"><span data-stu-id="6fe8e-224">In hello **New Standard User** section, perform hello following steps:</span></span>
   
   <span data-ttu-id="6fe8e-225">![Nowy użytkownik standardowy](./media/active-directory-saas-egnyte-tutorial/ic787825.png "nowego użytkownika standardowego")</span><span class="sxs-lookup"><span data-stu-id="6fe8e-225">![New Standard User](./media/active-directory-saas-egnyte-tutorial/ic787825.png "New Standard User")</span></span>   

   <span data-ttu-id="6fe8e-226">a.</span><span class="sxs-lookup"><span data-stu-id="6fe8e-226">a.</span></span> <span data-ttu-id="6fe8e-227">Typ hello **poczty E-mail**, **Username**i inne szczegóły ma tooprovision prawidłowe konto usługi Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="6fe8e-227">Type hello **Email**, **Username**, and other details of a valid Azure Active Directory account you want tooprovision.</span></span>
   
   <span data-ttu-id="6fe8e-228">b.</span><span class="sxs-lookup"><span data-stu-id="6fe8e-228">b.</span></span> <span data-ttu-id="6fe8e-229">Kliknij pozycję **Zapisz**.</span><span class="sxs-lookup"><span data-stu-id="6fe8e-229">Click **Save**.</span></span>
    
    >[!NOTE]
    ><span data-ttu-id="6fe8e-230">Właściciel konta usługi Azure Active Directory Hello otrzymają wiadomość e-mail z powiadomieniem.</span><span class="sxs-lookup"><span data-stu-id="6fe8e-230">hello Azure Active Directory account holder will receive a notification email.</span></span>
    >

>[!NOTE]
><span data-ttu-id="6fe8e-231">Możesz użyć innych Egnyte użytkownika konta tworzenia narzędzi lub interfejsów API dostarczonych przez Egnyte tooprovision kont użytkowników usługi AAD.</span><span class="sxs-lookup"><span data-stu-id="6fe8e-231">You can use any other Egnyte user account creation tools or APIs provided by Egnyte tooprovision AAD user accounts.</span></span>
> 

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="6fe8e-232">Przypisanie użytkownika testowego hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="6fe8e-232">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="6fe8e-233">W tej sekcji możesz włączyć toouse Simona Britta Azure logowania jednokrotnego za udzielanie dostępu tooEgnyte.</span><span class="sxs-lookup"><span data-stu-id="6fe8e-233">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooEgnyte.</span></span>

![Przypisz użytkownika][200] 

<span data-ttu-id="6fe8e-235">**tooassign tooEgnyte Simona Britta wykonaj hello następujące kroki:**</span><span class="sxs-lookup"><span data-stu-id="6fe8e-235">**tooassign Britta Simon tooEgnyte, perform hello following steps:**</span></span>

1. <span data-ttu-id="6fe8e-236">W portalu Azure hello, otwórz widok aplikacji hello, a następnie przejdź do widoku katalogu toohello i przejść za**aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="6fe8e-236">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Przypisz użytkownika][201] 

2. <span data-ttu-id="6fe8e-238">Z listy aplikacji hello wybierz **Egnyte**.</span><span class="sxs-lookup"><span data-stu-id="6fe8e-238">In hello applications list, select **Egnyte**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-egnyte-tutorial/tutorial_egnyte_app.png) 

3. <span data-ttu-id="6fe8e-240">W menu powitania po lewej stronie powitania kliknij **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="6fe8e-240">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Przypisz użytkownika][202] 

4. <span data-ttu-id="6fe8e-242">Kliknij przycisk **Dodaj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="6fe8e-242">Click **Add** button.</span></span> <span data-ttu-id="6fe8e-243">Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="6fe8e-243">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Przypisz użytkownika][203]

5. <span data-ttu-id="6fe8e-245">Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** hello listy użytkowników.</span><span class="sxs-lookup"><span data-stu-id="6fe8e-245">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="6fe8e-246">Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="6fe8e-246">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="6fe8e-247">Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="6fe8e-247">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="6fe8e-248">Testowanie rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="6fe8e-248">Testing single sign-on</span></span>

<span data-ttu-id="6fe8e-249">W tej sekcji można przetestować konfiguracji usługi Azure AD pojedynczego logowania jednokrotnego przy użyciu hello panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="6fe8e-249">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="6fe8e-250">Po kliknięciu kafelka Egnyte hello w hello Panel dostępu, należy pobrać automatycznie zalogowane tooyour Egnyte aplikacji.</span><span class="sxs-lookup"><span data-stu-id="6fe8e-250">When you click hello Egnyte tile in hello Access Panel, you should get automatically signed-on tooyour Egnyte application.</span></span>
<span data-ttu-id="6fe8e-251">Aby uzyskać więcej informacji na temat hello Panel dostępu, zobacz [toohello wprowadzenie panelu dostępu](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="6fe8e-251">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="6fe8e-252">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="6fe8e-252">Additional resources</span></span>

* [<span data-ttu-id="6fe8e-253">Lista samouczków dotyczących tooIntegrate aplikacji SaaS w usłudze Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="6fe8e-253">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="6fe8e-254">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="6fe8e-254">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-egnyte-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-egnyte-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-egnyte-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-egnyte-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-egnyte-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-egnyte-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-egnyte-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-egnyte-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-egnyte-tutorial/tutorial_general_203.png

