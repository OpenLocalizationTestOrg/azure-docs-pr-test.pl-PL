---
title: 'Samouczek: Integracji Azure Active Directory z SumoLogic | Dokumentacja firmy Microsoft'
description: "Dowiedz się, jak tooconfigure logowanie jednokrotne między usługą Azure Active Directory i SumoLogic."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: fbb76765-92d7-4801-9833-573b11b4d910
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/08/2017
ms.author: jeedes
ms.openlocfilehash: 2ef1bd329f5db8899f0b57744e4c0f6eed1c532f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-sumologic"></a><span data-ttu-id="6b52c-103">Samouczek: Integracji Azure Active Directory z SumoLogic</span><span class="sxs-lookup"><span data-stu-id="6b52c-103">Tutorial: Azure Active Directory integration with SumoLogic</span></span>

<span data-ttu-id="6b52c-104">Z tego samouczka, dowiesz się, jak toointegrate SumoLogic w usłudze Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="6b52c-104">In this tutorial, you learn how toointegrate SumoLogic with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="6b52c-105">Integracja z usługą Azure AD SumoLogic zapewnia hello następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="6b52c-105">Integrating SumoLogic with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="6b52c-106">Można kontrolować w usłudze Azure AD, kto ma dostęp do tooSumoLogic</span><span class="sxs-lookup"><span data-stu-id="6b52c-106">You can control in Azure AD who has access tooSumoLogic</span></span>
- <span data-ttu-id="6b52c-107">Można włączyć użytkownika użytkownicy tooautomatically get zalogowane tooSumoLogic (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="6b52c-107">You can enable your users tooautomatically get signed-on tooSumoLogic (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="6b52c-108">Możesz zarządzać kont w jednej centralnej lokalizacji - hello portalu Azure</span><span class="sxs-lookup"><span data-stu-id="6b52c-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="6b52c-109">Jeśli chcesz tooknow więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="6b52c-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="6b52c-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="6b52c-110">Prerequisites</span></span>

<span data-ttu-id="6b52c-111">tooconfigure integracji z usługą Azure AD z SumoLogic należy hello następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="6b52c-111">tooconfigure Azure AD integration with SumoLogic, you need hello following items:</span></span>

- <span data-ttu-id="6b52c-112">Subskrypcję usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="6b52c-112">An Azure AD subscription</span></span>
- <span data-ttu-id="6b52c-113">SumoLogic logowanie jednokrotne włączone subskrypcji</span><span class="sxs-lookup"><span data-stu-id="6b52c-113">A SumoLogic single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="6b52c-114">tootest hello kroków w tym samouczku, zaleca się przy użyciu środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="6b52c-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="6b52c-115">tootest hello kroki opisane w tym samouczku, należy stosować te zalecenia:</span><span class="sxs-lookup"><span data-stu-id="6b52c-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="6b52c-116">Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="6b52c-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="6b52c-117">Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz pobrać miesięczna wersja próbna [tutaj](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="6b52c-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="6b52c-118">Opis scenariusza</span><span class="sxs-lookup"><span data-stu-id="6b52c-118">Scenario description</span></span>
<span data-ttu-id="6b52c-119">W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym.</span><span class="sxs-lookup"><span data-stu-id="6b52c-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="6b52c-120">Scenariusz Hello opisane w tym samouczku składa się z dwóch głównych elementów:</span><span class="sxs-lookup"><span data-stu-id="6b52c-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="6b52c-121">Dodawanie SumoLogic z galerii hello</span><span class="sxs-lookup"><span data-stu-id="6b52c-121">Adding SumoLogic from hello gallery</span></span>
2. <span data-ttu-id="6b52c-122">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="6b52c-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-sumologic-from-hello-gallery"></a><span data-ttu-id="6b52c-123">Dodawanie SumoLogic z galerii hello</span><span class="sxs-lookup"><span data-stu-id="6b52c-123">Adding SumoLogic from hello gallery</span></span>
<span data-ttu-id="6b52c-124">tooconfigure hello integracji SumoLogic do usługi Azure AD, należy tooadd SumoLogic z hello galerii tooyour listę zarządzanych aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="6b52c-124">tooconfigure hello integration of SumoLogic into Azure AD, you need tooadd SumoLogic from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="6b52c-125">**tooadd SumoLogic z galerii hello, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="6b52c-125">**tooadd SumoLogic from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="6b52c-126">W hello  **[portalu Azure](https://portal.azure.com)**na temat hello panelu nawigacji po lewej stronie, kliknij przycisk **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="6b52c-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Usługa Active Directory][1]

2. <span data-ttu-id="6b52c-128">Przejdź za**aplikacje dla przedsiębiorstw**.</span><span class="sxs-lookup"><span data-stu-id="6b52c-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="6b52c-129">Następnie przejdź zbyt**wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="6b52c-129">Then go too**All applications**.</span></span>

    ![Aplikacje][2]
    
3. <span data-ttu-id="6b52c-131">tooadd nową aplikację, kliknij przycisk **nowej aplikacji** przycisk u góry hello okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="6b52c-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplikacje][3]

4. <span data-ttu-id="6b52c-133">W polu wyszukiwania hello wpisz **SumoLogic**.</span><span class="sxs-lookup"><span data-stu-id="6b52c-133">In hello search box, type **SumoLogic**.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-sumologic-tutorial/tutorial_sumologic_search.png)

5. <span data-ttu-id="6b52c-135">W panelu wyników hello zaznacz **SumoLogic**, a następnie kliknij przycisk **Dodaj** przycisk aplikacji hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="6b52c-135">In hello results panel, select **SumoLogic**, and then click **Add** button tooadd hello application.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-sumologic-tutorial/tutorial_sumologic_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="6b52c-137">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="6b52c-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="6b52c-138">W tej sekcji skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z SumoLogic w oparciu o nazwie "Britta Simona" użytkownika testowego.</span><span class="sxs-lookup"><span data-stu-id="6b52c-138">In this section, you configure and test Azure AD single sign-on with SumoLogic based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="6b52c-139">Dla pojedynczego logowania jednokrotnego toowork usługi Azure AD musi tooknow użytkownika odpowiednikiem hello w SumoLogic jest tooa użytkownika w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="6b52c-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in SumoLogic is tooa user in Azure AD.</span></span> <span data-ttu-id="6b52c-140">Innymi słowy relację łącza między użytkownika usługi Azure AD i hello użytkownikowi w SumoLogic musi toobe ustanowione.</span><span class="sxs-lookup"><span data-stu-id="6b52c-140">In other words, a link relationship between an Azure AD user and hello related user in SumoLogic needs toobe established.</span></span>

<span data-ttu-id="6b52c-141">W SumoLogic, należy przypisać wartość hello hello **nazwy użytkownika** w usłudze Azure AD jako wartość hello hello **Username** tooestablish hello łącze relacji.</span><span class="sxs-lookup"><span data-stu-id="6b52c-141">In SumoLogic, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="6b52c-142">tooconfigure i testowych usługi Azure AD rejestracji jednokrotnej z SumoLogic, należy po bloków konstrukcyjnych hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="6b52c-142">tooconfigure and test Azure AD single sign-on with SumoLogic, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="6b52c-143">**[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configuring-azure-ad-single-sign-on)**  -tooenable Twojego toouse użytkowników tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="6b52c-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="6b52c-144">**[Tworzenie użytkownika testowego usługi Azure AD](#creating-an-azure-ad-test-user)**  -tootest usługi Azure AD rejestracji jednokrotnej z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="6b52c-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="6b52c-145">**[Tworzenie użytkownika testowego SumoLogic](#creating-a-sumologic-test-user)**  -toohave odpowiednikiem Simona Britta w SumoLogic, który jest połączony toohello usługi Azure AD reprezentację użytkownika.</span><span class="sxs-lookup"><span data-stu-id="6b52c-145">**[Creating a SumoLogic test user](#creating-a-sumologic-test-user)** - toohave a counterpart of Britta Simon in SumoLogic that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="6b52c-146">**[Przypisanie użytkownika testowego hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Simona Britta toouse usługi Azure AD rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="6b52c-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="6b52c-147">**[Testowanie rejestracji jednokrotnej](#testing-single-sign-on)**  -tooverify czy hello konfiguracji działania.</span><span class="sxs-lookup"><span data-stu-id="6b52c-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="6b52c-148">Konfigurowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="6b52c-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="6b52c-149">W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w portalu Azure hello i skonfigurować logowanie jednokrotne w aplikacji SumoLogic.</span><span class="sxs-lookup"><span data-stu-id="6b52c-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your SumoLogic application.</span></span>

<span data-ttu-id="6b52c-150">**tooconfigure usługi Azure AD rejestracji jednokrotnej z SumoLogic, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="6b52c-150">**tooconfigure Azure AD single sign-on with SumoLogic, perform hello following steps:**</span></span>

1. <span data-ttu-id="6b52c-151">W portalu Azure na powitania hello **SumoLogic** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.</span><span class="sxs-lookup"><span data-stu-id="6b52c-151">In hello Azure portal, on hello **SumoLogic** application integration page, click **Single sign-on**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej][4]

2. <span data-ttu-id="6b52c-153">Na powitania **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** tooenable rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="6b52c-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-sumologic-tutorial/tutorial_sumologic_samlbase.png)

3. <span data-ttu-id="6b52c-155">Na powitania **SumoLogic domeny i adres URL** sekcji, wykonaj następujące kroki hello:</span><span class="sxs-lookup"><span data-stu-id="6b52c-155">On hello **SumoLogic Domain and URLs** section, perform hello following steps:</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-sumologic-tutorial/tutorial_sumologic_url.png)

    <span data-ttu-id="6b52c-157">a.</span><span class="sxs-lookup"><span data-stu-id="6b52c-157">a.</span></span> <span data-ttu-id="6b52c-158">W hello **adres URL logowania** tekstowym, wpisz adres URL za pomocą hello następującego wzorca:`https://<tenantname>.SumoLogic.com`</span><span class="sxs-lookup"><span data-stu-id="6b52c-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<tenantname>.SumoLogic.com`</span></span>

    <span data-ttu-id="6b52c-159">b.</span><span class="sxs-lookup"><span data-stu-id="6b52c-159">b.</span></span> <span data-ttu-id="6b52c-160">W hello **identyfikator** tekstowym, wpisz adres URL za pomocą hello następującego wzorca:</span><span class="sxs-lookup"><span data-stu-id="6b52c-160">In hello **Identifier** textbox, type a URL using hello following pattern:</span></span>
    | |
    |--|
    | `https://<tenantname>.us2.sumologic.com` |
    | `https://<tenantname>.sumologic.com` |
    | `https://<tenantname>.us4.sumologic.com` |
    | `https://<tenantname>.eu.sumologic.com` |
    | `https://<tenantname>.au.sumologic.com` |

    > [!NOTE] 
    > <span data-ttu-id="6b52c-161">Wartości te nie są prawdziwe.</span><span class="sxs-lookup"><span data-stu-id="6b52c-161">These values are not real.</span></span> <span data-ttu-id="6b52c-162">Zaktualizować te wartości z hello rzeczywisty adres URL logowania i identyfikator.</span><span class="sxs-lookup"><span data-stu-id="6b52c-162">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="6b52c-163">Skontaktuj się z [zespołem pomocy technicznej klienta SumoLogic](https://www.sumologic.com/contact-us/) tooget tych wartości.</span><span class="sxs-lookup"><span data-stu-id="6b52c-163">Contact [SumoLogic Client support team](https://www.sumologic.com/contact-us/) tooget these values.</span></span> 
 
4. <span data-ttu-id="6b52c-164">Na powitania **certyfikat podpisywania SAML** kliknij **certyfikatu (Base64)** , a następnie zapisz plik certyfikatu hello na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="6b52c-164">On hello **SAML Signing Certificate** section, click **Certificate (Base64)** and then save hello certificate file on your computer.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-sumologic-tutorial/tutorial_sumologic_certificate.png) 

5. <span data-ttu-id="6b52c-166">Kliknij przycisk **zapisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="6b52c-166">Click **Save** button.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-sumologic-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="6b52c-168">Na powitania **konfiguracji SumoLogic** kliknij **skonfigurować SumoLogic** tooopen **Konfigurowanie logowania jednokrotnego** okna.</span><span class="sxs-lookup"><span data-stu-id="6b52c-168">On hello **SumoLogic Configuration** section, click **Configure SumoLogic** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="6b52c-169">Kopiuj hello **identyfikator jednostki SAML i SAML pojedynczy znak na adres URL usługi** z hello **sekcji krótkimi opisami.**</span><span class="sxs-lookup"><span data-stu-id="6b52c-169">Copy hello **SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-sumologic-tutorial/tutorial_sumologic_configure.png) 

