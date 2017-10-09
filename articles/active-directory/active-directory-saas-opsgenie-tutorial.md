---
title: 'Samouczek: Integracji Azure Active Directory z OpsGenie | Dokumentacja firmy Microsoft'
description: "Dowiedz się, jak tooconfigure logowanie jednokrotne między usługą Azure Active Directory i OpsGenie."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 41b59b22-a61d-4fe6-ab0d-6c3991d1375f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/28/2017
ms.author: jeedes
ms.openlocfilehash: 50d31c234fb9716d05d681b9bc4164740a3a662b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-opsgenie"></a><span data-ttu-id="831fc-103">Samouczek: Integracji Azure Active Directory z OpsGenie</span><span class="sxs-lookup"><span data-stu-id="831fc-103">Tutorial: Azure Active Directory integration with OpsGenie</span></span>

<span data-ttu-id="831fc-104">Z tego samouczka, dowiesz się, jak toointegrate OpsGenie w usłudze Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="831fc-104">In this tutorial, you learn how toointegrate OpsGenie with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="831fc-105">Integracja z usługą Azure AD OpsGenie zapewnia hello następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="831fc-105">Integrating OpsGenie with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="831fc-106">Można kontrolować w usłudze Azure AD, kto ma dostęp do tooOpsGenie</span><span class="sxs-lookup"><span data-stu-id="831fc-106">You can control in Azure AD who has access tooOpsGenie</span></span>
- <span data-ttu-id="831fc-107">Można włączyć użytkownika użytkownicy tooautomatically get zalogowane tooOpsGenie (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="831fc-107">You can enable your users tooautomatically get signed-on tooOpsGenie (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="831fc-108">Możesz zarządzać kont w jednej centralnej lokalizacji - hello portalu Azure</span><span class="sxs-lookup"><span data-stu-id="831fc-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="831fc-109">Jeśli chcesz tooknow więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="831fc-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="831fc-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="831fc-110">Prerequisites</span></span>

<span data-ttu-id="831fc-111">tooconfigure integracji z usługą Azure AD z OpsGenie należy hello następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="831fc-111">tooconfigure Azure AD integration with OpsGenie, you need hello following items:</span></span>

- <span data-ttu-id="831fc-112">Subskrypcję usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="831fc-112">An Azure AD subscription</span></span>
- <span data-ttu-id="831fc-113">OpsGenie logowanie jednokrotne włączone subskrypcji</span><span class="sxs-lookup"><span data-stu-id="831fc-113">A OpsGenie single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="831fc-114">tootest hello kroków w tym samouczku, zaleca się przy użyciu środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="831fc-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="831fc-115">tootest hello kroki opisane w tym samouczku, należy stosować te zalecenia:</span><span class="sxs-lookup"><span data-stu-id="831fc-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="831fc-116">Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="831fc-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="831fc-117">Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz pobrać miesięczna wersja próbna [tutaj](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="831fc-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="831fc-118">Opis scenariusza</span><span class="sxs-lookup"><span data-stu-id="831fc-118">Scenario description</span></span>
<span data-ttu-id="831fc-119">W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym.</span><span class="sxs-lookup"><span data-stu-id="831fc-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="831fc-120">Scenariusz Hello opisane w tym samouczku składa się z dwóch głównych elementów:</span><span class="sxs-lookup"><span data-stu-id="831fc-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="831fc-121">Dodawanie OpsGenie z galerii hello</span><span class="sxs-lookup"><span data-stu-id="831fc-121">Adding OpsGenie from hello gallery</span></span>
2. <span data-ttu-id="831fc-122">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="831fc-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-opsgenie-from-hello-gallery"></a><span data-ttu-id="831fc-123">Dodawanie OpsGenie z galerii hello</span><span class="sxs-lookup"><span data-stu-id="831fc-123">Adding OpsGenie from hello gallery</span></span>
<span data-ttu-id="831fc-124">tooconfigure hello integracji OpsGenie do usługi Azure AD, należy tooadd OpsGenie z hello galerii tooyour listę zarządzanych aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="831fc-124">tooconfigure hello integration of OpsGenie into Azure AD, you need tooadd OpsGenie from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="831fc-125">**tooadd OpsGenie z galerii hello, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="831fc-125">**tooadd OpsGenie from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="831fc-126">W hello  **[portalu Azure](https://portal.azure.com)**na temat hello panelu nawigacji po lewej stronie, kliknij przycisk **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="831fc-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Usługa Active Directory][1]

2. <span data-ttu-id="831fc-128">Przejdź za**aplikacje dla przedsiębiorstw**.</span><span class="sxs-lookup"><span data-stu-id="831fc-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="831fc-129">Następnie przejdź zbyt**wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="831fc-129">Then go too**All applications**.</span></span>

    ![Aplikacje][2]
    
3. <span data-ttu-id="831fc-131">tooadd nową aplikację, kliknij przycisk **nowej aplikacji** przycisk u góry hello okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="831fc-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplikacje][3]

4. <span data-ttu-id="831fc-133">W polu wyszukiwania hello wpisz **OpsGenie**.</span><span class="sxs-lookup"><span data-stu-id="831fc-133">In hello search box, type **OpsGenie**.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-opsgenie-tutorial/tutorial_opsgenie_search.png)

5. <span data-ttu-id="831fc-135">W panelu wyników hello zaznacz **OpsGenie**, a następnie kliknij przycisk **Dodaj** przycisk aplikacji hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="831fc-135">In hello results panel, select **OpsGenie**, and then click **Add** button tooadd hello application.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-opsgenie-tutorial/tutorial_opsgenie_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="831fc-137">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="831fc-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="831fc-138">W tej sekcji skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z OpsGenie w oparciu o nazwie "Britta Simona" użytkownika testowego.</span><span class="sxs-lookup"><span data-stu-id="831fc-138">In this section, you configure and test Azure AD single sign-on with OpsGenie based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="831fc-139">Dla pojedynczego logowania jednokrotnego toowork usługi Azure AD musi tooknow użytkownika odpowiednikiem hello w OpsGenie jest tooa użytkownika w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="831fc-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in OpsGenie is tooa user in Azure AD.</span></span> <span data-ttu-id="831fc-140">Innymi słowy relację łącza między użytkownika usługi Azure AD i hello użytkownikowi w OpsGenie musi toobe ustanowione.</span><span class="sxs-lookup"><span data-stu-id="831fc-140">In other words, a link relationship between an Azure AD user and hello related user in OpsGenie needs toobe established.</span></span>

<span data-ttu-id="831fc-141">W OpsGenie, należy przypisać wartość hello hello **nazwy użytkownika** w usłudze Azure AD jako wartość hello hello **Username** tooestablish hello łącze relacji.</span><span class="sxs-lookup"><span data-stu-id="831fc-141">In OpsGenie, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="831fc-142">tooconfigure i testowych usługi Azure AD rejestracji jednokrotnej z OpsGenie, należy po bloków konstrukcyjnych hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="831fc-142">tooconfigure and test Azure AD single sign-on with OpsGenie, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="831fc-143">**[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configuring-azure-ad-single-sign-on)**  -tooenable Twojego toouse użytkowników tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="831fc-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="831fc-144">**[Tworzenie użytkownika testowego usługi Azure AD](#creating-an-azure-ad-test-user)**  -tootest usługi Azure AD rejestracji jednokrotnej z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="831fc-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="831fc-145">**[Tworzenie użytkownika testowego OpsGenie](#creating-a-opsgenie-test-user)**  -toohave odpowiednikiem Simona Britta w OpsGenie, który jest połączony toohello usługi Azure AD reprezentację użytkownika.</span><span class="sxs-lookup"><span data-stu-id="831fc-145">**[Creating a OpsGenie test user](#creating-a-opsgenie-test-user)** - toohave a counterpart of Britta Simon in OpsGenie that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="831fc-146">**[Przypisanie użytkownika testowego hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Simona Britta toouse usługi Azure AD rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="831fc-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="831fc-147">**[Testowanie rejestracji jednokrotnej](#testing-single-sign-on)**  -tooverify czy hello konfiguracji działania.</span><span class="sxs-lookup"><span data-stu-id="831fc-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="831fc-148">Konfigurowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="831fc-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="831fc-149">W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w portalu Azure hello i skonfigurować logowanie jednokrotne w aplikacji OpsGenie.</span><span class="sxs-lookup"><span data-stu-id="831fc-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your OpsGenie application.</span></span>

<span data-ttu-id="831fc-150">**tooconfigure usługi Azure AD rejestracji jednokrotnej z OpsGenie, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="831fc-150">**tooconfigure Azure AD single sign-on with OpsGenie, perform hello following steps:**</span></span>

1. <span data-ttu-id="831fc-151">W portalu Azure na powitania hello **OpsGenie** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.</span><span class="sxs-lookup"><span data-stu-id="831fc-151">In hello Azure portal, on hello **OpsGenie** application integration page, click **Single sign-on**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej][4]

2. <span data-ttu-id="831fc-153">Na powitania **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** tooenable rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="831fc-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-opsgenie-tutorial/tutorial_opsgenie_samlbase.png)

3. <span data-ttu-id="831fc-155">Na powitania **OpsGenie domeny i adres URL** sekcji, wykonaj następujące kroki hello:</span><span class="sxs-lookup"><span data-stu-id="831fc-155">On hello **OpsGenie Domain and URLs** section, perform hello following steps:</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-opsgenie-tutorial/tutorial_opsgenie_url.png)

    <span data-ttu-id="831fc-157">W hello **adres URL logowania** pole tekstowe, wprowadź adres URL hello:`https://app.opsgenie.com/auth/login`</span><span class="sxs-lookup"><span data-stu-id="831fc-157">In hello **Sign-on URL** textbox, type hello URL: `https://app.opsgenie.com/auth/login`</span></span>

4. <span data-ttu-id="831fc-158">Na powitania **certyfikat podpisywania SAML** kliknij **Certificate(Base64)** , a następnie zapisz plik certyfikatu hello na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="831fc-158">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-opsgenie-tutorial/tutorial_opsgenie_certificate.png) 

