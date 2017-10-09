---
title: 'Samouczek: Integracji Azure Active Directory z Pingboard | Dokumentacja firmy Microsoft'
description: "Dowiedz się, jak tooconfigure logowanie jednokrotne między usługą Azure Active Directory i Pingboard."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 28acce3e-22a0-4a37-8b66-6e518d777350
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/04/2017
ms.author: jeedes
ms.openlocfilehash: 0a916b1f9ef32d8124aa11284d2115bb4fc0bbc5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-pingboard"></a><span data-ttu-id="9b601-103">Samouczek: Integracji Azure Active Directory z Pingboard</span><span class="sxs-lookup"><span data-stu-id="9b601-103">Tutorial: Azure Active Directory integration with Pingboard</span></span>

<span data-ttu-id="9b601-104">Z tego samouczka, dowiesz się, jak toointegrate Pingboard w usłudze Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="9b601-104">In this tutorial, you learn how toointegrate Pingboard with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="9b601-105">Integracja z usługą Azure AD Pingboard zapewnia hello następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="9b601-105">Integrating Pingboard with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="9b601-106">Można kontrolować w usłudze Azure AD, kto ma dostęp do tooPingboard</span><span class="sxs-lookup"><span data-stu-id="9b601-106">You can control in Azure AD who has access tooPingboard</span></span>
- <span data-ttu-id="9b601-107">Można włączyć użytkownika użytkownicy tooautomatically get zalogowane tooPingboard (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="9b601-107">You can enable your users tooautomatically get signed-on tooPingboard (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="9b601-108">Możesz zarządzać kont w jednej centralnej lokalizacji - hello portalu zarządzania Azure</span><span class="sxs-lookup"><span data-stu-id="9b601-108">You can manage your accounts in one central location - hello Azure Management portal</span></span>

<span data-ttu-id="9b601-109">Jeśli chcesz tooknow więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="9b601-109">If you want tooknow more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="9b601-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="9b601-110">Prerequisites</span></span>

<span data-ttu-id="9b601-111">tooconfigure integracji z usługą Azure AD z Pingboard należy hello następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="9b601-111">tooconfigure Azure AD integration with Pingboard, you need hello following items:</span></span>

- <span data-ttu-id="9b601-112">Subskrypcję usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="9b601-112">An Azure AD subscription</span></span>
- <span data-ttu-id="9b601-113">Pingboard jednokrotnego włączone subskrypcji</span><span class="sxs-lookup"><span data-stu-id="9b601-113">A Pingboard single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="9b601-114">tootest hello kroków w tym samouczku, zaleca się przy użyciu środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="9b601-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="9b601-115">tootest hello kroki opisane w tym samouczku, należy stosować te zalecenia:</span><span class="sxs-lookup"><span data-stu-id="9b601-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="9b601-116">Nie należy używać środowiska produkcyjnego, chyba że jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="9b601-116">You should not use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="9b601-117">Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz pobrać miesięczna wersja próbna [tutaj](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="9b601-117">If you don't have an Azure AD trial environment, you can get an one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="9b601-118">Opis scenariusza</span><span class="sxs-lookup"><span data-stu-id="9b601-118">Scenario description</span></span>
<span data-ttu-id="9b601-119">W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym.</span><span class="sxs-lookup"><span data-stu-id="9b601-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="9b601-120">Scenariusz Hello opisane w tym samouczku składa się z dwóch głównych elementów:</span><span class="sxs-lookup"><span data-stu-id="9b601-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="9b601-121">Dodawanie Pingboard z galerii hello</span><span class="sxs-lookup"><span data-stu-id="9b601-121">Adding Pingboard from hello gallery</span></span>
2. <span data-ttu-id="9b601-122">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="9b601-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-pingboard-from-hello-gallery"></a><span data-ttu-id="9b601-123">Dodawanie Pingboard z galerii hello</span><span class="sxs-lookup"><span data-stu-id="9b601-123">Adding Pingboard from hello gallery</span></span>
<span data-ttu-id="9b601-124">tooconfigure hello integracji Pingboard do usługi Azure AD, należy tooadd Pingboard z hello galerii tooyour listę zarządzanych aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="9b601-124">tooconfigure hello integration of Pingboard into Azure AD, you need tooadd Pingboard from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="9b601-125">**tooadd Pingboard z galerii hello, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="9b601-125">**tooadd Pingboard from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="9b601-126">W hello  **[portalu zarządzania Azure](https://portal.azure.com)**na temat hello panelu nawigacji po lewej stronie, kliknij przycisk **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="9b601-126">In hello **[Azure Management Portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Usługa Active Directory][1]

2. <span data-ttu-id="9b601-128">Przejdź za**aplikacje dla przedsiębiorstw**.</span><span class="sxs-lookup"><span data-stu-id="9b601-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="9b601-129">Następnie przejdź zbyt**wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="9b601-129">Then go too**All applications**.</span></span>

    ![Aplikacje][2]
    
3. <span data-ttu-id="9b601-131">Kliknij przycisk **Dodaj** przycisk u góry hello hello okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="9b601-131">Click **Add** button on hello top of hello dialog.</span></span>

    ![Aplikacje][3]

4. <span data-ttu-id="9b601-133">W polu wyszukiwania hello wpisz **Pingboard**.</span><span class="sxs-lookup"><span data-stu-id="9b601-133">In hello search box, type **Pingboard**.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-pingboard-tutorial/tutorial_pingboard_search.png)

5. <span data-ttu-id="9b601-135">W panelu wyników hello zaznacz **Pingboard**, a następnie kliknij przycisk **Dodaj** przycisk aplikacji hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="9b601-135">In hello results panel, select **Pingboard**, and then click **Add** button tooadd hello application.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-pingboard-tutorial/tutorial_pingboard_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="9b601-137">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="9b601-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="9b601-138">W tej sekcji skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z Pingboard w oparciu o nazwie "Britta Simona" użytkownika testowego.</span><span class="sxs-lookup"><span data-stu-id="9b601-138">In this section, you configure and test Azure AD single sign-on with Pingboard based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="9b601-139">Dla pojedynczego logowania jednokrotnego toowork usługi Azure AD musi tooknow użytkownika odpowiednikiem hello w Pingboard jest tooa użytkownika w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="9b601-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Pingboard is tooa user in Azure AD.</span></span> <span data-ttu-id="9b601-140">Innymi słowy relację łącza między użytkownika usługi Azure AD i hello użytkownikowi w Pingboard musi toobe ustanowione.</span><span class="sxs-lookup"><span data-stu-id="9b601-140">In other words, a link relationship between an Azure AD user and hello related user in Pingboard needs toobe established.</span></span>

<span data-ttu-id="9b601-141">Ta relacja łącza zostanie nawiązane, przypisując wartość hello hello **nazwy użytkownika** w usłudze Azure AD jako wartość hello hello **Username** w Pingboard.</span><span class="sxs-lookup"><span data-stu-id="9b601-141">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in Pingboard.</span></span>

<span data-ttu-id="9b601-142">tooconfigure i testowych usługi Azure AD rejestracji jednokrotnej z Pingboard, należy po bloków konstrukcyjnych hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="9b601-142">tooconfigure and test Azure AD single sign-on with Pingboard, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="9b601-143">**[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configuring-azure-ad-single-sign-on)**  -tooenable Twojego toouse użytkowników tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="9b601-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="9b601-144">**[Tworzenie użytkownika testowego usługi Azure AD](#creating-an-azure-ad-test-user)**  -tootest usługi Azure AD rejestracji jednokrotnej z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="9b601-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="9b601-145">**[Tworzenie użytkownika testowego Pingboard](#creating-a-pingboard-test-user)**  -toohave odpowiednikiem Simona Britta w Pingboard, że jego reprezentacja toohello połączonej usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="9b601-145">**[Creating a Pingboard test user](#creating-a-pingboard-test-user)** - toohave a counterpart of Britta Simon in Pingboard that is linked toohello Azure AD representation of her.</span></span>
4. <span data-ttu-id="9b601-146">**[Przypisanie użytkownika testowego hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Simona Britta toouse usługi Azure AD rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="9b601-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="9b601-147">**[Testowanie rejestracji jednokrotnej](#testing-single-sign-on)**  -tooverify czy hello konfiguracji działania.</span><span class="sxs-lookup"><span data-stu-id="9b601-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="9b601-148">Konfigurowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="9b601-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="9b601-149">W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w portalu zarządzania Azure hello i skonfigurować logowanie jednokrotne w aplikacji Pingboard.</span><span class="sxs-lookup"><span data-stu-id="9b601-149">In this section, you enable Azure AD single sign-on in hello Azure Management portal and configure single sign-on in your Pingboard application.</span></span>

<span data-ttu-id="9b601-150">**tooconfigure usługi Azure AD rejestracji jednokrotnej z Pingboard, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="9b601-150">**tooconfigure Azure AD single sign-on with Pingboard, perform hello following steps:**</span></span>

1. <span data-ttu-id="9b601-151">W portalu zarządzania Azure hello na powitania **Pingboard** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.</span><span class="sxs-lookup"><span data-stu-id="9b601-151">In hello Azure Management portal, on hello **Pingboard** application integration page, click **Single sign-on**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej][4]

2. <span data-ttu-id="9b601-153">Na powitania **logowanie jednokrotne** okna dialogowego, jako **tryb** wybierz **na języku SAML logowania jednokrotnego** tooenable logowania jednokrotnego.</span><span class="sxs-lookup"><span data-stu-id="9b601-153">On hello **Single sign-on** dialog, as **Mode** select **SAML-based Sign-on** tooenable single sign on.</span></span>
 
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-pingboard-tutorial/tutorial_pingboard_samlbase.png)

3. <span data-ttu-id="9b601-155">Na powitania **Pingboard domeny i adres URL** sekcji, wykonaj następujące kroki, jeśli chcesz, aby aplikacja hello tooconfigure w hello **IDP** inicjowane tryb:</span><span class="sxs-lookup"><span data-stu-id="9b601-155">On hello **Pingboard Domain and URLs** section, perform hello following steps if you wish tooconfigure hello application in **IDP** initiated mode:</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-pingboard-tutorial/tutorial_pingboard_url.png)

    <span data-ttu-id="9b601-157">a.</span><span class="sxs-lookup"><span data-stu-id="9b601-157">a.</span></span> <span data-ttu-id="9b601-158">W hello **identyfikator** pole tekstowe, wartość hello typu jako:`http://<entity-id>.pingboard.com/sp`</span><span class="sxs-lookup"><span data-stu-id="9b601-158">In hello **Identifier** textbox, type hello value as: `http://<entity-id>.pingboard.com/sp`</span></span>

    <span data-ttu-id="9b601-159">b.</span><span class="sxs-lookup"><span data-stu-id="9b601-159">b.</span></span> <span data-ttu-id="9b601-160">W hello **adres URL odpowiedzi** tekstowym, wpisz adres URL za pomocą hello następującego wzorca:`https://<entity-id>.pingboard.com/auth/saml/consume`</span><span class="sxs-lookup"><span data-stu-id="9b601-160">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://<entity-id>.pingboard.com/auth/saml/consume`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="9b601-161">Należy pamiętać, że nie są one hello wartości rzeczywistych.</span><span class="sxs-lookup"><span data-stu-id="9b601-161">Please note that these are not hello real values.</span></span> <span data-ttu-id="9b601-162">Masz tooupdate tych wartości za pomocą hello rzeczywisty identyfikator i odpowiedzi adresu URL.</span><span class="sxs-lookup"><span data-stu-id="9b601-162">You have tooupdate these values with hello actual Identifier and Reply URL.</span></span> <span data-ttu-id="9b601-163">W tym miejscu zalecamy możesz toouse hello unikatową wartość ciągu w hello identyfikator.</span><span class="sxs-lookup"><span data-stu-id="9b601-163">Here we suggest you toouse hello unique value of string in hello Identifier.</span></span> <span data-ttu-id="9b601-164">Skontaktuj się z [zespołem pomocy technicznej klienta Pingboard](https://support.pingboard.com/) tooget tych wartości.</span><span class="sxs-lookup"><span data-stu-id="9b601-164">Contact [Pingboard Client support team](https://support.pingboard.com/) tooget these values.</span></span> 

4. <span data-ttu-id="9b601-165">Sprawdź **Pokaż zaawansowane ustawienia adresu URL**, jeśli chcesz, aby aplikacja hello tooconfigure w **SP** inicjowane tryb:</span><span class="sxs-lookup"><span data-stu-id="9b601-165">Check **Show advanced URL settings**, if you wish tooconfigure hello application in **SP** initiated mode:</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-pingboard-tutorial/tutorial_pingboard_sp_initiated01.png)

    <span data-ttu-id="9b601-167">a.</span><span class="sxs-lookup"><span data-stu-id="9b601-167">a.</span></span> <span data-ttu-id="9b601-168">W hello **adres URL logowania** pole tekstowe, wartość hello typu jako:`http://<sub-domain>.pingboard.com/sign_in`</span><span class="sxs-lookup"><span data-stu-id="9b601-168">In hello **Sign-on URL** textbox, type hello value as: `http://<sub-domain>.pingboard.com/sign_in`</span></span>
     
5. <span data-ttu-id="9b601-169">Na powitania **certyfikat podpisywania SAML** kliknij **XML metadanych** , a następnie zapisz plik XML hello na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="9b601-169">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello XML file on your computer.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-pingboard-tutorial/tutorial_pingboard_certificate.png) 