7. <span data-ttu-id="6b52c-171">W oknie przeglądarki innej witryny sieci web Zaloguj się w witrynie firmy SumoLogic tooyour jako administrator.</span><span class="sxs-lookup"><span data-stu-id="6b52c-171">In a different web browser window, log in tooyour SumoLogic company site as an administrator.</span></span>

8. <span data-ttu-id="6b52c-172">Przejdź za**Zarządzaj \> zabezpieczeń**.</span><span class="sxs-lookup"><span data-stu-id="6b52c-172">Go too**Manage \> Security**.</span></span>
   
    <span data-ttu-id="6b52c-173">![Zarządzanie](./media/active-directory-saas-sumologic-tutorial/ic778556.png "zarządzania")</span><span class="sxs-lookup"><span data-stu-id="6b52c-173">![Manage](./media/active-directory-saas-sumologic-tutorial/ic778556.png "Manage")</span></span>

9. <span data-ttu-id="6b52c-174">Kliknij przycisk **SAML**.</span><span class="sxs-lookup"><span data-stu-id="6b52c-174">Click **SAML**.</span></span>
   
    <span data-ttu-id="6b52c-175">![Ustawienia zabezpieczeń globalnych](./media/active-directory-saas-sumologic-tutorial/ic778557.png "ustawienia zabezpieczeń globalnych")</span><span class="sxs-lookup"><span data-stu-id="6b52c-175">![Global security settings](./media/active-directory-saas-sumologic-tutorial/ic778557.png "Global security settings")</span></span>

