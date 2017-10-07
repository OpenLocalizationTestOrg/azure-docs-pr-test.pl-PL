---
title: 'Samouczek: Integracji Azure Active Directory z Panopto | Dokumentacja firmy Microsoft'
description: "Dowiedz się, jak tooconfigure logowanie jednokrotne między usługą Azure Active Directory i Panopto."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 89c88e23-93ce-4970-9baa-1104c4e8fe4a
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/30/2017
ms.author: jeedes
ms.openlocfilehash: 76b30e1cd2782bb5fba3d229378b8f82652b6503
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-panopto"></a><span data-ttu-id="97cfa-103">Samouczek: Integracji Azure Active Directory z Panopto</span><span class="sxs-lookup"><span data-stu-id="97cfa-103">Tutorial: Azure Active Directory integration with Panopto</span></span>

<span data-ttu-id="97cfa-104">Z tego samouczka, dowiesz się, jak toointegrate Panopto w usłudze Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="97cfa-104">In this tutorial, you learn how toointegrate Panopto with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="97cfa-105">Integracja z usługą Azure AD Panopto zapewnia hello następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="97cfa-105">Integrating Panopto with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="97cfa-106">Można kontrolować w usłudze Azure AD, kto ma dostęp do tooPanopto</span><span class="sxs-lookup"><span data-stu-id="97cfa-106">You can control in Azure AD who has access tooPanopto</span></span>
- <span data-ttu-id="97cfa-107">Można włączyć użytkownika użytkownicy tooautomatically get zalogowane tooPanopto (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="97cfa-107">You can enable your users tooautomatically get signed-on tooPanopto (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="97cfa-108">Możesz zarządzać kont w jednej centralnej lokalizacji - hello portalu Azure</span><span class="sxs-lookup"><span data-stu-id="97cfa-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="97cfa-109">Jeśli chcesz tooknow więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="97cfa-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="97cfa-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="97cfa-110">Prerequisites</span></span>

<span data-ttu-id="97cfa-111">tooconfigure integracji z usługą Azure AD z Panopto należy hello następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="97cfa-111">tooconfigure Azure AD integration with Panopto, you need hello following items:</span></span>

- <span data-ttu-id="97cfa-112">Subskrypcję usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="97cfa-112">An Azure AD subscription</span></span>
- <span data-ttu-id="97cfa-113">Panopto logowanie jednokrotne włączone subskrypcji</span><span class="sxs-lookup"><span data-stu-id="97cfa-113">A Panopto single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="97cfa-114">tootest hello kroków w tym samouczku, zaleca się przy użyciu środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="97cfa-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="97cfa-115">tootest hello kroki opisane w tym samouczku, należy stosować te zalecenia:</span><span class="sxs-lookup"><span data-stu-id="97cfa-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="97cfa-116">Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="97cfa-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="97cfa-117">Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz pobrać miesięczna wersja próbna [tutaj](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="97cfa-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="97cfa-118">Opis scenariusza</span><span class="sxs-lookup"><span data-stu-id="97cfa-118">Scenario description</span></span>
<span data-ttu-id="97cfa-119">W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym.</span><span class="sxs-lookup"><span data-stu-id="97cfa-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="97cfa-120">Scenariusz Hello opisane w tym samouczku składa się z dwóch głównych elementów:</span><span class="sxs-lookup"><span data-stu-id="97cfa-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="97cfa-121">Dodawanie Panopto z galerii hello</span><span class="sxs-lookup"><span data-stu-id="97cfa-121">Adding Panopto from hello gallery</span></span>
2. <span data-ttu-id="97cfa-122">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="97cfa-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-panopto-from-hello-gallery"></a><span data-ttu-id="97cfa-123">Dodawanie Panopto z galerii hello</span><span class="sxs-lookup"><span data-stu-id="97cfa-123">Adding Panopto from hello gallery</span></span>
<span data-ttu-id="97cfa-124">tooconfigure hello integracji Panopto do usługi Azure AD, należy tooadd Panopto z hello galerii tooyour listę zarządzanych aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="97cfa-124">tooconfigure hello integration of Panopto into Azure AD, you need tooadd Panopto from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="97cfa-125">**tooadd Panopto z galerii hello, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="97cfa-125">**tooadd Panopto from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="97cfa-126">W hello  **[portalu Azure](https://portal.azure.com)**na temat hello panelu nawigacji po lewej stronie, kliknij przycisk **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="97cfa-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Usługa Active Directory][1]

2. <span data-ttu-id="97cfa-128">Przejdź za**aplikacje dla przedsiębiorstw**.</span><span class="sxs-lookup"><span data-stu-id="97cfa-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="97cfa-129">Następnie przejdź zbyt**wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="97cfa-129">Then go too**All applications**.</span></span>

    ![Aplikacje][2]
    
3. <span data-ttu-id="97cfa-131">tooadd nową aplikację, kliknij przycisk **nowej aplikacji** przycisk u góry hello okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="97cfa-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplikacje][3]

4. <span data-ttu-id="97cfa-133">W polu wyszukiwania hello wpisz **Panopto**.</span><span class="sxs-lookup"><span data-stu-id="97cfa-133">In hello search box, type **Panopto**.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-panopto-tutorial/tutorial_panopto_search.png)

5. <span data-ttu-id="97cfa-135">W panelu wyników hello zaznacz **Panopto**, a następnie kliknij przycisk **Dodaj** przycisk aplikacji hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="97cfa-135">In hello results panel, select **Panopto**, and then click **Add** button tooadd hello application.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-panopto-tutorial/tutorial_panopto_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="97cfa-137">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="97cfa-137">Configuring and testing Azure AD single sign-on</span></span>

<span data-ttu-id="97cfa-138">W tej sekcji możesz skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z Panopto na podstawie użytkownika testowego, nazywany "Britta Simona".</span><span class="sxs-lookup"><span data-stu-id="97cfa-138">In this section, you configure and test Azure AD single sign-on with Panopto based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="97cfa-139">Dla pojedynczego logowania jednokrotnego toowork usługi Azure AD musi tooknow użytkownika odpowiednikiem hello w Panopto jest tooa użytkownika w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="97cfa-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Panopto is tooa user in Azure AD.</span></span> <span data-ttu-id="97cfa-140">Innymi słowy relację łącza między użytkownika usługi Azure AD i hello użytkownikowi w Panopto musi toobe ustanowione.</span><span class="sxs-lookup"><span data-stu-id="97cfa-140">In other words, a link relationship between an Azure AD user and hello related user in Panopto needs toobe established.</span></span>

<span data-ttu-id="97cfa-141">W Panopto, należy przypisać wartość hello hello **nazwy użytkownika** w usłudze Azure AD jako wartość hello hello **Username** tooestablish hello łącze relacji.</span><span class="sxs-lookup"><span data-stu-id="97cfa-141">In Panopto, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="97cfa-142">tooconfigure i testowych usługi Azure AD rejestracji jednokrotnej z Panopto, należy po bloków konstrukcyjnych hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="97cfa-142">tooconfigure and test Azure AD single sign-on with Panopto, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="97cfa-143">**[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configuring-azure-ad-single-sign-on)**  -tooenable Twojego toouse użytkowników tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="97cfa-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="97cfa-144">**[Tworzenie użytkownika testowego usługi Azure AD](#creating-an-azure-ad-test-user)**  -tootest usługi Azure AD rejestracji jednokrotnej z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="97cfa-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="97cfa-145">**[Tworzenie użytkownika testowego Panopto](#creating-a-panopto-test-user)**  -toohave odpowiednikiem Simona Britta w Panopto, który jest połączony toohello usługi Azure AD reprezentację użytkownika.</span><span class="sxs-lookup"><span data-stu-id="97cfa-145">**[Creating a Panopto test user](#creating-a-panopto-test-user)** - toohave a counterpart of Britta Simon in Panopto that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="97cfa-146">**[Przypisanie użytkownika testowego hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Simona Britta toouse usługi Azure AD rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="97cfa-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="97cfa-147">**[Testowanie rejestracji jednokrotnej](#testing-single-sign-on)**  -tooverify czy hello konfiguracji działania.</span><span class="sxs-lookup"><span data-stu-id="97cfa-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="97cfa-148">Konfigurowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="97cfa-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="97cfa-149">W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w portalu Azure hello i skonfigurować logowanie jednokrotne w aplikacji Panopto.</span><span class="sxs-lookup"><span data-stu-id="97cfa-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Panopto application.</span></span>

<span data-ttu-id="97cfa-150">**tooconfigure usługi Azure AD rejestracji jednokrotnej z Panopto, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="97cfa-150">**tooconfigure Azure AD single sign-on with Panopto, perform hello following steps:**</span></span>

1. <span data-ttu-id="97cfa-151">W portalu Azure na powitania hello **Panopto** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.</span><span class="sxs-lookup"><span data-stu-id="97cfa-151">In hello Azure portal, on hello **Panopto** application integration page, click **Single sign-on**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej][4]

2. <span data-ttu-id="97cfa-153">Na powitania **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** tooenable rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="97cfa-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-panopto-tutorial/tutorial_panopto_samlbase.png)

3. <span data-ttu-id="97cfa-155">Na powitania **Panopto domeny i adres URL** sekcji, wykonaj następujące kroki hello:</span><span class="sxs-lookup"><span data-stu-id="97cfa-155">On hello **Panopto Domain and URLs** section, perform hello following steps:</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-panopto-tutorial/tutorial_panopto_url.png)

    <span data-ttu-id="97cfa-157">W hello **adres URL logowania** tekstowym, wpisz adres URL za pomocą hello następującego wzorca:`https://<tenant-name>.panopto.com`</span><span class="sxs-lookup"><span data-stu-id="97cfa-157">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<tenant-name>.panopto.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="97cfa-158">Ta wartość nie jest prawdziwe.</span><span class="sxs-lookup"><span data-stu-id="97cfa-158">This value is not real.</span></span> <span data-ttu-id="97cfa-159">Zaktualizuj tę wartość z hello rzeczywisty adres URL logowania.</span><span class="sxs-lookup"><span data-stu-id="97cfa-159">Update this value with hello actual Sign-On URL.</span></span> <span data-ttu-id="97cfa-160">Skontaktuj się z [zespołem pomocy technicznej klienta Panopto](mailto:support@panopto.com‎) tooget tej wartości.</span><span class="sxs-lookup"><span data-stu-id="97cfa-160">Contact [Panopto Client support team](mailto:support@panopto.com‎) tooget this value.</span></span> 
 
4. <span data-ttu-id="97cfa-161">Na powitania **certyfikat podpisywania SAML** kliknij **XML metadanych** , a następnie zapisz plik metadanych hello na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="97cfa-161">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-panopto-tutorial/tutorial_panopto_certificate.png) 