5. <span data-ttu-id="831fc-160">Kliknij przycisk **zapisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="831fc-160">Click **Save** button.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-opsgenie-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="831fc-162">Na powitania **konfiguracji OpsGenie** kliknij **skonfigurować OpsGenie** tooopen **Konfigurowanie logowania jednokrotnego** okna.</span><span class="sxs-lookup"><span data-stu-id="831fc-162">On hello **OpsGenie Configuration** section, click **Configure OpsGenie** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="831fc-163">Kopiuj hello **Sign-Out adres URL, identyfikator jednostki SAML i SAML pojedynczy znak na adres URL usługi** z hello **sekcji krótkimi opisami.**</span><span class="sxs-lookup"><span data-stu-id="831fc-163">Copy hello **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-opsgenie-tutorial/tutorial_opsgenie_configure.png) 

7. <span data-ttu-id="831fc-165">Otwórz inne wystąpienie przeglądarki, a następnie zalogować się w tooOpsGenie jako administrator.</span><span class="sxs-lookup"><span data-stu-id="831fc-165">Open another browser instance, and then log-in tooOpsGenie as an administrator.</span></span>

8. <span data-ttu-id="831fc-166">Kliknij przycisk **ustawienia**, a następnie kliknij przycisk hello **rejestracji jednokrotnej** kartę.</span><span class="sxs-lookup"><span data-stu-id="831fc-166">Click **Settings**, and then click hello **Single Sign On** tab.</span></span>
   
    ![OpsGenie rejestracji jednokrotnej](./media/active-directory-saas-opsgenie-tutorial/tutorial_opsgenie_06.png)

