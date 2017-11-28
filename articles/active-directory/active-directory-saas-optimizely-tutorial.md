---
title: 'Samouczek: Integracji Azure Active Directory z Optimizely | Dokumentacja firmy Microsoft'
description: "Dowiedz się, jak tooconfigure logowanie jednokrotne między usługą Azure Active Directory i Optimizely."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 28ef03e1-9aad-4301-af97-d94e853edc74
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/23/2017
ms.author: jeedes
ms.openlocfilehash: 868aefae27ca155d2963f3dcfcd79bbb564b48ba
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-optimizely"></a><span data-ttu-id="bb1f1-103">Samouczek: Integracji Azure Active Directory z Optimizely</span><span class="sxs-lookup"><span data-stu-id="bb1f1-103">Tutorial: Azure Active Directory integration with Optimizely</span></span>

<span data-ttu-id="bb1f1-104">Z tego samouczka, dowiesz się, jak toointegrate Optimizely w usłudze Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="bb1f1-104">In this tutorial, you learn how toointegrate Optimizely with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="bb1f1-105">Integracja z usługą Azure AD Optimizely zapewnia hello następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="bb1f1-105">Integrating Optimizely with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="bb1f1-106">Można kontrolować w usłudze Azure AD, kto ma dostęp do tooOptimizely</span><span class="sxs-lookup"><span data-stu-id="bb1f1-106">You can control in Azure AD who has access tooOptimizely</span></span>
- <span data-ttu-id="bb1f1-107">Można włączyć użytkownika użytkownicy tooautomatically get zalogowane tooOptimizely (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="bb1f1-107">You can enable your users tooautomatically get signed-on tooOptimizely (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="bb1f1-108">Możesz zarządzać kont w jednej centralnej lokalizacji - hello portalu Azure</span><span class="sxs-lookup"><span data-stu-id="bb1f1-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="bb1f1-109">Jeśli chcesz tooknow więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="bb1f1-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="bb1f1-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="bb1f1-110">Prerequisites</span></span>

<span data-ttu-id="bb1f1-111">tooconfigure integracji z usługą Azure AD z Optimizely należy hello następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="bb1f1-111">tooconfigure Azure AD integration with Optimizely, you need hello following items:</span></span>

- <span data-ttu-id="bb1f1-112">Subskrypcję usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="bb1f1-112">An Azure AD subscription</span></span>
- <span data-ttu-id="bb1f1-113">Optimizely logowanie jednokrotne włączone subskrypcji</span><span class="sxs-lookup"><span data-stu-id="bb1f1-113">An Optimizely single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="bb1f1-114">tootest hello kroków w tym samouczku, zaleca się przy użyciu środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="bb1f1-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="bb1f1-115">tootest hello kroki opisane w tym samouczku, należy stosować te zalecenia:</span><span class="sxs-lookup"><span data-stu-id="bb1f1-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="bb1f1-116">Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="bb1f1-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="bb1f1-117">Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz pobrać miesięczna wersja próbna [tutaj](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="bb1f1-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="bb1f1-118">Opis scenariusza</span><span class="sxs-lookup"><span data-stu-id="bb1f1-118">Scenario description</span></span>
<span data-ttu-id="bb1f1-119">W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym.</span><span class="sxs-lookup"><span data-stu-id="bb1f1-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="bb1f1-120">Scenariusz Hello opisane w tym samouczku składa się z dwóch głównych elementów:</span><span class="sxs-lookup"><span data-stu-id="bb1f1-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="bb1f1-121">Dodawanie Optimizely z galerii hello</span><span class="sxs-lookup"><span data-stu-id="bb1f1-121">Adding Optimizely from hello gallery</span></span>
2. <span data-ttu-id="bb1f1-122">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="bb1f1-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-optimizely-from-hello-gallery"></a><span data-ttu-id="bb1f1-123">Dodawanie Optimizely z galerii hello</span><span class="sxs-lookup"><span data-stu-id="bb1f1-123">Adding Optimizely from hello gallery</span></span>
<span data-ttu-id="bb1f1-124">tooconfigure hello integracji Optimizely do usługi Azure AD, należy tooadd Optimizely z hello galerii tooyour listę zarządzanych aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="bb1f1-124">tooconfigure hello integration of Optimizely into Azure AD, you need tooadd Optimizely from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="bb1f1-125">**tooadd Optimizely z galerii hello, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="bb1f1-125">**tooadd Optimizely from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="bb1f1-126">W hello  **[portalu Azure](https://portal.azure.com)**na temat hello panelu nawigacji po lewej stronie, kliknij przycisk **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="bb1f1-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Usługa Active Directory][1]

2. <span data-ttu-id="bb1f1-128">Przejdź za**aplikacje dla przedsiębiorstw**.</span><span class="sxs-lookup"><span data-stu-id="bb1f1-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="bb1f1-129">Następnie przejdź zbyt**wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="bb1f1-129">Then go too**All applications**.</span></span>

    ![Aplikacje][2]
    
3. <span data-ttu-id="bb1f1-131">tooadd nową aplikację, kliknij przycisk **nowej aplikacji** przycisk u góry hello okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="bb1f1-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplikacje][3]

4. <span data-ttu-id="bb1f1-133">W polu wyszukiwania hello wpisz **Optimizely**.</span><span class="sxs-lookup"><span data-stu-id="bb1f1-133">In hello search box, type **Optimizely**.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-optimizely-tutorial/tutorial_optimizely_search.png)

5. <span data-ttu-id="bb1f1-135">W panelu wyników hello zaznacz **Optimizely**, a następnie kliknij przycisk **Dodaj** przycisk aplikacji hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="bb1f1-135">In hello results panel, select **Optimizely**, and then click **Add** button tooadd hello application.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-optimizely-tutorial/tutorial_optimizely_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="bb1f1-137">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="bb1f1-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="bb1f1-138">W tej sekcji możesz skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z Optimizely na podstawie użytkownika testowego, nazywany "Britta Simona".</span><span class="sxs-lookup"><span data-stu-id="bb1f1-138">In this section, you configure and test Azure AD single sign-on with Optimizely based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="bb1f1-139">Dla pojedynczego logowania jednokrotnego toowork usługi Azure AD musi tooknow użytkownika odpowiednikiem hello w Optimizely jest tooa użytkownika w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="bb1f1-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Optimizely is tooa user in Azure AD.</span></span> <span data-ttu-id="bb1f1-140">Innymi słowy relację łącza między użytkownika usługi Azure AD i hello użytkownikowi w Optimizely musi toobe ustanowione.</span><span class="sxs-lookup"><span data-stu-id="bb1f1-140">In other words, a link relationship between an Azure AD user and hello related user in Optimizely needs toobe established.</span></span>

<span data-ttu-id="bb1f1-141">Ta relacja łącza zostanie nawiązane, przypisując wartość hello hello **nazwy użytkownika** w usłudze Azure AD jako wartość hello hello **Username** w Optimizely.</span><span class="sxs-lookup"><span data-stu-id="bb1f1-141">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in Optimizely.</span></span>

<span data-ttu-id="bb1f1-142">tooconfigure i testowych usługi Azure AD rejestracji jednokrotnej z Optimizely, należy po bloków konstrukcyjnych hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="bb1f1-142">tooconfigure and test Azure AD single sign-on with Optimizely, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="bb1f1-143">**[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configuring-azure-ad-single-sign-on)**  -tooenable Twojego toouse użytkowników tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="bb1f1-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="bb1f1-144">**[Tworzenie użytkownika testowego usługi Azure AD](#creating-an-azure-ad-test-user)**  -tootest usługi Azure AD rejestracji jednokrotnej z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="bb1f1-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="bb1f1-145">**[Tworzenie użytkownika testowego Optimizely](#creating-an-optimizely-test-user)**  -toohave odpowiednikiem Simona Britta w Optimizely, który jest połączony toohello usługi Azure AD reprezentację użytkownika.</span><span class="sxs-lookup"><span data-stu-id="bb1f1-145">**[Creating an Optimizely test user](#creating-an-optimizely-test-user)** - toohave a counterpart of Britta Simon in Optimizely that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="bb1f1-146">**[Przypisanie użytkownika testowego hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Simona Britta toouse usługi Azure AD rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="bb1f1-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="bb1f1-147">**[Testowanie rejestracji jednokrotnej](#testing-single-sign-on)**  -tooverify czy hello konfiguracji działania.</span><span class="sxs-lookup"><span data-stu-id="bb1f1-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="bb1f1-148">Konfigurowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="bb1f1-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="bb1f1-149">W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w portalu Azure hello i skonfigurować logowanie jednokrotne w aplikacji Optimizely.</span><span class="sxs-lookup"><span data-stu-id="bb1f1-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Optimizely application.</span></span>

<span data-ttu-id="bb1f1-150">**tooconfigure usługi Azure AD rejestracji jednokrotnej z Optimizely, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="bb1f1-150">**tooconfigure Azure AD single sign-on with Optimizely, perform hello following steps:**</span></span>

1. <span data-ttu-id="bb1f1-151">W portalu Azure na powitania hello **Optimizely** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.</span><span class="sxs-lookup"><span data-stu-id="bb1f1-151">In hello Azure portal, on hello **Optimizely** application integration page, click **Single sign-on**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej][4]

2. <span data-ttu-id="bb1f1-153">Na powitania **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** tooenable rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="bb1f1-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-optimizely-tutorial/tutorial_optimizely_samlbase.png)

3. <span data-ttu-id="bb1f1-155">Na powitania **Optimizely domeny i adres URL** sekcji, wykonaj następujące kroki hello:</span><span class="sxs-lookup"><span data-stu-id="bb1f1-155">On hello **Optimizely Domain and URLs** section, perform hello following steps:</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-optimizely-tutorial/tutorial_optimizely_url.png)

    <span data-ttu-id="bb1f1-157">a.</span><span class="sxs-lookup"><span data-stu-id="bb1f1-157">a.</span></span> <span data-ttu-id="bb1f1-158">W hello **adres URL logowania** tekstowym, wpisz adres URL za pomocą hello następującego wzorca:`https://app.optimizely.net/<instance name>`</span><span class="sxs-lookup"><span data-stu-id="bb1f1-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://app.optimizely.net/<instance name>`</span></span>

    <span data-ttu-id="bb1f1-159">b.</span><span class="sxs-lookup"><span data-stu-id="bb1f1-159">b.</span></span> <span data-ttu-id="bb1f1-160">W hello **identyfikator** tekstowym, wpisz adres URL za pomocą hello następującego wzorca:`urn:auth0:optimizely:contoso`</span><span class="sxs-lookup"><span data-stu-id="bb1f1-160">In hello **Identifier** textbox, type a URL using hello following pattern:  `urn:auth0:optimizely:contoso`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="bb1f1-161">Wartości te nie są hello prawdziwe.</span><span class="sxs-lookup"><span data-stu-id="bb1f1-161">These values are not hello real.</span></span> <span data-ttu-id="bb1f1-162">Wartość hello zaktualizuje hello rzeczywisty adres URL logowania i identyfikator, który znajduje się w dalszej części samouczka hello.</span><span class="sxs-lookup"><span data-stu-id="bb1f1-162">You will update hello value with hello actual Sign-on URL and Identifier, which is explained later in hello tutorial.</span></span> 

4. <span data-ttu-id="bb1f1-163">Na powitania **certyfikat podpisywania SAML** kliknij **Certificate(Base64)** , a następnie zapisz plik certyfikatu hello na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="bb1f1-163">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-optimizely-tutorial/tutorial_optimizely_certificate.png) 