5. <span data-ttu-id="97cfa-163">Kliknij przycisk **zapisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="97cfa-163">Click **Save** button.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-panopto-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="97cfa-165">Na powitania **konfiguracji Panopto** kliknij **skonfigurować Panopto** tooopen **Konfigurowanie logowania jednokrotnego** okna.</span><span class="sxs-lookup"><span data-stu-id="97cfa-165">On hello **Panopto Configuration** section, click **Configure Panopto** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="97cfa-166">Kopiuj hello **identyfikator jednostki SAML i SAML pojedynczy znak na adres URL usługi** z hello **sekcji krótkimi opisami.**</span><span class="sxs-lookup"><span data-stu-id="97cfa-166">Copy hello **SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-panopto-tutorial/tutorial_panopto_configure.png) 

7. <span data-ttu-id="97cfa-168">W oknie przeglądarki innej witryny sieci web Zaloguj się w witrynie firmy Panopto tooyour jako administrator.</span><span class="sxs-lookup"><span data-stu-id="97cfa-168">In a different web browser window, log in tooyour Panopto company site as an administrator.</span></span>

8. <span data-ttu-id="97cfa-169">Na powitania narzędzi po lewej stronie powitania kliknij **systemu**, a następnie kliknij przycisk **dostawców tożsamości**.</span><span class="sxs-lookup"><span data-stu-id="97cfa-169">In hello toolbar on hello left, click **System**, and then click **Identity Providers**.</span></span>
   
   <span data-ttu-id="97cfa-170">![System](./media/active-directory-saas-panopto-tutorial/ic777670.png "systemu")</span><span class="sxs-lookup"><span data-stu-id="97cfa-170">![System](./media/active-directory-saas-panopto-tutorial/ic777670.png "System")</span></span>