9. <span data-ttu-id="831fc-168">Wybierz tooenable logowania jednokrotnego, **włączone**.</span><span class="sxs-lookup"><span data-stu-id="831fc-168">tooenable SSO, select **Enabled**.</span></span>
   
    ![Ustawienia OpsGenie](./media/active-directory-saas-opsgenie-tutorial/tutorial_opsgenie_07.png) 

10. <span data-ttu-id="831fc-170">W hello **dostawcy** kliknij hello **usługi Azure Active Directory** kartę.</span><span class="sxs-lookup"><span data-stu-id="831fc-170">In hello **Provider** section, click hello **Azure Active Directory** tab.</span></span>
   
    ![Ustawienia OpsGenie](./media/active-directory-saas-opsgenie-tutorial/tutorial_opsgenie_08.png) 

11. <span data-ttu-id="831fc-172">Na stronie okna dialogowego hello Azure Active Directory wykonaj hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="831fc-172">On hello Azure Active Directory dialog page, perform hello following steps:</span></span>
   
    ![Ustawienia OpsGenie](./media/active-directory-saas-opsgenie-tutorial/tutorial_opsgenie_09.png)
    
    <span data-ttu-id="831fc-174">a.</span><span class="sxs-lookup"><span data-stu-id="831fc-174">a.</span></span> <span data-ttu-id="831fc-175">Wklej **pojedynczy znak na adres URL usługi**, która została skopiowana z hello portalu Azure do hello **SAML 2.0 Endpoint** pola tekstowego.</span><span class="sxs-lookup"><span data-stu-id="831fc-175">Paste **Single Sign On Service URL**, which you have copied from hello Azure portal into hello **SAML 2.0 Endpoint** textbox.</span></span>
    
    <span data-ttu-id="831fc-176">b.</span><span class="sxs-lookup"><span data-stu-id="831fc-176">b.</span></span> <span data-ttu-id="831fc-177">Otwórz pobrany zakodowanego certyfikatu base-64 w Notatniku, hello kopiowania zawartości go do Schowka, a następnie wklej go do hello **certyfikatu X.500** pola tekstowego.</span><span class="sxs-lookup"><span data-stu-id="831fc-177">Open your downloaded base-64 encoded certificate in notepad, copy hello content of it into your clipboard, and then paste it into hello **X.500 Certificate** textbox.</span></span>
    
    <span data-ttu-id="831fc-178">c.</span><span class="sxs-lookup"><span data-stu-id="831fc-178">c.</span></span> <span data-ttu-id="831fc-179">Kliknij przycisk **zapisać zmiany**.</span><span class="sxs-lookup"><span data-stu-id="831fc-179">Click **Save Changes**.</span></span>