5. <span data-ttu-id="bb1f1-165">Kliknij przycisk **zapisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="bb1f1-165">Click **Save** button.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-optimizely-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="bb1f1-167">Na powitania **konfiguracji Optimizely** kliknij **skonfigurować Optimizely** tooopen **Konfigurowanie logowania jednokrotnego** okna.</span><span class="sxs-lookup"><span data-stu-id="bb1f1-167">On hello **Optimizely Configuration** section, click **Configure Optimizely** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="bb1f1-168">Kopiuj hello **SAML pojedynczy znak na adres URL usługi** z hello **sekcji krótkimi opisami.**</span><span class="sxs-lookup"><span data-stu-id="bb1f1-168">Copy hello **SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-optimizely-tutorial/tutorial_optimizely_configure.png) 

7. <span data-ttu-id="bb1f1-170">tooconfigure rejestracji jednokrotnej w **Optimizely** po stronie, skontaktuj się z menedżerem ds. klientów Optimizely i zapewnić hello pobrane **certyfikatu (Base64)**, i **SAML pojedynczy znak na adres URL usługi** .</span><span class="sxs-lookup"><span data-stu-id="bb1f1-170">tooconfigure single sign-on on **Optimizely** side, contact your Optimizely Account Manager and provide hello downloaded **Certificate (Base64)**, and **SAML Single Sign-On Service URL**.</span></span> 