9. <span data-ttu-id="97cfa-171">Kliknij przycisk **dodać dostawcę**.</span><span class="sxs-lookup"><span data-stu-id="97cfa-171">Click **Add Provider**.</span></span>
   
   <span data-ttu-id="97cfa-172">![Dostawców tożsamości](./media/active-directory-saas-panopto-tutorial/ic777671.png "dostawców tożsamości")</span><span class="sxs-lookup"><span data-stu-id="97cfa-172">![Identity Providers](./media/active-directory-saas-panopto-tutorial/ic777671.png "Identity Providers")</span></span>
   
10. <span data-ttu-id="97cfa-173">W sekcji dostawcy SAML hello wykonaj hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="97cfa-173">In hello SAML provider section, perform hello following steps:</span></span>
   
    <span data-ttu-id="97cfa-174">![Konfiguracja SaaS](./media/active-directory-saas-panopto-tutorial/ic777672.png "SaaS konfiguracji")</span><span class="sxs-lookup"><span data-stu-id="97cfa-174">![SaaS configuration](./media/active-directory-saas-panopto-tutorial/ic777672.png "SaaS configuration")</span></span>
    
    <span data-ttu-id="97cfa-175">a.</span><span class="sxs-lookup"><span data-stu-id="97cfa-175">a.</span></span> <span data-ttu-id="97cfa-176">Z hello **typ dostawcy** listy, wybierz **SAML20**.</span><span class="sxs-lookup"><span data-stu-id="97cfa-176">From hello **Provider Type** list, select **SAML20**.</span></span>    
    
    <span data-ttu-id="97cfa-177">b.</span><span class="sxs-lookup"><span data-stu-id="97cfa-177">b.</span></span> <span data-ttu-id="97cfa-178">W hello **nazwa wystąpienia** tekstowym, wpisz nazwę wystąpienia hello.</span><span class="sxs-lookup"><span data-stu-id="97cfa-178">In hello **Instance Name** textbox, type a name for hello instance.</span></span>

    <span data-ttu-id="97cfa-179">c.</span><span class="sxs-lookup"><span data-stu-id="97cfa-179">c.</span></span> <span data-ttu-id="97cfa-180">W hello **przyjazny opis** tekstowym, wpisz przyjazny opis.</span><span class="sxs-lookup"><span data-stu-id="97cfa-180">In hello **Friendly Description** textbox, type a friendly description.</span></span>
    
    <span data-ttu-id="97cfa-181">d.</span><span class="sxs-lookup"><span data-stu-id="97cfa-181">d.</span></span> <span data-ttu-id="97cfa-182">W **Odbijanie adres Url strony** pole tekstowe, Wklej wartość hello **SAML pojedynczy znak na adres URL usługi**, które zostały skopiowane z portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="97cfa-182">In **Bounce Page Url** textbox, paste hello value of **SAML Single Sign-On Service URL**, which you have copied from Azure portal.</span></span>

    <span data-ttu-id="97cfa-183">e.</span><span class="sxs-lookup"><span data-stu-id="97cfa-183">e.</span></span> <span data-ttu-id="97cfa-184">W hello **wystawcy** pole tekstowe, Wklej wartość hello **identyfikator jednostki SAML**, które zostały skopiowane z portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="97cfa-184">In hello **Issuer** textbox, paste hello value of **SAML Entity ID**, which you have copied from Azure portal.</span></span>

    <span data-ttu-id="97cfa-185">f.</span><span class="sxs-lookup"><span data-stu-id="97cfa-185">f.</span></span> <span data-ttu-id="97cfa-186">Otwieranie certyfikatu zakodowanego base-64, które zostały pobrane z usługi Azure portalu, hello kopiowania zawartości go w Schowku tooyour, a następnie wklej go toohello **klucz publiczny** pola tekstowego.</span><span class="sxs-lookup"><span data-stu-id="97cfa-186">Open your base-64 encoded certificate, which you have downloaded from Azure portal, copy hello content of it in tooyour clipboard, and then paste it toohello **Public Key**  textbox.</span></span>