> [!TIP]
> <span data-ttu-id="831fc-180">Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz hello [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji hello!</span><span class="sxs-lookup"><span data-stu-id="831fc-180">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="831fc-181">Po dodaniu tej aplikacji z hello **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij hello **rejestracji jednokrotnej** hello kartę i dostępu do osadzonych dokumentacji za pośrednictwem hello  **Konfiguracja** sekcji u dołu hello.</span><span class="sxs-lookup"><span data-stu-id="831fc-181">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="831fc-182">Więcej o hello osadzonych dokumentacji funkcji w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="831fc-182">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="831fc-183">Tworzenie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="831fc-183">Creating an Azure AD test user</span></span>
<span data-ttu-id="831fc-184">Celem Hello w tej sekcji jest toocreate użytkownika testowego, w portalu Azure o nazwie Simona Britta hello.</span><span class="sxs-lookup"><span data-stu-id="831fc-184">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Tworzenie użytkowników usługi Azure AD][100]

<span data-ttu-id="831fc-186">**toocreate użytkownika testowego w usłudze Azure AD, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="831fc-186">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="831fc-187">W hello **portalu Azure**na temat hello w lewym okienku nawigacji, kliknij przycisk **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="831fc-187">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-opsgenie-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="831fc-189">toodisplay hello listę użytkowników, przejdź zbyt**użytkowników i grup** i kliknij przycisk **wszyscy użytkownicy**.</span><span class="sxs-lookup"><span data-stu-id="831fc-189">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-opsgenie-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="831fc-191">Witaj tooopen **użytkownika** okna dialogowego, kliknij przycisk **Dodaj** u góry hello hello okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="831fc-191">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-opsgenie-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="831fc-193">Na powitania **użytkownika** okna dialogowego wykonaj hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="831fc-193">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-opsgenie-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="831fc-195">a.</span><span class="sxs-lookup"><span data-stu-id="831fc-195">a.</span></span> <span data-ttu-id="831fc-196">W hello **nazwa** pole tekstowe, typ **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="831fc-196">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="831fc-197">b.</span><span class="sxs-lookup"><span data-stu-id="831fc-197">b.</span></span> <span data-ttu-id="831fc-198">W hello **nazwy użytkownika** pole tekstowe, hello typu **adres e-mail** z BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="831fc-198">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="831fc-199">c.</span><span class="sxs-lookup"><span data-stu-id="831fc-199">c.</span></span> <span data-ttu-id="831fc-200">Wybierz **Pokaż hasło** i zanotuj wartość hello hello **hasło**.</span><span class="sxs-lookup"><span data-stu-id="831fc-200">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="831fc-201">d.</span><span class="sxs-lookup"><span data-stu-id="831fc-201">d.</span></span> <span data-ttu-id="831fc-202">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="831fc-202">Click **Create**.</span></span>
 