10. <span data-ttu-id="6b52c-176">Z hello **wybierz konfigurację lub Utwórz nową** wybierz **usługi Azure AD**, a następnie kliknij przycisk **Konfiguruj**.</span><span class="sxs-lookup"><span data-stu-id="6b52c-176">From hello **Select a configuration or create a new one** list, select **Azure AD**, and then click **Configure**.</span></span>
   
    <span data-ttu-id="6b52c-177">![Skonfigurować SAML 2.0](./media/active-directory-saas-sumologic-tutorial/ic778558.png "skonfigurować SAML 2.0")</span><span class="sxs-lookup"><span data-stu-id="6b52c-177">![Configure SAML 2.0](./media/active-directory-saas-sumologic-tutorial/ic778558.png "Configure SAML 2.0")</span></span>

11. <span data-ttu-id="6b52c-178">Na powitania **skonfigurować SAML 2.0** okna dialogowego, wykonaj następujące kroki hello:</span><span class="sxs-lookup"><span data-stu-id="6b52c-178">On hello **Configure SAML 2.0** dialog, perform hello following steps:</span></span>
   
    <span data-ttu-id="6b52c-179">![Skonfigurować SAML 2.0](./media/active-directory-saas-sumologic-tutorial/ic778559.png "skonfigurować SAML 2.0")</span><span class="sxs-lookup"><span data-stu-id="6b52c-179">![Configure SAML 2.0](./media/active-directory-saas-sumologic-tutorial/ic778559.png "Configure SAML 2.0")</span></span>
   
    <span data-ttu-id="6b52c-180">a.</span><span class="sxs-lookup"><span data-stu-id="6b52c-180">a.</span></span> <span data-ttu-id="6b52c-181">W hello **Nazwa konfiguracji** pole tekstowe, typ **usługi Azure AD**.</span><span class="sxs-lookup"><span data-stu-id="6b52c-181">In hello **Configuration Name** textbox, type **Azure AD**.</span></span> 

    <span data-ttu-id="6b52c-182">b.</span><span class="sxs-lookup"><span data-stu-id="6b52c-182">b.</span></span> <span data-ttu-id="6b52c-183">Wybierz **tryb debugowania**.</span><span class="sxs-lookup"><span data-stu-id="6b52c-183">Select **Debug Mode**.</span></span>

    <span data-ttu-id="6b52c-184">c.</span><span class="sxs-lookup"><span data-stu-id="6b52c-184">c.</span></span> <span data-ttu-id="6b52c-185">W hello **wystawcy** pole tekstowe, Wklej wartość hello **identyfikator jednostki SAML**, które zostały skopiowane z portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="6b52c-185">In hello **Issuer** textbox, paste hello value of **SAML Entity ID**, which you have copied from Azure portal.</span></span> 

    <span data-ttu-id="6b52c-186">d.</span><span class="sxs-lookup"><span data-stu-id="6b52c-186">d.</span></span> <span data-ttu-id="6b52c-187">W hello **URL żądania uwierzytelniania** pole tekstowe, Wklej wartość hello **SAML pojedynczy znak na adres URL usługi**, które zostały skopiowane z portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="6b52c-187">In hello **Authn Request URL** textbox, paste hello value of **SAML Single Sign-On Service URL**, which you have copied from Azure portal.</span></span>

    <span data-ttu-id="6b52c-188">e.</span><span class="sxs-lookup"><span data-stu-id="6b52c-188">e.</span></span> <span data-ttu-id="6b52c-189">Otwieranie certyfikatu zakodowanego base-64 w Notatniku hello kopiowania zawartości go do Schowka, a następnie wklej hello cały certyfikat do **certyfikatu X.509** pola tekstowego.</span><span class="sxs-lookup"><span data-stu-id="6b52c-189">Open your base-64 encoded certificate in notepad, copy hello content of it into your clipboard, and then paste hello entire Certificate into **X.509 Certificate** textbox.</span></span>

    <span data-ttu-id="6b52c-190">f.</span><span class="sxs-lookup"><span data-stu-id="6b52c-190">f.</span></span> <span data-ttu-id="6b52c-191">Jako **atrybut poczty E-mail**, wybierz pozycję **podmiotu SAML użyj**.</span><span class="sxs-lookup"><span data-stu-id="6b52c-191">As **Email Attribute**, select **Use SAML subject**.</span></span>  

    <span data-ttu-id="6b52c-192">g.</span><span class="sxs-lookup"><span data-stu-id="6b52c-192">g.</span></span> <span data-ttu-id="6b52c-193">Wybierz **SP zainicjował konfiguracji logowania**.</span><span class="sxs-lookup"><span data-stu-id="6b52c-193">Select **SP initiated Login Configuration**.</span></span>

    <span data-ttu-id="6b52c-194">h.</span><span class="sxs-lookup"><span data-stu-id="6b52c-194">h.</span></span> <span data-ttu-id="6b52c-195">W hello **ścieżkę logowania** pole tekstowe, typ **Azure** i kliknij przycisk **zapisać**.</span><span class="sxs-lookup"><span data-stu-id="6b52c-195">In hello **Login Path** textbox, type **Azure** and click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="6b52c-196">Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz hello [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji hello!</span><span class="sxs-lookup"><span data-stu-id="6b52c-196">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="6b52c-197">Po dodaniu tej aplikacji z hello **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij hello **rejestracji jednokrotnej** hello kartę i dostępu do osadzonych dokumentacji za pośrednictwem hello  **Konfiguracja** sekcji u dołu hello.</span><span class="sxs-lookup"><span data-stu-id="6b52c-197">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="6b52c-198">Więcej o hello osadzonych dokumentacji funkcji w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="6b52c-198">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="6b52c-199">Tworzenie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="6b52c-199">Creating an Azure AD test user</span></span>
<span data-ttu-id="6b52c-200">Celem Hello w tej sekcji jest toocreate użytkownika testowego, w portalu Azure o nazwie Simona Britta hello.</span><span class="sxs-lookup"><span data-stu-id="6b52c-200">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Tworzenie użytkowników usługi Azure AD][100]

