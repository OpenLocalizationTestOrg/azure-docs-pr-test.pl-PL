---
title: 'Samouczek: Integracji Azure Active Directory z LogicMonitor | Dokumentacja firmy Microsoft'
description: "Dowiedz się, jak tooconfigure logowanie jednokrotne między usługą Azure Active Directory i LogicMonitor."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 496156c3-0e22-4492-b36f-2c29c055e087
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/22/2017
ms.author: jeedes
ms.openlocfilehash: ea5cb8b574d763cb114286e3b2a5c94ab5546756
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-logicmonitor"></a><span data-ttu-id="580be-103">Samouczek: Integracji Azure Active Directory z LogicMonitor</span><span class="sxs-lookup"><span data-stu-id="580be-103">Tutorial: Azure Active Directory integration with LogicMonitor</span></span>

<span data-ttu-id="580be-104">Z tego samouczka, dowiesz się, jak toointegrate LogicMonitor w usłudze Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="580be-104">In this tutorial, you learn how toointegrate LogicMonitor with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="580be-105">Integracja z usługą Azure AD LogicMonitor zapewnia hello następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="580be-105">Integrating LogicMonitor with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="580be-106">Można kontrolować w usłudze Azure AD, kto ma dostęp do tooLogicMonitor</span><span class="sxs-lookup"><span data-stu-id="580be-106">You can control in Azure AD who has access tooLogicMonitor</span></span>
- <span data-ttu-id="580be-107">Można włączyć użytkownika użytkownicy tooautomatically get zalogowane tooLogicMonitor (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="580be-107">You can enable your users tooautomatically get signed-on tooLogicMonitor (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="580be-108">Możesz zarządzać kont w jednej centralnej lokalizacji - hello portalu Azure</span><span class="sxs-lookup"><span data-stu-id="580be-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="580be-109">Jeśli chcesz tooknow więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="580be-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="580be-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="580be-110">Prerequisites</span></span>

<span data-ttu-id="580be-111">tooconfigure integracji z usługą Azure AD z LogicMonitor należy hello następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="580be-111">tooconfigure Azure AD integration with LogicMonitor, you need hello following items:</span></span>

- <span data-ttu-id="580be-112">Subskrypcję usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="580be-112">An Azure AD subscription</span></span>
- <span data-ttu-id="580be-113">LogicMonitor logowanie jednokrotne włączone subskrypcji</span><span class="sxs-lookup"><span data-stu-id="580be-113">A LogicMonitor single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="580be-114">tootest hello kroków w tym samouczku, zaleca się przy użyciu środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="580be-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="580be-115">tootest hello kroki opisane w tym samouczku, należy stosować te zalecenia:</span><span class="sxs-lookup"><span data-stu-id="580be-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="580be-116">Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="580be-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="580be-117">Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz pobrać miesięczna wersja próbna [tutaj](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="580be-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="580be-118">Opis scenariusza</span><span class="sxs-lookup"><span data-stu-id="580be-118">Scenario description</span></span>
<span data-ttu-id="580be-119">W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym.</span><span class="sxs-lookup"><span data-stu-id="580be-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="580be-120">Scenariusz Hello opisane w tym samouczku składa się z dwóch głównych elementów:</span><span class="sxs-lookup"><span data-stu-id="580be-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="580be-121">Dodawanie LogicMonitor z galerii hello</span><span class="sxs-lookup"><span data-stu-id="580be-121">Adding LogicMonitor from hello gallery</span></span>
2. <span data-ttu-id="580be-122">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="580be-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-logicmonitor-from-hello-gallery"></a><span data-ttu-id="580be-123">Dodawanie LogicMonitor z galerii hello</span><span class="sxs-lookup"><span data-stu-id="580be-123">Adding LogicMonitor from hello gallery</span></span>
<span data-ttu-id="580be-124">tooconfigure hello integracji LogicMonitor do usługi Azure AD, należy tooadd LogicMonitor z hello galerii tooyour listę zarządzanych aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="580be-124">tooconfigure hello integration of LogicMonitor into Azure AD, you need tooadd LogicMonitor from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="580be-125">**tooadd LogicMonitor z galerii hello, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="580be-125">**tooadd LogicMonitor from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="580be-126">W hello  **[portalu Azure](https://portal.azure.com)**na temat hello panelu nawigacji po lewej stronie, kliknij przycisk **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="580be-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Usługa Active Directory][1]

2. <span data-ttu-id="580be-128">Przejdź za**aplikacje dla przedsiębiorstw**.</span><span class="sxs-lookup"><span data-stu-id="580be-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="580be-129">Następnie przejdź zbyt**wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="580be-129">Then go too**All applications**.</span></span>

    ![Aplikacje][2]
    
3. <span data-ttu-id="580be-131">tooadd nową aplikację, kliknij przycisk **nowej aplikacji** przycisk u góry hello okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="580be-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplikacje][3]

4. <span data-ttu-id="580be-133">W polu wyszukiwania hello wpisz **LogicMonitor**.</span><span class="sxs-lookup"><span data-stu-id="580be-133">In hello search box, type **LogicMonitor**.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-logicmonitor-tutorial/tutorial_logicmonitor_search.png)

5. <span data-ttu-id="580be-135">W panelu wyników hello zaznacz **LogicMonitor**, a następnie kliknij przycisk **Dodaj** przycisk aplikacji hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="580be-135">In hello results panel, select **LogicMonitor**, and then click **Add** button tooadd hello application.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-logicmonitor-tutorial/tutorial_logicmonitor_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="580be-137">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="580be-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="580be-138">W tej sekcji skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z LogicMonitor w oparciu o nazwie "Britta Simona" użytkownika testowego.</span><span class="sxs-lookup"><span data-stu-id="580be-138">In this section, you configure and test Azure AD single sign-on with LogicMonitor based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="580be-139">Dla pojedynczego logowania jednokrotnego toowork usługi Azure AD musi tooknow użytkownika odpowiednikiem hello w LogicMonitor jest tooa użytkownika w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="580be-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in LogicMonitor is tooa user in Azure AD.</span></span> <span data-ttu-id="580be-140">Innymi słowy relację łącza między użytkownika usługi Azure AD i hello użytkownikowi w LogicMonitor musi toobe ustanowione.</span><span class="sxs-lookup"><span data-stu-id="580be-140">In other words, a link relationship between an Azure AD user and hello related user in LogicMonitor needs toobe established.</span></span>

<span data-ttu-id="580be-141">W LogicMonitor, należy przypisać wartość hello hello **nazwy użytkownika** w usłudze Azure AD jako wartość hello hello **Username** tooestablish hello łącze relacji.</span><span class="sxs-lookup"><span data-stu-id="580be-141">In LogicMonitor, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="580be-142">tooconfigure i testowych usługi Azure AD rejestracji jednokrotnej z LogicMonitor, należy po bloków konstrukcyjnych hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="580be-142">tooconfigure and test Azure AD single sign-on with LogicMonitor, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="580be-143">**[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configuring-azure-ad-single-sign-on)**  -tooenable Twojego toouse użytkowników tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="580be-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="580be-144">**[Tworzenie użytkownika testowego usługi Azure AD](#creating-an-azure-ad-test-user)**  -tootest usługi Azure AD rejestracji jednokrotnej z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="580be-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="580be-145">**[Tworzenie użytkownika testowego LogicMonitor](#creating-a-logicmonitor-test-user)**  -toohave odpowiednikiem Simona Britta w LogicMonitor, który jest połączony toohello usługi Azure AD reprezentację użytkownika.</span><span class="sxs-lookup"><span data-stu-id="580be-145">**[Creating a LogicMonitor test user](#creating-a-logicmonitor-test-user)** - toohave a counterpart of Britta Simon in LogicMonitor that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="580be-146">**[Przypisanie użytkownika testowego hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Simona Britta toouse usługi Azure AD rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="580be-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="580be-147">**[Testowanie rejestracji jednokrotnej](#testing-single-sign-on)**  -tooverify czy hello konfiguracji działania.</span><span class="sxs-lookup"><span data-stu-id="580be-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="580be-148">Konfigurowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="580be-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="580be-149">W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w portalu Azure hello i skonfigurować logowanie jednokrotne w aplikacji LogicMonitor.</span><span class="sxs-lookup"><span data-stu-id="580be-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your LogicMonitor application.</span></span>

<span data-ttu-id="580be-150">**tooconfigure usługi Azure AD rejestracji jednokrotnej z LogicMonitor, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="580be-150">**tooconfigure Azure AD single sign-on with LogicMonitor, perform hello following steps:**</span></span>

1. <span data-ttu-id="580be-151">W portalu Azure na powitania hello **LogicMonitor** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.</span><span class="sxs-lookup"><span data-stu-id="580be-151">In hello Azure portal, on hello **LogicMonitor** application integration page, click **Single sign-on**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej][4]

2. <span data-ttu-id="580be-153">Na powitania **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** tooenable rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="580be-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-logicmonitor-tutorial/tutorial_logicmonitor_samlbase.png)

3. <span data-ttu-id="580be-155">Na powitania **LogicMonitor domeny i adres URL** sekcji, wykonaj następujące kroki hello:</span><span class="sxs-lookup"><span data-stu-id="580be-155">On hello **LogicMonitor Domain and URLs** section, perform hello following steps:</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-logicmonitor-tutorial/tutorial_logicmonitor_url.png)

    <span data-ttu-id="580be-157">a.</span><span class="sxs-lookup"><span data-stu-id="580be-157">a.</span></span> <span data-ttu-id="580be-158">W hello **adres URL logowania** tekstowym, wpisz adres URL za pomocą hello następującego wzorca:`https://<companyname>.logicmonitor.com`</span><span class="sxs-lookup"><span data-stu-id="580be-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<companyname>.logicmonitor.com`</span></span>

    <span data-ttu-id="580be-159">b.</span><span class="sxs-lookup"><span data-stu-id="580be-159">b.</span></span> <span data-ttu-id="580be-160">W hello **identyfikator** tekstowym, wpisz adres URL za pomocą hello następującego wzorca:`https://<companyname>.logicmonitor.com`</span><span class="sxs-lookup"><span data-stu-id="580be-160">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<companyname>.logicmonitor.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="580be-161">Wartości te nie są prawdziwe.</span><span class="sxs-lookup"><span data-stu-id="580be-161">These values are not real.</span></span> <span data-ttu-id="580be-162">Zaktualizować te wartości z hello rzeczywisty adres URL logowania i identyfikator.</span><span class="sxs-lookup"><span data-stu-id="580be-162">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="580be-163">Skontaktuj się z [zespołem pomocy technicznej klienta LogicMonitor](https://www.logicmonitor.com/contact/) tooget tych wartości.</span><span class="sxs-lookup"><span data-stu-id="580be-163">Contact [LogicMonitor Client support team](https://www.logicmonitor.com/contact/) tooget these values.</span></span> 
 


4. <span data-ttu-id="580be-164">Na powitania **certyfikat podpisywania SAML** kliknij **XML metadanych** , a następnie zapisz plik metadanych hello na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="580be-164">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-logicmonitor-tutorial/tutorial_logicmonitor_certificate.png) 

5. <span data-ttu-id="580be-166">Kliknij przycisk **zapisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="580be-166">Click **Save** button.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-logicmonitor-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="580be-168">Zaloguj się za tooyour **LogicMonitor** witryny firmy jako administrator.</span><span class="sxs-lookup"><span data-stu-id="580be-168">Log in tooyour **LogicMonitor** company site as an administrator.</span></span>

7. <span data-ttu-id="580be-169">W menu hello na górze hello, kliknij przycisk **ustawienia**.</span><span class="sxs-lookup"><span data-stu-id="580be-169">In hello menu on hello top, click **Settings**.</span></span>
   
   <span data-ttu-id="580be-170">![Ustawienia](./media/active-directory-saas-logicmonitor-tutorial/ic790052.png "ustawienia")</span><span class="sxs-lookup"><span data-stu-id="580be-170">![Settings](./media/active-directory-saas-logicmonitor-tutorial/ic790052.png "Settings")</span></span>

8. <span data-ttu-id="580be-171">W hello bat nawigacji po lewej stronie powitania, kliknij przycisk **rejestracji jednokrotnej**</span><span class="sxs-lookup"><span data-stu-id="580be-171">In hello navigation bat on hello left side, click **Single Sign On**</span></span>
   
   <span data-ttu-id="580be-172">![Logowanie jednokrotne](./media/active-directory-saas-logicmonitor-tutorial/ic790053.png "logowanie jednokrotne")</span><span class="sxs-lookup"><span data-stu-id="580be-172">![Single Sign-On](./media/active-directory-saas-logicmonitor-tutorial/ic790053.png "Single Sign-On")</span></span>

9. <span data-ttu-id="580be-173">W hello **ustawień rejestracji jednokrotnej (SSO)** sekcji, wykonaj następujące kroki hello:</span><span class="sxs-lookup"><span data-stu-id="580be-173">In hello **Single Sign-on (SSO) settings** section, perform hello following steps:</span></span>
   
   <span data-ttu-id="580be-174">![Single Sign-On ustawienia](./media/active-directory-saas-logicmonitor-tutorial/ic790054.png "Single Sign-On ustawienia")</span><span class="sxs-lookup"><span data-stu-id="580be-174">![Single Sign-On Settings](./media/active-directory-saas-logicmonitor-tutorial/ic790054.png "Single Sign-On Settings")</span></span>
   
   <span data-ttu-id="580be-175">a.</span><span class="sxs-lookup"><span data-stu-id="580be-175">a.</span></span> <span data-ttu-id="580be-176">Wybierz **Włącz rejestrację jednokrotną**.</span><span class="sxs-lookup"><span data-stu-id="580be-176">Select **Enable Single Sign-on**.</span></span>

   <span data-ttu-id="580be-177">b.</span><span class="sxs-lookup"><span data-stu-id="580be-177">b.</span></span> <span data-ttu-id="580be-178">Jako **domyślne przypisania roli**, wybierz pozycję **tylko do odczytu**.</span><span class="sxs-lookup"><span data-stu-id="580be-178">As **Default Role Assignment**, select **readonly**.</span></span>
   
   <span data-ttu-id="580be-179">c.</span><span class="sxs-lookup"><span data-stu-id="580be-179">c.</span></span> <span data-ttu-id="580be-180">Otwórz w Notatniku plik metadanych hello pobrane, a następnie wklej zawartość pliku hello na powitania **metadanych dostawcy tożsamości** pola tekstowego.</span><span class="sxs-lookup"><span data-stu-id="580be-180">Open hello downloaded metadata file in notepad, and then paste content of hello file into hello **Identity Provider Metadata** textbox.</span></span>
   
   <span data-ttu-id="580be-181">d.</span><span class="sxs-lookup"><span data-stu-id="580be-181">d.</span></span> <span data-ttu-id="580be-182">Kliknij przycisk **zapisać zmiany**.</span><span class="sxs-lookup"><span data-stu-id="580be-182">Click **Save Changes**.</span></span>

> [!TIP]
> <span data-ttu-id="580be-183">Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz hello [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji hello!</span><span class="sxs-lookup"><span data-stu-id="580be-183">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="580be-184">Po dodaniu tej aplikacji z hello **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij hello **rejestracji jednokrotnej** hello kartę i dostępu do osadzonych dokumentacji za pośrednictwem hello  **Konfiguracja** sekcji u dołu hello.</span><span class="sxs-lookup"><span data-stu-id="580be-184">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="580be-185">Więcej o hello osadzonych dokumentacji funkcji w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="580be-185">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="580be-186">Tworzenie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="580be-186">Creating an Azure AD test user</span></span>
<span data-ttu-id="580be-187">Celem Hello w tej sekcji jest toocreate użytkownika testowego, w portalu Azure o nazwie Simona Britta hello.</span><span class="sxs-lookup"><span data-stu-id="580be-187">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Tworzenie użytkowników usługi Azure AD][100]

<span data-ttu-id="580be-189">**toocreate użytkownika testowego w usłudze Azure AD, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="580be-189">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="580be-190">W hello **portalu Azure**na temat hello w lewym okienku nawigacji, kliknij przycisk **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="580be-190">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-logicmonitor-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="580be-192">toodisplay hello listę użytkowników, przejdź zbyt**użytkowników i grup** i kliknij przycisk **wszyscy użytkownicy**.</span><span class="sxs-lookup"><span data-stu-id="580be-192">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-logicmonitor-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="580be-194">Witaj tooopen **użytkownika** okna dialogowego, kliknij przycisk **Dodaj** u góry hello hello okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="580be-194">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-logicmonitor-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="580be-196">Na powitania **użytkownika** okna dialogowego wykonaj hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="580be-196">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-logicmonitor-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="580be-198">a.</span><span class="sxs-lookup"><span data-stu-id="580be-198">a.</span></span> <span data-ttu-id="580be-199">W hello **nazwa** pole tekstowe, typ **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="580be-199">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="580be-200">b.</span><span class="sxs-lookup"><span data-stu-id="580be-200">b.</span></span> <span data-ttu-id="580be-201">W hello **nazwy użytkownika** pole tekstowe, hello typu **adres e-mail** z BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="580be-201">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="580be-202">c.</span><span class="sxs-lookup"><span data-stu-id="580be-202">c.</span></span> <span data-ttu-id="580be-203">Wybierz **Pokaż hasło** i zanotuj wartość hello hello **hasło**.</span><span class="sxs-lookup"><span data-stu-id="580be-203">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="580be-204">d.</span><span class="sxs-lookup"><span data-stu-id="580be-204">d.</span></span> <span data-ttu-id="580be-205">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="580be-205">Click **Create**.</span></span>
 
### <a name="creating-a-logicmonitor-test-user"></a><span data-ttu-id="580be-206">Tworzenie użytkownika testowego LogicMonitor</span><span class="sxs-lookup"><span data-stu-id="580be-206">Creating a LogicMonitor test user</span></span>

<span data-ttu-id="580be-207">AAD użytkowników toobe stanie toosign w muszą być elastycznie toohello LogicMonitor aplikacji przy użyciu nazwy użytkowników usługi Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="580be-207">For AAD users toobe able toosign in, they must be provisioned toohello LogicMonitor application using their Azure Active Directory user names.</span></span>

<span data-ttu-id="580be-208">**tooconfigure aprowizacji użytkowników, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="580be-208">**tooconfigure user provisioning, perform hello following steps:**</span></span>

1. <span data-ttu-id="580be-209">Zaloguj się za tooyour LogicMonitor witryny firmy jako administrator.</span><span class="sxs-lookup"><span data-stu-id="580be-209">Log in tooyour LogicMonitor company site as an administrator.</span></span>

2. <span data-ttu-id="580be-210">W menu hello na górze hello, kliknij przycisk **ustawienia**, a następnie kliknij przycisk **ról i użytkowników**.</span><span class="sxs-lookup"><span data-stu-id="580be-210">In hello menu on hello top, click **Settings**, and then click **Roles and Users**.</span></span>
   
   <span data-ttu-id="580be-211">![Role i użytkownicy](./media/active-directory-saas-logicmonitor-tutorial/ic790056.png "ról i użytkowników")</span><span class="sxs-lookup"><span data-stu-id="580be-211">![Roles and Users](./media/active-directory-saas-logicmonitor-tutorial/ic790056.png "Roles and Users")</span></span>

3. <span data-ttu-id="580be-212">Kliknij pozycję **Dodaj**.</span><span class="sxs-lookup"><span data-stu-id="580be-212">Click **Add**.</span></span>

4. <span data-ttu-id="580be-213">W hello **Dodaj konto** sekcji, wykonaj następujące kroki hello:</span><span class="sxs-lookup"><span data-stu-id="580be-213">In hello **Add an account** section, perform hello following steps:</span></span>
   
   <span data-ttu-id="580be-214">![Dodaj konto](./media/active-directory-saas-logicmonitor-tutorial/ic790057.png "Dodaj konto")</span><span class="sxs-lookup"><span data-stu-id="580be-214">![Add an account](./media/active-directory-saas-logicmonitor-tutorial/ic790057.png "Add an account")</span></span>
   
   <span data-ttu-id="580be-215">a.</span><span class="sxs-lookup"><span data-stu-id="580be-215">a.</span></span> <span data-ttu-id="580be-216">Typ hello **Username**, **poczty E-mail**, **hasło**, i **wpisz ponownie hasło** wartości hello Azure Active Directory użytkownika ma tooprovision do hello powiązanych pól tekstowych.</span><span class="sxs-lookup"><span data-stu-id="580be-216">Type hello **Username**, **Email**, **Password**, and **Retype password** values of hello Azure Active Directory user you want tooprovision into hello related textboxes.</span></span>
   
   <span data-ttu-id="580be-217">b.</span><span class="sxs-lookup"><span data-stu-id="580be-217">b.</span></span> <span data-ttu-id="580be-218">Wybierz **ról**, **wyświetlanie uprawnień**i hello **stan**.</span><span class="sxs-lookup"><span data-stu-id="580be-218">Select **Roles**, **View Permissions**, and hello **Status**.</span></span>
   
   <span data-ttu-id="580be-219">c.</span><span class="sxs-lookup"><span data-stu-id="580be-219">c.</span></span> <span data-ttu-id="580be-220">Kliknij przycisk **przesłać**.</span><span class="sxs-lookup"><span data-stu-id="580be-220">Click **Submit**.</span></span>

>[!NOTE]
><span data-ttu-id="580be-221">Możesz użyć innych LogicMonitor użytkownika konta tworzenia narzędzi lub interfejsów API dostarczonych przez tooprovision LogicMonitor usługi Azure Active Directory kont użytkowników.</span><span class="sxs-lookup"><span data-stu-id="580be-221">You can use any other LogicMonitor user account creation tools or APIs provided by LogicMonitor tooprovision Azure Active Directory user accounts.</span></span> 

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="580be-222">Przypisanie użytkownika testowego hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="580be-222">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="580be-223">W tej sekcji możesz włączyć toouse Simona Britta Azure logowania jednokrotnego za udzielanie dostępu tooLogicMonitor.</span><span class="sxs-lookup"><span data-stu-id="580be-223">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooLogicMonitor.</span></span>

![Przypisz użytkownika][200] 

<span data-ttu-id="580be-225">**tooassign tooLogicMonitor Simona Britta wykonaj hello następujące kroki:**</span><span class="sxs-lookup"><span data-stu-id="580be-225">**tooassign Britta Simon tooLogicMonitor, perform hello following steps:**</span></span>

1. <span data-ttu-id="580be-226">W portalu Azure hello, otwórz widok aplikacji hello, a następnie przejdź do widoku katalogu toohello i przejść za**aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="580be-226">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Przypisz użytkownika][201] 