### <a name="creating-a-opsgenie-test-user"></a><span data-ttu-id="831fc-203">Tworzenie użytkownika testowego OpsGenie</span><span class="sxs-lookup"><span data-stu-id="831fc-203">Creating a OpsGenie test user</span></span>

<span data-ttu-id="831fc-204">Celem Hello w tej sekcji jest toocreate użytkownika o nazwie Simona Britta w OpsGenie.</span><span class="sxs-lookup"><span data-stu-id="831fc-204">hello objective of this section is toocreate a user called Britta Simon in OpsGenie.</span></span> 

1. <span data-ttu-id="831fc-205">W oknie przeglądarki sieci web Zaloguj się do dzierżawy OpsGenie jako administrator.</span><span class="sxs-lookup"><span data-stu-id="831fc-205">In a web browser window, log into your OpsGenie tenant as an administrator.</span></span>

2. <span data-ttu-id="831fc-206">Przejdź tooUsers listy, klikając **użytkownika** w lewym panelu.</span><span class="sxs-lookup"><span data-stu-id="831fc-206">Navigate tooUsers list by clicking **User** in left panel.</span></span>
   
   ![Ustawienia OpsGenie](./media/active-directory-saas-opsgenie-tutorial/tutorial_opsgenie_10.png) 

3. <span data-ttu-id="831fc-208">Kliknij przycisk **dodać użytkownika**.</span><span class="sxs-lookup"><span data-stu-id="831fc-208">Click **Add User**.</span></span>

4. <span data-ttu-id="831fc-209">Na powitania **Dodaj użytkownika** okna dialogowego, wykonaj następujące kroki hello:</span><span class="sxs-lookup"><span data-stu-id="831fc-209">On hello **Add User** dialog, perform hello following steps:</span></span>
   
   ![Ustawienia OpsGenie](./media/active-directory-saas-opsgenie-tutorial/tutorial_opsgenie_11.png)
   
   <span data-ttu-id="831fc-211">a.</span><span class="sxs-lookup"><span data-stu-id="831fc-211">a.</span></span> <span data-ttu-id="831fc-212">W hello **E-mail** pole tekstowe, adres e-mail hello typu BrittaSimon rozwiązane w usłudze Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="831fc-212">In hello **Email** textbox, type hello email address of BrittaSimon addressed in Azure Active Directory.</span></span>
   
   <span data-ttu-id="831fc-213">b.</span><span class="sxs-lookup"><span data-stu-id="831fc-213">b.</span></span> <span data-ttu-id="831fc-214">W hello **imię i nazwisko** pole tekstowe, typ **Simona Britta**.</span><span class="sxs-lookup"><span data-stu-id="831fc-214">In hello **Full Name** textbox, type **Britta Simon**.</span></span>
   
   <span data-ttu-id="831fc-215">c.</span><span class="sxs-lookup"><span data-stu-id="831fc-215">c.</span></span> <span data-ttu-id="831fc-216">Kliknij pozycję **Zapisz**.</span><span class="sxs-lookup"><span data-stu-id="831fc-216">Click **Save**.</span></span> 