<span data-ttu-id="6b52c-202">**toocreate użytkownika testowego w usłudze Azure AD, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="6b52c-202">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="6b52c-203">W hello **portalu Azure**na temat hello w lewym okienku nawigacji, kliknij przycisk **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="6b52c-203">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-sumologic-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="6b52c-205">toodisplay hello listę użytkowników, przejdź zbyt**użytkowników i grup** i kliknij przycisk **wszyscy użytkownicy**.</span><span class="sxs-lookup"><span data-stu-id="6b52c-205">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-sumologic-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="6b52c-207">Witaj tooopen **użytkownika** okna dialogowego, kliknij przycisk **Dodaj** u góry hello hello okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="6b52c-207">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-sumologic-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="6b52c-209">Na powitania **użytkownika** okna dialogowego wykonaj hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="6b52c-209">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-sumologic-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="6b52c-211">a.</span><span class="sxs-lookup"><span data-stu-id="6b52c-211">a.</span></span> <span data-ttu-id="6b52c-212">W hello **nazwa** pole tekstowe, typ **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="6b52c-212">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="6b52c-213">b.</span><span class="sxs-lookup"><span data-stu-id="6b52c-213">b.</span></span> <span data-ttu-id="6b52c-214">W hello **nazwy użytkownika** pole tekstowe, hello typu **adres e-mail** z BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="6b52c-214">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="6b52c-215">c.</span><span class="sxs-lookup"><span data-stu-id="6b52c-215">c.</span></span> <span data-ttu-id="6b52c-216">Wybierz **Pokaż hasło** i zanotuj wartość hello hello **hasło**.</span><span class="sxs-lookup"><span data-stu-id="6b52c-216">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="6b52c-217">d.</span><span class="sxs-lookup"><span data-stu-id="6b52c-217">d.</span></span> <span data-ttu-id="6b52c-218">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="6b52c-218">Click **Create**.</span></span>
 
