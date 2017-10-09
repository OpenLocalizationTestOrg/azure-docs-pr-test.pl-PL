---
title: 'Samouczek: Integracji Azure Active Directory z HireVue | Dokumentacja firmy Microsoft'
description: "Dowiedz się, jak tooconfigure logowanie jednokrotne między usługą Azure Active Directory i HireVue."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: aadfc342-14db-4d74-a83d-f0c76f0cf63c
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/22/2017
ms.author: jeedes
ms.openlocfilehash: f890633ee4f13919c32a43d7b6cf30f2270ef6a1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-hirevue"></a><span data-ttu-id="80eca-103">Samouczek: Integracji Azure Active Directory z HireVue</span><span class="sxs-lookup"><span data-stu-id="80eca-103">Tutorial: Azure Active Directory integration with HireVue</span></span>

<span data-ttu-id="80eca-104">Z tego samouczka, dowiesz się, jak toointegrate HireVue w usłudze Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="80eca-104">In this tutorial, you learn how toointegrate HireVue with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="80eca-105">Integracja z usługą Azure AD HireVue zapewnia hello następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="80eca-105">Integrating HireVue with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="80eca-106">Można kontrolować w usłudze Azure AD, kto ma dostęp do tooHireVue</span><span class="sxs-lookup"><span data-stu-id="80eca-106">You can control in Azure AD who has access tooHireVue</span></span>
- <span data-ttu-id="80eca-107">Można włączyć użytkownika użytkownicy tooautomatically get zalogowane tooHireVue (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="80eca-107">You can enable your users tooautomatically get signed-on tooHireVue (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="80eca-108">Możesz zarządzać kont w jednej centralnej lokalizacji - hello portalu Azure</span><span class="sxs-lookup"><span data-stu-id="80eca-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="80eca-109">Jeśli chcesz tooknow więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="80eca-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="80eca-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="80eca-110">Prerequisites</span></span>

<span data-ttu-id="80eca-111">tooconfigure integracji z usługą Azure AD z HireVue należy hello następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="80eca-111">tooconfigure Azure AD integration with HireVue, you need hello following items:</span></span>

- <span data-ttu-id="80eca-112">Subskrypcję usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="80eca-112">An Azure AD subscription</span></span>
- <span data-ttu-id="80eca-113">HireVue logowanie jednokrotne włączone subskrypcji</span><span class="sxs-lookup"><span data-stu-id="80eca-113">A HireVue single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="80eca-114">tootest hello kroków w tym samouczku, zaleca się przy użyciu środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="80eca-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="80eca-115">tootest hello kroki opisane w tym samouczku, należy stosować te zalecenia:</span><span class="sxs-lookup"><span data-stu-id="80eca-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="80eca-116">Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="80eca-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="80eca-117">Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz pobrać miesięczna wersja próbna [tutaj](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="80eca-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="80eca-118">Opis scenariusza</span><span class="sxs-lookup"><span data-stu-id="80eca-118">Scenario description</span></span>
<span data-ttu-id="80eca-119">W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym.</span><span class="sxs-lookup"><span data-stu-id="80eca-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="80eca-120">Scenariusz Hello opisane w tym samouczku składa się z dwóch głównych elementów:</span><span class="sxs-lookup"><span data-stu-id="80eca-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="80eca-121">Dodawanie HireVue z galerii hello</span><span class="sxs-lookup"><span data-stu-id="80eca-121">Adding HireVue from hello gallery</span></span>
2. <span data-ttu-id="80eca-122">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="80eca-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-hirevue-from-hello-gallery"></a><span data-ttu-id="80eca-123">Dodawanie HireVue z galerii hello</span><span class="sxs-lookup"><span data-stu-id="80eca-123">Adding HireVue from hello gallery</span></span>
<span data-ttu-id="80eca-124">tooconfigure hello integracji HireVue do usługi Azure AD, należy tooadd HireVue z hello galerii tooyour listę zarządzanych aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="80eca-124">tooconfigure hello integration of HireVue into Azure AD, you need tooadd HireVue from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="80eca-125">**tooadd HireVue z galerii hello, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="80eca-125">**tooadd HireVue from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="80eca-126">W hello  **[portalu Azure](https://portal.azure.com)**na temat hello panelu nawigacji po lewej stronie, kliknij przycisk **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="80eca-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Usługa Active Directory][1]

2. <span data-ttu-id="80eca-128">Przejdź za**aplikacje dla przedsiębiorstw**.</span><span class="sxs-lookup"><span data-stu-id="80eca-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="80eca-129">Następnie przejdź zbyt**wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="80eca-129">Then go too**All applications**.</span></span>

    ![Aplikacje][2]
    
3. <span data-ttu-id="80eca-131">tooadd nową aplikację, kliknij przycisk **nowej aplikacji** przycisk u góry hello okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="80eca-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplikacje][3]

4. <span data-ttu-id="80eca-133">W polu wyszukiwania hello wpisz **HireVue**.</span><span class="sxs-lookup"><span data-stu-id="80eca-133">In hello search box, type **HireVue**.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-hirevue-tutorial/tutorial_hirevue_search.png)

5. <span data-ttu-id="80eca-135">W panelu wyników hello zaznacz **HireVue**, a następnie kliknij przycisk **Dodaj** przycisk aplikacji hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="80eca-135">In hello results panel, select **HireVue**, and then click **Add** button tooadd hello application.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-hirevue-tutorial/tutorial_hirevue_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="80eca-137">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="80eca-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="80eca-138">W tej sekcji skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z HireVue w oparciu o nazwie "Britta Simona" użytkownika testowego.</span><span class="sxs-lookup"><span data-stu-id="80eca-138">In this section, you configure and test Azure AD single sign-on with HireVue based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="80eca-139">Dla pojedynczego logowania jednokrotnego toowork usługi Azure AD musi tooknow użytkownika odpowiednikiem hello w HireVue jest tooa użytkownika w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="80eca-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in HireVue is tooa user in Azure AD.</span></span> <span data-ttu-id="80eca-140">Innymi słowy relację łącza między użytkownika usługi Azure AD i hello użytkownikowi w HireVue musi toobe ustanowione.</span><span class="sxs-lookup"><span data-stu-id="80eca-140">In other words, a link relationship between an Azure AD user and hello related user in HireVue needs toobe established.</span></span>

<span data-ttu-id="80eca-141">W HireVue, należy przypisać wartość hello hello **nazwy użytkownika** w usłudze Azure AD jako wartość hello hello **Username** tooestablish hello łącze relacji.</span><span class="sxs-lookup"><span data-stu-id="80eca-141">In HireVue, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="80eca-142">tooconfigure i testowych usługi Azure AD rejestracji jednokrotnej z HireVue, należy po bloków konstrukcyjnych hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="80eca-142">tooconfigure and test Azure AD single sign-on with HireVue, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="80eca-143">**[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configuring-azure-ad-single-sign-on)**  -tooenable Twojego toouse użytkowników tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="80eca-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="80eca-144">**[Tworzenie użytkownika testowego usługi Azure AD](#creating-an-azure-ad-test-user)**  -tootest usługi Azure AD rejestracji jednokrotnej z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="80eca-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="80eca-145">**[Tworzenie użytkownika testowego HireVue](#creating-a-hirevue-test-user)**  -toohave odpowiednikiem Simona Britta w HireVue, który jest połączony toohello usługi Azure AD reprezentację użytkownika.</span><span class="sxs-lookup"><span data-stu-id="80eca-145">**[Creating a HireVue test user](#creating-a-hirevue-test-user)** - toohave a counterpart of Britta Simon in HireVue that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="80eca-146">**[Przypisanie użytkownika testowego hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Simona Britta toouse usługi Azure AD rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="80eca-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="80eca-147">**[Testowanie rejestracji jednokrotnej](#testing-single-sign-on)**  -tooverify czy hello konfiguracji działania.</span><span class="sxs-lookup"><span data-stu-id="80eca-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="80eca-148">Konfigurowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="80eca-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="80eca-149">W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w portalu Azure hello i skonfigurować logowanie jednokrotne w aplikacji HireVue.</span><span class="sxs-lookup"><span data-stu-id="80eca-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your HireVue application.</span></span>

<span data-ttu-id="80eca-150">**tooconfigure usługi Azure AD rejestracji jednokrotnej z HireVue, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="80eca-150">**tooconfigure Azure AD single sign-on with HireVue, perform hello following steps:**</span></span>

1. <span data-ttu-id="80eca-151">W portalu Azure na powitania hello **HireVue** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.</span><span class="sxs-lookup"><span data-stu-id="80eca-151">In hello Azure portal, on hello **HireVue** application integration page, click **Single sign-on**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej][4]

2. <span data-ttu-id="80eca-153">Na powitania **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** tooenable rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="80eca-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-hirevue-tutorial/tutorial_hirevue_samlbase.png)

3. <span data-ttu-id="80eca-155">Na powitania **HireVue domeny i adres URL** sekcji, wykonaj następujące kroki hello:</span><span class="sxs-lookup"><span data-stu-id="80eca-155">On hello **HireVue Domain and URLs** section, perform hello following steps:</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-hirevue-tutorial/tutorial_hirevue_url.png)

    <span data-ttu-id="80eca-157">a.</span><span class="sxs-lookup"><span data-stu-id="80eca-157">a.</span></span> <span data-ttu-id="80eca-158">W hello **adres URL logowania** tekstowym, wpisz adres URL za pomocą hello następującego wzorca:</span><span class="sxs-lookup"><span data-stu-id="80eca-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern:</span></span>

    | <span data-ttu-id="80eca-159">Środowisko</span><span class="sxs-lookup"><span data-stu-id="80eca-159">Environment</span></span> | <span data-ttu-id="80eca-160">ADRES URL</span><span class="sxs-lookup"><span data-stu-id="80eca-160">URL</span></span> |
    |-------------|---|
    | <span data-ttu-id="80eca-161">Produkcji</span><span class="sxs-lookup"><span data-stu-id="80eca-161">Production</span></span> | `https://<companyname>.hirevue.com` |
    | <span data-ttu-id="80eca-162">Przemieszczania</span><span class="sxs-lookup"><span data-stu-id="80eca-162">Staging</span></span>    | `https://<companyname>.stghv.com` |
    
    <span data-ttu-id="80eca-163">b.</span><span class="sxs-lookup"><span data-stu-id="80eca-163">b.</span></span> <span data-ttu-id="80eca-164">W hello **identyfikator** tekstowym, wpisz adres URL jako:</span><span class="sxs-lookup"><span data-stu-id="80eca-164">In hello **Identifier** textbox, type a URL as:</span></span>
    
    | <span data-ttu-id="80eca-165">Środowisko</span><span class="sxs-lookup"><span data-stu-id="80eca-165">Environment</span></span> | <span data-ttu-id="80eca-166">URN</span><span class="sxs-lookup"><span data-stu-id="80eca-166">URN</span></span> |
    |-------------|-----|
    | <span data-ttu-id="80eca-167">Produkcji</span><span class="sxs-lookup"><span data-stu-id="80eca-167">Production</span></span> |`urn:federation:hirevue.com:saml:sp:prod` |
    | <span data-ttu-id="80eca-168">Przemieszczania</span><span class="sxs-lookup"><span data-stu-id="80eca-168">Staging</span></span>    | `urn:federation:hirevue.com:saml:sp:staging`|
    
    > [!NOTE] 
    > <span data-ttu-id="80eca-169">Wartości te nie są prawdziwe.</span><span class="sxs-lookup"><span data-stu-id="80eca-169">These values are not real.</span></span> <span data-ttu-id="80eca-170">Zaktualizować te wartości z hello rzeczywisty adres URL logowania i identyfikator.</span><span class="sxs-lookup"><span data-stu-id="80eca-170">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="80eca-171">Skontaktuj się z [zespołem pomocy technicznej klienta HireVue](mailto:samlsupport@hirevue.com) tooget tych wartości.</span><span class="sxs-lookup"><span data-stu-id="80eca-171">Contact [HireVue Client support team](mailto:samlsupport@hirevue.com) tooget these values.</span></span> 
 
4. <span data-ttu-id="80eca-172">Na powitania **certyfikat podpisywania SAML** kliknij **Certificate(Base64)** , a następnie zapisz plik certyfikatu hello na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="80eca-172">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-hirevue-tutorial/tutorial_hirevue_certificate.png) 

