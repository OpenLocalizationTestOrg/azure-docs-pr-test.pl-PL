---
title: 'Samouczek: Integracji Azure Active Directory z EverBridge | Dokumentacja firmy Microsoft'
description: "Dowiedz się, jak tooconfigure logowanie jednokrotne między usługą Azure Active Directory i EverBridge."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 58d7cd22-98c0-4606-9ce5-8bdb22ee8b3e
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/16/2017
ms.author: jeedes
ms.openlocfilehash: a260298279407ed709bc2e685a104410f9836a74
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-everbridge"></a><span data-ttu-id="18ffa-103">Samouczek: Integracji Azure Active Directory z EverBridge</span><span class="sxs-lookup"><span data-stu-id="18ffa-103">Tutorial: Azure Active Directory integration with EverBridge</span></span>

<span data-ttu-id="18ffa-104">Z tego samouczka, dowiesz się, jak toointegrate EverBridge w usłudze Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="18ffa-104">In this tutorial, you learn how toointegrate EverBridge with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="18ffa-105">Integracja z usługą Azure AD EverBridge zapewnia hello następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="18ffa-105">Integrating EverBridge with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="18ffa-106">Można kontrolować w usłudze Azure AD, kto ma dostęp do tooEverBridge</span><span class="sxs-lookup"><span data-stu-id="18ffa-106">You can control in Azure AD who has access tooEverBridge</span></span>
- <span data-ttu-id="18ffa-107">Można włączyć użytkownika użytkownicy tooautomatically get zalogowane tooEverBridge (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="18ffa-107">You can enable your users tooautomatically get signed-on tooEverBridge (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="18ffa-108">Możesz zarządzać kont w jednej centralnej lokalizacji - hello portalu Azure</span><span class="sxs-lookup"><span data-stu-id="18ffa-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="18ffa-109">Jeśli chcesz tooknow więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="18ffa-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="18ffa-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="18ffa-110">Prerequisites</span></span>

<span data-ttu-id="18ffa-111">tooconfigure integracji z usługą Azure AD z EverBridge należy hello następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="18ffa-111">tooconfigure Azure AD integration with EverBridge, you need hello following items:</span></span>

- <span data-ttu-id="18ffa-112">Subskrypcję usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="18ffa-112">An Azure AD subscription</span></span>
- <span data-ttu-id="18ffa-113">EverBridge jednokrotnego włączone subskrypcji</span><span class="sxs-lookup"><span data-stu-id="18ffa-113">An EverBridge single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="18ffa-114">tootest hello kroków w tym samouczku, zaleca się przy użyciu środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="18ffa-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="18ffa-115">tootest hello kroki opisane w tym samouczku, należy stosować te zalecenia:</span><span class="sxs-lookup"><span data-stu-id="18ffa-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="18ffa-116">Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="18ffa-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="18ffa-117">Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz pobrać miesięczna wersja próbna [tutaj](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="18ffa-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="18ffa-118">Opis scenariusza</span><span class="sxs-lookup"><span data-stu-id="18ffa-118">Scenario description</span></span>
<span data-ttu-id="18ffa-119">W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym.</span><span class="sxs-lookup"><span data-stu-id="18ffa-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="18ffa-120">Scenariusz Hello opisane w tym samouczku składa się z dwóch głównych elementów:</span><span class="sxs-lookup"><span data-stu-id="18ffa-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="18ffa-121">Dodawanie EverBridge z galerii hello</span><span class="sxs-lookup"><span data-stu-id="18ffa-121">Adding EverBridge from hello gallery</span></span>
2. <span data-ttu-id="18ffa-122">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="18ffa-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-everbridge-from-hello-gallery"></a><span data-ttu-id="18ffa-123">Dodawanie EverBridge z galerii hello</span><span class="sxs-lookup"><span data-stu-id="18ffa-123">Adding EverBridge from hello gallery</span></span>
<span data-ttu-id="18ffa-124">tooconfigure hello integracji EverBridge do usługi Azure AD, należy tooadd EverBridge z hello galerii tooyour listę zarządzanych aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="18ffa-124">tooconfigure hello integration of EverBridge into Azure AD, you need tooadd EverBridge from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="18ffa-125">**tooadd EverBridge z galerii hello, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="18ffa-125">**tooadd EverBridge from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="18ffa-126">W hello  **[portalu Azure](https://portal.azure.com)**na temat hello panelu nawigacji po lewej stronie, kliknij przycisk **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="18ffa-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Usługa Active Directory][1]

2. <span data-ttu-id="18ffa-128">Przejdź za**aplikacje dla przedsiębiorstw**.</span><span class="sxs-lookup"><span data-stu-id="18ffa-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="18ffa-129">Następnie przejdź zbyt**wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="18ffa-129">Then go too**All applications**.</span></span>

    ![Aplikacje][2]
    
3. <span data-ttu-id="18ffa-131">tooadd nową aplikację, kliknij przycisk **nowej aplikacji** przycisk u góry hello okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="18ffa-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplikacje][3]

4. <span data-ttu-id="18ffa-133">W polu wyszukiwania hello wpisz **EverBridge**.</span><span class="sxs-lookup"><span data-stu-id="18ffa-133">In hello search box, type **EverBridge**.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-everbridge-tutorial/tutorial_everbridge_search.png)

5. <span data-ttu-id="18ffa-135">W panelu wyników hello zaznacz **EverBridge**, a następnie kliknij przycisk **Dodaj** przycisk aplikacji hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="18ffa-135">In hello results panel, select **EverBridge**, and then click **Add** button tooadd hello application.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-everbridge-tutorial/tutorial_everbridge_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="18ffa-137">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="18ffa-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="18ffa-138">W tej sekcji skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z EverBridge w oparciu o nazwie "Britta Simona" użytkownika testowego.</span><span class="sxs-lookup"><span data-stu-id="18ffa-138">In this section, you configure and test Azure AD single sign-on with EverBridge based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="18ffa-139">Dla pojedynczego logowania jednokrotnego toowork usługi Azure AD musi tooknow użytkownika odpowiednikiem hello w EverBridge jest tooa użytkownika w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="18ffa-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in EverBridge is tooa user in Azure AD.</span></span> <span data-ttu-id="18ffa-140">Innymi słowy relację łącza między użytkownika usługi Azure AD i hello użytkownikowi w EverBridge musi toobe ustanowione.</span><span class="sxs-lookup"><span data-stu-id="18ffa-140">In other words, a link relationship between an Azure AD user and hello related user in EverBridge needs toobe established.</span></span>

<span data-ttu-id="18ffa-141">W EverBridge, należy przypisać wartość hello hello **nazwy użytkownika** w usłudze Azure AD jako wartość hello hello **Username** tooestablish hello łącze relacji.</span><span class="sxs-lookup"><span data-stu-id="18ffa-141">In EverBridge, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="18ffa-142">tooconfigure i testowych usługi Azure AD rejestracji jednokrotnej z EverBridge, należy po bloków konstrukcyjnych hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="18ffa-142">tooconfigure and test Azure AD single sign-on with EverBridge, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="18ffa-143">**[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configuring-azure-ad-single-sign-on)**  -tooenable Twojego toouse użytkowników tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="18ffa-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="18ffa-144">**[Tworzenie użytkownika testowego usługi Azure AD](#creating-an-azure-ad-test-user)**  -tootest usługi Azure AD rejestracji jednokrotnej z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="18ffa-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="18ffa-145">**[Tworzenie użytkownika testowego EverBridge](#creating-an-everbridge-test-user)**  -toohave odpowiednikiem Simona Britta w EverBridge, który jest połączony toohello usługi Azure AD reprezentację użytkownika.</span><span class="sxs-lookup"><span data-stu-id="18ffa-145">**[Creating an EverBridge test user](#creating-an-everbridge-test-user)** - toohave a counterpart of Britta Simon in EverBridge that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="18ffa-146">**[Przypisanie użytkownika testowego hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Simona Britta toouse usługi Azure AD rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="18ffa-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="18ffa-147">**[Testowanie rejestracji jednokrotnej](#testing-single-sign-on)**  -tooverify czy hello konfiguracji działania.</span><span class="sxs-lookup"><span data-stu-id="18ffa-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="18ffa-148">Konfigurowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="18ffa-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="18ffa-149">W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w portalu Azure hello i skonfigurować logowanie jednokrotne w aplikacji EverBridge.</span><span class="sxs-lookup"><span data-stu-id="18ffa-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your EverBridge application.</span></span>

<span data-ttu-id="18ffa-150">**tooconfigure usługi Azure AD rejestracji jednokrotnej z EverBridge, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="18ffa-150">**tooconfigure Azure AD single sign-on with EverBridge, perform hello following steps:**</span></span>

1. <span data-ttu-id="18ffa-151">W portalu Azure na powitania hello **EverBridge** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.</span><span class="sxs-lookup"><span data-stu-id="18ffa-151">In hello Azure portal, on hello **EverBridge** application integration page, click **Single sign-on**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej][4]

2. <span data-ttu-id="18ffa-153">Na powitania **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** tooenable rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="18ffa-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-everbridge-tutorial/tutorial_everbridge_samlbase.png)

3. <span data-ttu-id="18ffa-155">Na powitania **EverBridge domeny i adres URL** sekcji, wykonaj następujące kroki hello:</span><span class="sxs-lookup"><span data-stu-id="18ffa-155">On hello **EverBridge Domain and URLs** section, perform hello following steps:</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-everbridge-tutorial/tutorial_everbridge_url.png)

    <span data-ttu-id="18ffa-157">a.</span><span class="sxs-lookup"><span data-stu-id="18ffa-157">a.</span></span> <span data-ttu-id="18ffa-158">W hello **identyfikator** tekstowym, wpisz adres URL za pomocą hello następującego wzorca:`https://sso.everbridge.net/<companyname>`</span><span class="sxs-lookup"><span data-stu-id="18ffa-158">In hello **Identifier** textbox, type a URL using hello following pattern: `https://sso.everbridge.net/<companyname>`</span></span>

    <span data-ttu-id="18ffa-159">b.</span><span class="sxs-lookup"><span data-stu-id="18ffa-159">b.</span></span> <span data-ttu-id="18ffa-160">W hello **adres URL odpowiedzi** tekstowym, wpisz adres URL za pomocą hello następującego wzorca:`https://manager.everbridge.net/saml/SSO/<companyname>/alias/defaultAlias`</span><span class="sxs-lookup"><span data-stu-id="18ffa-160">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://manager.everbridge.net/saml/SSO/<companyname>/alias/defaultAlias`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="18ffa-161">Wartości te nie są prawdziwe.</span><span class="sxs-lookup"><span data-stu-id="18ffa-161">These values are not real.</span></span> <span data-ttu-id="18ffa-162">Witaj rzeczywisty identyfikator i odpowiedzi adresu URL, należy zaktualizować te wartości.</span><span class="sxs-lookup"><span data-stu-id="18ffa-162">Update these values with hello actual Identifier and Reply URL.</span></span> <span data-ttu-id="18ffa-163">Skontaktuj się z [zespołem pomocy technicznej EverBridge](mailto:support@everbridge.com) tooget tych wartości.</span><span class="sxs-lookup"><span data-stu-id="18ffa-163">Contact [EverBridge support team](mailto:support@everbridge.com) tooget these values.</span></span>
 
4. <span data-ttu-id="18ffa-164">Na powitania **certyfikat podpisywania SAML** kliknij **XML metadanych** , a następnie zapisz plik metadanych hello na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="18ffa-164">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-everbridge-tutorial/tutorial_everbridge_certificate.png) 