11. <span data-ttu-id="97cfa-187">Kliknij pozycję **Zapisz**.</span><span class="sxs-lookup"><span data-stu-id="97cfa-187">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="97cfa-188">Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz hello [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji hello!</span><span class="sxs-lookup"><span data-stu-id="97cfa-188">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="97cfa-189">Po dodaniu tej aplikacji z hello **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij hello **rejestracji jednokrotnej** hello kartę i dostępu do osadzonych dokumentacji za pośrednictwem hello  **Konfiguracja** sekcji u dołu hello.</span><span class="sxs-lookup"><span data-stu-id="97cfa-189">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="97cfa-190">Więcej o hello osadzonych dokumentacji funkcji w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="97cfa-190">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="97cfa-191">Tworzenie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="97cfa-191">Creating an Azure AD test user</span></span>

<span data-ttu-id="97cfa-192">Celem Hello w tej sekcji jest toocreate użytkownika testowego, w portalu Azure o nazwie Simona Britta hello.</span><span class="sxs-lookup"><span data-stu-id="97cfa-192">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Tworzenie użytkowników usługi Azure AD][100]

<span data-ttu-id="97cfa-194">**toocreate użytkownika testowego w usłudze Azure AD, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="97cfa-194">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="97cfa-195">W hello **portalu Azure**na temat hello w lewym okienku nawigacji, kliknij przycisk **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="97cfa-195">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-panopto-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="97cfa-197">toodisplay hello listę użytkowników, przejdź zbyt**użytkowników i grup** i kliknij przycisk **wszyscy użytkownicy**.</span><span class="sxs-lookup"><span data-stu-id="97cfa-197">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-panopto-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="97cfa-199">Witaj tooopen **użytkownika** okna dialogowego, kliknij przycisk **Dodaj** u góry hello hello okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="97cfa-199">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-panopto-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="97cfa-201">Na powitania **użytkownika** okna dialogowego wykonaj hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="97cfa-201">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-panopto-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="97cfa-203">a.</span><span class="sxs-lookup"><span data-stu-id="97cfa-203">a.</span></span> <span data-ttu-id="97cfa-204">W hello **nazwa** pole tekstowe, typ **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="97cfa-204">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="97cfa-205">b.</span><span class="sxs-lookup"><span data-stu-id="97cfa-205">b.</span></span> <span data-ttu-id="97cfa-206">W hello **nazwy użytkownika** pole tekstowe, hello typu **adres e-mail** z BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="97cfa-206">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="97cfa-207">c.</span><span class="sxs-lookup"><span data-stu-id="97cfa-207">c.</span></span> <span data-ttu-id="97cfa-208">Wybierz **Pokaż hasło** i zanotuj wartość hello hello **hasło**.</span><span class="sxs-lookup"><span data-stu-id="97cfa-208">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="97cfa-209">d.</span><span class="sxs-lookup"><span data-stu-id="97cfa-209">d.</span></span> <span data-ttu-id="97cfa-210">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="97cfa-210">Click **Create**.</span></span>
 