5. <span data-ttu-id="80eca-174">Kliknij przycisk **zapisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="80eca-174">Click **Save** button.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-hirevue-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="80eca-176">Na powitania **konfiguracji HireVue** kliknij **skonfigurować HireVue** tooopen **Konfigurowanie logowania jednokrotnego** okna.</span><span class="sxs-lookup"><span data-stu-id="80eca-176">On hello **HireVue Configuration** section, click **Configure HireVue** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="80eca-177">Kopiuj hello **Sign-Out adres URL, identyfikator jednostki SAML i SAML pojedynczy znak na adres URL usługi** z hello **sekcji krótkimi opisami.**</span><span class="sxs-lookup"><span data-stu-id="80eca-177">Copy hello **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-hirevue-tutorial/tutorial_hirevue_configure.png) 

7. <span data-ttu-id="80eca-179">tooconfigure rejestracji jednokrotnej w **HireVue** strony, należy pobrać hello toosend **Certificate(Base64)** i **Sign-Out adres URL, identyfikator jednostki SAML i SAML pojedynczy znak na adres URL usługi** za[zespołem pomocy technicznej HireVue](mailto:samlsupport@hirevue.com).</span><span class="sxs-lookup"><span data-stu-id="80eca-179">tooconfigure single sign-on on **HireVue** side, you need toosend hello downloaded **Certificate(Base64)** and **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** too[HireVue support team](mailto:samlsupport@hirevue.com).</span></span> <span data-ttu-id="80eca-180">To ustawienie toohave hello prawidłowo po obu stronach połączenia logowania jednokrotnego SAML one ustawić.</span><span class="sxs-lookup"><span data-stu-id="80eca-180">They set this setting toohave hello SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="80eca-181">Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz hello [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji hello!</span><span class="sxs-lookup"><span data-stu-id="80eca-181">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="80eca-182">Po dodaniu tej aplikacji z hello **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij hello **rejestracji jednokrotnej** hello kartę i dostępu do osadzonych dokumentacji za pośrednictwem hello  **Konfiguracja** sekcji u dołu hello.</span><span class="sxs-lookup"><span data-stu-id="80eca-182">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="80eca-183">Więcej o hello osadzonych dokumentacji funkcji w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="80eca-183">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="80eca-184">Tworzenie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="80eca-184">Creating an Azure AD test user</span></span>
<span data-ttu-id="80eca-185">Celem Hello w tej sekcji jest toocreate użytkownika testowego, w portalu Azure o nazwie Simona Britta hello.</span><span class="sxs-lookup"><span data-stu-id="80eca-185">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Tworzenie użytkowników usługi Azure AD][100]

