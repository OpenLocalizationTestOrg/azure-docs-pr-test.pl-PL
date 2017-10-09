---
title: "Samouczek: Integracji Azure Active Directory z powiększenia | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak tooconfigure logowanie jednokrotne między usługą Azure Active Directory i powiększenia."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 0ebdab6c-83a8-4737-a86a-974f37269c31
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/19/2017
ms.author: jeedes
ms.openlocfilehash: 623a1f428ad1f0aa2c8205b79d61720cad5fc6a5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-zoom"></a><span data-ttu-id="0ec26-103">Samouczek: Integracji Azure Active Directory z powiększenia</span><span class="sxs-lookup"><span data-stu-id="0ec26-103">Tutorial: Azure Active Directory integration with Zoom</span></span>

<span data-ttu-id="0ec26-104">Z tego samouczka, dowiesz się, jak toointegrate powiększenie w usłudze Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="0ec26-104">In this tutorial, you learn how toointegrate Zoom with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="0ec26-105">Integracja z usługą Azure AD powiększenia zapewnia hello następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="0ec26-105">Integrating Zoom with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="0ec26-106">Można kontrolować w usłudze Azure AD, kto ma dostęp do tooZoom.</span><span class="sxs-lookup"><span data-stu-id="0ec26-106">You can control in Azure AD who has access tooZoom.</span></span>
- <span data-ttu-id="0ec26-107">Można włączyć użytkownika użytkownicy tooautomatically get zalogowane tooZoom (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="0ec26-107">You can enable your users tooautomatically get signed-on tooZoom (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="0ec26-108">Możesz zarządzać kont w jednej centralnej lokalizacji - hello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="0ec26-108">You can manage your accounts in one central location - hello Azure portal.</span></span>

<span data-ttu-id="0ec26-109">Jeśli chcesz tooknow więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="0ec26-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="0ec26-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="0ec26-110">Prerequisites</span></span>

<span data-ttu-id="0ec26-111">Integracja tooconfigure usługi Azure AD z powiększenia, należy hello następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="0ec26-111">tooconfigure Azure AD integration with Zoom, you need hello following items:</span></span>

- <span data-ttu-id="0ec26-112">Subskrypcję usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="0ec26-112">An Azure AD subscription</span></span>
- <span data-ttu-id="0ec26-113">Powiększenie logowanie jednokrotne włączone subskrypcji</span><span class="sxs-lookup"><span data-stu-id="0ec26-113">A Zoom single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="0ec26-114">tootest hello kroków w tym samouczku, zaleca się przy użyciu środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="0ec26-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="0ec26-115">tootest hello kroki opisane w tym samouczku, należy stosować te zalecenia:</span><span class="sxs-lookup"><span data-stu-id="0ec26-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="0ec26-116">Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="0ec26-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="0ec26-117">Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz [uzyskać miesięczna wersja próbna](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="0ec26-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="0ec26-118">Opis scenariusza</span><span class="sxs-lookup"><span data-stu-id="0ec26-118">Scenario description</span></span>
<span data-ttu-id="0ec26-119">W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym.</span><span class="sxs-lookup"><span data-stu-id="0ec26-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="0ec26-120">Scenariusz Hello opisane w tym samouczku składa się z dwóch głównych elementów:</span><span class="sxs-lookup"><span data-stu-id="0ec26-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="0ec26-121">Dodawanie powiększenia z galerii hello</span><span class="sxs-lookup"><span data-stu-id="0ec26-121">Adding Zoom from hello gallery</span></span>
2. <span data-ttu-id="0ec26-122">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="0ec26-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-zoom-from-hello-gallery"></a><span data-ttu-id="0ec26-123">Dodawanie powiększenia z galerii hello</span><span class="sxs-lookup"><span data-stu-id="0ec26-123">Adding Zoom from hello gallery</span></span>
<span data-ttu-id="0ec26-124">integracji hello tooconfigure powiększenia do usługi Azure AD, należy tooadd powiększenia z hello galerii tooyour listę zarządzanych aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="0ec26-124">tooconfigure hello integration of Zoom into Azure AD, you need tooadd Zoom from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="0ec26-125">**tooadd powiększenia z galerii hello wykonaj hello następujące kroki:**</span><span class="sxs-lookup"><span data-stu-id="0ec26-125">**tooadd Zoom from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="0ec26-126">W hello  **[portalu Azure](https://portal.azure.com)**na temat hello panelu nawigacji po lewej stronie, kliknij przycisk **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="0ec26-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![przycisk usługi Azure Active Directory Hello][1]

2. <span data-ttu-id="0ec26-128">Przejdź za**aplikacje dla przedsiębiorstw**.</span><span class="sxs-lookup"><span data-stu-id="0ec26-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="0ec26-129">Następnie przejdź zbyt**wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="0ec26-129">Then go too**All applications**.</span></span>

    ![Blok aplikacje przedsiębiorstwa Hello][2]
    
3. <span data-ttu-id="0ec26-131">tooadd nową aplikację, kliknij przycisk **nowej aplikacji** przycisk u góry hello okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="0ec26-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Nowy przycisk aplikacji Hello][3]

4. <span data-ttu-id="0ec26-133">W polu wyszukiwania hello wpisz **powiększenie**, wybierz pozycję **powiększenie** z panelu wyników następnie kliknij przycisk **Dodaj** przycisk aplikacji hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="0ec26-133">In hello search box, type **Zoom**, select **Zoom** from result panel then click **Add** button tooadd hello application.</span></span>

    ![Powiększ hello listy wyników](./media/active-directory-saas-zoom-tutorial/tutorial_zoom_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="0ec26-135">Konfiguracja i testowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="0ec26-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="0ec26-136">W tej sekcji skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z powiększenia w oparciu o nazwie "Britta Simona" użytkownika testowego.</span><span class="sxs-lookup"><span data-stu-id="0ec26-136">In this section, you configure and test Azure AD single sign-on with Zoom based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="0ec26-137">Dla pojedynczego logowania jednokrotnego toowork usługi Azure AD musi tooknow użytkownika odpowiednikiem hello w powiększenia jest tooa użytkownika w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="0ec26-137">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Zoom is tooa user in Azure AD.</span></span> <span data-ttu-id="0ec26-138">Innymi słowy link relację między użytkownika usługi Azure AD i użytkownikowi hello w powiększenia musi toobe ustanowione.</span><span class="sxs-lookup"><span data-stu-id="0ec26-138">In other words, a link relationship between an Azure AD user and hello related user in Zoom needs toobe established.</span></span>

<span data-ttu-id="0ec26-139">Powiększenie, przypisywanie wartości hello hello **nazwy użytkownika** w usłudze Azure AD jako wartość hello hello **Username** tooestablish hello łącze relacji.</span><span class="sxs-lookup"><span data-stu-id="0ec26-139">In Zoom, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="0ec26-140">tooconfigure i testowych usługi Azure AD rejestracji jednokrotnej z powiększenia, należy po bloków konstrukcyjnych hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="0ec26-140">tooconfigure and test Azure AD single sign-on with Zoom, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="0ec26-141">**[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configure-azure-ad-single-sign-on)**  -tooenable Twojego toouse użytkowników tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="0ec26-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="0ec26-142">**[Tworzenie użytkownika testowego usługi Azure AD](#create-an-azure-ad-test-user)**  -tootest usługi Azure AD rejestracji jednokrotnej z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="0ec26-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="0ec26-143">**[Tworzenie użytkownika testowego powiększenia](#create-a-zoom-test-user)**  -toohave odpowiednikiem Simona Britta w powiększenia, który jest połączony toohello usługi Azure AD reprezentację użytkownika.</span><span class="sxs-lookup"><span data-stu-id="0ec26-143">**[Create a Zoom test user](#create-a-zoom-test-user)** - toohave a counterpart of Britta Simon in Zoom that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="0ec26-144">**[Przypisz użytkownika testowego hello Azure AD](#assign-the-azure-ad-test-user)**  -tooenable Simona Britta toouse usługi Azure AD rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="0ec26-144">**[Assign hello Azure AD test user](#assign-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="0ec26-145">**[Test rejestracji jednokrotnej](#test-single-sign-on)**  -tooverify czy hello konfiguracji działania.</span><span class="sxs-lookup"><span data-stu-id="0ec26-145">**[Test single sign-on](#test-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="0ec26-146">Konfigurowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="0ec26-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="0ec26-147">W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w portalu Azure hello i skonfigurować logowanie jednokrotne w aplikacji powiększenia.</span><span class="sxs-lookup"><span data-stu-id="0ec26-147">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Zoom application.</span></span>

<span data-ttu-id="0ec26-148">**tooconfigure usługi Azure AD rejestracji jednokrotnej z powiększenia, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="0ec26-148">**tooconfigure Azure AD single sign-on with Zoom, perform hello following steps:**</span></span>

1. <span data-ttu-id="0ec26-149">W portalu Azure na powitania hello **powiększenie** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.</span><span class="sxs-lookup"><span data-stu-id="0ec26-149">In hello Azure portal, on hello **Zoom** application integration page, click **Single sign-on**.</span></span>

    ![Skonfigurować łącze rejestracji jednokrotnej][4]

2. <span data-ttu-id="0ec26-151">Na powitania **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** tooenable rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="0ec26-151">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Okno dialogowe rejestracji jednokrotnej](./media/active-directory-saas-zoom-tutorial/tutorial_zoom_samlbase.png)

3. <span data-ttu-id="0ec26-153">Na powitania **powiększenie domeny i adres URL** sekcji, wykonaj następujące kroki hello:</span><span class="sxs-lookup"><span data-stu-id="0ec26-153">On hello **Zoom Domain and URLs** section, perform hello following steps:</span></span>

    ![Adresy URL i powiększenia domeny pojedynczy informacje logowania jednokrotnego](./media/active-directory-saas-zoom-tutorial/tutorial_zoom_url.png)

    <span data-ttu-id="0ec26-155">a.</span><span class="sxs-lookup"><span data-stu-id="0ec26-155">a.</span></span> <span data-ttu-id="0ec26-156">W hello **adres URL logowania** tekstowym, wpisz adres URL za pomocą hello następującego wzorca:`https://<companyname>.zoom.us`</span><span class="sxs-lookup"><span data-stu-id="0ec26-156">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<companyname>.zoom.us`</span></span>

    <span data-ttu-id="0ec26-157">b.</span><span class="sxs-lookup"><span data-stu-id="0ec26-157">b.</span></span> <span data-ttu-id="0ec26-158">W hello **identyfikator** tekstowym, wpisz adres URL za pomocą hello następującego wzorca:`https://<companyname>.zoom.us`</span><span class="sxs-lookup"><span data-stu-id="0ec26-158">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<companyname>.zoom.us`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="0ec26-159">Wartości te nie są prawdziwe.</span><span class="sxs-lookup"><span data-stu-id="0ec26-159">These values are not real.</span></span> <span data-ttu-id="0ec26-160">Zaktualizować te wartości z hello rzeczywisty adres URL logowania i identyfikator.</span><span class="sxs-lookup"><span data-stu-id="0ec26-160">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="0ec26-161">Skontaktuj się z [zespołem pomocy technicznej klienta powiększenie](https://support.zoom.us/hc) tooget tych wartości.</span><span class="sxs-lookup"><span data-stu-id="0ec26-161">Contact [Zoom Client support team](https://support.zoom.us/hc) tooget these values.</span></span> 
 
4. <span data-ttu-id="0ec26-162">Na powitania **certyfikat podpisywania SAML** kliknij **certyfikatu (Base64)** , a następnie zapisz plik certyfikatu hello na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="0ec26-162">On hello **SAML Signing Certificate** section, click **Certificate (Base64)** and then save hello certificate file on your computer.</span></span>

    ![link do pobierania certyfikatu Hello](./media/active-directory-saas-zoom-tutorial/tutorial_zoom_certificate.png) 

5. <span data-ttu-id="0ec26-164">Kliknij przycisk **zapisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="0ec26-164">Click **Save** button.</span></span>

    ![Skonfiguruj przycisk pojedynczego logowania jednokrotnego Zapisz](./media/active-directory-saas-zoom-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="0ec26-166">Na powitania **powiększenie konfiguracji** kliknij **skonfigurować powiększenie** tooopen **Konfigurowanie logowania jednokrotnego** okna.</span><span class="sxs-lookup"><span data-stu-id="0ec26-166">On hello **Zoom Configuration** section, click **Configure Zoom** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="0ec26-167">Kopiuj hello **Sign-Out adres URL, identyfikator jednostki SAML i SAML pojedynczy znak na adres URL usługi** z hello **sekcji krótkimi opisami.**</span><span class="sxs-lookup"><span data-stu-id="0ec26-167">Copy hello **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Konfiguracja powiększenia](./media/active-directory-saas-zoom-tutorial/tutorial_zoom_configure.png) 

7. <span data-ttu-id="0ec26-169">W oknie przeglądarki innej witryny sieci web Zaloguj się w witrynie firmy powiększenia tooyour jako administrator.</span><span class="sxs-lookup"><span data-stu-id="0ec26-169">In a different web browser window, log in tooyour Zoom company site as an administrator.</span></span>

8. <span data-ttu-id="0ec26-170">Kliknij przycisk hello **rejestracji jednokrotnej** kartę.</span><span class="sxs-lookup"><span data-stu-id="0ec26-170">Click hello **Single Sign-On** tab.</span></span>
   
    <span data-ttu-id="0ec26-171">![Karta rejestracji jednokrotnej](./media/active-directory-saas-zoom-tutorial/IC784700.png "logowanie jednokrotne")</span><span class="sxs-lookup"><span data-stu-id="0ec26-171">![Single sign-on tab](./media/active-directory-saas-zoom-tutorial/IC784700.png "Single sign-on")</span></span>

9. <span data-ttu-id="0ec26-172">Kliknij przycisk hello **zabezpieczeniem** karcie, a następnie przejdź toohello **rejestracji jednokrotnej** ustawienia.</span><span class="sxs-lookup"><span data-stu-id="0ec26-172">Click hello **Security Control** tab, and then go toohello **Single Sign-On** settings.</span></span>

10. <span data-ttu-id="0ec26-173">W hello sekcji rejestracji jednokrotnej wykonaj hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="0ec26-173">In hello Single Sign-On section, perform hello following steps:</span></span>
   
    <span data-ttu-id="0ec26-174">![Pojedynczy znak w sekcji](./media/active-directory-saas-zoom-tutorial/IC784701.png "logowanie jednokrotne")</span><span class="sxs-lookup"><span data-stu-id="0ec26-174">![Single sign-on section](./media/active-directory-saas-zoom-tutorial/IC784701.png "Single sign-on")</span></span>
   
    <span data-ttu-id="0ec26-175">a.</span><span class="sxs-lookup"><span data-stu-id="0ec26-175">a.</span></span> <span data-ttu-id="0ec26-176">W hello **adres URL logowania strony** pole tekstowe, Wklej wartość hello **SAML pojedynczy znak na adres URL usługi**, które zostały skopiowane z portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="0ec26-176">In hello **Sign-in page URL** textbox, paste hello value of **SAML Single Sign-On Service URL**, which you have copied from Azure portal.</span></span>
   
    <span data-ttu-id="0ec26-177">b.</span><span class="sxs-lookup"><span data-stu-id="0ec26-177">b.</span></span> <span data-ttu-id="0ec26-178">W hello **adres URL strony wylogowania** pole tekstowe, Wklej wartość hello **Sign-Out URL**, które zostały skopiowane z portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="0ec26-178">In hello **Sign-out page URL** textbox, paste hello value of **Sign-Out URL**, which you have copied from Azure portal.</span></span>
     
    <span data-ttu-id="0ec26-179">c.</span><span class="sxs-lookup"><span data-stu-id="0ec26-179">c.</span></span> <span data-ttu-id="0ec26-180">Otwieranie certyfikatu zakodowanego base-64 w Notatniku hello kopiowania zawartości go do Schowka, a następnie wklej go toohello **certyfikat dostawcy tożsamości** pola tekstowego.</span><span class="sxs-lookup"><span data-stu-id="0ec26-180">Open your base-64 encoded certificate in notepad, copy hello content of it into your clipboard, and then paste it toohello **Identity provider certificate** textbox.</span></span>

    <span data-ttu-id="0ec26-181">d.</span><span class="sxs-lookup"><span data-stu-id="0ec26-181">d.</span></span> <span data-ttu-id="0ec26-182">W hello **wystawcy** pole tekstowe, Wklej wartość hello **identyfikator jednostki SAML**, które zostały skopiowane z portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="0ec26-182">In hello **Issuer** textbox, paste hello value of **SAML Entity ID**, which you have copied from Azure portal.</span></span> 

    <span data-ttu-id="0ec26-183">e.</span><span class="sxs-lookup"><span data-stu-id="0ec26-183">e.</span></span> <span data-ttu-id="0ec26-184">Kliknij pozycję **Zapisz**.</span><span class="sxs-lookup"><span data-stu-id="0ec26-184">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="0ec26-185">Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz hello [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji hello!</span><span class="sxs-lookup"><span data-stu-id="0ec26-185">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="0ec26-186">Po dodaniu tej aplikacji z hello **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij hello **rejestracji jednokrotnej** hello kartę i dostępu do osadzonych dokumentacji za pośrednictwem hello  **Konfiguracja** sekcji u dołu hello.</span><span class="sxs-lookup"><span data-stu-id="0ec26-186">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="0ec26-187">Więcej o hello osadzonych dokumentacji funkcji w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="0ec26-187">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="0ec26-188">Tworzenie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="0ec26-188">Create an Azure AD test user</span></span>

<span data-ttu-id="0ec26-189">Celem Hello w tej sekcji jest toocreate użytkownika testowego, w portalu Azure o nazwie Simona Britta hello.</span><span class="sxs-lookup"><span data-stu-id="0ec26-189">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

   ![Tworzenie użytkownika testowego usługi Azure AD][100]

<span data-ttu-id="0ec26-191">**toocreate użytkownika testowego w usłudze Azure AD, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="0ec26-191">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="0ec26-192">W portalu Azure, w okienku po lewej stronie powitania hello kliknij hello **usługi Azure Active Directory** przycisku.</span><span class="sxs-lookup"><span data-stu-id="0ec26-192">In hello Azure portal, in hello left pane, click hello **Azure Active Directory** button.</span></span>

    ![przycisk usługi Azure Active Directory Hello](./media/active-directory-saas-zoom-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="0ec26-194">toodisplay hello listę użytkowników, przejdź zbyt**użytkowników i grup**, a następnie kliknij przycisk **wszyscy użytkownicy**.</span><span class="sxs-lookup"><span data-stu-id="0ec26-194">toodisplay hello list of users, go too**Users and groups**, and then click **All users**.</span></span>

    ![Witaj, "Użytkownicy i grupy" i "Wszyscy użytkownicy" łącza](./media/active-directory-saas-zoom-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="0ec26-196">Witaj tooopen **użytkownika** okno dialogowe, kliknij przycisk **Dodaj** u góry hello hello **wszyscy użytkownicy** okno dialogowe.</span><span class="sxs-lookup"><span data-stu-id="0ec26-196">tooopen hello **User** dialog box, click **Add** at hello top of hello **All Users** dialog box.</span></span>

    ![przycisk Dodaj Hello](./media/active-directory-saas-zoom-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="0ec26-198">W hello **użytkownika** okna dialogowego wykonaj hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="0ec26-198">In hello **User** dialog box, perform hello following steps:</span></span>

    ![okno dialogowe Hello użytkownika](./media/active-directory-saas-zoom-tutorial/create_aaduser_04.png)

    <span data-ttu-id="0ec26-200">a.</span><span class="sxs-lookup"><span data-stu-id="0ec26-200">a.</span></span> <span data-ttu-id="0ec26-201">W hello **nazwa** wpisz **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="0ec26-201">In hello **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="0ec26-202">b.</span><span class="sxs-lookup"><span data-stu-id="0ec26-202">b.</span></span> <span data-ttu-id="0ec26-203">W hello **nazwy użytkownika** pole typu hello adres e-mail użytkownika Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="0ec26-203">In hello **User name** box, type hello email address of user Britta Simon.</span></span>

    <span data-ttu-id="0ec26-204">c.</span><span class="sxs-lookup"><span data-stu-id="0ec26-204">c.</span></span> <span data-ttu-id="0ec26-205">Wybierz hello **Pokaż hasło** pole wyboru, a następnie zapisz hello wartość, która jest wyświetlana w hello **hasło** pole.</span><span class="sxs-lookup"><span data-stu-id="0ec26-205">Select hello **Show Password** check box, and then write down hello value that's displayed in hello **Password** box.</span></span>

    <span data-ttu-id="0ec26-206">d.</span><span class="sxs-lookup"><span data-stu-id="0ec26-206">d.</span></span> <span data-ttu-id="0ec26-207">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="0ec26-207">Click **Create**.</span></span>
 
### <a name="create-a-zoom-test-user"></a><span data-ttu-id="0ec26-208">Tworzenie użytkownika testowego powiększenia</span><span class="sxs-lookup"><span data-stu-id="0ec26-208">Create a Zoom test user</span></span>

<span data-ttu-id="0ec26-209">W kolejności toolog użytkowników tooenable usługi Azure AD w tooZoom musi być przygotowana do powiększenia.</span><span class="sxs-lookup"><span data-stu-id="0ec26-209">In order tooenable Azure AD users toolog in tooZoom, they must be provisioned into Zoom.</span></span> <span data-ttu-id="0ec26-210">W przypadku hello powiększenia Inicjowanie obsługi to zadanie ręczne.</span><span class="sxs-lookup"><span data-stu-id="0ec26-210">In hello case of Zoom, provisioning is a manual task.</span></span>

### <a name="tooprovision-a-user-account-perform-hello-following-steps"></a><span data-ttu-id="0ec26-211">tooprovision konta użytkownika, należy wykonać hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="0ec26-211">tooprovision a user account, perform hello following steps:</span></span>

1. <span data-ttu-id="0ec26-212">Zaloguj się za tooyour **powiększenie** witryny firmy jako administrator.</span><span class="sxs-lookup"><span data-stu-id="0ec26-212">Log in tooyour **Zoom** company site as an administrator.</span></span>
 
2. <span data-ttu-id="0ec26-213">Kliknij przycisk hello **zarządzania kontami** , a następnie kliknij pozycję **Zarządzanie użytkownikami**.</span><span class="sxs-lookup"><span data-stu-id="0ec26-213">Click hello **Account Management** tab, and then click **User Management**.</span></span>

3. <span data-ttu-id="0ec26-214">W sekcji Zarządzanie użytkownikami hello, kliknij przycisk **dodawania użytkowników**.</span><span class="sxs-lookup"><span data-stu-id="0ec26-214">In hello User Management section, click **Add users**.</span></span>
   
    <span data-ttu-id="0ec26-215">![Zarządzanie użytkownikami](./media/active-directory-saas-zoom-tutorial/IC784703.png "Zarządzanie użytkownikami")</span><span class="sxs-lookup"><span data-stu-id="0ec26-215">![User management](./media/active-directory-saas-zoom-tutorial/IC784703.png "User management")</span></span>

4. <span data-ttu-id="0ec26-216">Na powitania **dodawania użytkowników** wykonaj hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="0ec26-216">On hello **Add users** page, perform hello following steps:</span></span>
   
    <span data-ttu-id="0ec26-217">![Dodawanie użytkowników](./media/active-directory-saas-zoom-tutorial/IC784704.png "Dodawanie użytkowników")</span><span class="sxs-lookup"><span data-stu-id="0ec26-217">![Add users](./media/active-directory-saas-zoom-tutorial/IC784704.png "Add users")</span></span>
   
    <span data-ttu-id="0ec26-218">a.</span><span class="sxs-lookup"><span data-stu-id="0ec26-218">a.</span></span> <span data-ttu-id="0ec26-219">Jako **typ użytkownika**, wybierz pozycję **podstawowe**.</span><span class="sxs-lookup"><span data-stu-id="0ec26-219">As **User Type**, select **Basic**.</span></span>

    <span data-ttu-id="0ec26-220">b.</span><span class="sxs-lookup"><span data-stu-id="0ec26-220">b.</span></span> <span data-ttu-id="0ec26-221">W hello **wiadomości E-mail** pole tekstowe, adres e-mail hello typu prawidłowy Azure AD konta tooprovision.</span><span class="sxs-lookup"><span data-stu-id="0ec26-221">In hello **Emails** textbox, type hello email address of a valid Azure AD account you want tooprovision.</span></span>

    <span data-ttu-id="0ec26-222">c.</span><span class="sxs-lookup"><span data-stu-id="0ec26-222">c.</span></span> <span data-ttu-id="0ec26-223">Kliknij pozycję **Dodaj**.</span><span class="sxs-lookup"><span data-stu-id="0ec26-223">Click **Add**.</span></span>

> [!NOTE]
> <span data-ttu-id="0ec26-224">Możesz użyć innych powiększenia użytkownika konta tworzenia narzędzi lub interfejsów API dostarczonych przez tooprovision powiększenia usługi Azure Active Directory kont użytkowników.</span><span class="sxs-lookup"><span data-stu-id="0ec26-224">You can use any other Zoom user account creation tools or APIs provided by Zoom tooprovision Azure Active Directory user accounts.</span></span>

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="0ec26-225">Przypisz użytkownika testowego hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="0ec26-225">Assign hello Azure AD test user</span></span>

<span data-ttu-id="0ec26-226">W tej sekcji możesz włączyć toouse Simona Britta Azure logowania jednokrotnego za udzielanie dostępu tooZoom.</span><span class="sxs-lookup"><span data-stu-id="0ec26-226">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooZoom.</span></span>

![Przypisanie roli użytkownika hello][200] 

<span data-ttu-id="0ec26-228">**tooassign tooZoom Simona Britta wykonaj hello następujące kroki:**</span><span class="sxs-lookup"><span data-stu-id="0ec26-228">**tooassign Britta Simon tooZoom, perform hello following steps:**</span></span>

1. <span data-ttu-id="0ec26-229">W portalu Azure hello, otwórz widok aplikacji hello, a następnie przejdź do widoku katalogu toohello i przejść za**aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="0ec26-229">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Przypisz użytkownika][201] 

2. <span data-ttu-id="0ec26-231">Z listy aplikacji hello wybierz **powiększenie**.</span><span class="sxs-lookup"><span data-stu-id="0ec26-231">In hello applications list, select **Zoom**.</span></span>

    ![łącze powiększenia Hello na liście aplikacji hello](./media/active-directory-saas-zoom-tutorial/tutorial_zoom_app.png)  

3. <span data-ttu-id="0ec26-233">W menu powitania po lewej stronie powitania kliknij **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="0ec26-233">In hello menu on hello left, click **Users and groups**.</span></span>

    ![łącze "Użytkownicy i grupy" Hello][202]

4. <span data-ttu-id="0ec26-235">Kliknij przycisk **Dodaj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="0ec26-235">Click **Add** button.</span></span> <span data-ttu-id="0ec26-236">Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="0ec26-236">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Okienko Dodaj przypisania Hello][203]

5. <span data-ttu-id="0ec26-238">Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** hello listy użytkowników.</span><span class="sxs-lookup"><span data-stu-id="0ec26-238">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="0ec26-239">Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="0ec26-239">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="0ec26-240">Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="0ec26-240">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="0ec26-241">Test rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="0ec26-241">Test single sign-on</span></span>

<span data-ttu-id="0ec26-242">Celem Hello w tej sekcji jest tootest użyciu usługi Azure AD konfiguracji rejestracji jednokrotnej hello panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="0ec26-242">hello objective of this section is tootest your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="0ec26-243">Po kliknięciu kafelka powiększenia hello w hello Panel dostępu, należy pobrać automatycznie zalogowane tooyour powiększenia aplikacji.</span><span class="sxs-lookup"><span data-stu-id="0ec26-243">When you click hello Zoom tile in hello Access Panel, you should get automatically signed-on tooyour Zoom application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="0ec26-244">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="0ec26-244">Additional resources</span></span>

* [<span data-ttu-id="0ec26-245">Lista samouczków dotyczących tooIntegrate aplikacji SaaS w usłudze Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="0ec26-245">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="0ec26-246">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="0ec26-246">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-zoom-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-zoom-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-zoom-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-zoom-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-zoom-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-zoom-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-zoom-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-zoom-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-zoom-tutorial/tutorial_general_203.png