8. <span data-ttu-id="bb1f1-171">W odpowiedzi tooyour wiadomości e-mail Optimizely zapewnia hello na adres URL logowania (SSO zainicjował SP) i hello wartości Identyfikator usługi dostawcy jednostki.</span><span class="sxs-lookup"><span data-stu-id="bb1f1-171">In response tooyour email, Optimizely provides you with hello Sign On URL (SP-initiated SSO) and hello Identifier (Service Provider Entity ID) values.</span></span>

    <span data-ttu-id="bb1f1-172">a.</span><span class="sxs-lookup"><span data-stu-id="bb1f1-172">a.</span></span> <span data-ttu-id="bb1f1-173">Hello kopiowania **inicjowane SP adres URL logowania jednokrotnego** o Optimizely i Wklej do hello **na adres URL logowania** textbox w **Optimizely domeny i adres URL** sekcji z portalu Azure</span><span class="sxs-lookup"><span data-stu-id="bb1f1-173">Copy hello **SP-initiated SSO URL** provided by Optimizely, and paste into hello **Sign On URL** textbox in **Optimizely Domain and URLs** section on Azure portal</span></span> 

    <span data-ttu-id="bb1f1-174">b.</span><span class="sxs-lookup"><span data-stu-id="bb1f1-174">b.</span></span> <span data-ttu-id="bb1f1-175">Kopia hello **identyfikator jednostki dostawcy usługi** o Optimizely i Wklej do hello **identyfikator** textbox w **Optimizely domeny i adres URL** sekcji z portalu Azure</span><span class="sxs-lookup"><span data-stu-id="bb1f1-175">Copy hello **Service Provider Entity ID** provided by Optimizely, and paste into hello **Identifier** textbox in **Optimizely Domain and URLs** section on Azure portal</span></span> 