### <a name="creating-a-panopto-test-user"></a><span data-ttu-id="97cfa-211">Tworzenie użytkownika testowego Panopto</span><span class="sxs-lookup"><span data-stu-id="97cfa-211">Creating a Panopto test user</span></span>

<span data-ttu-id="97cfa-212">Nie ma elementu akcji można tooconfigure użytkownika inicjowania obsługi administracyjnej tooPanopto.</span><span class="sxs-lookup"><span data-stu-id="97cfa-212">There is no action item for you tooconfigure user provisioning tooPanopto.</span></span>  
<span data-ttu-id="97cfa-213">Gdy przypisany użytkownik podejmie próbę toolog w tooPanopto za pomocą panelu dostępu hello, Panopto sprawdza, czy istnieje hello użytkownika.</span><span class="sxs-lookup"><span data-stu-id="97cfa-213">When an assigned user tries toolog in tooPanopto using hello access panel, Panopto checks whether hello user exists.</span></span>  

<span data-ttu-id="97cfa-214">Jeśli nie jest Brak konta użytkownika dostępny jeszcze, są tworzone przez Panopto.</span><span class="sxs-lookup"><span data-stu-id="97cfa-214">If there is no user account available yet, it is automatically created by Panopto.</span></span>

>[!NOTE]
><span data-ttu-id="97cfa-215">Możesz użyć innych Panopto użytkownika konta tworzenia narzędzi lub interfejsów API dostarczonych przez Panopto tooprovision kont użytkowników usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="97cfa-215">You can use any other Panopto user account creation tools or APIs provided by Panopto tooprovision Azure AD user accounts.</span></span>
>
>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="97cfa-216">Przypisanie użytkownika testowego hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="97cfa-216">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="97cfa-217">W tej sekcji możesz włączyć toouse Simona Britta Azure logowania jednokrotnego za udzielanie dostępu tooPanopto.</span><span class="sxs-lookup"><span data-stu-id="97cfa-217">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooPanopto.</span></span>