>[!NOTE]
><span data-ttu-id="831fc-217">Britta pobiera wiadomość e-mail z instrukcjami konfigurowania jej profilu.</span><span class="sxs-lookup"><span data-stu-id="831fc-217">Britta gets an email with instructions for setting up her profile.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="831fc-218">Przypisanie użytkownika testowego hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="831fc-218">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="831fc-219">W tej sekcji możesz włączyć toouse Simona Britta Azure logowania jednokrotnego za udzielanie dostępu tooOpsGenie.</span><span class="sxs-lookup"><span data-stu-id="831fc-219">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooOpsGenie.</span></span>

![Przypisz użytkownika][200] 

<span data-ttu-id="831fc-221">**tooassign tooOpsGenie Simona Britta wykonaj hello następujące kroki:**</span><span class="sxs-lookup"><span data-stu-id="831fc-221">**tooassign Britta Simon tooOpsGenie, perform hello following steps:**</span></span>

1. <span data-ttu-id="831fc-222">W portalu Azure hello, otwórz widok aplikacji hello, a następnie przejdź do widoku katalogu toohello i przejść za**aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="831fc-222">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Przypisz użytkownika][201] 

2. <span data-ttu-id="831fc-224">Z listy aplikacji hello wybierz **OpsGenie**.</span><span class="sxs-lookup"><span data-stu-id="831fc-224">In hello applications list, select **OpsGenie**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-opsgenie-tutorial/tutorial_opsgenie_app.png) 

3. <span data-ttu-id="831fc-226">W menu powitania po lewej stronie powitania kliknij **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="831fc-226">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Przypisz użytkownika][202] 

4. <span data-ttu-id="831fc-228">Kliknij przycisk **Dodaj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="831fc-228">Click **Add** button.</span></span> <span data-ttu-id="831fc-229">Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="831fc-229">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Przypisz użytkownika][203]

5. <span data-ttu-id="831fc-231">Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** hello listy użytkowników.</span><span class="sxs-lookup"><span data-stu-id="831fc-231">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="831fc-232">Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="831fc-232">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="831fc-233">Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="831fc-233">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="831fc-234">Testowanie rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="831fc-234">Testing single sign-on</span></span>

<span data-ttu-id="831fc-235">Celem Hello w tej sekcji jest tootest programu Azure AD SSO konfiguracji przy użyciu hello panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="831fc-235">hello objective of this section is tootest your Azure AD SSO configuration using hello Access Panel.</span></span>

<span data-ttu-id="831fc-236">Po kliknięciu kafelka OpsGenie hello w hello Panel dostępu, należy pobrać automatycznie zalogowane tooyour OpsGenie aplikacji.</span><span class="sxs-lookup"><span data-stu-id="831fc-236">When you click hello OpsGenie tile in hello Access Panel, you should get automatically signed-on tooyour OpsGenie application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="831fc-237">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="831fc-237">Additional resources</span></span>

* [<span data-ttu-id="831fc-238">Lista samouczków dotyczących tooIntegrate aplikacji SaaS w usłudze Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="831fc-238">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="831fc-239">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="831fc-239">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-opsgenie-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-opsgenie-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-opsgenie-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-opsgenie-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-opsgenie-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-opsgenie-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-opsgenie-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-opsgenie-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-opsgenie-tutorial/tutorial_general_203.png