6. <span data-ttu-id="9b601-171">Kliknij przycisk **zapisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="9b601-171">Click **Save** button.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-pingboard-tutorial/tutorial_general_400.png)

7. <span data-ttu-id="9b601-173">tooconfigure logowania jednokrotnego po stronie Pingboard, Otwórz nowe okno przeglądarki i zaloguj tooyour Pingboard konta.</span><span class="sxs-lookup"><span data-stu-id="9b601-173">tooconfigure SSO on Pingboard side, open a new browser window and log in tooyour Pingboard Account.</span></span> <span data-ttu-id="9b601-174">Tooset admin Pingboard się funkcji logowania jednokrotnego musi być na.</span><span class="sxs-lookup"><span data-stu-id="9b601-174">You must be a Pingboard admin tooset up single sign on.</span></span>

8. <span data-ttu-id="9b601-175">Wybierz z górnego menu hello **aplikacji > integracji**</span><span class="sxs-lookup"><span data-stu-id="9b601-175">From hello top menu select **Apps > Integrations**</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-pingboard-tutorial/Pingboard_integration.png)

9.  <span data-ttu-id="9b601-177">Na powitania **integracji** pozycję Znajdź hello **"Azure Active Directory"** Kafelek, a następnie kliknij go.</span><span class="sxs-lookup"><span data-stu-id="9b601-177">On hello **Integrations** page, find hello **"Azure Active Directory"** tile, and click it.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-pingboard-tutorial/Pingboard_aad.png)