5. <span data-ttu-id="18ffa-166">Kliknij przycisk **zapisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="18ffa-166">Click **Save** button.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-everbridge-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="18ffa-168">Na powitania **konfiguracji EverBridge** kliknij **skonfigurować EverBridge** tooopen **Konfigurowanie logowania jednokrotnego** okna.</span><span class="sxs-lookup"><span data-stu-id="18ffa-168">On hello **EverBridge Configuration** section, click **Configure EverBridge** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="18ffa-169">Kopiuj hello **SAML pojedynczy znak na adres URL usługi** z hello **sekcji krótkimi opisami.**</span><span class="sxs-lookup"><span data-stu-id="18ffa-169">Copy hello **SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-everbridge-tutorial/tutorial_everbridge_configure.png) 

6. <span data-ttu-id="18ffa-171">tooget logowania jednokrotnego skonfigurowane dla aplikacji, należy na toosign tooyour Everbridge dzierżawy z uprawnieniami administratora.</span><span class="sxs-lookup"><span data-stu-id="18ffa-171">tooget SSO configured for your application, you need toosign-on tooyour Everbridge tenant as an administrator.</span></span>

7. <span data-ttu-id="18ffa-172">W menu hello na górze powitania kliknij hello **ustawienia** i wybierz **rejestracji jednokrotnej** w obszarze **zabezpieczeń**.</span><span class="sxs-lookup"><span data-stu-id="18ffa-172">In hello menu on hello top, click hello **Settings** tab and select **Single Sign-On** under **Security**.</span></span>
   
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-everbridge-tutorial/tutorial_everbridge_002.png)
   
    <span data-ttu-id="18ffa-174">a.</span><span class="sxs-lookup"><span data-stu-id="18ffa-174">a.</span></span> <span data-ttu-id="18ffa-175">W hello **nazwa** pole tekstowe, nazwa typu hello identyfikatora dostawcy (na przykład: Nazwa firmy).</span><span class="sxs-lookup"><span data-stu-id="18ffa-175">In hello **Name** textbox, type hello name of Identifier Provider (for example: your company name).</span></span>
   
    <span data-ttu-id="18ffa-176">b.</span><span class="sxs-lookup"><span data-stu-id="18ffa-176">b.</span></span> <span data-ttu-id="18ffa-177">W hello **Nazwa interfejsu API** pole tekstowe, nazwa typu hello interfejsu API.</span><span class="sxs-lookup"><span data-stu-id="18ffa-177">In hello **API Name** textbox, type hello name of API.</span></span>
   
    <span data-ttu-id="18ffa-178">c.</span><span class="sxs-lookup"><span data-stu-id="18ffa-178">c.</span></span> <span data-ttu-id="18ffa-179">Kliknij przycisk **wybierz plik** przycisk tooupload hello metadanych pliku, który został pobrany z portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="18ffa-179">Click **Choose File** button tooupload hello metadata file which you downloaded from Azure portal.</span></span>
   
    <span data-ttu-id="18ffa-180">d.</span><span class="sxs-lookup"><span data-stu-id="18ffa-180">d.</span></span> <span data-ttu-id="18ffa-181">W lokalizacji tożsamości SAML hello, wybierz **jest tożsamość w elemencie NameIdentifier hello hello instrukcji podmiotu**.</span><span class="sxs-lookup"><span data-stu-id="18ffa-181">In hello SAML Identity Location, select **Identity is in hello NameIdentifier element of hello Subject statement**.</span></span>
   
    <span data-ttu-id="18ffa-182">e.</span><span class="sxs-lookup"><span data-stu-id="18ffa-182">e.</span></span> <span data-ttu-id="18ffa-183">W hello **adresu URL logowania do dostawcy tożsamości** pole tekstowe, wartość hello Wklej adres URL logowania jednokrotnego SAML z usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="18ffa-183">In hello **Identity Provider Login URL** textbox, paste hello value of SAML SSO URL from Azure AD.</span></span>
   
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-everbridge-tutorial/tutorial_everbridge_003.png)
   
    <span data-ttu-id="18ffa-185">f.</span><span class="sxs-lookup"><span data-stu-id="18ffa-185">f.</span></span> <span data-ttu-id="18ffa-186">Hello dostawcy zainicjował żądanie powiązania usługi, wybierz **przekierowywanie HTTP**.</span><span class="sxs-lookup"><span data-stu-id="18ffa-186">In hello Service Provider Initiated Request Binding, select **HTTP Redirect**.</span></span>

    <span data-ttu-id="18ffa-187">g.</span><span class="sxs-lookup"><span data-stu-id="18ffa-187">g.</span></span> <span data-ttu-id="18ffa-188">Kliknij przycisk **Zapisz**</span><span class="sxs-lookup"><span data-stu-id="18ffa-188">Click **Save**</span></span>