9. <span data-ttu-id="bb1f1-176">W oknie innej przeglądarki, logowania jednokrotnego tooyour Optimizely aplikacji.</span><span class="sxs-lookup"><span data-stu-id="bb1f1-176">In a different browser window, sign-on tooyour Optimizely application.</span></span>

10. <span data-ttu-id="bb1f1-177">Kliknij nazwę u góry hello konta prawym narożniku, a następnie **ustawienia konta**.</span><span class="sxs-lookup"><span data-stu-id="bb1f1-177">Click you account name in hello top right corner and then **Account Settings**.</span></span>
   
    ![Azure AD rejestracji jednokrotnej](./media/active-directory-saas-optimizely-tutorial/tutorial_optimizely_09.png)

11. <span data-ttu-id="bb1f1-179">Na karcie Konto hello, hello pole wyboru **włączenia logowania jednokrotnego** w obszarze rejestracji jednokrotnej w hello **omówienie** sekcji.</span><span class="sxs-lookup"><span data-stu-id="bb1f1-179">In hello Account tab, check hello box **Enable SSO** under Single Sign On in hello **Overview** section.</span></span>
   
    ![Azure AD rejestracji jednokrotnej](./media/active-directory-saas-optimizely-tutorial/tutorial_optimizely_10.png)
    
12. <span data-ttu-id="bb1f1-181">Kliknij przycisk **Zapisz**</span><span class="sxs-lookup"><span data-stu-id="bb1f1-181">Click **Save**</span></span>