10. <span data-ttu-id="9b601-179">W hello modalne, kliknij poniżej **"Konfiguruj"**</span><span class="sxs-lookup"><span data-stu-id="9b601-179">In hello modal that follows click **"Configure"**</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-pingboard-tutorial/Pingboard_configure.png)

11. <span data-ttu-id="9b601-181">Na powitania po stronie można zauważyć, że "Integracja z usługą Azure rejestracji Jednokrotnej jest włączona.".</span><span class="sxs-lookup"><span data-stu-id="9b601-181">On hello following page, you will notice that "Azure SSO Integration is enabled.".</span></span> <span data-ttu-id="9b601-182">Otwórz hello pobrany plik XML metadanych w hello Notatnik i Wklej zawartość **metadanych IDP**.</span><span class="sxs-lookup"><span data-stu-id="9b601-182">Open hello downloaded Metadata XML file in a notepad and paste hello content in **IDP Metadata**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-pingboard-tutorial/Pingboard_sso_configure.png)

12. <span data-ttu-id="9b601-184">Plik Hello zostanie zweryfikowany, a jeśli wszystko jest poprawny, logowania jednokrotnego zostanie ono włączone</span><span class="sxs-lookup"><span data-stu-id="9b601-184">hello file will be validated, and if everything is correct, single sign on will now be enabled</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="9b601-185">Tworzenie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="9b601-185">Creating an Azure AD test user</span></span>
<span data-ttu-id="9b601-186">Celem Hello w tej sekcji jest toocreate użytkownika testowego, w portalu zarządzania Azure hello o nazwie Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="9b601-186">hello objective of this section is toocreate a test user in hello Azure Management portal called Britta Simon.</span></span>