> [!TIP]
> <span data-ttu-id="18ffa-189">Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz hello [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji hello!</span><span class="sxs-lookup"><span data-stu-id="18ffa-189">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="18ffa-190">Po dodaniu tej aplikacji z hello **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij hello **rejestracji jednokrotnej** hello kartę i dostępu do osadzonych dokumentacji za pośrednictwem hello  **Konfiguracja** sekcji u dołu hello.</span><span class="sxs-lookup"><span data-stu-id="18ffa-190">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="18ffa-191">Więcej o hello osadzonych dokumentacji funkcji w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="18ffa-191">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="18ffa-192">Tworzenie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="18ffa-192">Creating an Azure AD test user</span></span>
<span data-ttu-id="18ffa-193">Celem Hello w tej sekcji jest toocreate użytkownika testowego, w portalu Azure o nazwie Simona Britta hello.</span><span class="sxs-lookup"><span data-stu-id="18ffa-193">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Tworzenie użytkowników usługi Azure AD][100]

<span data-ttu-id="18ffa-195">**toocreate użytkownika testowego w usłudze Azure AD, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="18ffa-195">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="18ffa-196">W hello **portalu Azure**na temat hello w lewym okienku nawigacji, kliknij przycisk **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="18ffa-196">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-everbridge-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="18ffa-198">toodisplay hello listę użytkowników, przejdź zbyt**użytkowników i grup** i kliknij przycisk **wszyscy użytkownicy**.</span><span class="sxs-lookup"><span data-stu-id="18ffa-198">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-everbridge-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="18ffa-200">Witaj tooopen **użytkownika** okna dialogowego, kliknij przycisk **Dodaj** u góry hello hello okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="18ffa-200">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-everbridge-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="18ffa-202">Na powitania **użytkownika** okna dialogowego wykonaj hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="18ffa-202">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-everbridge-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="18ffa-204">a.</span><span class="sxs-lookup"><span data-stu-id="18ffa-204">a.</span></span> <span data-ttu-id="18ffa-205">W hello **nazwa** pole tekstowe, typ **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="18ffa-205">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="18ffa-206">b.</span><span class="sxs-lookup"><span data-stu-id="18ffa-206">b.</span></span> <span data-ttu-id="18ffa-207">W hello **nazwy użytkownika** pole tekstowe, hello typu **adres e-mail** z BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="18ffa-207">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="18ffa-208">c.</span><span class="sxs-lookup"><span data-stu-id="18ffa-208">c.</span></span> <span data-ttu-id="18ffa-209">Wybierz **Pokaż hasło** i zanotuj wartość hello hello **hasło**.</span><span class="sxs-lookup"><span data-stu-id="18ffa-209">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="18ffa-210">d.</span><span class="sxs-lookup"><span data-stu-id="18ffa-210">d.</span></span> <span data-ttu-id="18ffa-211">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="18ffa-211">Click **Create**.</span></span>
 
