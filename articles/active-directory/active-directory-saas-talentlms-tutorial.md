---
title: 'Samouczek: Integracji Azure Active Directory z TalentLMS | Dokumentacja firmy Microsoft'
description: "Dowiedz się, jak tooconfigure logowanie jednokrotne między usługą Azure Active Directory i TalentLMS."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: c903d20d-18e3-42b0-b997-6349c5412dde
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/13/2017
ms.author: jeedes
ms.openlocfilehash: 25538086602e58fbaab0fbf223f5b03908a74922
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-talentlms"></a><span data-ttu-id="47413-103">Samouczek: Integracji Azure Active Directory z TalentLMS</span><span class="sxs-lookup"><span data-stu-id="47413-103">Tutorial: Azure Active Directory integration with TalentLMS</span></span>

<span data-ttu-id="47413-104">Z tego samouczka, dowiesz się, jak toointegrate TalentLMS w usłudze Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="47413-104">In this tutorial, you learn how toointegrate TalentLMS with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="47413-105">Integracja z usługą Azure AD TalentLMS zapewnia hello następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="47413-105">Integrating TalentLMS with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="47413-106">Można kontrolować w usłudze Azure AD, kto ma dostęp do tooTalentLMS</span><span class="sxs-lookup"><span data-stu-id="47413-106">You can control in Azure AD who has access tooTalentLMS</span></span>
- <span data-ttu-id="47413-107">Można włączyć użytkownika użytkownicy tooautomatically get zalogowane tooTalentLMS (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="47413-107">You can enable your users tooautomatically get signed-on tooTalentLMS (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="47413-108">Możesz zarządzać kont w jednej centralnej lokalizacji - hello portalu Azure</span><span class="sxs-lookup"><span data-stu-id="47413-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="47413-109">Jeśli chcesz tooknow więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="47413-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="47413-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="47413-110">Prerequisites</span></span>

<span data-ttu-id="47413-111">tooconfigure integracji z usługą Azure AD z TalentLMS należy hello następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="47413-111">tooconfigure Azure AD integration with TalentLMS, you need hello following items:</span></span>

- <span data-ttu-id="47413-112">Subskrypcję usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="47413-112">An Azure AD subscription</span></span>
- <span data-ttu-id="47413-113">TalentLMS logowanie jednokrotne włączone subskrypcji</span><span class="sxs-lookup"><span data-stu-id="47413-113">A TalentLMS single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="47413-114">tootest hello kroków w tym samouczku, zaleca się przy użyciu środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="47413-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="47413-115">tootest hello kroki opisane w tym samouczku, należy stosować te zalecenia:</span><span class="sxs-lookup"><span data-stu-id="47413-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="47413-116">Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="47413-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="47413-117">Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz pobrać miesięczna wersja próbna tutaj: [oferta wersji próbnej](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="47413-117">If you don't have an Azure AD trial environment, you can get a one-month trial here: [Trial offer](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="47413-118">Opis scenariusza</span><span class="sxs-lookup"><span data-stu-id="47413-118">Scenario description</span></span>
<span data-ttu-id="47413-119">W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym.</span><span class="sxs-lookup"><span data-stu-id="47413-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="47413-120">Scenariusz Hello opisane w tym samouczku składa się z dwóch głównych elementów:</span><span class="sxs-lookup"><span data-stu-id="47413-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="47413-121">Dodawanie TalentLMS z galerii hello</span><span class="sxs-lookup"><span data-stu-id="47413-121">Adding TalentLMS from hello gallery</span></span>
2. <span data-ttu-id="47413-122">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="47413-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-talentlms-from-hello-gallery"></a><span data-ttu-id="47413-123">Dodawanie TalentLMS z galerii hello</span><span class="sxs-lookup"><span data-stu-id="47413-123">Adding TalentLMS from hello gallery</span></span>
<span data-ttu-id="47413-124">tooconfigure hello integracji TalentLMS do usługi Azure AD, należy tooadd TalentLMS z hello galerii tooyour listę zarządzanych aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="47413-124">tooconfigure hello integration of TalentLMS into Azure AD, you need tooadd TalentLMS from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="47413-125">**tooadd TalentLMS z galerii hello, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="47413-125">**tooadd TalentLMS from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="47413-126">W hello  **[portalu Azure](https://portal.azure.com)**na temat hello panelu nawigacji po lewej stronie, kliknij przycisk **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="47413-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Usługa Active Directory][1]

2. <span data-ttu-id="47413-128">Przejdź za**aplikacje dla przedsiębiorstw**.</span><span class="sxs-lookup"><span data-stu-id="47413-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="47413-129">Następnie przejdź zbyt**wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="47413-129">Then go too**All applications**.</span></span>

    ![Aplikacje][2]
    
3. <span data-ttu-id="47413-131">tooadd nową aplikację, kliknij przycisk **nowej aplikacji** przycisk u góry hello okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="47413-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplikacje][3]

4. <span data-ttu-id="47413-133">W polu wyszukiwania hello wpisz **TalentLMS**.</span><span class="sxs-lookup"><span data-stu-id="47413-133">In hello search box, type **TalentLMS**.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-talentlms-tutorial/tutorial_talentlms_search.png)

5. <span data-ttu-id="47413-135">W panelu wyników hello zaznacz **TalentLMS**, a następnie kliknij przycisk **Dodaj** przycisk aplikacji hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="47413-135">In hello results panel, select **TalentLMS**, and then click **Add** button tooadd hello application.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-talentlms-tutorial/tutorial_talentlms_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="47413-137">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="47413-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="47413-138">W tej sekcji możesz skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z TalentLMS na podstawie użytkownika testowego, nazywany "Britta Simona".</span><span class="sxs-lookup"><span data-stu-id="47413-138">In this section, you configure and test Azure AD single sign-on with TalentLMS based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="47413-139">Dla pojedynczego logowania jednokrotnego toowork usługi Azure AD musi tooknow użytkownika odpowiednikiem hello w TalentLMS jest tooa użytkownika w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="47413-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in TalentLMS is tooa user in Azure AD.</span></span> <span data-ttu-id="47413-140">Innymi słowy relację łącza między użytkownika usługi Azure AD i hello użytkownikowi w TalentLMS musi toobe ustanowione.</span><span class="sxs-lookup"><span data-stu-id="47413-140">In other words, a link relationship between an Azure AD user and hello related user in TalentLMS needs toobe established.</span></span>

<span data-ttu-id="47413-141">W TalentLMS, należy przypisać wartość hello hello **nazwy użytkownika** w usłudze Azure AD jako wartość hello hello **Username** tooestablish hello łącze relacji.</span><span class="sxs-lookup"><span data-stu-id="47413-141">In TalentLMS, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="47413-142">tooconfigure i testowych usługi Azure AD rejestracji jednokrotnej z TalentLMS, należy po bloków konstrukcyjnych hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="47413-142">tooconfigure and test Azure AD single sign-on with TalentLMS, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="47413-143">**[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configuring-azure-ad-single-sign-on)**  -tooenable Twojego toouse użytkowników tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="47413-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="47413-144">**[Tworzenie użytkownika testowego usługi Azure AD](#creating-an-azure-ad-test-user)**  -tootest usługi Azure AD rejestracji jednokrotnej z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="47413-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="47413-145">**[Tworzenie użytkownika testowego TalentLMS](#creating-a-talentlms-test-user)**  -toohave odpowiednikiem Simona Britta w TalentLMS, który jest połączony toohello usługi Azure AD reprezentację użytkownika.</span><span class="sxs-lookup"><span data-stu-id="47413-145">**[Creating a TalentLMS test user](#creating-a-talentlms-test-user)** - toohave a counterpart of Britta Simon in TalentLMS that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="47413-146">**[Przypisanie użytkownika testowego hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Simona Britta toouse usługi Azure AD rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="47413-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="47413-147">**[Testowanie rejestracji jednokrotnej](#testing-single-sign-on)**  -tooverify czy hello konfiguracji działania.</span><span class="sxs-lookup"><span data-stu-id="47413-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="47413-148">Konfigurowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="47413-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="47413-149">W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w portalu Azure hello i skonfigurować logowanie jednokrotne w aplikacji TalentLMS.</span><span class="sxs-lookup"><span data-stu-id="47413-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your TalentLMS application.</span></span>

<span data-ttu-id="47413-150">**tooconfigure usługi Azure AD rejestracji jednokrotnej z TalentLMS, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="47413-150">**tooconfigure Azure AD single sign-on with TalentLMS, perform hello following steps:**</span></span>

1. <span data-ttu-id="47413-151">W portalu Azure na powitania hello **TalentLMS** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.</span><span class="sxs-lookup"><span data-stu-id="47413-151">In hello Azure portal, on hello **TalentLMS** application integration page, click **Single sign-on**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej][4]

2. <span data-ttu-id="47413-153">Na powitania **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** tooenable rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="47413-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-talentlms-tutorial/tutorial_talentlms_samlbase.png)

3. <span data-ttu-id="47413-155">Na powitania **TalentLMS domeny i adres URL** sekcji, wykonaj następujące kroki hello:</span><span class="sxs-lookup"><span data-stu-id="47413-155">On hello **TalentLMS Domain and URLs** section, perform hello following steps:</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-talentlms-tutorial/tutorial_talentlms_url.png)

    <span data-ttu-id="47413-157">a.</span><span class="sxs-lookup"><span data-stu-id="47413-157">a.</span></span> <span data-ttu-id="47413-158">W hello **adres URL logowania** tekstowym, wpisz adres URL za pomocą hello następującego wzorca:`https://<tenant-name>.TalentLMSapp.com`</span><span class="sxs-lookup"><span data-stu-id="47413-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<tenant-name>.TalentLMSapp.com`</span></span>

    <span data-ttu-id="47413-159">b.</span><span class="sxs-lookup"><span data-stu-id="47413-159">b.</span></span> <span data-ttu-id="47413-160">W hello **identyfikator** tekstowym, wpisz adres URL za pomocą hello następującego wzorca:`http://<tenant-name>.talentlms.com`</span><span class="sxs-lookup"><span data-stu-id="47413-160">In hello **Identifier** textbox, type a URL using hello following pattern: `http://<tenant-name>.talentlms.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="47413-161">Wartości te nie są prawdziwe.</span><span class="sxs-lookup"><span data-stu-id="47413-161">These values are not real.</span></span> <span data-ttu-id="47413-162">Zaktualizować te wartości z hello rzeczywisty adres URL logowania i identyfikator.</span><span class="sxs-lookup"><span data-stu-id="47413-162">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="47413-163">Skontaktuj się z [zespołem pomocy technicznej klienta TalentLMS](https://www.talentlms.com/contact) tooget tych wartości.</span><span class="sxs-lookup"><span data-stu-id="47413-163">Contact [TalentLMS Client support team](https://www.talentlms.com/contact) tooget these values.</span></span> 
 
4. <span data-ttu-id="47413-164">Na powitania **certyfikat podpisywania SAML** hello kopiowania, sekcji **odcisk PALCA** wartość z zakresu od hello certyfikatu.</span><span class="sxs-lookup"><span data-stu-id="47413-164">On hello **SAML Signing Certificate** section, copy hello **THUMBPRINT** value from hello certificate.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-talentlms-tutorial/tutorial_talentlms_certificate.png) 

5. <span data-ttu-id="47413-166">Kliknij przycisk **zapisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="47413-166">Click **Save** button.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-talentlms-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="47413-168">Na powitania **konfiguracji TalentLMS** kliknij **skonfigurować TalentLMS** tooopen **Konfigurowanie logowania jednokrotnego** okna.</span><span class="sxs-lookup"><span data-stu-id="47413-168">On hello **TalentLMS Configuration** section, click **Configure TalentLMS** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="47413-169">Kopiuj hello **Sign-Out adres URL, identyfikator jednostki SAML i SAML pojedynczy znak na adres URL usługi** z hello **sekcji krótkimi opisami.**</span><span class="sxs-lookup"><span data-stu-id="47413-169">Copy hello **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-talentlms-tutorial/tutorial_talentlms_configure.png)  

7. <span data-ttu-id="47413-171">W oknie przeglądarki innej witryny sieci web Zaloguj się w witrynie firmy TalentLMS tooyour jako administrator.</span><span class="sxs-lookup"><span data-stu-id="47413-171">In a different web browser window, log in tooyour TalentLMS company site as an administrator.</span></span>

8. <span data-ttu-id="47413-172">W hello **& Ustawienia konta** kliknij hello **użytkowników** kartę.</span><span class="sxs-lookup"><span data-stu-id="47413-172">In hello **Account & Settings** section, click hello **Users** tab.</span></span>
   
    <span data-ttu-id="47413-173">![& Ustawienia konta](./media/active-directory-saas-talentlms-tutorial/IC777296.png "& Ustawienia konta")</span><span class="sxs-lookup"><span data-stu-id="47413-173">![Account & Settings](./media/active-directory-saas-talentlms-tutorial/IC777296.png "Account & Settings")</span></span>

9. <span data-ttu-id="47413-174">Kliknij przycisk **logowanie jednokrotne (SSO)**,</span><span class="sxs-lookup"><span data-stu-id="47413-174">Click **Single Sign-On (SSO)**,</span></span>

10. <span data-ttu-id="47413-175">W hello sekcji rejestracji jednokrotnej wykonaj hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="47413-175">In hello Single Sign-On section, perform hello following steps:</span></span>
   
    <span data-ttu-id="47413-176">![Logowanie jednokrotne](./media/active-directory-saas-talentlms-tutorial/IC777297.png "logowanie jednokrotne")</span><span class="sxs-lookup"><span data-stu-id="47413-176">![Single Sign-On](./media/active-directory-saas-talentlms-tutorial/IC777297.png "Single Sign-On")</span></span>   

    <span data-ttu-id="47413-177">a.</span><span class="sxs-lookup"><span data-stu-id="47413-177">a.</span></span> <span data-ttu-id="47413-178">Z hello **Typ integracji logowania jednokrotnego** listy, wybierz **SAML 2.0**.</span><span class="sxs-lookup"><span data-stu-id="47413-178">From hello **SSO integration type** list, select **SAML 2.0**.</span></span>

    <span data-ttu-id="47413-179">b.</span><span class="sxs-lookup"><span data-stu-id="47413-179">b.</span></span> <span data-ttu-id="47413-180">W hello **dostawcy tożsamości (IDP)** pole tekstowe, Wklej wartość hello **identyfikator jednostki SAML**, które zostały skopiowane z portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="47413-180">In hello **Identity provider (IDP)** textbox, paste hello value of **SAML Entity ID**, which you have copied from Azure portal.</span></span>
 
    <span data-ttu-id="47413-181">c.</span><span class="sxs-lookup"><span data-stu-id="47413-181">c.</span></span> <span data-ttu-id="47413-182">Wklej hello **odcisk palca** wartość z portalu Azure do hello **odcisk palca certyfikatu** pola tekstowego.</span><span class="sxs-lookup"><span data-stu-id="47413-182">Paste hello **Thumbprint** value from Azure portal into hello **Certificate fingerprint** textbox.</span></span>    

    <span data-ttu-id="47413-183">d.</span><span class="sxs-lookup"><span data-stu-id="47413-183">d.</span></span>  <span data-ttu-id="47413-184">W hello **zdalnego logowania adresu URL** pole tekstowe, Wklej wartość hello **SAML pojedynczy znak na adres URL usługi**, które zostały skopiowane z portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="47413-184">In hello **Remote sign-in URL** textbox, paste hello value of **SAML Single Sign-On Service URL**, which you have copied from Azure portal.</span></span>
 
    <span data-ttu-id="47413-185">e.</span><span class="sxs-lookup"><span data-stu-id="47413-185">e.</span></span> <span data-ttu-id="47413-186">W hello **zdalnego adresu URL wylogowania** pole tekstowe, Wklej wartość hello **Sign-Out URL**, które zostały skopiowane z portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="47413-186">In hello **Remote sign-out URL** textbox, paste hello value of **Sign-Out URL**, which you have copied from Azure portal.</span></span>

    <span data-ttu-id="47413-187">f.</span><span class="sxs-lookup"><span data-stu-id="47413-187">f.</span></span> <span data-ttu-id="47413-188">Wypełnij następujące hello:</span><span class="sxs-lookup"><span data-stu-id="47413-188">Fill in hello following:</span></span> 

    * <span data-ttu-id="47413-189">W hello **TargetedID** pole tekstowe, typ`http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name`</span><span class="sxs-lookup"><span data-stu-id="47413-189">In hello **TargetedID** textbox, type `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name`</span></span>
     
    * <span data-ttu-id="47413-190">W hello **imię** pole tekstowe, typ`http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname`</span><span class="sxs-lookup"><span data-stu-id="47413-190">In hello **First name** textbox, type `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname`</span></span>
    
    * <span data-ttu-id="47413-191">W hello **nazwisko** pole tekstowe, typ`http://schemas.xmlsoap.org/ws/2005/05/identity/claims/surname`</span><span class="sxs-lookup"><span data-stu-id="47413-191">In hello **Last name** textbox, type `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/surname`</span></span>
    
    * <span data-ttu-id="47413-192">W hello **E-mail** pole tekstowe, typ`http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress`</span><span class="sxs-lookup"><span data-stu-id="47413-192">In hello **Email** textbox, type `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress`</span></span>
    
11. <span data-ttu-id="47413-193">Kliknij pozycję **Zapisz**.</span><span class="sxs-lookup"><span data-stu-id="47413-193">Click **Save**.</span></span>
 
> [!TIP]
> <span data-ttu-id="47413-194">Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz hello [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji hello!</span><span class="sxs-lookup"><span data-stu-id="47413-194">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="47413-195">Po dodaniu tej aplikacji z hello **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij hello **rejestracji jednokrotnej** hello kartę i dostępu do osadzonych dokumentacji za pośrednictwem hello  **Konfiguracja** sekcji u dołu hello.</span><span class="sxs-lookup"><span data-stu-id="47413-195">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="47413-196">Więcej o hello osadzonych dokumentacji funkcji w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="47413-196">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="47413-197">Tworzenie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="47413-197">Creating an Azure AD test user</span></span>
<span data-ttu-id="47413-198">Celem Hello w tej sekcji jest toocreate użytkownika testowego, w portalu Azure o nazwie Simona Britta hello.</span><span class="sxs-lookup"><span data-stu-id="47413-198">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Tworzenie użytkowników usługi Azure AD][100]

<span data-ttu-id="47413-200">**toocreate użytkownika testowego w usłudze Azure AD, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="47413-200">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="47413-201">W hello **portalu Azure**na temat hello w lewym okienku nawigacji, kliknij przycisk **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="47413-201">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-talentlms-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="47413-203">toodisplay hello listę użytkowników, przejdź zbyt**użytkowników i grup** i kliknij przycisk **wszyscy użytkownicy**.</span><span class="sxs-lookup"><span data-stu-id="47413-203">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-talentlms-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="47413-205">Witaj tooopen **użytkownika** okna dialogowego, kliknij przycisk **Dodaj** u góry hello hello okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="47413-205">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-talentlms-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="47413-207">Na powitania **użytkownika** okna dialogowego wykonaj hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="47413-207">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-talentlms-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="47413-209">a.</span><span class="sxs-lookup"><span data-stu-id="47413-209">a.</span></span> <span data-ttu-id="47413-210">W hello **nazwa** pole tekstowe, typ **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="47413-210">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="47413-211">b.</span><span class="sxs-lookup"><span data-stu-id="47413-211">b.</span></span> <span data-ttu-id="47413-212">W hello **nazwy użytkownika** pole tekstowe, hello typu **adres e-mail** z BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="47413-212">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="47413-213">c.</span><span class="sxs-lookup"><span data-stu-id="47413-213">c.</span></span> <span data-ttu-id="47413-214">Wybierz **Pokaż hasło** i zanotuj wartość hello hello **hasło**.</span><span class="sxs-lookup"><span data-stu-id="47413-214">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="47413-215">d.</span><span class="sxs-lookup"><span data-stu-id="47413-215">d.</span></span> <span data-ttu-id="47413-216">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="47413-216">Click **Create**.</span></span>
 
### <a name="creating-a-talentlms-test-user"></a><span data-ttu-id="47413-217">Tworzenie użytkownika testowego TalentLMS</span><span class="sxs-lookup"><span data-stu-id="47413-217">Creating a TalentLMS test user</span></span>

<span data-ttu-id="47413-218">toolog użytkowników tooenable usługi Azure AD w tooTalentLMS, muszą mieć przydzielone do TalentLMS.</span><span class="sxs-lookup"><span data-stu-id="47413-218">tooenable Azure AD users toolog in tooTalentLMS, they must be provisioned into TalentLMS.</span></span> <span data-ttu-id="47413-219">W przypadku hello TalentLMS Inicjowanie obsługi to zadanie ręczne.</span><span class="sxs-lookup"><span data-stu-id="47413-219">In hello case of TalentLMS, provisioning is a manual task.</span></span>

<span data-ttu-id="47413-220">**tooprovision konta użytkownika, należy wykonać hello następujące kroki:**</span><span class="sxs-lookup"><span data-stu-id="47413-220">**tooprovision a user account, perform hello following steps:**</span></span>

1. <span data-ttu-id="47413-221">Zaloguj się za tooyour **TalentLMS** dzierżawy.</span><span class="sxs-lookup"><span data-stu-id="47413-221">Log in tooyour **TalentLMS** tenant.</span></span>

2. <span data-ttu-id="47413-222">Kliknij przycisk **użytkowników**, a następnie kliknij przycisk **Dodaj użytkownika**.</span><span class="sxs-lookup"><span data-stu-id="47413-222">Click **Users**, and then click **Add User**.</span></span>

3. <span data-ttu-id="47413-223">Na powitania **Dodaj użytkownika** okna dialogowego wykonaj hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="47413-223">On hello **Add user** dialog page, perform hello following steps:</span></span>
   
    <span data-ttu-id="47413-224">![Dodaj użytkownika](./media/active-directory-saas-talentlms-tutorial/IC777299.png "Dodaj użytkownika")</span><span class="sxs-lookup"><span data-stu-id="47413-224">![Add User](./media/active-directory-saas-talentlms-tutorial/IC777299.png "Add User")</span></span>  

    <span data-ttu-id="47413-225">a.</span><span class="sxs-lookup"><span data-stu-id="47413-225">a.</span></span> <span data-ttu-id="47413-226">W hello **imię** pole tekstowe, wprowadź hello imię użytkownika, takich jak **Britta**.</span><span class="sxs-lookup"><span data-stu-id="47413-226">In hello **First name** textbox, enter hello first name of user like **Britta**.</span></span>

    <span data-ttu-id="47413-227">b.</span><span class="sxs-lookup"><span data-stu-id="47413-227">b.</span></span> <span data-ttu-id="47413-228">W hello **nazwisko** pole tekstowe, wprowadź hello nazwisko użytkownika, takich jak **Simona**.</span><span class="sxs-lookup"><span data-stu-id="47413-228">In hello **Last name** textbox, enter hello last name of user like **Simon**.</span></span>
 
    <span data-ttu-id="47413-229">c.</span><span class="sxs-lookup"><span data-stu-id="47413-229">c.</span></span> <span data-ttu-id="47413-230">W hello **adres E-mail** pole tekstowe, wprowadź adres e-mail użytkownika, takie jak hello  **brittasimon@contoso.com** .</span><span class="sxs-lookup"><span data-stu-id="47413-230">In hello **Email address** textbox, enter hello email of user like **brittasimon@contoso.com**.</span></span>

    <span data-ttu-id="47413-231">d.</span><span class="sxs-lookup"><span data-stu-id="47413-231">d.</span></span> <span data-ttu-id="47413-232">Kliknij przycisk **dodać użytkownika**.</span><span class="sxs-lookup"><span data-stu-id="47413-232">Click **Add User**.</span></span>

>[!NOTE]
><span data-ttu-id="47413-233">Możesz użyć innych TalentLMS użytkownika konta tworzenia narzędzi lub interfejsów API dostarczonych przez TalentLMS tooprovision kont użytkowników usługi AAD.</span><span class="sxs-lookup"><span data-stu-id="47413-233">You can use any other TalentLMS user account creation tools or APIs provided by TalentLMS tooprovision AAD user accounts.</span></span>
 

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="47413-234">Przypisanie użytkownika testowego hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="47413-234">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="47413-235">W tej sekcji możesz włączyć toouse Simona Britta Azure logowania jednokrotnego za udzielanie dostępu tooTalentLMS.</span><span class="sxs-lookup"><span data-stu-id="47413-235">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooTalentLMS.</span></span>

![Przypisz użytkownika][200] 

<span data-ttu-id="47413-237">**tooassign tooTalentLMS Simona Britta wykonaj hello następujące kroki:**</span><span class="sxs-lookup"><span data-stu-id="47413-237">**tooassign Britta Simon tooTalentLMS, perform hello following steps:**</span></span>

1. <span data-ttu-id="47413-238">W portalu Azure hello, otwórz widok aplikacji hello, a następnie przejdź do widoku katalogu toohello i przejść za**aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="47413-238">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Przypisz użytkownika][201] 