> [!TIP]
> <span data-ttu-id="bb1f1-182">Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz hello [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji hello!</span><span class="sxs-lookup"><span data-stu-id="bb1f1-182">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="bb1f1-183">Po dodaniu tej aplikacji z hello **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij hello **rejestracji jednokrotnej** hello kartę i dostępu do osadzonych dokumentacji za pośrednictwem hello  **Konfiguracja** sekcji u dołu hello.</span><span class="sxs-lookup"><span data-stu-id="bb1f1-183">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="bb1f1-184">Więcej o hello osadzonych dokumentacji funkcji w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="bb1f1-184">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="bb1f1-185">Tworzenie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="bb1f1-185">Creating an Azure AD test user</span></span>
<span data-ttu-id="bb1f1-186">Celem Hello w tej sekcji jest toocreate użytkownika testowego, w portalu Azure o nazwie Simona Britta hello.</span><span class="sxs-lookup"><span data-stu-id="bb1f1-186">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Tworzenie użytkowników usługi Azure AD][100]

<span data-ttu-id="bb1f1-188">**toocreate użytkownika testowego w usłudze Azure AD, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="bb1f1-188">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="bb1f1-189">W hello **portalu Azure**na temat hello w lewym okienku nawigacji, kliknij przycisk **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="bb1f1-189">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-optimizely-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="bb1f1-191">toodisplay hello listę użytkowników, przejdź zbyt**użytkowników i grup** i kliknij przycisk **wszyscy użytkownicy**.</span><span class="sxs-lookup"><span data-stu-id="bb1f1-191">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-optimizely-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="bb1f1-193">Witaj tooopen **użytkownika** okna dialogowego, kliknij przycisk **Dodaj** u góry hello hello okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="bb1f1-193">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-optimizely-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="bb1f1-195">Na powitania **użytkownika** okna dialogowego wykonaj hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="bb1f1-195">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-optimizely-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="bb1f1-197">a.</span><span class="sxs-lookup"><span data-stu-id="bb1f1-197">a.</span></span> <span data-ttu-id="bb1f1-198">W hello **nazwa** pole tekstowe, typ **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="bb1f1-198">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="bb1f1-199">b.</span><span class="sxs-lookup"><span data-stu-id="bb1f1-199">b.</span></span> <span data-ttu-id="bb1f1-200">W hello **nazwy użytkownika** pole tekstowe, hello typu **adres e-mail** z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="bb1f1-200">In hello **User name** textbox, type hello **email address** of Britta Simon.</span></span>

    <span data-ttu-id="bb1f1-201">c.</span><span class="sxs-lookup"><span data-stu-id="bb1f1-201">c.</span></span> <span data-ttu-id="bb1f1-202">Wybierz **Pokaż hasło** i zanotuj wartość hello hello **hasło**.</span><span class="sxs-lookup"><span data-stu-id="bb1f1-202">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="bb1f1-203">d.</span><span class="sxs-lookup"><span data-stu-id="bb1f1-203">d.</span></span> <span data-ttu-id="bb1f1-204">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="bb1f1-204">Click **Create**.</span></span>
 
### <a name="creating-an-optimizely-test-user"></a><span data-ttu-id="bb1f1-205">Tworzenie użytkownika testowego Optimizely</span><span class="sxs-lookup"><span data-stu-id="bb1f1-205">Creating an Optimizely test user</span></span>

<span data-ttu-id="bb1f1-206">W tej sekcji należy utworzyć użytkownika o nazwie Simona Britta w Optimizely.</span><span class="sxs-lookup"><span data-stu-id="bb1f1-206">In this section, you create a user called Britta Simon in Optimizely.</span></span>

1. <span data-ttu-id="bb1f1-207">Na stronie głównej hello, wybierz **współpracownicy** kartę.</span><span class="sxs-lookup"><span data-stu-id="bb1f1-207">On hello home page, select **Collaborators** tab.</span></span>

2. <span data-ttu-id="bb1f1-208">tooadd nowego współpracownika toohello projektu, kliknij przycisk **nowego współpracownika**.</span><span class="sxs-lookup"><span data-stu-id="bb1f1-208">tooadd new collaborator toohello project, click **New Collaborator**.</span></span>
   
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-optimizely-tutorial/create_aaduser_10.png)