<span data-ttu-id="80eca-187">**toocreate użytkownika testowego w usłudze Azure AD, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="80eca-187">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="80eca-188">W hello **portalu Azure**na temat hello w lewym okienku nawigacji, kliknij przycisk **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="80eca-188">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-hirevue-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="80eca-190">toodisplay hello listę użytkowników, przejdź zbyt**użytkowników i grup** i kliknij przycisk **wszyscy użytkownicy**.</span><span class="sxs-lookup"><span data-stu-id="80eca-190">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-hirevue-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="80eca-192">Witaj tooopen **użytkownika** okna dialogowego, kliknij przycisk **Dodaj** u góry hello hello okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="80eca-192">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-hirevue-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="80eca-194">Na powitania **użytkownika** okna dialogowego wykonaj hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="80eca-194">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-hirevue-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="80eca-196">a.</span><span class="sxs-lookup"><span data-stu-id="80eca-196">a.</span></span> <span data-ttu-id="80eca-197">W hello **nazwa** pole tekstowe, typ **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="80eca-197">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="80eca-198">b.</span><span class="sxs-lookup"><span data-stu-id="80eca-198">b.</span></span> <span data-ttu-id="80eca-199">W hello **nazwy użytkownika** pole tekstowe, hello typu **adres e-mail** z BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="80eca-199">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="80eca-200">c.</span><span class="sxs-lookup"><span data-stu-id="80eca-200">c.</span></span> <span data-ttu-id="80eca-201">Wybierz **Pokaż hasło** i zanotuj wartość hello hello **hasło**.</span><span class="sxs-lookup"><span data-stu-id="80eca-201">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="80eca-202">d.</span><span class="sxs-lookup"><span data-stu-id="80eca-202">d.</span></span> <span data-ttu-id="80eca-203">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="80eca-203">Click **Create**.</span></span>
 