![Tworzenie użytkowników usługi Azure AD][100]

<span data-ttu-id="9b601-188">**toocreate użytkownika testowego w usłudze Azure AD, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="9b601-188">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="9b601-189">W hello **portalu zarządzania Azure**na temat hello w lewym okienku nawigacji, kliknij przycisk **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="9b601-189">In hello **Azure Management portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-pingboard-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="9b601-191">Przejdź za**użytkowników i grup** i kliknij przycisk **wszyscy użytkownicy** toodisplay hello listy użytkowników.</span><span class="sxs-lookup"><span data-stu-id="9b601-191">Go too**Users and groups** and click **All users** toodisplay hello list of users.</span></span>
    
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-pingboard-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="9b601-193">U góry okna dialogowego hello powitania kliknij **Dodaj** tooopen hello **użytkownika** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="9b601-193">At hello top of hello dialog click **Add** tooopen hello **User** dialog.</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-pingboard-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="9b601-195">Na powitania **użytkownika** okna dialogowego wykonaj hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="9b601-195">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-pingboard-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="9b601-197">a.</span><span class="sxs-lookup"><span data-stu-id="9b601-197">a.</span></span> <span data-ttu-id="9b601-198">W hello **nazwa** pole tekstowe, typ **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="9b601-198">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="9b601-199">b.</span><span class="sxs-lookup"><span data-stu-id="9b601-199">b.</span></span> <span data-ttu-id="9b601-200">W hello **nazwy użytkownika** pole tekstowe, hello typu **adres e-mail** z BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="9b601-200">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="9b601-201">c.</span><span class="sxs-lookup"><span data-stu-id="9b601-201">c.</span></span> <span data-ttu-id="9b601-202">Wybierz **Pokaż hasło** i zanotuj wartość hello hello **hasło**.</span><span class="sxs-lookup"><span data-stu-id="9b601-202">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="9b601-203">d.</span><span class="sxs-lookup"><span data-stu-id="9b601-203">d.</span></span> <span data-ttu-id="9b601-204">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="9b601-204">Click **Create**.</span></span>
 