2. <span data-ttu-id="47413-240">Z listy aplikacji hello wybierz **TalentLMS**.</span><span class="sxs-lookup"><span data-stu-id="47413-240">In hello applications list, select **TalentLMS**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-talentlms-tutorial/tutorial_talentlms_app.png) 

3. <span data-ttu-id="47413-242">W menu powitania po lewej stronie powitania kliknij **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="47413-242">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Przypisz użytkownika][202] 

4. <span data-ttu-id="47413-244">Kliknij przycisk **Dodaj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="47413-244">Click **Add** button.</span></span> <span data-ttu-id="47413-245">Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="47413-245">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Przypisz użytkownika][203]

5. <span data-ttu-id="47413-247">Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** hello listy użytkowników.</span><span class="sxs-lookup"><span data-stu-id="47413-247">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="47413-248">Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="47413-248">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="47413-249">Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="47413-249">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="47413-250">Testowanie rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="47413-250">Testing single sign-on</span></span>

<span data-ttu-id="47413-251">Celem Hello w tej sekcji jest tootest użyciu usługi Azure AD konfiguracji rejestracji jednokrotnej hello panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="47413-251">hello objective of this section is tootest your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="47413-252">Po kliknięciu powitalne TalentLMS kafelka w hello Panel dostępu, należy pobrać automatycznie zalogowane tooyour TalentLMS aplikacji</span><span class="sxs-lookup"><span data-stu-id="47413-252">When you click hello TalentLMS tile in hello Access Panel, you should get automatically signed-on tooyour TalentLMS application</span></span>

## <a name="additional-resources"></a><span data-ttu-id="47413-253">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="47413-253">Additional resources</span></span>

* [<span data-ttu-id="47413-254">Lista samouczków dotyczących tooIntegrate aplikacji SaaS w usłudze Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="47413-254">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="47413-255">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="47413-255">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-talentlms-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-talentlms-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-talentlms-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-talentlms-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-talentlms-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-talentlms-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-talentlms-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-talentlms-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-talentlms-tutorial/tutorial_general_203.png

