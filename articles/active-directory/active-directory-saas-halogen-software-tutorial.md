---
title: "Samouczek: Azure Active Directory integracji z oprogramowaniem chlorowców | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak tooconfigure logowanie jednokrotne między oprogramowaniem halogenowe i Azure Active Directory."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 2ca2298d-9a0c-4f14-925c-fa23f2659d28
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/23/2017
ms.author: jeedes
ms.openlocfilehash: bdb67de713771d6e306f287c4b13895f6336f7ba
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-halogen-software"></a><span data-ttu-id="1a56f-103">Samouczek: Azure Active Directory integracji z oprogramowaniem chlorowców</span><span class="sxs-lookup"><span data-stu-id="1a56f-103">Tutorial: Azure Active Directory integration with Halogen Software</span></span>

<span data-ttu-id="1a56f-104">Z tego samouczka, dowiesz się, jak toointegrate chlorowców oprogramowania w usłudze Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="1a56f-104">In this tutorial, you learn how toointegrate Halogen Software with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="1a56f-105">Integrowanie chlorowców oprogramowania z usługi Azure AD zapewnia hello następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="1a56f-105">Integrating Halogen Software with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="1a56f-106">Można kontrolować w usłudze Azure AD, kto ma dostęp do tooHalogen oprogramowania</span><span class="sxs-lookup"><span data-stu-id="1a56f-106">You can control in Azure AD who has access tooHalogen Software</span></span>
- <span data-ttu-id="1a56f-107">Można włączyć użytkownika użytkownicy tooautomatically get zalogowane tooHalogen oprogramowania (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="1a56f-107">You can enable your users tooautomatically get signed-on tooHalogen Software (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="1a56f-108">Możesz zarządzać kont w jednej centralnej lokalizacji - hello portalu Azure</span><span class="sxs-lookup"><span data-stu-id="1a56f-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="1a56f-109">Jeśli chcesz tooknow więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="1a56f-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="1a56f-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="1a56f-110">Prerequisites</span></span>

<span data-ttu-id="1a56f-111">tooconfigure integracji usługi Azure AD z oprogramowaniem chlorowców należy hello następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="1a56f-111">tooconfigure Azure AD integration with Halogen Software, you need hello following items:</span></span>

- <span data-ttu-id="1a56f-112">Subskrypcję usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="1a56f-112">An Azure AD subscription</span></span>
- <span data-ttu-id="1a56f-113">Oprogramowanie chlorowców logowanie jednokrotne włączone subskrypcji</span><span class="sxs-lookup"><span data-stu-id="1a56f-113">A Halogen Software single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="1a56f-114">tootest hello kroków w tym samouczku, zaleca się przy użyciu środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="1a56f-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="1a56f-115">tootest hello kroki opisane w tym samouczku, należy stosować te zalecenia:</span><span class="sxs-lookup"><span data-stu-id="1a56f-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="1a56f-116">Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="1a56f-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="1a56f-117">Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz pobrać miesięczna wersja próbna [tutaj](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="1a56f-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="1a56f-118">Opis scenariusza</span><span class="sxs-lookup"><span data-stu-id="1a56f-118">Scenario description</span></span>

<span data-ttu-id="1a56f-119">W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym.</span><span class="sxs-lookup"><span data-stu-id="1a56f-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="1a56f-120">Scenariusz Hello opisane w tym samouczku składa się z dwóch głównych elementów:</span><span class="sxs-lookup"><span data-stu-id="1a56f-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="1a56f-121">Dodawanie oprogramowania chlorowców z galerii hello</span><span class="sxs-lookup"><span data-stu-id="1a56f-121">Adding Halogen Software from hello gallery</span></span>
2. <span data-ttu-id="1a56f-122">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="1a56f-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-halogen-software-from-hello-gallery"></a><span data-ttu-id="1a56f-123">Dodawanie oprogramowania chlorowców z galerii hello</span><span class="sxs-lookup"><span data-stu-id="1a56f-123">Adding Halogen Software from hello gallery</span></span>

<span data-ttu-id="1a56f-124">tooconfigure hello integracji chlorowców oprogramowania do usługi Azure AD, należy tooadd chlorowców oprogramowania z listy tooyour galerii hello zarządzanych aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="1a56f-124">tooconfigure hello integration of Halogen Software into Azure AD, you need tooadd Halogen Software from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="1a56f-125">**tooadd chlorowców oprogramowania z galerii hello wykonaj hello następujące kroki:**</span><span class="sxs-lookup"><span data-stu-id="1a56f-125">**tooadd Halogen Software from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="1a56f-126">W hello  **[portalu Azure](https://portal.azure.com)**na temat hello panelu nawigacji po lewej stronie, kliknij przycisk **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="1a56f-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Usługa Active Directory][1]

2. <span data-ttu-id="1a56f-128">Przejdź za**aplikacje dla przedsiębiorstw**.</span><span class="sxs-lookup"><span data-stu-id="1a56f-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="1a56f-129">Następnie przejdź zbyt**wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="1a56f-129">Then go too**All applications**.</span></span>

    ![Aplikacje][2]
    
3. <span data-ttu-id="1a56f-131">tooadd nową aplikację, kliknij przycisk **nowej aplikacji** przycisk u góry hello okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="1a56f-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplikacje][3]

4. <span data-ttu-id="1a56f-133">W polu wyszukiwania hello wpisz **oprogramowania chlorowców**.</span><span class="sxs-lookup"><span data-stu-id="1a56f-133">In hello search box, type **Halogen Software**.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-halogen-software-tutorial/tutorial_halogensoftware_search.png)

5. <span data-ttu-id="1a56f-135">W panelu wyników hello, wybierz **oprogramowania chlorowców**, a następnie kliknij przycisk **Dodaj** przycisk aplikacji hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="1a56f-135">In hello results panel, select **Halogen Software**, and then click **Add** button tooadd hello application.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-halogen-software-tutorial/tutorial_halogensoftware_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="1a56f-137">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="1a56f-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="1a56f-138">W tej sekcji skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z oprogramowaniem chlorowców w oparciu o nazwie "Britta Simona" użytkownika testowego.</span><span class="sxs-lookup"><span data-stu-id="1a56f-138">In this section, you configure and test Azure AD single sign-on with Halogen Software based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="1a56f-139">Dla pojedynczego logowania jednokrotnego toowork usługi Azure AD musi tooknow użytkownika odpowiednikiem hello w oprogramowaniu halogenowe jest tooa użytkownika w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="1a56f-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Halogen Software is tooa user in Azure AD.</span></span> <span data-ttu-id="1a56f-140">Innymi słowy relację łącza między użytkownika usługi Azure AD i hello użytkownikowi w oprogramowaniu chlorowców musi toobe ustanowione.</span><span class="sxs-lookup"><span data-stu-id="1a56f-140">In other words, a link relationship between an Azure AD user and hello related user in Halogen Software needs toobe established.</span></span>

<span data-ttu-id="1a56f-141">W oprogramowaniu chlorowców przypisać wartość hello hello **nazwy użytkownika** w usłudze Azure AD jako wartość hello hello **Username** tooestablish hello łącze relacji.</span><span class="sxs-lookup"><span data-stu-id="1a56f-141">In Halogen Software, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="1a56f-142">tooconfigure i testowych usługi Azure AD rejestracji jednokrotnej z oprogramowaniem halogenowe, należy po bloków konstrukcyjnych hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="1a56f-142">tooconfigure and test Azure AD single sign-on with Halogen Software, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="1a56f-143">**[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configuring-azure-ad-single-sign-on)**  -tooenable Twojego toouse użytkowników tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="1a56f-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="1a56f-144">**[Tworzenie użytkownika testowego usługi Azure AD](#creating-an-azure-ad-test-user)**  -tootest usługi Azure AD rejestracji jednokrotnej z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="1a56f-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="1a56f-145">**[Tworzenie użytkownika testowego oprogramowania chlorowców](#creating-a-halogen-software-test-user)**  -toohave odpowiednikiem Simona Britta chlorowców oprogramowania, który jest połączony toohello usługi Azure AD reprezentację użytkownika.</span><span class="sxs-lookup"><span data-stu-id="1a56f-145">**[Creating a Halogen Software test user](#creating-a-halogen-software-test-user)** - toohave a counterpart of Britta Simon in Halogen Software that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="1a56f-146">**[Przypisanie użytkownika testowego hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Simona Britta toouse usługi Azure AD rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="1a56f-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="1a56f-147">**[Testowanie rejestracji jednokrotnej](#testing-single-sign-on)**  -tooverify czy hello konfiguracji działania.</span><span class="sxs-lookup"><span data-stu-id="1a56f-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="1a56f-148">Konfigurowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="1a56f-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="1a56f-149">W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w hello portalu Azure i skonfigurować rejestracji jednokrotnej w używanej aplikacji halogenowe.</span><span class="sxs-lookup"><span data-stu-id="1a56f-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Halogen Software application.</span></span>

<span data-ttu-id="1a56f-150">**tooconfigure usługi Azure AD rejestracji jednokrotnej z oprogramowaniem chlorowców wykonaj hello następujące kroki:**</span><span class="sxs-lookup"><span data-stu-id="1a56f-150">**tooconfigure Azure AD single sign-on with Halogen Software, perform hello following steps:**</span></span>

1. <span data-ttu-id="1a56f-151">W portalu Azure na powitania hello **oprogramowania chlorowców** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.</span><span class="sxs-lookup"><span data-stu-id="1a56f-151">In hello Azure portal, on hello **Halogen Software** application integration page, click **Single sign-on**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej][4]

2. <span data-ttu-id="1a56f-153">Na powitania **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** tooenable rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="1a56f-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-halogen-software-tutorial/tutorial_halogensoftware_samlbase.png)

3. <span data-ttu-id="1a56f-155">Na powitania **chlorowców oprogramowania domeny i adres URL** sekcji, wykonaj następujące kroki hello:</span><span class="sxs-lookup"><span data-stu-id="1a56f-155">On hello **Halogen Software Domain and URLs** section, perform hello following steps:</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-halogen-software-tutorial/tutorial_halogensoftware_url.png)

    <span data-ttu-id="1a56f-157">a.</span><span class="sxs-lookup"><span data-stu-id="1a56f-157">a.</span></span> <span data-ttu-id="1a56f-158">W hello **adres URL logowania** tekstowym, wpisz adres URL za pomocą hello następującego wzorca:`https://global.hgncloud.com/<companyname>`</span><span class="sxs-lookup"><span data-stu-id="1a56f-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://global.hgncloud.com/<companyname>`</span></span>

    <span data-ttu-id="1a56f-159">b.</span><span class="sxs-lookup"><span data-stu-id="1a56f-159">b.</span></span> <span data-ttu-id="1a56f-160">W hello **identyfikator** tekstowym, wpisz adres URL za pomocą hello następującego wzorca: `https://global.halogensoftware.com/<companyname>`,`https://global.hgncloud.com/<companyname>`</span><span class="sxs-lookup"><span data-stu-id="1a56f-160">In hello **Identifier** textbox, type a URL using hello following pattern: `https://global.halogensoftware.com/<companyname>`, `https://global.hgncloud.com/<companyname>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="1a56f-161">Wartości te nie są prawdziwe.</span><span class="sxs-lookup"><span data-stu-id="1a56f-161">These values are not real.</span></span> <span data-ttu-id="1a56f-162">Zaktualizować te wartości z hello rzeczywisty adres URL logowania i identyfikator.</span><span class="sxs-lookup"><span data-stu-id="1a56f-162">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="1a56f-163">Skontaktuj się z [zespołem pomocy technicznej klienta oprogramowania chlorowców](https://support.halogensoftware.com/) tooget tych wartości.</span><span class="sxs-lookup"><span data-stu-id="1a56f-163">Contact [Halogen Software Client support team](https://support.halogensoftware.com/) tooget these values.</span></span> 
 


4. <span data-ttu-id="1a56f-164">Na powitania **certyfikat podpisywania SAML** kliknij **XML metadanych** , a następnie zapisz plik metadanych hello na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="1a56f-164">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-halogen-software-tutorial/tutorial_halogensoftware_certificate.png) 

5. <span data-ttu-id="1a56f-166">Kliknij przycisk **zapisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="1a56f-166">Click **Save** button.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-halogen-software-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="1a56f-168">W oknie innej przeglądarki, logowania jednokrotnego tooyour **oprogramowania chlorowców** aplikacji jako administrator.</span><span class="sxs-lookup"><span data-stu-id="1a56f-168">In a different browser window, sign-on tooyour **Halogen Software** application as an administrator.</span></span>

7. <span data-ttu-id="1a56f-169">Kliknij przycisk hello **opcje** kartę.</span><span class="sxs-lookup"><span data-stu-id="1a56f-169">Click hello **Options** tab.</span></span> 
   
    ![Co to jest program Azure AD Connect][12]

8. <span data-ttu-id="1a56f-171">W okienku nawigacji po lewej stronie powitania kliknij **Konfiguracja SAML**.</span><span class="sxs-lookup"><span data-stu-id="1a56f-171">In hello left navigation pane, click **SAML Configuration**.</span></span> 
   
    ![Co to jest program Azure AD Connect][13]

9. <span data-ttu-id="1a56f-173">Na powitania **Konfiguracja SAML** wykonaj hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="1a56f-173">On hello **SAML Configuration** page, perform hello following steps:</span></span> 

    ![Co to jest program Azure AD Connect][14]

     <span data-ttu-id="1a56f-175">a.</span><span class="sxs-lookup"><span data-stu-id="1a56f-175">a.</span></span> <span data-ttu-id="1a56f-176">Jako **Unikatowy identyfikator**, wybierz pozycję **NameID**.</span><span class="sxs-lookup"><span data-stu-id="1a56f-176">As **Unique Identifier**, select **NameID**.</span></span>

     <span data-ttu-id="1a56f-177">b.</span><span class="sxs-lookup"><span data-stu-id="1a56f-177">b.</span></span> <span data-ttu-id="1a56f-178">Jako **mapy Unikatowy identyfikator do**, wybierz pozycję **Username**.</span><span class="sxs-lookup"><span data-stu-id="1a56f-178">As **Unique Identifier Maps To**, select **Username**.</span></span>
  
     <span data-ttu-id="1a56f-179">c.</span><span class="sxs-lookup"><span data-stu-id="1a56f-179">c.</span></span> <span data-ttu-id="1a56f-180">tooupload pliku metadanych pobranych, kliknij przycisk **Przeglądaj** tooselect hello pliku, a następnie **Przekaż plik**.</span><span class="sxs-lookup"><span data-stu-id="1a56f-180">tooupload your downloaded metadata file, click **Browse** tooselect hello file, and then **Upload File**.</span></span>
 
     <span data-ttu-id="1a56f-181">d.</span><span class="sxs-lookup"><span data-stu-id="1a56f-181">d.</span></span> <span data-ttu-id="1a56f-182">Konfiguracja hello tootest, kliknij przycisk **Uruchom Test**.</span><span class="sxs-lookup"><span data-stu-id="1a56f-182">tootest hello configuration, click **Run Test**.</span></span> 
    
    >[!NOTE]
    ><span data-ttu-id="1a56f-183">Należy toowait wiadomość hello "*hello SAML testu została ukończona. Zamknij to okno*".</span><span class="sxs-lookup"><span data-stu-id="1a56f-183">You need toowait for hello message "*hello SAML test is complete. Please close this window*".</span></span> <span data-ttu-id="1a56f-184">Zamknij hello otwartego okna przeglądarki.</span><span class="sxs-lookup"><span data-stu-id="1a56f-184">Then, close hello opened browser window.</span></span> <span data-ttu-id="1a56f-185">Witaj **Włącz SAML** pole wyboru jest włączone, tylko jeśli hello test została ukończona.</span><span class="sxs-lookup"><span data-stu-id="1a56f-185">hello **Enable SAML** checkbox is only enabled if hello test has been completed.</span></span> 
     
     <span data-ttu-id="1a56f-186">e.</span><span class="sxs-lookup"><span data-stu-id="1a56f-186">e.</span></span> <span data-ttu-id="1a56f-187">Wybierz **Włącz SAML**.</span><span class="sxs-lookup"><span data-stu-id="1a56f-187">Select **Enable SAML**.</span></span>
    
     <span data-ttu-id="1a56f-188">f.</span><span class="sxs-lookup"><span data-stu-id="1a56f-188">f.</span></span> <span data-ttu-id="1a56f-189">Kliknij przycisk **zapisać zmiany**.</span><span class="sxs-lookup"><span data-stu-id="1a56f-189">Click **Save Changes**.</span></span> 

> [!TIP]
> <span data-ttu-id="1a56f-190">Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz hello [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji hello!</span><span class="sxs-lookup"><span data-stu-id="1a56f-190">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="1a56f-191">Po dodaniu tej aplikacji z hello **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij hello **rejestracji jednokrotnej** hello kartę i dostępu do osadzonych dokumentacji za pośrednictwem hello  **Konfiguracja** sekcji u dołu hello.</span><span class="sxs-lookup"><span data-stu-id="1a56f-191">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="1a56f-192">Więcej o hello osadzonych dokumentacji funkcji w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="1a56f-192">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>


### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="1a56f-193">Tworzenie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="1a56f-193">Creating an Azure AD test user</span></span>

<span data-ttu-id="1a56f-194">Celem Hello w tej sekcji jest toocreate użytkownika testowego, w portalu Azure o nazwie Simona Britta hello.</span><span class="sxs-lookup"><span data-stu-id="1a56f-194">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Tworzenie użytkowników usługi Azure AD][100]

<span data-ttu-id="1a56f-196">**toocreate użytkownika testowego w usłudze Azure AD, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="1a56f-196">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="1a56f-197">W hello **portalu Azure**na temat hello w lewym okienku nawigacji, kliknij przycisk **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="1a56f-197">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-halogen-software-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="1a56f-199">toodisplay hello listę użytkowników, przejdź zbyt**użytkowników i grup** i kliknij przycisk **wszyscy użytkownicy**.</span><span class="sxs-lookup"><span data-stu-id="1a56f-199">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-halogen-software-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="1a56f-201">Witaj tooopen **użytkownika** okna dialogowego, kliknij przycisk **Dodaj** u góry hello hello okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="1a56f-201">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-halogen-software-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="1a56f-203">Na powitania **użytkownika** okna dialogowego wykonaj hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="1a56f-203">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-halogen-software-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="1a56f-205">a.</span><span class="sxs-lookup"><span data-stu-id="1a56f-205">a.</span></span> <span data-ttu-id="1a56f-206">W hello **nazwa** pole tekstowe, nazwa typu jako **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="1a56f-206">In hello **Name** textbox, type name as **BrittaSimon**.</span></span>

    <span data-ttu-id="1a56f-207">b.</span><span class="sxs-lookup"><span data-stu-id="1a56f-207">b.</span></span> <span data-ttu-id="1a56f-208">W hello **nazwy użytkownika** pole tekstowe, hello typu **adres e-mail** z BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="1a56f-208">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="1a56f-209">c.</span><span class="sxs-lookup"><span data-stu-id="1a56f-209">c.</span></span> <span data-ttu-id="1a56f-210">Wybierz **Pokaż hasło** i zanotuj wartość hello hello **hasło**.</span><span class="sxs-lookup"><span data-stu-id="1a56f-210">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="1a56f-211">d.</span><span class="sxs-lookup"><span data-stu-id="1a56f-211">d.</span></span> <span data-ttu-id="1a56f-212">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="1a56f-212">Click **Create**.</span></span>
 
### <a name="creating-a-halogen-software-test-user"></a><span data-ttu-id="1a56f-213">Tworzenie użytkownika testowego chlorowców oprogramowania</span><span class="sxs-lookup"><span data-stu-id="1a56f-213">Creating a Halogen Software test user</span></span>

<span data-ttu-id="1a56f-214">Celem Hello w tej sekcji jest toocreate użytkownika o nazwie Simona Britta chlorowców oprogramowania.</span><span class="sxs-lookup"><span data-stu-id="1a56f-214">hello objective of this section is toocreate a user called Britta Simon in Halogen Software.</span></span>

<span data-ttu-id="1a56f-215">**toocreate użytkownika o nazwie Simona Britta chlorowców oprogramowania, wykonaj hello następujące kroki:**</span><span class="sxs-lookup"><span data-stu-id="1a56f-215">**toocreate a user called Britta Simon in Halogen Software, perform hello following steps:**</span></span>

1. <span data-ttu-id="1a56f-216">Zaloguj się na tooyour **oprogramowania chlorowców** aplikacji jako administrator.</span><span class="sxs-lookup"><span data-stu-id="1a56f-216">Sign on tooyour **Halogen Software** application as an administrator.</span></span>

2. <span data-ttu-id="1a56f-217">Kliknij przycisk hello **użytkownika Centrum** , a następnie kliknij pozycję **Tworzenie użytkownika**.</span><span class="sxs-lookup"><span data-stu-id="1a56f-217">Click hello **User Center** tab, and then click **Create User**.</span></span>
   
    ![Co to jest program Azure AD Connect][300]  

3. <span data-ttu-id="1a56f-219">Na powitania **nowego użytkownika** okna dialogowego wykonaj hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="1a56f-219">On hello **New User** dialog page, perform hello following steps:</span></span>
   
    ![Co to jest program Azure AD Connect][301]

    <span data-ttu-id="1a56f-221">a.</span><span class="sxs-lookup"><span data-stu-id="1a56f-221">a.</span></span> <span data-ttu-id="1a56f-222">W hello **imię** pole tekstowe, typ imię użytkownika hello, takich jak **Britta**.</span><span class="sxs-lookup"><span data-stu-id="1a56f-222">In hello **First Name** textbox, type first name of hello user like **Britta**.</span></span>
    
    <span data-ttu-id="1a56f-223">b.</span><span class="sxs-lookup"><span data-stu-id="1a56f-223">b.</span></span> <span data-ttu-id="1a56f-224">W hello **nazwisko** pole tekstowe, typ nazwisko użytkownika hello, takich jak **Simona**.</span><span class="sxs-lookup"><span data-stu-id="1a56f-224">In hello **Last Name** textbox, type last name of hello user like **Simon**.</span></span> 

    <span data-ttu-id="1a56f-225">c.</span><span class="sxs-lookup"><span data-stu-id="1a56f-225">c.</span></span> <span data-ttu-id="1a56f-226">W hello **Username** pole tekstowe, typ **Simona Britta**, hello nazwy użytkownika podanej hello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="1a56f-226">In hello **Username** textbox, type **Britta Simon**, hello user name as in hello Azure portal.</span></span>

    <span data-ttu-id="1a56f-227">d.</span><span class="sxs-lookup"><span data-stu-id="1a56f-227">d.</span></span> <span data-ttu-id="1a56f-228">W hello **hasło** tekstowym, wpisz hasło dla Britta.</span><span class="sxs-lookup"><span data-stu-id="1a56f-228">In hello **Password** textbox, type a password for Britta.</span></span>
    
    <span data-ttu-id="1a56f-229">e.</span><span class="sxs-lookup"><span data-stu-id="1a56f-229">e.</span></span> <span data-ttu-id="1a56f-230">Kliknij pozycję **Zapisz**.</span><span class="sxs-lookup"><span data-stu-id="1a56f-230">Click **Save**.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="1a56f-231">Przypisanie użytkownika testowego hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="1a56f-231">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="1a56f-232">W tej sekcji możesz włączyć toouse Simona Britta Azure logowania jednokrotnego za udzielanie dostępu tooHalogen oprogramowania.</span><span class="sxs-lookup"><span data-stu-id="1a56f-232">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooHalogen Software.</span></span>

![Przypisz użytkownika][200] 

<span data-ttu-id="1a56f-234">**tooassign tooHalogen Simona Britta oprogramowania, wykonaj hello następujące kroki:**</span><span class="sxs-lookup"><span data-stu-id="1a56f-234">**tooassign Britta Simon tooHalogen Software, perform hello following steps:**</span></span>

1. <span data-ttu-id="1a56f-235">W portalu Azure hello, otwórz widok aplikacji hello, a następnie przejdź do widoku katalogu toohello i przejść za**aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="1a56f-235">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Przypisz użytkownika][201] 

2. <span data-ttu-id="1a56f-237">Z listy aplikacji hello wybierz **oprogramowania chlorowców**.</span><span class="sxs-lookup"><span data-stu-id="1a56f-237">In hello applications list, select **Halogen Software**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-halogen-software-tutorial/tutorial_halogensoftware_app.png) 

3. <span data-ttu-id="1a56f-239">W menu powitania po lewej stronie powitania kliknij **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="1a56f-239">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Przypisz użytkownika][202] 

4. <span data-ttu-id="1a56f-241">Kliknij przycisk **Dodaj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="1a56f-241">Click **Add** button.</span></span> <span data-ttu-id="1a56f-242">Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="1a56f-242">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Przypisz użytkownika][203]

5. <span data-ttu-id="1a56f-244">Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** hello listy użytkowników.</span><span class="sxs-lookup"><span data-stu-id="1a56f-244">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="1a56f-245">Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="1a56f-245">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="1a56f-246">Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="1a56f-246">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="1a56f-247">Testowanie rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="1a56f-247">Testing single sign-on</span></span>

<span data-ttu-id="1a56f-248">Celem Hello w tej sekcji jest tootest programu Azure AD SSO konfiguracji przy użyciu hello panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="1a56f-248">hello objective of this section is tootest your Azure AD SSO configuration using hello Access Panel.</span></span>

<span data-ttu-id="1a56f-249">Po kliknięciu kafelka oprogramowania chlorowców hello w hello Panel dostępu, należy pobrać automatycznie zalogowane tooyour chlorowców aplikacji.</span><span class="sxs-lookup"><span data-stu-id="1a56f-249">When you click hello Halogen Software tile in hello Access Panel, you should get automatically signed-on tooyour Halogen Software application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="1a56f-250">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="1a56f-250">Additional resources</span></span>

* [<span data-ttu-id="1a56f-251">Lista samouczków dotyczących tooIntegrate aplikacji SaaS w usłudze Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="1a56f-251">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="1a56f-252">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="1a56f-252">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-halogen-software-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-halogen-software-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-halogen-software-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-halogen-software-tutorial/tutorial_general_04.png

[12]: ./media/active-directory-saas-halogen-software-tutorial/tutorial_halogen_12.png

[13]: ./media/active-directory-saas-halogen-software-tutorial/tutorial_halogen_13.png

[14]: ./media/active-directory-saas-halogen-software-tutorial/tutorial_halogen_14.png

[100]: ./media/active-directory-saas-halogen-software-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-halogen-software-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-halogen-software-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-halogen-software-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-halogen-software-tutorial/tutorial_general_203.png

[300]: ./media/active-directory-saas-halogen-software-tutorial/tutorial_halogen_300.png

[301]: ./media/active-directory-saas-halogen-software-tutorial/tutorial_halogen_301.png