### <a name="creating-a-pingboard-test-user"></a><span data-ttu-id="9b601-205">Tworzenie użytkownika testowego Pingboard</span><span class="sxs-lookup"><span data-stu-id="9b601-205">Creating a Pingboard test user</span></span>

<span data-ttu-id="9b601-206">W przypadku użytkowników usługi Azure AD toolog kolejności tooenable do Pingboard muszą mieć przydzielone do Pingboard.</span><span class="sxs-lookup"><span data-stu-id="9b601-206">In order tooenable Azure AD users toolog into Pingboard, they must be provisioned into Pingboard.</span></span>  
<span data-ttu-id="9b601-207">W przypadku hello Pingboard Inicjowanie obsługi to zadanie ręczne.</span><span class="sxs-lookup"><span data-stu-id="9b601-207">In hello case of Pingboard, provisioning is a manual task.</span></span>

<span data-ttu-id="9b601-208">**tooprovision kont użytkowników, wykonaj hello następujące kroki:**</span><span class="sxs-lookup"><span data-stu-id="9b601-208">**tooprovision a user accounts, perform hello following steps:**</span></span>

1. <span data-ttu-id="9b601-209">Zaloguj się za tooyour Pingboard witryny firmy jako administrator.</span><span class="sxs-lookup"><span data-stu-id="9b601-209">Log in tooyour Pingboard company site as an administrator.</span></span>

2. <span data-ttu-id="9b601-210">Kliknij przycisk **"Dodaj pracownika"** znajdującego się na **katalogu** strony.</span><span class="sxs-lookup"><span data-stu-id="9b601-210">Click **“Add Employee”** button on **Directory** page.</span></span>

    ![Dodawanie pracownika](./media/active-directory-saas-pingboard-tutorial/create_testuser_add.png)

3. <span data-ttu-id="9b601-212">Na powitania **"Dodaj pracownika"** okna dialogowego wykonaj następujące kroki hello.</span><span class="sxs-lookup"><span data-stu-id="9b601-212">On hello **“Add Employee”** dialog page, perform hello following steps.</span></span>

    ![Zaproś inne osoby](./media/active-directory-saas-pingboard-tutorial/create_testuser_name.png)

    <span data-ttu-id="9b601-214">a.</span><span class="sxs-lookup"><span data-stu-id="9b601-214">a.</span></span> <span data-ttu-id="9b601-215">W hello **imię i nazwisko** pole tekstowe, hello Pełna nazwa typu Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="9b601-215">In hello **Full Name** textbox, type hello full name of Britta Simon.</span></span>

    <span data-ttu-id="9b601-216">b.</span><span class="sxs-lookup"><span data-stu-id="9b601-216">b.</span></span> <span data-ttu-id="9b601-217">W hello **E-mail** pole tekstowe, adres e-mail hello typu Simona Britta konta.</span><span class="sxs-lookup"><span data-stu-id="9b601-217">In hello **Email** textbox, type hello email address of Britta Simon account.</span></span>

    <span data-ttu-id="9b601-218">c.</span><span class="sxs-lookup"><span data-stu-id="9b601-218">c.</span></span> <span data-ttu-id="9b601-219">W hello **stanowisko** pole tekstowe, typ hello stanowisko Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="9b601-219">In hello **Job Title** textbox, type hello job title of Britta Simon.</span></span>

    <span data-ttu-id="9b601-220">d.</span><span class="sxs-lookup"><span data-stu-id="9b601-220">d.</span></span> <span data-ttu-id="9b601-221">W hello **lokalizacji** listy rozwijanej wybierz hello lokalizację Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="9b601-221">In hello **Location** dropdown, select hello location  of Britta Simon.</span></span>
    
    <span data-ttu-id="9b601-222">e.</span><span class="sxs-lookup"><span data-stu-id="9b601-222">e.</span></span> <span data-ttu-id="9b601-223">Kliknij pozycję **Dodaj**.</span><span class="sxs-lookup"><span data-stu-id="9b601-223">Click **Add**.</span></span>   