### <a name="creating-an-everbridge-test-user"></a><span data-ttu-id="18ffa-212">Tworzenie użytkownika testowego EverBridge</span><span class="sxs-lookup"><span data-stu-id="18ffa-212">Creating an EverBridge test user</span></span>

<span data-ttu-id="18ffa-213">W tej sekcji należy utworzyć użytkownika o nazwie Simona Britta w Everbridge.</span><span class="sxs-lookup"><span data-stu-id="18ffa-213">In this section, you create a user called Britta Simon in Everbridge.</span></span> <span data-ttu-id="18ffa-214">Praca z [zespołem pomocy technicznej EverBridge](mailto:support@everbridge.com) tooadd hello użytkowników hello Everbridge platformy.</span><span class="sxs-lookup"><span data-stu-id="18ffa-214">Work with [EverBridge support team](mailto:support@everbridge.com) tooadd hello users in hello Everbridge platform.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="18ffa-215">Przypisanie użytkownika testowego hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="18ffa-215">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="18ffa-216">W tej sekcji możesz włączyć toouse Simona Britta Azure logowania jednokrotnego za udzielanie dostępu tooEverBridge.</span><span class="sxs-lookup"><span data-stu-id="18ffa-216">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooEverBridge.</span></span>

![Przypisz użytkownika][200] 