2. <span data-ttu-id="580be-228">Z listy aplikacji hello wybierz **LogicMonitor**.</span><span class="sxs-lookup"><span data-stu-id="580be-228">In hello applications list, select **LogicMonitor**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-logicmonitor-tutorial/tutorial_logicmonitor_app.png) 

3. <span data-ttu-id="580be-230">W menu powitania po lewej stronie powitania kliknij **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="580be-230">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Przypisz użytkownika][202] 

4. <span data-ttu-id="580be-232">Kliknij przycisk **Dodaj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="580be-232">Click **Add** button.</span></span> <span data-ttu-id="580be-233">Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="580be-233">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Przypisz użytkownika][203]

5. <span data-ttu-id="580be-235">Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** hello listy użytkowników.</span><span class="sxs-lookup"><span data-stu-id="580be-235">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="580be-236">Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="580be-236">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="580be-237">Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="580be-237">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="580be-238">Testowanie rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="580be-238">Testing single sign-on</span></span>

<span data-ttu-id="580be-239">W tej sekcji można przetestować konfiguracji usługi Azure AD pojedynczego logowania jednokrotnego przy użyciu hello panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="580be-239">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>
 
<span data-ttu-id="580be-240">Po kliknięciu kafelka LogicMonitor hello w hello Panel dostępu, należy pobrać automatycznie zalogowane tooyour LogicMonitor aplikacji.</span><span class="sxs-lookup"><span data-stu-id="580be-240">When you click hello LogicMonitor tile in hello Access Panel, you should get automatically signed-on tooyour LogicMonitor application.</span></span>
<span data-ttu-id="580be-241">Aby uzyskać więcej informacji na temat hello Panel dostępu, zobacz [toohello wprowadzenie panelu dostępu](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="580be-241">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="580be-242">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="580be-242">Additional resources</span></span>

* [<span data-ttu-id="580be-243">Lista samouczków dotyczących tooIntegrate aplikacji SaaS w usłudze Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="580be-243">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="580be-244">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="580be-244">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-logicmonitor-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-logicmonitor-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-logicmonitor-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-logicmonitor-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-logicmonitor-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-logicmonitor-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-logicmonitor-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-logicmonitor-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-logicmonitor-tutorial/tutorial_general_203.png