![Przypisz użytkownika][200] 

<span data-ttu-id="97cfa-219">**tooassign tooPanopto Simona Britta wykonaj hello następujące kroki:**</span><span class="sxs-lookup"><span data-stu-id="97cfa-219">**tooassign Britta Simon tooPanopto, perform hello following steps:**</span></span>

1. <span data-ttu-id="97cfa-220">W portalu Azure hello, otwórz widok aplikacji hello, a następnie przejdź do widoku katalogu toohello i przejść za**aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="97cfa-220">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Przypisz użytkownika][201] 

2. <span data-ttu-id="97cfa-222">Z listy aplikacji hello wybierz **Panopto**.</span><span class="sxs-lookup"><span data-stu-id="97cfa-222">In hello applications list, select **Panopto**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-panopto-tutorial/tutorial_panopto_app.png) 

3. <span data-ttu-id="97cfa-224">W menu powitania po lewej stronie powitania kliknij **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="97cfa-224">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Przypisz użytkownika][202] 

4. <span data-ttu-id="97cfa-226">Kliknij przycisk **Dodaj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="97cfa-226">Click **Add** button.</span></span> <span data-ttu-id="97cfa-227">Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="97cfa-227">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Przypisz użytkownika][203]

5. <span data-ttu-id="97cfa-229">Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** hello listy użytkowników.</span><span class="sxs-lookup"><span data-stu-id="97cfa-229">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="97cfa-230">Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="97cfa-230">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="97cfa-231">Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="97cfa-231">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="97cfa-232">Testowanie rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="97cfa-232">Testing single sign-on</span></span>

<span data-ttu-id="97cfa-233">W tej sekcji można przetestować konfiguracji usługi Azure AD pojedynczego logowania jednokrotnego przy użyciu hello panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="97cfa-233">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="97cfa-234">Po kliknięciu kafelka Panopto hello w hello Panel dostępu, należy uzyskać automatycznie strony logowania Panopto aplikacji.</span><span class="sxs-lookup"><span data-stu-id="97cfa-234">When you click hello Panopto tile in hello Access Panel, you should get automatically login page of Panopto application.</span></span>
<span data-ttu-id="97cfa-235">Aby uzyskać więcej informacji na temat hello Panel dostępu, zobacz [toohello wprowadzenie panelu dostępu](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="97cfa-235">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="97cfa-236">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="97cfa-236">Additional resources</span></span>

* [<span data-ttu-id="97cfa-237">Lista samouczków dotyczących tooIntegrate aplikacji SaaS w usłudze Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="97cfa-237">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="97cfa-238">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="97cfa-238">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-panopto-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-panopto-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-panopto-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-panopto-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-panopto-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-panopto-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-panopto-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-panopto-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-panopto-tutorial/tutorial_general_203.png