### <a name="creating-a-sumologic-test-user"></a><span data-ttu-id="6b52c-219">Tworzenie użytkownika testowego SumoLogic</span><span class="sxs-lookup"><span data-stu-id="6b52c-219">Creating a SumoLogic test user</span></span>

<span data-ttu-id="6b52c-220">Użytkownicy usługi Azure AD toolog kolejności tooenable w tooSumoLogic muszą być tooSumoLogic elastycznie.</span><span class="sxs-lookup"><span data-stu-id="6b52c-220">In order tooenable Azure AD users toolog in tooSumoLogic, they must be provisioned tooSumoLogic.</span></span>  

* <span data-ttu-id="6b52c-221">W przypadku hello SumoLogic Inicjowanie obsługi to zadanie ręczne.</span><span class="sxs-lookup"><span data-stu-id="6b52c-221">In hello case of SumoLogic, provisioning is a manual task.</span></span>

<span data-ttu-id="6b52c-222">**tooprovision konta użytkownika, należy wykonać hello następujące kroki:**</span><span class="sxs-lookup"><span data-stu-id="6b52c-222">**tooprovision a user account, perform hello following steps:**</span></span>

1. <span data-ttu-id="6b52c-223">Zaloguj się za tooyour **SumoLogic** dzierżawy.</span><span class="sxs-lookup"><span data-stu-id="6b52c-223">Log in tooyour **SumoLogic** tenant.</span></span>