### <a name="creating-a-hirevue-test-user"></a><span data-ttu-id="80eca-204">Tworzenie użytkownika testowego HireVue</span><span class="sxs-lookup"><span data-stu-id="80eca-204">Creating a HireVue test user</span></span>

<span data-ttu-id="80eca-205">W tej sekcji należy utworzyć użytkownika o nazwie Simona Britta w HireVue.</span><span class="sxs-lookup"><span data-stu-id="80eca-205">In this section, you create a user called Britta Simon in HireVue.</span></span> <span data-ttu-id="80eca-206">We współpracy z [zespołem pomocy technicznej HireVue](mailto:samlsupport@hirevue.com) tooadd hello użytkowników hello HireVue platformy.</span><span class="sxs-lookup"><span data-stu-id="80eca-206">Please work with [HireVue support team](mailto:samlsupport@hirevue.com) tooadd hello users in hello HireVue platform.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="80eca-207">Przypisanie użytkownika testowego hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="80eca-207">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="80eca-208">W tej sekcji możesz włączyć toouse Simona Britta Azure logowania jednokrotnego za udzielanie dostępu tooHireVue.</span><span class="sxs-lookup"><span data-stu-id="80eca-208">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooHireVue.</span></span>

![Przypisz użytkownika][200] 

<span data-ttu-id="80eca-210">**tooassign tooHireVue Simona Britta wykonaj hello następujące kroki:**</span><span class="sxs-lookup"><span data-stu-id="80eca-210">**tooassign Britta Simon tooHireVue, perform hello following steps:**</span></span>