4. <span data-ttu-id="9b601-224">Ekran potwierdzenia, zostanie wyświetlone tooconfirm hello dodawania użytkownika.</span><span class="sxs-lookup"><span data-stu-id="9b601-224">A confirmation screen will come up tooconfirm hello addition of user.</span></span>
    
    ![Upewnij się](./media/active-directory-saas-pingboard-tutorial/create_testuser_confirm.png)
        
    > [!NOTE]
    > <span data-ttu-id="9b601-226">właścicielem konta usługi Azure Active Directory Hello będzie otrzymywać wiadomości e-mail i postępuj zgodnie tooconfirm łącze swojego konta przed staje się aktywny.</span><span class="sxs-lookup"><span data-stu-id="9b601-226">hello Azure Active Directory account holder will receive an email and follow a link tooconfirm their account before it becomes active.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="9b601-227">Przypisanie użytkownika testowego hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="9b601-227">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="9b601-228">W tej sekcji możesz włączyć toouse Simona Britta Azure logowania jednokrotnego za udzielanie jej tooPingboard dostępu.</span><span class="sxs-lookup"><span data-stu-id="9b601-228">In this section, you enable Britta Simon toouse Azure single sign-on by granting her access tooPingboard.</span></span>

![Przypisz użytkownika][200] 

<span data-ttu-id="9b601-230">**tooassign tooPingboard Simona Britta wykonaj hello następujące kroki:**</span><span class="sxs-lookup"><span data-stu-id="9b601-230">**tooassign Britta Simon tooPingboard, perform hello following steps:**</span></span>

1. <span data-ttu-id="9b601-231">W portalu zarządzania Azure hello, otwórz widok aplikacji hello, a następnie przejdź widok katalogu toohello i go za**aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="9b601-231">In hello Azure Management portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Przypisz użytkownika][201] 

2. <span data-ttu-id="9b601-233">Z listy aplikacji hello wybierz **Pingboard**.</span><span class="sxs-lookup"><span data-stu-id="9b601-233">In hello applications list, select **Pingboard**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-pingboard-tutorial/tutorial_pingboard_app.png) 

3. <span data-ttu-id="9b601-235">W menu powitania po lewej stronie powitania kliknij **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="9b601-235">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Przypisz użytkownika][202] 

4. <span data-ttu-id="9b601-237">Kliknij przycisk **Dodaj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="9b601-237">Click **Add** button.</span></span> <span data-ttu-id="9b601-238">Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="9b601-238">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Przypisz użytkownika][203]

5. <span data-ttu-id="9b601-240">Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** hello listy użytkowników.</span><span class="sxs-lookup"><span data-stu-id="9b601-240">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="9b601-241">Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="9b601-241">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="9b601-242">Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="9b601-242">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="9b601-243">Testowanie rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="9b601-243">Testing single sign-on</span></span>

<span data-ttu-id="9b601-244">W tej sekcji można przetestować konfiguracji usługi Azure AD pojedynczego logowania jednokrotnego przy użyciu hello panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="9b601-244">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="9b601-245">Po kliknięciu kafelka Pingboard hello w hello Panel dostępu, należy pobrać automatycznie zalogowane tooyour Pingboard aplikacji.</span><span class="sxs-lookup"><span data-stu-id="9b601-245">When you click hello Pingboard tile in hello Access Panel, you should get automatically signed-on tooyour Pingboard application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="9b601-246">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="9b601-246">Additional resources</span></span>

* [<span data-ttu-id="9b601-247">Lista samouczków dotyczących tooIntegrate aplikacji SaaS w usłudze Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="9b601-247">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="9b601-248">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="9b601-248">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-pingboard-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-pingboard-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-pingboard-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-pingboard-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-pingboard-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-pingboard-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-pingboard-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-pingboard-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-pingboard-tutorial/tutorial_general_203.png