2. <span data-ttu-id="6b52c-224">Przejdź za**Zarządzaj \> użytkowników**.</span><span class="sxs-lookup"><span data-stu-id="6b52c-224">Go too**Manage \> Users**.</span></span>
   
    <span data-ttu-id="6b52c-225">![Użytkownicy](./media/active-directory-saas-sumologic-tutorial/ic778561.png "użytkowników")</span><span class="sxs-lookup"><span data-stu-id="6b52c-225">![Users](./media/active-directory-saas-sumologic-tutorial/ic778561.png "Users")</span></span>

3. <span data-ttu-id="6b52c-226">Kliknij pozycję **Dodaj**.</span><span class="sxs-lookup"><span data-stu-id="6b52c-226">Click **Add**.</span></span>
   
    <span data-ttu-id="6b52c-227">![Użytkownicy](./media/active-directory-saas-sumologic-tutorial/ic778562.png "użytkowników")</span><span class="sxs-lookup"><span data-stu-id="6b52c-227">![Users](./media/active-directory-saas-sumologic-tutorial/ic778562.png "Users")</span></span>

4. <span data-ttu-id="6b52c-228">Na powitania **nowego użytkownika** okna dialogowego, wykonaj następujące kroki hello:</span><span class="sxs-lookup"><span data-stu-id="6b52c-228">On hello **New User** dialog, perform hello following steps:</span></span>
   
    <span data-ttu-id="6b52c-229">![Nowy użytkownik](./media/active-directory-saas-sumologic-tutorial/ic778563.png "nowego użytkownika")</span><span class="sxs-lookup"><span data-stu-id="6b52c-229">![New User](./media/active-directory-saas-sumologic-tutorial/ic778563.png "New User")</span></span> 
 
    <span data-ttu-id="6b52c-230">a.</span><span class="sxs-lookup"><span data-stu-id="6b52c-230">a.</span></span> <span data-ttu-id="6b52c-231">Typ hello powiązane informacje konta hello Azure AD ma tooprovision do hello **imię**, **nazwisko**, i **E-mail** pól tekstowych.</span><span class="sxs-lookup"><span data-stu-id="6b52c-231">Type hello related information of hello Azure AD account you want tooprovision into hello **First Name**, **Last Name**, and **Email** textboxes.</span></span>
  
    <span data-ttu-id="6b52c-232">b.</span><span class="sxs-lookup"><span data-stu-id="6b52c-232">b.</span></span> <span data-ttu-id="6b52c-233">Wybierz rolę.</span><span class="sxs-lookup"><span data-stu-id="6b52c-233">Select a role.</span></span>
  
    <span data-ttu-id="6b52c-234">c.</span><span class="sxs-lookup"><span data-stu-id="6b52c-234">c.</span></span> <span data-ttu-id="6b52c-235">Jako **stan**, wybierz pozycję **Active**.</span><span class="sxs-lookup"><span data-stu-id="6b52c-235">As **Status**, select **Active**.</span></span>
  
    <span data-ttu-id="6b52c-236">d.</span><span class="sxs-lookup"><span data-stu-id="6b52c-236">d.</span></span> <span data-ttu-id="6b52c-237">Kliknij pozycję **Zapisz**.</span><span class="sxs-lookup"><span data-stu-id="6b52c-237">Click **Save**.</span></span>