<span data-ttu-id="18ffa-218">**tooassign tooEverBridge Simona Britta wykonaj hello następujące kroki:**</span><span class="sxs-lookup"><span data-stu-id="18ffa-218">**tooassign Britta Simon tooEverBridge, perform hello following steps:**</span></span>

1. <span data-ttu-id="18ffa-219">W portalu Azure hello, otwórz widok aplikacji hello, a następnie przejdź do widoku katalogu toohello i przejść za**aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="18ffa-219">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Przypisz użytkownika][201] 

2. <span data-ttu-id="18ffa-221">Z listy aplikacji hello wybierz **EverBridge**.</span><span class="sxs-lookup"><span data-stu-id="18ffa-221">In hello applications list, select **EverBridge**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-everbridge-tutorial/tutorial_everbridge_app.png) 

3. <span data-ttu-id="18ffa-223">W menu powitania po lewej stronie powitania kliknij **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="18ffa-223">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Przypisz użytkownika][202] 

4. <span data-ttu-id="18ffa-225">Kliknij przycisk **Dodaj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="18ffa-225">Click **Add** button.</span></span> <span data-ttu-id="18ffa-226">Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="18ffa-226">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Przypisz użytkownika][203]

5. <span data-ttu-id="18ffa-228">Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** hello listy użytkowników.</span><span class="sxs-lookup"><span data-stu-id="18ffa-228">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="18ffa-229">Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="18ffa-229">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="18ffa-230">Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="18ffa-230">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="18ffa-231">Testowanie rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="18ffa-231">Testing single sign-on</span></span>

<span data-ttu-id="18ffa-232">Celem Hello w tej sekcji jest tootest użyciu usługi Azure AD konfiguracji rejestracji jednokrotnej hello panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="18ffa-232">hello objective of this section is tootest your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="18ffa-233">Po kliknięciu kafelka Everbridge hello w hello Panel dostępu, należy pobrać automatycznie zalogowane tooyour Everbridge aplikacji.</span><span class="sxs-lookup"><span data-stu-id="18ffa-233">When you click hello Everbridge tile in hello Access Panel, you should get automatically signed-on tooyour Everbridge application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="18ffa-234">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="18ffa-234">Additional resources</span></span>

* [<span data-ttu-id="18ffa-235">Lista samouczków dotyczących tooIntegrate aplikacji SaaS w usłudze Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="18ffa-235">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="18ffa-236">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="18ffa-236">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-everbridge-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-everbridge-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-everbridge-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-everbridge-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-everbridge-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-everbridge-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-everbridge-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-everbridge-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-everbridge-tutorial/tutorial_general_203.png