1. <span data-ttu-id="80eca-211">W portalu Azure hello, otwórz widok aplikacji hello, a następnie przejdź do widoku katalogu toohello i przejść za**aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="80eca-211">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Przypisz użytkownika][201] 

2. <span data-ttu-id="80eca-213">Z listy aplikacji hello wybierz **HireVue**.</span><span class="sxs-lookup"><span data-stu-id="80eca-213">In hello applications list, select **HireVue**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-hirevue-tutorial/tutorial_hirevue_app.png) 

3. <span data-ttu-id="80eca-215">W menu powitania po lewej stronie powitania kliknij **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="80eca-215">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Przypisz użytkownika][202] 

4. <span data-ttu-id="80eca-217">Kliknij przycisk **Dodaj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="80eca-217">Click **Add** button.</span></span> <span data-ttu-id="80eca-218">Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="80eca-218">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Przypisz użytkownika][203]

5. <span data-ttu-id="80eca-220">Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** hello listy użytkowników.</span><span class="sxs-lookup"><span data-stu-id="80eca-220">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="80eca-221">Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="80eca-221">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="80eca-222">Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="80eca-222">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="80eca-223">Testowanie rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="80eca-223">Testing single sign-on</span></span>

<span data-ttu-id="80eca-224">W tej sekcji można przetestować konfiguracji usługi Azure AD pojedynczego logowania jednokrotnego przy użyciu hello panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="80eca-224">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="80eca-225">Po kliknięciu kafelka HireVue hello w hello Panel dostępu, należy pobrać automatycznie zalogowane tooyour HireVue aplikacji.</span><span class="sxs-lookup"><span data-stu-id="80eca-225">When you click hello HireVue tile in hello Access Panel, you should get automatically signed-on tooyour HireVue application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="80eca-226">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="80eca-226">Additional resources</span></span>

* [<span data-ttu-id="80eca-227">Lista samouczków dotyczących tooIntegrate aplikacji SaaS w usłudze Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="80eca-227">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="80eca-228">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="80eca-228">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-hirevue-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-hirevue-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-hirevue-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-hirevue-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-hirevue-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-hirevue-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-hirevue-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-hirevue-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-hirevue-tutorial/tutorial_general_203.png