>[!NOTE]
><span data-ttu-id="6b52c-238">Możesz użyć innych SumoLogic użytkownika konta tworzenia narzędzi lub interfejsów API dostarczonych przez SumoLogic tooprovision kont użytkowników usługi AAD.</span><span class="sxs-lookup"><span data-stu-id="6b52c-238">You can use any other SumoLogic user account creation tools or APIs provided by SumoLogic tooprovision AAD user accounts.</span></span> 
> 

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="6b52c-239">Przypisanie użytkownika testowego hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="6b52c-239">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="6b52c-240">W tej sekcji możesz włączyć toouse Simona Britta Azure logowania jednokrotnego za udzielanie dostępu tooSumoLogic.</span><span class="sxs-lookup"><span data-stu-id="6b52c-240">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooSumoLogic.</span></span>

![Przypisz użytkownika][200] 

<span data-ttu-id="6b52c-242">**tooassign tooSumoLogic Simona Britta wykonaj hello następujące kroki:**</span><span class="sxs-lookup"><span data-stu-id="6b52c-242">**tooassign Britta Simon tooSumoLogic, perform hello following steps:**</span></span>

1. <span data-ttu-id="6b52c-243">W portalu Azure hello, otwórz widok aplikacji hello, a następnie przejdź do widoku katalogu toohello i przejść za**aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="6b52c-243">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Przypisz użytkownika][201] 

2. <span data-ttu-id="6b52c-245">Z listy aplikacji hello wybierz **SumoLogic**.</span><span class="sxs-lookup"><span data-stu-id="6b52c-245">In hello applications list, select **SumoLogic**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-sumologic-tutorial/tutorial_sumologic_app.png) 

3. <span data-ttu-id="6b52c-247">W menu powitania po lewej stronie powitania kliknij **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="6b52c-247">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Przypisz użytkownika][202] 

4. <span data-ttu-id="6b52c-249">Kliknij przycisk **Dodaj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="6b52c-249">Click **Add** button.</span></span> <span data-ttu-id="6b52c-250">Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="6b52c-250">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Przypisz użytkownika][203]

5. <span data-ttu-id="6b52c-252">Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** hello listy użytkowników.</span><span class="sxs-lookup"><span data-stu-id="6b52c-252">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="6b52c-253">Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="6b52c-253">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="6b52c-254">Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="6b52c-254">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="6b52c-255">Testowanie rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="6b52c-255">Testing single sign-on</span></span>

<span data-ttu-id="6b52c-256">Celem Hello w tej sekcji jest tootest użyciu usługi Azure AD konfiguracji rejestracji jednokrotnej hello panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="6b52c-256">hello objective of this section is tootest your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="6b52c-257">Po kliknięciu kafelka SumoLogic hello w hello Panel dostępu, należy pobrać automatycznie zalogowane tooyour SumoLogic aplikacji.</span><span class="sxs-lookup"><span data-stu-id="6b52c-257">When you click hello SumoLogic tile in hello Access Panel, you should get automatically signed-on tooyour SumoLogic application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="6b52c-258">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="6b52c-258">Additional resources</span></span>

* [<span data-ttu-id="6b52c-259">Lista samouczków dotyczących tooIntegrate aplikacji SaaS w usłudze Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="6b52c-259">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="6b52c-260">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="6b52c-260">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-sumologic-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-sumologic-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-sumologic-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-sumologic-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-sumologic-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-sumologic-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-sumologic-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-sumologic-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-sumologic-tutorial/tutorial_general_203.png