3. <span data-ttu-id="bb1f1-210">Wypełnij hello adres e-mail i przydzielić mu rolę.</span><span class="sxs-lookup"><span data-stu-id="bb1f1-210">Fill in hello email address and assign them a role.</span></span> <span data-ttu-id="bb1f1-211">Kliknij przycisk **zaprosić**.</span><span class="sxs-lookup"><span data-stu-id="bb1f1-211">Click **Invite**.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-optimizely-tutorial/create_aaduser_11.png)

4. <span data-ttu-id="bb1f1-213">Te otrzymają zaproszenie poczty e-mail.</span><span class="sxs-lookup"><span data-stu-id="bb1f1-213">They receive an email invite.</span></span> <span data-ttu-id="bb1f1-214">Przy użyciu adresu e-mail hello, mają toolog w tooOptimizely.</span><span class="sxs-lookup"><span data-stu-id="bb1f1-214">Using hello email address, they have toolog in tooOptimizely.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="bb1f1-215">Przypisanie użytkownika testowego hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="bb1f1-215">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="bb1f1-216">W tej sekcji możesz włączyć toouse Simona Britta Azure logowania jednokrotnego za udzielanie dostępu tooOptimizely.</span><span class="sxs-lookup"><span data-stu-id="bb1f1-216">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooOptimizely.</span></span>

![Przypisz użytkownika][200] 

<span data-ttu-id="bb1f1-218">**tooassign tooOptimizely Simona Britta wykonaj hello następujące kroki:**</span><span class="sxs-lookup"><span data-stu-id="bb1f1-218">**tooassign Britta Simon tooOptimizely, perform hello following steps:**</span></span>

1. <span data-ttu-id="bb1f1-219">W portalu Azure hello, otwórz widok aplikacji hello, a następnie przejdź do widoku katalogu toohello i przejść za**aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="bb1f1-219">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Przypisz użytkownika][201] 

2. <span data-ttu-id="bb1f1-221">Z listy aplikacji hello wybierz **Optimizely**.</span><span class="sxs-lookup"><span data-stu-id="bb1f1-221">In hello applications list, select **Optimizely**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-optimizely-tutorial/tutorial_optimizely_app.png) 

3. <span data-ttu-id="bb1f1-223">W menu powitania po lewej stronie powitania kliknij **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="bb1f1-223">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Przypisz użytkownika][202] 

4. <span data-ttu-id="bb1f1-225">Kliknij przycisk **Dodaj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="bb1f1-225">Click **Add** button.</span></span> <span data-ttu-id="bb1f1-226">Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="bb1f1-226">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Przypisz użytkownika][203]

5. <span data-ttu-id="bb1f1-228">Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** hello listy użytkowników.</span><span class="sxs-lookup"><span data-stu-id="bb1f1-228">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="bb1f1-229">Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="bb1f1-229">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="bb1f1-230">Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="bb1f1-230">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="bb1f1-231">Testowanie rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="bb1f1-231">Testing single sign-on</span></span>

<span data-ttu-id="bb1f1-232">W tej sekcji można przetestować konfiguracji usługi Azure AD pojedynczego logowania jednokrotnego przy użyciu hello panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="bb1f1-232">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="bb1f1-233">Po kliknięciu kafelka Optimizely hello w hello Panel dostępu, należy pobrać automatycznie zalogowane tooyour Optimizely aplikacji.</span><span class="sxs-lookup"><span data-stu-id="bb1f1-233">When you click hello Optimizely tile in hello Access Panel, you should get automatically signed-on tooyour Optimizely application.</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="bb1f1-234">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="bb1f1-234">Additional resources</span></span>

* [<span data-ttu-id="bb1f1-235">Lista samouczków dotyczących tooIntegrate aplikacji SaaS w usłudze Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="bb1f1-235">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="bb1f1-236">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="bb1f1-236">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-optimizely-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-optimizely-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-optimizely-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-optimizely-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-optimizely-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-optimizely-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-optimizely-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-optimizely-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-optimizely-tutorial/tutorial_general_203.png

